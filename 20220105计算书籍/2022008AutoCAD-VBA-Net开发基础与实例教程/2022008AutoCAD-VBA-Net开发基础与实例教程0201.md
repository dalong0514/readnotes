## 0201. 创建和编辑基本图形对象

相信每一位读者在最初学习 AutoCAD 的时候，都是先从创建基本图形对象作为突破口的。同样，在初学 NET 二次开发时，从学习创建基本图形对象开始仍然是您最佳的选择。程序运行后，图形窗口中出现期待的画面，会使您在学习过程中产生很强的成就感，对未来充满信心！

### 2.1 直线

#### 2.1.1 说明

本节程序运行的结果是在 AutoCAD2008 中，创建两条相互垂直的直线。

麻雀虽小，五脏俱全。通过这个程序，你将要开始了解 AutoCAD 数据库的基本结构，掌握各种图形对象的创建方法。

本书所使用的 C# 编程语言，涉及面向对象编程的概念。如果你第一次接触面向对象的编程，则建议可先阅读下面的 MSDN 文档：

[C# 文档 - 入门、教程、参考。 | Microsoft Docs](https://docs.microsoft.com/zh-cn/dotnet/csharp/)

#### 2.1.2 思路

首先，我们要知道。NET 的操作机理是完全不同于 VBA 的，和传统的 ObjectARX 很相似。在写程序之前，大家必须知道以下关于 AutoCAD 数据库的基础知识：

1、表。表是数据库的组成单位，一个数据库至少包含 9 个符号表（块表、层表、文字样式表、线型表、视图表、UCS 表、视口表、注册应用程序表、标注样式表）。

2、记录。记录是表的组成单位，一个表可能包含多条记录，也可能不包含任何记录。图 2.1 用来描述 AutoCAD 数据库的基本结构再好不过。实体包含在块表记录中，要创建一个图形对象，需要遵循下面的基本步骤：

1）得到创建对象的图形数据库。

2）在内存中创建实体类的一个对象。

3）打开图形数据库的块表。

4）打开一个存储实体的块表记录（通常绘图都在模型空间进行），所有模型空间的实体都存储在块表的「模型空间」记录中。

5）将该对象添加到块表记录中。

图 2.1 图形数据库的结构

#### 2.1.3 步骤

1、注册 AutoCAD 命令。

(1) 用第 1 章所学习的方法，新建一个类库项目 Lines，将其解决方案名修改为 Chap02，添加对 acbdmgd.dll 和 acmgd.dll 的引用，将二者的「复制本地」属性改为 False，将 Class1 类更名为 Lines。

2）在 Lines 类中注册一个名为「FirstLine」的命令。在语句 public class Lines 下的大括号内输入：

在输入 CommandMethod 后你会注意到其下方出现红色的波浪线，把鼠标移动到 CommandMethod 上后系统会弹出一行「未找到类型或命名空间的」的提示文本，如图 2.2(a) 所示。通过第 1 章的学习，我们知道应该为 CommandMethod 属性添加相应的命名空间，即在文件的开头加入如下语句：

```cs
using Autodesk.AutoCAD. Runtime;
```

你当然可以手动添加上面的语句，但通过 Visual Studio 2010，可以自动为程序添加相应的命名空间。只要单击 CommandMethod，当出现，图标后单击其右边的下拉按钮，如图 2.2(b) 所示，在弹出的菜单中选择最上部的 using 语句，这样对应的命名空间就被自动添加到文件的开头。

图 2.2 自动添加命名空间

2、绘制直线。

编写绘制直线的实现代码。最后 FirstLine 命令完整的代码如下：

上面代码中的 Database 类属于 Autodesk.AutoCAD.DatabaseServices 命名空间，Point3d 类属于 Autodesk.AutoCAD.Geometry 命名空间，你需要在 Lines 类的开头导入这两个命名空间。

现在，让我们根据本节开始所讲的创建图形对象的步骤来对上面的代码进行分析。




1）获取创建对象的图形数据库。

有两种方法获取图形数据库，一种是直接通过 HostApplicationServices 类的 WorkingDatabase 属性获取，代码如下：

Database db=HostApplicationServices. WorkingDatabase;

第二种方法是先获取当前活动文档，再通过文档获取对应的数据库，代码如下：

Document doc=Application. DocumentManager. MdiActiveDocument;

Database db=doc. Database;

上面添加直线的代码使用第一种方法获取当前图形数据库。

(2) 在内存中创建实体类的一个对象。

在。NET 中，Autodesk. AutoCAD. DatabaseServices 命名空间的 Line 类用来表示直线。直线的构造函数有两种形式，分别为：

public Line ()

public Line (Point3d pointer1, Point3d pointer2)

两个构造函数的名称相同，接受不同的参数，这是 ET 框架所支持的重载特性。重载是面向对象编程的一个重要特性，相同功能的函数采用同样的名称，大大减少了程序员的记忆量。

创建一条直线需要两个参数：起点和终点。第一种重载形式不接受任何参数，创建一条起点和终点都为（0,0,0) 的直线；第二种重载形式则接受直线的起点和终点。如果用第一种方法，则在创建直线后，要设置其起点和终点。一般来说，用第二种形式更方便一些。

提示

不接受任何参数的构造函数一般称为默认构造函数。

在。NET 中，Autodesk. AutoCAD. Geometry 命名空间的 Point3. D 结构表示点的三维坐标；Point22d 结构表示点的二维坐标（创建直线的构造函数需用 Point.3d 结构）。最常用的三维点

坐标的构造函数为：

public Point3d (double x, double y, double z)

(3) 打开图形数据库的块表。

在。NET 中，有关数据库的操作都是通过「事务处理」进行的。语句 Transaction trans=db

TransactionManager. StartTransactionO 表示开始进行事务处理。由于数据库的操作一般消耗较大的内存资源，虽然 C# 通过。NET Framework 公共语言运行库（CLR）自动释放用于存储不再需要的对象的内存，但内存的释放具有不确定性；一旦 CLR 决定执行垃圾回收，就会

释放内存。但是，通常最好尽快释放占用内存较大的资源。

Usig 语句允许程序员指定使用资源的对象应当何时释放内存资源。因此，代码中使用 usig 语句将事务处理的内容用大括号包围起来以释放占用的内存资源。

在内存中创建直线后，在图形窗口中并不能显示出来，只有把直线加到图形数据库中，我们才能看到它。要注意的是，添加图形对象到数据库中，必须先根据需要以「读」或者「写」的方式「打开」块表和块表记录，不然会产生错误！

事务处理 Transaction 类的 GetObject 函数的作用是获取驻留在 AutoCAD 数据库中的对象，因为这些对象是不能直接访问的。GetObject 函数有 3 种重载形式，其中最复杂的一种定义如下：

public virtual Autodesk. AutoCAD. DatabaseServices. DBObject Getobject (

Autodesk. AutoCAD. DatabaseServices. ObjectId id, Autodesk. AutoCAD. Database-

Services. OpenMode mode,

bool openErased, bool forceOpenOnLockedLayer)

其中，id 参数表示要获取对象的 ObjectId，对于块表或层表之类的符号表，它们的 ObjectId 可以通过当前数据库对象的相关属性获得，如块表就是 BlockTableld，层表就是 LayerTableld。在。NET 中，ObjectId 是表示实体对象的一种方式。当一个实体被创建时，AutoCAD 将自动为这个实体分配一个 ObjectId。。但是当 AutoCAD 被关闭时，ObjectId 会被释放掉，因此 ObjectId 不会被保存在 dwg 文件中。当下次打开这个 dwg 文件时，AutoCAD 又会自动为实体重新分配一个 ObjectId。同一个实体，在每次打开 dwg 文件时，ObjectId 都会不同。但在每一次编辑过程中，ObjectId 不会改变。

mode 参数表示打开对象的方式，它是一个 OpenMode 类型的枚举，有三个可取的值，分别为：

> ForRead：对象以读的方式被打开，只要它还没有以写或通知的方式被打开。

> For Write：对象以写的方式被打开，只要它还没有被打开，否则会打开失败。

> ForNotify：当对象被关闭、以读或写的方式被打开，但没有以通知的方式被打开时，

对象可以以通知的方式被打开，关于通知的详细介绍，请参考 ObjectARX SDK。

如果一个 AutoCAD 实体对象刚开始以读的方式被打开，那么你可以用该对象的 UpgradeOpen 函数来把打开状态切换成写。

openErased 参数表示是否获取数据库中已经被删除的对象。

forceOpenOnLockedLayer 参数表示是否强制打开在锁定层上的对象。

GetObject 函数的另外两个形式分别为：只指定 id 和 mode 参数（相当于 openErased= False, forceOpenOnLockedLayer=-false），或者指定 id、mode 及 openErased 参数（相当于 forceOpenOnLockedLayer=-false）。代码中使用的是前一种形式。

由于 GetObject 函数返回的是 DBObject 类对象，而我们要获取的是 BlockTable 类对象，因此需对函数返回的结果进行简单的类型强制转换，即在要转换的值或变量前面的圆括号中指定要强制转换到的类型。但若两者类型不匹配，强制转化具有产生异常的风险，因此 C# 中一般使用 s 和 is 运算符来测试强制转换是否会成功，而没有引发异常的风险。

as 运算符如果可以成功进行强制转换，它会实际返回强制转换值，当转换失败时，as 运算符将产生空，而不是引发异常。下面的代码展示了如何使用 as 运算符将 DBObject 类对象强制转换为 BlockTable 类对象：

DBObject obj=trans. Getobject (db. BlockTableId, OpenMode. ForRead);

BlockTable bt=obj as BlockTable;

if (bt! =null)

// 执行代码

is 运算符与 s 运算符类似，也是检查需要比较的类型是否兼容，但是它不会帮你进行任何的类型转换。所以需要自己进行显示转换。下面的代码展示了如何使用 s 运算符完成上面 as 运算符的转换工作：

BlockTable bt;

DBObject obj=trans. Getobject (db. BlockTableId, OpenMode. ForRead);

if (obj is BlockTable)

bt (BlockTable) obj;

// 执行代码

限于本书的篇幅，本书的代码基本上都使用简单的强制类型转换，读者在实际的程序开

发过程中应尽量使用上面介绍的 s 或 s 运行算符进行强制类型转换。

(4) 打开一个存储实体的块表记录（通常绘图都在模型空间进行）。

启动 AutoCAD 后，其块表中会自动生成三条块表记录，分别表示模型空间和两个布局。它们的名称是：*MODEL SPACE, *PAPER SPACE 和 * PAPER SPACE0。上面代码中，bt [BlockTableRecord.. ModelSpace】的值就是 * MODEL SPACE。模型空间所在的块表记录同样是通过 Transaction 类的 GetObject 函数来获取的，它的 ObjectId 可以通过调用上面获得的块表的索引器来获取，索引器的参数为 BlockTableRecord. ModelSpace.

提示

bt [BlockTableRecord. ModelSpace】在 C# 中称之为索引器，它允许类或结构的实例按 照与数组相同的方式进行访问。有关索引的具体介绍与使用方法请参考下面的 MSDN 文 http://msdn.microsoft.com/zh-cn/library/6x16t2tx (v=VS.100). Aspx

(5) 将对象添加到块表记录中。

在块表记录中加入上面创建的实体对象，并通知事务处理管理器，最后提交事务处理完成实体对象的真正添加。

3. 常用代码的处理

在编写代码时，我们经常会碰到一些重复的代码，如下面的代码是 AutoCAD 二次开发

过程中经常使用的：

// 获取当前活动图形数据库

Database db=HostApplicationServices. WorkingDatabase;

Editor ed=doc. Editor; // 命令行对象

// 开始事务处理

using (Transaction trans=db. TransactionManager. StartTransaction ())

try

trans. Commit (); // 提交事务处理

catch (System. Exception ex)

trans. Abort（）; // 如有异常，则放弃事务处理

对于上面这样常用的代码，可以将其添加到工具箱中，在需要的时候再从工具箱中双击

或拖放到代码窗口中，以减少代码输入工作量。具体操作步骤如下：

(1) 在代码窗口中选中需要的代码。

(2) 按住鼠标按钮不放并移动到工具箱。

(3) 释放鼠标按钮以放下文本，这样代码就被放置在工具箱中了。

(4) 用鼠标右键单击工具箱中的代码标识，在弹出工具箱

的快捷菜单中选择【重命名项】菜单项，为代码标识取

日常规

指针

个容易识别的名字。目 AutoCA 如程序基本框架

图 2.3 显示了工具箱上加入了上面常用的 AutoCAD

图 2.3 常用代码的定义

程序开发代码。

4. 类库封装

为了提高代码的重用性，我们把上面添加实体的代码重新组织一下，封装成一个新的类，

再进行调用。

提示

「封装」是面向对象编程的三大特性之一，意味着将一组相关属性、方法和其他成

员视为一个单元或对象。

新建一个类库项目，项目名和解决方案名均设置为 DotNetARX (读者可以根据自己的爱

好命名），添加对 acbdmgd.dll 和 acmgd. Dll 的引用，将二者的「复制本地」属性改为 False,

将 Class1 类更名为 Tools，并导入 ApplicationServices、DatabaseServices 和 Runtime 命名空间，在 Toos 类中添加如下代码，用于添加实体到文档的模型空间：

public ObjectId AddToModelSpace (Database db, Entity ent)

ObjectId entId; // 用于返回添加到模型空间中的实体 ObjectId

// 定义一个指向当前数据库的事务处理，以添加直线

using (Transaction trans=db. TransactionManager. StartTransaction ())

BlockTable bt= (BlockTable) trans. Getobject (

db. BlockTableId, OpenMode. ForRead); // 以读方式打开块表

// 以写方式打开模型空间块表记录

BlockTableRecord btr= (BlockTableRecord) trans. Getobject (

bt [BlockTableRecord. ModelSpace], OpenMode. Forwrite);

entId=btr. AppendEntity (ent); // 将图形对象的信息添加到块表记录中

trans. AddNewlyCreatedDBObject (ent, true); // 把对象添加到事务处理中

trans. Commit (); // 提交事务处理

return entId; // 返回实体的 ObjectId

这样定义的函数，我们只能通过类似于下面的代码来进行调用：

Tools tool=new Tools ();

tool. AddToModelSpace (db, ent);

其中的第一行代码显然是多余的，我们可以通过为函数定义添加 static 关键字让函数成为静态函数来解决这个问题。在 NET 中，静态函数可以直接通过类型名被引用，上面的代码可以简化成：

Tools. AddToModelSpace (doc, ent);

我们还可以对上面的代码再简化成如下形式：

db. AddToModelSpace (ent);

这就需要在函数定义中除了添加 static 关键字外，还需调用 C# 的扩展方法。扩展方法使您能够向现有类型「添加」方法，而无需创建新的派生类型、重新编译或以其他方式修改原始类型。扩展方法是一种特殊的静态方法，但可以像扩展类型上的实例方法一样进行调用。

实现扩展方法需遵循以下原则：

》定义一个静态类以包含扩展方法。

》将该扩展方法实现为静态方法，并使其至少具有与包含类相同的可见性。

》该方法的第一个参数指定方法所操作的类型；该参数必须以 hs 修饰符开头。

> 在调用代码中，添加一条 using 指令以指定包含扩展方法类的命名空间。》按照与调用类型上的实例方法一样的方式调用扩展方法。因此将 Tools 类及 AddToModelSpace 函数的声明修改成如下代码：

public static class EntTools

public static ObjectId AddToModelSpace (this Database db, Entity ent)

5. 添加 XML 文档注释

在 C# 中，可以为代码创建帮助文档，方法是在代码前添加 XML 文档注释。图 2.4 为一

个由 ML 文档注释生成的帮助文档。

☒DotNetARX5.0 (. ET3.5) 帮助文档口▣X

定位后退前法品鼎

目录 C）素引 D 搜素 S) Collapse All Language Filter: C#I Members I See Alsg

DotNetARX5,0 (. NET3. S）年文

国快速入门 Tools Class

日 CG☑DNA Namespace

HatehPalletteDialog Cl

LinqToARX Class Too 包含皆丰第有用的功能。

e●Tools C1ass

Tools. CoordinateSystem Namespace: DNA

Assembly: DotNetARX (in DotNetARX)

版本：5.0.0.1 (5.0.0.1)

Syntax

Members

All Members Methods◆

XNA Framework

Public Instance Declared Only X

Protected staticS Inherited. NET Compact

Framework Only 目

Member Description

AddEntitie (Entit】

衡数指率亦如一个餐的得号表记柔

adT2urrn 短 Rs 原 ni 标如一个实体到当物图形的港勒空间，

图 2.4XML 注释生成的帮助文档

公提示

从 XML 文档注释生成图 2.4 所示的帮助文档，可以使用免费的 Sandcastle Help File

Builder 软件，软件地址：http:/shfb.codeplex. Com/

下面的代码示例展示了如何为上面的自定义函数 AddToModelSpace 添加 XML 文档

注释。

/// <summary>

/// 将实体添加到模型空间

///</summary>

/// <param name="db"> 数据库对象 </param>

/// <param name="ent"> 要添加的实体《/param>

///,<returns》返回添加到模型空间中的实体 ObjectId</returns>.

public static objectId AddToModelSpace (this Database db, Entity ent)

」提示

在 Visual Studio 代码窗口中输入「/W」符号，Visual Studio 会自动为你生成 XML 文档注释框架，你只要填写有关的函数、参数及返回值的说明即可。关于 XML 文档注释的详细介绍请参考以下的 MSDN 文档：http:/msdn.microsoft.com/zh-cn/1 ibrary/b2s063f7 (v=VS.100). Aspx

要生成 XML 文档文件，你必须按以下步骤进行设置（见图 2.5）：

应用程序

配置 C）：活动①ebug）平台）：活动 Any CPU)

生成 *

生成事件

条件偏译符号）：

☑定义 DEBVG 常量）

调试

☑定义 TRACE 常量 T)

资源

目标平台 G): Any CPU

服务

☐允许不安全代码您）

☐忧化代码 2)

设置

错误和髻告

引用路径

警告等级）：

签名禁止显示警告⑤)

代码分析

将警告视为错误

⊙无）

O 全部 L)

○特定警告）

输出一

输出路径 Q): bin\Debug\ 浏览⑧)..

可 XL 文档文件《）：bin\Debug\DotNetARX.XM

口为 CON 互操作注册 C)

生成序列化程序集）：自动

高级四）.

图 2.5 添加 XML 文件注释支持

(1) 在解决方案资源管理器中，用鼠标右键单击 DotNetARX 项目并单击「属性」。（2) 在「配置属性」窗口单击「生成」选项卡。 (3) 勾选「XML 文档文件」属性。

(4) 编译程序，DotNetARX. XML 文件将出现在生成目录中。

6. 调用自定义函数

编译 DotNetARX 类库项目，生成 DotNetARX. Dll, 我们就可以像引用其他。NET 类库一样对它进行引用。

打开前面添加直线的类库项目，添加对 DotNetARX. Dll 的引用，在 Class1 类中再注册一个命令 SecondLine，用于调用自定义函数绘制一条直线，代码如下：

[CommandMethod ("SecondLine")]

public static void SecondLine ()

Database db=HostApplicationServices. WorkingDatabase;

Point3d startPoint=new Point3d (0,100,0);

Point3d endPoint=new Point3d (0,200,0);

Lineline=new Line (startPoint, endpoint);

db. AddToModelSpace (line);

当你输入最后一行代码的 db 变量后的点号时，Visual Studio 会出现如图 2.6 所示的智能

提示列表，从图中可以看到上面定义的 Database 类的 AddToModelSpace 扩展函数，并且还有 XML 注释的帮助内容。

db. A

AddShapeTextStyle

AddTableStyle

年 AddTextStyle

AddToCurrentSpace

AddToModelSpace 由展名）ObjectIdCollection Database. AddToModelSpace

AddToPaperSpace 将实体添加到模型空间

◆Adducs

AllowExtendedNames

Angbase L

图 2.6 智能提示自定义的帮助内容

AddToModelSpace 前面的：图标表示扩展方法。

2.1.4 效果

编译程序，启动 AutoCAD2008, 用 NetLoad 命令加载生成的 DLL 文件，执行 FirstLine 和 SecondLine 命令，在图形窗口中绘制出两条互相垂直的直线，如图 2.7 所示。

AutoCAD 2008 [Drawing1. Dvg】口回☒

文件）编辑）视图）插入）格式 Q）工具红）绘图血）标注 D

修改 M）窗口）帮助 0 Express

□日品乡 6 日 6 白￡·8Q@欧

AutoCAD 经典～网渐多 9Q 色口 0

8

心

㗊

O

3

《模型人布局 1 人布局 2/

命令：* 取消 *

命令：* 取消

命令：

-81.2285,246.1295,0.0000 捕捉姗格正交极轴对象捕捉对了、回鼎

图 2.7 创建直线的结果

2.1.5 小结

如果你认真手工输入了本节的代码，一定会感到很烦琐。的确，作为程序员一定要善于

利用集成开发环境所提供的功能。你可能已经注意到在 Visual Studio 中编写 C# 代码时，当输入某个关键字的第一个字母后，代码编辑器就会弹出如图 2.8 (a）所示的代码提示列表，你可以输入更多的字母来缩小列表中的单词范围，如列表光标已经指向你所需要的关键字，则按非字母键就可以完成关键字的输入。这个功能是 Visual Studio2010 中提供的智能感知（IntelliSense），它可以大大减轻。NET 程序员的代码输入量，使应用程序的开发工作变得更加轻松，并且有助于避免在编写代码时出现输入错误。

Documert doc=A Locwent doc=Application.

AppDomainManagerInitializationOptions 号 BeginQuit

化 AppDomainSetup

DisplayingCustomizeDialog

AppDomainUnloadedException DisplayingDraftingSettingsDialog

Append 证 ntity DisplayingOptionDialog

Application 子 DocumentManager

ApplicationException DoDragDrop

ApplicationId ◆Equals

ApplicationIdentity ◆GetSystemVariable

ApplicationLoadReasons InfoCenter

(a) (b)

图 2.8 Visual Studio2010 强大的智能感知

智能感知在 Visual Studio2010 中无处不在，除了上面的关键字自动提示外，我们再来看本节可以使用的另一项智能感知功能：

当你在变量后输入点号后，智能感知就会显示定义该变量的类所拥有的成员列表，如你输入表示 AutoCAD 应用程序的 Application 变量后，将出现如图 2.8 (b）所示的 Application 类成员列表。

学习本节后，应该掌握以下内容：

》理解 NET 中创建图形对象的基本机理。

》掌握直线对象的构造函数。

》获取块表、块表记录的方法。

> NET 类库的封装。

》自动添加命名空间。

> Visual Studio 智能感知对编程工作的简化。

> C# 扩展函数的使用。

> C#XML 注释的使用。

2.2 编辑图形对象

2.2.1 说明

前面一节我们学习了如何创建直线，本节将介绍对生成的直线进行编辑操作，包括如何修改直线的属性（如颜色、层号等）及对直线进行变换操作（如复制、移动、旋转、镜像等）。

2.2.2 思路

1. 使用事务处理打开和关闭对象

当你需要访问实体对象如直线时，必须首先以读或写的方式打开它（对象创建时也会以写的方式被打开）。

在 NET 中，ObjectId 是表示实体对象的最常用的一种方式。当一个实体被创建时，AutoCAD 图形数据库将自动为这个实体分配一个 ObjectId。因此在创建对象时，可以将该对象的 ObjectId 保存起来，在需要访问该对象时，再根据这个 ObjectId 打开其表示的实体对象，就可以修改或查询该对象的特性。

通过前面一节的学习，我们知道获取实体的 ObjectId 后，可以通过 Transaction（事务处理）类的 GetObject 函数打开 ObjectId 表示的实体对象来进行操作，因为这些对象是不能直接访问的。

事务处理对于读 / 写对象是安全的，因为在事务处理中打开的对象会在其退出时自动关 闭，但其代价是读 / 写时间会有所加长，因此你可以使用 ObjectId 的 Open 函数和 Entity 的 Close 函数来打开和关闭实体，这种处理方式类似于 C + 的编程方法。当你使用 Ope 函数打开对象并进行编辑后，可以使用 Cancel 函数撤销这些编辑操作。

父注意

当你使用 Open 函数打开一个对象后，在访问对象结束后要及时使用 Close 或 Cancel 函数，不然会导致 AutoCAD 变得不稳定。

由于 NET 中推荐使用事务处理来进行对象的操作，因此 Open、Close 和 Cancel 函数在 NET 中被标记为不建议使用。在 C# 中，不建议使用的项会用 Obsolete 特性说明，如 Open 函数被标记为不建议使用，并且给出了替代的办法：

[Obsolete ("For advanced use only.Use Getobject instead")]

public DBObject Open (OpenMode mode);

由于 Open、Close 和 Cancel 函数被标记为不建议使用，因此当你编写带这些函数的程序时，Visual Studio 会在这些函数下用绿色的波浪线对你进行提示并且编译时会有产生警告。

在事务处理中不要使用 Open、Close 和 Cancel 函数，这样可能导致对象无法被事务处理管理器正确地打开或关闭，进而可能会造成 AutoCAD 的崩溃！

从 AutoCAD2009 版本开始，NET 用一个新的类 OpenCloseTransaction 来解决 Transaction 速度慢和 Open 等函数不安全的问题，它封装了 ObjectId.Open/Close 函数的功能，并且可以与使用事务处理一样不用担心对象的关闭问题。OpenCloseTransaction 类的使用方法与 Transaction 类是完全一样的。

让我们看一下上面介绍的各种方法读 / 写对象所需要的时间，图 2.9 展示了不同方法读 / 写 AutoCAD 中 100000 个点所需要的时间。

从图 2.9 可以看出，对于读取操作，ObjectId.Open 函数效率最高，其读取时间只有最慢的 ObjectId. GetObject 的一半左右，而其他两个函数与 ObjectId.Open 读取时间基本上相近。对于写入操作，Transaction. GetObject 的效率最低，其写入时间超过最快的 OpenCloseTransaction.GetObject 的两倍还多。因此综合读 / 写能力，OpenCloseTransaction 是效率最高的，且拥有与 Transaction 一样安全的对象管理机制，建议读者在读 / 写实体对象时，尽量使用 OpenCloseTransaction。

2. 事务处理的提交、撤销与嵌套

在事务处理中改变对象状态后，你可以使用 Commit 函数保存这种改变。但如果改变过程中发生异常，那么你可以使用 Abot 函数撤销事务处理中所做的任何改变。由于 Abot 函数一般用于处理程序异常，因此可以把对 Abort 的调用放到异常处理的 catch 块中：

using (Transaction trans=db. TransactionManager. StartTransaction ())

try

{

trans. Commit (); // 提交事务处理，保存改变

}

catch

trans. Abort (); // 如有异常，则撤销改变

事务处理中还可以嵌套另外的事务处理。当你在一个事务处理中新建另外的事务处理时，这些新建的事务处理就会被添加到先前的事务处理中。需要注意的是，嵌套的事务处理提交或撤销的顺序与创建时的完全相反。比如你定义了三个事务处理，那么你在第二个事务处理之前必须首先提交第三个也就是最里面的事务处理。如果你撤销了最外层的事务处理，那么所有的事务处理中所做的改变均被撤销。图 2.10 展示了三个事务处理的嵌套关系。

可以使用 TransactionManager 类的 Num-berOfActiveTransactions 属性获取当前活动的事务处理数目，要获取最外层的事务处理则可以使用 TopTransaction 属性。

3. ObjectId 和句柄（Handle)

除了 ObjectId 外，AutoCAD 还为数据库对象分配了句柄和对象指针。其中对象指针的概念与 C++ 有关，这里就不进行详细介绍了。

句柄是 Windows 编程中一个常用的概念，在 AutoCAD.NET 编程中一般指 Handle 类，该类封装了一个 64 位的整型标识符，随 DWG 文件一起保存。

ObjectId 和句柄各有特点。

> ObjectId：在一个 AutoCAD 任务中，可能加载多个图形数据库，但是所有对象的

ObjectId 在本次任务中是独一无二的。在不同的 AutoCAD 任务中，同一个图形对象的 ObjectId 可能不同。

》句柄：在一个 AutoCAD 任务中，不能保证每个对象的句柄都唯一，但是在一个图形

数据库中所有对象的句都是唯一的。句柄随 DWG 图形一起保存，在两次任务期间同一对象的句柄是相同的。

ObjectId 和句柄之间可以相互转换，Database. GetObjectId 函数可以，而 ObjectId 类的 Handle 属性则可以通过对象的 ObjectId 获取对应的句柄。

4. 改变对象的读 / 写状态

当使用 GetObject 或 Open 函数打开对象后，你可以使用对象的 UpgradeOpen 或 DowngradeOpen 函数改变对象的打开状态。UpgradeOpen 函数将对象由只读的状态升级为可写的状态，而 DowngradeOpen 函数则将对象由可写的状态降级为只读。当你使用 UpgradeOpen 或 DowngradeOpen 函数进行状态切换后，无需再次调用相关的函数恢复对象的原始状态，因为关闭一个对象或结束事务处理后，对象的打开状态会被清除。

提

如果你只需要访问对象的属性，那么请尽量使用读的方式打开对象。虽然以写的方式也能访问对象的属性，但其效率远比读的方式低。

5. 实体的几何变换

通过上面打开实体的方法，可以对实体的属性进行读 / 写，但如果你需要对实体进行诸如移动、旋转、镜像之类的几何变换的话，就得使用 Entity 类的 TransformBy 函数了。TransformBy 函数的定义如下：

public virtual void TransformBy (Matrix3d transform);

所有 Entity 的派生类都实现了这个虚拟函数，因此所有的实体都可以使用此函数进行几

何变换。

transform 参数的类型是 Matrix3d，它是一个位于 Geometry 命名空间的几何类，用于表示一个四维变换矩阵，其基本形式如图 2.11 所示。

尽管可以像普通的矩阵那样修改变换矩阵中的元素，但是多种变换叠加的矩阵参数计算起来非常麻烦，所幸 Matrix3d 类提供了一些很有用的静态函数来帮你完成常用的几何变换。

> Translation：生成移动对象矩阵。

> Rotation：生成旋转矩。

> Scaling：生成比例缩放矩。

Mirroring：生成镜像矩。

2.2.3 步骤

(1) 首先打开 2.2.2 节创建的 DotNetARX 基本类库解决方案，添加一个新的类，命名为

EntTools，。导入 ApplicationServices、DatabaseServices 和 Geometry 命名空间，为了支持扩展函数，将 EntTools 类的声明修改如下：

public static class EntTools

在 EntTools 类中添加一个 Move 扩展函数，使用 TransformBy 函数对实体进行移动，代码如下（id 参数表示实体的 ObjectId, sourcePt 表示移动的源点，targetPt 表示移动的目标点）：

public static void Move (this ObjectId id, Point3d sourcept, Point3d targetpt)

// 构建用于移动实体的矩阵

Vector3d vector=targetpt. GetVectorTo (sourcept);

Matrix3d mt Matrix3d. Displacement (vector);

// 以写的方式打开 id 表示的实体对象

Entity ent (Entity) id. Getobject (OpenMode. ForWrite);

ent. TransformBy (mt); // 对实体实施移动

ent. DowngradeOpen (); // 为防止错误，切换实体为读的状态

要移动对象，可以使用 Matrix.3d 结构的静态函数 Displacement，其定义如下：

public static Matrix3d Displacement (Vector3d vector);

其中，vector 参数是一个 Vector.3d 结构的变量，表示移动向量，它指示一个给定的对象在什么方向要移动多远的距离。代码中使用 Point3d 结构的 Get VectorTo 函数返回两个点之间的方向矢量。

通过对象的 ObjectId 获取实体对象，一般是通过事务处理的 GetObject 函数进行的，但上面代码中未使用事务处理，而是直接使用 ObjectId 的 GetObject 函数。该函数实现的功能与事务处理的 GetObject 函数一样，但它可以防止形成嵌套事务处理从而提升代码的执行效率。

该函数有 3 种重载形式，其中最复杂的一种定义如下：

Public DBObject Getobject (

OpenMode mode, bool openErased, bool forceOpenOnLockedLayer);

其中，mode 参数表示打开对象的方式，openErased 参数表示是否获取数据库中已经被删除的对象，forceOpenOnLockedLayer 参数表示是否强制打开在锁定层上的对象。以上参数的具体说明，可参考上一节事务处理的 GetObject 函数。

需要注意的是，ObjectId 的 GetObject 函数必须保证 ObjectId 所在的数据库开启了事务处

理，否则会造成 AutoCAD 的崩溃。

签餐告

图形对象必须是在写的状态下才能进行平移，其他编辑操作也是这样。

(2) 重载 Move 函数，同样用于移动命令，代码如下（ent 参数表示需要移动的实体，sourcePt

表示移动的源点，targetPt 表示移动的目标点）：

public static void Move (this Entity ent, Point3d sourcept, Point3d targetpt)

if (ent. IsNewobject) // 如果是还未被添加到数据库中的新实体

// 构建用于移动实体的矩阵

Vector3d vector=targetpt. GetvectorTo (sourcept);

Matrix3d mt Matrix3d. Displacement (vector);

ent. TransformBy (mt); // 对实体实施移动

e1se// 如果是已经添加到数据库中的实体

ent.ObjectId. Move (sourcept, targetpt);

该重载函数直接将实体作为输入参数，其中对于还未被添加到数据库中的实体，由于实体本身处于打开状态，因此可以直接对实体进行移动。而对于已经添加到数据库中的实体，则调用步骤 1 中定义的函数对实体进行移动。

判断实体是否被添加到数据库中，可以通过 Entity 类的 IsNewObject 属性实现。

x 提示

对于下面编辑实体的函数，限于篇幅，这里只给出使用 ObjectId 作为输入参数的函数定义，对于使用 Entity 作为输入参数的函数则可参阅配书光盘。

(3) 添加一个 Copy 函数，用于复制命令，代码如下（id 参数表示实体的 ObjectId, sourcePt

表示复制的源点，targetPt 表示复制的目标点）：

public static ObjectId Copy (this ObjectId id, Point3d sourcept, Point3d targetpt)

// 构建用于复制实体的矩阵

Vector3d vector=targetpt. GetVectorTo (sourcePt); Matrix3d mt Matrix3d. Displacement (vector); // 获取 id 表示的实体对象

Entity ent (Entity) id. Getobject (OpenMode. ForRead);

Entity entCopy=ent. GetTransformedCopy (mt); // 获取实体的复制件 // 将复制的实体对象添加到模型空间

ObjectId copyId=id. Database. AddToModelSpace (entCopy);

return copyId; // 返回复制实体的 ObjectId

实体的 GetTransformedCopy 函数能得到复制的图形对象，要注意的是，该对象并没有加

入到图形数据库中，因此调用 DotNetARX 类库中的 AddToModelSpace 将其加入到图形数据库的模型空间中。

(4) 添加 Rotate 函数，用于旋转命令，代码如下（id 参数表示实体的 ObjectId, basePt 表示旋转基点，angle 表示旋转角度）：

public static void Rotate (this ObjectId id, Point3d basept, double angle)

Matrix3d mt Matrix3d. Rotation (angle, Vector3d. ZAxis, basept);

Entity ent (Entity) id. Getobject (OpenMode. Forwrite);

ent. TransformBy (mt);

ent. Downgradeopen ()

Matrix3d 类的静态函数 Rotation 得到一旋转矩阵，用于旋转操作，它的定义如下：

public static Matrix3d Rotation (double angle, Vector3d axis, Point3d center);

其中，angle 参数表示旋转的角度，axis 表示旋转轴，center 表示旋转中心。

(5) 添加 Scale 函数，用于缩放命令，代码如下（id 参数表示实体的 ObjectId, basePt

表示缩放基点，scaleFactor 表示缩放比例）：

public static void Scale (this ObjectId id, Point3d basept, double scaleFactor)

Matrix3d mt Matrix3d. Scaling (scaleFactor, basept);

Entity ent (Entity) id. Getobject (OpenMode. Forwrite);

ent. TransformBy (mt);

ent. Downgradeopen ()

Matrix:3d 类的静态函数 Scaling 返回一个缩放矩阵，用于缩放操作，它的定义如下：public static Matrix3d Scaling (double scaleAll, Point3d center）；其中，scaleAll 表示缩放比例，center 表示缩放中心。

(6) 添加 Mirror 函数，用于镜像命令，代码如下（id 参数表示实体的 ObjectId, mirrorPtl、mirrorPt2 分别表示镜像轴的第一点和第二点，eraseSourceObject 表示是否删除源对象）：

publicstaticObjectIdMirror (thisObjectIdid, Point3dmirrorPt1, Point3dmirrorpt2, bool eraseSourceObject)

Line3 d miLine=new Line3d (mirrorPt1, mirrorPt2); // 镜像线

Matrix3dmt=Matrix3d. Mirroring (miLine); // 镜像矩阵

ObjectId mirrorId=id;

Entity ent (Entity) id. Getobject (OpenMode. ForWrite);

// 如果删除源对象，则直接对源对象实行镜像变换

if (eraseSourceObject =true)

ent. TransformBy (mt);

else// 如果不删除源对象，则镜像复制源对象

Entity entCopy ent. GetTransformedCopy (mt);

mirrorId=id. Database. AddToModelSpace (entCopy);

return mirrorId;

}

对于镜像，先定义几何类的镜像线，得到镜像矩阵，再进行镜像变换（删除源对象时）或镜像复制（不删除源对象时）。

Matrix.3d 类的静态函数 Mirroring 返回一个镜像矩阵，用于镜像操作，它的定义如下：

public static Matrix3d Mirroring (Line3d line);

其中，输入参数 line 为 Geometry 命名空间的 Line3d 类，表示镜像线。

(7) 添加 Offset 函数，用于偏移命令，代码如下（id 参数表示实体的 ObjectId, dis 表示偏移距离）：

public static ObjectIdCollection offset (this ObjectId id, double dis)

ObjectIdCollection ids=new objectIdCollection ();

Curve cur id. Getobject (OpenMode. Forwrite) as Curve;

if (cur！=nu11)

try

// 获取偏移的对象集合

DBObjectCollection offsetCurves cur. GetoffsetCurves (dis);

// 将对象集合类型转换为实体类的数组，以方便加入实体的操作

Entity [] offsetEnts=new Entity [offsetCurves. Count];

offsetCurves. CopyTo (offsetEnts,0);

// 将偏移的对象加入到数据库

Ids id. Database. AddToModelSpace (offsetEnts);

catch// 如果偏移出现异常 f

Application. ShowAlertDialog（「无法偏移！「）；

else// 如果不是曲线

Application. ShowAlertDia1og（「无法偏移！「）；return ids; // 返回偏移后的实体 Id 集合

偏移操作首先要判断所选对象是否为曲线（Cuve），如果不是则在命令行提示用户并退

出。偏移操作和其他编辑命令不同，不是用矩阵的方法，而是用 Curve 类的 GetOffsetCurves

函数得到一个对象集合（一个对象偏移可能会生成多个对象），再用 DotNetARX 类库中的

AddToModelSpace 自定义函数将其添加到图形数据库中。要注意的是，这个 AddToModelSpace 函数与 2.2.2 节介绍的不一样，它可以接受实体数组或多个实体，其定义如下：

public static ObjectIdCollection AddToModelSpace (this Database db, params Entity [] ents)

其中，db 参数表示数据库；ents 参数表示要添加到模型空间的多个实体，该参数是一个可变参数，你可以为其赋值实体数组，也可以这样添加多个实体到模型空间：

db. AddToModelSpace (1ine, circle…）；

(8) 添加 ArrayRectang 函数，用于矩形阵列命令，代码如下（id 参数表示实体的 ObjectId:

numRows、numCols 分别表示矩形阵列的行数和列数，必须为正数；disRows、disCols 分别表示行间的距离和列间的距离）：

public static ObjectIdCollection ArrayRectang (this ObjectId id, int numRows, int numCols, double disRows, double disCols)

// 用于返回阵列后的实体集合的 ObjectId

ObjectIdCollection ids=new ObjectIdCollection ();

Entity ent= (Entity) id. GetObject (OpenMode, ForRead); // 以读的方式打开实体 for (int m =0; m numRows; m++)

for (int n 0; n numCols; n++)

// 获取平移矩阵

Matrix3dmt Matrix3d. Displacement (new Vector3d (n disCols, m disRows,0));

Entity entCopy=ent. GetTransformedCopy (mt); // 复制实体

// 将复制的实体添加到模型空间

ObjectId entCopyId=id. Database. AddToModelSpace (entCopy);

ids.Add (entCopyId); // 将复制实体的 ObjectId 添加到集合中

ent. UpgradeOpen (); // 切换实体为写的状态 ent. Erase (); // 删除实体

return ids; // 返回阵列后的实体集合的 ObjectId

矩形阵列实质上就是多重复制，因此只要计算出相应的矩阵即可用复制的方法实现矩形阵列。

(9) 添加 ArrayPolar 函数，用于环形阵列命令，代码如下（id 参数表示实体的 ObjectId; cenPt 表示环形阵列的中心点；numObi 表示在环形阵列中所要创建的对象数量；angle 是以弧度表示的填充角度，正值表示逆时针方向旋转，负值表示顺时针方向旋转，如果角度为 0 则出错）：

public static ObjectIdCollection ArrayPolar (

this ObjectId id, Point3d cenpt, int numobj, double angle)

ObjectIdCollection ids=new ObjectIdCollection ();

Entity ent (Entity) id. Getobject (OpenMode. ForRead);

for (int i 0; i <numObj -1; i++)

Matrix3dmt =Matrix3d. Rotation (angle *(i+1)/numobj,Vector3d.ZAxis, cenpt);

Entity entCopy ent. GetTransformedCopy (mt);

ObjectId entCopyId=id. Database. AddToModelSpace (entCopy);

ids. Add (entCopyId);

return ids;

环形阵列和矩形阵列类似，只是用旋转矩阵取代了平移矩阵。

(10) 对于删除，只要用事务处理打开要删除的对象，用. NET 自带的 Erase 函数即可删除（参阅配书光盘的 DotNetARX 目录下的 EntTools. Cs 文件）。

(11) 编译 DotNetARX 基本类库，然后打开本章的解决方案 Chap02, 加入一个新的类库项目 EntEdit，添加对 acbdmgd.dl、acmgd. Dl 和 DotNetARX. Dl 的引用，并将前二者的「复制本地」属性改为 False，将 Class1 类更名为 EntEdit，。并导入 ApplicationServices, DatabaseServices, EditorInput, Geometry, Runtime 和 DotNetARX 命名空间，在 EntEdit 类中注册一个 EditLine 命令，用三个事务处理创建 2 条直线，并修改直线的颜色：

[CommandMethod "EditLine")]

public static void EditLine ()

Document doc=Application. DocumentManager. MdiActiveDocument;

Database db=doc. Database;

// 事务处理管理器

Autodesk. AutoCAD. DatabaseServices. TransactionManager

Tm=db. TransactionManager;

// 开始第一个事务处理 tx1

using (Transaction trl=tm. StartTransaction ())

Point3d ptstart=Point3d. Origin;

Point3d ptEnd=new Point3d (100,0,0);

Line linel=new Line (ptstart, ptEnd);

ObjectId id1=db. AddToModelSpace (1ine1); // 添加直线到数据库中 // 开始第二个事务处理 tx2

using (Transaction tr2=tm. StartTransaction ())

1ine1. Upgrade0pen (); // 切换 1ine1 的状态为可写

1ine1. ColorIndex=1; // 设置直线的颜色为红色

objectId id2=id1. Copy (ptStart, ptEnd) ;// 复制直线

id2.Rotate (ptEnd,Math.PI/2);// 以直线的起点旋转 90 度 // 开始第三个事务处理 tx3

using (Transaction tr3=tm. StartTransaction ())

Line line2= (Line) tr3. Getobject (id2, OpenMode. Forwrite);

1ine2. ColorIndex=3; // 设置直线的颜色为绿色

tr3. Abort (); // 撤销第三个事务处理 tr3,1ine2 的颜色不变

// 提交第二个事务处理 tr2,1ine1 颜色变为红色，复制 1ine1 并旋转 90 度 tr2. Commit ()

tr1. Commit (); // 提交第二个事务处理 tr1, 添加 1ine1 到数据库中

2.2.4 效果

编译程序，启动 AutoCAD2008, 加载生成的 DLL 文件，执行 EditLine 命令，在图形窗口中绘制出两条互相垂直的红色直线，这说明第一和第二个事务处理中的任务已被执行，而第三个事务处理中改变第二条直线为绿色的任务已经被取消。

2.2.5 小结

学习本节后，读者应该掌握以下内容：

>. NET 中打开对象的方法和注意事项。

》如何对图形对象进行编辑操作。

》如何切换对象的读 / 写状态。

》几何变换矩阵的使用方法。

2.3 圆和圆孤

2.3.1 说明

除了第一节介绍的直线外，几何图形中最常用的图形应该就是圆和圆弧了。本节将介绍如何利用三点法创建圆和圆弧，同时还将结合圆弧和直线构建扇形。

2.3.2 思路

1. 圆

在。NET 中，Circle 类用来表示圆。创建圆的构造函数有两种重载形式，分别为

public Circle ();

public Circle (Point3d center, Vector3d normal, double radius);

创建一个圆需要三个参数：圆心、半径和圆所在的平面（一般用平面的法向矢量来表示）。第一种重载形式不接受任何参数，创建一个圆心为（0,0,0)、半径为 0 的圆，其所在平面法矢量为（0,0,1)，在加入到图形数据库之前，半径必须设为非 0 值，否则圆不会被创建；第二种重载形式则接受了圆心、圆所在平面法矢量和半径三个参数。如果用第一种方法，则在创建圆后，要设置圆心、半径和圆所在平面的法向矢量。和创建直线类似，用第二种形式更方便一些。

2. 圆弧

在。NET 中，AC 类用来表示圆弧，创建圆弧的构造函数有三种重载形式，分别为

public Arc ();

public Arc (Point3d center, double radius, double startAngle, double endAngle); public Arc (Point3d center, Vector3d normal, double radius, double startAngle, double endAngle);

最后一种重载形式接受最多的参数，其接收的 5 个参数分别是圆弧的圆心、法向矢量、半径、起始角度和终止角度。

Ac 类的默认构造函数创建一个圆心为（0,0,0)、半径为 0 的圆弧，其所在平面法矢量为（0,0,1)，起始和终止角度均为 0。在加入到图形数据库之前，半径必须设为非 0 值，否则圆弧不会被创建。

第二种构造函数相当于最后一种构造函数的 normal 参数为（0,0,1) 向量的情况。圆弧的起始和终止角度都用弧度来表示，如果起始角度大于终止角度，沿逆时针方向创建圆弧；否则，如果起始角度小于终止角度，沿顺时针方向创建圆弧。

为什么圆弧会有方向？简单一点说，就是因为圆弧的起点和终点可以交换，这就决定了

圆弧的起始角度可能会大于终止角度，如图 2.12 所示。

2.3.3 步骤

(1) 首先打开 DotNetARX 基本类库，新建一个类文件 CircleTools..cs，用于封装简化圆

创建的函数，在 CircleTools 类代码的顶部导入 DatabaseServices 和 Geometry 命名空间，修改

类的声明如下：

public static class CircleTools

接下来添加三点法画圆的函数。通过圆周上任意三点创建圆，如果用数学计算的方法求

出圆心和半径，则过于麻烦，方便快捷的方法是用 Geometry 命名空间中的几何类 CircularArc.3d 类来处理，关于几何类会在后面的章节中详细介绍。

在 CircleTools 类中添加 Circle 类的 AddCircle 扩展函数，用于通过圆上三点画圆，代码

如下：

public static bool Createcircle (this Circle circle, Point3d ptl, Point3d pt2, Point3d pt3)

// 先判断三点是否共线，得到 pt1 点指向 pt2、pt2 点的矢量

Vector3d va pt1. GetvectorTo (pt2);

Vector3d vb pt1. GetvectorTo (pt3);

// 如两矢量夹角为 0 或 180 度（π 弧度），则三点共线

if (va. GetAngleTo (vb) ==0 va. GetAngleTo (vb)==Math. PI)

return false;

else

// 创建一个几何类的圆弧对象

CircularArc3d geArc new CircularArc3d (pt1, pt2, pt3);

// 将圆弧对象的圆心和半径赋值给圆

circle. Center geArc. Center;

circle. Radius geArc. Radius;

return true;

CircularArc3d 类能够创建一个几何类的圆弧对象，该对象仅用来计算，不能在图形窗口中显示。CircularAre.3d 类有一个构造函数可以根据三点创建圆弧，这里正是使用该函数创建了几何类的圆弧。

创建好几何类的圆弧后，就可以查询该对象的圆心、所在平面、半径等特性，将这些参数传递到创建圆的函数中，就可以实现三点法画圆。

上面的函数定义中使用了第一节介绍的扩展方法，这样做的好处让你的代码看上去更加简洁，如下面的代码所示：

Circlecircle=new circle ();

circle. Createcircle (ptl, pt2, pt3);

(2) 新建一个类文件 ArcTools.. Cs，用于封装简化圆弧创建的函数，在 ArcTools 类代码的 J 顶部导入 DatabaseServices 和 Geometry 命名空间，修改类的声明如下：

public static class ArcTools

在 ArcTools 类中添加三点法创建圆弧的函数：

public static void CreateArc (this Arc arc, Point3d startpoint, Point3d pointOnArc, Point3d endpoint)

// 创建一个几何类的圆弧对象

CircularArc3d geArc=new CircularArc3d (startPoint, pointOnArc, endpoint); // 将几何类圆弧对象的圆心和半径赋值给圆弧 Point3d centerPoint=geArc. Center;

arc. Center centerPoint;

arc. Radius geArc. Radius;

// 计算起始和终止角度

arc. StartAngle startPoint. AngleFromXAxis (centerPoint);

arc. EndAngle endPoint. AngleFromXAxis (centerPoint);

代码中使用了一个自定义 Poit3d 类的扩展函数，用于计算从第一点到第二点所确定的矢量与 X 轴正方向的夹角，其定义如下（为便于使用，请将该函数放入 DotNetARX 类库的 GeTools 类中）：

public static double AngleFromXAxis (this Point3d pt1, Point3d pt2)

// 构建一个从第一点到第二点所确定的矢量

Vector2d vector=new Vector2d (pt1. X -pt2. X, pt1. Y-pt2. Y);

// 返回该矢量和 ⅹ 轴正半轴的角度（弧度）

return vector. Angle;

Vector.2d 类用来表示一个二维空间中的矢量，其 Angle 属性返回该矢量和 X 轴正半轴的

角度（弧度）。

(3) 编译 DotNetARX 基本类库，然后打开本章的解决方案 Chap02, 加入一个新的类库项 日，添加对 acbdmgd.dl、acmgd.dll 和 DotNetARX.dll 的引用，并将前二者的「复制本地」属性改为 False，将 Class1 类更名为 CircleAndArc，并导入 DatabaseServices、Geometry、Runtime 和 DotNetARX 命名空间，在 CircleAndArc 类中注册一个 Fan 命令用三点法创建一个扇形：

[CommandMethod ("Fan")]

public static void Fan ()

Database db=HostApplicationServices. WorkingDatabase;

using (Transaction trans=db. TransactionManager. StartTransaction ())

// 定义圆弧上的三个点

Point3d startPoint=new Point3d (100,0,0);

Point3d pointOnArc=new Point3d (50,25,0);

Point3d endpoint=new Point3d ();

// 调用三点法画圆弧的扩广展函数创建扇形的圆弧

Arc arc=new Arc ();

arc. CreateArc (startPoint, pointOnArc, endPoint);

// 创建扇形的两条半径

Line linel=new Line (arc. Center, startPoint);

Line line2=new Line (arc. Center, endPoint);

// 一次性添加实体到模型空间，完成扇形的创建

db. AddToModelSpace (linel, line2, arc);

trans. Commit (); // 提交事务处理

2.3.4 效果

编译程序，启动 AutoCAD2008, 加载生成的 DLL 文件，执行 Fan 命令，在图形窗口中出现如图 2.13 所示的扇形。

2.3.5 小结

本节示例代码只介绍了三点法创建圆和圆弧的方法，对于其他创建方法如按两点创建圆等，限于篇幅，代码未放在书中，请读者在配书光盘中阅读。

学习本节之后，再回顾一下涉及的知识点：》曲线类常用属性与函数的使用。》使用几何类实现三点法创建圆和圆弧。》使用几何类计算矢量与 X 轴正半轴的角度。

2.4 多段线

2.4.1 说明

在 CAD 软件开发中，多段线的使用范围很广，这是由于它可以包含多个直线或圆弧段，

特别适合表示一些连续的线（例如道路、边界、等高线等）。本节介绍多段线的创建，提供了创建多段线、矩形、正多边形、圆和圆弧的函数。需要注意的是，本节创建的圆与圆弧与上一节创建的圆与圆弧不同，它们实际上是由多段线构成的。

2.4.2 思路

AutoCAD 中包括三种类型的多段线。

》优化多段线：也称为轻量多段线，可以包含直线和圆弧段，可以指定线宽，但是所有

顶点必须在同一个平面上。

》二维多段线：也称为重量多段线，是 AutoCAD 早期的多段线版本，不推荐使用。》三维多段线：只能包含直线段，可以指定线宽，不要求所有顶点在同一个平面上。相比起来，优化多段线使用范围更广，使用起来涉及的细节也更多，这里主要介绍优化

多段线，至于重量多段线和三维多段线，只会在用到的时候简单说明。

优化多段线在。NET 中对应的是 Polyline 对象，图 2. L4 为 Polyline 类常用的属性和方法。

Polyline

carve

属性

行 C1osed【get: set: }: bo1 是否闭合

子 ConstantWidth {get: set:}: double 整体宽度

舒 E1 evation【gt: set：】：double 高度（多段线所在平面与 CS 原点之间的距）

Length【get：】：doub1e 长度

Normal【get: set：】：Vector3d 多段线所在平面的法向量

NumberOfVertices {get:}: int 顶点数

口方法

◆AddVertexAt (int index,, Point2dpt, double bulge,, double startWidth, double endWidth): void 为多段线添加顶点

◆GetBulgeAt (int index).: doubl。获取多段线的凸度

◆GetEndWidthAt (int index): double 获取多段线终点宽度

GetPoint2 dAt (int index): Point2d 获取多段线的顶点（二维）

9 GetPoint3 dAt (int value): Point3d 获取多段线的顶点（三维）

GetStartWidtht (int indes): doubl。获取多段线的起点宽度

◆Poly1ine0 缺省构造函数

Polyline (int vertices）构造函数，创建指定顶点数的多段线

◆RemoveVertexAt (int index): void 移除指定位置处的顶点

9 SetBulgeAt (int index,, double bulge): void 设置多段线的凸度

SetEndWidthAt (int index, double endWidth): vo1c，设置多段线的终点宽度

SetPointAt (int index, Point2dpt): voil 设置 pt 为多段线的顶点

SetStartWidthAt (int index,. Double starthdth): vo1 设置多段线的起点宽度

图 2.14 Polyline 类常用的属性和方法

2.4.3 步骤

(1) 首先打开 DotNetARX 基本类库，新建一个类文件 PolylineTools. Cs，用于封装简化多段线创建的函数，在 PolylineTools 类代码的顶部导入 DatabaseServices 和 Geometry 命名空间，修改类的声明如下：



Public. Static class PolylineTools

在 PolylineTools 类中添加 Polyline 类的 CreatePolyline 扩展函数，通过二维点集合创建多段线，代码如下：

public static void CreatePolyline (this Polyline pline, Point2dCollection pts)

for (int i=0; i <pts. Count; i++)

// 添加多段线的顶点

pline. AddvertexAt (i, pts [i],0,0,0);

CreatePolyline 函数使用了 Polyline 类的 AddVertexAt 函数为多段线添加 J 顶点，其函数定义为

public void AddvertexAt (int index, Point2d pt, double bulge,

double startwidth, double endwidth);

其中，index 参数用来指定要添加顶点的索引号（从 0 开始）；pt 参数指定顶点的位置：bulge 为要创建的顶点的凸度；start Width 和 end Width 表示从该顶点到下一个顶点之间边线的起始和终止线宽，代码中为了简化统一设置为 0。

凸度用来指定当前顶点的平滑性，其意义为：在多段线顶点显示中，选取顶点与下一个顶点形成的弧之间角度的四分之一正切值，0 表示直线，1 表示半圆，介于 0 与 1 之间的为劣弧，大于 1 为优弧。

图 2.15 很好地说明了凸度的概念。左边半圆的起点凸度为 1，右边半圆的起点凸度为 - 1，凸度的不同会导致圆弧方向的不同。

(2) 重载 CreatePolyline 扩展函数，使其能接受不固定的二维点，这样在调用该函数时就不需要生成一个二维点集合了，代码如下：

public static void Createpolyline (this Polyline pline, params Point2d [] pts)

pline. CreatePolyline (new Point2dCollection (pts));

定义了上面的可变参数形式的 CreatePolyline 函数后，可以这样创建多段线：

pline. CreatePolyline (pt1, pt2, pt3...);

(3) 添加一个函数 CreateRectangle，根据两个角点创建矩形：

public static void CreateRectangle (this Polyline pline, Point2d pt1, Point2d pt2)

// 设置矩形的 4 个顶点

double minX=Math.Min (pt1. X, pt2. X); double maxX=Math.Max (pt1. X, pt2. X) ; double miny=Math.Min (pt1. Y, pt2. Y) ; double maxy=Math.Max (pt1. Y, pt2. Y);

Point2dCollection pts=new Point2dCollection (); pts. Add (new Point2d (minx, minY)); pts. Add (new Point2d (minX,maxY)); pts. Add (new Point2d (maxX,maxy)); pts. Add (new Point2d (maxX, minY)); pline. CreatePolyline (pts);

pline. Closed=true; // 闭合多段线以形成矩形

代码中使用了 Polyline 类的 Closed 属性为 true 以生成闭合的多段线。

(4) 添加一个函数 CreatePolygon，用于根据中心点、边数和外接圆半径来创建正多边形：

public static void Createpolygon (this Polyline pline, Point2d centerpoint,

int number, double radius)

Point2dCollection pts=new Point2dCollection (number);

double angle=2*Math.PI/number; // 计算每条边对应的角度

// 计算多边形的顶点

for (int i 0; i <number; i++)

Point2d pt=new Point2d (centerpoint. X radius Math. Cos (i angle), centerPoint. Y radius Math.Sin (i*angle));

pts. Add (pt);

}

pline. CreatePolyline (pts);

plne. Closed=true; // 闭合多段线以形成多边形

函数的关键在于计算正多边形的所有顶点，这可以通过正多边形的中心点和顶点与中心

点的角度 α 计算得到，如图 2.16 所示。

(5) 添加一个函数 CreatePolyCircle，根据圆心和半径创建多段线形式的圆：

public static void CreatepolyCircle (this Polyline pline, Point2d centerpoint,

double radius)

// 计算多段线的顶点

Point2d ptl=new Point2d (centerPoint. X radius, centerPoint. Y);

Point2d pt2=new Point2d (centerPoint. X radius, centerPoint. Y);

Point2d pt3=new Point2d (centerPoint. X radius, centerPoint. Y);

Point2dCollection pts=new Point2dCollection ();

// 添加多段线的顶点

pline. AddvertexAt (0, pt1,1,0,0);

pline. AddvertexAt (1, pt2,1,0,0);

pline. AddvertexAt (2, pt3,1,0,0);

pline. Closed=true; // 闭合多段线以形成圆

代码中指定多段线的凸度为 1 以形成圆。

(6) 添加一个函数 CreatePolyArc., 根据圆心、半径、起始角度和终止角度创建多段线形式的圆弧：

public static void CreatepolyArc (this Polyline pline, Point2d centerPoint, double radius, double startAngle, double endangle)

// 计算多段线的顶点

Point2d ptl=new Point2d (centerPoint.X radius Math. Cos (startAngle),

centerPoint.Y radius Math. Sin (startAngle) ) ;

Point2d pt2=new Point2d (centerPoint.X radius Math. Cos (endAngle),

centerPoint.Y radius Math. Sin (endAngle)) ;

// 添加多段线的顶点

pline. AddvertexAt (0, pt1, Math.Tan ( (endAngle -startAngle) /4),0,0); pline. AddvertexAt (1, pt2,0,0,0);

代码中根据起始角度和终止角度指定多段线的凸度，以形成圆弧。

(7) 编译 DotNetARX 基本类库，然后打开本章的解决方案 Chap02, 加入一个新的类库项目 Polylines，添加对 acbdmgd.dl、acmgd. Dl 和 DotNetARX. Dl 的引用，并将前二者的「复制本地」属性改为 False，将 Class1 类更名为 Polylines，并导入 DatabaseServices、Geometry、Runtime 和 DotNetARX 命名空间，在 Polylines 类中注册一个 AddPolyline 命令用来测试前面创建的函数：

[CommandMethod "AddPolyline")]

public void Addpolyline ()

Database db=HostApplicationServices. WorkingDatabase;

using (Transaction trans=db. TransactionManager. StartTransaction ())

F

Point2d startPoint=Point2d. Origin;

Point2d endPoint=new Point2d (100,100); Point2d pt=new Point2d (60,70); Point2d center=new Point2d (50,50);

// 创建直线

Polyline pline=new Polyline ();

pline. CreatePolyline (startpoint, endpoint); // 创建矩形

Polyline rectangle=new Polyline ();

rectangle. CreateRectangle (pt, endPoint);

// 创建正六边形

Polyline polygon=new Polyline ();

polygon. CreatePolygon (Point2d. Origin,6,30); // 创建半径为 30 的圆

Polyline circle=new Polyline ();

circle. CreatePolyCircle (center,30);

// 创建圆弧，起点角度为 45 度，终点角度为 225 度

Polyline arc=new Polyline ();

double startAngle=45;

double endAngle=225;

arc. CreatePolyArc (center,50, startAngle. DegreeToRadian (), endAngle. DegreeToRadian ());

// 添加对象到模型空间

db. AddToModelSpace (pline, rectangle, polygon, circle, arc);

trans. Commit ()

}

代码中使用了 DotNetARX 基本类库的 GeTools.. Degree ToRadian 函数（为 double 类的扩展函数），将角度值转换为弧度值，其定义如下：

public static double DegreeToRadian (this double angle)

return angle (Math. PI 180.0);

2.4.4 效果

编译程序，启动 AutoCAD2008, 加载生成的 DLL 文件，执行 AddPolyline 命令，在图形窗口中出现如图 2. I7 所示的结果。

2.4.5 小结

学习本节之后，回顾一下涉及的知识点：

> 创建优化多段线，设置闭合特性。》创建矩形、正多边形。》创建多段线形式的圆和圆弧。》多段线中凸度的概念。》C# 可变参数的使用。

2.5 椭圆和样条曲线

2.5.1 说明

本节介绍创建椭圆和样条曲线的方法，其中椭圆是根据外接矩形创建的，而创建样条曲

线则直接调用构造函数。

2.5.2 思路

对于创建椭圆对象，可以直接调用 Ellipse 类的构造函数，其定义如下：

public Ellipse (Point3d center, Vector3d unitNormal, Vector3d majorAxis, double radiusRatio, double startAngle, double endAngle);

其中，center 参数表示椭圆的中心点，unitNormal 表示椭圆所在平面的法向量，majorAxis

表示椭圆 1/2 长轴的矢量（矢量的起点为椭圆的中心，终点为椭圆长轴的一个端点），radiusRatio

表示半径比例，startAngle 表示椭圆的起始角度，endAngle 表示椭圆的终止角度。

上面的参数中，半径比例是一个用来定义椭圆

半径比例 - 0.25

短轴相对于长轴的比例的参数，半径比例为 1 时椭

长轴

半径比例 - 0.75 圆实际上是一个圆，图 2.18 给出了一定半径比例时

短轴的椭圆形状。

图 2.18 半径比例的含义

根据外接矩形创建椭圆，椭圆长、短轴的端点

是外接矩形四条边的中点，因此只要确定外接矩形

的角点，椭圆的大小和形状就被确定。

样条曲线在工程中应用不是很多，因此本节直接调用 Spline 类的构造函数创建样条曲线。Spline 类共有 5 种形式的构造函数，本节实例中使用的是下面两种形式：

public Spline (Point3dCollection point, int order, double fitTolerance); public Spline (Point3dCollectionpoint, Vector3dstartTangent, Vector3dendTangent, int order, double fitTolerance);

其中，point 表示样条曲线的拟合点，order 表示拟合曲线的阶数（必须在 2~26），fitTolerance

表示允许的拟合误差，startTangent 和 endTangent 分别表示曲线起点和终点的切线方向。

2.5.3 步骤

(1) 首先打开 DotNetARX 基本类库，新建一个类文件 EllipseTools.. Cs，用于封装根据外



接矩形创建椭圆的函数，在 EllipseTools 类代码的顶部导入 DatabaseServices 和 Geometry 命名空间，修改类的声明如下：

public static class EllipseTools

在 EllipseTools 类中添加 Ellipse 类的 CreateEllipse 扩展函数，根据外接矩形创建椭圆，代码如下：

public static void CreateEllipse (this Ellipseellipse, Point3d pt1, Point3d pt2)

Point3 d center=GeTools. Midpoint (pt1, pt2); '// 椭圆的中心点

Vector3 d normal=Vector:3d. ZAxis; // 法向量设置为 (0,0,1)

/ 椭圆 1/2 长轴的矢量，矢量的起点为椭圆的中心，终点为椭圆长轴的一个端点

Vector3d majorAxis=new Vector3d (Math. Abs (pt1.X -pt2.X)/2,0,0);

// 椭圆短轴与长轴的长度比例

double ratio=Math. Abs ((pt1. Y pt2. Y) / (pt1. X -pt2. X) ) ;

// 设置椭圆的参数

ellipse. Set (center, normal, majorAxis, ratio,0,2 Math. PI);

根据外接矩形的两个角点首先可以计算出椭圆的中心点，然后计算椭圆的长轴端点和半 径比例，最后调用 Ellipse 类的 Set 函数设置椭圆的有关参数。其中，Math. Abs 函数用来获取数值的绝对值。

代码中获取椭圆中心点的函数利用了 DotNetARX 基本类库的 GeTools 类的 MidPoint 函数求得，该函数用来计算任意两点之间的中点，其定义如下：

public static Point3d Midpoint (Point3d pt1, Point3d pt2)

{

Point3d midPoint new Point3d ( (pt1.X pt2.X)/2.0,

(pt1.Y+pt2.Y)/2.0,

(pt1.Z+pt2. Z) /2.0);

return midpoint;

提示

Ellipse 类的 MajorAxis（长轴端，点）和 Normal（平面法向量）属性为只渎参数，因此要设置椭圆的这两个属性，你必须调用 St 函数来进行。

(2) 编译 DotNetARX 基本类库，然后打开本章的解决方案 Chap02, 加入一个新的类库项目 EllipseAndSpline，添加对 acbdmgd.dl、acmgd.dll 和 DotNetARX. Dl 的引用，并将前二者的「复制本地」属性改为 False，将 Class1 类更名为 EllipseAndSpline，。并导入 DatabaseServices、Geometry、Runtime 和 DotNetARX 命名空间，在 EllipseAndSpline 类中注册一个 AddEllipse 命令用来在图形中加入两个椭圆和一个椭圆弧：



[CommandMethod ("AddEllipse")] public void AddEllipse ()

Database db=HostApplicationServices. WorkingDatabase;

using (Transaction trans=db. TransactionManager. StartTransaction ())

Vector3 d majorAxis-=new Vector3d (40,0,0); // 长轴端点 // 使用中心点、所在平面、长轴矢量和半径比例（0.5) 创建一个椭圆 Ellipse ellipsel=new Ellipse (Point3d. Origin, Vector3d. ZAxis, majorAxis,0.5,0,2 Math. PI) i

E11 ipse e11ipse2=newE11ipse (); // 新建一个椭圆

// 定义外接矩形的两个角点

Point3d pt1=new Point3d (-40, -40,0);

Point3d pt2=new Point3d (40,40,0);

// 根据外接矩形创建椭圆

ellipse2. CreateEllipse (pt1, pt2);

// 创建椭圆弧

majorAxis new Vector3d (0,40,0);

Ellipse ellipseArc=new Ellipse (Point3d. Origin, Vector3d. ZAxis, majorAxis,0.25,Math. PI,2 Math. PI);

// 添加实体到模型空间

db. AddToModelSpace (ellipsel, ellipse2, ellipseArc);

trans. Commit ()

}

(3) 在 EllipseAndSpline 类中注册一个 AddSpline 命令用来在图形中加入两个样条曲线：

[CommandMethod ("Addspline")]

public void Addspline ()

Database db=HostApplicationServices. WorkingDatabase;

using (Transaction trans=db. TransactionManager. StartTransaction ())

// 使用样本点直接创建 4 阶样条曲线

Point3dCollection pts=new Point3dCollection ();

pts. Add (new Point3d (0,0,0)) ;

pts. Add (new Point3d (10,30,0));

pts. Add (new Point3d (60,80,0));

pts. Add (new Point3d (100,100,0));

Spline splinel=new Spline (pts,4,0);

// 根据起点和终点为的切线方向创建样条曲线

Vector3d startTangent=new Vector3d (5,1,0);

Vector3d endTangent=new Vector3d (5,1,0);

2.5.4 效果

编译程序，启动 AutoCAD2008, 加载生成的 DLL 文件，分别执行 AddEllipse 和 AddSpline 命令，在图形窗口中出现如图 2. L9 所示的结果。从图中可以看出，由于外接矩形实际上为正方形，因此根据其创建的椭圆实际上是一个圆。

2.5.5 小结

学习本节之后，回顾一下涉及的知识点：

》根据外接矩形创建椭圆。

》创建椭圆弧。

》创建样条曲线。

2.6 文字

2.6.1 说明

AutoCAD 中的文字共分两种：单行文字与多行文字。对简短的输入项使用单行文字，对于较长而且有内部格式的输入，可以使用多行文字。本节实例将创建带特殊字符的单行文字和有堆叠效果的多行文字。

2.6.2 思路

1. 单行文字

在。NET 中，DBText 类用来表示单行文字（请注意，不是 Text！）。DBText 类只有一个不带参数的构造函数，它将单行文字的属性设置如下：插入点和对齐点为（0,0,0)、倾斜和旋转角度为 0.0、高度为 0.0、宽度比例为 1.0、文字内容为 null、文字样式的 ObjectId 为 ObjectId.Null、镜像为 false、水平对齐方式为左对齐、垂直对齐方式为基线、法向量为（0,0,1)、厚度为 0.0。因此创建单行文字后，需对其插入点、文字内容、文字样式、文字高度、倾斜角度、旋转角度和对齐方式等属性进行设置。DBText 类的属性如图 2.20 所示。

图 2.20 中涉及与文字对齐有关的枚举类型如图 2.21 所示。

图 2.20 DBText 类属性图 2.21 文字对齐选项

文字对齐方式的具体含义如图 2.22 所示。

middle center top center

top left -top right

middle left -middle right

baseline left (default) - baseline right

bottom left_

bottom right

baseline center

middle

bottom center

图 2.22 文字的对齐方式

2. 多行文字

在。NET 中，MText 类用来表示多行文字。创建多行文字的步骤与创建单行文字的步骤基本类似，也是先用不带参数的默认构造函数创建多行文字，然后再对其插入点、文字内容、文字样式、文字宽度等属性进行设置。注意多行文字无法直接指定文字的高度，这是因为多行文字各部分文字的高度都可以单独设置。

3. 多行文字的格式代码

在 AutoCAD 中要创建诸如 m 这样的符号必须使用多行文字的堆叠特性，这属于多行文字格式代码的内容。关于 AutoCAD 的多行文字可以使用的格式代码，可以参考 AutoCAD 帮助文档中的相关说明，如图 2.23 所示。

根据格式代码对多行文字所起的修饰作用，可以将其分为两类：

》在多行文字中插入特殊字符。例如「川」可以在多行文字中插入反斜杠，{」可

在多行文字中插入一对大括号。对这类格式代码去掉一个特殊字符「」即可。

》修改多行文字的字体、颜色等特性。例如「File name；」用于修改部分文字的字体，

「S..;」用于对指定部分的文字进行堆叠。对这类格式代码可将「1」和「；」之间的字符从字符串中全部删除即可。

图 2.23 帮助系统中对多行文字格式代码的说明 AutoCAD 中用于堆叠的特殊字符有：

》斜杠（）以垂直方式堆叠文字，由水平线分隔。》井号（#）以对角形式堆叠文字，由对角线分隔。

》插入符（）创建公差堆叠（垂直堆叠，且不用直线分隔）。

2.6.3 步骤

(1) 首先打开 DotNetARX 基本类库，新建一个类文件 TextTools. Cs，用于封装与文字有关的特殊字符及多行文字的堆叠字符串。在 TextTools 类代码的顶部导入 DatabaseServices 命名空间。修改类的声明如下：

public static class TextTools

(2) 在 TextTools 类的上方添加一个名为 TextSpecialSymbol 的结构，用来封装文字中的特殊字符，代码如下：

public struct TextSpecialSymbol

public static readonly string Degree=@"\U+00B0"; // 度符号（°）

public static readonly string Tolerance=e"\U+00B1"; // 公差符号（±）

pub1 ic static readonly string Diameter: =e"\U+2205"; // 直径符号（Φ）

pub1 ic static readonly string AlmostEqua1=e"\U+2248"; // 几乎相等（≈）pub1 ic static readonly string Angle=g"\U+2220"; // 角度（∠）pub1 ic static readonly string Notequal=e"\U+2260"; // 不相等（≠）public static readonly string Square=@"\U+00B2"; //public static readonly string Cube=@"\U+00B3"; //

public static readonly string Overline=e「号号 o"; // 单行文字的上画线

public static readonly string Underlines=e"% u"; // 单行文字的下画线

Public static readonly string Alpha="\U+03B1"; // 希腊字母 a public static readonly string Belta=e"\U+03B2"; // 希腊字母 B public static readonly string Gamma=e"\U+03B3"; // 希腊字母 y

有的符号在键盘上不存在对应的按键，需要特殊的方法进行输入，称为特殊字符。在 AutoCAD 中，可以使用控制代码或 Unicode 字符串来表示特殊字符。控制代码以「%%」开头，如上面代码中的单行文字上、下画线。Unicode 字符串的格式为「U+nnnn」，其中 U 代表 Unicode 字符，nnnn 为四个十六进制数字的 Unicode 编码。

诸如直径（中）、公差（±）、度（°）之类的特殊字符，控制代码或 Unicode 字符串都可以对其进行表示。如直径（中）的控制代码为「%% d」，Unicode 字符串为「U+2205」。但由于一些特殊字符在多行文本中只能使用 Unicode 字符串，因此上面代码中除了单行文字的上、下画线（多行文字可以使用 MText 类的 UnderlineOn 和 UnderlineOff 属性开关下画线），采用控制代码外，其余均采用 Unicode 字符串。

需要注意的是，使用 Unicode 字符串表示特殊字符时，必须使用支持它们的字体。根据 AutoCAD 帮助文档，Unicode 字符串适用于下列 TrueType (TTF）字体和 SHX 字体：Simplex、RomanS、Isocp、Isocp22、Isocp3、Isoct、Isoct2、Isoct3、Isocpeur（仅 TTF 字体）、Isocpeur italic（仅 TTF 字体）、Isocteur（仅 TTF 字体）、Isocteur italic（仅 TTF 字体）。

公提示

上面代码中列出了本节实例将使用的特殊字符，对于其他的特殊字符（如土木工程

中经常使用的各级钢筋符号），你可以使用相同的方法进行处理。限于篇幅，这里不再 给出详细的实现代码，可参阅配书光盘「Chap02 DotNetARX」文件夹下的 TextTools.. Cs 文件。

(3) 在 TextTools 类中添加 StackText 函数，用于获取堆叠字符串，其实现代码如下（text

参数表示堆叠分数前的文字，supText 表示堆叠分数的分子，subText 表示堆叠分数的分母，stackType 表示堆叠类型，scale 表示堆叠文字的缩放比例）：

public static string StackText (string text, string supText, string subText, StackType stackType, double scale)

/ 设置堆叠方式所代表的字符，用于将 StackType 枚举转换为对应的字符

string [] strs=new string [] {"/", "#",

// 设置堆叠文字

return string. Format (

"\\A1: {0}{1}\\H{2:0. #) x; \\S{3}{4}{5}; (6) ",

text, "{"scale, supText, strs [(int) stackType],

subText, "}")

该函数的 stackType 参数类型为 StackType 类，该类是一个自定义的枚举类型，表示多行文字的堆叠方式，其定义如下：

public enum StackType

HorizontalFraction, // 水平分数堆叠，对应于「/」

ItalicFraction, // 斜分数堆叠，对应于「#」

Tolerance// 公差堆叠，对应于「」

(4) 编译 DotNetARX 基本类库，然后打开本章的解决方案 Chap02, 加入一个新的类库项目 Texts, 添加对 acbdmgd.dl、acmgd.dll 和 DotNetARX.dl 的引用，并将前二者的「复制本地」属性改为 False，将 Class1 类更名为 Texts，。并导入 DatabaseServices、。Geometry、Runtime 和 DotNetARX 命名空间，在 Texts 类中注册 AddText 命令，用于添加单行文字，其实现代码如下：

[CommandMethod ("AddText ")

public void AddText ()

Database db=HostApplicationServices. WorkingDatabase;

using (Transaction trans=db. TransactionManager. StartTransaction ())

DBText textFirst=new DBText (); // 创建第一个单行文字

textFirst. Position=new Point3d (50,50,0); // 文字位置

textFirst. Height=5; // 文字高度

// 设置文字内容，特殊格式为≈、下画线和平方

textFirst. Textstring =""+TextTools. AlmostEqual TextTools. Underline "2000"+TextTools. Underline "m"+TextTools. Square;

// 设置文字的水平对齐方式为居中

textFirst. HorizontalMode TextHorizontalMode. TextCenter;

// 设置文字的垂直对齐方式为居中

textFirst. VerticalMode TextVerticalMode. TextVerticalMid;

// 设置文字的对齐点

textFirst. AlignmentPoint textFirst. Position;

DBText textSecond: =new DBText (); // 创建第二个单行文字

textSecond. Height=5; // 文字高度

// 设置文字内容，特殊格式为角度、希腊字母和度数

textSecond. Textstring TextTools. Angle TextTools. Belta "=45"+TextTools. Degree;

// 设置文字的对齐方式为居中对齐

textSecond. HorizontalMode TextHorizontalMode. TextCenter;

textSecond. VerticalMode TextverticalMode. TextverticalMid;

// 设置文字的对齐点

textSecond. AlignmentPoint new Point3d (50,40,0);

DBText textLast=new DBText (); // 创建第三个单行文字

textLast. Height=5; // 文字高度

// 设置文字的内容，特殊格式为直径和公差

textLast. TextString=TextTools. Diameter+"30 的直径偏差为「+TextTools. Tolerance

+"0.01"；

// 设置文字的对齐方式为居中对齐

textLast. HorizontalMode TextHorizontalMode. TextCenter;

textLast. VerticalMode TextVerticalMode. TextverticalMid;

// 设置文字的对齐点

textLast. AlignmentPoint new Point3d (50,30,0);

db. AddToModelSpace (textFirst, textSecond, textLast); // 添加文本到模型空间 trans. Commit (); // 提交事务处理

}

使用 DBText 类的 Position 属性设置了单行文字的插入点后，如果再使用 AlignmentPoint 设置文字的对齐点，则 AutoCAD 会根据对齐点自动调整文字的 Position 属性。因此如果你要设置对齐点，则不必在程序中设置 Position 属性。为了让读者对此能有更深入的认识，程序对第一个单行文字分别设置了 Position 和 AlignmentPoint 属性，而对后面两个单行文字只设置了 AlignmentPoint 属性。可在后面的程序运行结果中看到这第一个单行文字的插入点并没有被设置为 Position 的值。

(5) 在 Texts 类中注册 AddStackText 命令，用于添加堆叠的多行文字，其实现代码如下：



多行文本的内容是由 Contents 属性指定的，而非单行文本的 TextString 函数。需要注意的是，多行文本被添加到图形后，该属性无法获得多行文字的真实内容，因为它返回的是包含了格式代码的文字内容。对于 AutoCAD2009 及以上版本，你可以使用 MText 类的 Text 属性获取去除了格式代码的多行文本内容。对于 AutoCAD2009 以下的版本，可参阅配书光盘中的 DotNetARX 目录下的 TextTools.cs 中的 GetText 自定义函数。

上面代码中分别使用了 MText 类的 ParagraphBreak 静态属性和 C# 中的回车符「n」对多行文本进行换行，它们的效果是一样的。你还可以使用 MTxt 类的其他属性设置特殊的文字属性，如 UnderlineOn、UnderlineOff 属性可以设置下画线，OverlineOn、OverlineOff 属性可以设置上画线。

2.6.4 效果

编译程序，启动 AutoCAD2008, 加载生成的 DLL 文件，分别执行 AddText 和 AddStackText 命令，在图形窗口中出现如图 2.24 所示的文字，其中左边三行为居中对齐的单行文字，文字内容包含多种特殊字符；右边三行为一个带各种堆叠效果的多行文字，同时该多行文字内的文字居中对齐。

现在让我们来看看单行文本的位置，选中最上面的单行文本，用鼠标右键单击选择【特性】快捷菜单项调出属性面板，如图 225 所示。从图中可以看出，该文字的对齐坐标为程序中设置的值，而位置坐标却非程序中设置的与对齐坐标相同的值。

2.6.5 小结

学习本节之后，需要掌握下面的内容：》创建单行文字和多行文字。

》如何为文字内容添加特殊字符和格式。》如何创建堆叠文字。

》单行文字与多行文字对齐方式的设置。

》如何获取多行文字去除特殊格式后的真实内容。

2.7 填充

2.7.1 说明

本节介绍图案填充和渐变色填充的创建。

2.7.2 思路

图案填充和渐变色填充在。NET 中都是 Hatch 类，该类的构造函数仅创建一个空的填充对象，所以还需要对填充类型、样式、图案名称、填充角度、边界等属性加以设置。创建填充的步骤如图 2.26 所示。

创建 Hatch 对象

设置 Hatch 对象的属性

角度（PatternAngle）人比例（PatternScale）等

设置填充的类型和填充图案名

图案填充渐变色填充

填充类型

设置 Hatch 对象为渐变色

(SetHatchPattern) (Hatchobject Type=GradientObject)

将 Hatch 对象加入空间

设置渐变色填充的类型和渐变图案

(SetGradient)

设置关联

(Associative）设置渐变的起始和结束颜色

添加填充边界

(SetGradientColors)

(AppendLoop)

计算并显示填充

(EvaluateHatch)

提交事务处理

图 2.26 创建填充的步骤

上图括号内的英文单词表示的是对应的 Hatch 类属性或函数。需要注意的是，如果不按照该图所示的步骤进行操作，则可能无法成功创建填充。

2.7.3 步骤

(1) 首先打开 DotNetARX 基本类库，新建一个类文件 HatchTools. Cs，用于封装与填充有关的操作，在 HatchTools 类代码的顶部导入 ApplicationServices、Colors 和 DatabaseServices 命名空间，修改类的声明如下：

public static class HatchTools

(2) 在 HatchTools 类中添加 CurrentPattern 属性，用于设置或读取默认的填充图案名称：



HPNAME 系统变量表示默认的填充图案名称，因此上面的代码使用了 Application 类的 GetSystem Variable 或 SetSystem Variable 来操作该变量值。需要注意的是，HPNAME 的值最多可包含 34 个字符，且不能有空格。代码在设置 HPNAME 前，对这些条件进行了判断，以防止程序出现异常。

代码中的「□」符号，表示键盘输入的空格。

(3) 在 HatchTools 类中添加 CreateHatch 函数，用来创建图案填充，其实现代码如下（hatch

表示填充对象，patternType 表示填充图案的类型，patternName 表示填充图案名，associative 表示填充是否与边界关联）：

public static void CreateHatch (this Hatchhatch, HatchPatternType patternType, string patternName, bool associative)

Database db=HostApplicationServices. WorkingDatabase;

hatch. SetDatabaseDefaults (); // 设置填充的属性为当前数据库默认值

// 设置图案填充的类型和填充图案名

hatch. SetHatchPattern (patternType, patternName);

db. AddToModelSpace (hatch); // 将填充添加到模型空间

// 设置填充与边界是否关联

hatch. Associativeassociative true false;

该函数的 patternType 参数属于 HatchPatternType 枚举，表示填充图案的类型，可以使用

的值有 UserDefined (用户定义，使用当前线型定义的填充图案) 、PreDefined（预定义，acad. pat 文件中定义的图案名称，acad. Pat 文件为 AutoCAD 默认的填充图案库文件）和 CustomDefined（自定义，acad. Pat 文件以外的其他 pat 文件中定义的图案名称）。

上面代码首先调用了 Hatch 类所属的实体类 Entity 的 SetDatabaseDefaults 函数将填充的如下属性设置为当前图形数据库的默认值：颜色、图层、线型、线形比例、可见性、打印样式、打印样式名和线宽。

Hatch 类的 SetHatchPattern 函数用来设置图案填充的类型和填充图案名，其定义如下：

其中，patternType 表示填充图案的类型，属于上面介绍的 HatchPatternType 枚举；patternName 表示图案的名称，其最多只允许 34 个字符，而且不允许带空格。

前面介绍过，必须严格按照一定的步骤，才能正确创建填充。因此上面的代码在对填充设置关联前，首先将其添加到模型空间中。这一点与前面几节介绍的实体对象是很不一样的，因为在将这些对象加入到模型空间前后，我们对其属性进行更改的效果是一样的。

(4) 在 HatchTools 类中添加 CreateGradientHatch 函数，用来创建渐变色填充，其实现代码如下（hatch 表示填充对象，gradientName 表示渐变色填充的图案名称，color1 表示渐变色填充的起始颜色，color2 表示渐变色填充的结束颜色，associative 表示填充是否与边界关联）：

public static void CreateGradientHatch (this Hatchhatch,

HatchGradientName gradientName, Color color1, Color color2, bool associative)

// 设置渐变填充的类型所代表的字符串，用于将 HatchGradientName 枚举转换为对应的字符串 string [] gradientNames=newstring [{"Linear", "Cylinder", "Invcylinder", "Spherical", "Invspherical", "Hemisperical", "InvHemisperical", "Curved", "Incurved"};

Database db=HostApplicationServices. WorkingDatabase;

hatch. SetDatabaseDefaults (); // 设置填充的默认值

// 设置填充的类型为渐变填充

hatch. HatchobjectType HatchobjectType. Gradientobject;

// 设置渐变填充的类型和图案名称

hatch. SetGradient (GradientPatternType. PreDefinedGradient, gradientNames [(int) gradientName]);

// 新建两个 Co1or 类对象，分别表示渐变填充的起始和结束颜色

GradientColor gColorl=new GradientColor (color1,0);

GradientColor gColor2=new GradientColor (color2,1);

// 设置渐变色的起始和结束颜色

hatch. SetGradientColors (new GradientColor [] gColor1, gColor2 })

db. AddToModelSpace (hatch); // 将填充添加到模型空间

// 设置填充与边界是否关联

hatch. Associative associative true false;

该函数的 gradientName 参数类型为 HatchGradientName 自定义枚举类型，表示渐变色的图案名称，其定义如下：

Hatch 类的 HatchObjectType 属性用来定义填充的类型，它的取值可为 HatchObject（图案填充）和 GradientObject（渐变色填充），Hatch 类默认取值为 HatchObject，。因此前面创建图案填充的函数不需要调用该属性。

Hatch 类的 SetGradient 函数用来设置渐变色填充的类型和图案名称，其定义如下：

public void SetGradient (GradientPatternType gradientType, string gradientName);

其中，gradientType 参数表示渐变填充的类型，它属于 GradientPatternType 枚举，可以使用的值有 PreDefinedGradient（预定义渐变）、UserDefinedGradient（用户定义渐变）；

gradientName 参数表示渐变色的图案名称，可以使用的图案名称为上面介绍的 HatchGradientName

自定义枚举中的值。

Hatch 类的 SetGradientColors 函数用来设置渐变色的起始和结束颜色，其定义如下：

public void SetGradientColors (GradientColor [] value);

其中，value 参数表示一个 GradientColor 类型的数组，该数组的个数只能为 2 个，第一个表示渐变色的起始颜色，第二个表示渐变色的结束颜色。GradientColor 是一种特殊的颜色，主要用于渐变色的操作，你可以使用 GradientColor 的构造函数将 AutoCAD 类的 Color 类转化为 GradientColor，它是通过线性插值将 Color 值转换为 GradientColor 值，其定义如下：

public GradientColor (Color color, float value);

其中，color 表示需要转换成渐变颜色的 AutoCAD 类的 Color 值，value 表示定义渐变运算的线性插值参数。

(5) 编译 DotNetARX 基本类库，然后打开本章的解决方案 Chap02, 加入一个新的类库项目 Hatches，添加对 acbdmgd.dl、acmgd.dl 和 DotNetARX. Dl 的引用，并将前二者的「复制本地」属性改为 False，将 Class1 类更名为 Hatches，。并导入 Colors、DatabaseServices、Geometry、Runtime 和 DotNetARX 命名空间，在 Hatches 类中注册 AddHatch 命令，用于添加一个图案填充，其实现代码如下：



在 AutoCAD 中选择【绘图 / 图案填充】菜单时，可以从【图案填充和渐变色】对话框获

得预定义类型的图案填充能使用的名称，单击其右侧的省略号按钮，还可以调出【填充图案选项板】，查看名称代表的图案，如图 2.27 所示。

如果能在程序中提供这个【填充图案选项板】，那就可以让用户非常容易地选择填充图案了，这会使你的程序看起来更加专业。但非常遗憾的是，Autodesk 并没有正式提供对【填充图案选项板】的访问接口。不过，我们可以通过封装 Autodesk 未正式公开的 C++ 函数来对【填充图案选项板】进行访问，上面代码中的 HatchPalletteDialog 类正是封装的结果。由于封 装使用的是 P/Invoke 技术，该内容会在本书最后进行介绍，本节就不再对其实现进行详细介绍了。只需要把配书光盘中 DotNetARX 目录下的 HatchPalletteDialog 类的代码复制到你的 DotNetARX 中并进行编译即可。

图 2.27 可使用的预定义填充图案及填充图案选项板

上面代码中首先调用了 HatchPalletteDialog 类的构造函数，然后调用该类的 ShowDialog 函数显示「填充图案选项板」。如果用户选择了填充图案，则通过 HatchPalletteDialog 类的 GetPattern 函数返回所选的图案名称，并将其作为输入参数传入前面自定义的 CreateHatch 函数创建图案填充，否则将使用当前图案名创建图案填充。

Hatch 类的 AppendLoop 函数用来为填充添加边界，其定义如下：

public void AppendLoop (HatchLoopTypes loopType, objectIdCollection dbobjIds);

其中，loopType 表示边界的类型，它属于 HatchLoopTypes 枚举，可以取值为 Default（缺省）和 Outermost（最外边）；dbObjIds 表示构成边界的实体集合的 ObjectId，该集合可以由一个或多个实体组成，如果使用多于一个的实体，则它们的端点必须相接以形成一个环。边界实体必须为如下类型：Line、Polyline、Circle、Ellipse、Spline 和 Region。

第一个添加的边界必须是包围填充的最外侧边界，因此你必须使用 HatchLoopTypes.. Outermost 作为输入参数的 AppendLoop 函数。最外侧的边界被添加好以后，你可以连续使用以 HatchLoopTypes. Default 为输入参数的 AppendLoop 函数为填充添加内部边界。内部边界定义了填充区域内的封闭区域，一般称为孤岛。Hatch 类的 HatchStyle 属性定义了孤岛的填充样式，其取值说明如下。

> Normal：指定标准的样式，即普通，为默认样式。该样式将从外部边界向内填充。如

果填充过程中遇到内部边界，则填充将关闭，直到遇到另一个边界为止。如果使用该样式进行填充，将不填充孤岛，但是孤岛中的孤岛将被填充。

> Outer：仅填充最外面的区域。该样式也是从最外面的区域边界向内进行图案填充，

但是遇到内部边界时会关闭图案填充并且不再打开。

> Ignore：：忽略内部边界，填充整个闭合区域。

图 2.28 显示了上面三种孤岛的填充样式。

为填充对象添加边界之后，必须使用 Hatch 类的 EvaluateHatch 函数计算并显示填充对象。

x 提示

如果指定的边界曲线不闭合，创建填充就会失败，你可以使用 NET 的异常处理机制如 y 语句对错误进行处理。

(6) 在 Hatches 类中注册 AddGradientHatch 命令，用于添加一个渐变色填充，其实现代码如下：

[CommandMethod ("AddGradientHatch")]

public void AddGradientHatch ()

Database db=HostApplicationServices. WorkingDatabase;

// 创建一个三角形

Polyline triangle=new Polyline ();

triangle. CreatePolygon (new Point2d (550,200),3,30);

using (Transaction trans=db. TransactionManager. StartTransaction ())

{

// 将三角形添加到模型空间中

ObjectId triangleId=db. AddToModelSpace (triangle);

// 创建一个 ObjectId 集合类对象，用于存储填充边界的 ObjectId

ObjectIdCollection ids=new ObjectIdCollection ();

ids,Add (triangleId);/ 将三角形的 ObjectId 添加到边界集合中

Hatch hatch=new Hatch (); // 创建填充对象

// 创建两个 Co1ox 类变量，分别表示填充的起始颜色（红）和结束颜色（蓝）

Color color1=Color. FromColorIndex (ColorMethod. ByLayer,1);

Color color2=Color.FromColor (System.Drawing. Color. Blue);

// 创建渐变填充，与边界无关联

hatch. CreateGradientHatch (HatchGradientName. Cylinder, colorl, color2, false);

// 为填充添加边界（三角形）

hatch. AppendLoop (HatchLoopTypes. Default, ids);

hatch. EvaluateHatch (true); // 计算并显示填充对象

trans. Commit (); // 提交更改

上面代码中使用了两种方法获取 Color 类的颜色值，第一种是使用 Color 类的静态函数

FromColorIndex，该函数将 AutoCAD 的颜色索引值转换为 Color 类颜色，定义如下：

public static Color FromColorIndex (ColorMethod colorMethod, short colorIndex);

其中，colorMethod 表示颜色值存储的方法，它属于 ColorMethod 枚举，可用的值包括

ByLayer、ByBlock、ByColor、ByAci、ByPen、Foreground、LayerOff、LayerFrozen、None;

colorIndex 表示 AutoCAD 的颜色索引值。

第二种方法使用 Color 类的静态函数 FromColor，该函数将 Windows 的颜色值转换为 Color 类颜色，定义如下：

public static Color FromColor (System. Drawing. Color value);

其中，value 表示 Windows 的颜色值，它属于 System. Drawing. Color 结构，表示一种 ARGB 颜色（alpha、红色、绿色、蓝色）。该结构提供了非常方便的访问各种颜色的方法，如 Color..Red 表示红色，Color..Blue 表示蓝色，Color. Orange 表示橙色。

System. Drawing. Color 类属于 System. Drawing 引用，你必须在项目中手动添加该引用。在解决方案管理器中用鼠标右键单击 Hatches 项目下的「引用」节点，在弹出的快捷菜单中选择【添加引用】，在【添加引用】对话框的【。NET】选项卡中选择「System. Drawing」，单击【确定】按钮，如图 2.29 所示。

除了代码中介绍的两种函数外，Color 类还提供了直接通过 RGB 值创建 Color 类颜色的 FromRgb 函数，其定义如下：

Public static Color FromRgb (byte red, byte green, byte blue);

其中，red、green、blue 参数分别表示红色、绿色和蓝色，它们是 byte 型的整数（8 位），有效值为 0~255。如 Color.. FromRgb (255,0,0) 表示红色。

2.7.4 效果

编译程序，启动 AutoCAD2008, 加载生成的 DLL 文件，执行 AddHatch 命令，系统会

弹出填充图案选项板，如图 2.30 所示。

选择一个填充图案，笔者选择的是「STARS」，单击【确定】按钮，得到如图 2.31 所示的左侧图形，其内侧为圆，外侧为正六边，中间充填了「STARS」表示的五角星图案。

执行 AddGradientHatch 命令，在正六边形的右侧会出现如图 2.31 右侧所示的由渐变色填充的三角形。

选择左边正六边形的边界并拖动其夹点移动，你会发现五角星填充会随其更改而自动更新，这说明该填充是与边界关联的。而你对右边三角形边界做出改动后，渐变填充不会跟随其改变，说明该填充与边界无关联。

2.7.5 小结

学习本节内容之后，需要掌握下面的知识点：

》创建填充的步骤及注意事项。

》如何使填充与边界关联。

》控制孤岛中的填充。

》使用填充图案选项板获取填充图案。

> Color 类对象的各种赋值方法。

2.8 面域

2.8.1 说明

本节介绍创建简单面域及组合面域的方法。

2.8.2 思路

1. 简单面域

Region 类代表 AutoCAD 中的面域。在。NET 中创建面域对象比较特别，它不是利用构造函数来完成对象的创建，而是使用 Region 类的一个静态函数 CreateFromCurves 来完成。

CreateFromCurves 函数的定义为：

public static DBObjectCollectionCreateFromCurves (DBObjectCollection curveSegments);

其中，curveSegments 参数表示一个曲线实体的集合对象，用来定义面域的边界，作为面

域边界的曲线必须首尾相连形成闭合环。

需要注意的是，如果有两条以上的曲线共用一个端点，那么得到的面域数量是不确定的，具体的面域数与实际形成闭合环的数量有关。由于创建面域的数量不确定，因此 CreateFromCurves 函数的返回值是 DBObjectCollection 类的对象集合，它保存了新创建面域的集合。

CreateFromCurves 函数只是在内存中创建了面域，因此为了显示面域，你必须将其添加图形数据库中。

x 注意

在创建面域时，作为面域边界的对象必须是 Line、Arc、Ellipse、Circle、Spline、Polyline3d 或 Polyline 类的对象。

2. 组合面域

你可以通过 Region 类的 BooleanOperation 函数即布尔操作创建组合面域，该函数的定义如下：

public virtual void BooleanOperation (BooleanOperationType operation, Region otherRegion);

其中，operation 表示布尔操作的类型，它是 BooleanOperationType 枚举，可以使用的值有 BoolUnite（并）、BoolSubtract（差）和 BoolIntersect（交）；otherRegion 表示除调用 BooleanOperation 函数的面域外，要进行布尔操作的另外一个面域。

BooleanOperation 函数的运行结果，会将组合面域赋值给调用该函数的面域。

2.8.3 步骤

(l）首先打开 DotNetARX 基本类库，新建一个类文件 RegionTools. Cs，用于封装与面域有关的操作，在 RegionTools 类代码的顶部导入 DatabaseServices 命名空间，修改类的声明如下：

public static class RegionTools

(2) 在 RegionTools 类中添加 CreateRegion，根据曲线创建面域，实现代码如下：

public static List <Region> CreateRegion (params Curve [] curves)

List <Region> regionList=new List <Region> (); // 新建面域列表，存储创建的面域 // 将可变数组转化为集合类，用于面域的创建

DBObjectCollection curveCollection=new DBObjectCollection ();

foreach (Curve curve in curves) // 遍历曲线

// 如果曲线已经被加入到数据库且为写的状态，则返回

if (curve. IsNewobject &curve. IsWriteEnabled)

return null;

curveCollection. Add (curve); // 将曲线添加到集合中

try

// 根据曲线集合，在内存中创建面域对象集合

DBObjectCollection regionObjs=Region. CreateFromCurves (curveCollection); // 将面域对象集合复制到面域列表

foreach (Region region in regionobjs)

regionList. Add (region);

ireturn regionList;

}

catch// 面域创建失败

定义了上面的可变参数形式的 CreateRegion 函数后，可以这样创建面域：

RegionTools. CreatePolyline (curvel, curve2, curve 3...);

CreateRegion 函数的返回值是根据 curves 参数中的曲线所生成的所有面域。

如果曲线已经被加入到数据库且为写的状态，则创建面域的操作会导致 AutoCAD 崩溃，

因此函数对该种类型的曲线进行了条件处理。

在创建面域时一个最常见的错误就是输入的多个曲线不闭合，这样就无法生成面域，对此函数使用了 y 语句进行了异常处理。

(3) 编译 DotNetARX 基本类库，然后打开本章的解决方案 Chap02, 加入一个新的类库

项目 Regions, 添加对 acbdmgd. d、acmgd..dl 和 DotNetARX.dl 的引用，并将前二者的「复制本地」属性改为 False，将 Class1 类更名为 Regions，并导入 DatabaseServices、Geometry、Runtime 和 DotNetARX 命名空间，在 Regions 类中注册 AddRegion 命令，用于添加一个简单的面域，其实现代码如下：

[CommandMethod ("AddRegion")]

public void AddRegion ()

Database db=HostApplicationServices. WorkingDatabase;

using (Transaction trans=db. TransactionManager. StartTransaction ())

// 创建一个三角形

Polyline triangle=new Polyline ();

triangle. CreatePolygon (new Point2d (550,200),3,30);

// 根据三角形创建面域

List <Region> regions=RegionTools. CreateRegion (triangle);

if (regions. Count==O) return; // 如果面域创建未成功，则返回

db. AddToModelSpace (regions [0]); // 将创建的面域添加到数据库中

// 获取面域的质量特性

getAreaProp (region);

trans. Commit (); // 提交更改

上述代码首先创建了一个三角形，然后调用前面定义的 CreateRegion 函数创建三角形面域，最后将生成的面域添加到图形中。

通过 AutoCAD 的 MASSPROP 命令，你可以获取面域的质量特性，如形心、周长、惯性

矩、旋转半径等。但非常遗憾的是，除了周长外，NET 并没有提供访问面域质量特性的方法。

不过，我们可以通过封装对应的 C++ 函数来获取相关的质量特性，上面代码中的 getAreaProp

函数正是调用封装的结果，其定义如下：

private void getAreaProp (Region region)

Editor ed=Application. DocumentManager. MdiActiveDocument. Editor;

ed. WriteMessage ("\n -- 面域 ー ---「）；

ed. WriteMessage ("\n 面积： (0}"，region.Area);

ed. WriteMessage ("\n 周长：{0｝「，region. Perimeter);

ed. WriteMessage ("\n 边界框上限：（0｝「，region. GetExtentsHigh ()); ed. WriteMessage ("\n 边界框下限：（0)「，region. GetExtentsLow ()); ed. WriteMessage ("\n 质心：（0｝「，region. GetCentroid ()); ed. WriteMessage ("\n 惯性矩为：（0}；（1｝「，

region. GetMomInertia () [0], region. GetMomInertia () [1]);

ed. WriteMessage ("\n 惯性积为：（0｝「，region. GetProdInertia ());

ed. WriteMessage ("\n 主力矩为：（0}；{1｝「，

region. GetprinMoments ([0], region. GetPrinMoments () [1]);

ed. WriteMessage ("\n 主方向为：{0}；{1｝「，

region. GetPrinAxes () [0], region. GetPrinAxes () [1]);

ed. WriteMessage ("\n 旋转半径为：{0}；{1}"，

region. GetRadiiGyration () [0],region.GetRadiiGyration () [1]);

getAreaProp 函数调用了封装 C + 面域质量特性的有关函数，由于封装使用的是 P/Invoke

技术，该内容会在本书最后进行介绍，本节就不再对其实现进行详细介绍了。只需要把配书光盘中 DotNetARX 目录下的 RegionTools.. Cs 文件中相关函数的代码复制到你的 DotNetARX 基本类库中并进行编译即可。

(4) 在 Regions 类中注册 AddComplexRegion 命令，使用布尔操作添加一个复杂的面域，其实现代码如下：



上面代码中使用了 NET 的 LNQ 技术对正六边形和圆形面域按面积大小进行排序，然后调用 Region 类的 BooleanOperation 函数对两个面域进行减操作，将正六边形减去圆后形成的组合面域添加到图形中。

关于 LNQ 的具体介绍，请参考本书第 3 章第 2 节的内容。

2.8.4 效果

编译程序，启动 AutoCAD2008, 加载生成的 DLL 文件，分别执行 AddRegion 和 AddComplexRegion 命令，得到如图 2.32 所示的结果。为了显示面域的效果，图中对面域添加了填充。

执行 AddRegion 命令时，会在 AutoCAD 的命令行得到如图 2.33 所示的结果，显示了 AddRegion 命令所创建面域的质量特性。

的令：AddReg1on

面域

面积：1169.13429510899

周长：155.884572681199

边界框上限：（580,225.980762113533)

边界框下限：1535,179,019237886467)

质心：（550,200)

惯性矩为：46896899.4125595：353794651,87867

惯性积为：128604772.961989

主力矩为：131527,60819976：131527.608199775

模型局 1 人布 2

主方向为：（0,0)：（0,0)

旋转￥径为：200.281052523697：550.102263220213

图 2.32 创建面域的结果图 2.33 面域的质量特性

2.8.5 小结

学习本节内容之后，需要掌握下面的知识点：

》使用 Region. CreateFromCurves 函数创建面域。

》使用布尔操作创建组合面域。

》创建面域时的错误处理。

》访问面域的质量特性。

29 尺寸标注

2.9.1 说明

尺寸标注在 AutoCAD 中一般简称为标注，是向图形中添加测量注释的过程。用户可以

为各种对象沿各个方向创建标注。基本的标注类型包括：线性标注、径向标注（半径、直径和折弯）、角度标注、坐标标注、弧长标注。线性标注可以是水平、垂直、对齐、旋转、基线或连续（链式）。图 2.34 列出了标注的几种示例。

角度标注

水平线性标注

200

对齐标注

100

Φ10 直径

50o

垂直线

性标注分 R20

半径标注

75 65 35

基线标注

连续标注

图 2.34 尺寸标注的类型

本节实例将会创建几种常用的标注，同时演示标注的文字替代（如水平线性标注的默认

文本是测量得到的长度值，通过文字替代可以将标注文本修改为任何字符串）。

2.9.2 思路

1. 标注的组成部分

在创建标注之前，有必要了解一下标注的组成部分。标注具有以下几种独特的元素：标注文字、尺寸线、箭头、尺寸界线和引线，如图 2.35 所示。

标注文字是用于指示测量值的文本字符串，它可以包含前缀、后缀和公差。尺寸线用于指示标注的方向和范围，对于角度标注，尺寸线是一段圆弧。箭头（也称为终止符号）显示在尺寸线的两端，可以为箭头或标记指定不同的尺寸和形状。尺寸界线（也称为投影线或证示线）从被标注的特征上延长至尺寸线。引线是一条直线或样条曲线，其中一端带有箭头，另一端带有多行文字对象或块。关于引线的内容，将在下一节进行介绍。

2. 标注的创建

本章介绍的标注类都派生于。NET 中的 Dimension 类，该类提供了标注的一些共有属性，如标注文字、标注样式等。但该类是一个抽象类，所以你不应该通过它来创建标注，而是使用其派生类进行创建。

要创建标注，首先应调用标注类的默认构造函数（即不带参数）构建具体的标注对象，然后再设置标注的属性。表 2.1 列出了。ET 中与标注有关的类及其需要设置的属性。

表 2.1 标注类及其属性

ArcDimension 类表示的弧长标注比较特殊，该类无默认构造函数。因此你必须使用其带参数的构造函数来构造弧长标注，该函数定义如下：

public ArcDimension (Point3d centerPoint, Point3d xLinelPoint, Point3d xLine2Point, Point3d arcPoint, string dimensionText, ObjectId dimensionStyle);

其中，centerPoint 表示圆心，xLinelPoint 和 xLine2 Point 分别表示第一条尺寸界线和第二条尺寸界线原点，arcPoint 表示尺寸弧线上的点，dimensionText 表示尺寸文字，dimensionStyle 表示标注样式。

尺寸公差并没有专门的类，本节实例将通过标注文本的处理来实现。

公提示

由于 Autodesk 并没有提供关联标注的接口，因此通过编程的方法无法实现关联标注的功能。

3. 更改标注的外观

标注的外观可以通过以下几种方式进行：

(1) 设置标注对象与标注外观有关的属性，如下面的语句将角度标注的单位格式设置为弧度：

LineAngularDimension2 dim=new LineAngularDimersion2 ();

dim. Dimaunit =3;

(2) 通过标注对象的 DimensionStyle（标注样式的 ObjectId）或 DimensionStyleName 标注样式名）属性设置其标注样式，这样可以让标注显示为标注样式中定义的外观。关于标注样式的内容，将在本书第 4 章第 3 节进行介绍。

(3) 通过 Application 类的 SetSystemVariable 函数设置标注系统变量，下面的语句与第一种方法运行的效果相同：

Application. SetSystemvariable ("DIMAUNIT",3);

LineAngularDimension2 dim=new LineAngularDimension2 ();

(4) 设置 Database 类与标注外观有关的属性，下面的语句与第一种方法运行的效果相同：

db. Dimaunit =3;

LineAngularDimension2 dim=new LineAngularDimension2 ();

需要注意的是，最后 2 种方法会导致设置语句以后的标注都使用设置的值。

2.9.3 步骤

(1) 打开本章的解决方案 Chap02, 加入一个新的类库项目 Dimensions，添加对 acbdmgd.dl、acmgd.dl 和 DotNetARX. Dl 的引用，并将前二者的「复制本地」属性改为 False，将 Class1 类更名为 Dimensions，并导入 DatabaseServices、Geometry、Runtime 和 DotNetARX 命名空间，在 Dimensions 类中注册 DimTest 命令，用于创建各种类型的标注。首先在其中添加要进行标注的图形：



(2) 在 DimTest 命令提交事务处理的语句「trans. CommitO；」之前，添加如下的创建转角标注的代码：



上面代码中需要说明的问题如下：1) 转角标注尺寸线的旋转角度。

RotatedDimension 类的 Rotation 属性用来转角标注尺寸线的旋转角度，必须为弧度。默认的 Rotation 属性值为 0，即为水平标注。如果要创建垂直标注，则应将 Rotation 属性设置 为 r/2 (对应于 90 度)。.NET 中的 Math.PI 表示 r。

2) 替代标注文字。

你可以使用 Dimension 类的 DimensionText 属性来替换所显示的标注值，该属性可以完全替换所显示的标注值，也可以向标注值附加文字。你可以在 DimensionText 属性中使用带一对括号（<》）的字符串，当字符串显示出来时，主标注值将替换括号。例如，当标注值为 5.08 时，用 DimensionText=「》mm」，将会显示为「5.08mm」。

当标注样式中使用「换算单位」时，你还可以用方括号（【门）来显示换算标注值，但必须在 DimensionText 属性中同时使用◇来替换主标注值时才会有效。例如：当主标注值为 5.08，换算标注值为 2.00 时，使用 Dimension Text=-「◇mm」时，将会显示「5.08 [2.00] mm」，而当 DimensionText=「◇mm【】」时，则会显示为「5.08mm [2.00]」。这也就是说，使用【只能更改换算标注值在文字中所显示的位置。

3) 根据几何关系求点坐标。

代码中使用了一个 DotNetARX 中自定义的 Point3d 类的扩展函数 PolarPoint，它用来获取与给定点指定角度和距离的点，其定义如下：

public static Point3d PolarPoint (this Point3d point, double angle, double dist) return new Point3d (point.X dist Math. Cos (angle), point. Y dist Math.

Sin (angle), point. Z);

其中，point 表示给定点，angle 表示以弧度为单位的角度值，dist 表示两点之间的距离。4) 尺寸公差。

对于尺寸公差，代码中使用了本章第 6 节堆叠文字（公差效果）并结合上面介绍的替代标注文字的方法进行处理。其具体显示效果，可以阅读本节效果部分。

(3) 在 DimTest 命令中继续添加创建对齐标注的代码：



上面代码中使用了本章第 6 节的 TextSpecialSymbol 自定义结构中的 Tolerance 字段（表

示公差符号），并结合替代标注文字的方法表示公差标注。

(4) 在 DimTest 命令中继续添加创建半径标注的代码：

// 创建半径标注

RadialDimension dimRadial=new RadialDimension ();

dimRadial. Center=cirl. Center; // 圆或圆弧的圆心

// 用于附着引线的圆或圆弧上的点

dimRadial. Chordpoint cir1. Center. PolarPoint (GeTools. DegreeToRadian (30), 15)；

dimRadial. LeaderLength=10; // 线长度

dims. Add (dimRadial); // 将半径标注添加到列表中

(5) 在 DimTest 命令中继续添加创建直径标注的代码：

// 创建直径标注

DiametricDimension dimDiametric=new DiametricDimension ();

// 圆或圆弧上第一个直径点的坐标

dimDiametric. Chordpoint =cir2. Center. PolarPoint (GeTools. DegreeToRadian (45), 10)；

// 圆或圆弧上第二个直径点的坐标

dimDiametric. FarChordPoint

cir2. Center. PolarPoint (GeTools. DegreeToRadian (-135),10);

dimDiametric. LeaderLength=O; // 从 ChordPoint 到注解文字或折线处的长度

dims. Add (dimDiametric); // 将直径标注添加到列表中

代码中使用了 DotNetARX 中的自定义函数 DegreeToRadian，将角度值转换为弧度值。

(6) 在 DimTest 命令中继续添加创建角度标注的代码：

/1 创建角度标注

Point3AngularDimension dimLineAngular=new Point3AngularDimension ();

// 圆或圆弧的圆心、或两尺寸界线间的共有顶点的坐标

dimLineAngular. CenterPoint line2. StartPoint;

// 指定两条尺寸界线的附着位置

DimLineAngular. XLinelPoint linel. Startpoint; dimLineAngular. XLine2Point line2. EndPoint; // 设置角度标志圆弧线上的点 dimLineAngular. ArcPoint ク line2. StartPoint. PolarPoint (GeTools. DegreeToRadian (135) ,10);

dims.Add (dimLineAngular); // 将角度标注添加到列表中

(7) 在 DimTest 命令中继续添加创建弧长标注的代码：

// 创建弧长标注，标注文字取为默认值

ArcDimension dimArc=new ArcDimension (arc. Center, arc. StartPoint, arc. EndPoint, arc. Center. PolarPoint (Math. PI, arc. Radius 10), " <> "db. Dimstyle);

dims. Add (dimArc); // 将弧长标注添加到列表中

ArcDimension 类无默认构造函数，因此代码中使用了前面介绍的不带参数的构造函数，其中，尺寸文字使用「◇」以使尺寸只显示标注值，而标注样式则通过调用 Database 类的 Dimstyle 属性将其设置为当前标注样式。

(8) 在 DimTest 命令中继续添加创建坐标标注的代码：

// 创建显示 X 轴值的坐标标注

OrdinateDimension dimX=new ordinateDimension ();

dimX. UsingXAxis=true; // 显示 X 轴值

dimx. DefiningPoint=cir2. Center; // 标注点

// 指定引线终点，即标注文字显示的位置

dimX. LeaderEndPoint cir2. Center. PolarPoint (-Math. PI 2,20);

dims. Add (dimx); // 将坐标标注添加到列表中

// 创建显示 Y 轴值的坐标标注

OrdinateDimension dimY=new OrdinateDimension ();

dimY. UsingXAxis=false; // 显示 Y 轴

dimY. DefiningPoint=cir2. Center; // 标注点

// 指定引线终点，即标注文字显示的位置

dimY. LeaderEndPoint cir2. Center. PolarPoint (0,20);

dims. Add (dimY); // 将坐标标注添加到列表中

OrdinateDimension 类的 bool 型 UsingXAxis 属性可以设置标注是 X 基准坐标标注（true）还是 Y 基准坐标标注（false）。需要注意的是，OrdinateDimension 类还有一个只读的 Using YAxis 属性，你可以用它来判断坐标是否为 Y 基准坐标标注，但无法进行设置操作。

(9) 在 DimTest 命令中继续添加如下的代表，将上面创建的各类标注添加到当前图形的模型空间中：



2.9.4 效果

编译程序，启动 AutoCAD2008, 用 NetLoad 命令加载生成的 DLL 文件，执行 DimTest 命令，得到如图 2.36 所示的结果。

60±88☏

R15 20 500.2

2.66 50

900

90mm

图 2.36 创建标注

2.9.5 小结

学习本节的内容之后，应该熟练掌握下面的知识点：

》尺寸标注的类型和组成部分。

》使用 DimensionText 属性进行尺寸文字替代。

》使用不同的方法更改标注的外观。

》如何通过文字堆叠创建尺寸公差。

》通过几何关系计算未知点的坐标。

2.10 引线与形位公差

2.10.1 说明

本节实例将介绍如何创建引线、多重引线和形位公差。

2.10.2 思路

1. 引线

引线对象是一条线或样条曲线，其一端带有箭头，另一端带有多行文字、形位公差或块参照（称为注释）。在某些情况下，有一条短水平线（又称为基线）将注释连接到引线上。图 2.37 演示了各种形式的引线。

图 2.37 各种形式的引线

引线在。NET 中对应的是 Leader 类对象，该类的构造函数仅创建一个空的引线对象。用构造函数创建引线后，你可以使用 Leader 类的 Append Vertex 函数为引线添加顶点，其中 AppendVertex 函数其定义如下：

public virtual bool Appendvertex (Point3d pointToAdd);

其中，pointToAdd 表示需要添加的引线顶点坐标。

引线创建并添加好顶点以后，可以使用以下的 Leader 类属性对其进行设置。

> Annotation：为引线设置关联的注释对象的 ObjectId。

> IsSplined：取值为 true 时，表示引线为平滑的样条曲线，否则为直线。默认情况为

直线。

》以 Dim 开头的属性：设置引线的外观，如箭头的类型（Dimldrblk）和大小（Dimasz）。2. 多重引线

普通引线的线条只能是一条，但很多情况下我们需要引线指向不同的地方来标识同一个内容，这就需要 AutoCAD2008 以上版本提供的多重引线功能。多重引线比普通引线增加了更多的控制选项，你可以根据需要先创建引线箭头、引线基线或引线内容。

. NET 中的 MLeader 类表示多重引线。与 Leader 类一样，你需要先使用 MLeader 类的默认构造函数创建一个多重引线对象，然后按以下步骤添加引线和注释：

(1) 调用 AddLeader 函数添加引线束，引线束由基线和一些单引线构成。

(2) 通过 AddLeaderLine 函数在引线束中添加单引线。

(3) 通过 AddFirst Vertex、Set Vertex、AddLast Vertex 为单引线添加顶点。

(4) 反复执行步骤 2 和 3，直到单引线添加完毕。

(5) 使用 ContentType 属性设置单引线的注释类型，该属性是一个 ContentType 类枚举，取值可以为 NoneContent（无注释）、BlockContent（块参照）、MtextContent（多行文字）和 ToleranceContent（形位公差）。

(6) 根据注释类型，分别调用对应的属性设置注释对象。其中，多行文字可以使用 MTxt 属性，块参照可以使用 BlockContentId（表示块参照的 ObjectId）。

3. 形位公差

形位公差属于机械制图的范畴，它表示特征的形状、轮廓、方向、位置和跳动的极限偏差。可以通过特征控制框来添加形位公差，这些框会包含一个标注的所有公差信息。特征控制框至少由两个组件组成。第一个特征控制框包含一个几何特征符号，表示应用公差的几何特征，例如位置、轮廓、形状、方向或跳动。形状公差控制直线度、平面度、圆度和圆柱度；轮廓控制直线和表面。图 2.38 展示了特征为位置的形位公差。

图 2.38 形位公差示例

. NET 中的 FeatureControlFrame 类对应的是形位公差。与前面的引线一样，你可以先用该类的默认构造函数创建一个形位公差对象，然后调用 Text 和 Location 属性分别设置构成公差符号的文字字符串和图形中放置公差的位置。

创建完公差后，你可以使用 FeatureControlFrame 类的属性对其外观进行设置，其中，Dimclrd 表示形位公差符号的颜色；Dimclrt 表示公差文字的颜色；Dimgap 表示公差符号和文字之间的间隙；Dimtxt 表示公差文字的尺寸；Dimtxsty 表示公差文字的样式。

2.10.3 步骤

(1) 首先打开 DotNetARX 基本类库，新建一个类文件 DimTools.cs，用于封装与引线及形位公差有关的操作，在 DimTools 类代码的顶部导入 ApplicationServices 和 DatabaseServices 命名空间，修改类的声明如下：

public static class DimTools

(2) 在 DimTools 类中添加 ArrowBlock 属性，用于获取或设置当前标注尺寸线末端显示的箭头块：

public static string ArrowBlock

// 获取 DIMBLK 系统变量值，它表示尺寸线末端显示的箭头块

get return Application. GetSystemvariable ("DIMBLK"). ToString ()

set

// 设置 DIMBLK 系统变量值

Application. SetSystemvariable ("DIMBLK", value);

DIMBLK 系统变量表示当前尺寸线末端显示的箭头块，因此上面的代码使用了 Application 类的 GetSystem Variable 或 SetSystem Variable 来操作该变量值。

(3) 在 DimTools 类中添加 GetArrowObjectId 函数，用于获取箭头块的 ObjectId (db 参数表示数据库对象，arrowName 参数表示箭头块的名称）：



(4) 为了方便代码的编写，在 DimTools 类的上方添加名为 DimArrowBlock 结构，将

AutoCAD 自带的箭头符号进行封装：

public struct DimArrowBlock

public static readonly string C1 osedFilled: =""; // 实心闭合

public static readonly string Dot="_DOT"; //

为了节省篇幅，上面代码中只列出了 2 个箭头符号，其余符号的代码请按图 2.39 中的赋

值语句进行添加。

图实心闭合 ClosedFilled=-「「倒 30 度角 Angle30="OPEN30"

E 空心闭合 ClosedBlank="CLOSEDBLANK"E 小点 DotSmall="DOTSMALL"

☐闭合 Closed="CLOSED「西空心点 DotBlank="DOTBLANK"

围点 Dot="DOT「回空心小点 DotSmallBlank="SMALL"

☑建筑标记 ArchitecturalTick=」ARCHTICK「回方框 Box="BOXBLANK"

☑倾斜 Oblique="OBLIQUE「口实心方框 BoxFilled="BOXFILLED"

@打开 Open="OPEN" ☒基准三角形 Triangle="DATUMBLAN"

3 指示原点 Origin=」ORIGIN"☑实心基准三角形 TriangleFilled="DATUMFILLED"

@指示原点 2 Origin22="ORIGIN2" ☑积分 Integral="INTEGRAL"

a 直角 RightAngle="OPEN90" 口无 None="NONE"

图 2.39 常用箭头符号

(5) 在 DimTools 类中添加 CreateTolerance 函数，用于设置形位公差值：

public static void CreateTolerance (this FeatureControlFrame f frame, string geometricSym, string torlerance, string firstDatum, string secondDatum, string thirdDatum)

if (frame==null) return; // 特征控制框对象必须已定义，否则返回

// 设置形位公差值，各组成部分用竖线（V）分隔

frame.Text=geometricSym+「号 v"+, torlerance+「号号 v"+

firstDatum+「号号 v"+secondDatum+「号号 v"+thirdDatum;

函数中的 frame 参数表示形位公差特征控制框对象；geometricSym 参数表示几何特征符号，用于公差的几何特征，例如位置、轮廓、形状、方向或跳动；torlerance 参数表示公差值；firstDatum 参数表示第一级基准要素；secondDatum 参数表示第二级基准要素；thirdDatum 参数表示第三级基准要素。

(6) 为了方便代码的编写，在 DimTools 类的上方添加名为 DimFormatCode 结构，将所有 AutoCAD 支持的形位公差符号封装到一个结构类型中：

public struct DimFormatCode

pub1 ic static readonly string Angular=g"(\Fgdt;"+"a}"; // 倾斜度（∠）

每一种形位公差符号的格式都是 {Fgdt: X｝，其中 X 表示格式代码，图 2.40 列出了所有的公差符号及其对应的格式代码。为了节省篇幅，上面代码中只例出了倾斜度（∠）符号，其余公差符号的代码请参考配书光盘中 DotNetARX 目录下 DimTools.cs 文件中的 DimFormatCode 结构的定义。

倾斜度 a 位置度 ⑤不考虑特征尺寸 s

垂直度 b 线轮廓度 k 全跳动度

平面度 c ①最小实体要求直线度

面轮廓度 d @最大实体要求 m 柱形沉孔 V

圆度 e 心公差直径 n 埋头孔 w

平行度 f 口正方形 0 沉孔深度 ⅹ

圆柱度 g ® 延伸公差带 p 锥形接续器 y

圆跳动度 h 中心线 9 锥度

对称度同轴度 r

图 2.40 所有的形位公差符号

(7) 编译 DotNetARX 基本类库，然后打开本章的解决方案 Chap02, 加入一个新的类库 项目 Leaders,。添加对 acbdmgd. dl、acmgd. dl 和 DotNetARX. Dl 的引用，并将前二者的「复制本地」属性改为 False，将 Class1 类更名为 Leaders，并导入 DatabaseServices、Geometry、Runtime 和 DotNetARX 命名空间，在 Leaders 类中注册 AddLeader 命令，用于添加一条引线，其实现代码如下：



上面代码首先创建了一个直径为 0.219 的小圆，然后创建一个多行文本作为引线的注释对象，接着添加一条从多行文本指向小圆的引线，并设置其文字偏移和箭头大小，最后将引线与多行文本进行关联。

代码中多行文本的内容字符串中部分使用了本章第 6 节的 TextSpecialSymbol 自定义结构中的 Diameter（表示直径符号中）和 Tolerance 字段（表示公差符号士）。

(8) 在 Leaders 类中注册 AddMLeader 命令，用于添加由两条单引线组成的多重引线，其实现代码如下：



上面的代码中应注意以下 2 点：

》由于多重引线的第二条单引线只指定了头点，其终点将使用前一条单引线的终点。》注释对象会随着多重引线一起被加入到图形中，因此你不必手工加入注释对象。（9) 在 Leaders 类中注册 AddRoadMLeader 命令，用多条多重引线表示道路的组成部分（道路中心线、机动车道、人行道、绿化带），其实现代码如下：

代码首先加入 AutoCAD 自带的「点」符号箭头块，然后创建表示道路的组成部分（道路中心线、机动车道、人行道、绿化带）的 4 条多重引线并将其添加到图形中，最后设置多重引线的外观。

MLeader 类的 ArrowSize 属性表示多重引线的箭头大小，DoglegLength 属性表示基线的长度，TextAttachmentType 属性表示多重引线的基线连接到注释文字的方式，它是 TextAttachmentType 类型的枚举，取值可以为 AttachmentTopOfTop（第一行顶部）、AttachmentMiddleOfTop（第一行中间）、AttachmentMiddle（文字中间）、AttachmentMiddleOfBottom（最后一行中间）、AttachmentBottomOfBottom（最后一行底部）、AttachmentBottomLine（最后一行底部并加下画线）、AttachmentBottomOfTopLine（第一行底部并加下画线）、AttachmentBottomOfTop（第一行底部）、AttachmentAllLine（第一行底部并且所有文字都加下画线）。

多重引线的箭头大小、基线长度等属性的设置，必须放在将多重引线加入到图形后，否则这些属性仍然会被系统赋值为图形数据库的当前值。

(l0) 在 Leaders 类中注册 AddTolerance 命令，用于添加形位公差：



2.10.4 效果

编译程序，启动 AutoCAD2008, 用 NetLoad 命令加载生成的 DLL 文件，分别执行 AddLeader 和 AddTolerance 命令，得到如图 2.41 所示的结果。

分别执行 AddMLeader 和 AddRoadMLeader 命令，得到如图 2.42 所示的结果。

绿化带

人行道

机动车道

道路中心线

4×f0.219±0.005

⊕p0.20@A@B③c① 多重引线示例

图 2.41 引线与形位公差图 2.42 多重引线

由于前面的引线与形位公差的尺寸太小，因此你必须使用 Z00m 命令才能观察到上图的结果。

2.10.5, 小结

学习本节的内容之后，应该熟练掌握下面的知识点：》引线和多重引线的创建。

》如何修改多重引线的箭头类型与尺寸。》如何修改多重引线的基线长度。

》如何为多重引线的注释文字添加下画线。》形位公差的创建。


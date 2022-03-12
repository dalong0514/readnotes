## 记忆时间

## 卡片

### 0101. 主题卡 ——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡 ——

根据反常识，再补充三个证据——就产生三张术语卡。

### 0202. 术语卡 ——

### 0203. 术语卡 ——

### 0301. 人名卡 ——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

### 0401. 金句卡 ——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 数据信息卡 —— ObjectARX、ObjectARX Wizards、AutoCAD .NET Wizards 三者关系

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

### 0601. 任意卡 ——

最后还有一张任意卡，记录个人阅读感想。



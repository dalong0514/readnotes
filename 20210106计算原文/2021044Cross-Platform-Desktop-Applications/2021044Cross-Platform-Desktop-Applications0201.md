# 0201. Laying the foundation for your first desktop application

This chapter covers: 1) Building a file explorer in both NW.js and Electron. 2) Setting up your application  Structuring your application's files  Understanding how the user interface of the application works  Accessing the filesystem in Node.js

As developers, we often forget how lucky we are to work in an industry where the tools are readily available and free or relatively inexpensive to get ahold of. In this chapter, we'll get to grips with building desktop applications through creating a file explorer application. We'll look at how the app is built with both NW.js and Electron so that we can compare and contrast the ways in which they approach desktop applications.

Grab a cup of tea or coffee, a pen and paper, and settle in for some programming.

为你的首款桌面应用搭建基础架构

本章要点：1）使用 NW.js 和 Electron 分别构建一个文件浏览器应用。2）对应用进行设置。3）组织应用程序文件。4）理解应用界面的工作原理。5）使用 Node.js 访问文件系统。

作为开发者，我们经常会忘却自己身处在一个这样幸福的环境中：许多工具都是现成的，可以免费或者以相对较低的成本就能够获取到。在本章中，我们将会通过构建一个文件浏览器应用了解如何构建桌面应用。我们会用 NW.js 和 Electron 分别构建同一个应用，从而来比较使用这两个框架在构建桌面应用时有何异同。

准备一杯茶或者咖啡、一支笔、一张纸，我们这就开始编程吧。

## 2.1 What we're going to build

Whether you use a Windows PC, a Mac, or Linux, there are a few things common to all of them—they store files organized in folders, and they all have their own take on how to organize files in folders, as well as how you find and display those files to the user. This isn't a problem for people who use only one OS, but those who have to learn to use a new OS (such as when going to work at a new organization) can struggle to get their head around how to do simple tasks like rename a folder, or find out where the file that they saved to their computer is located.

It feels fitting to approach the idea of making a file explorer that works the same across all OSs, so that's what we'll build: a file explorer.

2.1 我们将构建什么应用

不论你用的是 Windows 或者 Mac 又或者是 Linux，它们都有一些共同之处 —— 它们都以文件夹的形式来组织文件，都有各自组织文件的方式，以及都有如何查询和显示那些文件给用户的方法。这对于只用一种操作系统的人来说不是什么问题，但对那些还得学用新系统的人（比如到了新的工作环境时）而言，诸如如何对文件夹进行重命名、如何找到保存在计算机中的文件这样简单的操作都可能会让他们头痛不已。

这样看来，做一款跨系统的文件浏览器是一个不错的主意，是的，没错，这正是我们准备要做的：一款文件浏览器应用。

### 2.1.1 Introducing Lorikeet, the file explorer

There's a common joke in developer circles that says naming things is the second hard problem in computer science (caching being the first hard problem). Sometimes it's nice to take inspiration from nature, so we'll name the file explorer Lorikeet, after the colorful native Australian bird.

Lorikeet is a file explorer with the following goals:

 Allow users to browse folders and find files  Allow users to open the file(s) with their default app

These are relatively simple goals, but implementing features to support them will provide enough scope to help you become familiar with building a desktop application. Building Lorikeet will also help demonstrate the different approaches that NW.js and Electron offer for developing desktop applications.

Building a desktop application is a lengthy process consisting of many steps: constructing user journeys, creating wireframes, writing tests, fleshing out the wireframes, writing code, and making sure that the app works as intended. For the sake of learning about NW.js and Electron, we'll work off of the basis that we have some user journeys and wireframes for the file explorer and focus on building a functional version of it.

You'll flesh out the features in the wireframes one by one, which helps to provide a natural flow to building the app, and gives you a chance to see where the code lives and what it does. Figure 2.1 shows a wireframe.

Figure 2.1 Wireframe of the file explorer app you'll build

With this wireframe, you take the app and break it down into separate features, helping you to implement the app one feature at a time. The first feature to work on is where the user begins to use the app—in this case, the start screen. But before you can do that, you need to create an app to store the code in.

文件浏览器 —— Lorikeet 介绍

程序员界有一个从熟知的玩笑是这样说的：命名是计算机科学中第二难的事情（缓存是头等难题）。有时候，从大自然获取灵感是很不错的思路，所以我们将这款文件浏览器命名为 Lorikeet，来源于澳大利亚的一种漂亮的小鹦鹉。

Lorikeet 这款文件浏览器将具备以下功能：1）用户浏览文件夹和查找文件。2）用户可以使用默认的应用程序打开文件。

尽管这些功能听上去很简单，但要实现它们需要大量的相关技术知识，这将帮助你熟悉如何构建一个桌面应用。构建 Lorikeet 的过程中也会展示 NW.js 和 Electron 在开发桌面应用方面的异同之处。

构建一个桌面应用工序繁杂：构建用户使用路径、创建线框图、编写测试、更新线框图、编码、确认应用工作正确。考虑到以学习 NW.js 和 Electron 为主，我们不介绍如何构建用户路径以及线框图这些基本的东西，关注在构建一个可用的版本。

线框图会随着功能的增加相应地进行修改，这有助于你了解真实情况下构建应用的流程，也能让你明白具体代码的作用。图 2.1 展示了线框图。

根据这个线框图，我们将应用划分为几个功能，这样有助于我们逐个功能地去实现。首先我们要实现的功能是用户使用应用的入口 —— 在本例中就是我们的启动界面。不过在动手做之前，先得创建应用来存放代码。

图 2.1 即将构建的文件浏览器应用的线框图

## 2.2 Creating the app

As you saw in chapter 1, it's relatively easy to get started with creating desktop applications with either NW.js or Electron. Regardless of which framework you begin to build the app with, you'll need to have Node.js installed (a quick and simple process you can do in a minute). To see how to install Node.js on your computer, see “Installing Node.js” in the appendix.

Once you have Node.js installed on your computer, the next step is to install both of the desktop application frameworks on your computer (if you haven't already).

2.2 创建应用

如第 1 章中所介绍的，不论是用 NW.js 或是 Electron，创建一个桌面应用都是比较简单的。不管你用哪个框架构建应用，都需要先安装 Node.js （这非常容易，1 分钟就可装完）。要了解如何在你的计算机中安装 Node.js，可以参见附录 A。安装好 Node.js 后，接下来就要在你的计算机中安装桌面应用开发框架了（如果你还没有安装的话）。

### 2.2.1 Installing NW.js and Electron

If you've already installed NW.js and Electron as explained in chapter 1, please skip to section 2.2.2. If not, you can run the following commands in the Terminal. For NW.js, run the following command to install NW.js as a global module:

```
npm install -g nw
```

For Electron, run the following command to install Electron as a global module:

```
npm install -g electron
```

Once they're installed, you can proceed to build the NW.js version of the Lorikeet application.

2.2.1 安装 NW.js 和 Electron

如果像第 1 章介绍的那样，你已经安装好了 NW.js 和 Electron，那请直接跳至 2.2.2 节。如果还没有，你可以在终端程序中运行如下命令。对于 NW.js，运行如下命令来全局安装 NW.js：

```
npm install -g nw
```

对于 Electron，运行如下命令来全局安装 Electron：

```
npm install -g electron
```

安装好之后，我们开始用 NW.js 来构建 NW.js 版本的 Lorikeet 应用。

### 2.2.2 Creating the files and folders for the NW.js-powered app

The next step is to create a folder that will store the code for your app. Choose a location on your computer where you like to store your code work, and run the following command to create a folder named lorikeet-nwjs:

mkdir lorikeet-nwjs

Once the folder (or directory, as some developers call it) is created, the next step is to create a package.json file for the app. This is Node.js's equivalent of a manifest file, where you store configuration information for the app. First, create the file inside the application folder:

cd lorikeet-nwjs touch package.json

Running on Windows?

If so, there isn't a touch command. What you can do instead is simply create the file using a code editor such as Notepad++ or even GitHub's Atom.

Now that you have a package.json file that you can edit, you can use whatever text editor you like to open the package.json file and insert the following code into it:

```
{

"name": "lorikeet", "version": "1.0.0", "main": "index.html"

}
```

The package.json file follows the same conventions used for creating modules that are then used in Node.js applications via npm. The name field has the name of the application, and must not contain spaces. The version field contains the version of the software, which we call 1.0.0 in accordance with a versioning format known as semantic versioning (also known as SemVer). The main field is used to tell NW.js what file to load when it's booted—in this case, the index.html file. These are the minimum requirements that NW.js has for the package.json file before it can load an application. You haven't yet created the web page that's loaded by NW.js, so you should probably create that next.

The index.html file is a pretty standard example for the moment. To create it, run the following command in your command-line tool (or create the file with Notepad++/Atom in Windows):

touch index.html

Once that's done, using your favorite text editor, insert the code in the following listing into the index.html file.

Listing 2.1

Adding the index.html file's contents for the NW.js app

<html> <head> <title>Lorikeet</title> </head> <body> <h1>Welcome to Lorikeet</h1> </body> </html>

Now that the index.html file is created, you're in a position to make NW.js run the app. To do that, simply run the following command in the Terminal, or your Command Prompt/PowerShell in Windows:

This will load the NW.js app. Because no further arguments were passed to the command, NW.js will inspect the files located in the current working directory where the command was run (in this case, the lorikeet-nwjs folder) and search for a package.json file. When it finds the package.json file, it will then load that file. The package.json file's main field will indicate to NW.js to load the index.html file in the app, which it then does, and you should see the screen shown in figure 2.2.

Figure 2.2 NW.js running a bare-minimum app. The app displays the contents of the index.html file, which means it's working as expected so far. Later in the chapter, you'll replace this simple HTML with the UI that makes up the app.

The title of the app window is loaded from the value inside the <title> element in the index.html file. You can edit the value of that field, save the change to the file, and run the application again from the command line to see the changes.

Can I load the index.html file in a web browser?

You can try, but any code that's calling out to NW.js's APIs or to Node.js code will result in a JavaScript error, so it's best not to. Even though NW.js apps appear to be running inside an embedded web browser, the app is more sophisticated because it has access to both Node.js/NW.js APIs and the DOM in the same JavaScript context.

With one folder and two files in that folder, you have the main skeleton code that will get a bare-bones version of the application up and running. At this point, you can adjust the contents of the index.html file to change the UI that's displayed by the application, but before you do any more on the NW.js version of the application, let's take a look at how you can achieve the same bare-bones application version with Electron.

2.2.2 为 NW.js 版本的应用创建文件和文件夹

接下来，为应用创建一个文件夹来存放代码。在你的计算机中选择一个你喜欢存放代码的位置，运行如下命令创建一个名为 lorikeet-nwjs 的文件夹：

```
mkdir lorikeet-nwjs
```

文件夹（有些开发者称之为「目录」）创建好后，接下来为应用创建 package. json 文件。在 Node.js 中，这和 manifest 文件一样，用来保存应用的配置信息。首先，在应用文件夹中创建一个文件：

```
cd lorikeet-nwjs
touch package.js
```

在 Windows 上运行

如果你用的是 Windows，那么是没有 touch 命令的。你可以用诸如 Notepad++ 或者 GitHub 的 Atom 代码编辑器来创建文件。

现在可以为 package.json 文件添加内容了，你可以用你喜欢的文本编辑器打开 package.json 文件，并插入如下内容：

这里的 package.json 文件和在 Node.js 应用中创建 npm 模块时一样，遵循同样的规则。name 字段表示应用的名字，不能包含空格。version 字段表示应用的版本号，本例中是 1.0.0，版本号命名规则遵循语义化版本（大家熟知的 SemVer）。main 字段表示了 NW.js 需要加载的应用启动文件 —— 本例中为 index.html 文件。要让 NW.js 启动应用程序，至少要在 package.json 文件中包含以上这些字段。接下来我们来创建 NW.js 需要加载的 Web 页面。

一般我们会将页面命名为 index.html 文件。使用命令行工具（或者在 Windows 系统中使用 Notepad++ 或者 Atom）运行如下命令即可创建：

```
touch index.html
```

完成后，使用你喜欢的文本编辑器，将代码清单 2.1 中的内容插入 index.html 文件。

代码清单 2.1 为 NW.js 应用添加 index.html 文件内容

现在 index.html 文件创建好了，接下来要让 NW.js 将应用程序运行起来。这很简单，只要在终端、Windows 系统中的命令提示符下或者 PowerShell 中运行如下命令即可：

```
nw .
```

该命令会加载 NW.js 应用。如果没有为该命令指定任何参数，NW.js 就会在执行上述命令所在的当前工作目录中（本例中就是 lorikeet-nwjs 文件夹）查找 package. json 文件。找到 package.json 文件后，就会加载该文件。package.json 中的 main 字段会告诉 NW.js 去加载应用中的 index.html 文件，加载完成后就会看到图 2.2 所示的界面。

图 2.2 NW.js 正在运行一个很简单的应用。应用显示了 index.html 文件的内容，意味着目前为止工作正常。在本章后续部分，我们会将这个简单的 HTML 替换为应用所需的 UI

视窗的标题是通过 index.html 页面中的 `<title>` 标签中的内容指定的。你可以编辑该字段值，保存文件，并从命令行再次运行应用来查看修改后的效果。

我可以通过 Web 浏览器加载 index.html 文件吗

你可以试试，但是任何使用了 NW.js API 以及 Node.js 代码的都会导致 JavaScript 错误，所以最好还是不要这样操作。尽管 NW.js 应用看起来是运行在一个内嵌的 Web 浏览器中的，不过它本身复杂得多，因为它在同一个 JavaScript 上下文中既访问了 Node.js/NW.js API，又访问了 DOM。

有了一个文件夹和其中的两个文件，就拥有了最主要的基础代码，可以让一个最简单的应用运行起来了。接下来，可以修改 index.html 文件内容来改变应用的 UI，不过在动手进一步修改这个 NW.js 版本的应用前，让我们先来使用 Electron 创建一个同样的最简单的应用。

### 2.2.3 Creating the files and folders for the Electron-powered app

The Electron version of the application starts off very much in the same fashion. You'll begin by creating a folder named lorikeet-electron. You can do this by running this command in the Terminal/Command Prompt:

mkdir lorikeet-electron

This will create a folder named lorikeet-electron. This is the main application folder for the application, and inside it will be the application's files. Now you'll create the next file needed by the application, the package.json file. In your terminal or via your text editor, create a file named package.json inside the lorikeet-electron folder:

cd lorikeet-electron touch package.json

Once you have an empty package.json file, you'll move on to populating the file with the configuration needed by Electron. Inside the package.json file, add the following JSON configuration:

{

"name": "lorikeet", "version": "1.0.0", "main": "main.js"

}

The package.json file looks almost identical to the package.json file used by the NW.js version of the application, with one exception: the main property is different. In NW.js, the file that's loaded is an HTML file. In Electron, the file that's loaded is a JavaScript file. The file you load in the case of the Electron version of the application is called main.js.

The main.js file is responsible for loading the Electron application and any browser windows that it will display as part of that application. In your terminal or your text editor, create the file main.js and insert the following content.

The main.js file will result in loading the index.html file. Here, you create the index.html file and put the following contents into it:

<html> <head> <title>Lorikeet</title> </head> <body> <h1>Welcome to Lorikeet</h1> </body> </html>

Once you've saved the index.html file, you're in a position to run the Electron application from the command line. Go to the Terminal or Command Prompt and type the following command inside the lorikeet-electron folder to run the application:

cd lorikeet-electron electron .

If you run the application now, you should see something like figure 2.3.

Figure 2.3 The Lorikeet app running on Electron. This is what Electron apps look like by default—pretty much like the NW.js variant.

The Electron app looks almost identical to the NW.js app. The index.html file is exactly the same as the one used for the NW.js variant of the Lorikeet app, and to load the application from the command line is practically the same.

Having built the Lorikeet app's bare-bones application structure in both NW.js and Electron, you can see that they share some similar coding conventions—after all, as mentioned, Cheng Zhao worked on both NW.js and Electron. But they differ in terms of how they go about loading the app.

So far, I've shown you how to build and set up the Lorikeet app's skeleton of files and folders with both frameworks. The next stage is to start working on the first feature of the application that the user sees, as shown back in figure 2.1.

We'll continue to compare and contrast the approaches taken with both frameworks but share code where it's possible.

2.2.3 为 Electron 版本的应用创建文件和文件夹

创建 Electron 版的应用的步骤与用 NW.js 创建的非常相似。首先创建一个 lorikeet-electron 文件夹。可以在终端程序或者命令提示符应用中运行如下命令进行创建：

```
mkdir lorikeet-electron
```

上述命令会创建一个名为 lorikeet-electron 的文件夹。这是应用程序的主文件夹，在该文件夹中放置应用文件。接下来，创建应用所需的 package.json 文件。使用你的终端应用或者文本编辑器，在 lorikeet-electron 文件夹中创建一个名为 package. json 的文件：

```
cd lorikeet-electron
touch package.json
```

有了空的 package.json 文件后，接下来为该文件添加 Electron 应用所需的配置信息。在 package.json 文件中添加如下 JSON 格式的配置信息：

这里的 package.json 文件和 NW.js 版本所用的 package.json 文件大致相同，除了 main 属性有所不同。在 NW.js 中需要指定一个 HTML 文件。而在 Electron 中，则是一个 JavaScript 文件。在本例中，该文件为 main.js。

main.js 文件负责加载 Electron 应用以及任何应用所需的浏览器视窗。使用你的终端应用或者编辑器，创建 main.js 文件并插入代码清单 2.2 中的内容。

代码清单 2.2 Electron 版应用的 main.js 文件

main.js 文件最终会加载 index.html 文件。所以，创建 index.html 文件，并插入如下内容：

保存 index.html 文件后，就可以从命令行运行 Electron 应用了。在 lorikeetelectron 文件夹中使用终端应用或者命令提示符应用，输入如下命令来运行应用：

```
cd lorikeet-electron
electron .
```

运行后会看到如图 2.3 所示的样子。

Electron 版的应用和 NW.js 版的应用非常相似。其中 index.html 文件和 NW.js 版的完全一样，而且从命令行加载应用的方式也完全一致。

图 2.3 Electron 版的 Lorikeet 应用。这是 Electron 应用默认的样子 —— 和 NW.js 版的非常相似

使用 NW.js 和 Electron 构建了最简单的 Lorikeet 应用后，你可以发现它们有相同的编码规范 —— 值得一提的是，毕竟赵成在 NW.js 和 Electron 项目上都参与过开发。不过它们加载应用的方式有所不同。

至此，我已经给大家展示了如何使用两个框架构建最简单的 Lorikeet 应用。如此前图 2.1 所示，接下里我们开始实现应用的第一个功能。

在实现过程中，我们还会继续比较两个框架的异同，必要的时候也还会复用代码。

## 2.3 Implementing the start screen

The start screen has a number of components to it. We'll start with the display of the personal folder, as shown in figure 2.4.

Figure 2.4 The Lorikeet wireframe. Notice the circled item in the wireframe. This is the item you want to build first.

This is the first feature you'll flesh out in the UI and then implement in both versions of the Lorikeet app.

2.3 实现启动界面

启动界面由几个部分组成。我们先从展示用户个人文件夹信息开始，如图 2.4 所示。

图 2.4 Lorikeet 线框图。注意其中画圈的部分，我们先来实现这部分

这是我们要实现的第一个功能，会在两个版本的 Lorikeet 应用中都进行实现。

### 2.3.1 Displaying the user's personal folder in the toolbar

Three parts comprise this feature:

 The HTML that makes up the toolbar and the personal folder  The CSS that applies the layout and styling of the toolbar and the personal folder  The JavaScript that will discover what the user's personal folder is and display it in the UI

The good news is that the HTML, CSS, and even the JavaScript needed for this feature are exactly the same in both the NW.js and Electron versions of the Lorikeet app. In this case, you'll be able to show it once but use the same code in both applications. Let's start with the HTML.

ADDING THE HTML FOR THE TOOLBAR AND PERSONAL FOLDER

The index.html file is the main screen for both the NW.js and Electron versions of our applications. For both versions of the application, open the index.html file in a text editor and change it to what you see in the next listing.

Once you've done this for both applications, we can move on to creating the CSS stylesheets that will manage the layout and styling of the toolbar and personal folder.

ADDING THE CSS FOR THE TOOLBAR AND PERSONAL FOLDER

Styling desktop applications is no different than styling web pages. CSS can be embedded inside the HTML for a page, but it's better to put it into a separate file so that you can see all the CSS styling in one place, as well as keep the index.html file readable.

Start by creating a file in the application called app.css at the same folder level as the index.html file. Next, add the CSS in the following listing to the app.css file.

Listing 2.4 Adding the toolbar and personal folder CSS to the app.css file

Now, you need to make sure that the app.css file will be loaded by the index.html file. In the index.html file, add a line to the index.html file so that it reads like the following listing.

After you've saved the index.html file with this change, you can either reload the NW.js and Electron applications (if you have them open and running) or load them again from the Terminal/Command Prompt with this:

cd lorikeet-electron && electron . cd lorikeet-nwjs && nw

Once you have reloaded the applications with the new code, you'll see that the UI is starting to take shape, as shown in figures 2.5 and 2.6.

Figure 2.5 The Lorikeet NW.js app with the toolbar and personal folder. The personal folder listing is blank, but we'll get around to making it appear soon.

Figure 2.6

The Lorikeet Electron app with the toolbar and personal folder

The toolbar and the personal folder are visible and styled, but what remains is to be able to discover what the path for the user's personal folder is and display that in the UI. This is the next step we'll take.

DISCOVERING THE USER'S PERSONAL FOLDER WITH NODE.JS

To display the path of the user's personal folder, you need a way to discover it, one that works across all OSs. On Mac OS, the user's personal folder tends to be located in the /Users/<username> folder with their username (mine is /Users/pauljensen). On Linux, the user's personal folder tends to be in the /home/<username> folder, and on Windows 10 the it's located in the C: drive under the Users/<username> folder. If only OSs operated in a common, standard fashion!

Thankfully, this is accommodated in Node.js's ecosystem on npm packages. An npm module called osenv by Isaac Schlueter (former Node.js lead maintainer and the founder of npm) has a function that discovers and returns the user's personal folder (or home folder, as it's also known). To use this, you need to install the npm module in the application. Run the following command in the Terminal or Command Prompt to install the library (make sure to do this for both versions of the Lorikeet app):

npm install osenv --save

The –-save flag at the end of the command tells the npm command to add the module as a dependency in the package.json manifest file. If you open the package.json manifest file (say, in this case, for the NW.js variant of the application), you'll see the change, as shown next.

Listing 2.6

The modified package.json file

{

"name": "lorikeet", "version": "1.0.0", "main": "index.html", "dependencies": { "osenv": "^0.1.3" }

The new dependencies property, with osenv listed as module dependency for app

}

You'll also notice that there's a new folder that appears in the application folders for both applications, a folder called node_modules. This folder contains any locally installed npm modules that are installed for the application. If you browse the node_modules folder, you'll see a folder named osenv. This is where the osenv module's code has been installed.

With the osenv module installed, you now want to load the user's personal folder and display it in the personal folder UI element in the index.html file. This demonstrates one of the unique aspects of NW.js and Electron as Node.js desktop application frameworks: you can execute Node.js code directly in the index.html file. Don't believe me? Try this. Modify the index.html file so that the code looks like the next listing.

Listing 2.7

Displaying the user's personal folder to the index.html file

Make sure the index.html file is changed to this in both the NW.js and Electron versions of the Lorikeet app.

After you save the files, reload the applications using the technique shown earlier:

cd lorikeet-electron && electron . cd lorikeet-nwjs && nw

You can expect to see your personal folder listed in the personal folder UI element of the app, as shown in figures 2.7 and 2.8.

Figure 2.7 NW.js app

The user's personal folder displayed in the Lorikeet

Figure 2.7 is impressive. You can call Node.js directly in a script tag in the index.html file. How about Electron? Does it do the same? Check out figure 2.8.

Figure 2.8

The user's personal folder displayed in the Lorikeet Electron app

It does. Not only have you been able to call Node.js code inside a script tag in the index.html file, but you've been able to use a Node.js module from npm in the frontend part of your code. Plus, you've been able to use identical code across both NW.js and Electron so far, which goes to show how compatible they are, as well as why some projects have been so successful in being ported from NW.js to Electron (such as Light Table, for example).

Now that you've implemented the display of the user's personal folder in the toolbar, we should move on to implementing the next feature in the UI: the display of the user's files and folders in their personal folder.

2.3.2 Showing the user's files and folders in the UI

In the preceding section, we started off by creating the UI elements first and then populated the user's personal folder path in the UI element. For this feature, we'll work on getting ahold of a list of the user's files and folders first and then figure out from there how we display them in the UI of the application. For a quick reminder, figure 2.9 shows the UI element we're looking to implement.

Figure 2.9

The UI element we're looking to implement next in the app

To implement this UI feature, you need to do the following:

1

2

3

Get the list of files and folders at the user's personal folder path For each file/folder listing, find out if it's a file or a folder Pass that list of files/folders to the UI to be rendered as files with icons

You already have a way to get at the user's personal folder path. Now what you need is a way to get ahold of the list of files and folders at that path. Luckily for you, Node.js implements a standard library for querying the computer's filesystem, called fs. One of the functions available to get a list of files and folders is the readdir function, as documented at http://mng.bz/YR5B.

For both the NW.js and Electron versions of the Lorikeet app, you'll create an app.js file. This file will contain JavaScript code that can call Node.js as well as interact with the DOM. You'll use this file to help store the code that will display the list of files for you.

First, create an app.js file at the same folder level as the index.html and app.css files. Next, you'll move the code that loads the user's personal folder path into it. Add the following code to the app.js file:

'use strict'; const osenv = require('osenv'); function getUsersHomeFolder() { return osenv.home(); }

After adding the code to the app.js file, the next step is to include the app.js file as a script tag in the index.html and call the getUsersHomeFolder method in the DOM in place of the current call to the osenv module's home function. Change the index.html file so that it looks like the next listing.

Listing 2.8

Adding the app.js file to the index.html file

<html>

<head> <title>Lorikeet</title>

<link rel="stylesheet" href="app.css" />

<script src="app.js"></script>

</head> <body>

<div id="toolbar">

Includes app.js as script tag in index.html

<div id="current-folder">

<script> document.write(getUsersHomeFolder()); </script> </div> </div> </body> </html>

Calls app.js's getUsersHomeFolder function in place of direct call to Osenv module's home function

If you reload the applications, you'll see that they behave the same, which is exactly what you want. You can now start to add code to the app.js file for getting the list of the files. You'll start by requiring Node.js's filesystem module, which comes as part of Node.js's standard library, and then adding a new function called getFilesInFolder that will retrieve the files in the folder passed to it. After that, you'll create a function called main that will pass the user's personal folder into that function, and from the resulting list of files log the absolute paths for them out in the console.

Change the code in the app.js file so that it looks like the following.

Listing 2.9

Logging the list of files and folders in the user's personal folder

After saving the app.js file, the next step is to see what happens when you run the code. Reload the application. In the case of Electron, if you toggle showing the developer tools for the application, you can expect to see the list of files in the Console tab, as shown in figure 2.10.

Figure 2.10 The Lorikeet Electron app showing the list of files being logged to the Console tab. To see the list of files on your computer, click View > Toggle Developer Tools.

You now know that you can get at the list of files in the user's personal folder. The next challenge is to figure out what the name and file/folder type is for each file in the list and to then display these items in the UI as a list of files and folders with icons.

Your goal is to be able to take a list of files and pass them through another function in Node.js's file system API. This will identify whether they're files or directories, as well as what their names and full file paths are. Do the following:

1

2

3

Use the fs.stat function method, as documented at http://mng.bz/46U5. Use the async module to handle calling a series of asynchronous functions and collecting their results.

Pass the list of results to another function that will handle their display.

In the app.js file for both variants of the Lorikeet app, install the async module via the Terminal or Command Prompt:

npm install async --save

After installing the async module to both applications, the next step is to change the app.js code so that it will detect what the files in the user's personal folder are. Change the code to that shown next.

Listing 2.10

Changing the app.js code to detect file types

With the app.js file saved to the computer and the applications reloaded, you'll see something like figure 2.11 in the developer tools.

Not only do you now have the application returning the list of files in the user's personal folder, but you have it in a data structure that has the filename and file type included as well. This sets you up perfectly for the next step in implementing the UI feature: displaying filenames and icons in the application's UI.

VISUALLY DISPLAYING THE FILES AND FOLDERS

In the previous code for the app.js file, you created a function called displayFiles. You want to use this function to handle displaying the files as names and icons in the UI. Because there are many files to be rendered in the UI, you'll use an HTML template for each file and then render an instance of that template to the UI.

You'll start by adding the HTML template to the index.html file, as well as a div element to contain the files that are being displayed. Change the index.html file so that it looks like the following listing.

Listing 2.11

Adding the file template and main area to the index.html file

The purpose of the template element is to hold a copy of the HTML that you'd like to render for each file, and the div element is where the template instances will be rendered and stored for each file that you find in the user's personal folder. You'll then add some JavaScript to the app.js file that will handle creating an instance of the template and adding it to the UI. Adjust the app.js file so that the code reads like the next listing.

Listing 2.12

Rendering the template instances in the UI via the app.js file

Now that HTML is being added to the app to handle the display of the files and the folders in the application, you want to make sure that the list of files and folders look styled and are displayed in a grid fashion. In the app.css file, change the CSS to match the following code.

Listing 2.13

Adding styling to the app.css file for displaying the files

This CSS will ensure that the items are displayed in a clear and grid-like fashion and that the toolbar will remain in a fixed position, visible above the files in the app as the main area div element is scrolled by the user.

You're almost there. All that's left to do is add the icons for the different file types to the application folder. Create a folder called images in the application folders with these commands in either the Terminal or the Command Prompt:

cd lorikeet-electron mkdir images cd ../lorikeet-nwjs mkdir images

Now, you can add some images for the file and directory icons. Inside the images folder, you'll insert two images named file.svg and directory.svg. The files are sourced from the OpenClipArt.org site from these URLs:

 https://openclipart.org/detail/137155/folder-icon  https://openclipart.org/detail/83893/file-icon

Save the files in the images folder (under the names file.svg for the file icon and directory.svg for the folder icon) and reload the application, and you should see something like figures 2.12 and 2.13.

Figure 2.12 The Lorikeet NW.js app showing the files and folders. Here, you see the beginnings of what looks like a file explorer application.

The file type property of the files is used to determine whether the icon is for a file or for a directory. This helps you easily distinguish files from folders. You'll also see that the file/folder names are displayed in alphanumerical order. In figure 2.12, dotfiles and hidden folders can be seen that would otherwise be hidden by other file explorer applications. Figure 2.13 shows the Electron Lorikeet app.

Figure 2.13

The Lorikeet Electron app showing files and folders

The Electron variant of the Lorikeet app looks almost identical to the NW.js version. All in all, the results look good, and that's the end of the exercise for this chapter.

2.3.1 在工具条中展示用户个人文件夹信息

实现该功能可分为三部分内容：1）HTML 负责构建工具条和用户个人文件夹信息。2）CSS 负责布局工具条和用户个人文件夹展示上的布局以及样式。3）JavaScript 负责找到用户个人文件夹信息在哪里并在 UI 上展示出来。






好在实现这个功能所用到的 HTML、CSS 和 JavaScript 内容在 NW.js 版本和 Electron 版本的 Lorikeet 应用中是一样的。在本例中，你将能够展示一次这部分代码，但在两个版本的应用中使用的是相同的代码。让我们从 HTML 代码开始。

添加展示工具条和个人文件夹的 HTML 代码

index.html 是用于展示我们 NW.js 和 Electron 两个版本应用的主屏幕。在文本编辑器中打开两个版本应用中的 index.html 文件，并将内容改为代码清单 2.3 所示的那样。

代码清单 2.3 在 index.html 文件中添加展示工具条和与用户个人文件夹信息相关的内容

在两个版本的应用中都修改完成后，我们来创建 CSS 代码来控制工具条和用户个人文件夹信息展示时候的布局和样式。

为工具条和用户个人文件夹信息添加 CSS 代码

为桌面应用添加样式和为 Web 页面添加样式没什么区别。CSS 可以直接内嵌在页面的 HTML 中，不过最好还是把它放在另外一个单独的文件中，这样既可以在同一个地方看到所有的 CSS 代码，也可以保持 index.html 的可读性。

我们先来创建一个名为 app.css 的文件，将其放在存放 index.html 文件的目录中。然后，将代码清单 2.4 中的内容插入 app.css 文件。

代码清单 2.4 在用于工具条和用户个人信息的 CSS 代码添加到 app.css 文件中



现在要确保 app.css 文件会被 index.html 文件加载。在 index.html 文件中，如代码清单 2.5 所示添加一行代码。

代码清单 2.5 在 index.html 文件中添加一个 link 标签，指向 app.css 文件

保存修改完的 index.html 文件，接下来你可以重新加载 NW.js 和 Electron 版应用（如果已经在运行了的话）或者从终端应用或者命令提示符应用输入如下命令再次运行：

cd lorikeet-electron && electron .

cd lorikeet-nwjs && nw

使用最新代码重新运行后，你会看到界面发生了变化，如图 2.5 和图 2.6 所示。

▲图 2.5 NW.js 版本的 Lorikeet 应用，包含了一个工具条和用户个人文件夹信息。其中用户个人文件夹信息还是空白的，不过我们很快就会让它显示内容

图 2.6 Electron 版的 Lorikeet 应用，包含了工具条和用户个人文件夹信息

工具条和用户个人文件夹信息都显示出来了，而且也有指定的样式，不过还需要找到用户个人文件夹的路径并将其显示在界面上。这部分内容接下来会做介绍。

通过 Node.js 找到用户个人文件夹所在的路径

要显示用户个人文件夹的路径，我们先得想办法获取到该路径，而且该方法要支持所有操作系统。在 Mac OS 中，用户个人文件夹位于 / Users/<username>，这里 username 是用户名（我的是 /Users/pauljensen）。在 Linux 中，用户个人文件夹位于 /home/<username>，在 Windows 10 中，则位于 C 盘的 /Users/<username>。不同操作系统位置不同！

幸运的是，这个问题已经在 Node.js 生态中通过 npm 模块解决了。有一个 Isaac Schlueter （前 Node.js 维护者以及 npm 作者）开发的模块，叫 osenv，其中有一个函数会返回用户个人文件夹（或者叫 home 目录）。要使用该模块，你需要先在应用中安装它，在终端应用或者命令提示符应用中运行如下命令可进行安装（别忘了在两个版本的 Lorikeet 应用中都执行如下命令）：

npm install osenv --save

命令最后的 --save 标志是告诉 npm 将该模块作为依赖的模块添加到 package. json 文件中。如果你打开 package.json 文件（以 NW.js 版本的应用为例），就会看到其内容发生了改变，如代码清单 2.6 所示。

代码清单 2.6 修改后的 package.json 文件

你还会发现在两个版本的应用文件夹下都多了一个新的名为 node_modules 的文件夹。所有为应用安装的本地 npm 模块都会放在这个文件夹中。如果打开 node_modules 文件夹，就会看到一个名为 osenv 的文件夹，这就是 osenv 模块安装的位置。

安装好 osenv 模块后，我们就可以找到用户个人文件夹并将其信息在 index.html 文件中对应的界面上显示出来。这也证明了 NW.js 和 Electron 作为 Node.js 桌面应用开发框架独特的功能之一：可以在 index.html 文件中直接执行 Node.js 代码。不信？那就试试吧。将 index.html 文件修改为代码清单 2.7 所示的内容。

代码清单 2.7 在 index.html 文件中显示用户个人文件夹信息

确保 NW.js 和 Electron 版的 Lorikeet 应用的 index.html 都修改了。保存修改后，根据此前介绍过的，运行如下命令重新启动应用：

cd lorikeet-electron && electron .

cd lorikeet-nwjs && nw

现在应该能看到你的个人文件夹信息已经显示在应用中对应的界面上了，如图 2.7 和图 2.8 所示。

图 2.7 NW.js 版的 Lorikeet 应用显示的用户个人文件夹信息

图 2.7 显示得超赞。你可以在 index.html 的 <script> 标签中直接调用 Node.js。那么 Electron 怎么样的？是否也一样呢？请看图 2.8。

图 2.8 Electron 版的 Lorikeet 应用显示的用户个人文件夹信息

没错。正如你所见，不仅可以在 index.html 文件中的 <script> 标签中调用 Node.js 代码，还可以在前端代码中使用通过 npm 安装的 Node.js 模块。不仅如此，至此我们的 NW.js 和 Electron 都用了同样的代码，由此可见两者兼容性有多好，这也是为什么很多项目都可以很方便地从 NW.js 切换到 Electron（比如，Light Table 应用）。

现在已经实现了在工具条中显示用户个人文件夹信息了，接下来实现下一个功能：将用户个人文件夹中的文件和文件夹显示出来。

2.3.2 显示用户个人文件夹中的文件和文件夹

在前面的内容中，我们先创建界面元素，然后将用户个人文件夹信息显示在界面上。对于这次这个功能，我们先要获取到用户个人文件夹中的文件和文件夹信息，再想办法把它们显示在界面上。回忆一下，图 2.9 显示的是我们要实现的样子。

图 2.9 我们接下来要实现的样子

要实现该功能，我们需要做以下这些事情：

1． 获取到用户个人文件夹中的文件和文件夹列表信息。

2． 对每个文件或者文件夹，判断它是文件还是文件夹。

3． 将文件或文件夹列表信息显示到界面上，并用对应的图标区分出来。

你已经获取到用户个人文件夹的路径了，现在需要做的就是想办法获取到该路径下的文件和文件夹列表信息。幸运的是，Node.js 提供了一个名为 fs 的标准库，可用来查询计算机中的文件系统。该标准库中有一个方法叫 readdir，用它来获取某个路径下的文件和文件夹信息，具体文档参见 http://mng.bz/YR5B。

对 NW.js 和 Electron 版的 Lorikeet 应用都创建一个 app.js 文件。该文件中的 JavaScript 代码可以调用 Node.js，也可以操作 DOM。我们将获取文件和文件夹列表信息的代码就放在这个文件中。

首先，在 index.html 和 app.css 同目录下创建一个 app.js 文件。然后将获取用户个人文件夹信息的代码移到该文件中。将如下代码插入 app.js 文件：



添加完上述代码后，接下来在 index.html 中用一个 <script> 标签将 app.js 文件加载进来，并在 DOM 位置调用 app.js 中的 getUsersHomeFolder 方法。将 index.html 修改为如代码清单 2.8 所示的内容。

代码清单 2.8 将 app.js 添加到 index.html 文件中

重启应用就会发现，它们没有任何区别，和预期的一样。现在可以往 app.js 中添加代码来获取文件列表了。首先加载 Node.js 的文件系统模块，它是 Node.js 标准库的一部分，紧接着添加一个新的函数叫 getFilesInFolder，用来获取传进来的文件夹下面的文件列表信息。然后再创建一个 main 函数，调用该函数并将用户个人文件夹路径作为参数传递进去，再将获取到的包含所有文件绝对路径的列表在控制台打印出来。

将 app.js 文件修改为如代码清单 2.9 所示的内容。

代码清单 2.9 将用户个人文件夹下的文件和文件夹列表打印出来

保存好 app.js 文件后，接下来重启应用来看看效果。在 Electron 应用中，如果打开应用的开发者工具，就能在其 Console 选项卡中看到打印出来的文件列表，如图 2.10 所示。

现在你已经知道如何获取用户个人文件夹下的文件列表了。接下来的问题是如何获取到文件名以及文件类型（是文件还是文件夹），并将它们以不同的图标在界面上显示出来。

你的目标是能够接收文件列表作为参数并将它们传递给 Node.js 文件系统 API 中的另一个函数。该函数能够识别是文件还是文件夹以及它们的名字和完整的路径。你需要完成下面三件事情：

1． 使用 fs.stat 函数，具体文档参见 http://mng.bz/46U5。

2． 使用 async 模块来处理调用一系列异步函数的情况并收集它们的结果。

3． 将结果列表传递给另外一个函数将它们显示出来。

图 2.10 Electron 版的 Lorikeet 应用在 Console 选项卡中将文件列表信息打印了出来。要在你的计算机中查看，单击 View->Toggle Developer Tools。

在两个版本的 Lorikeet 应用的 app.js 文件中，通过终端应用或者命令提示符应用安装 async 模块：

npm install async --save

为两个版本的应用都安装好 async 模块后，接下来修改 app.js 的代码，以实现获取用户个人文件夹中有哪些文件和文件夹的功能。将 app.js 的代码修改为如代码清单 2.10 所示的内容。

代码清单 2.10 修改 app.js 代码实现检查文件类型的功能

保存 app.js 并重启应用后，就会从开发者工具中看到图 2.11 所示的结果。

你现在不仅获取到了用户个人文件夹下的文件列表信息，而且还将文件名以及文件类型都保存在了数据结构中。有了这些，接下来实现将它们以对应的图标展示在界面上就变得事半功倍了。

图 2.11 开发者工具中的 Console 选项卡显示了文件列表信息。注意第一个展开的对象包含的类型是文件，第二个则是目录

视觉上显示文件和文件夹

在此前 app.js 的代码中，你创建了一个名为 displayFiles 的函数。打算用这个函数处理将文件名字以及对应的图标展示在界面上。由于要展示的文件很多，我们将为每个文件定义一套模板，然后为每个文件创建一个该模板的实例再渲染到界面上。

先在 index.html 文件中添加 HTML 模板，模板中包含一个 div 元素，其中包含了要显示的文件信息。把 index.html 文件修改为如代码清单 2.11 所示的样子。

代码清单 2.11 在 index.html 文件主内容区添加为展示文件信息的模板

上述 template 元素的目的是为每一个要渲染的文件信息定义一套 HTML 模板，真正被渲染的是模板实例中的 div 元素，它会将用户个人文件夹中的每个文件信息都显示出来。接下来需要在 app.js 中添加一些 JavaScript 代码，用来创建模板实例并添加到界面上。将 app.js 文件修改为如代码清单 2.12 所示的内容。

代码清单 2.12 通过 app.js 文件在界面上渲染模板实例

现在 HTML 已经添加好了，可以在应用中显示文件和文件夹信息了。接下来确保文件和文件夹信息以正确的样式显示，并且显示在栅格布局中。在 app.css 文件中，修改 CSS 代码为代码清单 2.13 所示的内容。

代码清单 2.13 在 app.css 文件中添加 CSS 代码，为显示的文件和文件夹信息定义样式

上述 CSS 代码确保了列表项显示在一个整洁的栅格布局中，其中工具条始终固定在顶部，在显示文件列表的主区域 div 元素的上方，用户可以对主区域进行滚动。

马上就要完成了。剩下的任务是在应用文件夹中为不同类型的文件添加对应的图标。使用终端应用或者命令提示符应用，通过运行如下命令，在应用文件夹中创建一个名为 images 的文件夹：

cd lorikeet-electron

mkdir imagescd ../lorikeet-nwjsmkdir images

现在，你可以为文件和文件夹添加对应的图标了。在 images 文件夹中，添加两张名为 file.svg 和 directory.svg 的图片。这两张图片来自 OpenClipArt.org 网站，可以通过如下 URL 获取：

■ https://openclipart.org/detail/137155/folder-icon

■ https://openclipart.org/detail/83893/file-icon

在 images 文件夹中保存这两张图片（ 文件图标使用 file.svg，文件夹图标使用 directory.svg），然后重启应用就会看到如图 2.12 和图 2.13 所示的样子了。

图 2.12 NW.js 版的 Lorikeet 应用展示了文件和文件夹信息。这看上去像一个文件浏览器应用的样子了

文件类型属性是用来决定使用文件图标还是文件夹图标的，这有助于你对文件和文件夹进行区分，而且文件和文件夹的名字是按照字母顺序进行排序的。在图 2.12 中，文件名以点开始的文件以及隐藏文件都显示出来了，而这些在其他文件浏览器应用中一般都不会显示。图 2.13 显示的是 Electron 版的 Lorikeet 应用。

图 2.13 Electron 版的 Lorikeet 应用显示了文件和文件夹信息

Electron 版和 NW.js 版的 Lorikeet 应用看上去几乎一模一样。总的来说，看上去还不错，至此，本章的练习就结束了。




## Summary

In this chapter, you began using NW.js and Electron for building the type of application that many people use with their computers on a daily basis. You've walked through the process of creating the applications from scratch and understand how you can approach the task of building an application feature-by-feature. Here are some of the things the chapter covered:

1 The best way to approach a wireframe is to tackle it one feature at a time.

2 Good semantics is encouraged as a way to relate features to the underlying code that supports it.

3 CSS is the prime way to style UI elements in NW.js and Electron desktop apps.  You can use Node.js and other third-party libraries with ease in your desktop application.

4 The approaches of NW.js and Electron allow for them to use almost the same code, but Electron requires a bit more code and a slightly different configuration in the package.json file.

What's been great is that in using the same code across both NW.js and Electron variants of the Lorikeet app, you've been able to see how similar the desktop application frameworks are, as well as notice the areas where they're different. This should give you the confidence that should you choose one framework for your application and find that it's not the right one for you, then it won't be too difficult to switch to using the other framework.

Another takeaway here is that you're able to use the same skills for building websites as for creating the UI for a desktop application, and that means getting up to speed quickly when building a desktop application.

In the next chapter, we'll expand on the work done here by adding the meaty parts of the application. We'll begin to explore the APIs of NW.js and Electron to add features such as browsing through folders, searching the files and folders by name, and opening files.

在本章中，我们介绍了使用 NW.js 和 Electron 构建一款许多人都会在他们的计算机中使用的应用。还从头开始介绍了构建一款应用的流程以及如何逐个实现应用的功能。下面是本章介绍过的内容：

1、实现线框图最好的办法是，一个功能一个功能地去实现。

2、具备良好语义的代码可以更好地表达它要实现的功能。

3、在 NW.js 和 Electron 应用中，CSS 是主要定义界面元素样式的方式。

4、在你的桌面应用中使用 Node.js 以及其他第三方库是非常容易的。

5、由于 NW.js 和 Electron 的实现思路，它们互相之间可以共享代码，不过在 package.json 配置文件方面，Electron 会要求更多的代码，稍微有一些区别。

最棒的就是，对于 NW.js 和 Electron 版的 Lorikeet 应用，它们可以使用同样的代码，你也看到了使用这两个框架构建出来的应用是多么相似，当然你也留意到了它们不同的部分。这就意味着，就算此前你为你的应用所选择的框架是错误的，切换到另外一个框架也不是什么难事。

还值得一提的是，你可以用构建 Web 网站的技术去构建桌面应用的界面，这就意味着可以很快地构建桌面应用。在下一章中，我们会继续扩展本章中的应用，增加更实用的功能。我们将会介绍 NW.js 和 Electron 的 API，并使用它们实现诸如浏览文件夹内容、通过名字查询文件和文件夹，以及打开文件这样的功能。
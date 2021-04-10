# 2021043Electron-From-Beginner-to-ProR01

## 记忆时间

## 目录

0101 Welcome to Electron

0201 Installing Electron

0301 The Electron Quick Start

0401 BrowserWindow Basics

0601 Understanding the IPC Module

## 0101. Welcome to Electron

### Summary

This chapter has given you a general overview of Electron. We have touched on its two core technologies: Node and Chromium, as well as introduced its dual-process design. You should have an initial sense of what an Electron-based application is capable of.

In the coming chapters, we will begin exploring these capabilities in much more detail, as well as some we did not even mention yet.

### 1.0

GitHub Electron (or simply Electron) allows you to build desktop applications using just HTML, CSS, and JavaScript. Sounds like a pretty ambitious statement to make. But it is indeed true, just as Apache Cordova (also known as PhoneGap) enables you to create mobile applications also with just HTML, CSS, JS, and so does Electron for the desktop.

Originally released in July 2013 by Cheng Zhao, an engineer at Github, it was part of their effort to produce a new code editor, Atom. Initially, the project was known as the Atom Shell but was soon rebranded simply as Electron. Although other solutions existed, this project quickly gained traction within the development community. In fact, Adobe AIR, released back in 2008, originally supported building desktop applications with HTML, CSS, and JavaScript, in addition to ActionScript. So the desire to leverage web technologies beyond the browser is certainly not a new one.

In this book, we will take you through the entire Electron ecosystem from its initial setup, through its key features, like creating native menus and windows and more, and how to deploy our app so it can be distributed to our users. Rather bog you down in understanding some abstract sample applications, we are going to be focusing on the core code needing to make Electron work. So, you don't need to know the latest framework to use Electron, but having some basic knowledge with Node.js is useful.

Here is a brief outline of what we are going to be covering: 1) Setting up Electron. 2) Adding native menus. 3) Implementing native dialogs. 4) Exploring creating the application's window. 5) Creating installable and auto-updating applications. 6) Learning how to interact with the user's system.

So, if you are ready to start learning about Electron, let's get started.

### 1.1 What Is Electron?

Electron is a blend of two incredibly popular technologies: Node.js (or simply Node) and Chromium. Thus, any web application you have written can run on Electron. Similarly, any Node application you have written can run on Electron. But the power of Electron is that you can use both solutions together.

This book is about how to use these two technologies together to create rich and engaging desktop applications. For example, we have been developing a simple desktop application that will assist developers generate their `manifest.json` file for their Progressive Web Apps. For those unfamiliar with Progressive Web Apps (PWAs), they are web apps that use modern web capabilities to deliver native app-like experiences within the browser. We could have simply written a Node script that developers could run from the command line. But instead we leverage Electron to create a more compelling desktop application. It is one that allows you to auto-generate the app icons simply by dragging the image on the application, and it will save out the collection for you.

Breaking Electron down into its two components (thankfully the physics naming stopped and we aren't referring to these subparts as quarks), they each have specific functions.

The Node component handles things like file system access, compiled module support, and CommonJS Module support. The Chromium component handles things like rendering HTML and CSS, its own JavaScript engine, and the full suite of Web APIs.

Electron is a straightforward runtime. It is not a massive framework/library like Angular or React, but rather a collection of APIs that we can leverage with those or other frameworks. The structure of an Electron application is also open to personal taste. Usually, the UI framework will have more to say about the directory structure than Electron's requirements. However, there are general guidelines that would be wise to follow when developing.

#### 1.1.1 What Is Node?

Node.js was initially released in 2009 as an open source project, enabling developers to create server-side applications using JavaScript. What made this project interesting was that it leveraged Google's newly open sourced V8 engine to act as its JavaScript runtime. A top of that runtime, the project added APIs for accessing the local file system, creating servers, as well as the ability to load modules.

Node has enjoyed a tremendous surge of popularity from across the development community. As such, there is a huge collection of modules that are available for use within your Electron application.

1-2『这里的信息让自己对 Node 有了一个初步的了解，Node 原来也是一种后端语言，基于 JS 的后端语言。那么之前听耗子哥说的，「JS 是唯一前后端通吃的语言」，此时才算理解。Node 的概念做一张主题卡片。（2021-03-25）』

#### 1.1.2 What Is Chromium?

Chromium is the open source version of Google's Chrome web browser. Although it shares much of the same code base and feature set, there are a few differences (albeit minor) and it is released under a different license. What is included with Electron is technically the Chromium Content Module (CCM). Quite the mouthful, hence why most simply refer it is as Chromium. But what is the Chromium Content Module? It is the core code that makes a web browser a web browser. It includes the Blink rendering engine and its own V8 JavaScript engine. The CCM will handle retrieving and rendering HTML, loading and parsing CSS, and executing JavaScript as well.

The CCM only focuses on the core needs to render a web page. Additional features, like supporting Chrome Extensions, or syncing your Chrome bookmarks, are not supported. Just remember that its core purpose is to render web content.

1『 Chromium，目前的理解是阉割版的 Chrome，而且是开源的。做一张术语卡片。（2021-03-25）』

### 1.2 Who Is Using Electron?

So many open source projects come and go. Is Electron worth investing your time and energy into learn? Yes. Although, Electron's original purpose was to act as the shell for GitHub's Atom editor, companies large and small found it to be a good solution for their development needs. Since it was backed by a recognizable company, the risks were a bit lower than trusting your next big thing on an unproven project. If you go to atom.electron.io you can see a massive collection of applications that have been released with Electron as its core.

Obviously Github is actively supporting it, as it is the foundation of their Atom editor. But who else? The very popular team messaging application Slack is built atop Electron, enabling them to develop a common UI across the operating systems. If Atom is not your code editor of choice, then Microsoft's Visual Studio Code might be. This popular editor is also built atop Electron. This is currently our editor of choice at the moment. The team at Microsoft has leveraged common development languages of HTML, CSS, and JavaScript to create a very compelling editor tuned for working with TypeScript and more that works across both macOS and Windows.

1『我去啊，VS Code 竟然是用 electron 写的，Postman 也是。（2021-03-25）』

A variety of familiar web tools have also been able to transform themselves into the desktop-based applications. If you are familiar with Yeoman, a web project generator, there is now a version with a user interface instead of the standard command-line version you are probably familiar with. The team at Basecamp, a popular project management tool, now supports an out of browser experience. If you have worked with Zeplin.io to inspect your visual designs, then the desktop version was developed with Electron. The Postman API inspection tool is another great example of what is possible as an Electron application.

These are just some of the examples of some first-class web applications that have been able to break free from the browser and create desktop-centric versions of their applications. If you would like to explore some other applications that have been built with Electron, visit https://electron.atom.io/apps/.

[Electron 应用 | Electron](https://www.electronjs.org/apps)

### 1.3 What Do I Need to Know?

Unlike traditional desktop development, the only skills you need to have to develop with Electron are a good understanding of HTML, CSS, and JavaScript, and a touch of Node. Being comfortable with your command line wouldn't hurt either. The fact that we can leverage our existing skills and take them from the browser on to the desktop is what is exciting about Electron. We will be using Git to seed our starter Electron apps, but nothing more than that is needed. But working with a version control system is always a recommended skill.

This book is going to take a slightly different approach to covering how Electron works. Since it is simply a runtime, it is framework agnostic. So rather than working through an application built in the framework that you don't know, we are going to just stick with vanilla JavaScript. Now, you should have a modest understanding of HTML and CSS. As for your JavaScript skills, if you have a general understanding of modern JavaScript (aka ES6), you will be fine.

Another area that can be helpful to have is some experience with Node. We will be using the module system throughout this book. But we will provide some foundations on these and any advanced topics that we might need to cover in this book.

### 1.4 Why Should I Choose Electron?

We can assume by the fact you have bought this book, that either there is a need to build a desktop application for yourself, a client or your employer, or you are simply curious about it.

If you have done any web application developing, you no doubt understand the challenges of having to support a wide range of browsers, each with different levels of standards support. Don't get us wrong, the browser's standard support has come a long way in recent years. But, there are still workarounds and polyfills needed to properly deploy a web application to the world. For those working with enterprise clients, you may be further handicapped to legacy browsers and operating systems. When you create an Electron application, you embed a copy of the Chromium engine with the application, so you know exactly what features your application and support have and how your content will render. For example, if you want to use Flexbox as part of your layout solution, you safely can do so (Figure 1-1). If using the Service Worker or Fetch API is something needed for your application, you only need to make sure that the build Electron supports it.

Figure 1-1. The FlexBox support table from caniuse.com

No longer will referencing a feature on caniuse.com be disappointing but rather one of possibilities. As a general rule, Electron updates its Chromium module about two weeks after it is released to the public. The Node component typically takes a bit longer to update. As you begin to embark on larger Electron projects, you will want to also monitor the development process of both of these projects. There might be an issue that you need to be aware or feature added that can greatly make your life easier. But, don't worry – once you can package your application, those runtimes are baked into your application.

#### 1.4.1 Electron's Advantages

Electron applications are just like any other desktop application as they are installed locally on the user's hard drive. They can be launched directly from the Windows taskbar or from the OSX Dock, and there is no need to launch a browser and navigate to some url to run your application. When you need to open or save a file, these dialogs are native in appearance and interaction. Your Electron application can support full drag-and-drop interaction with a local file system, or even associate itself with a file type, so when a user double-clicks the associated file your app will open.

We also have the ability have custom application menus that conform to each platform's user interface guidelines. Contextual menus are available that allow your user to control-click or right-click to display your custom menu. We will show you how to add this functionality in a later chapter.

If you need to trigger a system-wide notification, we can leverage Chromium's Notification API to do so. Electron will go even further that traditional window desktop applications, and create applications that only live in the menubar or system tray.

Electron provides a solid framework that will allow you to develop first-class desktop applications.

#### 1.4.2 Beyond the Sandbox

If you have ever worked with an external API, then you are probably familiar with the restrictions that you have to work. We all have fought with Cross Origin Resource Sharing issues, or establishing proxies in order to allow our web application to work correctly.

Electron operates in a much looser environment with regard to security than your browser. The general assumption is that the user has actively chosen to install and run this application. As such, a degree of trust is then assumed between the user and application.

This allows our Electron application much more freedom, but at the same time we have to use this power with caution.

#### 1.4.3 Offline First Design

With typical web application development, you can usually assume the user is online. Now this is changing with the increase in Progressive Web Apps, but some level of online capability is there for your web app to function. Electron applications have to take the opposite approach. You should not assume that you have an Internet connection. In fact, portions of this chapter were written at 35,000 feet on a plane without WiFi. But I was still able to write in a completely offline mode. Even if your application is dependent on communicating with a back end, you can design your application to function in an offline mode, and sync the data once a connection is reestablished. You will need to take some time to consider how this design pattern will affect the interaction and development of your Electron application.

1『这里提供了一个意想不到的思路。用 Electron 实现的离线功能，断网的时候用本地数据，连线的时候再自动做一下同步功能。两不耽误。（2021-04-10）』

### 1.5 How Does Electron Work?

Electron-based applications run in two distinct processes: the main process and the render process (Figure 1-2). Each of these two processes has a specific responsibility within your application. While Electron provides a good collection of Node modules for use within your application, many of these modules are only available within a specific process. Knowing these restrictions will help you design the code structure of your application. For example, access to the operating system APIs are restricted to just the main process, and access to the system's clipboard is available to both the main and render process. Knowing this dual-process structure is important, as it will define where some aspects of your application's code need to reside.

1『这里看到了熟悉的「Node modules」，一般是用 `npm inatll` 或者 `yarn install` 来安装的。（2021-03-25）』

| Main Process | Renderer Process |
| --- | --- |
| File system access | HTML & CSS Renderer |
| Compiled Module support | Document Object Model (DOM) Access |
| CommonJS Modules | Web API |

Figure 1-2. The two processes that power an Electron application

#### 1.5.1 The Main Process

Within the main process is where your application will handle various system-level activities, like life-cycle events (starting up, preparing to quit, actually quitting, switching between the foreground and background, as just a few examples). This is also the process where application menus are created, as well as any native dialogs, like file open or file save. Our main process is what is used to bootstrap our application. This is the JavaScript file that is referenced within our package.json file, but more on that in the later chapters.

1-3『这里的信息：1）让我想起来学小程序时的知识，它也是分两条线的，一条主程序的挂起等逻辑，另外一条负责渲染页面。2）还有一个关键信息：This is the JavaScript file that is referenced within our package.json file. 原来主程序的实现是放在配置文件里的。（2021-03-25）』

#### 1.5.2 The Render Process

The main process also has another responsibility, which is to spawn any render processes. It is these processes that would display the UI of your application. Each of these render processes will load your content and execute it within its own thread. We can spawn as many windows as we need for our application. Now unlike a standard web app, each of these processes has access to all the installed Node modules, giving you a lot of capabilities.

The render process is isolated from any interaction with any system-level events. Remember, those interactions must be done within the main process. However, Electron does include an interprocess communication system to allow for events and data to be passed back and forth between the main and any renderer process.

One last thing to note, your Electron app actually does not need to have a render process, but it most likely will. This is a perfect option for taking your Node scripts and making them friendlier to use.

#### 1.5.3 Other Solutions

Electron is not the only solution that will enable you to take your web content and enable it to become a desktop application. The most common alternative to using Electron is known as NW.js (originally known as node-webkit). These two projects share some common legacy, remember Cheng Zhao? Well before creating Electron, he was actively involved with the node-webkit project.

Table 1-1 lists some key differences between the projects.

Table 1-1. Project differences

| - |  Electron | NW.JS |
| --- | --- | --- |
| Chromium Type | Current build of Chromium | A forked version of Chromium |
| Node Process design | Separate Node processes | Shared Node process |
| Auto-Updating | Built-in API | Not included |
| Crash Reporting | Built-in API | Not included |
| Windows Support | Windows 7 or later | Windows XP or later |

Some of the key take aways from this table are the fact that NW.js uses a forked (or copy of the original code) version of Chromium. This may introduce issues such as standards support or delays in improvements or fixes within the Chromium module. Some use functions like Auto-Updating and Crash Reporting must be handled with your own custom solution, rather than leveraging the built-in APIs. The Node process design is also worth noting. Since Electron uses separate processes, it should be more performant than an NW.js application that must share the Node process. One of NW.js' advantages is the fact it supports a much older version of Windows. If your target audience might include that legacy operating system, then NW.js would be your only option between the two.

## 0201. Installing Electron

Getting your work environment configured to use Electron is fairly straightforward, but there are a couple of items required to get you started. If you are an experienced developer, you probably already have Node and Git installed. If so, feel free to skip to the Install Electron section of this chapter. If not, let's get started by installing Node.

## 0301. The Electron Quick Start

### Summary

There are many ways you can build your Electron application. If you go with a vanilla approach — that is, just using plain old JavaScript instead of a framework — this is the file you'll be working in. Since there are so many ways to build an Electron application, far too many to cover in one book, we will be focusing on leveraging Electron's features using simple JavaScript examples. Using the Electron Quick Start as a starting point for our exercises will be helpful in keeping this focus.

### 3.0

Getting started with Electron can be confusing. Where do you put files? What do you name files? What code do you need to start with? How should your code be organized?

Luckily for us, folks who work on Electron have created a Github repository to assist you, and us, with getting started with Electron. We will be using the Electron Quick Start as the starting point for our example applications in this book. The Electron Quick Start is located at https://github.com/electron/electron-quick-start on Github. Review the code in this repository. It is very simple, and it contains code to handle the basic needs of an Electron application.

1-2-3『

[electron/electron-quick-start: Clone to try a simple Electron app](https://github.com/electron/electron-quick-start)

fork 了该项目放在了文件夹「dalong.electron」下。发现用 yarn 不行，必须使用 npm，应该是设置的问题，不然墨菲搭建的框架咋用的 yarn。（2021-03-26）

```
npm install
npm start
```

』

There are many ways to write the code for Electron's Renderer Process. You could use any number of frameworks: Angular, React, Vue… frankly, too many to be named here. We're leaving this decision to you. Our goal with this book is to ensure you understand how to code for Electron, in both the Main and Renderer Processes, and by using a vanilla approach as the Quick Start's code can focus on Electron's features and create a foundation upon which you may build.

1『大赞，Electron 的渲染层实现，跟开发 web 端一模一样，前端三大主流框架自己随便选。（2021-03-25）』

### 3.1 Getting the Quick Start Code

You will need to have Git, Node, and npm installed on your computer to build from the Electron Quick Start.

Developers usually have a directory on their system where they keep their code projects. Typically, there can be a HOME/Code/ directory. For the purposes of this book, we are going to assume this is where your code is kept. Please remember to use the path to the code on your system when you see HOME/Code/.

Open your terminal application. On Mac OS X, this application is located in the Applications/Utilities folder. On Windows it is located in Start | Program Files | Accessories | Command Prompt, although you might prefer using Git Bash, to download examples more easily.

From your terminal application, change directories to your Code folder. From your Code folder, enter the following command:

```
git clone https://github.com/electron/electron-quick-start quick-start
```

This command creates a copy of the Electron Quick Start repository inside the quick-start folder in the path from which the command was made. Now, change directories into the quick-start directory:

```
cd quick-start
```

Now clear the repository's history so we can start from scratch from Git's perspective:

```
git init
```

You should see a message like the following:

```
Reinitialized existing Git repository in /Users/<username>/Code//quick-start/.git/
```

One of the nice things about Git repositories and npm is that you don't need to carry around external modular code with you all the time. We just need to ask npm to install the node modules associated with this project by using the following command:

```
npm install
```

Now you are ready to open your new project inside your favorite integrated development environment. We are using Microsoft Visual Studio Code, so you will see that UI in many of our screenshots.

### 3.2 Updating the Project to Make It Yours

The first step after setting up your new Electron project is to update the package.json file. If you are starting a completely new project, without example files, the package.json file will be created when running npm init. Right now, the file should look something like this:

```
{
  "name": "electron-quick-start",
  "version": "1.0.0",
  "description": "A minimal Electron application",
  "main": "main.js",
  "scripts": {
    "start": "electron ."
  },
  "repository": "https://github.com/electron/electron-quick-start",
  "keywords": [
    "Electron",
    "quick",
    "start",
    "tutorial",
    "demo"
  ],
  "author": "GitHub",
  "license": "CC0-1.0",
  "devDependencies": {
    "electron": "^12.0.2"
  }
}
```

name: The name of your application. The expected format is using lowercase letters with dashes between words. In the samples we are building for this book, the name isn't all that important, but for future application, the name may be critical. Make certain to update this to the name you wish to use and keep it up to date.

version: This represents the version of your application's code. It should be updated to match the current release of the application.

description: This key, oddly enough, is where you place a brief description of your application.

main: This key is critical. This is where you tell Electron to locate the code for the Main Process. If you decide to create a directory for this file to keep your project's structure neat, you will need to update this node to reflect that change. Otherwise, Electron will fail to run.

scripts: This key tells Node Package Manager (npm) what actions to take for specific commands. Here, entering npm run start results in the command electron. being run. This is a convenient way to organize commands.

repository: This key points to the repository where your code is stored. Feel free to change this to your repository.

keywords: Enter any keywords that may be used to describe your application.

author: That's you! Put your name or your organization's name here.

license: This is the code representing which license you've decided to release your code under. You'll find over 500 license types at this link: https://gist.github.com/robertkowalski/7620849. Before releasing an application or the code for a repository, you should take the time to examine your licensing options.

Dependencies and devDependencies: These are a list of names and versions of modules that are required for the project. There is currently no dependencies key for this project. The devDependencies key contains ‘electron’, which is used to create our application. These properties will get updated when you install new modules.

Now that we've examined the package.json file, let's take a look at the application by using this command:

```
npm start
```

You should see something similar to Figure 3-1 on your screen.

Figure 3-1. The starter Electron application's main window and development tools

Note: You can quit this application using the typical means: command-q, electron ➤ Quit on Mac oS X or File ➤ Quit on Windows. From the terminal application you may also enter the control-c key combination to quit the application.

Next we'll take a look at the code that makes this starter project work.

### 3.3 The Main Process File

As we mentioned before, Electron has two processes: the Main Process and the Renderer Process. In our starter project, the code for the Main Process resides inside the main.js file.

Note: naming the Main process file main.js is a best practice. and it makes good sense: the main.js file represents the starting point for node to fire up your Main process. While you may decide to organize the code for your Main process into a sensible directory and file structure, you should keep a main.js file to represent the starting point for your project.

The main.js file contains basic code required for any Electron application as well as some helpful comments, as shown in Listing 3-1.

Listing 3-1. main.js

```js
// Modules to control application life and create native browser window
const {app, BrowserWindow} = require('electron')
const path = require('path')

function createWindow () {
  // Create the browser window.
  const mainWindow = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      preload: path.join(__dirname, 'preload.js')
    }
  })

  // and load the index.html of the app.
  mainWindow.loadFile('index.html')

  // Open the DevTools.
  // mainWindow.webContents.openDevTools()
}

// This method will be called when Electron has finished
// initialization and is ready to create browser windows.
// Some APIs can only be used after this event occurs.
app.whenReady().then(() => {
  createWindow()
  
  app.on('activate', function () {
    // On macOS it's common to re-create a window in the app when the
    // dock icon is clicked and there are no other windows open.
    if (BrowserWindow.getAllWindows().length === 0) createWindow()
  })
})

// Quit when all windows are closed, except on macOS. There, it's common
// for applications and their menu bar to stay active until the user quits
// explicitly with Cmd + Q.
app.on('window-all-closed', function () {
  if (process.platform !== 'darwin') app.quit()
})

// In this file you can include the rest of your app's specific main process
// code. You can also put them in separate files and require them here.
```

书籍源码：

```js
const electron = require('electron')
// Module to control application life.
const app = electron.app
// Module to create native browser window.
const BrowserWindow = electron.BrowserWindow

const path = require('path')
const url = require('url')

// Keep a global reference of the window object, if you don't, the window will
// be closed automatically when the JavaScript object is garbage collected.
let mainWindow

function createWindow () { 
  // Create the browser window. 
  mainWindow = new BrowserWindow({width: 800, height: 600})

  // and load the index.html of the app. 
  mainWindow.loadURL(url.format({ 
    pathname: path.join(__dirname, 'index.html'), 
    protocol: 'file:', 
    slashes: true 
  }))

// Open the DevTools. 
mainWindow.webContents.openDevTools()

// Emitted when the window is closed. 
mainWindow.on('closed', function () { 
  // Dereference the window object, usually you would store windows 
  // in an array if your app supports multi windows, this is the time 
  // when you should delete the corresponding element. 
  mainWindow = null })
}

// This method will be called when Electron has finished
// initialization and is ready to create browser windows.
// Some APIs can only be used after this event occurs.
app.on('ready', createWindow)

// Quit when all windows are closed.
app.on('window-all-closed', function () { 
  // On OS X it is common for applications and their menu bar 
  // to stay active until the user quits explicitly with Cmd + Q 
  if (process.platform !== 'darwin') { 
    app.quit() 
  }})

app.on('activate', function () { 
  // On OS X it's common to re-create a window in the app when the 
  // dock icon is clicked and there are no other windows open. 
  if (mainWindow === null) { 
    createWindow() 
  }})

// In this file you can include the rest of your app's specific main process
// code. You can also put them in separate files and require them here.
```

1『拉下来的 git 源码跟数据的源码不太一样。（2021-03-26）』

The top of the file gives us access to the modules required for this application:

```js
const electron = require('electron')
// Module to control application life.
const app = electron.app
// Module to create native browser window.
const BrowserWindow = electron.BrowserWindow

const path = require('path')
const url = require('url')
```

The electron constant is, as you'd expect, the Electron module. It gives you access to all of the Electron APIs as well as any extensions to Node that Electron provides.

The app constant is the part of the Electron API that gives you access to the event life cycle of our application. We'll see examples of how app is used further down in the code.

The BrowserWindow constant represents your Renderer Process. We will use BrowserWindow to create an instance of Chromium, the windows that make up the UIs of our application.

1『跟脑子里的知识关联上了，这里实例化后 BrowserWindow 对象，代表两大核心线程里的渲染层（Renderer Process）。（2021-04-10）』

The path and url constants represent Node modules, part of the Node API that is accessible by any Electron application. url is used to help with creating URLs. path helps with dealing with files and directories.

The next piece of code comes with some guidance in the form of a comment:

```js
function createWindow () { 
  // Create the browser window. 
  mainWindow = new BrowserWindow({width: 800, height: 600})

  // and load the index.html of the app. 
  mainWindow.loadURL(url.format({ 
    pathname: path.join(__dirname, 'index.html'), 
    protocol: 'file:', 
    slashes: true 
  }))

// Open the DevTools. 
mainWindow.webContents.openDevTools()

// Emitted when the window is closed. 
mainWindow.on('closed', function () { 
  // Dereference the window object, usually you would store windows 
  // in an array if your app supports multi windows, this is the time 
  // when you should delete the corresponding element. 
  mainWindow = null })
}
```

This method does the following steps:

1 Creates an instance of a BrowserWindow, passing along an object used to configure that window to be 800 pixels wide and 600 pixels high.

2 Loads that window using the path and url modules to access the index.html file. This file is the starting point for your Renderer Process.

3 The line `mainWindow.webContents.openDevTools()` does what you think it does: opens up the Developer Tools that are part of Chromium. These tools are extremely helpful for debugging the Renderer Process.

1『怪不得自己跑起来的程序开发者窗口关着的，要自己打开。因为源码里这一行被注释掉了。（2021-03-26）』

4 Listens for the `closed` event on the new window instance. The guidance here is around how to manage multiple windows, if the app uses them. The function here merely nulls your window instance, but this is where you may wish to add code in the future.

Finally, we get to the part of the code where the app listeners control when the window is created, and when the application quits.

```js
// This method will be called when Electron has finished
// initialization and is ready to create browser windows.
// Some APIs can only be used after this event occurs.
app.on('ready', createWindow)

// Quit when all windows are closed.
app.on('window-all-closed', function () { 
  // On OS X it is common for applications and their menu bar 
  // to stay active until the user quits explicitly with Cmd + Q 
  if (process.platform !== 'darwin') { 
    app.quit() 
  }})

app.on('activate', function () { 
  // On OS X it's common to re-create a window in the app when the 
  // dock icon is clicked and there are no other windows open. 
  if (mainWindow === null) { 
    createWindow() 
  }})

// In this file you can include the rest of your app's specific main process
// code. You can also put them in separate files and require them here.
```

The app instance is listening to three events here: `ready`, `window-all-closed`, and `activate`. Upon receiving the `ready` event, the createWindow that we discussed above is called. As the commented guidance references, the `windows-all-closed` is listened for because on the MacOS X platform you can close all of an application's windows but not quit the application. That is not true on Windows and Linux, so this code quits the application on those platforms.

Also of note, here is the use of `process`, part of the Node API. For instance, `process.platform` will return `darwin` for Mac OS X, and `win32` for the Windows platform. Even on Windows 64-bit, process.platform will read `win32`, while process.arch (stands for Architecture) will return `x64`. And since you can have an application open without any windows open on the Mac OS X platform, the `active` event is listened for and creates a new window when emitted. This bit of code is not testing to see which platform the application is on because this condition — where the `active` event is emitted and `mainWindow === null` will only occur on the Mac OS X platform.

Finally, at the very bottom of the main.js file we are given more guidance, letting us know that we should add more Main Process code here or require other files if that is how you wish to organize your code.

### 3.4 The Quick Start's Renderer Process

As we mentioned before, the main.js file identifies the html file used to start up Electron's renderer process. The process is started using the `mainWindow.loadURL()` call in this code block:

```js
  // and load the index.html of the app. 
  mainWindow.loadURL(url.format({ 
    pathname: path.join(__dirname, 'index.html'), 
    protocol: 'file:', 
    slashes: true 
  }))
```

Using Node's url.format() method, this code creates a path to the index.html file by joining the file name with the Electron variable `__dirname` that points us to the file in the root of our project.

Let's review the index.html file:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <!-- https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP -->
    <meta http-equiv="Content-Security-Policy" content="default-src 'self'; script-src 'self'">
    <meta http-equiv="X-Content-Security-Policy" content="default-src 'self'; script-src 'self'">
    <title>Hello World!</title>
  </head>
  <body>
    <h1>Hello World!</h1>
    We are using Node.js <span id="node-version"></span>,
    Chromium <span id="chrome-version"></span>,
    and Electron <span id="electron-version"></span>.

    <!-- You can also require other files to run in this process -->
    <script src="./renderer.js"></script>
  </body>
</html>
```

原书源码：

```html
<!DOCTYPE html> 
<html> 
  <head>
    <meta charset="UTF-8">
    <title>Hello World!</title> 
  </head> 
  <body> 
    <h1>Hello World!</h1> 
    <!-- All of the Node.js APIs are available in this renderer process. --> 
    We are using Node.js <script>document.write(process.versions.node)</script>, 
    Chromium <script>document.write(process.versions.chrome)</script>, 
    and Electron <script>document.write(process.versions.electron)</script>. 
  </body>
  
  <script> 
    // You can also require other files to run in this process 
    require('./renderer.js') 
  </script> 
</html>
```

Again, another simple file, this one is a basic HTML file. But there are a few important points to remember about this file to help you understand how Electron works.

First, in the middle of the page there are several script tags that contain calls to Node's process API:

```html
    <!-- All of the Node.js APIs are available in this renderer process. --> 
    We are using Node.js <script>document.write(process.versions.node)</script>, 
    Chromium <script>document.write(process.versions.chrome)</script>, 
    and Electron <script>document.write(process.versions.electron)</script>. 
```

As you can see from the comment, all of Node's APIs are available to the renderer process, which is why you have access to the process API inside this HTML file. In this instance, the code lets us see which versions of Node, Chromium, and Electron are being used with this application. Figure 3-1 shows how this renders.

Figure 3-2. The starter Electron application, the version numbers dynamically added

This code isn't necessary but it is useful in helping us understand how Electron works. The other important piece to the index.html file is the script tag at the bottom of the file:

```html
  <script> 
    // You can also require other files to run in this process 
    require('./renderer.js') 
  </script> 
```

This tag uses require to import the renderer.js file. In most cases, this will be the starting point for the JavaScript for your application. If we take a look at the actual file, we will see it only contains the following comment:

```js
// This file is required by the index.html file and will
// be executed in the renderer process for that window.
// All of the Node.js APIs are available in this process.
```

## 0401. BrowserWindow Basics

### Summary

In this chapter, we explored the basic options of BrowserWindow creation: show, width, height, minWidth, maxWidth, minHeight, maxHeight, resizable, movable, and alwaysOnTop. We also explored two window types: frameless and transparent. The knowledge we gained here will help us as we move into the next chapters.

### 4.0

As explained in earlier chapters, the Renderer Process is where your application appears. The Renderer Process uses Chromium to render your user interface. The Main Process creates Renderer Processes by creating instances of the BrowserWindow object.

In this chapter, we explore the basic options for creating BrowserWindow instances as well as explore the frameless and transparent window types.

### 4.1 Getting Started

Let's take a moment to make this package.json match our own by updating some nodes.

1 Change the name node to "browser-window-sample".

2 Change the version number to "0.0.1" since we are just starting out. If you are unfamiliar with semantic versioning, version numbers are broken into three elements: MAJOR.MINOR.PATCH. As this is our starting point, we will begin numbering with 0.0.1.

3 In the description let's use something like "A sample Electron application to demonstrate BrowserWindow creation".

4 Remove the repository property. If you decide to put your results in a repository you can change or re-add this property with the correct address.

5 Keywords can be "Electron," "BrowserWindow," "sample".

6 "author": Your name goes here.

7 If you wish to change the licensing type, you can do that with this property. By default, it is set to Creative Commons 1.0 Universal. There are many alternative options available; choose the one that best suits your needs.

#### 4.1.1 Disabling Chrome DevTools

In this chapter, we will be repeatedly starting and stopping our project to see how different settings affect the window our project creates. We also need to make sure that Dev Tools are turned off so they don't interfere with what we see. Open the main.js file and find the line in the code that makes the Dev Tools appear and comment it like this (note the highlighted code added):

```js
// Open the DevTools.
// mainWindow.webContents.openDevTools()
```

Now that the Dev Tools are out of the way, let's take a look at what the default code without the Dev Tools creates (Figure 4-1). From the terminal application, navigate to the project folder and run the following command:

```
npm start
```

Figure 4-1. The starter Electron window without the Chrome DevTools

Remember this command as we will be using it many times in this chapter. As you can see, this is a simple window. Nothing exciting here. Let's review the code that initializes this window in the createWindow method inside the main.js file:

```js
function createWindow () { 
  // Create the browser window. 
  mainWindow = new BrowserWindow({width: 800, height: 600})

  // and load the index.html of the app. 
  mainWindow.loadURL(url.format({ 
    pathname: path.join(__dirname, 'index.html'), 
    protocol: 'file:', 
    slashes: true 
  }))

// Open the DevTools. 
mainWindow.webContents.openDevTools()

// Emitted when the window is closed. 
mainWindow.on('closed', function () { 
  // Dereference the window object, usually you would store windows 
  // in an array if your app supports multi windows, this is the time 
  // when you should delete the corresponding element. 
  mainWindow = null })
}
```

When createWindow is called, the mainWindow variable is created by calling the new BrowserWindow constructor. There is an argument being passed to the constructor in the form of an object with the properties of width and height.

Lower in that code block we call the loadURL method on the mainWindow. The argument required for the loadURL method is created using Node's url module, a utility module that assists in the creation and formatting of URLs:

```js
function createWindow () { 
  // Create the browser window. 
  mainWindow = new BrowserWindow({width: 800, height: 600})

  // and load the index.html of the app. 
  mainWindow.loadURL(url.format({ 
    pathname: path.join(__dirname, 'index.html'), 
    protocol: 'file:', 
    slashes: true 
  }))

```

1-3『

最新版的项目此处代码有调整，感觉新代码更加简洁，估计以前的函数被废弃了。（2021-03-26）

```js
function createWindow () {
  // Create the browser window.
  const mainWindow = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      preload: path.join(__dirname, 'preload.js')
    }
  })

  // and load the index.html of the app.
  mainWindow.loadFile('index.html')

  // Open the DevTools.
  // mainWindow.webContents.openDevTools()
}
```

』

The format method from the url module allows you to create a link to the file that the Renderer Process will use to render. Note the properties used in the argument for the format method. This is the way Node likes to have URLs created:

1 pathname: uses Node's path module to create a string by connecting the two pieces of the path, `__dirname` (a Node global), and the name of the file to be rendered.

2 protocol: the loading protocol to use. Typically for Electron, ‘file:' is the setting. Please note the use of the colon.

3 slashes: Setting this to true adds ‘//' to the protocol making it ‘file:///', in this case making it properly use three slashes.

After we load the file for the window, we need to add a listener to the window so we can capture the ‘closed' event and, as is best practice for desktop applications, clear the mainWindow variable:

```js
// Emitted when the window is closed. 
mainWindow.on('closed', function () { 
  // Dereference the window object, usually you would store windows 
  // in an array if your app supports multi windows, this is the time 
  // when you should delete the corresponding element. 
  mainWindow = null })
}
```

1-3『

新版代码（2021-03-26）：

```js
// Quit when all windows are closed, except on macOS. There, it's common
// for applications and their menu bar to stay active until the user quits
// explicitly with Cmd + Q.
app.on('window-all-closed', function () {
  if (process.platform !== 'darwin') app.quit()
})

// In this file you can include the rest of your app's specific main process
// code. You can also put them in separate files and require them here.
```

』

### 4.2 Update Code to Use the ready-to-show Event

The first change we will make to our code is to establish a best practice of waiting for the BrowserWindow's ready-to-show event before showing the window. This best practice is recommended in Electron's documentation and is often overlooked. When you create a BrowserWindow directly, as our code does currently, the Renderer Process starts and immediately displays. But the content you are displaying may not be fully rendered. To avoid this condition we will listen for the ‘ready-to-show' event and call the BrowserWindow's `show()` method to display the window. Make the following changes to the createWindow method:

```js
function createWindow () { 
  // Create the browser window. 
  mainWindow = new BrowserWindow({
    show: false,
    backgroundColor: '#FFF',
    width: 800, 
    height: 600
  })

  // and load the index.html of the app. 
  mainWindow.loadURL(url.format({ 
    pathname: path.join(__dirname, 'index.html'), 
    protocol: 'file:', 
    slashes: true 
  }))

// Open the DevTools. 
// mainWindow.webContents.openDevTools()

// Wait for 'ready-to-show' to display our window
mainWindow.once('ready-to-show', () => {
  mainWindow.show()
})

// Emitted when the window is closed. 
mainWindow.on('closed', function () { 
  // Dereference the window object, usually you would store windows 
  // in an array if your app supports multi windows, this is the time 
  // when you should delete the corresponding element. 
  mainWindow = null })
}
```

1『

新增的代码单独拎出来：

```js
    show: false,
    backgroundColor: '#FFF',
    
// Wait for 'ready-to-show' to display our window
mainWindow.once('ready-to-show', () => {
  mainWindow.show()
})    
```

』

At the top of this code block we've added the show property set to false, which prevents the created window from displaying.

The next new property is the backgroundColor. The best practice here is to try to match the background color used in your application so that if the window does display before the content is rendered, there won't be a flash between displaying the window's default background color of ‘#FFF' (white) and the background color of your application. This setting is effective with the show property set to true but is a good practice to generally follow. This property only accepts hexcodes for its value and not colors defined in rgb() or rgba(). It is worth noting that this parameter only accepts hexadecimal values, and nothing of the form rgb() or rgba().

Later in the code block we've added the listener for the ‘ready-to-show' event. In our current code, this event occurs quickly since we are not loading up a lot of code and assets in our sample like you might with a real application. We are also using one of the new ES6 features, the fat arrow function. If you are not familiar with this feature, it provides a shorthand notation to have a callback execute it function.

In ES5, we would have written a simple multiply function like this:

```js
var multiply = function (x,y) { 
  return x * y;
}
```

But in ES6, using the new arrow function formation, we can write the same function this way:

```js
var multiply = (x, y) => { return x * y };
```

The arrow function example allows us to accomplish the same result with fewer lines of code and approximately half the typing.

Now that we have established these best practices, let's explore BrowserWindow's options.

### 4.3 BrowserWindow Options Argument

Let's do an experiment here to give us some insight into how the BrowserWindow's argument works. If you haven't done so already, quit the application and delete the argument object making that line of code look like this:

```js
mainWindow = new BrowserWindow()
```

Run the `npm start` command to see how the window appears (Figure 4-2).

Figure 4-2. The starter Electron window opening using the ‘ready-to-show' event

If it appears that nothing has changed, you are correct. The window is centered on the screen and is 800 pixels wide, 600 pixels high. If you grab the title bar, the window will move. Grab the any edge of the window and you can resize it to any size you would like.

The points being made here are:

1 The BrowserWindow's options argument is not required.

2 The BrowserWindow has defaults in place so that, if you do not enter options like the width and height properties in the argument, the window will still appear.

A list of all available options can be found in the Electron documentation: [BrowserWindow | Electron](https://www.electronjs.org/docs/api/browser-window#class-browserwindow).

In this case, the default for width is 800(px) and the default is 600(px). The documentation for the BrowserWindow cites over 40 optional properties, all with defaults. Let's continue by looking at some of the other window properties to which we have access.

#### 4.3.1 Basic Window Properties (width, height, minWidth, minHeight, maxWidth, maxHeight)

Let's update the code to add an argument to the BrowserWindow method.

```js
// Create the browser 
window.mainWindow = new BrowserWindow({  
  show: false,     // DEFAULT: true  
  backgroundColor: "#FFF",  // DEFAULT: '#FFF'  
  width: 800,     // DEFAULT: 800  
  height: 600,     // DEFAULT: 600  
  minWidth: 800,     // DEFAULT: 0  
  maxWidth: 1024,    // DEFAULT: UNLIMITED  
  minHeight: 600,    // DEFAULT: 0  
  maxHeight: 768,    // DEFAULT: UNLIMITED  
  resizable: true,    // DEFAULT: true  
  movable: true     // DEFAULT: true
})
```

1『首先，跑起来没窗口，想了下才反应过来，上面的代码窗口不显示的：`show: false`，注释掉即可。其次，窗口的最小最大尺寸确实固定死了，不能拉更小或更大。（2021-03-26）』

Take a moment to note what we are trying to illustrate with the comments in this code. On the left side are the window properties we wish to affect. On the right side are comments informing us of the default for each of these properties. While these comments aren't required, they will help us moving through this chapter.

Now, run npm start in the terminal and see how these additional properties change our window. No need to give you a screenshot. The initial appearance of the window hasn't changed. While the screen size is 800 x 600 pixels, if you try resizing the window you'll find that you cannot make it smaller than it currently is and no larger than 1024 x 768 pixels.

Please be aware that these sizing constraints are user-oriented constraints. Once the window is created, you may resize it using BrowserWindow methods like setBounds(bounds) and setSize(width, height) to change the size of your window. If you do decide to resize your window, you should take a look at the `setMinimumSize(width, height)` and `setMaximumSize(width, height)` to apply new resize constraints.

#### 4.3.2 The center, x and y Properties

You may notice that this code is not passing a center property in the options argument. Best practices suggest that if your application is a single window application, it should initially appear in the center of the screen. Since our example application is loading in the center of the screen, we can assume that the default setting for center is true even though the default is not currently documented.

Also, not appearing in our code are the x and y options, which control where the top left corner of the window will appear. The defaults for these options are to center the window. That is, when you do not pass the x and y options as part of the options argument for BrowserWindow, Electron does the math taking the width and height properties along with screen dimensions and sets the x and y properties so that the window is centered. Setting the x and y options essentially turns the center option to false.

The x and y options are the only options that are optionally required. What does that mean? If you pass the x option you must pass the y option. The same goes when passing the y option; the x option must be passed as well. If you pass either of these options by themselves, the option is ignored.

For the purposes of this exercise, these properties will not be added to our code. The default settings will do.

#### 4.3.3 The resizable and movable Properties

Let's make another change to the code so we can see how changing the resizable and movable properties affect the other properties:

```js
// Create the browser 
window.mainWindow = new BrowserWindow({  
  show: false,     // DEFAULT: true  
  backgroundColor: "#FFF",  // DEFAULT: '#FFF'  
  width: 800,     // DEFAULT: 800  
  height: 600,     // DEFAULT: 600  
  minWidth: 800,     // DEFAULT: 0  
  maxWidth: 1024,    // DEFAULT: UNLIMITED  
  minHeight: 600,    // DEFAULT: 0  
  maxHeight: 768,    // DEFAULT: UNLIMITED  
  resizable: false,    // DEFAULT: true  
  movable: false     // DEFAULT: true
})
```

After you quit the application and run npm start again you'll find that changing the resizable property to false restricts any resizing of the application. In effect, the minWidth, minHeight, maxWidth, and maxHeight properties are basically ignored. That doesn't mean you should ignore these properties if your window is not resizable. You may wish to turn the resizable property on and off. Setting minimum and maximum sizes is a good practice.

Now try moving the window by dragging the title bar. This window will not move. A best practice here would be to always use the default setting of movable: true unless there is a compelling reason to make it immovable. Most desktop applications allow a user to decide where they want the application's windows to appear.

The alwaysOnTop property is another setting that is important. The default setting for this property is false. Setting alwaysOnTop to true means that while the application is running, this window is above all other windows in the application and on the computer. We can add alwaysOnTop to the bottom of our options argument and reset our resizable and movable properties so our code looks like this:

```js
  // Create the browser window.
  const mainWindow = new BrowserWindow({  
    backgroundColor: "#FFF",  // DEFAULT: '#FFF'  
    width: 800,     // DEFAULT: 800  
    height: 600,     // DEFAULT: 600  
    minWidth: 800,     // DEFAULT: 0  
    maxWidth: 1024,    // DEFAULT: UNLIMITED  
    minHeight: 600,    // DEFAULT: 0  
    maxHeight: 768,    // DEFAULT: UNLIMITED  
    resizable: true,    // DEFAULT: true  
    movable: true,     // DEFAULT: true
    alwaysOnTop: true  // DEFAULT: false
  })
```

Quit the application and run npm start to see this in action. As described, the window stays on top of everything, even windows belonging to the operating system. Again, the best practice is to go with the default setting of false with this property unless there is a compelling reason for blocking all other user interfaces and irritating users.

#### 4.3.4 The title Property

You would think that something like the title property would be something simple. Well, it is, but it may not work the way you might think, so pay attention. The title property is used in the title bar of your window. The Electron documentation says that the title property is, like all the other properties, and the default for title is「Electron.」But let's look at how it really works.

Without adding any code to our project, run the npm start command and look at the text that appears in the title bar (Figure 4-3):

Figure 4-3. Our application name shown in the window's title bar

See, there it is:「Hello, World!」Where is that coming from? Let's find out. Quit the application and open the index.html file in the project. This is the file that our BrowserWindow is being told to render. Up in the head element of that file you will see the title element:

```html
  <head>
    <meta charset="UTF-8">
    <!-- https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP -->
    <meta http-equiv="Content-Security-Policy" content="default-src 'self'; script-src 'self'">
    <meta http-equiv="X-Content-Security-Policy" content="default-src 'self'; script-src 'self'">
    <title>Hello World!</title>
  </head>
```

So, we've learned that the text in the title element of the head element of our rendered HTML file will be used in the title bar of our application. But let's dig a little deeper. Open the main.js file in the project and add the title option to the BrowserWindow argument object (make sure you reset alwaysOnTop to false):

```js
  // Create the browser window.
  const mainWindow = new BrowserWindow({  
    backgroundColor: "#FFF",  // DEFAULT: '#FFF'  
    width: 800,     // DEFAULT: 800  
    height: 600,     // DEFAULT: 600  
    minWidth: 800,     // DEFAULT: 0  
    maxWidth: 1024,    // DEFAULT: UNLIMITED  
    minHeight: 600,    // DEFAULT: 0  
    maxHeight: 768,    // DEFAULT: UNLIMITED  
    resizable: true,    // DEFAULT: true  
    movable: true,     // DEFAULT: true
    alwaysOnTop: true,  // DEFAULT: false
    title: "Goodbye, Moon?"  // DEFAULT: "Electron"
  })
```

Run the npm start command and look at our results (Figure 4-4).

Figure 4-4. Updating the Electron Window title

Wait, what? Why aren't we seeing "Goodbye, Moon?" in our title bar? You see, the HTML content that the Renderer Process is rendering overrides the optional title argument. Let's prove this out. Go back to the index.html file and comment out the title element:

```html
<head>  
  <meta charset="UTF-8"> 
   <!-- <title>Goodbye, Moon?</title> -->
</head>
```

Now run npm start and see what displays in the title bar (Figure 4-5).

Figure 4-5. Our Electron window title properly updated

There's our "Goodbye, Moon?" Nice. Let's take this experiment one step further and comment out the title optional argument.

```js
// title: "Goodbye, Moon?" // DEFAULT: "Electron"
```

Now our code has the title argument commented in the main.js file as well as the title element comment in the index.html file commented so we should see the default setting of "Electron" in our title bar, right? Run the npm start command to see (Figure 4-6):

Figure 4-6. The Electron window title via the package.json value

1『测试了，html 那边和 JS 这边都有代码，html 那边优先；注释掉任意一方，以不注释掉的信息为准；同时注释掉两边，显示系统默认的 title。（2021-03-26）』

OK, what just happened? Are you seeing what we are seeing? We're seeing the text "browser-window-sample" in the title bar, but you may see something else. At the time of this writing, we asked the contributors to the Electron project if this was on purpose but haven't gotten a response. Needless to say, if you changed the package.json property like we suggested at the beginning of this chapter you could be seeing the text you placed there. Weird, right? Let's test this out by deleting that line in the package.json file. Normally, we'd ask you to comment that line, but commenting isn't allowed in JSON. Please remember to re-create that line after this experiment. So, without the name property in our package.json file we can run the npm start command and finally see (Figure 4-7):

Figure 4-7. The Electron window title restored

"Electron"! Hizzah! We were confused at first, too. But we learned something, right? If you do not provide a title argument when you create a BrowserWindow instance, or you do not provide a title in the HTML file you are rendering you will probably get a title that you don't want. (Make sure you re-create the name line in the package.json file.)

Best practices for the title option are to take control of the text that appears in your title bar. You may wish to do this in the Main Process or the Renderer Process. Depending on what kind of application you've created, the text that appears in the title bar could be dynamic. You may need to add a `"*"` at the end or beginning of the title text to indicate that a file hasn't been saved. The file being loaded by the Renderer Process might be a template that dynamically loads other files, or even navigates to other files. Making sure that the title element is in the HTML file by default may work in many cases, but if not give thought to which of the processes makes sense to manage the text that appears in the title bar.

To change the title dynamically on macOS, you can call `mainWindow.setTitle (‘Goodbye, Moon');` this will override your window title (even when it is set in the HTML). Windows (the Operating System) is trickier and will retain the default title (either from HTML or package.json until the user interacts with the window (maximize/minimize/resize).

### 4.4 Other Window Types

While the windows we have been creating so far in this chapter are typically the kind of windows applications will use, there are two other window types we should mention: frameless and transparent windows.

#### 4.4.1 Frameless Windows

A frameless window is a window that has no chrome. This means that the window will appear without any borders or toolbars associated with a browser window and only display the HTML content provided. Let's look at how a frameless window is created.

Frameless windows can be created by using the frame option and setting it to false. Add this option at the bottom of our BrowserWindow code like so:

```js
  // Create the browser window.
  const mainWindow = new BrowserWindow({
    backgroundColor: "#FFF",  // DEFAULT: '#FFF'  
    width: 800,     // DEFAULT: 800  
    height: 600,     // DEFAULT: 600  
    minWidth: 800,     // DEFAULT: 0  
    maxWidth: 1024,    // DEFAULT: UNLIMITED  
    minHeight: 600,    // DEFAULT: 0  
    maxHeight: 768,    // DEFAULT: UNLIMITED  
    resizable: true,    // DEFAULT: true  
    movable: true,     // DEFAULT: true
    alwaysOnTop: true,  // DEFAULT: false
    title: "Goodbye, Moon?",  // DEFAULT: "Electron"
    frame: false,
    webPreferences: {
      preload: path.join(__dirname, 'preload.js')
    }
  })
```

Now we can run the npm start command and look at a frameless window (Figure 4-8).

Figure 4-8. Our Electron application in a frameless window

There it is, a frameless, naked window. No borders. No title bar. No toolbars. Just the bare window. But we need to review some of the things that we can't see that are missing. If you are running on macOS, the first thing you may notice is the normal windows controls that appear in the upper left corner aren't there. You know, the traffic light on its side with a red, yellow, and green button. With those controls missing, you can't close this window using the mouse. Speaking of the mouse, try moving this window. You can't. There is no title bar for you to grab. In some cases, this behavior may be desirable. But we might want to have the window appear as frameless but still give users typical control over the window, so we need to make sure we can get these features back if we need them.

To get a frameless window on macOS that has the window controls, we must create the frameless window a different way. To get the desired window, we do not use the frame option at all. We need to use the titleBarStyle option. The default option for titleBarStyle is ‘default', but we want to use the ‘hidden' or ‘hidden-inset' options. Comment the line with the frame option and then add the following code:

```js
  // Create the browser window.
  const mainWindow = new BrowserWindow({
    backgroundColor: "#FFF",  // DEFAULT: '#FFF'  
    width: 800,     // DEFAULT: 800  
    height: 600,     // DEFAULT: 600  
    minWidth: 800,     // DEFAULT: 0  
    maxWidth: 1024,    // DEFAULT: UNLIMITED  
    minHeight: 600,    // DEFAULT: 0  
    maxHeight: 768,    // DEFAULT: UNLIMITED  
    resizable: true,    // DEFAULT: true  
    movable: true,     // DEFAULT: true
    alwaysOnTop: true,  // DEFAULT: false
    title: "Goodbye, Moon?",  // DEFAULT: "Electron"
    // frame: false,
    titleBarStyle: 'hidden',
    webPreferences: {
      preload: path.join(__dirname, 'preload.js')
    }
  })
```

Run the npm start command and look (Figure 4-9).

Figure 4-9. The Electron application in a frameless window with window controls added

Here we see that the window controls are shown, but, as the option ‘hidden' suggests, the title bar is not seen. The other option for titleBarStyle is ‘hidden-inset'. We can change that code and take a look at how that window displays. Quit the application if it is still running, make the following change to the code, and run the npm start command:

```js
titleBarStyle: 'hidden-inset' // DEFAULT: 'default'
```

The change is subtle (Figure 4-10). As compared to the ‘hidden' setting, the controls have slightly inset into the window. Choose which option to suit your purposes. Note: this property has no effect on Windows OS.

Figure 4-10. The Electron application in a frameless window with window controls added in the inset mode

Now, we need to see about getting the ability to move our frameless window back. For this issue we need to rely upon some CSS. If we want to make the whole window movable, we can simple apply a style to the body of the HTML being rendered. Quit the application if it is still running, open the index.html, and make the following change to the body element:

```html
<body style="-webkit-app-region: drag">
```

Run the npm start command and test out our application.No reason to show you a screenshot, but we should discuss the effects this change has made. Use your mouse to click-hold anywhere near the top area of the window and move the window around. Yes! We can move our window. But let's check doing the same on the bottom area of the window. No dice. What is going on here?

Since we are applying the CSS fix to the body element, only that element will trigger dragging, but the body element is restricted to the size of the content. Quit the application so we may make a change to our CSS so we can see what is really happening:

```js
<body style="border:1px solid red;-webkit-app-region: drag">
```

When we run the npm start command we see a red box around the content at the top of the window.

Now we can see where we can drag the window around and where we cannot. This is because the boundaries of body element are constrained by the content it holds. So, this technique may not be the best way to re-create this feature. Let's also consider what happens to button elements that may be applied inside the body element. The CSS overrides the button behavior so now your buttons don't work. What about selecting text? No, that won't work either.

What have we learned from this experiment? The best practice for moving a frameless window would be to provide an element at the top of the window that can be made draggable. The user expects this behavior and not click-holding anywhere on the window.

Note that if you set the window property movable to false, it will override the CSS property we've set on the body and prevent dragging.

#### 4.4.2 Transparent Windows

Another window type we can explore is a transparent window. This window type is just what you might expect: you can see anything underneath the window. Before we explore making our window transparent, take heed to this warning: you may find that you have lost your application. At 100% transparent, you won't see it. It can be disorienting, so don't panic. If you get confused, go back to your terminal window and use the control-c keyboard combination to stop the application.

Let's make some changes to our main.js file to make a transparent window possible:

```js
  // Create the browser window.
  const mainWindow = new BrowserWindow({
    backgroundColor: "#FFF",  // DEFAULT: '#FFF'  
    width: 800,     // DEFAULT: 800  
    height: 600,     // DEFAULT: 600  
    minWidth: 800,     // DEFAULT: 0  
    maxWidth: 1024,    // DEFAULT: UNLIMITED  
    minHeight: 600,    // DEFAULT: 0  
    maxHeight: 768,    // DEFAULT: UNLIMITED  
    resizable: true,    // DEFAULT: true  
    movable: true,     // DEFAULT: true
    alwaysOnTop: true,  // DEFAULT: false
    title: "Goodbye, Moon?",  // DEFAULT: "Electron"
    // frame: false,
    // titleBarStyle: 'hidden-inset',
    transparent: true,
    webPreferences: {
      preload: path.join(__dirname, 'preload.js')
    }
  })
```

Run the npm start command and prepare yourself to be amazed (Figure 4-11).

Figure 4-11. The Electron window with transparency enabled

Wait a minute. That's not a transparent window. It looks exactly like a frameless window. It seems that just setting the transparent option to true isn't enough. Let's change one more option, the backgroundColor option, and see what we get. Specifically, we will comment out the option:

```js
  // Create the browser window.
  const mainWindow = new BrowserWindow({
    // backgroundColor: "#FFF",  // DEFAULT: '#FFF'  
    width: 800,     // DEFAULT: 800  
    height: 600,     // DEFAULT: 600  
    minWidth: 800,     // DEFAULT: 0  
    maxWidth: 1024,    // DEFAULT: UNLIMITED  
    minHeight: 600,    // DEFAULT: 0  
    maxHeight: 768,    // DEFAULT: UNLIMITED  
    resizable: true,    // DEFAULT: true  
    movable: true,     // DEFAULT: true
    alwaysOnTop: true,  // DEFAULT: false
    title: "Goodbye, Moon?",  // DEFAULT: "Electron"
    // frame: false,
    // titleBarStyle: 'hidden-inset',
    transparent: true,
    webPreferences: {
      preload: path.join(__dirname, 'preload.js')
    }
  })
```

1『哈哈，整个窗口全部透明了，超级有趣。（2021-03-26）』

Figure 4-12. The Electron window with transparency properly enabled

Yeah, that is more like it. Depending on what is on your screen, you can barely see the text of the index.

We've made a transparent window, but we need to know about the restrictions for this window, too. With the frame option set to false, you have all the restrictions as a typical frameless window: no title bar, no toolbars, and the window will not move without modification. Add to these restrictions that you may find it nearly impossible to resize a transparent window. How could you? You can't see the edges of the window. Be aware: setting the reset option to true can make a transparent window stop working. More restrictions and information about creating transparent windows on different platforms can be found in Electron's documentation. Please note that on Windows, this property has for effect to make the whole window and its content disappear, rendering the application unusable.

Please be responsible when you use transparent windows. You do not want the users of your application to think you are playing tricks; but you could set an rgba() background-color on your `<html>` or `<body>` tags to obtain a semi-transparent window that gives you a background but lets you see what's underneath.

## 0601. Understanding the IPC Module

We briefly saw the use of the inter-process communication (IPC) module as one solution for having contextual menus in our application. In this chapter, we are going to explore this module in greater depth. Now, this is not the most glamorous part of API, but it is certainly the workhorse that much of our real-world applications will rely upon.

### 6.1 Getting Started

Since Electron applications are broken into two separate processes (main and render), we need a system to communicate between them. That system is in the IPC module. This module allows you to send and receive synchronous and asynchronous messages between the processes. Each process has a specific module: ipcRenderer and ipcMain (Figure 6-1).

1『原来是靠 IPC module 来连接 electron 的两大核心部分：main process and render process。（2021-03-27）』

Main Process <=>  Renderer Process

Figure 6-1. The IPC API provides a communication bridge between the processes.

Let's clone a fresh copy of Electron.

```
git clone https://github.com/electron/electron-quick-start ipc-example
```

1-2『这里第二次拷这种类似命令了，才意识的 GitHub 的一个仓库里其实是可以放不同的版本的「仓库」的。有时间去研究下如何实现的。（2021-03-27）』—— 未完成

Next, change your active directory to electron-quick-start.

```
cd ipc-example
```

Now, we need to install the dependencies:

```
npm install
```

Finally, reset Git with:

```
git init
```

1『

初始化后弹出的信息：

```
Reinitialized existing Git repository in /Users/Daglas/dalong.electron/ipc-example/.git/
```

不过一直没弄明白这里的「初始化」有啥用。（2021-03-27）

』

With our fresh copy of Electron, let's begin exploring the various IPC solutions.

### 6.2 Synchronous IPC Messaging

Let's begin by defining a few quick styles for our button and response field, the result of this can be seen in Figure 6-2. Open the index.html file and place this style block within our `<head>` tag:

```html
    <style> 
      p { 
        font-family: sans-serif; 
        border: 1px solid #ccc; 
        border-radius: 4px; 
        padding: .5rem; 
        background-color: #ddd; 
        box-shadow: inset 0 0 2px #aaa; 
      }
      button { 
        color: rebeccapurple; 
        font-family: sans-serif; 
        font-weight: bold; 
        padding: .5rem; 
        background-color: #ccc; 
        box-shadow: 2px 2px 2px #ccc; 
      }
    </style>
```

Next, replace the content within the `<body>` tag with the following:

```html
    <button id="sendSyncMsgBtn">Ping Main Process</button>
    <p id="syncReply">Awaiting response</p>
```

Figure 6-2. Our Electron application with our button

1『

自己的源码：

```html
  <body>
    <button id="sendSyncMsgBtn">Ping Main Process</button>
    <p id="syncReply">Awaiting response</p>
    <!-- <h1>Hello World!</h1> -->
    <!-- We are using Node.js <span id="node-version"></span>,
    Chromium <span id="chrome-version"></span>,
    and Electron <span id="electron-version"></span>. -->

    <!-- You can also require other files to run in this process -->
    <script src="./renderer.js"></script>
  </body>
```

』

Now, let's open the renderer.js to add the code that will be triggered when we click our button, as well as the code needed to accept the response back.

First, we need to import the correct IPC module. Since this code will be executed in the Renderer process, we will use the IPCRenderer module.

```js
const ipc = require('electron').ipcRenderer
```

Next, we need to get the reference to our button.

```js
const syncMsgBtn = document.getElementById('sendSyncMsgBtn')
```

With our reference, we can attach our event listener to it:

```js
syncMsgBtn.addEventListener('click', function () {
})
```

Working with IPC, is much like Isaac Newton's Third Law of motion (for every action, there is an equal and opposite reaction), for every IPC send there must be an IPC receive method.

The basic structure of this call is

```js
ipcRenderer.sendSync (channel, [, arg1][, arg2], [,...})
```

The channel value is a string that is used as a message identifier. It is this identifier that the companion method will be listening for. You can optionally send additional values as arguments. These can be any JavaScript primitive (string, number, arrays, objects). In the spirit of communications, let's have our function send the famous words from Alexander Graham Bell:

```js
syncMsgBtn.addEventListener('click', function () { 
    const reply = ipc.sendSync('synchronous-message', 'Mr. Watson, come here.')
})
```

Whenever, we are working with IPC events, once we write our sending function, we switch to the other process and write the companion stub function. So, let's switch to the main.js file and do this.

The Main process will also need to import the IPC module as well.

```js
const ipc = electron.ipcMain
```

Now, we can write our receiver function. The function is straightforward, and we define which channel it should listen on, and a function to execute.

```js
ipc.on('synchronous-message', function (event, arg) {

})
```

Note: often when coding electron application, we have multiple files open at the same time. More than once, we have forgotten to save all the files and wonder why our code does not work. You might want to start to learn the key command to perform a save all to ensure all the files are saved and your code will execute properly.

The callback function has two arguments: the event object and the arguments. While the arguments will contain the data that our sending function passed over, the event object has some special functions. The event object has the built-in ability to respond to the sender. Meaning, there is no need to write another set of listeners and receivers to communicate a response.

For synchronous IPC messages, the method is `event.returnValue`. This value can be a string, a number or an object. For this example, let's just keep it a string.

```jd
ipc.on('synchronous-message', function (event, arg) {
  event.returnValue = 'I heard you!'
})
```

Switching back to the renderer.js file, we can now add the code to handle this returned value. The value that we sent over from the main process will be stored in the reply.

```js
syncMsgBtn.addEventListener('click', function () {
    const reply = ipc.sendSync('synchronous-message', 'Mr. Watson, come here.')
    console.log(reply)
})
```

We will then craft a simple message that we will display. Let's use the new templating feature in ES6 to do this. This is done using the `$()` syntax, so the message can be written as such:

```js
const message = `Synchronous message reply: ${reply}`
```

If you have not used the `${}` syntax before, it greatly improves the readability of your concatenated strings. You will also note we are using \` or back ticks instead of ' or ". This is another new habit to try to pick up. The advantage of using \` is you can now have your string extend for more than one line. However, in this case we don't need it.

With our message string constructed, we can update the innerHTML our paragraph:

```js
document.getElementById('syncReply').innerHTML = message
```

Here is the complete code:

```js
syncMsgBtn.addEventListener('click', function () {
    const reply = ipc.sendSync('synchronous-message', 'Mr. Watson, come here.')
    console.log(reply)
    const message = `Synchronous message reply: ${reply}`
    document.getElementById('syncReply').innerHTML = message
})
```

Save all the files and run the application. Click the button, and our message should appear in the window (Figure 6-3).

Figure 6-3. The result of our IPC call being displayed

This is the basics of using synchronous IPC within Electron. Now, let's explore using IPC messaging in an asynchronous fashion.

1-2『

跑不通，报错找不到 ipc 对象，说明没引用出来，还在看了下墨菲写数据流 electron 的代码，发现现在引用的方式改了，

```js
const {app, BrowserWindow, ipcMain} = require('electron')
const path = require('path')

ipcMain.on('synchronous-message', function (event, arg) {
  event.returnValue = 'I heard You'
})
```

目前还是跑步起来。（2021-03-27）

』—— 未完成


### 6.3 Asynchronous IPC Messaging

Often, the event that we trigger by sending our IPC message might take a noticeable amount of time for the method to finish and the response returned to the renderer process. This will leave our renderer process nonfunctioning. Certainly not the best user experience for your application. For these situations, we can use the asynchronous IPC methods instead.

Let's add two more elements to our HTML file, the result of this can be seen in Figure 6-3:

```html
<button id="sendAsyncMsgBtn">Ping Main Process Async</button>
<p id="asyncReply">Awaiting async response</p>
```

Figure 6-4. Our Electron application with the async UI ready

Switching to our renderer.js file, we will get the reference to our new button:

```js
const asyncMsgBtn = document.getElementById('sendAsyncMsgBtn')
```

then like before, we will create an event listener for the button click:

```js
asyncMsgBtn.addEventListener('click', function () {

})
```

There are two key differences in working with asynchronous IPC messages. The first is instead of using the sendSync method, we use the send method instead.

```js
asyncMsgBtn.addEventListener('click', function () { 
  ipc.send('asynchronous-message', ''That's one small step for man')
})
```

The other difference is that we now need to explicitly write the callback function that will handle the response from the Main process.

```js
ipc.on('asynchronous-reply', function (event, arg) { 
    const message = `Asynchronous message reply: ${arg}` 
    document.getElementById('asyncReply').innerHTML = message
})
```

The IPC code in the Main process changes slightly as well in the main.js file. The actual listener does remain the same, but the method to respond changes. Instead of calling the returnValue method on the Event object, we now use event.sender.send to respond.

```js
ipc.on('asynchronous-message', function (event, arg) { 
    if (arg === "That's one small step for man") { 
        event.sender.send('asynchronous-reply', ', one giant leap for mankind.') 
    }
})
```

Note: if we are using a different channel name for our asynchronous response, this allows us to have multiple ipC messaging flows occurring.

Go ahead and save the files and run the application. You should be able trigger both styles of IPC messaging (Figure 6-5).

Figure 6-5. Our Electron application, showing the results of our IPC call

### 6.4 Managing Event Listeners

Much like we probably heard as a child about cleaning up after yourself, the same holds true for any event listener or IPC listener we might create within our Electron application. The IPC modules have the same syntax for either the sync or async process. If we want to remove a single listener from the method on the Main process, the syntax is:

```js
ipcMain.removeListener( channel name, function)
```

and from the Renderer process:

```js
ipcRenderer.removeListener( channel name, function)
```

The function should be the reference to the function that was executed by the on method.

If you need to remove all the listeners on a specific channel, you can use the removeAllListeners method to do so. Here is the basic syntax:

```js
ipcMain.removeAllListeners(channel)
```

and

```js
ipcRenderer.removeAllListeners(channel)
```

In both of our earlier examples, our two event listeners had their functions defined within the listener itself. For example, if our Main process needed to know if a user had logged into our system, we could have this event shell:

```js
function userDidLogin() { 
  ipcRenderer.on('userLogin', this.handleLoginSuccess);
}

function userDidLogout() { 
  ipcRenderer.removeListener('userLogin', this.handleLoginSuccess);
}

function handleLoginSuccess(event, args) { 
  console.log('data', args.data);
}
```

This could be tied to changing a Menu Item based on the user's login status, or some other method. For this example, once we have had the state change, there is no need to keep listening for that event. By removing it, that is one less thing our application must concern itself with.

Electron's IPC module provides one more useful methods along these same lines. That method is:

```js
ipc.once(channel, listener)
```

This method is available for both the Main and Renderer process. The method will listen on the specific channel. Once it has received the event, it will execute the listener function, then remove itself from the IPC listeners.

### 6.5 Summary

Although the IPC module does not have a lot of methods – just variations of sending and receiving – it is the backbone for our Electron processes to coexist. You will use this module to possibly start a third-party Node library in the Main process from a user action in the Renderer process. In our next chapter, we will be leveraging them quite a bit to work with Electron's dialog module.
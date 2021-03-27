# 0301. The Electron Quick Start

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

## 3.1 Getting the Quick Start Code

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

## 3.2 Updating the Project to Make It Yours

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

## 3.3 The Main Process File

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

## 3.4 The Quick Start's Renderer Process

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

## Summary

There are many ways you can build your Electron application. If you go with a vanilla approach — that is, just using plain old JavaScript instead of a framework — this is the file you'll be working in. Since there are so many ways to build an Electron application, far too many to cover in one book, we will be focusing on leveraging Electron's features using simple JavaScript examples. Using the Electron Quick Start as a starting point for our exercises will be helpful in keeping this focus.
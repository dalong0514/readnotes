Debugging Your Electron Application

Hopefully, the only debugging that you have had to do, so far, while exploring this book, has been to fix a simple typo. But, there will come a time as you begin to develop your Electron application that you will need to debug your code in a more complex fashion. In this chapter, we will look at some of the tools and techniques available to you.

Chromium's Dev Tools

You should already be familiar with the primary tool that you can use to debug your Renderer process, the built-in Dev Tools from Chromium. By default, the electron-quick-start code base has these tools enabled. To display the DevTools, simply call

mainWindow.webContents.openDevTools()

This command will then open a copy of the DevTools within our application's window, as shown in

Figure 13-1. These are the same tools that you have probably used when debugging in Google Chrome.

© Chris Griffith, Leif Wells 2017 C. Griffith, L. Wells, Electron: From Beginner to Pro, https://doi.org/10.1007/978-1-4842-2826-5_13

199

Chapter 13 ■ Debugging Your eleCtron appliCation

Figure 13-1. Chrome Dev Tools

We can inspect individual HTML elements and explore the CSS styles for them as well. The familiar

JavaScript console is available, allowing us to examine our JavaScript code's outputs.

There are two other related Electron commands you should be aware of. If you want to close the

instance of the DevTools, you can simply call

mainWindow.webContents.closeDevTools()

But, rather than manage the hiding and showing of the DevTools while you are developing, often an additional set of menu items is added that is specific to debugging. This is a technique we use when developing our Electron project. It is nothing fancy, just a top-level menu named Debug and single menu item that allows us to toggle the display of the DevTools. The actual command is simply this:

mainWindow.webContents.toggleDevTools()

Here is the menu snippet for our Debug menu that you can insert into your menu definition:

{ label: 'Debug', submenu: [ {  label: 'Toggle Developer Tools',  accelerator: (function () {  if (process.platform === 'darwin') {   return 'Alt+Command+I'  } else {   return 'Ctrl+Shift+I'  }  })(),

200

Chapter 13 ■ Debugging Your eleCtron appliCation

click: function (item, focusedWindow) {  if (focusedWindow) {   focusedWindow.toggleDevTools()  }  } } ]}

We are passing the reference to the active BrowserWindow to our click function with the

focusedWindow parameter. This parameter will allow us to toggle the DevTools on the correct window if our Electron application has multiple windows.

For more on using Chrome's DevTools, see https://developer.chrome.com/devtools for a detailed

tutorial on using them.

Debugging the Main Process

While the Chrome DevTools allows us to debug the Renderer Process, debugging the Main Process requires some additional changes to do so. Since the Main Process is our Node process, it executes without being directly exposed. To debug any code that is running within this process, we must rely on external debuggers that support the V8 debugging protocol. Two common tools that support this are VS Code and node-inspector.

Debugging the Main Process in VS CodeOne of the easiest methods to debug Electron's Main Process is to use the built-in debugging tools in VS Code. VS Code has built-in debugging support for Node.js and can debug JavaScript, TypeScript, and any other language that gets transpiled to JavaScript.

For those unfamiliar with the term transpiling, it is the process of taking one language and

■ Note re-creating it in another. examples are writing in CoffeeScript and producing standard JavaScript.

To use this, we need to add a debug configuration to our project. First, we need to create a .vscode

directory if one does not already exist, at the top level of our project. Within this directory, create a launch.json file. This file will contain the debug configurations that VS Code will use to connect to our instance of our Electron app.

{ "version": "0.2.0", "configurations": [ {  "name": "Debug Electron Main Process",  "type": "node",  "request": "launch",  "cwd": "${workspaceRoot}",  "runtimeExecutable": "${workspaceRoot}/node_modules/.bin/electron",  "program": "${workspaceRoot}/main.js" } ]}

201

Chapter 13 ■ Debugging Your eleCtron appliCation

For Windows, use "${workspaceRoot}/node_modules/.bin/electron.cmd" for a runtimeExecutable.With VS Code set up to debug our Main Process, let's try it out. Add a breakpoint in your main.js file by double-clicking in the left gutter on the line you want the breakpoint to be added, as shown in Figure 13-2. Next, switch to the Debug view in VS Code (Shift-Cmd-D).

Figure 13-2. VS Code's Debug Panel

202

Next, make sure the Debug Electron Main Process configuration is selected from the drop-down menu

in the debug pane, as shown in Figure 13-3.

Chapter 13 ■ Debugging Your eleCtron appliCation

Figure 13-3. The Debug Target option menu

203

Chapter 13 ■ Debugging Your eleCtron appliCation

Then click the green debug button next to that menu. VS Code will then launch Electron for you and

once a breakpoint is reached, give you the ability inspect your code's state, as shown in Figure 13-4. In earlier version of VS Code, there were reported issues using this. The suggested workaround was to uncheck both the Exceptions breakpoint options. According to the filed issue on Github (https://github.com/Microsoft/vscode/issues/16321), this problem has been resolved. But there is nothing more frustrating than not being able to debug to a bug.

Figure 13-4. The debugger in VS Code for the main process

For more information on debugging with VS Code, visit https://code.visualstudio.com/Docs/

editor/debugging.

Debugging the Main Process in node-inspectorIf your background is more of a NodeJs developer, rather than a front-end developer, you might be more familiar using a tool like node-inspector, as shown in Figure 13-5. To use this solution with Electron, we need to perform several installation steps.

204

Chapter 13 ■ Debugging Your eleCtron appliCation

First, we need to install the node-gyp required tools. For those unfamiliar with node-gyp, it is a cross

platform command-line tool written in Node.js for compiling native add-on modules for Node.js. Detailed instructions for this installation can be found at: https://github.com/nodejs/node-gyp#installation

Next, we can install node-inspector itself. This package wraps the node-inspector package to work with

Electron.

npm install node-inspector --save-dev

Now, the next installation is the node-pre-gyp package. This package is an interface between npm and

node-gyp, and allows the use of C++ addons from third party binaries.

npm install node-pre-gyp

With both packages installed, let's go ahead and recompile the node-inspector v8 modules for Electron.

$ node_modules/.bin/node-pre-gyp --target=VERSION --runtime=electron --fallback-to-build --directory node_modules/v8-debug/ --dist-url=https://atom.io/download/atom-shell reinstall$ node_modules/.bin/node-pre-gyp --target=VERSION --runtime=electron --fallback-to-build --directory node_modules/v8-profiler/ --dist-url=https://atom.io/download/atom-shell reinstall

■ Note

You will need to update the target argument to be your electron version number.

Now, we need to be able to run Electron with the debug port enabled. This is done with a command-line switch, --debug=[port]. With this switch, Electron will listen for the V8 debugger protocol messages. The default port is 5858. You can either launch Electron directly from the command line using

electron --debug=5858 .

or you can edit the scripts in package.json file to include this switch:

"scripts": { "start": "electron --debug=5858 ."}

If you want to pause execution on the first line of JavaScript, use the –debug-brk switch instead

electron --debug-brk=5858 .

With Electron running, open another terminal window to be able to start the node-inspector server.

ELECTRON_RUN_AS_NODE=true path/to/electron.app|exe node_modules/node-inspector/bin/inspector.js

Now, open http://127.0.0.1:8080/debug?ws=127.0.0.1:8080&port=5858 in Chrome. You may have

to click pause if starting with --debug-brk to force the UI to update.

205

Chapter 13 ■ Debugging Your eleCtron appliCation

Figure 13-5. node-inspector working with our Electron app

You can now use the node-inspector to debug your application.

Chrome DevTools Extensions

Chrome's DevTools can be extended using add-on extensions. This can be quite useful, as you will probably be building your Electron application with an additional framework like React or Angular. The following DevTools Extensions are tested and guaranteed to work in Electron:

•	•	•	•	•

Ember Inspector

React Developer Tools

Backbone Debugger

jQuery Debugger

AngularJS Batarang

206

Chapter 13 ■ Debugging Your eleCtron appliCation

Vue.js devtools

•	•	 Cerebral Debugger•

Redux DevTools Extension

To use one of these extensions, visit http://electron.atom.io/docs/tutorial/devtools-extension/

for the steps for their installation.

Devtron

There is also a dedicated DevTools extension just for Electron known as Devtron. This extension was built to focus on some Electron-specific needs, like monitoring IPC messages and linting. Installing Devtron is on a project-by-project basis. For our look at what this extension can do, we will use the sample app we built when exploring Electron's IPC system. With your command line's working directory set to that project, type in the following command:

npm install devtron --save-dev

This will install the package for use as a development-only dependency. Go ahead and launch our

Electron application using npm start.

To use Devtron with your Electron application, you will need to be able to access Chrome's DevTools,

as shown in Figure 13-6. The DevTools extension should be now loaded and available as an option along the top of the DevTools window.

Figure 13-6. Devtron's user interface

Let's explore the five sections in Devtron

207

Chapter 13 ■ Debugging Your eleCtron appliCation

Require GraphAs your Electron application grows in complexity, you will be relying on the use of more and more libraries. The Require Graph pane, shown in Figure 13-7, allows you to view and trace the loading order of your JavaScript files. To see the output of this inspection, click the Load Graph button.

Figure 13-7. The Require Graph interface

Not only can we see the load order of our libraries, but we see the dependencies as well. If you start to

encounter startup time issues or rendering slowdowns, using this graph might help you uncover the bottleneck.

208

Chapter 13 ■ Debugging Your eleCtron appliCation

Event ListenersDevtron enables you to explore the events and listeners that your app has registered, as shown in Figure 13-8. Unfortunately, it will only listen on the core Electron APIs, meaning that none of your custom listeners will be tracked, like a button press in the UI. But as you build out your application, you will begin to interact more with these core events to provide your user a more native application experience, and you will want to ensure they are properly registered and active.

Figure 13-8. Devtron's Event Listener interface

Here we see our application's createWindow function that is call from the electron.remote.app ready event.

209

Chapter 13 ■ Debugging Your eleCtron appliCation

IPC MonitorDuring our exploration of using Electron's IPC module, we tracked the messages using simple console logging. Devtron's IPC monitoring panel allows you to track and inspect the IPC messages (both synchronous and asynchronous), as shown in Figure 13-9. Since the IPC messaging traffic can be quite heavy in a complex application, you need to manually enable the event recording. Click the Record in the toolbar to start the recording. If you have any IPC messages you can trigger, go ahead and trigger them. Each IPC channel is logged, along with the arguments that are passed.

Figure 13-9. Devtron's IPC monitoring interface

Here we see the results of triggering our sample sync and async IPC messages from our sample IPC

application in Chapter 6.

210

Chapter 13 ■ Debugging Your eleCtron appliCation

LinterDevtron also provides some application-level linting that you can invoke. While it does not go deep into your code and check for application-specific issues, the Devtron linter will check your application for some common issues like handling various error events, as shown in Figure 13-10.

Figure 13-10. Devtron Lint Check interface

For our simple IPC demo application, the linter reported:

•	 We were not using the most current version of Electron.•	 We had bundled our app into an asar archive.•	 We do not handle the crashed event.•	 We do not handle the unresponsive event.•	 We do not handle the uncaughtException event.

While not an issue for our demo, when building a releasable application, these are items that your code

should address.

211

Chapter 13 ■ Debugging Your eleCtron appliCation

AccessibilityDevtron will also perform a basic accessibility audit of your application. Click the Audit App button to have Devtron scan your app for common accessibility issues, as shown in Figure 13-11.

Figure 13-11. Devtron's Accessibility interface

For example, we failed the accessibility requirement to have the content's human language indicated.

This is an easy fix to perform. In the index.html, replace <html> with <html lang=「en」>. To learn more about what each of these issues refers to, use the docs button to view a detailed guide on the rule Devtron uses.

As you can see, Devtron can provide some useful tools when debugging your Electron application.

Spectron

Most commercial grade applications will employ some form of automated testing for their application. Spectron is a framework that allows you to write your integration tests for your Electron app. It is built using a combination of ChromeDriver and WebdriverIO, so both the Main Process and Renderer Process can be tested.

To install Spectron, simply navigate to your project's main directory and run

npm install spectron --save-dev

Spectron supports working with continuous integration services like Travis or AppVeyor, and is

compatible with many testing libraries like Mocha, Jasmine, and Chai. Now, writing the actual tests is beyond the scope of this book, but to learn more about Spectron, visit https://electron.atom.io/spectron/.

Summary

As developers, you are always striving to ship a product without any bugs or issues. In this chapter, we explored several techniques and tools you can use to debug the special nature of an Electron application. For those looking to leverage integration testing of their application, we introduce you to the Spectron module.212

CHAPTER 14

Testing with Spectron


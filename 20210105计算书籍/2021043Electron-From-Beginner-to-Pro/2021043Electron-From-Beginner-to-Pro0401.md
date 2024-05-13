# 0401. BrowserWindow Basics

As explained in earlier chapters, the Renderer Process is where your application appears. The Renderer Process uses Chromium to render your user interface. The Main Process creates Renderer Processes by creating instances of the BrowserWindow object.

In this chapter, we explore the basic options for creating BrowserWindow instances as well as explore the frameless and transparent window types.

## 4.1 Getting Started

Let's take a moment to make this package.json match our own by updating some nodes.

1 Change the name node to "browser-window-sample".

2 Change the version number to "0.0.1" since we are just starting out. If you are unfamiliar with semantic versioning, version numbers are broken into three elements: MAJOR.MINOR.PATCH. As this is our starting point, we will begin numbering with 0.0.1.

3 In the description let's use something like "A sample Electron application to demonstrate BrowserWindow creation".

4 Remove the repository property. If you decide to put your results in a repository you can change or re-add this property with the correct address.

5 Keywords can be "Electron," "BrowserWindow," "sample".

6 "author": Your name goes here.

7 If you wish to change the licensing type, you can do that with this property. By default, it is set to Creative Commons 1.0 Universal. There are many alternative options available; choose the one that best suits your needs.

### 4.1.1 Disabling Chrome DevTools

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

## 4.2 Update Code to Use the ready-to-show Event

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

## 4.3 BrowserWindow Options Argument

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

### 4.3.1 Basic Window Properties (width, height, minWidth, minHeight, maxWidth, maxHeight)

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

### 4.3.2 The center, x and y Properties

You may notice that this code is not passing a center property in the options argument. Best practices suggest that if your application is a single window application, it should initially appear in the center of the screen. Since our example application is loading in the center of the screen, we can assume that the default setting for center is true even though the default is not currently documented.

Also, not appearing in our code are the x and y options, which control where the top left corner of the window will appear. The defaults for these options are to center the window. That is, when you do not pass the x and y options as part of the options argument for BrowserWindow, Electron does the math taking the width and height properties along with screen dimensions and sets the x and y properties so that the window is centered. Setting the x and y options essentially turns the center option to false.

The x and y options are the only options that are optionally required. What does that mean? If you pass the x option you must pass the y option. The same goes when passing the y option; the x option must be passed as well. If you pass either of these options by themselves, the option is ignored.

For the purposes of this exercise, these properties will not be added to our code. The default settings will do.

### 4.3.3 The resizable and movable Properties

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

### 4.3.4 The title Property

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

## 4.4 Other Window Types

While the windows we have been creating so far in this chapter are typically the kind of windows applications will use, there are two other window types we should mention: frameless and transparent windows.

### 4.4.1 Frameless Windows

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

### 4.4.2 Transparent Windows

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

## 4.5 Summary

In this chapter, we explored the basic options of BrowserWindow creation: show, width, height, minWidth, maxWidth, minHeight, maxHeight, resizable, movable, and alwaysOnTop. We also explored two window types: frameless and transparent. The knowledge we gained here will help us as we move into the next chapters.
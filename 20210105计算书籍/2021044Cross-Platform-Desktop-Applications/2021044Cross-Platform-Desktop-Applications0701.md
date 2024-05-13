Part 3 Mastering Node.js desktop application development

Many APIs are available in desktop application frameworks to help provide features like accessing the webcam and clipboard, opening and saving files to the hard disk, and more. This part explores the various ways in which NW.js and Electron allow you to add a number of features to your desktop apps.

Chapters 7, 8, and 9 look at ways to control the look and feel of your desktop apps, from controlling the window dimensions and full-screen behavior, through to creating menus and making tray apps.

Chapter 10 explores how to implement drag-and-drop functionality in your apps through HTML5 APIs, and chapter 11 shows you how to integrate webcam functionality for taking photos from your computer’s webcam and saving them to disk.

Chapters 12 and 13 deal with different ways you can store and access app data and how to access data in the OS clipboard.

Toward the end of this part of the book, we’ll look at using keyboard shortcuts to implement controls for a game, and how to integrate a real-time Twitter feed into a desktop notifications app.

第 3 部分 精通 Node.js 桌面应用开发

在桌面应用开发框架中，有很多 API 提供了像访问 webcam 和剪贴板、在磁盘上打开和保存文件等这样的功能。这部分将介绍如何使用 NW.js 和 Electron 为你的桌面应用添加一系列功能。

第 7、8、9 章介绍如何控制桌面应用的样子，从控制视窗大小、全屏显示等，到创建菜单以及制作托盘应用。

第 10 章介绍如果在应用中使用 HTML5 API 实现拖曳功能，第 11 章将展示如何将 webcam 功能集成到应用中，实现通过计算机的 webcam 来拍照以及将照片保存到磁盘上。

第 12 章和第 13 章介绍使用不同的方法来保存和获取应用数据，以及如何访问操作系统剪贴板上的数据。

在这部分结束的时候，我们会介绍使用键盘快捷键来操作游戏，以及将推特的推文列表整合到一个桌面提醒应用中。

# 0701. Controlling how your desktop app is displayed

自定义桌面应用的外观

## Summary

In this chapter, we’ve looked at different ways in which you can craft your app’s display, depending on what the app needs to do for the user. Some quick takeaways:

1 You can create windowed apps with specific width and height dimensions.

2 You can restrict those dimensions so that the app’s display stays fixed.

3 It’s easy to run your app in full-screen mode for videos and gaming.

4 Alternatively, you can remove the app window and run it as a frameless app.

5 Be careful with frameless apps because they come with some UI quirks you’ll need to handle around dragging, click events, and text selection.

6 Kiosk-mode apps are useful for ATMs and apps running in public areas.

The first thing to think about with crafting your app is whether the app needs to operate within a fixed or dynamic window, or even if it needs a window at all. Then, you can configure the window options in the package.json manifest file to make the app window constrained to specific dimensions, or expand to take up the full screen. Also, remember that depending on whether your app is window-based or even a kioskmode app, the ability to navigate is important, so make sure you can exit a kiosk app from somewhere within the app’s UI.

In chapter 8, we’ll look at implementing tray applications with NW.js and Electron.

在本章中，我们介绍了如何根据应用的需求来定制应用的界面样式。快速过一下在本章中学到的内容：

1、可以创建指定宽高尺寸的应用。

2、可以限制尺寸，从而让应用保持在一个固定的尺寸范围内。

3、可以很容易地让应用进入全屏模式来播放视频或者玩游戏。

4、也可以移除应用视窗，让它成为无边框的应用。

5、对于无边框的应用要非常小心，因为你需要自己处理拖动、单击事件以及文本选中操作。

6、kiosk 模式对于运行在 ATM 机以及其他公共场所中的应用来说非常有用。

当定制应用的时候，首先要思考的就是应用是否需要在一个固定的或者动态的视窗中操作，甚至是否真的需要视窗。然后，你可以通过在 package.json 文件中配置 window 选项来设置将应用固定在指定的尺寸上，或者进入全屏模式。还有，记住根据应用是否是基于视窗的还是需要进入 kiosk 模式，能够在应用内进行导航是很重要的，因此需要确保你可以在应用内退出一个 kiosk 模式下的应用。

在第 8 章中，我们会介绍如何使用 NW.js 和 Electron 来构建托盘应用。

## 7.0

This chapter covers: 1) Controlling the application window. 2) Setting the application window's dimensions. 3) Making applications run in full-screen mode. 4) Creating kiosk applications.

When you build a desktop app, one of the first considerations is how the user will interact with it. Will it be a windowed app that can operate at the same time as other apps, a publicly accessible terminal in a bank, or an immersive experience that will consume all of the user’s attention, like a game?

A desktop app can take many forms. It can operate in a window that can be maximized and minimized as needed, or run in full-screen mode, like a video game. In this chapter, we’ll explore options for controlling the way the app is displayed to the user, and I’ll show you some methods that will come in handy when you’re building apps.

本章要点：1）控制应用视窗。2）设置应用视窗的尺寸。3）全屏模式运行应用。4）创建一个 kiosk 应用。

构建桌面应用时，首先要考虑的事情之一就是用户如何使用应用。是和其他应用一样提供一个视窗让用户始终在其中进行操作呢，还是像银行的终端那样，又或者是像游戏那样提供一个沉浸式的体验，让用户沉醉在其中。桌面应用的形式有多种。它可以最大化展示，也可以最小化展示，或者像游戏应用那样全屏运行。在本章中，我们会介绍多种控制应用展现的方案，而且我会教你一些构建应用时很容易上手的方法。

## 7.1 Window sizes and modes

User interfaces come in a range of different dimensions; traditional IM apps like AIM or MSN Messenger (if you’re old enough to remember them) tended to have a long portrait window listing many contacts that users would want to chat with. Over time, apps like Slack and Gitter have approached the world of IM with a different window size, much in the style of a forum, and to accommodate longer messages and images (there’s a tendency in Slack communities to use a lot of animated GIFs). Window sizes for apps need to provide the best possible UX, so it’s important to be able to make them fit the dimension required for the UI. Figure 7.1 shows an example.

Figure 7.1 Skype in action. Notice the tall style of the UI, accommodating mainly chat messages.

In NW.js and Electron, there are multiple ways to configure the window. We’ll take a look at how you can configure an app window’s width and height in NW.js.

7.1.1 Configuring window dimensions for an NW.js app

NW.js allows you to configure the window’s width and height via the package.json file. In the GitHub repository for this book, the chapter-07 folder holds a copy of the example NW.js app called window-resizing-nwjs. The code for it looks like this:

This is a pretty basic HTML file, containing an h1 element inside the body tag with the words Hello World, much like the Hello World examples shown earlier in this book. If you want to add window dimensions to the app, you can adjust them to work by using this for the package.json file:

{

"name" : "window-sizing-nwjs", "version" : "1.0.0", "main" : "index.html", "window" : {

"width" : 300,

"height" : 200 }

}

The window’s width and height are specified in pixels. This allows you to make sure that when the app opens, its width and height are set at those dimensions. This is one way you can control the window’s width and height. Figure 7.2 shows an example of what the changes look like.

This demonstrates how you can control the app window’s initial width and height in NW.js. How do you do the same with Electron?

Figure 7.2 An app with window properties applied. You can see here that the app is small.

7.1.2 Configuring window dimensions for an Electron app

Electron’s ability to configure window dimensions is similar to that of NW.js, but the approach is different. Where NW.js allows you to specify the configuration in the package.json manifest file, Electron requires that you configure window dimensions at the point in which the app window is initialized.

In the book’s GitHub repository, you’ll find an Electron app inside the chapter-07 folder called window-sizing-electron. Here’s what the code for that app looks like:

{

"name" : "window-sizing-electron", "version" : "1.0.0", "main" : "main.js"

}

And then there’s the accompanying index.html file that you’ll display:

Finally, the place where the magic happens: the main.js file, shown next.

Listing 7.1

The main.js for the Electron window sizing app

'use strict';

const electron = require('electron');

const app = electron.app; const BrowserWindow = electron.BrowserWindow;

let mainWindow = null;

app.on('window-all-closed', () => {

if (process.platform !== 'darwin') app.quit(); });

app.on('ready', () => {

mainWindow = new BrowserWindow({ width: 400, height: 200 }); mainWindow.loadURL(`file://${__dirname}/index.html`);

mainWindow.on('closed', () => { mainWindow = null; });

});

Where the width and height of the window are set

Now, you can run the app with electron . from the Terminal or Command Prompt, and you should see the app pop up looking like figure 7.3.

Figure 7.3 The Electron app running with a dimension of 400-pixel width and 200-pixel height. Notice that the app looks like it’s running in an extreme landscape mode.

Electron’s approach means you have fine-grained control over the dimensions of each app window. For more details on all the attributes you can pass into the creation of a BrowserWindow object instance, see http://electron.atom.io/docs/api/browser-window/.

That covers adjusting the size of the app window at loading time. Now, we’ll look into how to get greater control over those window dimensions for the app.

7.1.3 Constraining dimensions of window width and height in NW.js

If you want to prevent the users of your apps from changing the width and height of your desktop app (and causing the UI to look skewed and weird), you can pass the options listed in table 7.1.

Property
Description
max_width
max_height
min_width
min_height
Sets the maximum width of the window Sets the maximum height of the window Sets the minimum width of the window Sets the minimum height of the window
Options to restrict window resizing 
Here’s how it would look in the package.json file: 
"window": { "max_width": 1024, "min_width": 800, "max_height": 768, "min_height": 600 } 
Figure 7.4 shows what dimensions are affected in the app window. 
Max/min height 
Max/min width 
Figure 7.4 The window dimensions affected by the max/min width and max/min height 
In the example JSON payload, you constrain the width of the window so that it can’t be greater than 1024 pixels or less than 800 pixels. You also constrain the height of the window to be no greater than 768 pixels and no less than 600 pixels. Being able to constrain the window width and height (even when the user attempts to resize them) gives you greater control over making sure the look and feel of the app fits with the intended design. 

This is good when you know what window dimensions you want to constrain to when the app loads. But what if you want the app window’s width and height to be set to dynamic values, such as an app displaying an image (where the window’s width and height match the dimensions of the image)?

The good news is that there’s a way to do that with NW.js’s window API. Say you have an image on your computer with dimensions of 900 x 550 pixels, and you want to size the window to match. You can set the width and height of the window to 900 pixels wide and 550 pixels high with the code shown in the following listing.

Listing 7.2

Dynamically resizing the app window

const gui = require('nw.gui');

const win = gui.Window.get();

win.width = 1024; win.height = 768;

References GUI API in NW.js

Sets width and height of window dynamically

Uses GUI API to select current app window

Being able to resize the window programmatically lets you make the app window match the dimensions of the content inside it and therefore give a better experience to the user.

You can also use the same API to control where the window is rendered on the screen. The GUI API in NW.js allows you to position the window at a set of coordinates relative to the screen. The next listing shows an example of doing this programmatically with NW.js.

Listing 7.3

Positioning the window relative to the screen

const gui = require('nw.gui');

const win = gui.Window.get();

win.x = 400;

win.y = 500;

Sets horizontal coordinate of app window

Sets vertical coordinate of app window

This code affords you the ability to determine exactly where on the screen the app window will be positioned, which is good in the case of utility applications and the like.

We’ll now take a look at how Electron handles constraining app windows.

7.1.4 Constraining dimensions of window width and height in Electron

The settings for constraining the dimensions of app windows in Electron are defined on the BrowserWindow instance. You’ll remember from earlier in the chapter that to create an app window, you have to initialize an instance of the BrowserWindow class in the code.

Listing 7.4

Initializing a BrowserWindow instance in Electron

'use strict';

const electron = require('electron'); const app = electron.app; const BrowserWindow = electron.BrowserWindow;

let mainWindow = null;

app.on('window-all-closed', () => { if (process.platform !== 'darwin') app.quit(); });

app.on('ready', () => {

Passes options to BrowserWindow instance

mainWindow = new BrowserWindow({ width: 400, height: 200 }); mainWindow.loadURL(`file://${__dirname}/index.html`);

mainWindow.on('closed', () => { mainWindow = null; });

});

The mainWindow variable is an instance of the BrowserWindow class of Electron and is passed an object containing the width and height for the window. Here, you can set the maximum and minimum width and height properties for the app window. Say, for example, you want to make sure that the app cannot be resized below 300 px wide and 150 px high, and cannot be resized beyond 600 px wide and 450 px high—you can pass these options into the BrowserWindow instance:

mainWindow = new BrowserWindow({ width: 400, height: 200, minWidth: 300, minHeight: 150, maxWidth: 600, maxHeight: 450 });

Table 7.2 shows the properties to change for the window width and height.

The approach taken by Electron is nice because it lets you define individual settings for each app window that your app creates, and you can configure all of those settings in one place in the code, rather than look for them in separate places in the code. It’s simpler than in NW.js, and where NW.js uses snake case (as in max_width) property names, Electron uses camel case (as in maxWidth) property names, JavaScript-style.

By default, Electron renders the app in the middle of the screen. If you want to position the app window in a specific area of the screen, you can control this by passing x and y coordinates to the initialization of the BrowserWindow, like this:

mainWindow = new BrowserWindow({ width: 400, height: 800, x: 10, y: 10 });

The position of the window is set to begin at 10 pixels from the left (x) and 10 pixels from the top (y), and so it offers you the ability to control where you position the app window on the screen.

Having explored window sizing and positioning, we’ll now look at how to configure the app to run as a frameless application, or even in full-screen mode.

7.2 Frameless windows and full-screen apps

When you visit a train station and look at the display of train times and announcements, chances are the display is powered by a desktop app running in full-screen mode. Touch-screen monitors such as ATM machines also run desktop apps that are designed to prevent users from exiting the app, known as kiosk apps. Computer games also exhibit the same behavior, so the need for building apps that hide the underlying OS is a common one.

Electron and NW.js allow developers to tailor their apps so that they run in fullscreen mode (for video playback and games), as well as frameless (for media players and other utilities) and kiosk (for information kiosks and point-of-sale applications). We’ll take a look at how NW.js enables this and then look at Electron’s approach for comparison.

7.2.1 Full-screen applications in NW.js

Video games are a prime example of apps that run in full-screen mode when they first boot up. Recent versions of Mac OS have enabled apps to operate easily in full-screen mode, and NW.js takes advantage of this feature in two ways: via configuration options in the package.json manifest file, or dynamically via the JavaScript API. The following code is an example of enabling your desktop app to run in full-screen mode when it launches via the package.json file:

{

"window": { "fullscreen": true }

}

If you put the following JSON into the package.json file of an NW.js desktop app and then run the app, you can expect to see the app go straight into full-screen mode upon launch, where the title bar is not visible and the contents of the app take up the entire screen.

Alternatively, if you want to prevent users from being able to make an app enter full-screen mode, you can set the value to false.

As mentioned earlier, it’s possible to make the app go full-screen programmatically via NW.js’s native UI API, as follows:

const gui = require('nw.gui'); const window = gui.Window.get(); window.enterFullscreen();

Say you have a dead-simple NW.js app (such as a Hello World example), and you want a screen click to trigger full-screen mode. The app has some simple HTML for the home page, as shown next.

Listing 7.5

Example of programmatically triggering full-screen mode

Insert that into the main index.html file for the app and run the app from the command line with nw. You should see a screen like figure 7.5.

Figure 7.5 App with a button that turns on fullscreen mode when clicked

Click the Go Full Screen button and you should see the app go to full-screen. So how did that happen? Going through the HTML, you can see some embedded JavaScript that called out to NW.js’s GUI API, fetched the current window, and told it to enter

full-screen mode. You wrapped the call to enter full-screen mode in a function called goFullScreen, which the button element in the page triggered when clicked.

This is all good, but what if you’re already in full-screen mode and want to leave that mode? NW.js accommodates this as well. You can modify the existing code so that it can call the API function leaveFullscreen, but the trick here is to track what the current state of the window is (whether it’s already in full-screen mode). You can find out what the mode of the app window is with an API call called isFullscreen.

You’ll modify the previous example so that when the button is clicked and the app window enters full-screen mode, the button will change its text to “Exit Full Screen” and leave full-screen mode. Replace the HTML in the index.html file with this code:

This replaces the goFullScreen function with a toggleFullScreen function that makes an API call to determine whether the app window is in full-screen mode. The API call returns either true (it is in full-screen mode) or false. The function is called when the user clicks the button. When the user first clicks it, the function will enter into full-screen mode (because the app isn’t initially in full-screen mode). It will also change the text on the button to read “Exit Full Screen” to reflect the fact that the app is in full-screen mode. When the user clicks the button a second time, because the app window is in full-screen mode, you’ll leave that mode, and alter the text of the button to read “Go Full Screen.” This behavior allows the user to toggle full-screen mode in a simple and easy-to-understand fashion.

After you’ve changed the HTML and reloaded the app from the command line, click the Go Full Screen button. Not only should the app window enter full-screen mode, the button should now display “Exit Full Screen,” as shown in figure 7.6.

Figure 7.6 Example app in fullscreen mode. Notice that the button text has changed to allow the user to exit full-screen mode.

Being able to enter and exit full-screen mode in desktop apps can be handy, particularly when it comes to video playback. In fact, due to a bug that existed with supporting full-screen playback of videos in NW.js apps (see issue #55 on the GitHub repository), we (at Axisto Media) managed to work around the issue for our British Medical Journal (BMJ) app by accessing the shadow DOM of the video element and toggling the full-screen mode when the user clicked the Play/Pause button.

Full-screen mode enables users to take full advantage of the screen when using the app and display it in such a way as to eliminate the distractions of other windows in the background.

Now that you’ve seen how this is done in NW.js, we’ll take a look at how Electron handles supporting full-screen applications.

7.2.2 Full-screen applications in Electron

Electron also offers configuration for full-screen mode. When creating a new BrowserWindow instance, you can set options to configure for full-screen mode. To make an Electron app run in full-screen mode when it’s started, pass the following configuration option when creating the BrowserWindow instance:

mainWindow = new BrowserWindow({fullscreen: true});

When the app runs, it will go straight into full-screen mode. This is a good option for an app that plays videos or games.

But what if you don’t want people to have this option? How do you disable it? Simple: you pass the fullscreenable property with a value of false when initializing the BrowserWindow instance, as demonstrated in the following code:

mainWindow = new BrowserWindow({fullscreenable: false});

This configuration option means that the user will not be able to make the app enter full-screen mode from the title bar. This can be useful in cases where you want to maintain the dimensions of an app’s user interface, such as with a small utility application.

If you want to be able to trigger this functionality programmatically, you’ll need to call a function on the mainWindow instance after it’s initialized. I’ll re-create the example that I made for NW.js, using Electron instead, so you can compare the two.

Listing 7.6

Code for the main.js file for the full-screen Electron example

'use strict';

const electron = require('electron');

const app = electron.app; const BrowserWindow = electron.BrowserWindow;

let mainWindow = null;

app.on('window-all-closed', () => {

if (process.platform !== 'darwin') app.quit(); });

app.on('ready', () => {

mainWindow = new BrowserWindow(); mainWindow.loadURL(`file://${__dirname}/index.html`);

mainWindow.on('closed', () => { mainWindow = null; });

});

Here, you see that the app code is pretty much standard. Next, you’ll create the index.html file that has the button for toggling between full-screen mode and window mode.

Listing 7.7

The index.html file for the full-screen Electron example

<html>

<head> <title>Fullscreen app programmatic Electron</title> </head>

<script src="app.js"></script>

<body> <h1>Hello from Electron</h1>

<button id="fullscreen" onclick="toggleFullScreen();">

Go full screen </button> </body> </html>

Loads client-side code as separate JavaScript file

Calls function in the app.js file called toggleFullScreen to do the toggling

As in the NW.js variant of the code, the app has a button that is used to trigger toggling between full-screen mode and window mode. The only difference here is that you load a separate app.js file that has the client-side code for toggling. Finally, you add a standard package.json file as from the previous Electron example, and then the code for the app.js file shown next.

Listing 7.8

The app.js file for the full-screen Electron example

Uses remote API to get current window page is being rendered in

const remote = require('electron').remote;

function toggleFullScreen() {

}

Uses remote API to interact with main process from renderer process

const button = document.getElementById('fullscreen'); const win = remote.getCurrentWindow(); if (win.isFullScreen()) {

win.setFullScreen(false);

button.innerText = 'Go full screen'; } else {

win.setFullScreen(true);

button.innerText = 'Exit full screen'; }

Calls BrowserWindow instance’s isFullScreen function to check if window is in full-screen mode

If so, switches to window mode by calling the instance’s setFullScreen function with false

If not, switches to full-screen mode

This is a good example of the difference in approaches between NW.js and Electron. Electron handles how the front-end calls to the back-end of the app by providing an API called remote. This allows the renderer process (front end) to send messages to the main process (back end), so that you can do things like get ahold of the BrowserWindow instance and interact with it. You can then call various functions on the BrowserWindow instance to inspect its current settings (such as whether it’s running in full-screen mode) and use that to determine whether to make it render in full-screen mode or windowed mode.

What other functions can I call on the BrowserWindow instance?

This book touches on some (but not all) of the functions that can be called on the BrowserWindow instance. There's a wide range of configuration options for the BrowserWindow class in Electron, like being able to make the title bar styling different in Mac OS X (such as what Hyper, Kitematic, and WebTorrent use).

For more about these configuration options and functions that can be called on initialized BrowserWindow instances, check out http://electron.atom.io/docs/api/browserwindow/.

This demonstrates how to toggle between full-screen mode and window mode in Electron. Next, we’ll look at how to make more-radical changes to your app UI, in the form of frameless apps.

7.2.3 Frameless apps

Although being able to make your apps go full-screen at the click of a button is fun, it may not be suited for your app’s purposes. Some apps, including media players, onscreen widgets, and other utility apps, run without displaying any of the app window around them, and instead display a unique UI. An example of this is the music player VOX on Mac OS X, shown in figure 7.7. Notice that the UI is custom, and there is no Mac OS X UI visible (no title bar, no traffic-light buttons, only a simple X to close the window).

Figure 7.7 VOX music player in Mac OS X, playing a song. Notice the distinct lack of Mac OS X’s UI elements and title bar.

CREATING FRAMELESS APPS IN NW.JS

These apps are known as frameless apps, and you can create them in NW.js as well. Alter the package.json manifest file so that the window section contains a property called frame, with the value set to false, as in this code sample:

You can modify the package.json further to allow for transparency behind the app’s screen, so that you can use rounded corners and create interesting interfaces. Changing the package.json to use this:

"window" : { "frame" : false, "transparent": true, "width": 300, "height": 150 }

You now have the basis for creating an app that’s similar in style to the interface style presented in the VOX app if you adjust the index.html file to look like the next listing.

Listing 7.9

Creating a frameless app with styled rounded corners

If you run the example via the command line, you’ll see the app on your desktop, as shown in figure 7.8.

Figure 7.8 A frameless app running on the desktop. The app style mimics an exaggerated version of the rounded-corner UI on VOX, to demonstrate how the app can have a transparent background.

Although this offers the chance to create some snazzy custom UIs for your desktop apps, bear in mind some caveats to using this approach. The first is that after disabling the window frame, you need to provide buttons for closing/minimizing the app window (alternatively, you can allow the user to close the app from the main toolbar of the OS).

It’s important to note that frameless apps aren’t draggable by default. This is because they have no UI element set (such as the title bar) that allows them to be dragged. That said, there’s a way to enable them to be dragged. The key is to use a custom CSS property on the HTML for the screen, known as –webkit-app-region.

For HTML elements that you want to make draggable (such as the body tag for example), apply the following CSS:

If you append this CSS property to the body tag in the embedded CSS stylesheet from the previous example and reload the app, you’ll see that it can now be dragged across the screen. I’d like to be able to say that’s all there is to it, but unfortunately that’s not the case. Applying this CSS property to the body tag makes all HTML elements within the app an area that will drag the app, including the text that says “Frameless app example.” Try selecting the text—you cannot. The entire contents of the DOM under the body tag are also draggable, which might not be the behavior that you want for that part of the app. How do you resolve this?

The answer depends on what the nature of the HTML element needs to do. If the HTML element in question is a clickable element, like a button or a drop-down field, then you’ll want to give those HTML elements the -webkit-app-region property with a value of no-drag, like this:

button, select { -webkit-app-region: no-drag; }

This will enable you to be able to click buttons without the draggable behavior kicking in. Alternatively, if the HTML elements in question are elements that you want to be able to select snippets of for copying and pasting into other documents and apps (such as p tags and img tags), then you can make them selectable by the -webkituser-select property alongside the –webkit-app-region CSS property with a value of no-drag:

p, img {

-webkit-user-select: all;

-webkit-app-region: no-drag; }

You’ll need to do this on all the HTML elements that you want to be selectable, as well as all UI elements that need to be clickable. It can be a bit of a pig, but it ultimately means that you can have a completely custom look to your UI and make your app stand out from the rest.

The final version of the index.html file should look like the following.

Listing 7.10

The index.html file for the transparent frameless app

Now you can drag the app around the screen and see the background behind the rounded corners. That gives you an idea of how you can approach creating transparent apps in NW.js. Now we’ll look at how the same can be done with Electron.

CREATING FRAMELESS APPS WITH ELECTRON

As demonstrated earlier in the chapter, Electron handles configuring app windows via the initialization of the BrowserWindow instance. You can make the app frameless or transparent by passing a property to the initialization of the BrowserWindow at runtime. The following code is an example of how to configure a frameless app in Electron:

mainWindow = new BrowserWindow({ frame: false });

The app will now run in frameless mode, and you’ll see something like figure 7.9.

Figure 7.9 An Electron app running in frameless mode. Notice how the content of the app is positioned so closely to the top and left of the app? The app’s corners are rounded by default as part of Mac OS X.

If you want to try this example for yourself, you can give it a spin in the chapter-07 folder of the GitHub repository at https://github.com/paulbjensen/cross-platformdesktop-applications, under the app example frameless-app-electron.

Electron also allows you to make app windows transparent by passing the transparent property in the following example:

mainWindow = new BrowserWindow({ transparent: true });

Figure 7.10 shows what a transparent Electron app looks like.

Figure 7.10 A transparent app in Electron. Notice how the background is completely transparent, but you can see the title bar buttons as well as the app's text.

Transparency in Electron is a great feature as long as it doesn’t complicate the UX. For small utility applications, this can be a useful attribute, but that depends on what the app is doing and whom it is for.

Some apps can run in environments where the user isn’t necessarily trusted with complete access to the computer, such as in public terminals with touchscreen interfaces. In the next section, we’ll look at implementing kiosk applications.

7.2.4 Kiosk mode applications

Sometimes you get the chance to build an app that will be used by lots of people, but with a catch—the app is public, such as the information area of a museum, or maybe a bank, and needs to be able to run in a mode where the user can’t quit the app and start messing around with the computer (not a prospect anyone wants to entertain). Apps like these need to restrict access to the underlying OS, as though they’re running at kiosks (which, in some cases, they are).

Kiosk mode in both NW.js and Electron is a locked-down mode where access to the underlying OS is difficult—in fact, being able to quit the app has to be manually added by the developer (otherwise, they have to physically reboot the computer to regain access to it).

CREATING KIOSK-MODE APPS IN NW.JS

To enable your app to run in kiosk mode, you’ll need to modify your package.json manifest file so that it has a property of kiosk with the value set to true, as in the following example:

You can go ahead and give this a try in one of the example apps, but (and it is a big but) make sure that nothing is left unsaved before you do.

This is because you might have to reboot your computer in order to regain access to it. In kiosk mode, the app automatically enters full-screen mode, but without the title bar. The only way you can exit the app is by pressing Alt-Tab or Ctrl-Alt-Del on the keyboard—otherwise, you’re stuck inside the app with no way out of it.

Say you need to build a kiosk app for someone, but you also need to be able to exit the program (in case there’s an issue with the OS). How do you do that?

The answer is to implement some kind of keyboard shortcut or button that when clicked or typed calls an API function on the app window called leaveKioskMode. Like the full-screen API functions, kiosk mode has equivalent API functions for entering/leaving kiosk mode, as well as for detecting whether the app window is in kiosk mode.

Imagine that you have an app that will run at a display kiosk and you want to provide a way for the IT systems administrator to get access to the computer’s OS without having to resort to rebooting the computer (in particular, if access to the computer’s power supply and reboot button is physically obscured). You decide to add a button called exit to the app window to help the administrator get back to the OS.

Make sure that the package.json file looks like this:

{

"name" "version" "main" "window" "kiosk" }

: "kiosk-mode-example-app", : 1.0, : "index.html", : { : true

}

And the index.html file should look like the following.

Listing 7.11

Kiosk app’s index.html file, with an essential toggle button

You’ll notice you use the same pattern you used for the first full-screen mode app example (click a button, exit mode). This is so you can easily demonstrate the functionality of being able to leave kiosk mode from the app. If you now run the app, you should expect to see something like figure 7.11.

Figure 7.11 An app running in kiosk mode. The app runs across the entire screen, and access to the OS is obscured.

Click the Exit button, and the app will leave kiosk mode and switch back to a normal window layout.

No, NW.js still allows users to quit apps using the global keyboard shortcuts (for example, Alt-F4 on Windows). The reason it allows this is because virus detection software will block apps that attempt to override access to these global keyboard shortcuts.

ARE ALL KEYBOARD SHORTCUTS BLOCKED BY KIOSK MODE?

This shows how you can create kiosk apps with NW.js. For Electron, the process for creating kiosk mode apps is dead simple.

CREATING KIOSK APPS WITH ELECTRON

Electron is able to make apps run in kiosk mode by passing one attribute to the initialization of the BrowserWindow instance called (can you guess?) kiosk. Here’s an example:

mainWindow = new BrowserWindow({ kiosk: true });

With the browser window configured this way, the app is able to run in full-screen mode, and the only way to quite the app is via the keyboard shortcut (Command-Q on Mac OS X, Alt-F4 on Windows/Linux).

But if you want to provide some form of programmatic access to kiosk mode and be able to toggle it via a button, you can do that in precisely the same fashion as you would with toggling the full-screen app example.

You can try the app from the source code in the kiosk-app-programmatic-electron folder in the chapter-07 folder of the book’s GitHub repository. The app is a pretty standard setup, but with distinct differences in the index.html and app.js files. The following listing shows what the index.html file looks like.

Listing 7.12

The index.html file for the programmatic kiosk mode Electron app

When the kiosk button is clicked, you expect it to call a function called toggleKiosk. This is a function that is defined in the app.js file, shown next.

Listing 7.13

The app.js file for the programmatic kiosk mode Electron app

const remote = require('electron').remote;

Defines toggleKiosk function that’s called when button is clicked

function toggleKiosk() { const button = document.getElementById('kiosk'); const win = remote.getCurrentWindow(); Detects if app is if (win.isKiosk()) { running in kiosk mode win.setKiosk(false); button.innerText = 'Enter kiosk mode'; If so, triggers exiting kiosk mode } else { and updating button text win.setKiosk(true); button.innerText = 'Exit kiosk mode'; If not, triggers entering kiosk } mode and updating button text

}

When running, the app is able to enter kiosk mode when the button is first clicked, and then is able to exit it when it has been put into kiosk mode. This allows you to create buttons for easily closing the app—say, if it’s running at a computer that doesn’t have keyboard access.

Kiosk mode is useful for apps that are used by members of the public, and where access to the underlying OS needs to be obscured. That said, as mentioned earlier, there are still ways to be able to escape from kiosk mode, so it’s not a complete guarantee of protection from those who know their way around, but at least it will keep the majority from messing around with computers in public areas.

7.1 视窗的尺寸和模式

界面可以有不同的尺寸：像 AIM 或者 MSN（岁数大的朋友可能知道这个应用）这样传统的即时消息应用通常窗体会比较长，用来展示可以聊天的联系人。随着时间的推移，像 Slack 和 Gitter 这样的世界级即时消息应用采用了不同的视窗尺寸，更多的是像论坛那样，为了更好地展示很长的消息以及大图（Slack 的用户会更多地使用 GIF 动图）。应用视窗的尺寸需要提供最好的用户体验，因此，让应用视窗符合界面要求就变得非常重要。图 7.1 展示了一个例子。

图 7.1 使用中的 Skype。注意视窗尺寸比较长，这是为了更好地展示聊天消息

在 NW.js 和 Electron 中，有很多方式可以配置视窗的尺寸。我们先来看一下如何在 NW.js 中配置应用视窗的宽度和高度。

7.1.1 配置 NW.js 应用的视窗尺寸

NW.js 可以让你通过 package.json 文件来配置视窗的宽度和高度。在本书的 GitHub 仓库中，在 chapter-07 文件夹中有名为 window-resizing-nwjs 的 NW.js 示例应用的代码。其代码如下所示：

这是非常简单的 HTML 文件，在 body 标签中包含了一个 h1 元素，其中有 Hello World 文字，和本书此前的 Hello World 示例类似。如果你想设置应用的视窗尺寸，可以通过 package.json 文件来实现：

视窗的宽度和高度单位是像素。上述设置可以确保应用打开的时候，视窗尺寸和你设置的一样。这是一种控制视窗尺寸的方式。图 7.2 展示了启动后应用视窗的样子。

图 7.2 设置了视窗大小的应用，你会发现应用视窗变小了

上述例子展示了如何在 NW.js 应用中设置视窗的初始宽度和高度。那么在 Electron 中要怎么做呢？

7.1.2 配置 Electron 应用的视窗尺寸

和 NW.js 差不多，Electron 也支持配置视窗尺寸，不过方式不同。NW.js 可以让你在 package.json 文件中进行配置，而 Electron 则要求你在应用视窗初始化的时候设置尺寸。

在本书的 GitHub 仓库中，你可以在 chapter-07 文件夹下找到一个名为 windowsizing-electron 的应用代码。具体代码如下所示：

最后是奇迹发生的地方：main.js 文件，如代码清单 7.1 所示。

代码清单 7.1 Electron 中视窗尺寸应用的 main.js 文件的内容

现在，你可以通过终端应用或者命令提示符应用执行 electron．来运行应用，之后就能看到如图 7.3 所示的样子。

Electron 的这种方式意味着对每个视窗你都可以很好地控制其尺寸。要想了解更多创建 BrowserWindow 实例时支持的参数，可以访问 https://electron.atom.io/docs/api/browser-window/。

图 7.3 运行在 400 像素宽、200 像素高的视窗中的 Electron 应用。注意，应用看起来像运行在横屏模式下

以上介绍了在应用加载时如何调整视窗的尺寸。现在，我们来看一下如何对应用视窗进行更多的设置。

7.1.3 在 NW.js 中限制视窗的尺寸

如果你不想让用户随时调整桌面应用的宽高（这会让界面变乱，看起来怪怪的），可以使用表 7.1 所列出的选项。

下面展示了这些选项在 package.json 文件中的样子：

图 7.4 展示了上述配置生效后应用的样子。

在上面这个示例的 JSON 数据结构中，设置了视窗的宽度最大不能超过 1024 像素，最小不能小于 800 像素。还设置了视窗的高度最大不能超过 768 像素，最小不能小于 600 像素。能够限制视窗的宽度和高度（尽管用户想改变尺寸）可以让你更好地将界面的样子控制在预期范围内。

图 7.4 视窗尺寸受最大 / 最小宽度以及最大 / 最小高度影响

当应用启动的时你就知道要设置视窗的尺寸，那么上述方法很好。但是，如果你要设置的视窗宽度和高度都是动态的值呢？比如，应用要显示一张图片（这时视窗尺寸就要匹配图片的尺寸）。

好消息是这种情况下可以使用 NW.js 的视窗 API。假设你计算机中有一张 900×550 像素大小的图片，并且你想让视窗和这张图片大小一致，那么可以将视窗设置为 900 像素宽以及 550 像素高，如代码清单 7.2 所示。

能够通过编程的方式设置视窗尺寸就可以让视窗适应视窗内内容的尺寸，这会提高用户体验。

还可以通过使用同样的 API 来设置视窗在屏幕上显示的位置。NW.js 中的 GUI API 支持设置视窗在屏幕中的相对坐标位置。下面的代码清单 7.3 展示了在 NW.js 中使用编程的方式设置视窗显示位置的例子。

代码清单 7.3 设置视窗相对屏幕的位置

上述代码让你可以决定应用视窗要显示在屏幕中的哪个位置，这对工具类应用或者类似的应用非常有帮助。

现在我们来看一下在 Electron 中如何限制视窗尺寸。

7.1.4 在 Electron 中限制视窗的尺寸

在 Electron 中是通过设置 BrowserWindow 实例来实现对视窗尺寸进行限制的。你应该还记得本章前面介绍过，要创建应用视窗，要在代码中创建一个 BrowserWindow 的实例，如代码清单 7.4 所示。

代码清单 7.4 在 Electron 中创建一个 BrowserWindow 实例

mainWindow 是 Electron 中 BrowserWindow 类的一个实例，将视窗的宽度和高度传递给了这个对象。这里，你可以为应用视窗设置最大和最小宽度以及最大和最小高度。举一个例子，假设你要确保应用视窗的宽度不小于 300 像素，高度不小于 150 像素，也不能超过 600 像素宽以及 450 像素高，那么可以将这些配置项传递给 BrowserWindow 实例：

表 7.2 展示了改变视窗宽度和高度的配置项。

Electron 采取的这种方式很不错，因为它可以让你单独为每个视窗进行设置，而且可以在代码的同一处书写这些配置，不需要在不同地方进行设置，这比在 NW.js 中要更加简单。另外针对属性名，NW.js 使用的是蛇形命名（max_width），而 Electron 使用的是驼峰命名（maxWidth），更贴近 JavaScript 风格。

默认情况下，Electron 在屏幕居中的位置渲染应用视窗。如果你想让应用视窗在指定区域显示，那么可以在创建 BrowserWindow 实例的时候设置其 x 和 y 坐标，就像这样：

mainWindow = new BrowserWindow({

width: 400, height:800, x: 10, y: 10})；

视窗的初始显示位置设置在距离左侧 10 个像素、距离上部 10 个像素处的位置，也就是说，它支持你控制应用在屏幕中的显示位置。

介绍完设置视窗尺寸以及显示位置，接下来看一下如何设置应用以无边框模式以及全屏模式运行。

7.2 无边框应用以及全屏应用

我们在火车站看到的时刻表和通知的显示屏就是一个全屏运行的桌面应用。像 ATM 这种触屏设备运行的也是桌面应用，并且设计为防止用户退出该应用，这种俗称 kiosk 应用。电脑游戏也采取的是这种方式，因此构建全屏运行的应用是非常常见的需求。

Electron 和 NW.js 都支持开发者将应用设置为在全屏模式下运行（像视频播放器以及游戏），也可以设置为无边框模式运行（像媒体播放器以及其他一些工具），还支持 kiosk 应用（像信息展示类应用以及自动售货机应用）。下面我们来看看在 NW.js 中如何进行设置，然后作为比较，再看看在 Electron 中如何进行设置。

7.2.1 NW.js 中的全屏应用

视频游戏是最主要的一类启动就直接进入全屏模式运行的应用。新版本的 Mac OS 操作系统支持应用方便地进入全屏模式，NW.js 利用了这个特性，并支持两种配置形式：通过修改 package.json 中的配置项或通过 JavaScript API 来动态设置。下述代码展示了通过 package.json 来设置应用一启动就进入全屏模式的例子：

如果你把上述 JSON 代码保存到 NW.js 桌面应用的 package.json 文件中并启动该应用，会发现应用一启动就进入了全屏模式，没有标题栏，应用内容占满了整个屏幕。

或者如果你想阻止用户让应用进入全屏模式，可以将该值设置为 false。

此前提到过，你也可以通过 NW.js 的原生 UI API 以编程的形式将应用设置为全屏运行，如下所示：

const gui = require ('nw.gui');

const window = gui. Window. get

()；window.enterFullscreen()；

假设你有一个非常简单的 NW.js 应用（比如像 Hello World 这种），并且想让用户单击后进入全屏模式。那么该应用首页就大概会是清单 7.5 所示的样子。

代码清单 7.5 通过编程方式触发进入全屏模式的例子

将上述代码插入应用的 index.html 文件，然后从命令行运行 nw 命令，就能看到如图 7.5 所示的样子。

图 7.5 应用中有一个按钮，单击它应用就进入全屏模式

单击 Go full screen 按钮，可看到应用进入了全屏模式。怎么做到的呢？通过查看 HTML 代码，你会看到里面内嵌了 JavaScript 代码，调用了 NW.js 的 UI API，这部分代码获取当前视窗并告诉该视窗进入全屏模式。这部分代码被封装为一个名为 goFullScreen 的函数，当页面上的按钮元素被单击的时候就调用该函数。

这很不错，不过，如果应用进入了全屏模式，要怎样才能退出呢？NW.js 对这一点也是支持的。你可以修改现有的代码来调用 leaveFullscreen 这个 API 函数，不过你需要知道当前视窗的状态（是否已经在全屏模式了）。可以通过应用视窗上的 isFullscreen 函数来获取当前状态。

接下来修改此前的例子，当单击按钮后，应用进入全屏模式，并且按钮文字变为 Exit full screen，单击后退出全屏模式。将 index.html 文件内容替换为如下 HTML 内容：

这里将 goFullScreen 函数修改为 toggleFullScreen 函数，该函数发起了一个 API 调用来判断当前视窗是否在全屏模式下。这个 API 返回 true（表示在全屏模式下）或者 false。当用户单击按钮时会调用这个函数。当用户第一次单击按钮的时候，应用会进入全屏模式（因为应用初始状态下不在全屏模式下）。按钮文字也会被改为 Exit fullscreen，以此表示应用当前在全屏模式下。当用户再次单击按钮时，由于应用已经在全屏模式下了，因此会退出全屏模式，同时将按钮文字改为 Go full screen。这种行为可以让用户以简单易懂的方式进行全屏模式的切换。

修改完 HTML 代码并从命令行重启应用后，单击 Go full screen 按钮，应用会进入全屏模式，按钮此刻也显示为 Exit full screen，如图 7.6 所示。

图 7.6 全屏模式下的示例应用。注意按钮文字已经改变了，可以让用户退出全屏模式

对于视频播放应用，进行全屏模式切换是非常常见的需求。事实上，由于在支持 NW.js 应用全屏模仿视频方面有一个 bug（见 GitHub 代码仓库中的第 55 号缺陷），在我们（Axisto Media）的 British Medical Journay（BMJ）应用中用曲线救国的方式解决了这个问题，方法是当用户单击播放 / 暂停按钮时，我们访问视频元素的影子 DOM（Shadow DOM）来切换全屏模式。

在使用应用的时候，全屏模式可以让用户充分利用屏幕，也可以减少其背后其他视窗的干扰。

现在你已经知道了在 NW.js 中如何实现全屏模式，接下来我们看一下 Electron 是如何支持全屏应用的。

7.2.2 Electron 中的全屏应用

Electron 也支持设置应用为全屏模式。当创建一个新的 BrowserWindow 实例时，可以设置全屏模式的参数。要在启动的时候设置应用进入全屏模式，在创建 BrowserWindow 实例的时候，将下面的配置项作为参数传递进去就可以了：

mainWindow = new BrowserWindow({fullscreen: true});

这样应用启动时就会直接进入全屏模式。这对于播放视频和游戏的应用来说是一个不错的选择。

但是如果你不想给用户这个选项呢？怎样禁用这个选项呢？很简单：在创建 BrowserWindow 实例的时候，传递一个 fullscreenable 属性并将其值设为 false，如下面的代码所示：

mainWindow = new BrowserWindow({fullscreenable: false});

上述配置项的作用是用户将无法通过标题栏中的按钮让应用进入全屏模式。这对于像小工具类的应用，希望将界面保持在一个尺寸来说是非常有用的。

如果你想通过编程的方式来让应用进入全屏模式，需要在初始化的时候调用 mainWindow 实例上的一个方法。我会将此前用 NW.js 实现的示例应用用 Electron 再实现一次，这样你就可以对它们进行对比了，如代码清单 7.6 所示。

代码清单 7.6 Electron 版全屏示例应用中 main.js 文件的代码

如你所见，代码非常标准。接下来，创建一个 index.html 文件，显示一个按钮用来切换全屏模式，如代码清单 7.7 所示。

代码清单 7.7 Electron 版全屏示例应用中 index.html 文件的内容

在 NW.js 版本的代码中，应用中有一个按钮，用来在全屏模式和视窗模式之间进行切换。这里唯一的区别就是你加载了一个单独的 app.js 文件，该文件中包含了客户端代码来处理全屏模式的切换。最后，你为上述 Electron 示例应用添加了一个标准的 package.json 文件，app.js 文件的代码如代码清单 7.8 所示。

代码清单 7.8 Electron 版全屏示例应用中 app.js 文件的内容

这是展现 NW.js 和 Electron 处理全屏模式区别很好的例子。Electron 通过提供 remote API 来让前端代码可以和后端代码进行通信。它允许 renderer 进程（前端）发送数据给 main 进程（后端），从而实现获取 BrowserWindow 实例并和它进行交互。接着你可以调用 BrowserWindow 实例中的诸多函数来获取当前设置（比如是否运行在全屏模式中），由此来判断是否要让应用进入全屏模式或者视窗模式。

BrowserWindow 实例中还可以调用哪些函数

本书介绍了部分（并非全部）可以在 BrowserWindow 实例中调用的函数。在 Electron 中，BrowserWindow 类在初始化的时候接受很多配置项，比如在 Mac OS X 中可以设置不同的标题栏样式（像 Hyper、Kitematic 以及 WebTorrent 这样）。

要了解更多初始化 BrowserWindow 实例可以传递的配置项以及可以调用的函数，请查看 http://electron.atom.io/docs/api/browser-window/。

上述示例展示了如何在 Electron 中在全屏模式和视窗模式间进行切换。接下来，我们来看看在无边框应用中如何更多地改变应用界面样式。

7.2.3 无边框应用

尽管可以通过单击按钮就让应用进入全屏模式还算比较有趣，但这未必能满足你的应用需求。有些应用，包括媒体播放器、屏幕小部件以及其他工具类应用，运行的时候都是没有视窗边框的，而是展示了一个独特的界面样式。Mac OS X 系统中的音乐播放器 VOX 就是其中一个例子，如图 7.7 所示。注意，界面是完全定制的，没有 MacOS X 的系统样式（没有标题栏、没有交通灯按钮，只有一个简单的关闭按钮来关闭应用）。

X 的系统样式（没有标题栏、没有交通灯按钮，只有一个简单的关闭按钮来关闭应用）。

图 7.7 Mac OS X 系统中的 VOX 音乐播放器，正在播放歌曲。注意，界面上没有 Mac OS X 的系统样式，也没有标题栏

在 NW.js 中创建无边框应用

这类应用称为无边框应用，在 NW.js 中也可以创建此类应用。修改 package.json 文件的内容，在 window 配置部分设置一个 frame 属性，值为 false，示例代码如下所示：

可以进一步修改 package.json 文件来设置应用背景的透明度，这样你就可以使用圆边并创建出非常有意思的界面样式了。将 package.json 文件修改为如下内容：

如果将 index.html 文件修改为代码清单 7.9 所示的内容，你就有了和 VOX 应用差不多的界面样式了。

代码清单 7.9 创建带圆边的无边框应用

如果通过命令行启动上述示例应用，你会在桌面上看到如图 7.8 所示的应用样式。

如果通过命令行启动上述示例应用，你会在桌面上看到如图 7.8 所示的应用样式。

图 7.8 运行在桌面上的无边框应用。应用模拟了 VOX 的圆边样式，以此来展示如何为应用设置透明的背景

尽管这能够让你为桌面应用创建华丽的界面，但也要注意，这同样会带来一些麻烦。首先，在禁用视窗边框后，你需要自己提供按钮来关闭 / 最小化应用视窗（或者，也可以让用户通过操作系统的工具栏来关闭应用）。

还有很重要的一点要注意，无边框应用默认状态下是不能被拖动的。这是因为界面上没有可以被拖动的元素（比如标题栏）。也就是说，是没有办法可以让应用被拖动的。关键在于为屏幕的 HTML 元素设置一个名为 - webkit-app-region 的 CSS 属性。

要想将 HTML 元素设置为可拖动的（比如 body 标签），将下面的 CSS 应用上去就可以了：

-webkit-app-region: drag;

在此前的示例中，如果你将该 CSS 属性通过内嵌 CSS 样式表作用到 body 标签上再重启应用，就会发现应用已经可以在屏幕上被拖动了。我希望一切就这么简单，但是不幸的是并非如此。将该 CSS 属性作用到 body 标签后会导致应用区域内所有的 HTML 元素都可以拖动应用，包括 Frameless app example 这样的文字。试着选中文本 —— 你会发现并不能选中。所有 body 标签中的 DOM 元素都可以被拖动，这也许并不是你期望的。那么怎么解决这个问题呢？

答案取决于 HTML 元素自身的属性。如果 HTML 元素本身是可以单击的元素，像按钮或者下拉菜单，那么可以给这些 HTML 元素设置一个 - webkit-app-region 属性，值为 no-drag，就像下面这样：

button, select {

-webkit-app-re

gion: no-drag;}

它会让你单击按钮的时候不触发拖动行为。或者如果对于一些 HTML 元素你想让它们可以被选中，用于复制和粘贴（如 p 标签和 img 标签），那么可以通过结合 - webkit-user-select 和 - webkit-app-region 这两个属性，并将 - webkituser-select 的值设为 no-drag 来实现：

p, img {

-webki

t-user-select: all; -webki

t-app-region: no-drag;}

如果你想让 HTML 元素可以被选中或者可以被单击，那么要对所有这些元素都进行设置。工作量有点大，不过这同时也意味着你可以完全定制应用的界面，让你的应用能够出类拔萃。

最终版本的 index.html 文件如代码清单 7.10 所示。

代码清单 7.10 背景透明且无边框的应用的 index.html 文件

现在你可以将应用在界面上进行拖动了，也能看到圆角边框后面的内容了。以上展示了如何在 NW.js 中创建背景透明的应用。现在，我们来看看在 Electron 中如何实现同样的需求。

使用 Electron 创建无边框应用

本章前面部分提到过，Electron 是在初始化 BrowserWindow 实例的时候来配置应用视窗的。你可以在运行时初始化 BrowserWindow 实例的时候通过传递一个配置项来设置应用是无边框的或者透明的。如下代码就是一个在 Electron 中配置无边框应用的例子：

mainWindow = new BrowserWindow({ frame: false });

应用会以无边框模式运行，如图 7.9 所示。

如果你想自己尝试运行一下这个示例，可以查看位于 https://github.com/paulbjensen/cross-platform-desktop-applications 的 GitHub 仓库，在 chapter-07 文件夹中有一个 frameless-app-electron 的示例应用。

图 7.9 一个运行在无边框模式下的 Electron 应用。注意到应用内容和左上角靠得很近了吗？Mac OS X 中默认应用的边角是圆的

Electron 还支持通过传递 transparent 属性来设置透明的应用视窗，代码如下所示：

mainWindow = new BrowserWindow({ transparent: true });

图 7.10 展示了透明的 Electron 应用的样子。

图 7.10 Electron 中一个透明的应用。注意整个背景都是透明的，但是可以看到标题栏的按钮以及应用中的文字

只要不让用户体验变得更复杂，支持透明本身在 Electron 中是一个很好的功能。对于一些小型工具类应用，这会非常有用，不过也要看具体应用的需求和使用人群。

有些应用运行在一些环境下，这些环境下用户不被信任不能拥有完全访问计算机的权限，比如，具备触屏体验的公共终端系统。接下来的内容，我们会介绍如何实现 kiosk 应用。

7.2.4 kiosk 应用

当你有机会构建被大量用户使用的应用时要注意 —— 应用在公共区域使用，比如博物馆的信息展示区域，或者可能在银行，这就需要应用要在一种特定的模式下运行，在这种模式下用户不能退出应用也不能通过这台计算机输入任何信息（并非供用户娱乐的）。尽管这类应用是运行在 kiosk 模式下的（有的时候确实是运行在这种模式下），但是它们需要被限制对底层操作系统资源的访问权限。

kiosk 这种模式在 NW.js 和 Electron 中都属于锁定模式，在这种模式下要访问底层操作系统资源是很困难的 —— 事实上，在这种模式下要退出应用除非让开发者手动添加这个功能，否则，他们只能通过重启计算机来实现。

在 NW.js 中创建 kiosk 应用

要让应用进入 kiosk 模式，需要修改 package.json 文件，并设置 kiosk 属性为 true，如下面的例子所示：

你也可以拿一个示例应用来尝试一下，不过，在尝试之前，确保所有必要的修改都已经保存了。

这是因为你可能需要重启计算机才能再进行其他操作。在 kiosk 模式下，应用会自动进入全屏模式，但是没有标题栏。唯一可以退出应用的办法就是按住键盘上的 Alt+Tab 组合键或者 Ctrl+Alt+Del 组合键 —— 否则，你就在这个应用中出不去了。

假设你需要为某人构建一个 kiosk 应用，但是你也需要让用户能够退出程序（万一操作系统有 bug）。那么要怎么做呢？

答案就是实现键盘快捷键或者单击按钮后调用应用视窗上的 leaveKioskMode API 函数。和全屏 API 函数一样，kiosk 模式也有对应的 API 函数可以用于进入 / 退出 kiosk 模式，也可以用于检测当前应用视窗是否在 kiosk 模式下。

想象一下你有一个应用运行在 kiosk 模式下，并且你想给 IT 系统管理员提供一个访问计算机操作系统的方法，而不需要他重启计算机（特别是当计算机接着电源而且重启按钮被藏起来的时候）。你决定在应用视窗上增加一个退出按钮来帮助管理员返回到操作系统中。

确保 package.json 文件和如下所示内容一致：

并且确保 index.html 文件的内容如代码清单 7.11 所示。

代码清单 7.11 kiosk 应用的 index.html 文件，有一个明显的退出按钮

你会发现这和第一个全屏应用示例（单击按钮，退出全屏模式）所采用的方法一样。上述示例展示了如何让一个应用退出 kiosk 模式。如果你现在运行该应用，就能看到如图 7.11 所示的样子了。

图 7.11 运行在 kiosk 模式下的应用。应用占据了整个屏幕，整个操作系统被遮住了

单击 Exit 按钮，应用就会退出 kiosk 模式回到普通的视窗布局。

kiosk 模式下所有的键盘快捷键会被禁止吗

不，NW.js 仍然允许你通过全局的键盘快捷键（比如，Windows 系统的 Alt+F4 组合键）来退出应用。之所以允许是因为病毒检测软件会阻止应用视图覆盖全局的快捷键。

上述例子展示了如何通过 NW.js 来创建 kiosk 应用。对于 Electron 来说，创建 kiosk 模式下的应用非常简单。

使用 Electron 创建 kiosk 应用

Electron 支持在初始化 BrowserWindow 实例的时候通过传递一个名为 kiosk 的属性来设置应用进入 kiosk 模式。下面是一个例子：

通过上述配置后，应用会进入全屏模式。要退出应用，唯一的办法是通过快捷键（Mac OS X 上是 Command+Q,Windows/Linux 上是 Alt+F4）。

不过如果你想通过编程的方式进入 kiosk 模式并且可以通过一个按钮来切换的话，可以使用与此前全屏模式那个例子一样的办法来实现。

通过本书 GitHub 仓库中 chapter-07 文件夹中的 kiosk-app-programmatic-electron 文件夹中的源代码，你可以试着运行该应用。这个应用非常标准，唯一的不同是 index.html 和 app.js 文件。代码清单 7.12 所示的是 index.html 文件的内容。

代码清单 7.12 kiosk 模式下 Electron 应用的 index.html 文件

当单击 kiosk 按钮时，会调用一个名为 toggleKiosk 的函数。该函数定义在 app.js 文件中，如代码清单 7.13 所示。

代码清单 7.13 kiosk 模式下 Electron 应用的 app.js 文件

当运行上述应用时，第一次单击按钮的时候应用会进入 kiosk 模式，进入 kiosk 模式后也可以退出。这就让你可以创建按钮来很容易地关闭应用 —— 想象一下该应用运行在一台没有键盘的计算机中。

对于在公共场合被人使用，并且对底层操作系统资源的访问受限的应用来说，kiosk 模式是非常有用的。不过话说回来，正如此前提到的，依然还是有办法可以退出 kiosk 模式的，因此并不能完全保证让应用无法退出，不过至少可以保证绝大多数普通用户在公共场所的计算机中是无法退出应用的。

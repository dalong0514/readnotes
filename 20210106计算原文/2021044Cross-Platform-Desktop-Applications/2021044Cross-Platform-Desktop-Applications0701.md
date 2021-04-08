This chapter covers Controlling the application window Setting the application window's dimensions Making applications run in full-screen mode Creating kiosk applications

When you build a desktop app, one of the first considerations is how the user willinteract with it. Will it be a windowed app that can operate at the same time asother apps, a publicly accessible terminal in a bank, or an immersive experiencethat will consume all of the user's attention, like a game?

A desktop app can take many forms. It can operate in a window that can be max-imized and minimized as needed, or run in full-screen mode, like a video game. Inthis chapter, we'll explore options for controlling the way the app is displayed tothe user, and I'll show you some methods that will come in handy when you'rebuilding apps.

7.1 Window sizes and modes

User interfaces come in a range of different dimensions; traditional IM apps likeAIM or MSN Messenger (if you're old enough to remember them) tended to have

121

122

CHAPTER 7 Controlling how your desktop app is displayed

a long portrait window listing many contacts that users would want to chat with. Overtime, apps like Slack and Gitter have approached the world of IM with a different win-dow size, much in the style of a forum, and to accommodate longer messages andimages (there's a tendency in Slack communities to use a lot of animated GIFs). Win-dow sizes for apps need to provide the best possible UX, so it's important to be able tomake them fit the dimension required for the UI. Figure 7.1 shows an example.

Figure 7.1 Skype in action. Notice the tall style of the UI, accommodating mainly chat messages.

In NW.js and Electron, there are multiple ways to configure the window. We'll take alook at how you can configure an app window's width and height in NW.js.

7.1.1

Configuring window dimensions for an NW.js app

NW.js allows you to configure the window's width and height via the package.json file.In the GitHub repository for this book, the chapter-07 folder holds a copy of theexample NW.js app called window-resizing-nwjs. The code for it looks like this:

<html> <head> <title>Window sizing NW.js</title> </head>

Window sizes and modes

123

<body> <h1>Hello World</h1> </body></html>

This is a pretty basic HTML file, containing an h1 element inside the body tag with thewords Hello World, much like the Hello World examples shown earlier in this book. Ifyou want to add window dimensions to the app, you can adjust them to work by usingthis for the package.json file:

{ "name" : "window-sizing-nwjs", "version" : "1.0.0", "main" : "index.html", "window" : { "width" : 300, "height" : 200 }}

The window's width and height are specified in pix-els. This allows you to make sure that when the appopens, its width and height are set at those dimen-sions. This is one way you can control the window'swidth and height. Figure 7.2 shows an example ofwhat the changes look like.

This demonstrates how you can control the appwindow's initial width and height in NW.js. How doyou do the same with Electron?

Figure 7.2 An app with window properties applied. You can see here that the app is small.

7.1.2

Configuring window dimensions for an Electron appElectron's ability to configure window dimensions is similar to that of NW.js, but theapproach is different. Where NW.js allows you to specify the configuration in the pack-age.json manifest file, Electron requires that you configure window dimensions at thepoint in which the app window is initialized.

In the book's GitHub repository, you'll find an Electron app inside the chapter-07

folder called window-sizing-electron. Here's what the code for that app looks like:

{ "name" : "window-sizing-electron", "version" : "1.0.0", "main" : "main.js"}

And then there's the accompanying index.html file that you'll display:

<html> <head> <title>Window sizing Electron</title>

124

CHAPTER 7 Controlling how your desktop app is displayed

</head> <body> <h1>Hello from Electron</h1> </body></html>

Finally, the place where the magic happens: the main.js file, shown next.

Listing 7.1 The main.js for the Electron window sizing app

'use strict';

const electron = require('electron');const app = electron.app;const BrowserWindow = electron.BrowserWindow;

let mainWindow = null;

app.on('window-all-closed', () => { if (process.platform !== 'darwin') app.quit();});

app.on('ready', () => { mainWindow = new BrowserWindow({ width: 400, height: 200 });  mainWindow.loadURL(`file://${__dirname}/index.html`); mainWindow.on('closed', () => { mainWindow = null; });});

Where the width and height of the window are set

Now, you can run the app with electron . from the Terminal or Command Prompt,and you should see the app pop up looking like figure 7.3.

Figure 7.3 The Electron app running with a dimension of 400-pixel width and 200-pixel height. Notice that the app looks like it's running in an extreme landscape mode.

Electron's approach means you have fine-grained control over the dimensions of eachapp window. For more details on all the attributes you can pass into the creation of aBrowserWindow object instance, see http://electron.atom.io/docs/api/browser-window/. That covers adjusting the size of the app window at loading time. Now, we'll look

into how to get greater control over those window dimensions for the app.

7.1.3

Constraining dimensions of window width and height in NW.jsIf you want to prevent the users of your apps from changing the width and height ofyour desktop app (and causing the UI to look skewed and weird), you can pass theoptions listed in table 7.1.

Window sizes and modes

125

Table 7.1 Options to restrict window resizing

Property

Description

max_width

max_height

min_width

min_height

Sets the maximum width of the window

Sets the maximum height of the window

Sets the minimum width of the window

Sets the minimum height of the window

Here's how it would look in the package.json file:

"window": { "max_width": 1024, "min_width": 800, "max_height": 768, "min_height": 600}

Figure 7.4 shows what dimensions are affected in the app window.

Max/min height

Max/min width

Figure 7.4 The window dimensions affected by the max/min width and max/min height

In the example JSON payload, you constrain the width of the window so that it can'tbe greater than 1024 pixels or less than 800 pixels. You also constrain the height of thewindow to be no greater than 768 pixels and no less than 600 pixels. Being able toconstrain the window width and height (even when the user attempts to resize them)gives you greater control over making sure the look and feel of the app fits with theintended design.

126

CHAPTER 7 Controlling how your desktop app is displayed

This is good when you know what window dimensions you want to constrain towhen the app loads. But what if you want the app window's width and height to be setto dynamic values, such as an app displaying an image (where the window's width andheight match the dimensions of the image)?

The good news is that there's a way to do that with NW.js's window API. Say youhave an image on your computer with dimensions of 900 x 550 pixels, and you want tosize the window to match. You can set the width and height of the window to 900 pix-els wide and 550 pixels high with the code shown in the following listing.

Listing 7.2 Dynamically resizing the app window

const gui = require('nw.gui');         References GUI const win = gui.Window.get();    API in NW.js

win.width = 1024;  win.height = 768;

Sets width and height of window dynamically

Uses GUI API to select current app window

Being able to resize the window programmatically lets you make the app windowmatch the dimensions of the content inside it and therefore give a better experienceto the user.

You can also use the same API to control where the window is rendered on thescreen. The GUI API in NW.js allows you to position the window at a set of coordinatesrelative to the screen. The next listing shows an example of doing this programmati-cally with NW.js.

Listing 7.3 Positioning the window relative to the screen

const gui = require('nw.gui');const win = gui.Window.get();win.x = 400;        win.y = 500;

Sets horizontal coordinate of app window

Sets vertical coordinate of app window

This code affords you the ability to determine exactly where on the screen the app win-dow will be positioned, which is good in the case of utility applications and the like.

We'll now take a look at how Electron handles constraining app windows.

7.1.4

Constraining dimensions of window width and height in Electron

The settings for constraining the dimensions of app windows in Electron are definedon the BrowserWindow instance. You'll remember from earlier in the chapter that tocreate an app window, you have to initialize an instance of the BrowserWindow class inthe code.

Window sizes and modes

127

Listing 7.4 Initializing a BrowserWindow instance in Electron

'use strict';

const electron = require('electron');const app = electron.app;const BrowserWindow = electron.BrowserWindow;

let mainWindow = null;

app.on('window-all-closed', () => { if (process.platform !== 'darwin') app.quit();});

Passes options toBrowserWindowinstance

app.on('ready', () => { mainWindow = new BrowserWindow({ width: 400, height: 200 }); mainWindow.loadURL(`file://${__dirname}/index.html`); mainWindow.on('closed', () => { mainWindow = null; });});

The mainWindow variable is an instance of the BrowserWindow class of Electron and ispassed an object containing the width and height for the window. Here, you can setthe maximum and minimum width and height properties for the app window. Say, forexample, you want to make sure that the app cannot be resized below 300 px wide and150 px high, and cannot be resized beyond 600 px wide and 450 px high—you canpass these options into the BrowserWindow instance:

mainWindow = new BrowserWindow({ width: 400, height: 200, minWidth: 300, minHeight: 150, maxWidth: 600, maxHeight: 450});

Table 7.2 shows the properties to change for the window width and height.

Table 7.2 Properties for changing window width and height

Property

Description

maxWidth

maxHeight

minWidth

minHeight

Sets the maximum width of the window

Sets the maximum height of the window

Sets the minimum width of the window

Sets the minimum height of the window

The approach taken by Electron is nice because it lets you define individual settingsfor each app window that your app creates, and you can configure all of those settingsin one place in the code, rather than look for them in separate places in the code. It'ssimpler than in NW.js, and where NW.js uses snake case (as in max_width) propertynames, Electron uses camel case (as in maxWidth) property names, JavaScript-style.

128

CHAPTER 7 Controlling how your desktop app is displayed

By default, Electron renders the app in the middle of the screen. If you want toposition the app window in a specific area of the screen, you can control this by pass-ing x and y coordinates to the initialization of the BrowserWindow, like this:

mainWindow = new BrowserWindow({ width: 400, height: 800, x: 10, y: 10});

7.2

The position of the window is set to begin at 10 pixels from the left (x) and 10 pixelsfrom the top (y), and so it offers you the ability to control where you position the appwindow on the screen.

Having explored window sizing and positioning, we'll now look at how to config-

ure the app to run as a frameless application, or even in full-screen mode.

Frameless windows and full-screen appsWhen you visit a train station and look at the display of train times and announce-ments, chances are the display is powered by a desktop app running in full-screenmode. Touch-screen monitors such as ATM machines also run desktop apps that aredesigned to prevent users from exiting the app, known as kiosk apps. Computer gamesalso exhibit the same behavior, so the need for building apps that hide the underlyingOS is a common one.

Electron and NW.js allow developers to tailor their apps so that they run in full-screen mode (for video playback and games), as well as frameless (for media playersand other utilities) and kiosk (for information kiosks and point-of-sale applications).We'll take a look at how NW.js enables this and then look at Electron's approach forcomparison.

7.2.1

Full-screen applications in NW.jsVideo games are a prime example of apps that run in full-screen mode when they firstboot up. Recent versions of Mac OS have enabled apps to operate easily in full-screenmode, and NW.js takes advantage of this feature in two ways: via configuration optionsin the package.json manifest file, or dynamically via the JavaScript API. The followingcode is an example of enabling your desktop app to run in full-screen mode when itlaunches via the package.json file:

{ "window": { "fullscreen": true }}

If you put the following JSON into the package.json file of an NW.js desktop app andthen run the app, you can expect to see the app go straight into full-screen modeupon launch, where the title bar is not visible and the contents of the app take up theentire screen.

Frameless windows and full-screen apps

129

Alternatively, if you want to prevent users from being able to make an app enter

full-screen mode, you can set the value to false.

As mentioned earlier, it's possible to make the app go full-screen programmatically

via NW.js's native UI API, as follows:

const gui = require('nw.gui');const window = gui.Window.get();window.enterFullscreen();

Say you have a dead-simple NW.js app (such as a Hello World example), and you wanta screen click to trigger full-screen mode. The app has some simple HTML for thehome page, as shown next.

Listing 7.5 Example of programmatically triggering full-screen mode

<html> <head>  <title>Full-screen app programmatic NW.js</title>  <script>  'use strict';

const gui = require('nw.gui');   const win = gui.Window.get();

Loads NW's UI library

Gets ahold of the app window

function goFullScreen () {   win.enterFullscreen();  }  </script> </head> <body> <h1>Full-screen app example</h1> <button onclick="goFullScreen();">Go full screen</button> </body></html>

Creates function that will put app in full-screen mode

Clicking button calls goFullScreen function,putting app window in full-screen mode

Insert that into the main index.html file for the app and run the app from the com-mand line with nw. You should see a screen like figure 7.5.

Figure 7.5 App with a button that turns on full-screen mode when clicked

Click the Go Full Screen button and you should see the app go to full-screen. So howdid that happen? Going through the HTML, you can see some embedded JavaScriptthat called out to NW.js's GUI API, fetched the current window, and told it to enter

130

CHAPTER 7 Controlling how your desktop app is displayed

full-screen mode. You wrapped the call to enter full-screen mode in a function calledgoFullScreen, which the button element in the page triggered when clicked.

This is all good, but what if you're already in full-screen mode and want to leavethat mode? NW.js accommodates this as well. You can modify the existing code so thatit can call the API function leaveFullscreen, but the trick here is to track what thecurrent state of the window is (whether it's already in full-screen mode). You can findout what the mode of the app window is with an API call called isFullscreen.

You'll modify the previous example so that when the button is clicked and the appwindow enters full-screen mode, the button will change its text to「Exit Full Screen」and leave full-screen mode. Replace the HTML in the index.html file with this code:

<html> <head> <title>Full-screen app example</title> <script>  'use strict';  const gui = require('nw.gui');  const win = gui.Window.get();

function toggleFullScreen () {  const button = document.getElementById('fullscreen');  if (win.isFullscreen) {   win.leaveFullscreen();   button.innerText = 'Go full screen';  } else {   win.enterFullscreen();   button.innerText = 'Exit full screen';  }  }

</script> </head> <body> <h1>Full-screen app example</h1> <button id="fullscreen" onclick="toggleFullScreen();">Go full

screen</button>

</body></html>

This replaces the goFullScreen function with a toggleFullScreen function thatmakes an API call to determine whether the app window is in full-screen mode. TheAPI call returns either true (it is in full-screen mode) or false. The function is calledwhen the user clicks the button. When the user first clicks it, the function will enterinto full-screen mode (because the app isn't initially in full-screen mode). It will alsochange the text on the button to read「Exit Full Screen」to reflect the fact that the appis in full-screen mode. When the user clicks the button a second time, because theapp window is in full-screen mode, you'll leave that mode, and alter the text of thebutton to read「Go Full Screen.」This behavior allows the user to toggle full-screenmode in a simple and easy-to-understand fashion.

Frameless windows and full-screen apps

131

After you've changed the HTML and reloaded the app from the command line,click the Go Full Screen button. Not only should the app window enter full-screenmode, the button should now display「Exit Full Screen,」as shown in figure 7.6.

Figure 7.6 Example app in full-screen mode. Notice that the button text has changed to allow the user to exit full-screen mode.

Being able to enter and exit full-screen mode in desktop apps can be handy, particu-larly when it comes to video playback. In fact, due to a bug that existed with supportingfull-screen playback of videos in NW.js apps (see issue #55 on the GitHub repository),we (at Axisto Media) managed to work around the issue for our British Medical Jour-nal (BMJ) app by accessing the shadow DOM of the video element and toggling thefull-screen mode when the user clicked the Play/Pause button.

Full-screen mode enables users to take full advantage of the screen when using theapp and display it in such a way as to eliminate the distractions of other windows in thebackground.

Now that you've seen how this is done in NW.js, we'll take a look at how Electron

handles supporting full-screen applications.

7.2.2

Full-screen applications in Electron

Electron also offers configuration for full-screen mode. When creating a new Browser-Window instance, you can set options to configure for full-screen mode. To make anElectron app run in full-screen mode when it's started, pass the following configura-tion option when creating the BrowserWindow instance:

mainWindow = new BrowserWindow({fullscreen: true});

When the app runs, it will go straight into full-screen mode. This is a good option foran app that plays videos or games.

But what if you don't want people to have this option? How do you disable it? Sim-ple: you pass the fullscreenable property with a value of false when initializing theBrowserWindow instance, as demonstrated in the following code:

mainWindow = new BrowserWindow({fullscreenable: false});

This configuration option means that the user will not be able to make the app enterfull-screen mode from the title bar. This can be useful in cases where you want to main-tain the dimensions of an app's user interface, such as with a small utility application.

132

CHAPTER 7 Controlling how your desktop app is displayed

If you want to be able to trigger this functionality programmatically, you'll need tocall a function on the mainWindow instance after it's initialized. I'll re-create the exam-ple that I made for NW.js, using Electron instead, so you can compare the two.

Listing 7.6 Code for the main.js file for the full-screen Electron example

'use strict';

const electron = require('electron');const app = electron.app;const BrowserWindow = electron.BrowserWindow;

let mainWindow = null;

app.on('window-all-closed', () => { if (process.platform !== 'darwin') app.quit();});

app.on('ready', () => { mainWindow = new BrowserWindow(); mainWindow.loadURL(`file://${__dirname}/index.html`); mainWindow.on('closed', () => { mainWindow = null; });});

Here, you see that the app code is pretty much standard. Next, you'll create theindex.html file that has the button for toggling between full-screen mode and win-dow mode.

Listing 7.7 The index.html file for the full-screen Electron example

<html> <head> <title>Fullscreen app programmatic Electron</title> </head> <script src="app.js"></script>      <body> <h1>Hello from Electron</h1> <button id="fullscreen" onclick="toggleFullScreen();">  Go full screen </button> </body></html>

Loads client-side code as separate JavaScript file

Calls function in the app.js file called toggleFullScreen to do the toggling

As in the NW.js variant of the code, the app has a button that is used to trigger tog-gling between full-screen mode and window mode. The only difference here is thatyou load a separate app.js file that has the client-side code for toggling. Finally, youadd a standard package.json file as from the previous Electron example, and then thecode for the app.js file shown next.

Frameless windows and full-screen apps

133

Listing 7.8 The app.js file for the full-screen Electron example

Uses remote API to get current window page is being rendered in

Uses remote API to interact with main process from renderer process

const remote = require('electron').remote;

function toggleFullScreen() { const button = document.getElementById('fullscreen'); const win = remote.getCurrentWindow();   if (win.isFullScreen()) {       win.setFullScreen(false);      button.innerText = 'Go full screen'; } else { win.setFullScreen(true);    button.innerText = 'Exit full screen'; }}

Calls BrowserWindow instance's isFullScreen function to check if window is in full-screen mode

If so, switches to window mode by calling the instance's setFullScreen function with false

If not, switches to full-screen mode

This is a good example of the difference in approaches between NW.js and Electron.Electron handles how the front-end calls to the back-end of the app by providing anAPI called remote. This allows the renderer process (front end) to send messages tothe main process (back end), so that you can do things like get ahold of the Browser-Window instance and interact with it. You can then call various functions on theBrowserWindow instance to inspect its current settings (such as whether it's running infull-screen mode) and use that to determine whether to make it render in full-screenmode or windowed mode.

What other functions can I call on the BrowserWindow instance?This book touches on some (but not all) of the functions that can be called on theBrowserWindow instance. There's a wide range of configuration options for theBrowserWindow class in Electron, like being able to make the title bar styling differ-ent in Mac OS X (such as what Hyper, Kitematic, and WebTorrent use).

For more about these configuration options and functions that can be called on initial-ized BrowserWindow instances, check out http://electron.atom.io/docs/api/browser-window/.

This demonstrates how to toggle between full-screen mode and window mode in Elec-tron. Next, we'll look at how to make more-radical changes to your app UI, in theform of frameless apps.

7.2.3

Frameless appsAlthough being able to make your apps go full-screen at the click of a button is fun,it may not be suited for your app's purposes. Some apps, including media players,

134

CHAPTER 7 Controlling how your desktop app is displayed

onscreen widgets, and other utility apps, run without displaying any of the app win-dow around them, and instead display a unique UI. An example of this is the musicplayer VOX on Mac OS X, shown in figure 7.7. Notice that the UI is custom, and thereis no Mac OS X UI visible (no title bar, no traffic-light buttons, only a simple X to closethe window).

Figure 7.7 VOX music player in Mac OS X, playing a song. Notice the distinct lack of Mac OS X's UI elements and title bar.

CREATING FRAMELESS APPS IN NW.JSThese apps are known as frameless apps, and you can create them in NW.js as well. Alterthe package.json manifest file so that the window section contains a property calledframe, with the value set to false, as in this code sample:

{"name" : "frameless-transparent-app-nwjs","version" : "1.0.0","main" : "index.html","window" : { "frame" : false}}

You can modify the package.json further to allow for transparency behind the app'sscreen, so that you can use rounded corners and create interesting interfaces. Chang-ing the package.json to use this:

"window" : { "frame" : false, "transparent": true, "width": 300, "height": 150}

You now have the basis for creating an app that's similar in style to the interface stylepresented in the VOX app if you adjust the index.html file to look like the next listing.

Listing 7.9 Creating a frameless app with styled rounded corners

<html> <head> <title>Transparent NW.js app - you won't see this title</title>

Frameless windows and full-screen apps

135

<style rel="stylesheet">  html {  border-radius: 25px;  }

body{  background: #333;       color: white;  font-family: 'Signika';  }

p {  padding: 1em;  text-align: center;  text-shadow: 1px 1px 1px rgba(0,0,0,0.25);  }

</style> </head> <body> <p>Frameless app example</p> </body></html>

If you run the example via the command line, you'll see the app on your desktop, asshown in figure 7.8.

Figure 7.8 A frameless app running on the desktop. The app style mimics an exaggerated version of the rounded-corner UI on VOX, to demonstrate how the app can have a transparent background.

Although this offers the chance to create some snazzy custom UIs for your desktop apps,bear in mind some caveats to using this approach. The first is that after disabling thewindow frame, you need to provide buttons for closing/minimizing the app window(alternatively, you can allow the user to close the app from the main toolbar of the OS). It's important to note that frameless apps aren't draggable by default. This isbecause they have no UI element set (such as the title bar) that allows them to bedragged. That said, there's a way to enable them to be dragged. The key is to use a cus-tom CSS property on the HTML for the screen, known as –webkit-app-region.

For HTML elements that you want to make draggable (such as the body tag for

example), apply the following CSS:

-webkit-app-region: drag;

136

CHAPTER 7 Controlling how your desktop app is displayed

If you append this CSS property to the body tag in the embedded CSS stylesheet fromthe previous example and reload the app, you'll see that it can now be draggedacross the screen. I'd like to be able to say that's all there is to it, but unfortunatelythat's not the case. Applying this CSS property to the body tag makes all HTML ele-ments within the app an area that will drag the app, including the text that says「Fra-meless app example.」Try selecting the text—you cannot. The entire contents of theDOM under the body tag are also draggable, which might not be the behavior thatyou want for that part of the app. How do you resolve this?

The answer depends on what the nature of the HTML element needs to do. If theHTML element in question is a clickable element, like a button or a drop-down field,then you'll want to give those HTML elements the -webkit-app-region property witha value of no-drag, like this:

button, select { -webkit-app-region: no-drag;}

This will enable you to be able to click buttons without the draggable behavior kickingin. Alternatively, if the HTML elements in question are elements that you want to beable to select snippets of for copying and pasting into other documents and apps(such as p tags and img tags), then you can make them selectable by the -webkit-user-select property alongside the –webkit-app-region CSS property with a valueof no-drag:

p, img { -webkit-user-select: all; -webkit-app-region: no-drag;}

You'll need to do this on all the HTML elements that you want to be selectable, as wellas all UI elements that need to be clickable. It can be a bit of a pig, but it ultimatelymeans that you can have a completely custom look to your UI and make your appstand out from the rest.

The final version of the index.html file should look like the following.

Listing 7.10 The index.html file for the transparent frameless app

<html> <head> <title>Transparent NW.js app - you won't see this title</title> <style rel="stylesheet">  html {  border-radius: 25px;  -webkit-app-region: drag;  }

body {  background: #333;

Frameless windows and full-screen apps

137

color: white;  font-family: 'Signika';  }

p {  padding: 1em;  text-align: center;  text-shadow: 1px 1px 1px rgba(0,0,0,0.25);  }

button, select {   -webkit-app-region: no-drag;  }

p, img {   -webkit-user-select: all;   -webkit-app-region: no-drag;  }

</style> </head> <body> <p>Frameless app example</p> </body></html>

Now you can drag the app around the screen and see the background behind therounded corners. That gives you an idea of how you can approach creating transpar-ent apps in NW.js. Now we'll look at how the same can be done with Electron.CREATING FRAMELESS APPS WITH ELECTRONAs demonstrated earlier in the chapter, Electron handles configuring app windows viathe initialization of the BrowserWindow instance. You can make the app frameless ortransparent by passing a property to the initialization of the BrowserWindow at runtime.The following code is an example of how to configure a frameless app in Electron:

mainWindow = new BrowserWindow({ frame: false });

The app will now run in frameless mode, and you'll see something like figure 7.9.

Figure 7.9 An Electron app running in frameless mode. Notice how the content of the app is positioned so closely to the top and left of the app? The app's corners are rounded by default as part of Mac OS X.

If you want to try this example for yourself, you can give it a spin in the chapter-07folder of the GitHub repository at https://github.com/paulbjensen/cross-platform-desktop-applications, under the app example frameless-app-electron.

138

CHAPTER 7 Controlling how your desktop app is displayed

Electron also allows you to make app windows transparent by passing the trans-

parent property in the following example:

mainWindow = new BrowserWindow({ transparent: true });

Figure 7.10 shows what a transparent Electron app looks like.

Figure 7.10 A transparent app in Electron. Notice how the background is completely transparent, but you can see the title bar buttons as well as the app's text.

7.2.4

Transparency in Electron is a great feature as long as it doesn't complicate the UX.For small utility applications, this can be a useful attribute, but that depends on whatthe app is doing and whom it is for.

Some apps can run in environments where the user isn't necessarily trusted withcomplete access to the computer, such as in public terminals with touchscreen inter-faces. In the next section, we'll look at implementing kiosk applications.

Kiosk mode applicationsSometimes you get the chance to build an app that will be used by lots of people, butwith a catch—the app is public, such as the information area of a museum, or maybe abank, and needs to be able to run in a mode where the user can't quit the app andstart messing around with the computer (not a prospect anyone wants to entertain).Apps like these need to restrict access to the underlying OS, as though they're run-ning at kiosks (which, in some cases, they are).

Kiosk mode in both NW.js and Electron is a locked-down mode where access to theunderlying OS is difficult—in fact, being able to quit the app has to be manuallyadded by the developer (otherwise, they have to physically reboot the computer toregain access to it).CREATING KIOSK-MODE APPS IN NW.JSTo enable your app to run in kiosk mode, you'll need to modify your package.jsonmanifest file so that it has a property of kiosk with the value set to true, as in the fol-lowing example:

{ "window": { "kiosk":true }}

You can go ahead and give this a try in one of the example apps, but (and it is a big but)make sure that nothing is left unsaved before you do.

Frameless windows and full-screen apps

139

This is because you might have to reboot your computer in order to regain accessto it. In kiosk mode, the app automatically enters full-screen mode, but without thetitle bar. The only way you can exit the app is by pressing Alt-Tab or Ctrl-Alt-Del onthe keyboard—otherwise, you're stuck inside the app with no way out of it.

Say you need to build a kiosk app for someone, but you also need to be able to exit

the program (in case there's an issue with the OS). How do you do that?

The answer is to implement some kind of keyboard shortcut or button that whenclicked or typed calls an API function on the app window called leaveKioskMode.Like the full-screen API functions, kiosk mode has equivalent API functions forentering/leaving kiosk mode, as well as for detecting whether the app window is inkiosk mode.

Imagine that you have an app that will run at a display kiosk and you want to pro-vide a way for the IT systems administrator to get access to the computer's OS withouthaving to resort to rebooting the computer (in particular, if access to the computer'spower supply and reboot button is physically obscured). You decide to add a buttoncalled exit to the app window to help the administrator get back to the OS.

Make sure that the package.json file looks like this:

{ "name"  : "kiosk-mode-example-app", "version" : 1.0, "main"  : "index.html", "window" : { "kiosk" : true }}

And the index.html file should look like the following.

Listing 7.11 Kiosk app's index.html file, with an essential toggle button

<html> <head> <title>Kiosk mode NW.js app example</title> <script>  'use strict';

const gui = require('nw.gui');  const win = gui.Window.get();

function exit () {      win.leaveKioskMode();  }

Creates function to tell app window to get out of kiosk mode

</script> </head> <body> <h1>Kiosk mode app</h1> <button onclick="exit();">Exit</button>  </body></html>

Clicking button calls function to get out of kiosk mode

140

CHAPTER 7 Controlling how your desktop app is displayed

You'll notice you use the same pattern you used for the first full-screen mode appexample (click a button, exit mode). This is so you can easily demonstrate the func-tionality of being able to leave kiosk mode from the app. If you now run the app, youshould expect to see something like figure 7.11.

Figure 7.11 An app running in kiosk mode. The app runs across the entire screen, and access to the OS is obscured.

Click the Exit button, and the app will leave kiosk mode and switch back to a normalwindow layout.

ARE ALL KEYBOARD SHORTCUTS BLOCKED BY KIOSK MODE? No, NW.js still allowsusers to quit apps using the global keyboard shortcuts (for example, Alt-F4 onWindows). The reason it allows this is because virus detection software willblock apps that attempt to override access to these global keyboard shortcuts.

This shows how you can create kiosk apps with NW.js. For Electron, the process forcreating kiosk mode apps is dead simple.CREATING KIOSK APPS WITH ELECTRONElectron is able to make apps run in kiosk mode by passing one attribute to the initializa-tion of the BrowserWindow instance called (can you guess?) kiosk. Here's an example:

mainWindow = new BrowserWindow({ kiosk: true });

With the browser window configured this way, the app is able to run in full-screenmode, and the only way to quite the app is via the keyboard shortcut (Command-Q onMac OS X, Alt-F4 on Windows/Linux).

But if you want to provide some form of programmatic access to kiosk mode andbe able to toggle it via a button, you can do that in precisely the same fashion as youwould with toggling the full-screen app example.

You can try the app from the source code in the kiosk-app-programmatic-electronfolder in the chapter-07 folder of the book's GitHub repository. The app is a prettystandard setup, but with distinct differences in the index.html and app.js files. The fol-lowing listing shows what the index.html file looks like.

Listing 7.12 The index.html file for the programmatic kiosk mode Electron app

<html> <head> <title>Programmatic Kiosk app Electron</title> </head>

Summary

141

<script src="app.js"></script> <body> <h1>Hello from Electron</h1> <button id="kiosk" onclick="toggleKiosk();">Enter kiosk</button>  </body></html>

Clicking button triggersentering or exiting kiosk mode

When the kiosk button is clicked, you expect it to call a function called toggleKiosk.This is a function that is defined in the app.js file, shown next.

Listing 7.13 The app.js file for the programmatic kiosk mode Electron app

const remote = require('electron').remote;

function toggleKiosk() {         const button = document.getElementById('kiosk'); const win = remote.getCurrentWindow(); if (win.isKiosk()) {       win.setKiosk(false);      button.innerText = 'Enter kiosk mode'; } else { win.setKiosk(true);       button.innerText = 'Exit kiosk mode'; }}

Defines toggleKiosk function that's called when button is clicked

Detects if app is running in kiosk mode

If so, triggers exiting kiosk mode and updating button text

If not, triggers entering kiosk mode and updating button text

7.3

When running, the app is able to enter kiosk mode when the button is first clicked,and then is able to exit it when it has been put into kiosk mode. This allows you to cre-ate buttons for easily closing the app—say, if it's running at a computer that doesn'thave keyboard access.

Kiosk mode is useful for apps that are used by members of the public, and whereaccess to the underlying OS needs to be obscured. That said, as mentioned earlier,there are still ways to be able to escape from kiosk mode, so it's not a complete guaran-tee of protection from those who know their way around, but at least it will keep themajority from messing around with computers in public areas.

SummaryIn this chapter, we've looked at different ways in which you can craft your app's dis-play, depending on what the app needs to do for the user. Some quick takeaways: You can create windowed apps with specific width and height dimensions. You can restrict those dimensions so that the app's display stays fixed. It's easy to run your app in full-screen mode for videos and gaming. Alternatively, you can remove the app window and run it as a frameless app. Be careful with frameless apps because they come with some UI quirks you'll

need to handle around dragging, click events, and text selection.

 Kiosk-mode apps are useful for ATMs and apps running in public areas.

142

CHAPTER 7 Controlling how your desktop app is displayed

The first thing to think about with crafting your app is whether the app needs to oper-ate within a fixed or dynamic window, or even if it needs a window at all. Then, youcan configure the window options in the package.json manifest file to make the appwindow constrained to specific dimensions, or expand to take up the full screen. Also,remember that depending on whether your app is window-based or even a kiosk-mode app, the ability to navigate is important, so make sure you can exit a kiosk appfrom somewhere within the app's UI.

In chapter 8, we'll look at implementing tray applications with NW.js and Electron.

Creating tray applications

This chapter covers Building tray-based applications Displaying application windows from the tray

menu


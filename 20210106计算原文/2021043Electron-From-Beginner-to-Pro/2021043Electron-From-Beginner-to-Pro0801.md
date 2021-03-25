WebContents, Screens, and Locales

The development team at GitHub has added many good features to Electron. There are a few features that we would like to make you aware of and experiment with in this chapter.

First, we'll take a look at a property of the BrowserWindow called webContents, which has many events

and methods but we'll be focusing on a few items with which we think you should become familiar: capturing events, managing windows, and capturing a window as an image or pdf file. After that, we'll take a look at the screens module and learn how to detect the screens attached to your user's system. Finally, we'll review how to detect the system's locale so you can display the correct language in your application for your users.

Let's get started by setting up the Electron Quick Start project so we have a clean place to start.

Getting Started

As with each of these examples, we are using the Electron Quick Start example. We will use git clone to create a new copy of the quick start in a new folder, in this case named webcontents-screens-locale-example. First, open terminal and navigate to the folder where you would like to place your code.

git clone https://github.com/electron/electron-quick-start webcontents-screens-locale-example

Next, change your active directory to electron-quick-start.

cd webcontents-screen-locals-example

Now, we need to install the dependencies:

npm install

Finally, reset Git with

git init

Now that you have our example project installed, type npm start into your terminal application just to

make sure the application loads and runs as expected.

© Chris Griffith, Leif Wells 2017 C. Griffith, L. Wells, Electron: From Beginner to Pro, https://doi.org/10.1007/978-1-4842-2826-5_8

129

Chapter 8 ■ WebContents, sCreens, and LoCaLes

Let's take a moment to modify this package.json file to match our own by updating some nodes.

1. Change the name node to「webcontents-screens-locale-example.」

2. Change the version number to「0.0.1」since we are just starting out.

3.

In the description let's use something like「A sample Electron application to demonstrate online detection.」

4. Remove the repository node. If you decide to put your results in a repository you

can change or re-add this node with the correct address.

5. Keywords can be「Electron,」「webcontents,」,「screens,」「locale,」「example.」

6.

「author」: Your name goes here.

7. Let's change the「license」node to「MIT.」

Now that we have our webcontents-screens-locale-example project created and have made certain that

it runs, let's start making some changes to the code.

Discovering Electron's WebContents

If you wanted to build a Web browser with GitHub Electron, you would use the Electron's webContents event emitter. A lot. Mind you, we don't suggest you build a browser with Electron. People have done it, but it sounds like a lot of work. Nevertheless, many of the events and methods inside the webContents object deal with things your application probably won't need except for a few items we'd like to draw to your attention.

The web contents can be accessed directly in the Main Process or as part of a BrowserWindow's instance. How you access the events and methods of webContents will depend upon what you are trying to accomplish. In this chapter, we will try to give you some guidance on how to access these events and methods.

The first thing we should do is take a look at what webContents look like when printed to the console. Open the main.js file in your favorite code editor and start by adding the line for the webContents constant along with the console log statement as it appears below at the top of your code:

const electron = require('electron')// Module to control application life.const app = electron.app// Module to create native browser window.const BrowserWindow = electron.BrowserWindowconst webContents = electron.webContents

const path = require('path')const url = require('url')

console.log('webContents', webContents.getAllWebContents())

All we are doing here is creating a constant that gives us access to Electron's webContents object and then logging the contents of webContents object to the console using webContent's getAllWebContents() method. Save the file, and in your terminal application run the npm start command and take a look at the output (Figure 8-1).

130

Chapter 8 ■ WebContents, sCreens, and LoCaLes

Figure 8-1. Message in the console reveals webContents at startup is an empty array

Well, that wasn't in any way exciting. The only output we are seeing is webContents []. Of course,

we have done this on purpose so that we can show you that this early in the application startup process, webContents is an empty array. In other words, we won't see anything inside this array until we add a BrowserWindow object to the screen. Let's do that now.

At the bottom of the createWindow function, add the console log seen at here at the bottom of the

createWindow method to your code.

function createWindow () { // Create the browser window. mainWindow = new BrowserWindow({width: 800, height: 600})

// and load the index.html of the app. mainWindow.loadURL(url.format({ pathname: path.join(__dirname, 'index.html'), protocol: 'file:', slashes: true }))

// Open the DevTools. // mainWindow.webContents.openDevTools()

// Emitted when the window is closed. mainWindow.on('closed', function () {

131

Chapter 8 ■ WebContents, sCreens, and LoCaLes

// Dereference the window object, usually you would store windows // in an array if your app supports multi windows, this is the time // when you should delete the corresponding element. mainWindow = null })

console.log('webContents', webContents.getAllWebContents());}

Quit the sample Electron application, save your file, and run the npm start command in the terminal

again so we can look at what appears inside webContents after we have created a window in our application (Figure 8-2).

Figure 8-2. New console log shows the webContents array after a window is created

132

That is more like it, right? That is a lot of data! We'll print it out here so we can review what is there.

Chapter 8 ■ WebContents, sCreens, and LoCaLes

webContents []webContents [ WebContents { webContents: [Circular], history: [], currentIndex: -1, pendingIndex: -1, inPageIndex: -1, _events:  { 'navigation-entry-commited': [Function],  'ipc-message': [Function],  'ipc-message-sync': [Function],  'pepper-context-menu': [Function],  'devtools-reload-page': [Function],  'will-navigate': [Function],  'did-navigate': [Function],  destroyed: [Object],  'devtools-opened': [Function],  '-new-window': [Function],  '-web-contents-created': [Function],  '-add-new-contents': [Function],  move: [Function],  activate: [Function],  'page-title-updated': [Function] }, _eventsCount: 15, _maxListeners: 0, browserWindowOptions: { width: 800, height: 600 } } ]

Of course, the first line is our first console log call that returns an empty array. The second line is where

things get interesting. Inside the array is a WebContents object that is represented here in a naked kind of way. You can see that there is a history array that would hold objects representing the pages loaded by this window. The currentIndex, pendingIndex and inPageIndex are how the WebContents tracks the history. The next set of lines is an object that contains references to internal events that WebContents uses. Finally, at the bottom is the browserWindowOptions object that shows the options that were specified when our window was created. Let's test this out.

Inside our createWindow method, update the code with the following line in bold.

function createWindow () { // Create the browser window. mainWindow = new BrowserWindow({width: 800, height: 600, title: 'hello world'})

Now we can run the npm start command and see the title of our window in the console log output

(Figure 8-3).

133

Chapter 8 ■ WebContents, sCreens, and LoCaLes

Figure 8-3. The console output for the webContents array

See how that works? In case you can't read it, the interesting part looks like this:

browserWindowOptions: { width: 800, height: 600, title: 'hello world' }

A Little Setup Before We Begin

To make this example more effective for the content we are presenting, we need to make some updates to our current code. This example is going to create two windows, and we could also create two separate methods. But let's be practical and update our current createWindow method to be a little more dynamic. Let's change createWindow to look like this:

function createWindow (fileStr, options) { // Create the browser window. let win= new BrowserWindow(options)

// and load the index.html of the app. win.loadURL(url.format({ pathname: path.join(__dirname, fileStr),

134

Chapter 8 ■ WebContents, sCreens, and LoCaLes

protocol: 'file:', slashes: true }))

// Open the DevTools. // win.webContents.openDevTools()

// Emitted when the window is closed. win.on('closed', function () { // Dereference the window object, usually you would store windows // in an array if your app supports multi windows, this is the time // when you should delete the corresponding element. win = null })

return win}

Note the items in bold. Our createWindow method now takes two arguments: fileStr which is expected to be the name of the file our window will load, and options that is expected to be an object containing the setting for the window. Next, we create a variable named「win」for our new window, instantiate that window passing the options argument, load the URL for that window using the fileStr argument, and finally return the window.

Now to make this work, we need to make a change inside our「ready」event listener. Make the following

change:

app.on('ready', () => { mainWindow = createWindow('index.html', { width: 800, height: 600, title: 'MAIN' })})

Here, we are setting our mainWindow variable by passing arguments to the createWindow method.

Nice. Now, there is one more thing to do to make this work. Open your index.html file and remove the text from inside the title tag in the header. The code should look like this:

<head> <meta charset="UTF-8"> <title></title> </head>

The reason we are clearing the title in the HTML header here is that currently, on the macOS, if there is a title in the header it does not get overwritten in the Electron window creation process. This does not occur on the Windows platform.

Let's run the npm start command in the terminal to make sure it works (Figure 8-4).

135

Chapter 8 ■ WebContents, sCreens, and LoCaLes

Figure 8-4. Our updated Main Window

Note that the title in the title bar is now「MAIN.」Nice, right. A window created in a more dynamic way. One more change and we'll be ready to move on. First, at the top of our file, update the following line so we have a new variable named secondWindow.

let mainWindow, secondWindow

Now, let's update our「ready」listener to create another window:

app.on('ready', () => { mainWindow = createWindow('index.html', { width: 800, height: 600, title: 'MAIN' }) secondWindow = createWindow('index.html', { width: 400, height: 400, title: 'SECOND' })})

If we've done everything properly, we should see two windows. Let's check it out by running the npm

start command (Figure 8-5).

136

Chapter 8 ■ WebContents, sCreens, and LoCaLes

Figure 8-5. Our main and second windows load

That does it. Now we're ready to move on to adding a few event listeners to our project.

WebContents Events

So, now that you have a little idea of what the WebContents object represents and can set up the project to load two windows, let's start leveraging webContents to get a little more information. The BrowserWindow's WebContents object emits a couple of events that you might need to use in your application. To give you an idea of what those events are, here's an alphabetical list of them:

•	•	•	•	•	•

「before-input-event」

「certificate-error」

「context-menu」

「crashed」

「cursor-changed」

「destroyed」

137

Chapter 8 ■ WebContents, sCreens, and LoCaLes

•	•	•	•	•	•	•	•	•	•	•	•	•	•	•	•	•	•	•	•	•	•	•	•	•	•	•	•	•

「devtools-closed」

「devtools-focused」

「devtools-opened」

「devtools-reload-page」

「did-change-theme-color」

「did-fail-load」

「did-finish-load」

「did-frame-finish-load」

「did-get-response-details」

「did-get-redirect-request」

「did-navigate」

「did-navigate-in-page」

「did-start-loading」

「did-stop-loading」

「dom-ready」

「found-in-page」

「login」

「media-started-playing」

「media-paused」

「new-window」

「page-favicon-updated」

「paint」

「plugin-crashed」

「select-client-certificate」

「select-bluetooth-device」

「update-target-url」

「will-attach-webview」

「will-navigate」

「will-prevent-unload」

Depending on what the application you are building does, not all of these events will be relevant to you. They are named very practically, so you can guess what they represent. We listed each of them here to give you an idea of how many events webContents emits, and if any of them peak an interest you should review the documentation to get a clear idea of what they do. Our assumption is that you will be creating an application that, for the most part, is self-contained and doesn't load a web application from the Internet. Under that assumption we are going to focus on a couple of events that you may find helpful:「did-start-loading,」「did-get-response-details,」「dom-ready,」「did-finish-load,」and「did-stop-loading.」

138

Chapter 8 ■ WebContents, sCreens, and LoCaLes

If you wish to explore any of the other events available, feel free to use the resulting code from this

exercise as a starting point for your investigations.

The「did-start-loading」Event

The first event we will look at is the「did-start-loading」event. This event is fired by the window's WebContent's object and happens, oddly enough, when the window begins loading. For various reasons, we may wish to capture this event on the Main Process in our application, perhaps to inform the user of this activity, or to trigger another activity. Let's create a listener inside our createWindow method to see how this works. Inside the main.js file, at the bottom of the createWindow method and before the return window line, add this event handler:

win.webContents.on('did-start-loading', event => { console.log('did-start-loading', event.sender.webContents.browserWindowOptions.title)})

This is a pretty simple event listener typically used in debugging. Since we know that the event.sender is a BrowserWindow object and has a webContents property, we can log the browserWindowOptions' title property in the console. Run the npm start command to see this working (Figure 8-6).

Figure 8-6. The message we sent to the console was not received

139

Chapter 8 ■ WebContents, sCreens, and LoCaLes

Hold on. That didn't work. What did we do wrong? It is good practice to place event listeners on any

object before the event is fired. In this case, since the「did-start-loading」event is fired when window.loadURL() is called, we need to attach that event before that line. Move that line up in our code to appear immediately below the creation of the win variable:

function createWindow (fileStr, options) { // Create the browser window. let win = new BrowserWindow(options)

win.webContents.on('did-start-loading', event => { console.log('did-start-loading', event.sender.webContents.browserWindowOptions.title) })

Now we can run the npm start command to see if the event is properly captured (Figure 8-7).

Figure 8-7. Now the console messages appear in the terminal window

140

Chapter 8 ■ WebContents, sCreens, and LoCaLes

Now we can see the console log along with the title we sent to the createWindow method. Awesome.

Now we can add a couple of more events that may be important to capture in your application:「dom-ready,」「did-finish-load,」and「did-stop-loading.」In the main.js file, just below the「did-start-loading」event listener, add listeners for「dom-ready,」「did-finish-load,」and「did-stop-loading」like below:

function createWindow (fileStr, options) { // Create the browser window. let window = new BrowserWindow(options)

window.webContents.on('did-start-loading', event => { console.log('did-start-loading', event.sender.webContents.browserWindowOptions.title) })

window.webContents.on('dom-ready', event => { console.log('dom-ready') })

window.webContents.on('did-finish-load', event => { console.log('did-finish-load', event.sender.webContents.getTitle()) })

window.webContents.on('did-stop-loading', event => { console.log('did-stop-loading', event.sender.webContents.id) })

// and load the index.html of the app. window.loadURL(url.format({ pathname: path.join(__dirname, fileStr), protocol: 'file:', slashes: true }))

// Emitted when the window is closed. window.on('closed', function () { // Dereference the window object, usually you would store windows // in an array if your app supports multi windows, this is the time // when you should delete the corresponding element. window = null })

return window}

We have included these events on purpose and each has a specific purpose. Notice how we have different console log calls in each listener. The listener of「dom-ready」is just logging the event name, while「did-finish-load」logs the sender's WebContent's title, and the「did-stop-loading」logs the sender's WebContent's id.

As a side note, try to remember the difference between these event names:「load」and「loading」in

「did-finish-load」and「did-stop-loading.」If you decide to use both events and one of them isn't being captured, you may have incorrectly used「did-finish-loading,」for instance, instead of「did-finish-load.」These two event names might catch you off guard.

141

Chapter 8 ■ WebContents, sCreens, and LoCaLes

Run the npm start command in the terminal and see what happens (Figure 8-8).

Figure 8-8. Messages from the event listeners appear in the terminal window

Interesting, right? Here's a printout of the console logs so we can review them.

did-start-loading MAINdid-start-loading SECONDdom-readydom-readydid-finish-load index.htmldid-stop-loading 1did-finish-load index.htmldid-stop-loading 2

Note first that there are two of each message logged. The first two messages help you understand why, of course, and that is because we are opening two windows. Now, let's take a moment to consider our new event listeners' console logs.

Were you expecting「dom-ready」to show up last? Or「did-finish-load」? As Web developers we are

typically conditioned to keep an eye on the「dom-ready」event, but both「did-finish-load」and「did-stop-loading」occur after the「dom-ready」event is fired. And if the application that your BrowserWindow object is loading is complex - like an Angular or React application instead of the simple index.html file we are currently loading - there may be things that application may also be waiting for the「dom-ready」event to fire, as well. If your Main Process is waiting for the window to be ready before attempting to interact with it, you may wish to rely upon the「did-stop-loading」event.

142

Chapter 8 ■ WebContents, sCreens, and LoCaLes

Why isn't the「did-finish-load」event logging「MAIN」or「SECOND」instead of「index.html」? We were

wondering that as well. In our investigations, it seemed that relying upon the getTitle method would be poor form since it is not showing the information we requested. At least we can see the ids appear to be correct in the「did-stop-loading.」

Let's try something else in the「did-finish-load」listener and see if we can't do better. Change the

following code in bold in the main.js file:

window.webContents.on('did-finish-load', event => { console.log('did-finish-load', BrowserWindow.fromId(event.sender.webContents.id).getTitle()) })

Again, note that if you have not removed the title text inside the header of the HTML, that text may be

captured instead of the text that was dynamically set.

What we are doing here is leveraging the BrowserWindow class' fromId method with the event sender's

WebContent's id to get the window object so we can call getTitle() on it. I know that sounds like technical gymnastics, but if you want a consistent way to get the window title, this method may be helpful.

Run the npm start command and see it in action (Figure 8-9).

Figure 8-9. Better information captured by event listeners

143

Chapter 8 ■ WebContents, sCreens, and LoCaLes

The capturePage Method

The WebContents object has another nice feature that you may wish to take advantage of: the capturePage method. Capturing your application's screen is a feature that developers often are charged with creating. Luckily for us, the developers at Electron have made it easy for us to capture an image of our window, and Electron's Inter-Process Communication makes it easy to communicate between the Main and Renderer Processes, and Node.js makes it easy to save that image. This example will take a moment to set up, but we are certain you will find it rewarding.

Let's begin in the Renderer process. Open your index.html file. Remember, we are using this file as the

basis for both our「MAIN」and「SECOND」windows, so changes in this file will appear in both windows. Inside the index.html code, make the following update just above the closing tag of the body element (</body>):

<div>  <button id="captureButton">Capture PNG</button> </div>

Basically, we just added a button to the window. Now, open the renderer.js file, which is where the

JavaScript code for the Renderer Process is being kept. Right now there are just a few lines of commented text. Add the following code to the file:

const { ipcRenderer } = require('electron')

document.getElementById('captureButton').addEventListener('click', captureButtonClickHandler)

function captureButtonClickHandler() { ipcRenderer.send('capture-window')}

In the first line of our code we add Electron's ipcRenderer module to our project. If you remember from an earlier chapter, the ipcRenderer is how the Renderer Process communicates with the Main Process. The next line is the click listener for the「captureButton」element we added to the index.html file. Finally, we added the captureButtonClickHandler method inside, which we call the Main Process with the「capture-window」event. Before we move on to the Main Process part of this example, let's run the npm start command and take a look at what we've got (Figure 8-10).

144

Chapter 8 ■ WebContents, sCreens, and LoCaLes

Figure 8-10. The new button appears in both windows

Two windows? Check. New button on each window? Check. We've passed inspection! Now open the

main.js file and add the following code in bold to the top of the file:

const electron = require('electron')// Module to control application life.const app = electron.app// Module to create native browser window.const BrowserWindow = electron.BrowserWindowconst webContents = electron.webContentsconst ipcMain = electron.ipcMain

const path = require('path')const url = require('url')const fs = require('fs')

// Keep a global reference of the window object, if you don't, the window will// be closed automatically when the JavaScript object is garbage collected.let mainWindow, secondWindow, windowToCapture

Here we are adding ipcMain, the Main Process module for Inter-Process Communication, along with

「fs,」the file system module from Node.js that gives us access to the computer's drive. Finally, we add the windowToCapture variable, which we will be using in a moment. Also, you may wish to delete the console.log() line here, as it is unnecessary.

145

Chapter 8 ■ WebContents, sCreens, and LoCaLes

Next, at the bottom of the main.js file, add this code:

ipcMain.on('capture-window', event => { windowToCapture = BrowserWindow.fromId(event.sender.webContents.id) let bounds = windowToCapture.getBounds() windowToCapture.webContents.capturePage({x: 0, y: 0, width: bounds.width, height: bounds.height}, imageCaptured)})

function imageCaptured(image) { let desktop = app.getPath('desktop') let filePath = desktop + '/' + windowToCapture.getTitle() + '-captured-file.png' console.log(filePath) let png = image.toPNG()

fs.writeFileSync(filePath, png)}

The first item here is the「capture-window」event listener, which sets the windowToCapture variable,

creates a bounds object (an object that contains x, y, width, and height properties) by accessing the BrowserWindow's getBounds method. Finally, the listener calls the BrowserWindow's WebContents' capturePage method, passing 0 for x and y and then the bounds object's width and height. The second argument for the capturePage method is the name of the callback function, imageCaptured, which is invoked when capturePage completes its work.

The imageCaptured method, which expects a NativeImage object to be passed in, comes next.

NativeImage is a handy object provided by Electron, which allows developers the ability to create application icons in the PNG and JPEG formats, to handle situations like this. Next, the method creates a variable named desktop, a string that represents the path to the computer's desktop folder, by calling app.getPath(‘desktop'). Best practice would be to present a dialog that allows the user to choose where to place this file, but we can take a shortcut here to save time. Check out the Dialogs chapter to get more information about Dialogs, and, as always, ask the user where they want files to be saved.

Once we have the desktop path, we combine it with the title of the window and add「-captured-file.png」to it. Please observe that the desktop path does not end in a trailing「/」, which is why we've added it between the desktop path and the window title. And, then we call the NativeImage method toPNG(), which converts the image of our window into a variable named png. Now that we have the png and the path to where we'd like to save it, all we need to do is save the png file. This is where the FS module comes in. Using the writeFileSync method and passing the path and the png, we trigger a write function that will either work or throw an error.

As a side note, if you are planning on saving files with your Electron application, make sure you

familiarize yourself with the Node.js FS module and the writeFileSync and writeFile methods. We are using writeFileSync here because it suits our purposes, but the writeFile method works asynchronously, which may be more useful for avoiding user interface blocking when saving large files.

Let's save our files and give the npm start command a go and see how it works. When the application

loads, click the「capture image」button. An image should be saved to your desktop.

We chose to click on the button in the window named「SECOND,」so these are our results (Figure 8-11).

146

Chapter 8 ■ WebContents, sCreens, and LoCaLes

Figure 8-11. Capturing the window. Note the saved file on the desktop.

Awesome. Our code saved a file to the desktop and named it correctly. Open up the file so we can take a

look at it (Figure 8-12).

Figure 8-12. The captured image. Note the color of the button.

147

Chapter 8 ■ WebContents, sCreens, and LoCaLes

OK. This isn't right. There are two problems with this file. First, why is the button blue? That is because

when we grabbed the image, the button was in the down position. So, the image is correctly showing the button, but that isn't what we want today. Also, notice that the background of the image is gray. Shouldn't it be white like it appears on the screen?

We can fix these problems fairly easily. First, inside our「ready」listener in the main.js file, place the

following updates in bold:

app.on('ready', () => { mainWindow = createWindow('index.html', { width: 800, height: 600, title: 'MAIN',

backgroundColor: '#FFF' })

secondWindow = createWindow('index.html', { width: 400, height: 400, title: 'SECOND',

backgroundColor: '#FFF' })

})

Here, we've added the background color property to our options object so that when the window is

created it has a background color. Without this property being set, Electron thinks it doesn't have a color and makes the image appear to have a gray background (it is actually transparent).

Next, we want to grab the image of the window after the button has been released. There are a few

ways to do this. We choose to use JavaScript's setTimout method to trigger the capturePage method. In the「capture-window」listener, make the following changes in bold:

ipcMain.on('capture-window', event => { windowToCapture = BrowserWindow.fromId(event.sender.webContents.id) let bounds = windowToCapture.getBounds() // DO THIS TO CAPTURE THE SCREEN WITH UP BUTTONS setTimeout(() => { windowToCapture.webContents.capturePage({x: 0, y: 0, width: bounds.width,

height: bounds.height}, imageCaptured)

}, 500)})

This code waits half a second (that is what the 500 argument represents in milliseconds for

setTimeout()), and then calls the same function as before to capture the window image. Give it a try to see your results (Figure 8-13).

148

Chapter 8 ■ WebContents, sCreens, and LoCaLes

Figure 8-13. Captured image of the window without the button down state

Alright! That is more like it! Great job!

The printToPDF Method

Like the capturePage method, the WebContents' printToPDF method can be equally helpful. It is basically the same setup as the capturePage exercise. Let's get started.

Open your index.html file and add the following code in bold to add a second button:

<body> <h1>Hello World!</h1> <!-- All of the Node.js APIs are available in this renderer process. --> We are using Node.js <script>document.write(process.versions.node)</script>, Chromium <script>document.write(process.versions.chrome)</script>, and Electron <script>document.write(process.versions.electron)</script>. <div>

<button id="captureButton">Capture PNG</button>  <button id="printButton">Print to PDF</button>

</div> </body>

149

Chapter 8 ■ WebContents, sCreens, and LoCaLes

Then, in the renderer.js, update this line at the top of the file with the code in bold which will add a new

variable named windowToPrint.

let mainWindow, secondWindow, windowToCapture, windowToPrint

Now, add the following code in bold to listen to the click event and broadcast an event over Inter-

Process Communication to the Main Process:

const { ipcRenderer } = require('electron')

document.getElementById('captureButton').addEventListener('click', captureButtonClickHandler)document.getElementById('printButton').addEventListener('click', printButtonClickHandler)

function captureButtonClickHandler() { ipcRenderer.send('capture-window')}

function printButtonClickHandler() { ipcRenderer.send('print-to-pdf')}

Now, open the main.js file and add the following code to the bottom of the file:

ipcMain.on('print-to-pdf', event => { windowToPrint = BrowserWindow.fromId(event.sender.webContents.id)

windowToPrint.webContents.printToPDF({}, pdfCreated)})

function pdfCreated(error, data) { let desktop = app.getPath('desktop') let filePath = desktop + '/' + windowToPrint.getTitle() + '-printed.pdf'

if(error) { console.error(error.message) } if(data) { fs.writeFile(filePath, data, error => {  if(error) {  console.error(error.message)  } }) }}

Just like in the capturePage section of this chapter, we are listening for an event over IPC, and this time

it is the「print-to-pdf」event we broadcast from the Renderer Process. We create a BrowserWindow object by leveraging the Event's WebContents object's id property and then call that BrowserWindow object's Webcontents' printToPDF method. The first argument for the printToPDF method is an object that holds any custom options you may like to set, options like margins of the page, the size of the page, and whether the

150

Chapter 8 ■ WebContents, sCreens, and LoCaLes

background of the window should be captured. We are sending along an empty object, which means we are accepting the default options for this PDF file. Finally, like before, we use the FS module to write the file to the desktop. Save your files and run the npm start command in the console to see your results, which should look like the following screenshots (Figures 8-14 and 8-15).

Figure 8-14. Using printToPDF saved a file to the desktop

Figure 8-15. The PDF that was created using printToPDF

151

Chapter 8 ■ WebContents, sCreens, and LoCaLes

Getting Information about Screens

Another practical feature that your Electron may need to access is Electron's screen module. The screen module gives you information about the screen or screens attached to the user's computer. You can also use screen to listen for when new displays are added or removed, or when the displays change size. Some of these items may seem unimportant for the kind of application you are planning to build, so this exercise will take you through the process of using one of the practical features of screen: using the screen module to set the location of a window.

We are going to continue working with this chapter's code, but please take a moment to comment or

remove any of the console logs in your code so we can have a clean terminal window to work with.

As developers, we often work using multiple monitors attached to our computers. This is the case with the computer we are using here, so we will take advantage of that fact. Let's begin by adding a method to the bottom of our main.js file.

// SCREEN FUNCTIONS AND EVENTSfunction getScreenInfo() { let screen = electron.screen let currentScreens = screen.getAllDisplays() console.log('screens', currentScreens)}

This method creates a variable named screen by referencing electron.screen, which is important to

remember. If we had created a constant at the top of this file to represent the screens module, we would have received an error stating that electron.screens isn't available until after the application is ready. This makes sense: it is not until the application has initialized that it can access the computer's screen.

Next, we use the getAllDisplays method to create the currentScreens variable. Then, we log the contents

of the currentScreens variable so we can take a look at what they look like in the terminal window.

Now we need to call this method. Inside our「ready」listener for our application, update the code in

bold to call getScreenInfo():

app.on('ready', () => { getScreenInfo() mainWindow = createWindow('index.html', { width: 800, height: 600, title: 'MAIN', backgroundColor: '#FFF' }) secondWindow = createWindow('index.html', { width: 400, height: 400, title: 'SECOND', backgroundColor: '#FFF' })})

Let's take a look at our results by running the npm start command in the terminal (Figure 8-16).

152

Chapter 8 ■ WebContents, sCreens, and LoCaLes

Figure 8-16. Information about the screens appears in the terminal window

That's a lot of data in the terminal window. Let's print it out here so we can review it together.

screens [ { id: 709428740, bounds: { x: 0, y: 0, width: 1920, height: 1200 }, workArea: { x: 0, y: 23, width: 1920, height: 1173 }, size: { width: 1920, height: 1200 }, workAreaSize: { width: 1920, height: 1173 }, scaleFactor: 1, rotation: 0, touchSupport: 'unknown' }, { id: 69731266, bounds: { x: 1920, y: 300, width: 1440, height: 900 }, workArea: { x: 1920, y: 300, width: 1440, height: 900 }, size: { width: 1440, height: 900 }, workAreaSize: { width: 1440, height: 900 }, scaleFactor: 2, rotation: 0, touchSupport: 'unknown' }, { id: 709428739, bounds: { x: -1920, y: 0, width: 1920, height: 1200 }, workArea: { x: -1920, y: 0, width: 1920, height: 1200 }, size: { width: 1920, height: 1200 }, workAreaSize: { width: 1920, height: 1200 }, scaleFactor: 1, rotation: 0, touchSupport: 'unknown' } ]

153

Chapter 8 ■ WebContents, sCreens, and LoCaLes

First, note that the screen variable is an array of three objects. Those three objects represent the three

monitors, or screens, attached to this computer. Each of these objects has properties of bounds, workArea, size, workAreaSize, scaleFactor, rotation, and touchSupport. That is a lot of information. Take a look at the bounds property of each object. Note that the coordinates do not overlap. For instance, the three x properties are 0, 1920, and -1920. That means that screen 1 is in the middle at 0, screen 2 is to the right of screen 1 at 1920, and screen 3 is to the left of the screen 1 at -1920. Hopefully that makes sense. But, for practical purposes, this is way too much information, so let's update our code and use a different method to narrow down our scope.

Update the getScreenInfo method to match the following code. We are commenting out our original call

to getAllDisplays and adding a call for getPrimaryDisplay.

// SCREEN FUNCTIONS AND EVENTSfunction getScreenInfo() { let screen = electron.screen

let primaryScreen = screen.getPrimaryDisplay() console.log('prime', primaryScreen)}

Now, let's give the npm start command a try and see what we get (Figure 8-17).

Figure 8-17. Information about the primary display appears in the terminal window

154

Chapter 8 ■ WebContents, sCreens, and LoCaLes

OK, so, the getPrimaryDisplay method returns on screen. Nice. Same properties as the objects we

received from the getAllDisplays, only this object represents the screen the user has designated as their main screen (or, in this case, the screen where the macOS dock is located). Let's use this information to position our second screen.

First, inside our getScreenInfo method, let's comment two lines and return the bounds of the

getPrimaryDisplay so we can use it later. Make the following updates to the method:

// SCREEN FUNCTIONS AND EVENTSfunction getScreenInfo() { let screen = electron.screen

return screen.getPrimaryDisplay().bounds}

Now, we need to put that information to use. Inside the「ready」listener, make the following changes

in bold:

app.on('ready', () => { let screenBounds = getScreenInfo()

mainWindow = createWindow('index.html', { width: 800, height: 600, title: 'MAIN', backgroundColor: '#FFF' })

let newX = screenBounds.width - 400 let newY = screenBounds.height - 400 secondWindow = createWindow('index.html', { x: newX, y: newY, width: 400, height: 400, title: 'SECOND', backgroundColor: '#FFF' })})

What we are doing here is placing the secondWindow into the bottom right corner of our primary

screen by using a little Math and updating our window options. First, we create a variable named screenBounds and call the getScreenInfo method to set it. Then we take the width property of screen bounds and, since we know that the width of the second window is 400 pixels, we subtract the window's width. Then, we do the same with height. That gets us the new x and y coordinates that we use to position our second window. It is important to remember on macOS, when the dock is locked on the screen and window cannot overlap the dock when it is resized, and therefore the bounds will never equal that of the primary screen. Also, remember from the BrowserWindow chapter that we must use both the x and y properties with setting the options for a window; otherwise the properties are ignored.

Run the npm start command and see where the second window displays (Figure 8-18).

155

Chapter 8 ■ WebContents, sCreens, and LoCaLes

Figure 8-18. The second window appears in the bottom corner

Finding Locales

The final practical feature we will review in this chapter is Electron's Locales feature. Locales are used to discover the language settings on the computer being used. Internationalization, or i18n is so named because the word begins with an「I,」ends in an「n,」and has 18 characters in between; and localization, or l10n, is important because these days, an Electron application can easily be distributed through the Internet to users all around the world. Wouldn't it be nice to display text and menu items in the language preferred by the user? Of course, you would since you like your users and want them to enjoy using your application.How you implement your i18n features will be up to you. The Web application you are displaying in

your Renderer Process probably has modules available to implement i18n, but you still need to detect it. Sure, you can check the window.navigator.userLanguage in the Renderer Process, but to create the application's menus are created in the Main Process. Discovering the locale of the system your application is running on in the Main Process is essential.

For now, let's add the following line in bold to our「ready」listener.

app.on('ready', () => { console.log(app.getLocale())

mainWindow = createWindow('index.html', { width: 800, height: 600, title: 'MAIN',

backgroundColor: '#FFF' })

let newX = screenBounds.width - 400 let newY = screenBounds.height - 400

156

Chapter 8 ■ WebContents, sCreens, and LoCaLes

secondWindow = createWindow('index.html', { x: newX, y: newY, width: 400, height: 400,

title: 'SECOND', backgroundColor: '#FFF' })

})

Now, run the npm start command and take a look at your terminal window (Figure 8-19).

Figure 8-19. The locale appears in the terminal window

On this computer, the log entry in the terminal window says en-US, which, of course, means that this computer has been set up to display English and things like currency and units of measurement based on how people who live in the United States would see them. In the Electron documentation, you will find a long list of languages that can be discovered using getLocale(). Now that you know how to access the locale, there is absolutely no reason to not get internationalization running for your application.

Summary

In this chapter, we took a look at webContents, screen, and Locales. We learned how to access the webContents object's methods like getTitle() on BrowserWindow objects. We created listeners for important webContents events. We learned how to create an image and PDF file from a window using the webContents object's capturePage() and printToPDF() methods. We learned how to get information on all the displays attached to the user's computer and how to identify the primary display. And, finally, we learned how to discover what locale the user's computer has been set up to use. We hope that you found this information helpful.

157

CHAPTER 9


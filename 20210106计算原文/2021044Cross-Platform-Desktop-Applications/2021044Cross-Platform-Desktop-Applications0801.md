 Adding menu items to the tray menu

Some apps aren't as beefy as others and focus on doing something specific anddoing it well. They also focus on being accessible to the user without having toswitch windows or switch focus from the current app that's in front of them. As aresult, app functionality is made available from the tray bar of the OS, which islocated at the bottom of the Windows GUI, at the top of the screen on a Mac,and—depending on what flavor of distribution and graphical desktop environmentyou use—either the top or bottom on Linux (Gnome tends to be at the top, andKDE tends to be at the bottom).

Tray apps tend to be utility apps like timers, music controls, and instant messag-ing. They use menus and changing icons to communicate the status of the app. Inthis chapter, we'll look at how you can use NW.js's UI API to make tray apps by cre-ating a small utility tray app with a dropdown menu. We'll then replicate this exam-ple with Electron to compare its tray app functionality.

143

144

8.1

CHAPTER 8 Creating tray applications

Creating a simple tray app with NW.jsYou'll build something small and simple, as shown in figure 8.1.

Figure 8.1 The app you'll build: a simple tray app with lists

Let's say you have a simple Hello World NW.js app, and you'd like to give it a tray iconto access it from the OS's main bar. Figure 8.2 shows what you want to create in themenu bar.

Figure 8.2 Your tray app displaying in the tray area of the OS's main bar

You can do that by changing index.html to contain the following embedded JavaScript:

<html> <head> <title>tray app example</title> <script>  const gui = require('nw.gui');  const tray = new gui.Tray({title: 'My tray app'}); </script> </head> <body> <h1>Hello world</h1> </body></html>

Creating a simple tray app with NW.js

145

In this code, you extend the example Hello World app with some embedded Java-Script, and in that script are two lines of interest: the first is the one that loads NW.js'sUI API, and the second is the one that creates a new tray, with the title「My tray app.」If you run this app from the command line, you should see the usual Hello Worldexample app, but you'll also see this item appear in your OS's main bar, as shown infigure 8.2.

SHOULD YOU USE TEXT LABELS FOR TRAY APPS? If you want to support Mac OSX only, then that's fine, but on Windows and Linux, tray apps display iconsonly. Your safest option is to go with using icons only for your tray apps.

You'll see that the text label you gave the tray app is displayed in the tray area. You'llalso notice some other tray apps running there (VOX and 1Password), which choosenot to display labels, only icons. If you want to display an icon as well (because it usesless space in the tray area), you can do that too with NW.js. Assume that you have asimple .png icon that you'd like to use (in this case, I've created a simple note-takingicon with Pixelmator, at a resolution of 32 x 32 pixels). Save it in the same folderwhere the index.html file is kept and alter the JavaScript line that creates the tray appto this:

const tray = new gui.Tray({icon: 'icon@2x.png'});

After making those changes, you'll need to rerun NW.js from the command line, andyou should see the tray app icon look like figure 8.3.

Figure 8.3 The tray app displaying a custom icon created with Pixelmator

This gives you a nice icon that fits with the pattern of tray apps on Mac OS X, butyou'll probably notice one oddity: the app icon's colors are in grayscale. That's some-thing that NW.js does, but Electron renders the icon in color.

8.1.1

Adding menus to your tray iconIf you click on your tray app icon now, it doesn't do anything. You want to use the trayapp as a way to execute other commands and interact with your app. Menus provide away for tray apps to display a list of contents or trigger other actions. You want a solu-tion that shows a menu listing the notes when the icon is clicked, as in figure 8.4.

Figure 8.4 The notes tray app displaying a list of notes

146

CHAPTER 8 Creating tray applications

You can extend your simple tray app by adding a menu that lists a number of pre-defined notes. Clicking one of the notes loads the contents of that note in the appwindow. Let's start by creating some sample note content to put at the start of theembedded JavaScript:

const notes = [ {  title: 'todo list',  contents: 'grocery shopping\npick up kids\nsend birthday party invites'}, {  title: 'grocery list',  contents: 'Milk\nEggs\nButter\nDouble Cream'}, {  title: 'birthday invites',  contents: 'Dave\nSue\nSally\nJohn and Joanna\nChris and Georgina\nElliot' }];

Now that you have content, you can add the titles of the notes to a new menu as menuitems, and attach that new menu to the tray:

const menu = new gui.Menu();notes.forEach((note) => { menu.append(new gui.MenuItem({label: note.title}));}

tray.menu = menu;

Here, you initialize a new Menu object and then loop through the list of notes, display-ing their titles in the menu. After that, the menu is attached to the tray. Run NW.js onthe app's code from the command line, and you should see a result like the oneshown in figure 8.4.

So far, so good, but there's a bit more to do. You haven't yet got the tray menuitems to interact with the app window, and you'd like to make the tray app work insuch a way that when a note is clicked from the menu, the contents of that note areloaded into the app window.

To do this, you'll need to do the following:

 Change the HTML in the screen to have placeholders for the title and contents

of a note.

 Create a function to insert the title and contents of a note into the HTML. Alter the menuItem objects to trigger this function when they're clicked.

Start by modifying the body tag's inner HTML. Change it to this:

<body> <h1 id="title"></h1> <div id="contents"></div> </body>

Creating a simple tray app with NW.js

147

The h1 tag will contain the title of the note (hence, the id attribute with a value of"title"), and the div tag will contain the contents of the note (again, with the idattribute of "contents"). Next, at the top of the embedded JavaScript, create a func-tion that will insert the title and contents of a note into the page:

function displayNote (note) { document.getElementById('title').innerText = note.title; document.getElementById('contents').innerText = note.contents; }

This function inserts the title and contents of the note object passed to it into theHTML elements on the page. Once you have this function, you'll modify the menu-Item objects so they call the displayNote function with the note object when clicked. To do that, though, you need to move some of that code into a new function,because you shouldn't make functions within a loop (otherwise, you get some unex-pected behavior with the variable that's passed to the function). Create a new functioncalled appendNoteToMenu and define it after the initialization of the menu object:

function appendNoteToMenu (note) { const menuItem = new gui.MenuItem({ label: note.title, click: () => { displayNote(note); } }); menu.append(menuItem);  }

The function receives the note object and generates a MenuItem object. It sets thelabel of the menu item to the note's title and defines a function to execute whenthe menu item is clicked. The function calls displayNote with the note object, so thatwhen the menu item is clicked, the note's title and contents are displayed in the appwindow. Finally, the menu item is added to the menu object.

Before the menu is added to the tray, modify the bit of code that loops through the

notes to call the appendNoteToMenu function, like so:

notes.map(appendNoteToMenu);

You're almost there. Next, make sure the app displays the first note in the list and giveit a bit of styling to make it more genuine.

When the HTML for the app has loaded, you'll be able to trigger displaying thefirst note that's available. Add the following JavaScript toward the end of the script tag:

document.addEventListener('DOMContentLoaded', () => { displayNote(notes[0]);});

When the app loads, as shown in figure 8.5, you should see that the first note is dis-played in the app window.

148

CHAPTER 8 Creating tray applications

Figure 8.5 The notes app displaying the first note in the list

Before you call this app done, add a link in the index.html file to a CSS stylesheet calledapp.css so you can make the notes app look a bit more like a note, as shown next.

Adds the link for an app.css file

Listing 8.1 Adding the CSS link to the index.html file

<html> <head> <title>tray app example</title> <link href="app.css" rel="stylesheet">  <script>  'use strict';

Next, add an app.css file with the following CSS:

body { background: #E2D53C; color: #292929; font-family: 'Comic Sans', 'Comic Sans MS'; font-size: 14pt; font-style: italic;}

With the styling change in place, the notes app should now look like figure 8.6.

Figure 8.6 The notes app with CSS styling applied

If you run the app with NW.js from the command line, when you click a note title in thetray app's menu, you can expect the note's title and contents to display in the app window.

IS THERE A COPY OF THIS APP'S FULL SOURCE CODE? Yes, you can grab the codeexample tray App NW.js from this GitHub Repository: https://github.com/paulbjensen/cross-platform-desktop-applications

Creating a tray app with Electron

149

Now that you've created a tray app with NW.js, let's see how you go about replicatingthe example with Electron.

8.2

Creating a tray app with ElectronElectron's modular approach to creating apps lends itself well to creating tray apps.The API is similar to the one provided by NW.js, and this section shows how to re-createthe tray app from the previous section, but with Electron's API.

8.2.1 Building the initial app skeleton

The bare-minimum set of files needed for a tray app follows:

 main.js for the app's code A PNG image for the app icon A package.json file for the app's configuration

When creating a tray app in Electron, you don't need an index.html file, but you wantto show the content of the notes in the list, so you'll have a file for that, as well as anapp.js file for the app's front-end code.

You'll start by writing the app's package.json. Make a folder called tray-app-electron

and insert a file named package.json with the following code:

{ "name" : "tray-app-electron", "version" : "1.0.0", "main" : "main.js"}

Now, create the index.html file where the contents of the notes will be displayed. Cre-ate an index.html file and insert the following HTML into it:

<html> <head> <title>tray app Electron</title> <link href="app.css" rel="stylesheet"> <script src="app.js"></script> </head> <body> <h1 id="title"></h1> <div id="contents"></div> </body></html>

The index.html applies the same HTML structure as the NW.js example, except thatwhere NW.js has inline JavaScript, you move the front-end JavaScript into the app.jsfile. This is because Electron keeps the front-end JavaScript separate from the back-end JavaScript and requires using inter-process communication to transmit data fromthe app's back end to the browser window, as you'll see later in the example.

150

CHAPTER 8 Creating tray applications

The app.css file is identical to the app.css file that you used in the NW.js tray app,so I won't repeat it here, and the same goes for the app icon. The main meat of theapp is in the main.js file (back end) and the app.js file (front end). We'll look at themain.js file first.

Create a file called main.js and insert the following code.

Listing 8.2 The main.js file for the Electron tray app

'use strict';

const electron = require('electron');const app = electron.app;const Menu = electron.Menu;      const tray = electron.Tray;        const BrowserWindow = electron.BrowserWindow;

Requires Electron's Menu API

Loads its tray API

let appIcon = null;      let mainWindow = null;

Creates a null appIcon variable so tray app doesn't get garbage collected

const notes = [ { title: 'todo list', contents: 'grocery shopping\npick up kids\nsend birthday party invites' }, { title: 'grocery list', contents: 'Milk\nEggs\nButter\nDouble Cream' }, { title: 'birthday invites', contents: 'Dave\nSue\nSally\nJohn and Joanna\nChris and Georgina\nElliot' }];

function displayNote (note) { mainWindow.webContents.send('displayNote', note); }

function addNoteToMenu (note) { return { label: note.title, type: 'normal', click: () => { displayNote(note); } };}

Uses Electron's WebContents API to send data to browser window to display note's contents

Creates contextmenu for trayapp, loopingthrough notes toadd menu items

Binds context menu to tray app

Sets atooltip ontray app

app.on('ready', () => { appIcon = new Tray('icon@2x.png');     let contextMenu = Menu.buildFromTemplate(notes.map(addNoteToMenu));  appIcon.setToolTip('Notes app');         appIcon.setContextMenu(contextMenu);

Creates tray app with icon

mainWindow = new BrowserWindow({ width: 800, height: 600 }); mainWindow.loadURL(`file://${__dirname}/index.html`);

Creating a tray app with Electron

151

mainWindow.webContents.on('dom-ready', () => { displayNote(notes[0]);     });});

When app window is loaded, defaults to displaying first note

Now, the back-end code will create the tray app, its menu, and a BrowserWindowinstance to display a note's contents. This will allow the app to load up with the firstnote. The app.js file handles when a note is clicked in the menu. The app.js file willuse Electron's ipcRenderer module to handle receiving the displayNote event andthe note passed from the main process to the renderer process, so you can update theHTML inside the BrowserWindow process.

In the app.js file, insert the code shown next.

Listing 8.3 The app.js file for the Electron tray example

function displayNote(event, note) {        document.getElementById('title').innerText = note.title; document.getElementById('contents').innerText = note.contents;}

displayNote function inserts contents of note into HTML

const ipc = require('electron').ipcRenderer;   ipc.on('displayNote', displayNote);

Upon menu item click or when app loads,ipcRenderer module intercepts event and note;then passes them to displayNote

Electron's ipcRenderer module listens for events being triggered by back-end process

Electron's ipcRenderer module is able to send and receive data to/from Electron'smain process. In the context of the tray app, the back-end process passes data to thebrowser window via the web contents API, so the displayNote event and the note arepassed from the back end to the front end, and ipcRenderer listens on that event.When the event is triggered, ipcRenderer will pick up the note and pass it to the func-tion that handles inserting the note into the HTML. Figure 8.7 shows what the applooks like.

Figure 8.7 The Electron notes app. Notice how Electron renders the app icon in color by default.

152

CHAPTER 8 Creating tray applications

8.3

In this section, you've been able to use your knowledge of menus to build tray appsthat users can access easily—usually utility apps like chat apps, password managers,and to-do list apps. You've seen how to configure the icon for the app as well as attacha menu to it when it's clicked.

SummaryIn this chapter, we've looked at different ways to create tray apps in NW.js and Elec-tron. Tray apps are neat little utilities. When creating them, make sure to check howthey work across all OSs, because there will be variation (Mac OS X lets you use labelswith them, for example, but Windows and Linux only show icons). Also, rememberthat icons need to be within a 32 x 32–pixel dimension. We also looked at how to addmenu items to tray apps. Some key takeaways: You can use text for the app's tray menu display, but icons are preferable due to

how Windows and Linux display them.

 NW.js tray apps seem to display the tray icon in grayscale on Mac OS X, whereas

Electron tray apps display in color.

In chapter 9, we'll look at ways to mimic the look and feel of the user's OS.

Creating applicationand context menus

This chapter covers Creating application window menus Handling Mac OS's approach to menus Handing Windows's/Linux's approach to menus Creating context menus for the content inside of


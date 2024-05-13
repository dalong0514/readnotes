NW.js and Electron

Applications need to store data; when you're playing a game and loading from asaved level, or configuring settings for how you use a particular app, or even storingstructured data in a line-of-business app, data must be stored somewhere and mustbe accessed by the app with ease.

Options for how to store data in your app range from using the HTML5 local-Storage API to using embedded databases in your desktop app. In this chapter,we'll explore some options and see how you can use them with your desktop apps.

12.1 What data storage option should I use?

In the old days, this was a simple question—there were fewer options. Traditionally,web apps relied solely on storing data in databases that lived on back-end servers.With the advent of client-side storage APIs for HTML5, the ability to store data onthe client has resulted in the emergence of new libraries for that purpose, and forsynchronizing that data with an external database.

199

200

CHAPTER 12 Storing app data

Table 12.1 lists options for storing your data in web apps, and these can therefore

be used in both Electron and NW.js apps.

Table 12.1 Options for storing data

Name

Database type

Type

URL

IndexedDB

Key/Value

localStorage

Key/Value

Browser API

Browser API

https://is.gd/wwDSgj

https://is.gd/3XbaFQ

Lovefield

PouchDB

SQLite

NeDB

LevelDB

Relational

Document

Relational

Document

Key/Value

Client-side library

https://github.com/google/lovefield

Client-side library

https://pouchdb.com/

Embedded

Embedded

Embedded

http://sqlite.com/

https://is.gd/f44eap

http://leveldb.org/

Minimongo

Document

Client-side library

https://is.gd/yTRXhe

Lots of options are available, sure, but which one should you use? That depends onwhat data you're storing, how much of it you're storing, and how you'll need to querythat data.

If you have a good idea what kind of data you're going to be storing, and theschema for that data is known up front and is unlikely to change while the app is inuse, relational databases are worth considering due to the benefits of their powerfulquerying capabilities.

If you need to store no more than 5 MB of data for your app (for example, user set-tings), you can get away with using the browser-based API options, which impose limitsof 5 MB on how much data can be stored on them.

Another thing to consider is how you'll need to query the data. If the data is denor-malized and stored in tables with references to data in other tables, then a document-based approach might not be the most efficient when it comes to querying the data.The design of the data schemas and whether the data is denormalized or not will gosome way toward helping you choose whether to opt for a SQL-based or NoSQL-baseddatabase for data storage.

Enough debating about which option to pick. Let's give some of them a spin.

12.2 Storing a sticky note with the localStorage API

You'll create a simple single sticky note app called Let Me Remember. It's a dead-sim-ple app that will demonstrate what localStorage is handy for (storing text-based datain a key/value data store). There are two separate versions of the app for the differentframeworks, one for NW.js (called let-me-remember-nwjs) and one for Electron(called let-me-remember-electron). Both apps can be found in the book's GitHubrepository at http://mng.bz/fYrm and http://mng.bz/COlh.

Storing a sticky note with the localStorage API

201

You can either take a look at one of those apps and run the code according to theREADME instructions or assemble it from scratch. We'll look at the Electron versionof the app first, for a change.

12.2.1 Creating the Let Me Remember app with Electron

The app is mostly a vanilla boilerplate, but with a few distinct touches. Let's start withthe package.json file and work from there. First, you create a folder for the app. Youcan use the following commands in a terminal:

mkdir let-me-remembercd let-me-remember

Now, you can create a package.json file inside the folder and insert the code shown inthe next listing.

Listing 12.1 Making the package.json file for the Let Me Remember Electron app

{ "name": "let-me-remember-electron", "version": "1.0.0", "description": "A sticky note app for Electron", "main": "main.js", "scripts": { "start": "node_modules/.bin/electron .", "test": "echo \"Error: no test specified\" && exit 1" }, "keywords": [ "electron" ], "author": "Paul Jensen <paulbjensen@gmail.com>", "license": "MIT", "dependencies": { "electron ": "^1.3.7" }}

The main property in the package.json file indicates that the main.js file is the app'spoint of entry. The main.js file is mostly vanilla boilerplate, but there's a bit of codethat you need to make the app window frameless, as well as to apply width/height con-straints. This is so the app can have the look and feel of a sticky note to the user.

Don't forget to run npm install after saving the package.json to install the Elec-

tron dependency.

Let's create the main.js file next and add the code to it shown next.

Listing 12.2 Making the main.js file for the Let Me Remember Electron app

'use strict';

const electron = require('electron');const app = electron.app;const BrowserWindow = electron.BrowserWindow;

202

CHAPTER 12 Storing app data

let mainWindow = null;

app.on('window-all-closed', () => { if (process.platform !== 'darwin') app.quit();});

app.on('ready', () => { mainWindow = new BrowserWindow({ width: 480, height: 320, frame: false       }); mainWindow.loadURL(`file://${__dirname}/index.html`); mainWindow.on('closed', () => { mainWindow = null; });});

Sets frame attribute to false to make app window frameless

The main.js file configures the app window to be of a fairly small size so that it resem-bles the dimensions of a sticky note and has a frameless app window. Inside the appwindow is the index.html file that will be the only visible element of the app. Let's nowflesh out the index.html file with the content from the next listing.

Listing 12.3 Making the index.html file for the Let Me Remember Electron app

<html> <head>  <title>Let Me Remember</title>  <link rel="stylesheet" type="text/css" href="app.css">  <script src="app.js"></script> </head> <body>  <div id="close" onclick="quit();">x</div>   <textarea onKeyUp="saveNotes();"></textarea>  </body></html>

Triggers call to quit when clicking X

textarea element saves text on every keystroke

The index.html file is fairly simple, because the app itself is quite simple. There's noapp frame, so you implement a custom close button that, when clicked, will quit theapp. You then also define a textarea element, which is responsible for displayingthe text of the sticky note as well as allowing the user to edit it.

At the top of the index.html file, you load two front-end files: an app.css stylesheetand an app.js JavaScript file. We'll look at the stylesheet first. In the app's folder, cre-ate an app.css file, and put the CSS shown next inside.

Listing 12.4 Creating the app.css file for the Let Me Remember Electron app

body { background: #ffe15f; color: #694921; padding: 1em;}

Storing a sticky note with the localStorage API

203

textarea { font-family: 'Hannotate SC', 'Hanzipen SC','Comic Sans', 'Comic Sans MS'; outline: none; font-size: 18pt; border: none; width: 100%; height: 100%; background: none;}

#close { cursor: pointer; position: absolute; top: 8px; right: 10px; text-align: center; font-family: 'Helvetica Neue', 'Arial'; font-weight: 400;}

The CSS code here uses fairly common CSS rules and could be repurposed in a webapp if you wanted. The body is styled to look like the yellow paper commonly associ-ated with a sticky note, and the textarea is styled to look like handwriting—it evenuses Comic Sans as a last resort (the last time I saw Comic Sans in use was at AOL).Finally, the close button is given a different styling to make the X character look likethe one used for a close button.

With the styling applied, all that's left to do now is create the app.js file that con-tains the quit and saveNotes functions. In the same app folder, create the app.js fileand insert the code shown here.

Listing 12.5 The app.js file for the Let Me Remember Electron app

'use strict';

const electron = require('electron');const app = electron.remote.app;

Loads app module via remote API to enable quitting app

Calls HTML5 localStorage API to check for notes data

function initialize () { let notes = window.localStorage.notes;  if (!notes) notes = 'Let me remember...';    window.document.querySelector('textarea').value = notes; }

If none, sets it to default value

Loads notes data for display in textarea element

function saveNotes () { let notes = window.document.querySelector('textarea').value;   window.localStorage.setItem('notes',notes);  Saves text }content to HTML5 localStorage API

function quit () { app.quit(); }

quit function wraps call to quit function on the app module

window.onload = initialize;

Gets textcontent intextareaelement

204

CHAPTER 12 Storing app data

The app.js file helps implement the loading of data from the computer via theHTML5 localStorage API and then allows the user to record notes on the stickyand close the app down. When they type some notes, the notes are saved. When theyreopen the app, the notes they saved will be displayed in the sticky, as shown in fig-ure 12.1.

Figure 12.1 The Let Me Remember Electron app running on Windows 10. If you type some notes, close the app, and reopen it, it will load with the notes that you typed.

With the help of the HTML5 localStorage API, you've been able to add data persis-tence to your app and make it work in such a way that saving the notes happens invisi-bly in the background. It's the kind of user experience you want the app to provide—seamless.

Now, you can take a look at how the NW.js implementation differs in its approach.

12.2.2 Implementing the Let Me Remember app with NW.js

The NW.js implementation of the app varies slightly. It has the same CSS as the Elec-tron variant of the app and almost identical versions of the app.js and index.html files.You'll work from the package.json and look at the files from there.

Create a folder for the app, and then create a package.json file inside it and insert

the following code:

{ "name" : "let-me-remember", "version": "1.0.0", "main": "index.html", "window": { "width": 480, "height": 320, "frame": false }}

The package.json file is pretty much vanilla, with the exception of the window proper-ties. You've set the initial width and height to a relatively small size (similar to a largesticky note stuck on the screen) and turned off the window frame so that it will looklike a sticky note stuck on the screen.

Storing a sticky note with the localStorage API

205

Next, you'll add the index.html file in the folder, and put the following code in there:

<html> <head> <title>Let Me Remember?</title> <link rel="stylesheet" type="text/css" href="app.css"> <script src="app.js"></script> </head> <body> <div id="close" onclick="process.exit(0)">x</div>  <textarea onKeyUp="saveNotes();"></textarea> </body></html>

The HTML file is a simple file as well. You use a textarea element to capture thenotes that you want to jot down inside the sticky note. You could have used a p ele-ment with a contenteditable attribute, but you need to be able to capture the eventwhen new content enters the p element, and currently there isn't a way to do that. Youalso have a div element with the ID attribute of "close", which when clicked will trig-ger the process of exiting the app (because you've hidden the window frame aroundthe app, and therefore you wouldn't have a way to close the app graphically, except fornavigating to the menu bar and closing the app from there). Note that this doesn'tcall a quit() function, because you can directly call Node.js's process global variablefrom the JavaScript context in the HTML.

The app.css file is identical to the one used in the Electron app, shown in listing 12.4,so you can avoid repeating yourself on that. As for the app.js file, the code is similarbut has a little less code, as shown next.

Listing 12.6 The app.js file for the Let Me Remember NW.js app

'use strict';

function initialize () { let notes = window.localStorage.notes; if (!notes) notes = 'Let me remember...'; window.document.querySelector('textarea').value = notes;}

function saveNotes () { let notes = window.document.querySelector('textarea').value; window.localStorage.setItem('notes',notes);}

window.onload = initialize;

It's quite a nice, compact bit of code, so let's go through it. When the app and theDOM have loaded, you call an initialize function to retrieve any notes that arestored under the key name of notes. If there are no notes, then you provide somedefault copy,「Let me remember. . .」and insert that into the textarea element inthe page.

206

CHAPTER 12 Storing app data

If you take a quick glance back to the index.html file, you'll notice that the text-area element had an onKeyUp attribute that called a function named saveNotes. Well,the saveNotes function does what the name suggests—it gets the text that's currentlyin the textarea element of the app and calls the localStorage API's setItem func-tion to set the value of notes to that text.

If you type in some items you want to get, such as a grocery list, and then close theapp, you should find that when you reopen the app, the notes have been saved andwill be displayed as before, as in figure 12.2.

Figure 12.2 The Let Me Remember NW.js app. I've added some grocery list items for shopping later.

The localStorage API is ideal for storing unstructured text with a simple key/valuestorage mechanism (getItem, setItem). The Let Me Remember app example youwent through is an ideal use case for it, but a lot of other apps will need to store struc-tured data that's not necessarily in string format—it might be an array of strings, orintegers, or other kinds of data types.

One potential approach to storing that kind of data is serializing and deserializingthe data with JSON.stringify() and JSON.parse(). If the use case of your app is welldefined, then this approach can work. An example of this is the popular TodoMVCproject. To demonstrate this, you'll port one of the TodoMVC app examples tobecome a desktop app, with a few changes.

12.3 Porting a to-do list web app

Storing a to-do list with the localStorage API is possible—in fact, this is how theTodoMVC project handles data persistence.

The TodoMVC project is a collection of examples of the same to-do list app, imple-mented using different JavaScript frameworks. Its purpose is to show developers howeach framework approaches implementing a to-do list app so that users can find theright framework for their needs.

There are lots of different implementations of the TodoMVC app, including Sock-etstream (a framework for real-time web apps that I've been involved with in the past).

Porting a to-do list web app

207

You'll take a popular framework called React and use its implementation as the exam-ple that you'll port to a desktop app.

Porting this app will demonstrate a major key benefit of both Electron and NW.js:

how easy it is to reuse code from a web app inside a desktop app.

12.3.1 Porting a TodoMVC web app with NW.js

First, you need to make a copy of the TodoMVC GitHub repository. Find a folderwhere you want to install a local copy of the repository and clone it to there with Gitfrom the Terminal:

git clone git@github.com:tastejs/todomvc.git

Inside the cloned GitHub repository, you'll find an examples folder containing all thedifferent implementations of the TodoMVC app. You're interested in the foldernamed react. Open the folder in your text editor/IDE of choice and add these lines tothe package.json file:

"name":"todo-mvc-app","version":"1.0.0","main":"index.html","window": { "toolbar":false}

Save the package.json file, and run nw inside the folder in the Terminal. You shouldsee the app running on your desktop. Add some to-do list items to it and then closethe app and reopen it. What you'll see is something like figure 12.3.

Figure 12.3 The TodoMVC app running as a desktop app via NW.js, with data being stored in the app via the HTML5 localStorage API

208

CHAPTER 12 Storing app data

What's so cool about this is that with six lines of code added to one file, you've turneda web app into a desktop app. If only all apps could be ported that easily! If you'reinterested in seeing what's going on behind the scenes, take a look at the js/utils.jsfile, particularly at the store function that begins on line 28. The function is a get-ter/setter that wraps access to the HTML5 localStorage API and makes use of theJSON.stringify() and JSON.parse() methods to handle storing and retrieving data.

Why not store structured data using Web SQL?It's a good question. Naturally, SQL would make a good fit for storing structured datasuch as the data inside the TodoMVC project. The reason that it isn't used, and whyI don't mention it in the book, is because Web SQL as a web standard is being dep-recated and hence will enter a graveyard of web standards that have been abandonedover time.

12.3.2 Porting a TodoMVC app with Electron

I'd like to say that the Electron app version is as simple, but it requires a few moresteps. First, you need to modify the package.json file for the TodoMVC React exampleso that it looks like the code in the following listing.

Listing 12.7 The package.json file for the TodoMVC React Electron app

{ "private": true, "dependencies": { "classnames": "^2.1.5", "director": "^1.2.0", "electron-prebuilt": "^1.2.5",   "react": "^0.13.3", "todomvc-app-css": "^2.0.0", "todomvc-common": "^1.0.1" }, "main":"main.js",    }

Adds Electron as dependency to list of dependencies for repo

Adds main field for app's entry point, pointing to main.js file you'll make

The modifications to the package.json file are so that you can get Electron to run theapp. Next, we'll look at implementing the main.js file that you need to make the Elec-tron app load. Create a file called main.js, and put the following code into it:

'use strict';

const electron = require('electron');const app = electron.app;const BrowserWindow = electron.BrowserWindow;

let mainWindow = null;

Summary

209

app.on('window-all-closed', () => { if (process.platform !== 'darwin') app.quit();});

app.on('ready', () => { mainWindow = new BrowserWindow(); mainWindow.loadURL(`file://${__dirname}/index.html`); mainWindow.on('closed', () => { mainWindow = null; });});

The main.js file is pretty standard and is used to load the index.html file in the Reactexample app. If you try to load the app, you'll find that the example doesn't work. Open-ing the developer tools on the app and looking at the Console Tab reveals a JavaScripterror: 'classNames' is not defined. This error is occurring in the todoItem.jsx filelocated inside the js folder of the React example folder. The classNames variable is com-ing from a Node.js module that's loaded in the index.html file as a script tag.

One way to fix this error is to require the classnames module inside the todoItem.jsxfile so you can guarantee the module is loaded by the time the React code is evaluated.In the todoItem.jsx file, add the following line of code on line 8, before the instantlyinvoked function expression:

const classNames = require('classnames');

Now, you can run the app from the command line by running this in the same direc-tory as the TodoMVC app:

electron

This will get the TodoMVC app to run. What this demonstrates is that when you port aweb app to Electron, there are a few more steps involved; but also, loading libraries inthe DOM can't be guaranteed to happen in the order you expect, so you should beaware of that.

12.4 Summary

In this chapter, we've looked at how you can go about storing data for your desktopapps. You looked at what options exist for storing your app's data, and explored usingthe HTML5 localStorage API to implement a notes app. You then explored how ver-satile NW.js and Electron are by using them to convert a web app into a desktop appthat persists its data locally.

You can store simple datasets in your desktop app using HTML5's localStorageAPI and, if needed, serialize and deserialize structured data with that too; but you'rebetter off using an embedded database for that kind of data.

Now that we've covered ways to store and retrieve data for your apps, we canexplore another element of handling data in your apps—specifically, how you get andset data from the OS clipboard.

Copying andpasting contentsfrom the clipboard

This chapter covers Accessing the clipboard in NW.js and Electron Copying text content to the clipboard Clearing the clipboard Copying Electron's other data types to the


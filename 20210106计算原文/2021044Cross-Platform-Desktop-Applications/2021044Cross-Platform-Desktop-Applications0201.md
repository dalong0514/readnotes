 Accessing the filesystem in Node.js

As developers, we often forget how lucky we are to work in an industry where thetools are readily available and free or relatively inexpensive to get ahold of. In thischapter, we'll get to grips with building desktop applications through creating a fileexplorer application. We'll look at how the app is built with both NW.js and Elec-tron so that we can compare and contrast the ways in which they approach desktopapplications.

Grab a cup of tea or coffee, a pen and paper, and settle in for some programming.

2.1 What we're going to build

Whether you use a Windows PC, a Mac, or Linux, there are a few things common toall of them—they store files organized in folders, and they all have their own takeon how to organize files in folders, as well as how you find and display those files to

31

32

CHAPTER 2 Laying the foundation for your first desktop application

the user. This isn't a problem for people who use only one OS, but those who have tolearn to use a new OS (such as when going to work at a new organization) can struggleto get their head around how to do simple tasks like rename a folder, or find outwhere the file that they saved to their computer is located.

It feels fitting to approach the idea of making a file explorer that works the same

across all OSs, so that's what we'll build: a file explorer.

2.1.1

Introducing Lorikeet, the file explorerThere's a common joke in developer circles that says naming things is the secondhard problem in computer science (caching being the first hard problem). Some-times it's nice to take inspiration from nature, so we'll name the file explorer Lori-keet, after the colorful native Australian bird.

Lorikeet is a file explorer with the following goals: Allow users to browse folders and find files Allow users to open the file(s) with their default app

These are relatively simple goals, but implementing features to support them will pro-vide enough scope to help you become familiar with building a desktop application.Building Lorikeet will also help demonstrate the different approaches that NW.js andElectron offer for developing desktop applications.

Building a desktop application is a lengthy process consisting of many steps: con-structing user journeys, creating wireframes, writing tests, fleshing out the wireframes,writing code, and making sure that the app works as intended. For the sake of learningabout NW.js and Electron, we'll work off of the basis that we have some user journeysand wireframes for the file explorer and focus on building a functional version of it.

You'll flesh out the features in the wireframes one by one, which helps to provide anatural flow to building the app, and gives you a chance to see where the code livesand what it does. Figure 2.1 shows a wireframe.

/Users/paulbjensen

Search

Lorikeet

Desktop

Documents

Downloads

Movies

Music

Pictures

Public

Work

Diary.doc

elephants.jpg

Figure 2.1Wireframe of the file explorer app you'll build

Creating the app

33

With this wireframe, you take the app and break it down into separate features, help-ing you to implement the app one feature at a time. The first feature to work on iswhere the user begins to use the app—in this case, the start screen. But before you cando that, you need to create an app to store the code in.

2.2

Creating the appAs you saw in chapter 1, it's relatively easy to get started with creating desktop applica-tions with either NW.js or Electron. Regardless of which framework you begin to buildthe app with, you'll need to have Node.js installed (a quick and simple process youcan do in a minute). To see how to install Node.js on your computer, see「InstallingNode.js」in the appendix.

Once you have Node.js installed on your computer, the next step is to install both

of the desktop application frameworks on your computer (if you haven't already).

2.2.1

Installing NW.js and Electron

If you've already installed NW.js and Electron as explained in chapter 1, please skip tosection 2.2.2. If not, you can run the following commands in the Terminal. For NW.js,run the following command to install NW.js as a global module:

npm install -g nw

For Electron, run the following command to install Electron as a global module:

npm install -g electron

Once they're installed, you can proceed to build the NW.js version of the Lorikeetapplication.

2.2.2

Creating the files and folders for the NW.js-powered app

The next step is to create a folder that will store the code for your app. Choose a loca-tion on your computer where you like to store your code work, and run the followingcommand to create a folder named lorikeet-nwjs:

mkdir lorikeet-nwjs

Once the folder (or directory, as some developers call it) is created, the next step is tocreate a package.json file for the app. This is Node.js's equivalent of a manifest file,where you store configuration information for the app. First, create the file inside theapplication folder:

cd lorikeet-nwjstouch package.json

34

CHAPTER 2 Laying the foundation for your first desktop application

Running on Windows?If so, there isn't a touch command. What you can do instead is simply create the fileusing a code editor such as Notepad++ or even GitHub's Atom.

Now that you have a package.json file that you can edit, you can use whatever text edi-tor you like to open the package.json file and insert the following code into it:

{ "name": "lorikeet", "version": "1.0.0", "main": "index.html"}

The package.json file follows the same conventions used for creating modules that arethen used in Node.js applications via npm. The name field has the name of the applica-tion, and must not contain spaces. The version field contains the version of the soft-ware, which we call 1.0.0 in accordance with a versioning format known as semanticversioning (also known as SemVer). The main field is used to tell NW.js what file to loadwhen it's booted—in this case, the index.html file. These are the minimum require-ments that NW.js has for the package.json file before it can load an application. Youhaven't yet created the web page that's loaded by NW.js, so you should probably createthat next.

The index.html file is a pretty standard example for the moment. To create it,run the following command in your command-line tool (or create the file withNotepad++/Atom in Windows):

touch index.html

Once that's done, using your favorite text editor, insert the code in the following list-ing into the index.html file.

Listing 2.1 Adding the index.html file's contents for the NW.js app

<html> <head> <title>Lorikeet</title> </head> <body> <h1>Welcome to Lorikeet</h1> </body></html>

Now that the index.html file is created, you're in a position to make NW.js run theapp. To do that, simply run the following command in the Terminal, or your Com-mand Prompt/PowerShell in Windows:

nw

Creating the app

35

This will load the NW.js app. Because no further arguments were passed to the com-mand, NW.js will inspect the files located in the current working directory where thecommand was run (in this case, the lorikeet-nwjs folder) and search for a package.jsonfile. When it finds the package.json file, it will then load that file. The package.jsonfile's main field will indicate to NW.js to load the index.html file in the app, which itthen does, and you should see the screen shown in figure 2.2.

Figure 2.2 NW.js running a bare-minimum app. The app displays the contents of the index.html file, which means it's working as expected so far. Later in the chapter, you'll replace this simple HTML with the UI that makes up the app.

The title of the app window is loaded from the value inside the <title> element inthe index.html file. You can edit the value of that field, save the change to the file, andrun the application again from the command line to see the changes.

Can I load the index.html file in a web browser?You can try, but any code that's calling out to NW.js's APIs or to Node.js code willresult in a JavaScript error, so it's best not to. Even though NW.js apps appear to berunning inside an embedded web browser, the app is more sophisticated because ithas access to both Node.js/NW.js APIs and the DOM in the same JavaScript context.

With one folder and two files in that folder, you have the main skeleton code that willget a bare-bones version of the application up and running. At this point, you can adjustthe contents of the index.html file to change the UI that's displayed by the application,but before you do any more on the NW.js version of the application, let's take a look athow you can achieve the same bare-bones application version with Electron.

2.2.3

Creating the files and folders for the Electron-powered appThe Electron version of the application starts off very much in the same fashion.You'll begin by creating a folder named lorikeet-electron. You can do this by runningthis command in the Terminal/Command Prompt:

mkdir lorikeet-electron

This will create a folder named lorikeet-electron. This is the main application folderfor the application, and inside it will be the application's files. Now you'll create the

36

CHAPTER 2 Laying the foundation for your first desktop application

next file needed by the application, the package.json file. In your terminal or via yourtext editor, create a file named package.json inside the lorikeet-electron folder:

cd lorikeet-electrontouch package.json

Once you have an empty package.json file, you'll move on to populating the file withthe configuration needed by Electron. Inside the package.json file, add the followingJSON configuration:

{ "name": "lorikeet", "version": "1.0.0", "main": "main.js"}

The package.json file looks almost identical to the package.json file used by the NW.jsversion of the application, with one exception: the main property is different. InNW.js, the file that's loaded is an HTML file. In Electron, the file that's loaded is aJavaScript file. The file you load in the case of the Electron version of the applicationis called main.js.

The main.js file is responsible for loading the Electron application and anybrowser windows that it will display as part of that application. In your terminal oryour text editor, create the file main.js and insert the following content.

Listing 2.2 The main.js file for the Electron app

'use strict';

const electron = require('electron'); const app = electron.app;const BrowserWindow = electron.BrowserWindow;

Electron is loaded via npm

let mainWindow = null;

app.on('window-all-closed',() => {     if (process.platform !== 'darwin') app.quit();});

app.on('ready', () => {       mainWindow = new BrowserWindow(); mainWindow.loadURL(`file://${app.getAppPath()}/index.html`); mainWindow.on('closed', () => { mainWindow = null; });});

When app is ready to run, tells main window to load index.html, and when that window is closed, sets mainWindow variable to null

mainWindow variable keeps application's main window in JavaScript context, so garbage collection, which would close application window, doesn't remove it

Mimics UX of Windows and Linux applications — closing only application window for app quits app; on Mac OS, closing application window doesn't close app

Creating the app

37

The main.js file will result in loading the index.html file. Here, you create the index.htmlfile and put the following contents into it:

<html> <head> <title>Lorikeet</title> </head> <body> <h1>Welcome to Lorikeet</h1> </body></html>

Once you've saved the index.html file, you're in a position to run the Electron appli-cation from the command line. Go to the Terminal or Command Prompt and type thefollowing command inside the lorikeet-electron folder to run the application:

cd lorikeet-electronelectron .

If you run the application now, you should see something like figure 2.3.

Figure 2.3 The Lorikeet app running on Electron. This is what Electron apps look like by default—pretty much like the NW.js variant.

The Electron app looks almost identical to the NW.js app. The index.html file isexactly the same as the one used for the NW.js variant of the Lorikeet app, and to loadthe application from the command line is practically the same.

Having built the Lorikeet app's bare-bones application structure in both NW.js andElectron, you can see that they share some similar coding conventions—after all, asmentioned, Cheng Zhao worked on both NW.js and Electron. But they differ in termsof how they go about loading the app.

So far, I've shown you how to build and set up the Lorikeet app's skeleton of filesand folders with both frameworks. The next stage is to start working on the first fea-ture of the application that the user sees, as shown back in figure 2.1.

We'll continue to compare and contrast the approaches taken with both frame-

works but share code where it's possible.

38

2.3

CHAPTER 2 Laying the foundation for your first desktop application

Implementing the start screenThe start screen has a number of components to it. We'll start with the display of thepersonal folder, as shown in figure 2.4.

/Us/Usersers/pa/paulbulbjenjensensen

SeaSearchrch

LorLorikeikeetet

DesDesktoktopp

DocDocumeumentsnts

DowDownlonloadsads

MovMoviesies

MusMusicic

PicPicturtureses

Public

Work

Diary.doc

elephants.jpg

Figure 2.4 The Lorikeet wireframe. Notice the circled item in the wireframe. This is the item you want to build first.

This is the first feature you'll flesh out in the UI and then implement in both versionsof the Lorikeet app.

2.3.1 Displaying the user's personal folder in the toolbar

Three parts comprise this feature:

 The HTML that makes up the toolbar and the personal folder The CSS that applies the layout and styling of the toolbar and the personal folder The JavaScript that will discover what the user's personal folder is and display it

in the UI

The good news is that the HTML, CSS, and even the JavaScript needed for this featureare exactly the same in both the NW.js and Electron versions of the Lorikeet app. Inthis case, you'll be able to show it once but use the same code in both applications.Let's start with the HTML.ADDING THE HTML FOR THE TOOLBAR AND PERSONAL FOLDERThe index.html file is the main screen for both the NW.js and Electron versions of ourapplications. For both versions of the application, open the index.html file in a texteditor and change it to what you see in the next listing.

Listing 2.3 Adding the toolbar and personal folder HTML to the index.html file

<html> <head> <title>Lorikeet</title> </head>

Implementing the start screen

39

<body>  <div id="toolbar">        <div id="current-folder"></div>  </div> </body></html>

Replaces welcome message with HTML for toolbar and personal folder

Once you've done this for both applications, we can move on to creating the CSSstylesheets that will manage the layout and styling of the toolbar and personal folder.ADDING THE CSS FOR THE TOOLBAR AND PERSONAL FOLDERStyling desktop applications is no different than styling web pages. CSS can be embed-ded inside the HTML for a page, but it's better to put it into a separate file so that youcan see all the CSS styling in one place, as well as keep the index.html file readable.

Start by creating a file in the application called app.css at the same folder level as

the index.html file. Next, add the CSS in the following listing to the app.css file.

Listing 2.4 Adding the toolbar and personal folder CSS to the app.css file

body {  padding: 0;  margin: 0;  font-family: 'Helvetica','Arial','sans';}

#toolbar {  position: absolute;  background: red;  width: 100%;  padding: 1em;}

#current-folder {  float: left;  color: white;  background: rgba(0,0,0,0.2);  padding: 0.5em 1em;  min-width: 10em;  border-radius: 0.2em;}

Now, you need to make sure that the app.css file will be loaded by the index.html file.In the index.html file, add a line to the index.html file so that it reads like the follow-ing listing.

Listing 2.5 Adding the app.css link tag to the index.html file

<html> <head> <title>Lorikeet</title> <link rel="stylesheet" href="app.css" /> </head>

Links tag that loads app.css file in index.html file

40

CHAPTER 2 Laying the foundation for your first desktop application

<body> <div id="toolbar">  <div id="current-folder"></div> </div> </body></html>

After you've saved the index.html file with this change, you can either reload theNW.js and Electron applications (if you have them open and running) or load themagain from the Terminal/Command Prompt with this:

cd lorikeet-electron && electron .cd lorikeet-nwjs && nw

Once you have reloaded the applications with the new code, you'll see that the UI isstarting to take shape, as shown in figures 2.5 and 2.6.

Figure 2.5 The Lorikeet NW.js app with the toolbar and personal folder. The personal folder listing is blank, but we'll get around to making it appear soon.

Figure 2.6 The Lorikeet Electron app with the toolbar and personal folder

The toolbar and the personal folder are visible and styled, but what remains is to beable to discover what the path for the user's personal folder is and display that in theUI. This is the next step we'll take.DISCOVERING THE USER'S PERSONAL FOLDER WITH NODE.JSTo display the path of the user's personal folder, you need a way to discover it, onethat works across all OSs. On Mac OS, the user's personal folder tends to be located inthe /Users/<username> folder with their username (mine is /Users/pauljensen). OnLinux, the user's personal folder tends to be in the /home/<username> folder, andon Windows 10 the it's located in the C: drive under the Users/<username> folder. Ifonly OSs operated in a common, standard fashion!

Thankfully, this is accommodated in Node.js's ecosystem on npm packages. Annpm module called osenv by Isaac Schlueter (former Node.js lead maintainer and thefounder of npm) has a function that discovers and returns the user's personal folder

Implementing the start screen

41

(or home folder, as it's also known). To use this, you need to install the npm modulein the application. Run the following command in the Terminal or Command Promptto install the library (make sure to do this for both versions of the Lorikeet app):

npm install osenv --save

The –-save flag at the end of the command tells the npm command to add the moduleas a dependency in the package.json manifest file. If you open the package.json mani-fest file (say, in this case, for the NW.js variant of the application), you'll see thechange, as shown next.

Listing 2.6 The modified package.json file

{ "name": "lorikeet", "version": "1.0.0", "main": "index.html", "dependencies": {    "osenv": "^0.1.3" }}

The new dependencies property, with osenv listed as module dependency for app

You'll also notice that there's a new folder that appears in the application folders forboth applications, a folder called node_modules. This folder contains any locallyinstalled npm modules that are installed for the application. If you browse thenode_modules folder, you'll see a folder named osenv. This is where the osenv mod-ule's code has been installed.

With the osenv module installed, you now want to load the user's personal folderand display it in the personal folder UI element in the index.html file. This demon-strates one of the unique aspects of NW.js and Electron as Node.js desktop applicationframeworks: you can execute Node.js code directly in the index.html file. Don't believeme? Try this. Modify the index.html file so that the code looks like the next listing.

Listing 2.7 Displaying the user's personal folder to the index.html file

<html> <head> <title>Lorikeet</title> <link rel="stylesheet" href="app.css" /> </head> <body> <div id="toolbar">  <div id="current-folder">  <script>         document.write(require('osenv').home());  </script>  </div> </div> </body></html>

Loads osenv module via Node.js's require function, then calls the home function on the library, and the resulting value is written into the DOM by document.write

42

CHAPTER 2 Laying the foundation for your first desktop application

Make sure the index.html file is changed to this in both the NW.js and Electron ver-sions of the Lorikeet app.

After you save the files, reload the applications using the technique shown earlier:

cd lorikeet-electron && electron .cd lorikeet-nwjs && nw

You can expect to see your personal folder listed in the personal folder UI element ofthe app, as shown in figures 2.7 and 2.8.

Figure 2.7 The user's personal folder displayed in the Lorikeet NW.js app

Figure 2.7 is impressive. You can call Node.js directly in a script tag in the index.htmlfile. How about Electron? Does it do the same? Check out figure 2.8.

Figure 2.8 The user's personal folder displayed in the Lorikeet Electron app

It does. Not only have you been able to call Node.js code inside a script tag in theindex.html file, but you've been able to use a Node.js module from npm in the front-end part of your code. Plus, you've been able to use identical code across both NW.jsand Electron so far, which goes to show how compatible they are, as well as why someprojects have been so successful in being ported from NW.js to Electron (such as LightTable, for example).

Now that you've implemented the display of the user's personal folder in the tool-bar, we should move on to implementing the next feature in the UI: the display of theuser's files and folders in their personal folder.

2.3.2

Showing the user's files and folders in the UIIn the preceding section, we started off by creating the UI elements first and thenpopulated the user's personal folder path in the UI element. For this feature, we'llwork on getting ahold of a list of the user's files and folders first and then figure outfrom there how we display them in the UI of the application. For a quick reminder,figure 2.9 shows the UI element we're looking to implement.

Implementing the start screen

43

/Users/paulbjensen

Search

Lorikeet

Desktop

Documents

Downloads

Movies

Music

Pictures

Public

Work

Diary.doc

elephants.jpg

Figure 2.9 The UI element we're looking to implement next in the app

To implement this UI feature, you need to do the following:

1 Get the list of files and folders at the user's personal folder path2 For each file/folder listing, find out if it's a file or a folder3 Pass that list of files/folders to the UI to be rendered as files with icons

You already have a way to get at the user's personal folder path. Now what you need isa way to get ahold of the list of files and folders at that path. Luckily for you, Node.jsimplements a standard library for querying the computer's filesystem, called fs. Oneof the functions available to get a list of files and folders is the readdir function, asdocumented at http://mng.bz/YR5B.

For both the NW.js and Electron versions of the Lorikeet app, you'll create anapp.js file. This file will contain JavaScript code that can call Node.js as well as interactwith the DOM. You'll use this file to help store the code that will display the list of filesfor you.

First, create an app.js file at the same folder level as the index.html and app.cssfiles. Next, you'll move the code that loads the user's personal folder path into it. Addthe following code to the app.js file:

'use strict';

const osenv = require('osenv');

function getUsersHomeFolder() { return osenv.home();}

After adding the code to the app.js file, the next step is to include the app.js file as ascript tag in the index.html and call the getUsersHomeFolder method in the DOM in

44

CHAPTER 2 Laying the foundation for your first desktop application

place of the current call to the osenv module's home function. Change the index.htmlfile so that it looks like the next listing.

Listing 2.8 Adding the app.js file to the index.html file

<html> <head> <title>Lorikeet</title> <link rel="stylesheet" href="app.css" /> <script src="app.js"></script>    </head> <body> <div id="toolbar">  <div id="current-folder">  <script>   document.write(getUsersHomeFolder());   </script>  </div> </div> </body></html>

Includes app.js as script tag in index.html

Calls app.js's getUsersHomeFolder function in place of direct call to Osenv module's home function

If you reload the applications, you'll see that they behave the same, which is exactlywhat you want. You can now start to add code to the app.js file for getting the list ofthe files. You'll start by requiring Node.js's filesystem module, which comes as partof Node.js's standard library, and then adding a new function called getFilesIn-Folder that will retrieve the files in the folder passed to it. After that, you'll create afunction called main that will pass the user's personal folder into that function, andfrom the resulting list of files log the absolute paths for them out in the console.

Change the code in the app.js file so that it looks like the following.

Listing 2.9 Logging the list of files and folders in the user's personal folder

'use strict';

const fs = require('fs');    const osenv = require('osenv');

Node.js's fs module loads in the app

function getUsersHomeFolder() { return osenv.home(); }

function getFilesInFolder(folderPath, cb) {  fs.readdir(folderPath, cb); }

Simple wrapper around the fs.readdir function for getting list of files

function main() {         const folderPath = getUsersHomeFolder(); getFilesInFolder(folderPath, (err, files) => {  if (err) {             return alert('Sorry, we could not load your home folder');  }

Function that combines user's personal folder path with getting its list of files

Simplemessageto displayin caseof errorloadingfolder'sfiles

Implementing the start screen

45

files.forEach((file) => {  console.log(`${folderPath}/${file}`);  }); }); }

main();

For each file in list, logs full path for file to console

After saving the app.js file, the next step is to see what happens when you run thecode. Reload the application. In the case of Electron, if you toggle showing the devel-oper tools for the application, you can expect to see the list of files in the Console tab,as shown in figure 2.10.

Figure 2.10 The Lorikeet Electron app showing the list of files being logged to the Console tab. To see the list of files on your computer, click View > Toggle Developer Tools.

You now know that you can get at the list of files in the user's personal folder. The nextchallenge is to figure out what the name and file/folder type is for each file in the listand to then display these items in the UI as a list of files and folders with icons.

Your goal is to be able to take a list of files and pass them through another functionin Node.js's file system API. This will identify whether they're files or directories, aswell as what their names and full file paths are. Do the following:

1 Use the fs.stat function method, as documented at http://mng.bz/46U5.2 Use the async module to handle calling a series of asynchronous functions and

collecting their results.

3 Pass the list of results to another function that will handle their display.

46

CHAPTER 2 Laying the foundation for your first desktop application

In the app.js file for both variants of the Lorikeet app, install the async module via theTerminal or Command Prompt:

npm install async --save

After installing the async module to both applications, the next step is to change theapp.js code so that it will detect what the files in the user's personal folder are. Changethe code to that shown next.

Listing 2.10 Changing the app.js code to detect file types

'use strict';

const async = require('async');  const fs = require('fs'); const osenv = require('osenv'); const path = require('path');

Includes async and path Node.js modules into app

function getUsersHomeFolder() { return osenv.home(); }

function getFilesInFolder(folderPath, cb) { fs.readdir(folderPath, cb); }

function inspectAndDescribeFile(filePath, cb) {  let result = {  file: path.basename(filePath),  path: filePath, type: '' }; fs.stat(filePath, (err, stat) => {   if (err) {  cb(err);  } else {  if (stat.isFile()) {   result.type = 'file';  }  if (stat.isDirectory()) {   result.type = 'directory';  }  cb(err, result);  } }); }

function inspectAndDescribeFiles(folderPath, files, cb) { async.map(files, (file, asyncCb) => {        let resolvedFilePath = path.resolve(folderPath, file);  inspectAndDescribeFile(resolvedFilePath, asyncCb); }, cb); }

function displayFiles(err, files) {       if (err) {  return alert('Sorry, we could not display your files'); }

Uses path module to get name for file

fs.stat call supplies an object you can query to find out file's type

Uses async module to call asynchronous function and collects results together

Creates displayFiles function to be end point where files will end up being displayed

Implementing the start screen

47

files.forEach((file) => { console.log(file); }); }

function main() { let folderPath = getUsersHomeFolder(); getFilesInFolder(folderPath, (err, files) => {  if (err) {  return alert('Sorry, we could not load your home folder');  }  inspectAndDescribeFiles(folderPath, files, displayFiles); }); }

main();

With the app.js file saved to the computer and the applications reloaded, you'll seesomething like figure 2.11 in the developer tools.

Not only do you now have the application returning the list of files in the user'spersonal folder, but you have it in a data structure that has the filename and file typeincluded as well. This sets you up perfectly for the next step in implementing the UIfeature: displaying filenames and icons in the application's UI.

Figure 2.11 The files list in the Console tab of the Developer Tools. Notice how the first expanded object has the type file, and the second expanded object has the type directory.

48

CHAPTER 2 Laying the foundation for your first desktop application

VISUALLY DISPLAYING THE FILES AND FOLDERSIn the previous code for the app.js file, you created a function called displayFiles.You want to use this function to handle displaying the files as names and icons in theUI. Because there are many files to be rendered in the UI, you'll use an HTML tem-plate for each file and then render an instance of that template to the UI.

You'll start by adding the HTML template to the index.html file, as well as a divelement to contain the files that are being displayed. Change the index.html file sothat it looks like the following listing.

Listing 2.11 Adding the file template and main area to the index.html file

<html> <head> <title>Lorikeet</title> <link rel="stylesheet" href="app.css" /> <script src="app.js"></script> </head> <body> <template id="item-template">   <div class="item">  <img class="icon" />  <div class="filename"></div>  </div> </template> <div id="toolbar">  <div id="current-folder">  <script>   document.write(getUsersHomeFolder());  </script>  </div> </div>  <div id="main-area"></div>  </body></html>

Adds template HTML element to index.html

Adds a div element with ID "main-area" to be holder for the files

The purpose of the template element is to hold a copy of the HTML that you'd liketo render for each file, and the div element is where the template instances will berendered and stored for each file that you find in the user's personal folder. You'llthen add some JavaScript to the app.js file that will handle creating an instance ofthe template and adding it to the UI. Adjust the app.js file so that the code readslike the next listing.

Listing 2.12 Rendering the template instances in the UI via the app.js file

'use strict';

const async = require('async');const fs = require('fs');const osenv = require('osenv');const path = require('path');

Implementing the start screen

49

function getUsersHomeFolder() { return osenv.home();}

function getFilesInFolder(folderPath, cb) { fs.readdir(folderPath, cb);}

function inspectAndDescribeFile(filePath, cb) { let result = {file: path.basename(filePath),path: filePath, type: '' }; fs.stat(filePath, (err, stat) => { if (err) {  cb(err); } else {  if (stat.isFile()) {  result.type = 'file';  }  if (stat.isDirectory()) {  result.type = 'directory';  }  cb(err, result); } });}

function inspectAndDescribeFiles(folderPath, files, cb) { async.map(files, (file, asyncCb) => { let resolvedFilePath = path.resolve(folderPath, file); inspectAndDescribeFile(resolvedFilePath, asyncCb); }, cb);}

Adds new function called displayFile that handles rendering template instance

function displayFile(file) {         const mainArea = document.getElementById('main-area'); const template = document.querySelector('#item-template'); let clone = document.importNode(template.content, true);   clone.querySelector('img').src = `images/${file.type}.svg`;  clone.querySelector('.filename').innerText = file.file;   mainArea.appendChild(clone);       }

Creates copy of template instance

Alters instance to include file's name and icon

Appends template instance to "main-area" div element

function displayFiles(err, files) { if (err) { return alert('Sorry, we could not display your files'); } files.forEach(displayFile);   }

Passes files to the displayFile function in the displayFiles function

function main() { let folderPath = getUsersHomeFolder(); getFilesInFolder(folderPath, (err, files) => { if (err) {  return alert('Sorry, we could not load your home folder'); }

50

CHAPTER 2 Laying the foundation for your first desktop application

inspectAndDescribeFiles(folderPath, files, displayFiles); });}

main();

Now that HTML is being added to the app to handle the display of the files and thefolders in the application, you want to make sure that the list of files and folders lookstyled and are displayed in a grid fashion. In the app.css file, change the CSS to matchthe following code.

Listing 2.13 Adding styling to the app.css file for displaying the files

body {  padding: 0;  margin: 0;  font-family: 'Helvetica','Arial','sans';}

#toolbar {  top: 0px;  position: fixed;  background: red;  width: 100%;  z-index: 2;}

#current-folder {  float: left;  color: white;  background: rgba(0,0,0,0.2);  padding: 0.5em 1em;  min-width: 10em;  border-radius: 0.2em;  margin: 1em;}

#main-area {  clear: both;  margin: 2em;  margin-top: 3em;  z-index: 1;}

.item {  position: relative;  float: left;  padding: 1em;  margin: 1em;  width: 6em;  height: 6em;  text-align: center;}

.item .filename {  padding-top: 1em;  font-size: 10pt;}

Implementing the start screen

51

This CSS will ensure that the items are displayed in a clear and grid-like fashion andthat the toolbar will remain in a fixed position, visible above the files in the app as themain area div element is scrolled by the user.

You're almost there. All that's left to do is add the icons for the different file typesto the application folder. Create a folder called images in the application folders withthese commands in either the Terminal or the Command Prompt:

cd lorikeet-electronmkdir imagescd ../lorikeet-nwjsmkdir images

Now, you can add some images for the file and directory icons. Inside the imagesfolder, you'll insert two images named file.svg and directory.svg. The files are sourcedfrom the OpenClipArt.org site from these URLs:

 https://openclipart.org/detail/137155/folder-icon https://openclipart.org/detail/83893/file-icon

Save the files in the images folder (under the names file.svg for the file icon and direc-tory.svg for the folder icon) and reload the application, and you should see somethinglike figures 2.12 and 2.13.

Figure 2.12 The Lorikeet NW.js app showing the files and folders. Here, you see the beginnings of what looks like a file explorer application.

52

CHAPTER 2 Laying the foundation for your first desktop application

The file type property of the files is used to determine whether the icon is for a file orfor a directory. This helps you easily distinguish files from folders. You'll also see thatthe file/folder names are displayed in alphanumerical order. In figure 2.12, dotfilesand hidden folders can be seen that would otherwise be hidden by other file explorerapplications. Figure 2.13 shows the Electron Lorikeet app.

Figure 2.13 The Lorikeet Electron app showing files and folders

2.4

The Electron variant of the Lorikeet app looks almost identical to the NW.js version.All in all, the results look good, and that's the end of the exercise for this chapter.

SummaryIn this chapter, you began using NW.js and Electron for building the type of applicationthat many people use with their computers on a daily basis. You've walked throughthe process of creating the applications from scratch and understand how you canapproach the task of building an application feature-by-feature. Here are some of thethings the chapter covered:

 The best way to approach a wireframe is to tackle it one feature at a time. Good semantics is encouraged as a way to relate features to the underlying code

that supports it.

Summary

53

 CSS is the prime way to style UI elements in NW.js and Electron desktop apps. You can use Node.js and other third-party libraries with ease in your desktop

application.

 The approaches of NW.js and Electron allow for them to use almost the samecode, but Electron requires a bit more code and a slightly different configura-tion in the package.json file.

What's been great is that in using the same code across both NW.js and Electron vari-ants of the Lorikeet app, you've been able to see how similar the desktop applicationframeworks are, as well as notice the areas where they're different. This should giveyou the confidence that should you choose one framework for your application andfind that it's not the right one for you, then it won't be too difficult to switch to usingthe other framework.

Another takeaway here is that you're able to use the same skills for building web-sites as for creating the UI for a desktop application, and that means getting up tospeed quickly when building a desktop application.

In the next chapter, we'll expand on the work done here by adding the meaty partsof the application. We'll begin to explore the APIs of NW.js and Electron to add fea-tures such as browsing through folders, searching the files and folders by name, andopening files.

Building your firstdesktop application

This chapter covers Opening files from the file explorer Accessing the filesystem Refactoring code using Node.js's module

functionality


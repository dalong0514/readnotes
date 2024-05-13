clipboard

Copying data from one source and using it in another is a function that's prettystandard with today's apps. Some utility apps add value to this functionality by auto-matically copying screenshots to the clipboard, or keeping track of multiple dataitems that are copied to the clipboard.

In this chapter, we'll look at how NW.js and Electron enable you to use the OS'sclipboard to copy and paste content, as well as how to clear the clipboard (a goodpractice, especially when copying/pasting sensitive data).

By the end of the chapter, you'll have a good understanding of how to access

and alter the user's clipboard.

210

Accessing the clipboard

211

13.1 Accessing the clipboard

Copying and pasting from the OS clipboard improves the UX by taking a manual stepout of the user journey. Take, for example, the password manager app 1Password byAgileBits. When you enter your password in a website login, the app automaticallycopies the password to your clipboard for pasting into the password field of the loginform the next time you log in.

The clipboard APIs in Electron and NW.js allow you to store and retrieve text-based data to and from the clipboard. To illustrate how this works, you'll build a verysimple app that lists a number of common phrases, film quotes, and things you mightwant to type into a chat window, and saves some nuggets that you want to keep forlater. You'll call it Pearls.

If you want to have a look at premade versions of these apps, the NW.js and Elec-tron versions of the app are available in the pearls-nwjs app in the book's GitHubrepository at http://mng.bz/4V2D. You can download the code and run it per theinstructions, or if you prefer to see how the app is made from scratch, read on.

13.1.1 Creating the Pearls app with NW.js

You'll start by creating a folder called pearls-nwjs to store the app's files. Then, add thepackage.json file. In your text editor, create the package.json file and add the follow-ing content to it:

{ "name":"pearls", "version":"1.0.0", "main":"index.html", "window": { "width": 650, "height": 550, "toolbar": false }, "scripts": { "start": "node_modules/.bin/nw ." }, "dependencies": { "nw": "^0.15.3" }}

The package.json file is much like the package.json for other NW.js apps, with theonly unique bits being the window width and height properties. Next, implementthe index.html file, and put the following code into it:

<html> <head> <title>Pearls</title> <link href="app.css" rel="stylesheet" /> <script src=" app.js"></script> </head>

212

CHAPTER 13 Copying and pasting contents from the clipboard

<body> <template id="phrase">  <div class="phrase"

onclick="copyPhraseToClipboard(this.innerText);"></div>

</template> <div id="phrases"></div> </body></html>

The index.html file does a few things: It loads an app stylesheet as well as an app.js filefor loading the phrases and copying them into the clipboard. It then also contains atemplate tag for the phrase, used for each phrase you want to display in the app win-dow. The following listing shows the CSS for the Pearls app.

Listing 13.1 The app.css file for the Pearls NW.js app

body { padding: 0; margin: 0; background: #001203;}

#phrases { padding: 0.5em;}

.phrase { float: left; padding: 1em; margin: 1em; border-radius: 12px; border: solid 1px #ccc; font-family: 'Helvetica Neue', 'Arial' 'Sans-Serif'; font-style: italic; width: 9em; min-height: 7em; text-align: center; color: #fff;}

.phrase:hover { cursor: pointer; background: #1188de;}

The CSS for the app is designed so that the app has a dark background, and thephrases are highlighted against that dark background with white text surrounded by awhite border. When a phrase is hovered over, the background color of that phraseturns blue.

Next, load the app.js file, shown here.

Accessing the clipboard

213

Listing 13.2 The app.js file for the Pearls NW.js app

'use strict';

const gui = require('nw.gui');const clipboard = gui.Clipboard.get();  const phrases = require('./phrases');     let phrasesArea;let template;

Loads example phrases to use in app

Loads NW.js's Clipboard API through NW.gui module

function addPhrase (phrase) {           template.content.querySelector('div').innerText = phrase; let clone = window.document.importNode(template.content, true); phrasesArea.appendChild(clone);}

Adds a phrase to app window

Function loads phrases from phrases.js file into app window

function loadPhrasesInto () {         phrasesArea = window.document.getElementById('phrases'); template = window.document.querySelector('#phrase'); phrases.forEach(addPhrase);}

function copyPhraseToClipboard (phrase) {  clipboard.set(phrase, 'text');}

When phrase is clicked, function is triggered to copy phrase into clipboard

window.onload = loadPhrasesInto;

When app is done loading HTML, triggers loading phrases

The key bit of the app is the function copyPhraseToClipboard, which uses the clip-board API to set a value to the clipboard—in this case, the phrase that was clicked.The phrases.js file contains a list of quotes from various films like Kindergarten Cop andothers (I'll let you figure out the rest). Here's the list of phrases:

'use strict';

module.exports = [ 'I have to return some videotapes', 'Do not attempt to grow a brain', 'So tell me, do you feel lucky? Well do ya, Punk!', 'We\'re gonna need a bigger boat', 'We can handle a little chop', 'Get to the choppa!', 'Hold onto your butts', 'Today we\'re going to play a wonderful game called "Who is your daddy, and

what does he do?"',

'Yesterday we were an army without a country. Tomorrow we must decide...

which country we want to buy!'

];

The phrases.js file exports a list of strings that are movie quotes from various films.That list is then loaded by the app.js file into the app window.

Now, you can run the app with npm start, and you should see an app that looks

like figure 13.1.

214

CHAPTER 13 Copying and pasting contents from the clipboard

Figure 13.1 The Pearls app running with NW.js on Microsoft Windows 10

What content can I store and retrieve from the clipboard?NW.js currently only allows text-based content to be stored and retrieved from the OSclipboard—unfortunately, images can't be accessed or stored. It is hoped that othercontent types will be able to be stored and accessed from the clipboard in the future,but for now text will have to do.

If you want to get/set other types of content to the clipboard, you may be better offgoing with Electron because that has support for other data types.

If you wanted to access the contents of the clipboard (say you had a quotation from aweb page that you copied to the clipboard but hadn't pasted anywhere), you could dothat by using the following line of code in your app:

let copiedText = clipboard.get('text');

Accessing the clipboard

215

This can be useful in cases where you want to automatically record copied content (suchas for a note-taking app where content is being copied out of pages and documents).Sometimes you want the clipboard cleared (such as when it's used to store sensitiveinformation). To do that, call this line on the API:

clipboard.clear();

The clipboard API offers the ability to store and retrieve text-based content from theOS clipboard, but if you need to work with other data (such as files), then you mightstill be in luck.

What does the clipboard API in Electron look like in comparison?

13.1.2 Creating the Pearls app with Electron

The Pearls app Electron example's source code can be found in the pearls-electronapp folder in the book's GitHub repository.

The app's code is similar to that of the Pearls app NW.js example, with the excep-tions of the package.json file, the app.js file, and the main.js file required by Electronto load an app. The next listing shows the package.json file for this app.

Listing 13.3 The package.json file for the Pearls Electron app

{ "name": "pearls-electron", "version": "1.0.0", "description": "A clipboard API example for Electron and the book 'Cross

Platform Desktop apps'",

"main": "main.js", "scripts": { "start": "node_modules/.bin/electron .", "test": "echo \"Error: no test specified\" && exit 1" }, "keywords": [ "electron", "clipboard" ], "author": "Paul Jensen <paulbjensen@gmail.com>", "license": "MIT", "dependencies": { "electron ": "^1.3.7" }}

The package.json file is generated by running npm init from the command line and ismodified slightly to include the Electron npm dependency, as well as the start com-mand so that you can run npm start to make the app boot. It also loads the main.jsfile as the Electron app's first entry point. The code for the main.js file is shown next.

216

CHAPTER 13 Copying and pasting contents from the clipboard

Listing 13.4 The main.js file for the Pearls Electron app

'use strict';

const electron = require('electron');const app = electron. app;const BrowserWindow = electron.BrowserWindow;

let mainWindow = null;

app.on('window-all-closed', () => { if (process.platform !== 'darwin') app.quit();});

app.on('ready', () => { mainWindow = new BrowserWindow({ width: 670, height: 550, useContentSize: true }); mainWindow.loadURL(`file://${__dirname}/index.html`); mainWindow.on('closed', () => { mainWindow = null; });});

The main.js file loads a standard app window with a specific width and height so youcan display the phrases in a 3 x 3 grid initially, as well as ensure that the app windowsize is based on the size of the content window.

The index.html, app.css, and phrases.js files are identical to the NW.js equivalentof the app, so there's no point repeating those here. What is different, though, is howthe clipboard API methods are called in Electron, which you can see in the app.js file.

Listing 13.5 The app.js file for the Pearls Electron app

'use strict';

const electron = require('electron');const clipboard = electron.clipboard;  const phrases = require('./phrases');let phrasesArea;let template;

Loads Electron's clipboard API

function addPhrase (phrase) { template.content.querySelector('div').innerText = phrase; let clone = window.document.importNode(template.content, true); phrasesArea. app endChild(clone);}

function loadPhrasesInto () { phrasesArea = window.document.getElementById('phrases'); template = window.document.querySelector('#phrase'); phrases.forEach(addPhrase);}

function copyPhraseToClipboard (phrase) { clipboard.writeText(phrase);    }

Make3 call to clipboard API to write some text to clipboard

window.onload = loadPhrasesInto;

Accessing the clipboard

217

Figure 13.2 Pearls running with Electron on Windows 10. The app looks almost identical to the one shown in figure 13.1, with the exception of the toolbar and the app icon.

If you run the app via npm start, you'll see the app looking like figure 13.2.

The way in which you access the clipboard from Electron follows a semantic nam-ing convention of read and write. In the app.js file for the Pearls app, the call to putsome text content in the clipboard is clipboard.writeText. To read the content inthe clipboard, you can make the following code call:

const content = clipboard.readText();

To clear the clipboard's content, you can make an identical function call to the clip-board API:

clipboard.clear()

The API method call is identical to the one used in NW.js—another signal of howmuch the two frameworks share in common. That said, Electron has evolved more

218

CHAPTER 13 Copying and pasting contents from the clipboard

API methods that allow it to do more than copy and paste text from the clipboard, asyou'll see in the next section.

13.1.3 Setting other types of content to the clipboard with Electron

Unlike NW.js, Electron allows you to put RTF, HTML, and even images on the clip-board. The API methods follow the same patterns as the readText and writeTextfunctions that the clipboard API exposes. We'll briefly walk through some of them,but to read more, see the API documentation at http://electron.atom.io/docs/api/clipboard/.

The clipboard API has methods for the following content types: Text HTML Images RTF

Calling the API methods from the clipboard API looks like this:

const electron = require('electron');const clipboard = electron.clipboard;

let image = clipboard.readImage();let richText = clipboard.readRTF();let html = clipboard.readHTML();

clipboard.writeImage(image);clipboard.writeRTF(richText);clipboard.writeHTML(html);

Here, you can see the pattern of read/write for getting content from the clipboard aswell as setting content to it.

13.2 Summary

In this chapter, we worked through an app that copied movie quotes into the user'sclipboard, and explored the API methods available to the developer for copying text-based and other types of data into the clipboard.

The key takeaway from this chapter is that you can only copy and paste text-basedcontent with the clipboard API in NW.js, but Electron can handle multimedia contentlike images and RTF.

In chapter 14, we'll take a look at how the various desktop app frameworks goabout implementing keyboard shortcuts. We'll make it fun by putting them into awell-known 2D game called Snake.

Binding onkeyboard shortcuts

This chapter covers Learning how NW.js and Electron work with

keyboard shortcuts


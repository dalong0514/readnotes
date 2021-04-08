 Implementing search features in the desktop app

Building an app is a journey of creating an initial skeleton of the app and progres-sively adding to the skeleton until it begins to resemble a complete product. Themoment when the product comes alive with features is often, for me, the moment Iget excited, and in this chapter those moments shall arrive.

In chapter 2, you began a journey of building a file explorer called Lorikeet andgot to a stage where you had the UI for a working desktop application. In this chap-ter, you'll continue that journey and add features that will result in a file explorerapp you can call a minimally viable product.

The goal is that not only will you have made the app's features by the end of thechapter, but you'll understand exactly how Electron and NW.js let you do that. Theprocess will give you enough experience to start using those desktop app frame-works in other places as well. Chances are, your mind will open up with lots of ideas

54

Exploring the folders

55

for things you can do that you didn't know how to do before. Excited? Good! Get com-fortable and settle in for round two.

3.1

Exploring the foldersThe main ingredients for making this happen are now in place: the files and foldersfor a given path can now be displayed visually in the window. Next you need to buildthe functionality so that when the user double-clicks a folder in the main area, the appnavigates to that folder and displays its contents in the main area.

3.1.1 Refactoring the code

If you look at the app.js file now, you'll notice that it's beginning to look a bit mud-dled, and at this point it's worth refactoring the code so that it doesn't become over-whelming and difficult to manage. Refactoring the file requires organizing the codeinto logical groups, as shown in figure 3.1.

Before

After

app.js

app.js

fileSystem.js

userInterface.js

Figure 3.1 You'll start breaking out the code into logical groups of functionality so that the code is more readable and easier to work with.

In figure 3.1, the app.js file will be turned into three files. There will still be an app.jsfile as the main entry point for the front-end code, but there will also be two otherfiles. The fileSystem.js file will contain code that handles interacting with the files andfolders on the user's computer, and the userInterface.js file will hold functions thathandle UI interactions. These are two distinct logical groups, and they will allow youto keep the code orderly.

Create two files in the Lorikeet folder at the same level as the app.js file: fileSys-

tem.js and userInterface.js. In the fileSystem.js file, insert the code shown here.

Listing 3.1 The code for the fileSystem.js file

'use strict';

const async = require('async');const fs = require('fs');const osenv = require('osenv');const path = require('path');

56

CHAPTER 3 Building your first desktop application

function getUsersHomeFolder() { return osenv.home();}

function getFilesInFolder(folderPath, cb) { fs.readdir(folderPath, cb);}

function inspectAndDescribeFile(filePath, cb) { let result = { file: path.basename(filePath), path: filePath, type: '' }; fs.stat(filePath, (err, stat) => { if (err) {  cb(err); }  else {  if (stat.isFile()) {  result.type = 'file';  }  if (stat.isDirectory()) {  result.type = 'directory';  }  cb(err, result); } });}

function inspectAndDescribeFiles(folderPath, files, cb) { async.map(files, (file, asyncCb) => { let resolvedFilePath = path.resolve(folderPath, file); inspectAndDescribeFile(resolvedFilePath, asyncCb); }, cb);}

module.exports = { getUsersHomeFolder, getFilesInFolder, inspectAndDescribeFiles};

The fileSystem.js file contains the getUsersHomeFolder, getFilesInFolder, inspect-AndDescribeFile, and inspectAndDescribeFiles functions from the app.js file. Theextra bit of code at the bottom exposes some of the functions that need to be accessedby other files through the use of the module.exports function call, a CommonJSJavaScript convention for exposing public code items in libraries. This is an importantfactor in the way you organize and make your code usable across multiple projects.

In the userInterface.js file, insert the code shown in the following listing.

Listing 3.2 The code for the userInterface.js file

'use strict';

let document;

function displayFile(file) { const mainArea = document.getElementById('main-area'); const template = document.querySelector('#item-template');

Exploring the folders

57

let clone = document.importNode(template.content, true); clone.querySelector('img').src = `images/${file.type}.svg`; clone.querySelector('.filename').innerText = file.file; mainArea.appendChild(clone);}

function displayFiles(err, files) { if (err) { return alert('Sorry, you could not display your files'); } files.forEach(displayFile);}

function bindDocument (window) { if (!document) { document = window.document; }}

module.exports = { bindDocument, displayFiles };

displayFiles function is public function exposed by userInterface.js module

Here, you expose the bindDocument and displayFiles functions in the code. ThebindDocument function is used to pass the window.document context to the user-Interface.js file—otherwise, the file will not be able to access the DOM in the NW.jsvariant of the app (Electron is unaffected). The displayFiles function is used todisplay all the files, and because there's no need to call the displayFile functionseparate from the displayFiles function, you don't expose the displayFile func-tion as a public API.

Now that the code that was in the app.js file has been moved into the fileSystem.js

and userInterface.js files, you can replace the app.js file with the code shown here.

Listing 3.3 The code for the app.js file

'use strict';

const fileSystem = require('./fileSystem');const userInterface = require('./userInterface');

function main() { userInterface.bindDocument(window); let folderPath = fileSystem.getUsersHomeFolder(); fileSystem.getFilesInFolder(folderPath, (err, files) => { if (err) {  return alert('Sorry, you could not load your home folder'); } fileSystem.inspectAndDescribeFiles(folderPath, files,

userInterface.displayFiles);

});}

main();

58

CHAPTER 3 Building your first desktop application

The app.js file is now 17 lines of code and is much more readable. Here, you can seethat there are two Node.js modules included in the code (fileSystem and userInterface),and that the main function is identical to how it was in the app.js file, with the excep-tion of calling functions from the Node.js modules instead.

The last change left is to alter the index.html file so that the function that calls theuser's personal folder is calling the fileSystem file module. Change the index.html fileso that it looks like the following code.

Listing 3.4 Changes for the index.html file

<html> <head> <title>Lorikeet</title> <link rel="stylesheet" href="app.css" /> <script src="app.js"></script> </head> <body> <template id="item-template">  <div class="item">  <img class="icon" />  <div class="filename"></div>  </div> </template> <div id="toolbar">  <div id="current-folder">  <script>   document.write(fileSystem.getUsersHomeFolder());  </script>  </div> </div> <div id="main-area"></div> </body></html>

Save the changes to the files. The refactoring is almost complete. The next featureyou want to add is the ability to navigate folders by double-clicking them in the fileexplorer.

3.1.2 Handling double-clicks on folders

One of the common features of using a file explorer is navigating folders by double-clicking the folder icon. You'll add this functionality to the Lorikeet app.

When you double-click a folder, the UI of the app updates so that the following

things happen:

 The current folder changes to that of the folder that's clicked. The files that were displayed in the file explorer are updated to show the files

for the folder path that was clicked.

 When you click another folder, the same behavior occurs again.

Exploring the folders

59

You also want to make sure that double-clicking a folder behaves as you expect, andthat double-clicking a file opens that file in its default application. To achieve that,you'll do the following:

 Create a function in the userInterface.js file called displayFolderPath, which

will update the current folder path displayed in the UI.

 Add another function in the userInterface.js file called clearView, which will

remove the files and folders that are currently displayed in the main area.

 Create a function called loadDirectory, which will handle querying the com-puter for the files and folders at a given folder path and then display the files andfolders in the main area. This code is effectively moved out of the app.js file.

 Alter the displayFile function so that it attaches an event listener to a folder

icon to trigger loading that folder.

 Change the app.js file so that it calls the loadDirectory function of the user-

Interface.js file.

 Remove the script tag inside the current-folder element in the index.html

file, because it's no longer needed.

In the userInterface.js file, change the code to look like the next listing.

Listing 3.5 Changing the userInterface.js file

'use strict';

let document;const fileSystem = require('./fileSystem');

Adds fileSystem module to use its APIs

function displayFolderPath(folderPath) {       document.getElementById('current-folder').innerText = folderPath;}

Adds function to display current folder

function clearView() {           const mainArea = document.getElementById('main-area'); let firstChild = mainArea.firstChild; while (firstChild) { mainArea.removeChild(firstChild); firstChild = mainArea.firstChild; }}

Clears items out of main-area div element

loadDirectory changes current folder path and updates main area

function loadDirectory(folderPath) {    return function (window) { if (!document) document = window.document; displayFolderPath(folderPath); fileSystem.getFilesInFolder(folderPath, (err, files) => {  clearView();  if (err) {  return alert('Sorry, you could not load your folder');  }  fileSystem.inspectAndDescribeFiles(folderPath, files, displayFiles); }); };}

60

CHAPTER 3 Building your first desktop application

function displayFile(file) { const mainArea = document.getElementById('main-area'); const template = document.querySelector('#item-template'); let clone = document.importNode(template.content, true); clone.querySelector('img').src = `images/${file.type}.svg`;

if (file.type === 'directory') {      clone.querySelector('img')  .addEventListener('dblclick', () => {  loadDirectory(file.path)();  }, false); }

Adds double-click event listener to icon if it's for a directory

clone.querySelector('.filename').innerText = file.file; mainArea.appendChild(clone);}

function displayFiles(err, files) { if (err) { return alert('Sorry, you could not display your files'); } files.forEach(displayFile);}

function bindDocument (window) { if (!document) { document = window.document; }}

Makes sureloadDirectory functionis exposed as public API

module.exports = { bindDocument, displayFiles, loadDirectory };

Next, amend the app.js file so that it calls the loadDirectory function from the user-Interface.js file. Change the app.js file to look like the following code.

Listing 3.6 Changing the app.js file for folder clicks

'use strict';

const fileSystem = require('./fileSystem');const userInterface = require('./userInterface');

function main() { userInterface.bindDocument(window); let folderPath = fileSystem.getUsersHomeFolder(); userInterface.loadDirectory(folderPath)(window); }

Calls userInterface.js file's loadDirectory function

window.onload = main;

Calls main function after HTML for app has loaded in window

One more change left to do. You can now remove the script tag from inside the current-folder div element. Change the current-folder div element in the index.html fileso that it looks like this:

<div id="current-folder"></div>

Exploring the folders

61

With those files changed, reload the app. Now, when you double-click an app folder,you'll see that the folder path changes in the toolbar, and the files and folders on dis-play in the main area change as well. An example of this is shown in Electron in fig-ure 3.2.

Figure 3.2 The Lorikeet app in Electron after navigating to a list of files inside of a folder, three levels away from the starting folder path

And figure 3.3 shows the same result in NW.js with the same file changes.

Figure 3.3 The Lorikeet app in NW.js, navigating to a hidden folder inside of my home folder

You can see here that you've been able to use plain vanilla JavaScript, HTML, andCSS to implement what is beginning to feel like a real desktop app. So far so good—but it's not mission complete yet. You're going to add quick search functionality tothe app.

62

3.2

CHAPTER 3 Building your first desktop application

Implementing quick searchFigure 3.4 shows a preview of what you'll add next: quick search functionality.

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

Figure 3.4 The quick search feature that you want to implement in the app

If you have a folder containing lots of files, searching through the entire list of themcan be tedious. In the wireframe, the toolbar features a search field in the top right,and to implement an in-directory search feature is relatively easy. You'll need to dothe following:

1 Add a search field to the top right of the toolbar.2 Add an in-memory search library.3 Add the list of files and folders in the current folder to the search index.4 When the user begins searching, filter the files displayed in the main area.

3.2.1

Adding the search field in the toolbarThe first thing you need to do is add some HTML for the search field in the top tool-bar. Insert the following HTML snippet into the index.html file, after the current-folder div element:

<input type="search" id="search" results="5" placeholder="Search" />

This adds an input tag with the type search and some extra attributes that give it thevisual style of a search field. The next step is to add the following CSS to the app.cssstylesheet:

#search { float: right; padding: 0.5em; min-width: 10em; border-radius: 3em; margin: 2em 1em; border: none; outline: none;}

Implementing quick search

63

Once this is done, the search field appears as shown in figure 3.5.

Figure 3.5 The search field in the top toolbar, like the wireframe in figure 3.4. Interestingly, the results attribute on an input element with the type search inserts a magnifying glass inside the text field.

3.2.2

Adding an in-memory search libraryNow that the search field exists, you need a way to perform searching on the list offiles and folders with a searching library. Thankfully, you don't need to write one, asthis is a common need that has already been satisfied.

lunr.js is a client-side search library, written by Oliver Nightingale (a colleagueof mine when we both worked at New Bamboo, now part of Thoughtbot). It allowsyou to create an index for the list of the files and folders and perform searches withthat index.

You can install lunr.js with npm from the command line:

npm install lunr --save

This will install lunr.js inside the node_modules folder and save it as a dependency tothe package.json file. Now, you need to create a new file at the same level as the app.jsfile, called search.js. You can create it either on the command line with the commandtouch search.js or via your text editor. Once it exists, add the code shown in thenext listing to the search.js file.

Listing 3.7 Inserting code into the search.js file

'use strict';

const lunr = require('lunr');  let index;

function resetIndex() {   index = lunr(function () { this.field('file'); this.field('type'); this.ref('path'); });}

function addToIndex(file) {  index.add(file);}

function find(query, cb) {   if (!index) { resetIndex(); }

Requires lunr.js as dependency via npm

resetIndex function resets search index

Adds file to index for searching against

Queries index for a given file here

64

CHAPTER 3 Building your first desktop application

const results = index.search(query); cb(results);}

module.exports = { addToIndex, find, resetIndex };

Exposes some functions for public API

The code implements three functions: addToIndex allows you to add files to the index,find allows you to query the index, and resetIndex resets the index when you need toview a new folder and clear the existing index. You expose these functions throughmodule.exports so that you can load the file in app.js and access those functions.

Once you've created and saved the search.js file, you need to attach it to the search

field in the UI, as well as get it to change what files are displayed in the main area.

3.2.3 Hooking up the search functionality with the UI

To have the search field trigger searching the file names, you need to be able to inter-cept the event of typing the query in the field. You can do this by adding a function tothe userInterface.js file called bindSearchField, which will attach an event listenerto the search field. In the userInterface.js file, add the following function to the file:

function bindSearchField(cb) { document.getElementById('search').addEventListener('keyup', cb, false);}

This code will intercept any events where the user has typed in the search field, andthe key on the keyboard is back up (hence, the event name keyup). You also add thisfunction to the module.exports object at the bottom of the userInterface.js file sothat you can expose it to the app.js file, as shown here:

module.exports = { bindDocument, displayFiles, loadDirectory, bindSearchField };

This function will be used to attach a function to the search field in the UI that triggerseach time the user presses a key on the keyboard while typing into the search field.

Here, you'll inspect the value that exists inside the search field. If it's blank, thenyou don't want to filter any files. But if it has another value, then you want to filter thefiles that are displayed in the main area. To achieve that, you need to do the following:

 Before you load a folder path in the main area, you reset the search index. When a file is added to the main area, you add it to the search index. When the search field is empty, you make sure that all files are on show. When the search field has a term, you filter the display of the files based on

that term.

But first, you should include the search module at the top of the dependencies list of theuserInterface.js file. Change the top of the userInterface.js file so that it looks like this:

'use strict';let document;const fileSystem = require('./fileSystem');const search = require('./search');

Implementing quick search

65

This provides you with access to the search module. Following the inclusion of thesearch module, the first change you want to make is to the loadDirectory function.You want it to reset the search index every time it's called so it only searches for filesthat are in the current folder path. Change the loadDirectory function's code tomatch the next listing.

Listing 3.8 Resetting the search index when calling loadDirectory

function loadDirectory(folderPath) { return function (window) { if (!document) document = window.document;  search.resetIndex();        displayFolderPath(folderPath); fileSystem.getFilesInFolder(folderPath, (err, files) => {  clearView();  if (err) {  return alert('Sorry, you could not load your folder');  }  fileSystem.inspectAndDescribeFiles(folderPath, files, displayFiles); }); };}

Adds the call to reset the search index

Once that's done, the next thing you want to adjust is the displayFile function belowthe loadDirectory function. The function will handle adding the file to the searchindex as well as making sure that the img element contains a reference to the file'spath so that the file can be filtered visually without needing to add/remove elementsfrom the DOM. Change the displayFile function's code to look like the following.

Listing 3.9 Adding files to the search index in the displayFile function

function displayFile(file) { const mainArea = document.getElementById('main-area'); const template = document.querySelector('#item-template'); let clone = document.importNode(template.content, true); search.addToIndex(file);           clone.querySelector('img').src = `images/${file.type}.svg`; clone.querySelector('img').setAttribute('data-filePath', file.path);  if (file.type === 'directory') {  clone.querySelector('img')  .addEventListener('dblclick', () => {   loadDirectory(file.path)  }, false); } clone.querySelector('.filename').innerText = file.file; mainArea.appendChild(clone); }

Attaches file's path as dataattribute to image element

Adds file to search index here

Next, add a function for filtering the results visually. This function uses a function tolook at the file paths for the files and folders on display in the main area and checkwhether any of them matches with the search results for the term typed into the

66

CHAPTER 3 Building your first desktop application

search field. After the bindSearchField function, add the function shown in the nextlisting to the userInterface.js file.

Listing 3.10 Adding the filterResults function to the userInterface.js file

function filterResults(results) {           const validFilePaths = results.map((result) => { return result.ref; }); const items = document.getElementsByClassName('item'); for (var i = 0; i < items.length; i++) { let item = items[i]; let filePath = item.getElementsByTagName('img')[0]  .getAttribute('data-filepath'); if (validFilePaths.indexOf(filePath) !== -1) {    item.style = null;        } else {  item.style = 'display:none;';  } }}

If so, make sure file is visible

If not, hide file

Collects file paths forsearch results so youcan compare them

Does file's path match with one of the search results?

You can add a small utility function to handle the case of resetting the filter. Thisoccurs when the search field is blank. Add the following function after the filter-Results function that was added to the userInterface.js file:

function resetFilter() { const items = document.getElementsByClassName('item'); for (var i = 0; i < items.length; i++) { items[i].style = null; }}

Here, you use a selector to select all div elements that have a CSS class of item, andmake sure they're visible by removing any custom style attributes that would havemarked them as hidden. Also, you want to make sure that the filterResults andresetFilter functions are publically available via the module API. Change the module.exports object at the bottom of the userInterface.js file so that it looks like this:

module.exports = { bindDocument, displayFiles, loadDirectory, bindSearchField, filterResults, resetFilter};

That's all the changes to make to the userInterface.js file for now. Next, turn yourattention to the app.js file and change it so that

 It binds on the search field in the user interface. It passes the search field's term to the search tool lunr. It then passes the results from the search tool back to the UI for rendering.

Change the code in the app.js file so that it looks like the code shown next.

Implementing quick search

67

Listing 3.11 Integrating the search feature into the app.js file

'use strict';

const fileSystem = require('./fileSystem'); const userInterface = require('./userInterface'); const search = require('./search');

Loads search module into app.js

function main() { userInterface.bindDocument(window); let folderPath = fileSystem.getUsersHomeFolder(); userInterface.loadDirectory(folderPath)(window); userInterface.bindSearchField((event) => {    const query = event.target.value;  if (query === '') {  userInterface.resetFilter();    } else {  search.find(query, userInterface.filterResults);  } }); }

window.onload = main;

Listens for changes to search field's value

If search field is blank, resets filter in UI

If search field has a value, passes it to search module's find function and filters results in UI

After saving this file along with the previous files, reload the app. The app loads likebefore, but this time you'll find that when you type a term into the search field, thefiles and folders in the main area of the app are filtered to show only those that matchthe search term. If you then type a blank value into the search field, all the files andfolders inside the current folder path are shown. Even as you double-click a folder andnavigate into it to see its files and folders, the search field will work on that currentfolder and filter its contents, as shown in figure 3.6.

Figure 3.6 The search field filtering files based on their name inside Atom's hidden folder

68

CHAPTER 3 Building your first desktop application

With about six handcrafted files totaling no more than 281 lines of code and somenpm modules, you've managed to build a file explorer. The file explorer can showthe files in a folder, traverse the folders, and filter the files based on the name of thefile as indicated in the original wireframe. Not bad, given the relatively small size ofthe code.

Next, you want to improve navigating through the app as well as getting files to

open with their default application.

3.3

Enhancing navigation in the appYou've gotten to a stage where you can display the contents of the user's personalfolder and allow them to traverse through those folders to see what other files andfolders exist on their computer, as well as filter the files and folders by a search query.Now you'll help the user navigate backward as well, as there isn't currently a way to dothat in the app.

To do this, you'll give the user the ability to navigate the folders via the currentfolder path—you'll make it a clickable path, with each folder in the path going to thatfolder's location on the computer.

3.3.1 Making the current folder path clickable

Figure 3.7 shows what you want to do.

Clicking on the folderitem here, changes whatis rendered there

Figure 3.7 When clicking any path in the current folder path in the top toolbar, you want to display the contents of the folder in the main area.

The current folder is currently a line of text that's displayed in the UI in the toolbar,but it can be used to do so much more. In this case, you're looking to change it so thatit looks the same as it looks now but allows the user to load a different folder path byclicking a folder name in the path, like clicking a link in a web page, as shown in fig-ure 3.8.

Let's begin by looking at the code that handles the display of the current folder inthe toolbar, the displayFolderPath function in the userInterface.js file. You'll needto modify this function so that instead of returning the current folder path, it passesthe folder path to another function, which will convert that folder path into a set of

Enhancing navigation in the app

69

b

Each path contains a snippet ofHTML that contains its folder path.

d

You pass this path tothe loadFolder() function,so that it loads inthe application.

c

When a user clicks on a path item in thecurrent folder path, you fetch its folder path.

Figure 3.8 How clicking a path item in the current folder path will end up loading that path in the app

span HTML elements. The span tags will contain not only the name of the folder, butalso a data attribute referring to the path of that folder. This is so that when the folderis selected, you can pass that folder to the loadFolder function and load the folder inthe app.

Let's begin by creating a function that will receive a folder name and return thefolder as a list of HTML span tags, with the path for that folder added as an attributeon the span tag. Call this function convertFolderPathIntoLinks and place it in theuserInterface.js file. First, you need to add a module dependency at the top of the file(after the search module require) to load Node.js's path module:

const path = require('path');

The path module is used to return the path separator used by the operating system. InMac OS and Linux, the path separator is a forward slash (/), but on Windows it's abackward slash (\). This will be used by the function to create the folder path for eachfolder as well as to display the full path for the current folder. In the convertFolder-PathIntoLinks function, the following code is used:

function convertFolderPathIntoLinks (folderPath) { const folders = folderPath.split(path.sep); const contents = []; let pathAtFolder = ''; folders.forEach((folder) => {  pathAtFolder += folder + path.sep;

70

CHAPTER 3 Building your first desktop application

contents.push(`<span class="path" data-path="${pathAtFolder.slice(0,

-1)}">${folder}</span>`);

}); return contents.join(path.sep).toString();}

The function takes the path for the folder and turns it into a list of folders by splittingit on the folder path separator. With this list of folders in the current folder path, youcan begin to create the span tags for each one. Each span tag will have a class attri-bute with a value of path, a data-path attribute that contains the path for that folder,and, finally, the name of the folder as the text inside the span tag.

Once the span tags are created, the HTML is joined together and returned as astring. This HTML is then used by the displayFolderPath function. It receives thecurrent folder path and returns the HTML to be inserted into the toolbar. As a result,you'll need to update the function to insert HTML instead of text. Adjust the display-FolderPath function to this code:

function displayFolderPath(folderPath) { document.getElementById('current-folder') .innerHTML = convertFolderPathIntoLinks(folderPath);}

The function now uses innerHTML to insert the HTML into the current-folder ele-ment in the screen, and the convertFolderPathIntoLinks function receives thefolder path passed to the displayFolderPath function and returns HTML in its place.The nice thing about this change is how you only had to change a small part of thedisplayFolderPath function, rather than lots of changes in multiple places. This is adesirable goal with coding: construct it so that it can be altered with ease. With thischange accomplished, you now need to handle clicking a folder name in the toolbarand having the screen navigate to that folder.

In the userInterface.js file, you'll add another function that will bind on a userclicking a folder name (in this case, any span element with a class of path) and returnthe folder path to a callback function. The callback function can then use the folderpath to pass that to the code that handles loading a folder. Add the following code tothe userInterface.js file, roughly toward the bottom of the file, but before the module.exports object:

function bindCurrentFolderPath() { const load = (event) => { const folderPath = event.target.getAttribute('data-path'); loadDirectory(folderPath)(); };

const paths = document.getElementsByClassName('path'); for (var i = 0; i < paths.length; i++) { paths[i].addEventListener('click', load, false); }}

Enhancing navigation in the app

71

You then want to call this function as part of the displayFolderPath function. Changethe displayFolderPath function to this:

function displayFolderPath(folderPath) { document.getElementById('current-folder') .innerHTML = convertFolderPathIntoLinks(folderPath); bindCurrentFolderPath();}

The userInterface.js file is easily extended to include extra functionality for handlingclicks on path items in the current folder path—which is nice, because it allows you toeasily alter your code without having to rewire whole swathes of the codebase.

3.3.2 Getting the app to load at the folder path

This simple one-line change enables the functionality to work, and the last codechange you want to do before you put it into action is to make the span elements showa pointer when the cursor passes over them. Add the following code to the app.css file:

span.path:hover { opacity: 0.7; cursor: pointer;}

With these changes saved, you can now reload the app, click through folders as nor-mal, and then go back by clicking a folder in the current folder path. This ensuresthat users can navigate back to other folders, because otherwise they would be stuck.What you've done so far is replicate a feature that's common to all native file explorersacross the operating systems (navigating folders via paths), but you added a twist to itso that the paths are clickable—not all file explorers do this. This shows how withElectron or NW.js you have the power to not only re-create desktop experiences usingweb technologies, but also combine them in ways to do new things that haven't beendone in desktop apps before.

Now that you've added that feature, the next step is to handle opening files with

their default application.

3.3.3 Opening files with their default application

So far in the app, you've focused a lot on interacting with folders, but now you need tolook at how you can make the file explorer open files like images, videos, documents,and other items.

In order to implement this feature, you'll need to do the following: Handle clicking on a file as opposed to a folder. Pass the file path for that file to NW.js/Electron's way of opening external files.

We'll look at handling clicking a file first.

72

CHAPTER 3 Building your first desktop application

CLICKING A FILEYou'll probably remember from earlier on in the chapter that you detected whetherthe file you were rendering to the main area was a folder, and attached an event to itwhen it was double-clicked. You'll use the same pattern again to handle double-clicking files.

In the userInterface.js file is the displayFile function that handles displaying theindividual files and folders in the main area, as well as attaching events to them.Change the function so that it looks like the following listing.

Listing 3.12 Adding file double-clicking to the displayFile function

function displayFile(file) { const mainArea = document.getElementById('main-area'); const template = document.querySelector('#item-template'); let clone = document.importNode(template.content, true); search.addToIndex(file); clone.querySelector('img').src = `images/${file.type}.svg`; clone.querySelector('img').setAttribute('data-filePath', file.path); if (file.type === 'directory') {  clone.querySelector('img')  .addEventListener('dblclick', () => {   loadDirectory(file.path)();  }, false); } else {          clone.querySelector('img')  .addEventListener('dblclick', () => {   fileSystem.openFile(file.path);   }, false);  } clone.querySelector('.filename').innerText = file.file; mainArea.appendChild(clone);}

Not a directory, therefore a file, so you can attach an event to it

Calls out to new function in the fileSystem module called openFile, which is passed the path to the file

The couple of extra lines of code allow you to listen to the file being double-clickedand attach it to a new function called openFile in the fileSystem.js module, whichyou'll now create.

The openFile function in the fileSystem.js module is going to call out to eitherElectron or NW.js's shell API. The shell API is able to open URLs, files, and folders intheir default applications. To show you how compatible Electron and NW.js are asdesktop app frameworks, you'll write one item of code that can be used across bothframeworks without any need for modification.

In the fileSystem.js file, add the following snippet of code toward the top of the

file, below the dependency declarations:

let shell;

if (process.versions.electron) { shell = require('electron').shell;} else { shell = window.require('nw.gui').Shell;}

Enhancing navigation in the app

73

This snippet of code can run on either an Electron app or an NW.js app, which meansless code for you to have to write/adjust. Notice how Electron and NW.js call out to ashell object (though NW.js calls it via the GUI API, and with a title-cased name). Ifthe app is running as an Electron application, it will load Electron's shell API, and ifrunning NW.js, it will load NW.js' shell API.

With the shell API loaded for the given Node.js desktop app framework, you nowcall out to the shell API's method for opening files. Add the function shown in the fol-lowing listing to the fileSystem.js file, right before the module.exports object.

Listing 3.13 Adding the openFile function to the fileSystem.js file

function openFile(filePath) { shell.openItem(filePath);  }

Calls the shell API's openItem function with the file path

Notice anything funny? The shell API's function name for opening files is the sameacross both Electron and NW.js. It's a pleasant surprise that may seem unexpectedunless you know a bit about NW.js and Electron's shared history.

With this new function, all you need to do now is make sure it's available as a pub-lic API function in the fileSystem.js file. Amend the module.exports object so that itincludes the function, as shown in the following code:

module.exports = { getUsersHomeFolder, getFilesInFolder, inspectAndDescribeFiles, openFile};

I'd almost say you're done, but there's one more thing (to borrow a phrase from thelate Steve Jobs). You want to give the app a visual indicator that the files and the fold-ers can be clicked when the cursor is hovering over them. You can extend the last CSSrule you added earlier to the app.css file. As a reminder, it looked like this:

span.path:hover { opacity: 0.7; cursor: pointer;}

Extend it so that it also applies to the file and folder icons in the main area:

span.path:hover, img:hover { opacity: 0.7; cursor: pointer;}

With those changes saved, reload the app and have a go at double-clicking files in theLorikeet app. You'll see that those files end up opening in their default applications.

74

3.4

CHAPTER 3 Building your first desktop application

Fantastic! You now have a functional file explorer that can open files, as well as explorefolders and filter the view by name.

SummaryIn this chapter, you built on the beginnings of a desktop app and created some richfeatures that make the app a usable, minimally viable product. You also had a chanceto explore how you can evolve a desktop app's codebase to remain readable, and howyou can organize the code for a desktop app (because there's no convention-over-configuration approach to doing this currently). Things we've covered include the following: Refactoring the code by using Node.js's module functionality Using third-party libraries to implement search features Applying Electron and NW.js's shell API to handle opening files with their

default applications

 Improving app navigation to make the desktop app more usable

The main thing to take away from this chapter is that with a couple-hundred lines ofcode and some external files, you can build an app that replicates what a native desk-top app can do (and one that has relatively complex functionality). Not only that,you've been able to use third-party libraries like lunr.js to help provide this functional-ity, and structured the code in such a way that it can be used in web apps and allow forbuilding apps for both the web and desktop from the same source code.

In chapter 4, you'll prepare the app for distribution: you'll hide the app developertoolbar, give the app its own icon, and build it so that it can be run as a native app oneach of the operating systems.

Shipping your firstdesktop application


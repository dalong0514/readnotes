the application

Menus are important for providing users with lots of feature choices. Anyone famil-iar with using Microsoft Office will know how much functionality is available tousers from the app menu when using Word or Excel. It's one of the most effectiveUI patterns in widespread use today.

In this chapter, we'll look at how to create app menus for your desktop apps.You'll see how they're handled differently by Mac OS compared to Windows andLinux. We'll then look at context menus, which provide the user with options whenright-clicking on elements within the app, such as being able to insert an item ofcontent at a particular point within a document.

153

154

9.1

CHAPTER 9 Creating application and context menus

Adding menus to your appThree kinds of menus are available for your Node.js desktop apps: app windowmenus, context menus, and tray menus (covered in chapter 8). App window menusappear in the top of an app window under the title bar (or in the system menu on MacOS), and you see context menus when right-clicking an item in the app. We'll take alook at app window menus first.

9.1.1

App window menus

Creating an app menu bar is a bit tricky, and you must consider which OSs you'retargeting.

Surprisingly, this is something that Microsoft Windows and Linux operating sys-tems handle exactly the same way, and Mac OS is the odd one. On Windows andLinux, each app window has its own menu placed within it. For Mac OS, there's onlyone app menu for all the windows (displayed in the OS's menu bar, separate from theapp window).

NW.js accommodates this difference in approaches by offering an API method spe-cific to Mac OS and other methods for Windows and Linux. Electron, however, doesnot. It provides a single API method for creating app menus. We'll look at these APIswith examples in both frameworks to compare their approaches.

9.1.2

Creating menus for Mac OS apps with NW.js

A special API function is available for creating an app menu for Mac OS. To demon-strate this, let's take an example Hello World app and add a Mac OS app menu to it(this code is the mac-app-menu-nwjs app in the book's GitHub repository). You'll addthe basic package.json file and then a standard index.html file with a link to an app.jsfile that will contain the code for the app's Mac OS menu.

Listing 9.1 The app.js file for the Mac app menu with NW.js

'use strict';

const gui = require('nw.gui');

Creates Menu instance as menu bar

Transforms menu into a Mac OS menu and passes app name

const mb = new gui.Menu({ type: 'menubar' }); mb.createMacBuiltin('Mac app menu example');

gui.Window.get().menu = mb;

Attaches that menu to app's window

The app.js file in listing 9.1 embeds some JavaScript that initializes a new Menu object,creates the built-in Mac menu from it, gets the current app window, and sets its menuto be the Mac menu you generated. The end result should look like figure 9.1.

Adding menus to your app

155

Figure 9.1 NW.js's default app menu for Mac OS apps. The menu provides some default actions such as copying/pasting content, hiding/closing windows, and finding out a bit about the app.

The built-in menu options allow the user to get up and running with a set of com-mands nested under the Edit and Window menu items, listed in table 9.1.

Table 9.1 Commands for menu options

Edit menu command

What it does

Undo

Redo

Cut

Copy

Paste

Delete

Select All

Reverts the last action

Restores the last action that was undone

Copies content and removes it from its current location

Copies selected content

Puts copied content in a given location

Removes selected content from a location

Selects all content

Window menu command

What it does

Minimize

Shrinks the window and animates its location in the task bar

Close Window

Closes the window

Bring All to Front

Makes all the windows for the app appear above other windows

These are pretty standard commands that you'll find across apps with any kind ofcomprehensive functionality.

Let's take a look at how Electron handles making Mac OS menus compared to

NW.js.

9.1.3

Creating menus for Mac OS apps with ElectronThe logical composition of menus and menu items is the same when you're creatingmenus in Electron apps, but the API functions to create and combine them arenamed differently. To illustrate this, we'll walk through an example app with a menuin Electron. The code for this is also in the book's GitHub repository under the appname mac-app-menu-electron.

When you download the app, you'll find a typical Electron app example, and thepart of the code we're interested in is in the app.js file. When defining an app menu

156

CHAPTER 9 Creating application and context menus

in Electron, you need to add it to an app window, and therefore this needs to be donein the code for the render process that handles the app window. Let's now walkthrough the code for defining an app menu in Electron.

Listing 9.2 Creating an app menu in Electron

'use strict';

const electron = require('electron');const Menu = electron.remote.Menu;  const name = electron.remote.app.getName();

Submenuitemsdefinedas array

Menu itemcan havetypes thatdo defaultactions(displayingAbout dialog)

const template = [{      label: '',    submenu: [  {  label: 'About ' + name,  role: 'about'  }, {       type: 'separator' }, {  label: 'Quit',  accelerator: 'Command+Q',   click: electron.remote.app.quit  } ]}];

LoadMenu module via remote API

App name also loaded via remote

Defines template array to contain menu items

Leaves label blank—app's name overridden on Mac OS

Menu items can have other types (separators between menu items)

Passes keyboard shortcut as string via accelerator property

Defines custom actions when menu item is clicked on click property

const menu = Menu.buildFromTemplate(template); Menu.setAppMenu(menu);

Sets app's menu from template

Uses buildFromTemplate function to create app menu

This code will result in an app that has a simple set of actions that can be performedas illustrated in figure 9.2.

Figure 9.2 Electron rendering the menu items for Mac OS apps. Note the process name is displayed as the app menu's label name, with an About menu item, a separator, and the Quit menu item, with the keyboard shortcut displayed to the right.

This example is basic, and you may want to have more options available, such as Editand Window menus that have typical actions like resizing windows and copy-and-pasteactions. If you want full control over those actions, you can copy the example providedby Electron at http://electron.atom.io/docs/api/menu/ into your app. Or you canavoid copying lines of code into your app by using an npm module called electron-default-menu, available from www.npmjs.com/package/electron-default-menu. To

Adding menus to your app

157

show the menu library in action, you'll alter the app's code to use it in place of thetemplate variable. First, you need to install the module in the app's code via npm:

npm install electron-default-menu --save

After installing the npm module, change the contents of the app.js file to the codeshown next.

Listing 9.3 Using electron-default-menu in the app.js file

'use strict';

const electron = require('electron');const defaultMenu = require('electron-default-menu'); const Menu = electron.remote.Menu;

const menu = Menu.buildFromTemplate(defaultMenu()); Menu.setAppMenu(menu);

Requires npm module to use later

Calls it in place of template code to provide default menu

Now, reload the app, and you'll see a full app menu, as shown in figure 9.3.

Figure 9.3 The Electron app with menu items for Edit, View, and Window options

The electron-default-menu module provides the app window with more actions andprovides a base for adding other menu items. The defaultMenu() function returns anarray, so adding/removing menu items can be done via pop, push, shift, and unshiftfunctions on the menu variable. For a full list of functions available on the array, seehttp://mng.bz/cS21.

HOW DO I CHANGE THE APP MENU'S FIRST ITEM NAME? On Mac OS, the appmenu's first item is set to the app's name, regardless of what value is set in thecode. This is because Mac OS gets that name from the app's Info.plist file. Ifyou want to change the first menu item's label, you'll need to edit this file inthe built version of your app. For more information, see http://mng.bz/12r1.

Now that we've covered how to handle Mac menus in your desktop apps, we'll turnour attention to how to handle them in Windows and Linux.

158

9.1.4

CHAPTER 9 Creating application and context menus

Creating menus for Windows and Linux appsBecause Windows and Linux handle menus differently than Mac OS, NW.js providesdifferent API methods for creating menus, so you'll go through the same example(Hello World) with those methods. First, you'll create an app with NW.js.BUILDING WINDOWS/LINUX APP MENUS WITH NW.JSLet's say you have an app that needs a menu bar, with one menu item (File), and fornested menu items, you have the following commands: Say Hello and Quit the App.Figure 9.4 shows the app you want to create.

Figure 9.4 The app you want to build, with the menu in the top left

The Say Hello menu item shows an alert dialog with the message「Hello World」insideit, and the Quit the App menu item closes the app. First, let's focus on creating themenu bar and implementing the File menu item.CREATING THE MENU BARLet's say you start with the following index.html content:

<html> <head> <title>Windows/Linux menu app example for NW.js</title> </head> <body> <h1>Windows/Linux menu example</h1> </body></html>

Adding menus to your app

159

This initial page contains no code for the menu yet, so you'll start by adding a scripttag in the head section of the HTML (after the title tag):

<script> 'use strict';</script>

Next, inside the script tag you'll load the GUI library:

<script> 'use strict';

const gui  = require('nw.gui'); const menuBar = new gui.Menu({type:'menubar'});</script>

You load NW.js's GUI library so that you can begin to create the menu. On the followingline, you create a menu bar, where menu items will be placed in the app window. Youhave to do this before you can begin to create any menu items, which is what followsnext. On the following line inside the script tag, you initialize the File menu item:

<script> 'use strict';

const gui  = require('nw.gui'); const menuBar = new gui.Menu({type:'menubar'}); const fileMenu = new gui.MenuItem({label: 'File'});</script>

Now that you've initialized all the objects you want to render in the app window, youneed to attach the file menu to the menu bar:

<script> 'use strict';

const gui  = require('nw.gui'); const menuBar = new gui.Menu({type:'menubar'}); const fileMenu = new gui.MenuItem({label: 'File'});

menuBar.append(fileMenu);</script>

The menu bar has an append function that allows you to add menu items to it, andyou use this to add the File menu item. Now, you can attach the menu bar to the appwindow, like so:

<script> 'use strict';

const gui  = require('nw.gui'); const menuBar = new gui.Menu({type:'menubar'}); const fileMenu = new gui.MenuItem({label: 'File'});

menuBar.append(fileMenu); gui.Window.get().menu = menuBar;</script>

160

CHAPTER 9 Creating application and context menus

The gui.Window.get() function call selects the current app window, and calling.menu on it allows you to attach the menu bar to it. You can take a look at the example(make sure that there's an accompanying package.json manifest file to support load-ing the example with NW.js) by running nw on the folder in the command line. Youshould see something like figure 9.5.

Figure 9.5 The app window shows a menu bar at the top with the File menu item.

Great! So far, you know how to create menu items in the main menu for an app win-dow. But if you click the File menu item, nothing happens. You need to attach a menuto the File menu item with options to say hello and to quit the app.SUBMENUSContinuing with the existing code that you've written, you'll do the following: Initialize some menu items for the Say Hello and Quit the App actions. Create a menu to attach those menu items to. Attach that menu to the File menu item.

The important thing to bear in mind is that menu items always attach to menus, and amenu can be nested under a menu item, creating a submenu. You'll see this as youadd the two actions to the File menu item.

Let's start by creating the menu items. In the script tag, add two lines for the

menu items, below the initialization of the fileMenu menu.

Listing 9.4 Creating submenu items for the File menu item

<script> 'use strict'; const gui  = require('nw.gui');

Adding menus to your app

161

const menuBar = new gui.Menu({type:'menubar'});const fileMenu = new gui.MenuItem({label: 'File'});

const sayHelloMenuItem = new gui.MenuItem({label: 'Say hello'});const quitAppMenuItem = new gui.MenuItem({label: 'Quit the app'}); menuBar.append(fileMenu); gui.Window.get().menu = menuBar;</script>

You've created two new menu items: sayHelloMenuItem and quitAppMenuItem. Younow need to initialize a menu to attach these menu items to. We'll call this menufileMenuSubMenu (not exactly the most inventive name, but at least it's descriptive)and initialize it after the newly created menu items. Then, you'll attach the menuitems to the File menu. Adjust the code to look like the following listing.

Listing 9.5 Attaching the action menu items to the submenu

<script> 'use strict'; const gui  = require('nw.gui'); const menuBar = new gui.Menu({type:'menubar'}); const fileMenu = new gui.MenuItem({label: 'File'});

const sayHelloMenuItem = new gui.MenuItem({label: 'Say hello'}); const quitAppMenuItem = new gui.MenuItem({label: 'Quit the app'});

const fileMenuSubMenu = new gui.Menu(); fileMenuSubMenu.append(sayHelloMenuItem); fileMenuSubMenu.append(quitAppMenuItem);

menuBar.append(fileMenu); gui.Window.get().menu = menuBar;</script>

Here, you create a new menu and attach the menu items for the actions to it. You'realmost there. The next bit is to bind that menu onto the File menu item. In NW.js,menu items have a submenu property, and setting this attaches a menu onto a menuitem, creating a submenu. Add another line after appending the two menu items andbefore appending the fileMenu to the menuBar, as shown next.

Listing 9.6 Attaching the submenu to the file menu

<script> 'use strict';

const gui  = require('nw.gui'); const menuBar = new gui.Menu({type:'menubar'}); const fileMenu = new gui.MenuItem({label: 'File'});

const sayHelloMenuItem = new gui.MenuItem({label: 'Say hello'}); const quitAppMenuItem = new gui.MenuItem({label: 'Quit the app'});

const fileMenuSubMenu = new gui.Menu(); fileMenuSubMenu.append(sayHelloMenuItem); fileMenuSubMenu.append(quitAppMenuItem);

162

CHAPTER 9 Creating application and context menus

fileMenu.submenu = fileMenuSubMenu;

menuBar.append(fileMenu); gui.Window.get().menu = menuBar;</script>

By setting the submenu property on the fileMenu object to the fileMenuSubMenu, youcreate a submenu for the File menu item. Save the file, run nw on the app folder fromthe command line, and when you click the File menu item, you should now see thetwo action items appear, like in figure 9.6.

Figure 9.6 The File menu item now has a submenu, with the actions that you want to perform on the app.

Now you're beginning to see something like the finished product—nested menuitems that will allow you to trigger actions when you click them. The final bit thatremains is to trigger actions when you click them. This is an easy thing to do in NW.js.When specifying the menu items and their labels, you can also provide functions tocall when the menu items are clicked. In this case, you can add two simple functionsto the sayHelloMenuItem and quitAppMenuItem objects in your code; adjust the code tolook like this:

const sayHelloMenuItem = new gui.MenuItem( { label: 'Say hello',  click: () => { alert('Hello'); } });

const quitAppMenuItem = new gui.MenuItem( { label: 'Quit the app',  click: () => { process.exit(0); } });

When initializing the menu item objects, you set the click attribute on them withfunctions that you want to execute when they're clicked. In this case, clicking theSay Hello menu item will trigger an alert dialog with the word「Hello,」and clickingthe Quit the App menu item will call Node.js's process.exit function to terminatethe app.

Adding menus to your app

163

Save the code and reload the app from the command line. When you click the Filemenu and then click Say Hello, you should see the dialog box. Once you've dismissedthe dialog, click the Quit the App menu item, and the program will close.

If you run the app on OpenSUSE Linux (Tumbleweed edition), you'll see some-

thing akin to figure 9.7.

Figure 9.7 The Windows/Linux menu app example for NW.js running on OpenSUSE Tumbleweed edition

Now that you've created the app using NW.js, let's take a look at what's involved in cre-ating the same app with Electron. CREATING THE MENU APP WITH ELECTRONElectron's approach to creating app menus is simpler, in my opinion, because you canpass an object with submenus as arrays, rather than having to call multiple API meth-ods to append menus. You'll replicate the app you created for the NW.js app exampleusing Electron's APIs, and notice the difference in approaches.

I've created an app for this called windows-linux-menu-app-electron in the book'sGitHub repository. You can download the app from there and give it a spin. I'll talkyou through the interesting bits of the code.

The code for the app is similar to that for the NW.js variant, but the differencehere is that you add an app.js file to hold the browser window code for the app, whereyou'll define the custom code for the menu.

Let's take a look at that app.js file where all the interesting stuff happens.

Listing 9.7 The app.js file for the Windows/Linux app menu with Electron

'use strict';

const electron = require('electron');   const Menu = electron.remote.Menu;

Requires Menu API via Electron's remote API

const sayHello = () => { alert('Hello'); };

const quitTheApp = () => { electron.remote.app.quit(); };

const template = [ { label: 'File', submenu: [     {  label: 'Say Hello',  click: sayHello  },

Generates menu template with submenu items as an array

164

CHAPTER 9 Creating application and context menus

{  label: 'Quit the app',  click: quitTheApp  } ] }];

const menu = Menu.buildFromTemplate(template);  Menu.setAppMenu(menu);

Generates menu for that item; attaches it to app

You can see that Electron offers a simpler API when it comes to creating menus withsubmenu items. When you run the app on Windows 10, you see figure 9.8.

Figure 9.8 The Electron Menu app running on Windows 10. Note that it's almost identical to the NW.js example, bar the app icon.

9.1.5

Now you know how to create app menus, but suppose you want your app to have dif-ferent menus for the various OSs (so as to follow their UX conventions). How do youcater for that?

Choosing which menu to render based on the OSNow that you have different code for handling menus for both Mac and Windows/Linux, the next step is to be able to load different versions of the menu specific to theOS that the app is running on. For example, say you have two functions that wraploading the menus for the different OSs, one called loadMenuForMacOS and anothercalled loadMenuForWindowsAndLinux, and you need to make sure that loadMenuFor-MacOS runs only on a Mac—otherwise, loadMenuForWindowsAndLinux executes instead.This can be done using Node.js's OS API, with the following code:

const os = require('os');

function loadMenuForWindowsAndLinux () {}function loadMenuForMacOS () {}

if (os.platform() === 'darwin') { loadMenuForMacOS;} else { loadMenuForWindowsAndLinux;}

This checks if the OS's platform name is 'darwin' (which is what Mac OS calls itselftechnically). If it is, you load the menu for Mac OS—otherwise, you load the menu forWindows and Linux. This is how you can ensure that the menus work for both Win-dows/Linux and Mac OS in their respective formats. Hopefully, one day you won'tneed to do this kind of workaround, but for now this is how it's done.

Context menus

165

9.2

Context menusSometimes you want to be able to interact with content inthe app window and perform a number of actions relevantto that content. For example, when you right-click a pieceof selected text in a word processor, you'll see options tocut/copy the content, to check the spelling of the content,and even to search for the content on a search engine.

Electron and NW.js's menu APIs can be used to createcontext pop-up menus that are triggered when clickingcontent inside of the app window, such as in figure 9.9.

9.2.1

Creating the context menu app with NW.js

To explore how the API works across both frameworks,I've built a simple WYSIWYG HTML editor named Cirrus(see figure 9.10). The editor lets you create HTML pagesby typing text into the editor window, and it then gener-ates HTML for you. The feature you'll add to Cirrus is the ability to right-click a pieceof content inside the WYSIWYG editor and display a relevant context menu that willallow commands to be performed on that content. We'll walk through the NW.jsexample first, and then the Electron example afterward for comparison.

Figure 9.9 A context menu displayed in Microsoft Word 2016 for Mac

First, download a copy of the Cirrus NW.js app from the book's GitHub repository.Now, take a good look around the code in the app.js file to get familiar with it, and

Figure 9.10 Cirrus, a simple WYSIWYG HTML editor

166

CHAPTER 9 Creating application and context menus

then look at how you can use context menus to insert multimedia content such asimages and videos. Figure 9.11 shows what you want to achieve.

Figure 9.11 A wireframe of the context menu you want to create

From the wireframe, you need to do the following:

1 Create a menu with two items, insert an image, and insert a video.2 Create a way to bind the menu on appearing when a right-click is made on the

content in the design view.

3 Create functions for the menu items of inserting an image and inserting a

video.

4 Create a way to insert HTML into a specific cursor position in the content in

the design view.

You'll start by creating an empty JavaScript file called designMenu.js in the cirrus folder.This will hold the code for the context menu shown in the wireframe in figure 9.11.Then you'll add a single line of HTML to the index.html file to allow you to select animage to insert into the page, as well as load the designMenu.js file in the app.js file.

In the designMenu.js file, add the code (bit by bit) shown here.

Listing 9.8 Creating insert image/video context menus, part 1

'use strict';

let x;       let y;       let document;

Uses these variables to store coordinates where context menu was clicked

function insertContent (content) {      const range = document.caretRangeFromPoint(x, y); if (range) { range.insertNode(content); }}

Adds function that inserts text content at the place where context menu was raised

This allows you to handle tracking where the context menu is clicked and then insertsome text content into that point in the page. The following listing continues the process.

Context menus

167

Listing 9.9 Creating insert image/video context menus, part 2

function openImageFileDialog (cb) {      const inputField = document.querySelector('#imageFileSelector'); inputField.addEventListener('change', () => { const filePath = this.value; cb(filePath); }); inputField.click();}

Function to handleopening file dialog menufor selecting an image

function insertImage () {      openImageFileDialog((filePath) => { if (filePath !== '') {  const newImageNode = document.createElement('img');  newImageNode.src = filePath;  insertContent(newImageNode); } });}

Function to trigger opening image file dialog; then inserts image into the HTML page as image element

You now have the bits for inserting an image from the context menu when the userright-clicks in the HTML page, as shown in the next listing.

Listing 9.10 Creating insert image/video context menus, part 3

function parseYoutubeVideo (youtubeURL) {      if (youtubeURL.indexOf('youtube.com/watch?v=') > -1) {  return youtubeURL.split('watch?v=')[1]; } else if (youtubeURL.match('https://youtu.be/') !== null) {  return youtubeURL.split('https://youtu.be/')[1]; } else if (youtubeURL.match('<iframe') !== null) {  return youtubeURL.split('youtube.com/embed/')[1].split('"')[0];  } else {  alert('Unable to find a YouTube video id in the url');  return false; } }

Function looks after getting YouTube video URL, handling different YouTube share formats

When inserting video, user sees dialog asking for YouTube URL, which is passed into parser to handle different share formats

function insertVideo () {    const youtubeURL = prompt('Please insert a YouTube url'); if (youtubeURL) {  const videoId = parseYoutubeVideo(youtubeURL);

iframe elementto load theYouTube videois constructedand insertedinto HTML page

if (videoId) {              const newIframeNode = document.createElement('iframe');  newIframeNode.width = 854;  newIframeNode.height = 480;  newIframeNode.src = `https://www.youtube.com/embed/${videoId}`;  newIframeNode.frameborder = 0;  newIframeNode.allowfullscreen = true;  insertContent(newIframeNode);  } } }

168

CHAPTER 9 Creating application and context menus

You've added the functions for inserting a YouTube video into the HTML page. Nowall that's left to do is hook up those functions to the context menu interface, whichyou now need to construct, as in the following listing.

Listing 9.11 Creating insert image/video context menus, part 4

function initialize (window, gui) {     if (!document) document = window.document; const menu = new gui.Menu();

menu.append( new gui.MenuItem({  label: 'Insert image',  click: insertImage }) );        menu.append( new gui.MenuItem({  label: 'Insert video',  click: insertVideo }) );

With NW.js GUI, creates menu instance for context menu

Adds menu item for inserting an image

Adds another menu item for inserting a video

Creates function to load everything; passed NW.js's window and GUI library as arguments

document.querySelector('#designArea')    .addEventListener('contextmenu', (event) => {  event.preventDefault();  x = event.x;  y = event.y;  menu.popup(event.x, event.y);  return false; });}

module.exports = initialize;

Exports the module

Attaches that menu to app's design area so that right-clicking inside it loads that context menu

Next, in the index.html file, add the following line of code (in bold) after the openingbody tag:

</head> <body> <input type="file" accept="image/*" id="imageFileSelector" class="hidden"/>

Finally, add the following line of code for loading the designMenu.js file in the depen-dencies section of the app.js file:

const designMenu = require('./designMenu');

At the end of the initialize function in the app.js file, add the line of code to loadthe designMenu code:

designMenu(window, gui);

Context menus

169

You should have the same code as is in the addContextMenu branch of the app's coderepository on GitHub. If you give the app a spin, open an HTML file to start editing,and right-click inside the content when on the design tab, you should see the contextmenu shown in figure 9.12.

Figure 9.12 The context menu on display in the Cirrus WYSIWYG HTML editor

If you click Insert Image, you'll get a File dialog for selecting an image to insert intothe page, and if you click Insert Video, you'll see a prompt dialog asking for a You-Tube URL for a video to embed in the page.

9.2.2 How do context menus work with NW.js?

Setting up a context menu uses a similar API to the one for setting up app windowmenus, with one difference—you don't have to pass any options when initializing themenu instance, as shown here:

const menu = new gui.Menu();

With the menu object initialized, you can add menu items for the Insert Image andInsert Video options to the menu object:

menu.append( new gui.MenuItem({ label: 'Insert image', click: insertImage }));menu.append( new gui.MenuItem({ label: 'Insert video', click: insertVideo }));

At this stage, clicking either menu item will trigger commands for picking an imagefile or a YouTube video to embed in the page. You can ignore the specifics of how

170

CHAPTER 9 Creating application and context menus

those work for now and focus on how the menu appears where the user right-clicksthe content inside the app.

In NW.js's API, the menu object instance has a pop-up function that when passedthe x and y coordinates on the app, will bring up the menu at that location on theapp, as shown in figure 9.13.

Figure 9.13 The menu.popup function allows you to control the exact placement of the context menu within the app.

To bind this function with the location the user right-clicks in the app window, youneed a way to track the coordinates of the user's right-click. There's a way to do thiswith browser-specific JavaScript, as illustrated in the following code:

document.querySelector('#designArea') .addEventListener('contextmenu', (event) => {  event.preventDefault(); menu.popup(event.x, event.y); return false; });

Here, you look for the div element where the WYSIWYG part of the page is displayedthat can be edited, and attach an event listener on it for whenever a user right-clicksanywhere inside the div element (the event is named contextmenu). When this eventoccurs, you prevent the default behavior from occurring and instead call the menu'spop-up command with the coordinates where the right-click occurred.

9.2.3 Giving menu items icons

You'll notice from the context menu in the Cirrus app that the options aren't easy todistinguish between—they have similarly named labels. You can use icons to helpmake them more distinct. In NW.js, you have the ability to add icons to menu items,which is an easy way to identify them.

The menu items created for the Insert Image and Insert Video commands can be

modified to look like this:

Context menus

171

menu.append( new gui.MenuItem({ icon: 'picture.png', label: 'Insert image', click: insertImage }));menu.append( new gui.MenuItem({ icon: 'youtube.png', label: 'Insert video', click: insertVideo }));

You add an icon attribute to the MenuItem's options, with images that have been gen-erated from the Font Awesome library. You can use these icons in the app (they existin the icons branch on the Cirrus app's GitHub repository), and when you load theapp and right-click a loaded page in design view, you should see something like fig-ure 9.14.

Figure 9.14 The context menu, with icons displayed next to the menu item commands

9.2.4

In the last couple of pages, you've created a WYSIWYG app from scratch and addedfeatures for inserting images or videos via context menu items. Now we'll take a quicklook at how you'd do the same thing using Electron.

Creating a context menu with ElectronRather than build the entire app from scratch, you can download a copy of the codefor the app Cirrus Electron from the book's GitHub repository. We'll walk through thebit concerning the context menu so that you can grasp how Electron handles imple-menting that.

The app is built, and you want to add a context menu for displaying options toinsert an image or video. The context menu has two items: Open, for opening anHTML file to edit, and Save, for saving the updates to that file back on the computer.These actions involve reading data from a file on the user's computer, as well as saving

172

CHAPTER 9 Creating application and context menus

data to those files back onto the user's computer. The part of the app that the usersees is the UI, which runs in the render process, and the part that reads and writesdata to the hard disk runs in the main process. You need to use Electron's inter-processcommunication APIs (ipcMain and ipcRenderer) to transmit file paths and contentfrom the front end (renderer) to the back end (main), as well as transmit content andfile save state changes from the back end (main) to the front end (renderer).

If you've downloaded a copy of the app's code from GitHub, take a look at theapp.js file inside the cirrus-electron folder. At the top of the app.js file, you declarethe dependencies for the app, as shown here.

Listing 9.12 The app dependencies for the Cirrus-electron's front-end code

const electron  = require('electron');const Menu   = electron.remote.Menu;   const MenuItem  = electron.remote.MenuItem;const ipc   = electron.ipcRenderer;     const dialog  = electron.remote.dialog; const designMenu = require('./designMenu');let currentFile;let content;let tabWas;let done;

Accesses Dialog API forFile Opening dialog,again via remote API

Loads menu API from renderer process via remote API

Calls ipcRenderer API so you can pass data to main process

Anytime you want to access an API that's in the main process, you can do it via Elec-tron's remote API. In this case, you want to access the menu and dialog APIs for theapp. Because you're going to be asking the main process to read files and save contentto files as well, you call Electron's ipcRenderer module to allow you to pass messagesto the app's main process.

Figure 9.15 shows a diagram to demonstrate what you're trying to achieve. This fig-ure illustrates the flow of IPC events from the renderer process (where the front endexists) to the main process (where the back end exists). This is used when you selectan index.html file from the Open File dialog and want to load the contents of that file

Main process

Renderer process

readFile

FileRead

saveFile

fileSaved

Figure 9.15 The IPC events in the app for communicating when to read a file and when to save it

Context menus

173

into the editor. It's also used when you want to save the contents in the editor back tothe file.

To demonstrate this in action, let's take a look at the bit of code in the app.js file

that handles when you want to open a file, on line 26, shown next.

Listing 9.13 The code for opening files from the UI on Cirrus Electron

function openFile (cb) { dialog.showOpenDialog((files) => {    ipc.send('readFile', files);      if (files) currentFile = files[0];  if (cb && typeof cb === 'function') cb(); }); }

Calls dialog API to load dialog for opening an HTML file

Pass list of files to main process

A list of files is passed to the main process, which is then intercepted in code thatexists in the main.js file, and is shown next.

Listing 9.14 The code for opening files from the back end on Cirrus Electron

'use strict';

const electron = require('electron');const fs = require('fs');const app = electron.app;const BrowserWindow = electron.BrowserWindow;const ipc = electron.ipcMain;     let mainWindow = null;

app.on('window-all-closed', () => { if (process.platform !== 'darwin') app.quit();});

Includes Electron's IPC API for main process

app.on('ready', () => { mainWindow = new BrowserWindow(); mainWindow.loadURL(`file://${__dirname}/index.html`); mainWindow.on('closed', () => { mainWindow = null; });});

function readFile (event, files) {     if (files) { const filePath = files[0];        fs.readFile(filePath, 'utf8', (err, data) => {  event.sender.send('fileRead', err, data);   }); }};

readFile function reads contents of a given file

Chooses first filePath in list of files—you can work only with one at a time

Once contents are read, sends it back to renderer process

Defines saveFile function that saves contents to a file

function saveFile (event, currentFile, content) {  fs.writeFile(currentFile, content, (err) => { event.sender.send('fileSaved', err);  });}

Sends result back to renderer process

ipc.on('readFile', readFile);   ipc.on('saveFile', saveFile);

Listens for readFile and saveFile events emitted via IPC

174

CHAPTER 9 Creating application and context menus

This code wraps filesystem API methods and attaches them to event listeners that areprovided by the IPC module, thus bridging the separate JavaScript contexts of themain process (back end) and the renderer process (front end). To complete the walk-through, we'll look next at what happens on the front end in the app.js file when a fileis read or saved.

In the app.js file, you use the same pattern of listening on events in the IPC mod-ule to intercept when a file is read ('fileRead') or saved ('fileSaved'). You thentrigger actions when those events are emitted. The next listing shows the code thathandles this.

Listing 9.15 Handling fileRead and fileSave IPC events on the front end

ipc.on('fileRead', (event, err, data) => {  loadMenu(true); if (err) throw(err); if (!done) bindClickingOnTabs(); hideSelectFileButton(); setContent(data); showViewMode('design');});

When fileRead event is emitted, loads UI for editor with that file's contents

Reports on whether save succeeded or not

ipc.on('fileSaved', (event, err) => {  if (err) return alert('There was an error saving the file'); alert('File Saved');});

This code demonstrates that you can send data from the front end to the back endand back, as long as the front-end code is set up to listen on events that are emitted bythe back end.

With all this in place, you're able to display the UI for the editor with a fileloaded and allow users to insert images or videos by right-clicking the HTML file indesign mode.

9.2.5

Adding the context menu with ElectronThe code for the context menu is similar to the NW.js example, but differs in a fewplaces. The following is a snippet of the code from the designMenu.js file:

function initialize () { const menu = new Menu(); menu.append(new MenuItem({label: 'Insert image', click: insertImage })); menu.append(new MenuItem({label: 'Insert video', click: insertVideo })); document.querySelector('#designArea') .addEventListener('contextmenu', function (event) {  event.preventDefault();  x = event.x;  y = event.y;  menu.popup(event.x, event.y);  return false; });}

Summary

175

You can see that Electron offers a similar API for appending menu items to a menu.The process is also identical in the way that the menu is able to appear.

HOW DOES ELECTRON HANDLE CALLING PROMPT()? Electron doesn't support theprompt() browser call, which shows a dialog with a text field. Cheng Zhao hassaid that because the feature would require a lot of work to implement andbecause the feature is rarely used, he won't implement it. In order to supportusing the prompt in Electron, you can use the dialog's npm module, availableat www.npmjs.com/package/dialogs.

9.3

SummaryThis chapter covered how to implement app window menus and context menus withNW.js and Electron. Some key takeaways from the chapter include the following:

 There are different API methods for handling the different ways that Windows/Linux and Mac handle app menus. The best strategy is to use OS detection tosupport both approaches.

 To implement context menus, you'll want to override the app's contextmenu

DOM event.

 When you want app window menu items to manipulate contents in the browser

window, use Electron's IPC APIs to facilitate transmitting the data.

Important aspects to consider when you're constructing menus for your app is whetherthe menu needs to be unique for each window of the app, as well as whether the appwill be used on Macs. Mac OS has a single menu that applies to all app windows, andthis needs to be taken into account.

In chapter 10, we'll continue on the theme of the UI by looking at implementingdrag-and-drop functionality, as well as how to make the app look like it's native to theuser's OS.

Dragging anddropping files andcrafting the UI

This chapter covers Configuring drag-and-drop functionality Mimicking the native look and feel of the


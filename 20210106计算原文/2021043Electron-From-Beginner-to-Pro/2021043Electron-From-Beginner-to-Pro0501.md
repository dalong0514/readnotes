Adding Custom Menus

Menus are also something that traditional web app have never had access to. The application menus were always that of the browsers. If the user accessed a contextual menu on the page, the default browser contextual menu would appear. Web apps had no ability to change either one. However, Electron gives you full control over creating both application-level menus, as well as contextual menus.

We will explore creating both the application-level menus and the contextual menus. Electron uses the

Menu and the MenuItem modules together to create the custom menus that your application will use.

Getting Started

Let's clone a fresh copy of the Electron Quick Start example.

git clone https://github.com/electron/electron-quick-start custom-menu-demo

Next, change your active directory to electron-quick-start.

cd custom-menu-demo

Now, we need to install the dependencies:

npm install

Finally, reset Git with

git init

You might have noticed that our previous Electron samples already included a standard application

menu. In fact, it is a robust menu system with many of the standard functions already defined (Figure 5-1).

© Chris Griffith, Leif Wells 2017 C. Griffith, L. Wells, Electron: From Beginner to Pro, https://doi.org/10.1007/978-1-4842-2826-5_5

73

Chapter 5 ■ adding Custom menus

Figure 5-1. The default Electron menu

But if we want to have a custom menu in our application, then the creation of the entire menu must be

defined by the developer. So, let's get started building our basic application menu. Figure 5-2 shows what our final menu structure will look like on macOS.

Electron

About electron-quick-start------Services------Hide electron-quick-startHide OthersShow All------Quit

Edit

UndoRedo------CutCopyPasteSelect All------Start DictationEmoji & Symbols

Figure 5-2. Menu hierarchy diagram

View

ReloadToggle Full ScreenToggle Developer Tools------App Menu Demo

Window

MinimizeClose------Reopen Window------Being All to Front------Hello World

Help

SearchLearn More

Now the application menu is only available in the main process, so let's open the main.js file in our

editor. Within our existing constants, we will define another for our Menu module:

const Menu = electron.Menu

74

Then once our application is ready, we can attach our menu. Locate this function in main.js

Chapter 5 ■ adding Custom menus

app.on('ready', createWindow)

and replace it with this:

app.on('ready', function () { const menu = Menu.buildFromTemplate(template) Menu.setApplicationMenu(menu) createWindow()})

One of the methods in the Menu module is the ability to create a menu object from a template. Rather than append each menu item one by one, Electron gives us the ability to create a menu template and have it properly generate our menu object for us. Once we have created our menu object, we can replace the default application menu that the Electron shell provides.

if you run the application in its current state, you will encounter an error, as we have not defined a

■ Note template yet.

Menu Templates

Let's start creating our menu template. For any modest application, you will have quite a lengthy template, so we are going to build up our template in steps to ensure that the formatting is correct.

After we define the mainWindow variable, add this code block for a simple menu that will have two

top-level menus, and each with a single menu item:

let template = [{ label: 'Menu 1', submenu: [{ label: 'Menu item 1' }]}, { label: 'Menu 2', submenu: [{ label: 'Another Menu item' }, { label: 'One More Menu Item' }]}]

The menu template is an array of objects. Each object will define an individual menu that will be shown

in the application's menu bar. To define text that will be shown, we assign that value to its label property. In this code sample, we are defining two menus: Menu 1 and Menu 2.

To define the menu items – the elements that are shown when a user selects that menu – we set the submenu property to an array of menu objects. For Menu 1, we only define one menu item with a label of Menu item 1. For the second menu, Menu 2, we will define two menu items: Another Menu Item and One More Menu Item.

Before we test out our menu, we need to make a special adjustment for running on macOS.

75

Chapter 5 ■ adding Custom menus

macOS's Application Menu

Ignoring the Apple menu, which is systemwide, on macOS, the first menu item of the application menu is the application's name. Currently, this menu is labeled Electron, since that is the root application that we are using. Once we build our application for distribution, this label will reflect our actual application name. This application menu is where you will find the applications preference's menu, the ability to hide the application or other applications, and the quit menu. If we simply define our menu template without accommodating for this special menu, we will have an issue. Our first menu definition will be incorrectly displayed. The main menu label will not be shown, but the menu items will be inserted under the application menu.

To solve this, we will need to shift our menus one position if we are running on macOS. After the

template definition in the main.js file, we can add this code to offset our template if we are running on a macOS system:

if (process.platform === 'darwin') { const name = electron.app.getName() template.unshift({ label: name, submenu: [{  label: 'Quit',  accelerator: 'Command+Q',  click: function () {  app.quit()  } }] })}

This will only adjust our menu structure. The traditional menu items that we typically would see in this

menu will not be there. However, we did include the Quit menu item to make working with this sample a bit easier. We will address adding in the rest of the menu items for the macOS application menu later in the chapter. For now, let's explore expanding our menus.

Defining Keyboard Shortcuts and Menu Item Roles

Let's replace our simple menu template with one that is more complex, like a standard Edit menu. Here is the template we will use:

let template = [{ label: 'Edit App', submenu: [{ label: 'Undo', accelerator: 'CmdOrCtrl+Z', role: 'undo' }, { label: 'Redo', accelerator: 'Shift+CmdOrCtrl+Z', role: 'redo' }, { type: 'separator' }, {

76

Chapter 5 ■ adding Custom menus

label: 'Cut', accelerator: 'CmdOrCtrl+X', role: 'cut' }, { label: 'Copy', accelerator: 'CmdOrCtrl+C', role: 'copy' }, { label: 'Paste', accelerator: 'CmdOrCtrl+V', role: 'paste' }, { label: 'Select All', accelerator: 'CmdOrCtrl+A', role: 'selectall' }]}]

We set the top-level menu's name through using the label property. Now, standard convention for the

Edit menu is simply to call it Edit; we are changing it to Edit App so you can verify that the menu is your menu and not the predefined Electron Edit menu.

You should always follow the platform convention for keyboard shortcuts and menu naming. refer to

■ Note each platform's user interface guidelines forfurther information.

Next, we will set the submenu with an array of menu items. Let's look at the first submenu:

{ label: 'Undo', accelerator: 'CmdOrCtrl+Z', role: 'undo'}

Again, we set the menu's name through using the label property. Next, we define the accelerator. This is

an optional property, but this is how you define the keyboard shortcut for the menu item. We can listen for the following modifiers:

Alt

•	 Command (or Cmd for short)•	 Control (or Ctrl for short)•	 CommandOrControl (or CmdOrCtrl for short)•	•	 Option•	•	•

Super

AltGr

Shift

77

Chapter 5 ■ adding Custom menus

The modifier is then combined with a keycode to define our accelerator. In our snippet, our accelerator

is set to be ‘CmdOrCtrl+Z'. This means that if the user presses either the Command key or the Control key (based on the platform) and the Z key, the menu item will be triggered.

Since our Electron application will be running on a variety of platforms, we need a solution to properly

map our accelerators to the platform's conventions. For example, on Windows and Linux, there Is no Command key. But by using the CommandOrControl modifier, Electron will properly map the modifier to the correct key based on the platform.

Although the Option modifier does exist, it is recommended that you use Alt instead. The Option key

only exists on macOS, whereas the Alt key is available on all platforms.

The Super key is mapped to the Windows key on Windows and Linux and Cmd on macOS.It is also possible to combine modifiers together. Typically, this is just including the Shift modifier as an

additional keypress.

The next property that is defined is role. While many of our menu items might trigger custom actions within our application, many of them will simply map to a standard role. Rather than try to implement the behavior of each action in a click function, we can leverage the built-in role behavior.

The role property can have the following values:

undo

redo

cut

copy

paste

delete

selectall

pasteandmatchstyle

•	•	•	•	•	•	•	•	•	 minimize - Minimize current window•	•	•	•	•	•	•	•

reload - Reload the current window

close - Close current window

quit- Quit the application

resetzoom - Reset the focused page's zoom level to the original size

zoomin - Zoom in the focused page by 10%

zoomout - Zoom out the focused page by 10%

toggledevtools - Toggle developer tools in the current window

togglefullscreen- Toggle full screen mode on the current window

On OSX, the role can also have following additional values:

•	•	•	•	•

about - Map to the orderFrontStandardAboutPanel action

hide - Map to the hide action

hideothers - Map to the hideOtherApplications action

unhide - Map to the unhideAllApplications action

startspeaking - Map to the startSpeaking action

78

Chapter 5 ■ adding Custom menus

stopspeaking - Map to the stopSpeaking action

front - Map to the arrangeInFront action

zoom - Map to the performZoom action

•	•	•	•	 window - The submenu is a「Window」menu•	•

services - The submenu is a「Services」menu

help - The submenu is a「Help」menu

If you don't want to use one of the predefined roles, you can set the click property to call a custom

function

{ label: 'Generate Icon', click: doGenerateIcon}

Now when the user selects the Generate Icon menu item, our custom function doGenerateIcon will be

called. Electron will automatically pass in three parameters: menuItem, browserWIndow, and event, into our function. The menuItem parameter can be used to determine which menu item the function was called from. The browserWindow parameter will tell us which window had focus when the function was called. This is important when you have a multi-window application and need to affect something in a specific renderer view. The final parameter, event, will tell have the state of the modifier keys when the function was triggered.

on macos, if you specify a menu item's role, you can only affect the label and the accelerator.

■ Note all other menu item options are ignored.

There are several other menu item properties that you should be aware of. The first is the simple

separator. This menu item will insert the horizontal line in the menu (Figure 5-3).

{  type: 'separator' }

79

Chapter 5 ■ adding Custom menus

Figure 5-3. The Edit Menu

Creating Submenus and Checkmarks

Another menu type that you will use is the submenu. We already used it to define the menus under each menu name. But if you want to create a submenu from a menu item, this is the type you will use. After the Select All definition in our Edit App menu, let's add a demonstration of both the separator and a submenu:

{ label: 'Select All', accelerator: 'CmdOrCtrl+A', role: 'selectall' }, { type: 'separator' }, { label: 'My Submenu', submenu: [  {  label: 'Item 1'  },

80

Chapter 5 ■ adding Custom menus

{  label: 'Item 2'  } ] }

Figure 5-4 shows what this looks like.

Figure 5-4. Our custom submenu

In addition to these menu item types, there are several other properties that can be set on a menu item. These are setting the enable property. If this is set to false, the menu item will be grayed out and unclickable. To hidden a menu completely, set the visible property to false.

Often you might want to indicate that a menu item's function is active. Typically, this is shown through

using a checkmark next to the menu name (see Figure 5-5). Electron offers two methods to achieve this. The first is the checkbox type. Set the type of the menu item to ‘checkbox'. The status checkbox is set via the checked property.

{ label: 'Item 1', type: 'checkbox', checked: true}

81

Chapter 5 ■ adding Custom menus

Figure 5-5. The menuitem with a checkmark

The toggling of the checkbox will be managed completely by your application.If your menu item is a part of collection of options, where one item must always be selected, then you

can use the menu item type ‘radio'.

{ label: 'Item 1', type: 'radio', checked: false},{ label: 'Item 2', type: 'radio', checked: true}

Electron will handle the switching of the checkmark between the menu items automatically for you, but

you will still need to handle the application logic of that selection yourself.

82

Completing the macOS's Application Menu

Earlier in this chapter, we added a brief bit of code, to adjust our menus on macOS to render correctly. Now, let's return to that code block and replace it with the completed version (see Figure 5-6).

Chapter 5 ■ adding Custom menus

if (process.platform === 'darwin') { let name = 'App Name' template.unshift({ label: name, submenu: [  {  label: `About ${name}`,  role: 'about',  },  { type: 'separator' },  {  label: 'Preferences',  accelerator: 'Command+,',  click: appPrefs  },  { type: 'separator' },  {  label: 'Services',  role: 'services',  submenu: [],  },  { type: 'separator' },  {  label: `Hide ${name}`,  accelerator: 'Command+H',  role: 'hide',  }, {  label: 'Hide Others',  accelerator: 'Command+Alt+H',  role: 'hideothers',

}, {  label: 'Show All',  role: 'unhide',  },  { type: 'separator' },  {  label: `Quit ${name}`,  accelerator: 'Command+Q',  click: function () {    app.quit()    }  }] })}

83

Chapter 5 ■ adding Custom menus

Figure 5-6. The application menu on macOS

■ Note the preferences menu calls a custom function, appprefs, which is not defined; the rest of the template can rely on the built menu roles. also, our quit menu item will perform an immediate quit. if your application needs to check if a file needs to be saved, you will need to expand this function to allow for that functionality.

macOS's Window Menu ModificationsOSX also has another menu modification that is needed to align with its user interface guidelines. The ‘Window' menu has some additional menu items that need to be included, such as ‘Bring All to Front'. There is also the ability to close or minimize the current window from this menu as well.

84

Chapter 5 ■ adding Custom menus

The standard Window menu will look like this:

{ label: 'Window', role: 'window', submenu: [{ label: 'Minimize', accelerator: 'CmdOrCtrl+M', role: 'minimize' }, { label: 'Close', accelerator: 'CmdOrCtrl+W', role: 'close' }, { type: 'separator' }, { label: 'Reopen Window', accelerator: 'CmdOrCtrl+Shift+T', enabled: false, key: 'reopenMenuItem', click: function () {  app.emit('activate') } }]}

Add this new menu to our template. Since the menu templates can get very lengthy and have complex nesting, we will assign each menu to its own variable then push it onto the template array. This helps keep the code a bit more manageable.

let windowMenu = { label: 'Window', role: 'window', submenu: [{ label: 'Minimize', accelerator: 'CmdOrCtrl+M', role: 'minimize' }, { label: 'Close', accelerator: 'CmdOrCtrl+W', role: 'close' }, { type: 'separator' }, { label: 'Reopen Window', accelerator: 'CmdOrCtrl+Shift+T', enabled: false, key: 'reopenMenuItem',

85

Chapter 5 ■ adding Custom menus

click: function () {  app.emit('activate') } }]}

template.push(windowMenu)

We can then extend this base menu to include a ‘Bring All to Front' menu item, and a separator

before it. Since the template is just an array of objects, we can just select the correct index, then adjust the submenu. For our sample menu template, our Window menu is at index 2. Remember, we shifted the menus by 1 to accommodate the Application menu on macOS (see Figure 5-7).

Figure 5-7. The Bring All to Front menu inserted into the Window Menu

86

Then we simply push our two new menu items onto the submenu.

Chapter 5 ■ adding Custom menus

if (process.platform === 'darwin') { ...

template[2].submenu.push({ type: 'separator' }, {  label: 'Bring All to Front',  role: 'front' })}

Here is a complete starter menu system for your Electron application:

let template = [{ label: 'Edit', submenu: [{ label: 'Undo', accelerator: 'CmdOrCtrl+Z', role: 'undo' }, { label: 'Redo', accelerator: 'Shift+CmdOrCtrl+Z', role: 'redo' }, { type: 'separator' }, { label: 'Cut', accelerator: 'CmdOrCtrl+X', role: 'cut' }, { label: 'Copy', accelerator: 'CmdOrCtrl+C', role: 'copy' }, { label: 'Paste', accelerator: 'CmdOrCtrl+V', role: 'paste' }, { label: 'Select All', accelerator: 'CmdOrCtrl+A', role: 'selectall' }]}, { label: 'View', submenu: [{ label: 'Reload', accelerator: 'CmdOrCtrl+R', click: function (item, focusedWindow) {

87

Chapter 5 ■ adding Custom menus

if (focusedWindow) {  // on reload, start fresh and close any old  // open secondary windows  if (focusedWindow.id === 1) {   BrowserWindow.getAllWindows().forEach(function (win) {   if (win.id > 1) {    win.close()   }   })  }  focusedWindow.reload()  } } }, { label: 'Toggle Full Screen', accelerator: (function () {  if (process.platform === 'darwin') {  return 'Ctrl+Command+F'  } else {  return 'F11'  } })(), click: function (item, focusedWindow) {  if (focusedWindow) {  focusedWindow.setFullScreen(!focusedWindow.isFullScreen())  } } }, { label: 'Toggle Developer Tools', accelerator: (function () {  if (process.platform === 'darwin') {  return 'Alt+Command+I'  } else {  return 'Ctrl+Shift+I'  } })(), click: function (item, focusedWindow) {  if (focusedWindow) {  focusedWindow.toggleDevTools()  } } }]}, { label: 'Window', role: 'window', submenu: [{ label: 'Minimize', accelerator: 'CmdOrCtrl+M', role: 'minimize' }, {

88

Chapter 5 ■ adding Custom menus

label: 'Close', accelerator: 'CmdOrCtrl+W', role: 'close' }, { type: 'separator' }, { label: 'Reopen Window', accelerator: 'CmdOrCtrl+Shift+T', enabled: false, key: 'reopenMenuItem', click: function () {  app.emit('activate') } }]}, { label: 'Help', role: 'help', submenu: [{ label: 'Learn More', click: function () {  electron.shell.openExternal('http://electron.atom.io') } }]}]

Since we have now included a View menu into our template, we will adjust the index value for the Bring

All to Front menuitem by one.

template[3].submenu.push({ type: 'separator'}, { label: 'Bring All to Front', role: 'front' })

89

Chapter 5 ■ adding Custom menus

Contextual Menus

Electron can also create a context, or right-click menu, with the Menu and MenuItem modules as well. Figure 5-8 shows what a contextual menu looks like.

Figure 5-8. The contextual menu

Unlike the application menu, where a default one is included, there is no default contextual menu built in. This functionality must be completely written by us. However, since the user action occurs within the window itself, the click event is occurring within the Renderer Process. But, the Menu and MenuItem modules can only be directly used by the Main Process. We can't directly mix using APIs that are allowed in the specific processes. There are two solutions to this problem of using an API in a different process. The first solution is to leverage the Remote module. From the documentation, the remote module provides a simple way to do inter-process communication (IPC) between the renderer process (web page) and the main process.

By importing this module in the renderer.js file, we can in turn access the Menu module within our

Render process. Here is a simple contextual menu sample.

const { remote } = require('electron')const { Menu } = remote

const myContextMenu = Menu.buildFromTemplate ([ { label: 'Cut', role: 'cut' },

90

Chapter 5 ■ adding Custom menus

{ label: 'Copy', role: 'copy' }, { label: 'Paste', role: 'paste' }, { label: 'Select All', role: 'selectall' }, { type: 'separator' }, { label: 'Custom', click() { console.log('Custom Menu') } }])

window.addEventListener('contextmenu', (event) => { event.preventDefault() myContextMenu.popup()} )

The other solution is to use the IPC (Inter-Process Communication) module directly. This method

might be preferred since interactions with the contextual menu might have an impact on the application's menu. Keeping all the menu-related code in one process might make more organizational sense. Although we will cover the IPC module in detail in a later chapter, let's outline the code to show this solution.

Main Process (in main.js)

//////Contextual Menu Importsconst MenuItem = electron.MenuItemconst ipc = electron.ipcMain

...

////////Contextual Menu//////const contextMenu = new Menu()contextMenu.append(new MenuItem({ label: 'Cut', role: 'cut' }))contextMenu.append(new MenuItem({ label: 'Copy', role: 'copy' }))contextMenu.append(new MenuItem({ label: 'Paste', role: 'paste' }))contextMenu.append(new MenuItem({ label: 'Select All', role: 'selectall' }))contextMenu.append(new MenuItem({ type: 'separator' }))contextMenu.append(new MenuItem({ label: 'Custom', click() { console.log('Custom Menu') } }))

ipc.on('show-context-menu', function (event) { const win = BrowserWindow.fromWebContents(event.sender) contextMenu.popup(win)})

Renderer Process [in renderer.js]const { remote, ipcRenderer } = require('electron')const ipc = ipcRenderer

window.addEventListener('contextmenu', (event) => { event.preventDefault() ipc.send('show-context-menu')})

91

Chapter 5 ■ adding Custom menus

In this code sample, we are recreating the same menu from our first contextual menu sample using the direct menu style. Then we create an IPC event listener. This listener will listen for our custom event, ‘show-context-menu'. It will then resolve from which window our message came from, then trigger the contextual menu using the popup method.

On the Renderer process, we have the same event listener for the contextmenu event. But instead of directly

triggering the menu, we use the IPC send command to broadcast our custom event to the Main process.

Summary

In this chapter, we have explored the various options you have when creating your application's menu system. We covered how to assign key commands, or accelerators, to menu items; how to enable or disable an menuitem; and how to have it trigger either prebuilt actions or custom code.

We also briefly looked at how to have custom context, or right-click, menus with our Electron

application, giving it one more layer of a ‘native' feel.

92

CHAPTER 6


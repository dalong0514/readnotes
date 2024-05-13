Summary

This concludes our journey together through this book. We tried to cover many of the various parts of Electron and its supporting technologies at a reasonable depth and in an order that made sense. There is nowhere near enough space or time for this book to cover each and every part of Electron, but this should give you a very strong base on which to rapidly build amazing, sleek, and performant desktop applications. Keep trying new things, and join us in the journey of making Electron a great framework!

265

Index

 AAuto updates

build application, 251generate an update, 251Heroku, 248macOS, 245server options, 248signing your application, 250testing, 250update server, 249user feedback, 247windows applications, 252

downloaded dialog, 260Electron Builder, 260generate an update, 259No Update dialog, 258sign in, 254Squirrel Installer, 255

 BBrowserWindow

argument

alwaysOnTop property, 60basic window properties, 59frameless window, 66movable properties, 60ready-to-show' event, 58resizable property, 60title property, 61transparent window, 70center, x and y properties, 59

Chrome DevTools, 54code updation, 56show() method, 56

 CChrome Dev tools, 54, 200

debug menu, 200extensions, 206

Chromium, 2createWindow method, 54, 56

 DDebugging, main process

node-inspector, 204target option, 203in VS Code, 201

Devtron

accessibility audit, 212description, 207event listeners, 209IPC monitor, 210linter, 211Require Graph pane, 208user interface, 207

Dialog module, 103

BrowserWindow parameter, 110error dialogs, 127file directories, 115

delete, 116read, 116

file open dialog, 103file selection, 108message dialog, 119

callback function, 127custom icons, 125error type, 120on macOS, 123showMessageBox method, 120warning type, 121Node's FS module, 112

access flag values, 112delete, 115file information, 113fs.watch() method, 115open method, 112to read, 114to write, 114

showOpenDialog

properties, 105–106

© Chris Griffith, Leif Wells 2017 C. Griffith, L. Wells, Electron: From Beginner to Pro, https://doi.org/10.1007/978-1-4842-2826-5

267

Dialog module (cont.)

showSaveDialog method, 116title property, 107

Dock icon, 159

Apple's Human Interface Guidelines, 161application setting, 160badges, 165bounce, 163change icon, 165npm start command, 160, 162package.json file, 160

 EElectron

advantages, 4APIs, 263

ClientRequest (main process), 263community resources, 264crashReporter (both processes), 263desktopCapturer (renderer process), 263DownloadItem (main process), 264electron forge, 264.net (main process), 264

beyond sandbox, 5chromium, 2definition, 1FlexBox support table, 4main process, 6, 44node, 2NW.js, 7overview, 2package.json file creation, 42render process, 6, 48window title properly, 63

Electron Builder, 231

app icon configuration, 238

macOS DMG, 238windows installer, 239configuration options, 233directory structure, 231dist directory, 236Linux on macOS, 233OSX installer window, 237package.json file, 232testing, 235windows on macOS, 233

 F, GFinding locales, 156Frameless window, 66

268

 HHeroku, 248

 I, J, KInstallation, 9

electron, 38git, 20Node, 9

Inter-process communication (IPC)

module, 93, 189, 224asynchronous message, 98communication bridge, 93event listeners, 101synchronous message, 94

 LloadURL method, 55

 M, NMenus, 73

additional values, 78checkmark, 82contextual menu, 90edit, 80hierarchy diagram, 74keyboard shortcuts, 77macOS's application, 76, 83modifier, 78role property, 78submenus, 80super key, 78templates, 75window modification, 84

 O, POnline/offline detection

checkIsOnline method, 188checkOnlineStatus method, 187combined approach, 187main process, 183render process, 176updateOnlineStatus

method, 187

 QQuick Start code, 41

 RRenderer process, 223–224

 SScreens, 152Shell, 169

package.json file, 170shell.beep, 170shell.beep method, 170shell.openExternal(filePath)

method, 173

shell.openItem(filePath) method, 172shell.showItemInFolder(filePath)

method, 171

Spectron testing, 212, 214

add test.js file, 215browserWindow API, 218click method, 227describe method, 216getWindowCount method, 217log statement, 223package.json file, 214project creation, 224renderer process, 223screen size, 222window.webContents.send()

method, 226

Splash window, 189file creation, 191installation, 190load main window, 196renderer.js file, 197set up, 190version number, 193

 TTransparent window, 70

 U, Vurl.format() method, 48

 W, X, Y, ZWebContents

capturePage method, 144createWindow() method, 134did-finish-load event, 141did-start-loading event, 139, 141empty array, 131events, 137getAllWebContents() method, 130imageCaptured method, 146overview, 130printToPDF method, 149

269


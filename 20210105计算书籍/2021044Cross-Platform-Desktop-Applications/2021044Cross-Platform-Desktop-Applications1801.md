OS apps.

These tools go a long way toward helping you to provide a smooth installationexperience for your users. Bear in mind that there currently aren't any major buildingtools in the NW.js and Electron space that simplify turning built Linux executablesinto packages for Yum, YaST, and Apt. That's something you'll have to do manually.

appendixInstalling Node.js

There are a couple of different ways to install Node.js, but the simplest way to get itinstalled is by visiting https://nodejs.org and clicking the Downloads link in the topnavigation bar. You'll see a page of download options for different operating sys-tems. If you're running Windows or Mac OS, you can choose to download one ofthe installers available. If you're running Linux, you can either download a tarballof the source code and compile it or install it via a package manager. For instruc-tions on using a Linux package manager to install Node.js, take a look at https://nodejs.org/en/download/package-manager.

INSTALLING MULTIPLE VERSIONS OF NODE.JS WITH NVM Another option fordevelopers running Mac OS X or Linux is to use nvm (Node Version Man-ager) to handle installing Node.js. nvm allows you to install multiple ver-sions of Node.js on your computer and then switch between the differentversions. This is very useful when you want to test how your code runsagainst newer versions of Node.js. It also enables you to work on multipleNode.js applications that are running different versions of Node.js. Formore on nvm, visit https://github.com/creationix/nvm.

316

index

for Microsoft Windows OS applications

158–164

applications

accessing clipboard

with Electron 215–218with NW.js 211–215

creating desktop notifications

in Electron 235–239in NW.js 239–242

creating executables for Linux OS 311–315

creating executables for Mac OS 306–311

with Electron 313–315with NW.js 312

with Electron 309–311with NW.js 306–308

creating executables for Windows OS 292–296

building .exe with NW.js 293–294installing virtual machine 292–293with Electron 294–296with NW.js 292

creating setup installer for Windows 296–306

creating using LocalStorage API 200–206

with Electron 304–306with NW.js 296–304

with Electron 201–204with NW.js 204–206

dragging and dropping files onto 176, 180–186

with Electron 180with NW.js 177–179

finding packages for 103frameless 128–133, 138–142creating in NW.js 134–137creating with Electron 137–138

full-screen 128–142

in Electron 131–133in NW.js 128–131

Symbols

^ (caret character) 105/ (forward slash) 69=> function 19

A

Aboukhadijeh, Feross 5acceptance testing 247addContextMenu 169addEventListener 99addStylesheet function 182addToIndex function 64, 254–255After hook 260APIs (application program interfaces)

accessing via JavaScript 14common methods in Chromium 116common methods in Node.js 116public methods, creating with

module.exports 100–101

App folder, in Electron 113app.css file 39, 148, 150appdmg module 307appendNoteToMenu function 147Application class, Spectron 257application program interfaces. See APIsapplication window menus 154–164

choosing which menu to render based on

OS 164

creating 153–175

for Linux OS applications 158–164for Mac OS applications with Electron

for Mac OS applications with NW.js

155–157

154–155

317

318

INDEX

applications (continued)

games

creating global keyboard shortcuts with

Electron 231–233

creating with NW.js 220–230

kiosk 138–142

creating in NW.js 138–140creating with Electron 140–142

packaging 291–315

creating executables for Linux OS

creating executables for Mac OS 306–311creating executables for Windows OS

creating setup installer for Windows OS

311–315

292–296

296–306

packaging with npm 105–107publishing to npm 106–107running in Electron 114standalone

creating for Linux OS with Electron

313–315

creating for Linux OS with NW.js 312

storing data 199–209

choosing from available options 199–200creating applications using LocalStorage

API 200–206

porting to-do list web applications 206–209See also default applications; web applications;

tray applications

applyDiscount function 101architecture, of Node.js in NW.js 115asar tool 294assert library 252async module 45–46asynchronous programming, versus synchronous

programming 92–94

Atom Shell 8Audits tab, Developer Tools window 269Ava 254Axisto Media 131

B

bar element 221BDD (behavior-driven development) 247–248bindDocument function 57binding, on keyboard shortcuts 219–233

creating games with NW.js 220–230creating global keyboard shortcuts with

Electron 231–233

bindSavingPhoto function 189–190, 195bindSearchField function 64, 66, 255BitTorrent 6Blink rendering engine 109

blocking 92body element 221body tag 123, 276breakpoints 273Bring All to Front command, Window menu 155browser development tools 267–270Browser folder, in Electron 113BrowserWindow class 126–127, 133bugs, identifying root cause 265–270

debugging with browser developer tools

267–270

identifying location of 266See also debugging

build tools

using for Electron 80–81using for NW.js 79button element 237

C

callback 93canvas element 189, 191, 221caret character 105Cascading Style Sheets. See CSSChrist, Adam 28ChromeDriver, functional testing with 256Chromium 110

and Node.js, bridging JavaScript context

between 112

common API methods in 116

class attribute 70classNames variable 209clearBreakpoint() function 273clearView function 59click attribute 162clipboards

accessing 211–218

creating applications with Electron

215–218

creating applications with NW.js 211–215copying and pasting contents from 210–218setting content with Electron 218

clipboard.writeText 217Close Window command, Window menu 155code, refactoring 55–58codebase, building applications for multiple

OSs 16

CoffeeScript 105cog icon 267CommandOrControl 232Common folder, in Electron 114CommonJS 100config.example.js file 237config.js file 237console method 116

INDEX

319

with NW.js developer tools 275–279

with Node.js 271–275

Node debug 272–273remotely 273–275

Console tab 277Elements tab 276Sources tab 277–279

default applications, opening files with 71–74defaultMenu() function 157Delete command, Edit menu 155denormalized data 200dependencies, controlling versions in

package.json 105–106

See also development dependencies

describe function 250designing UI, mimicking native look of OS

180–186

designMenu.js file 166desktop applications 31–74

building example application 31–33configuring window dimensions in

using Electron 123–124using NW.js 122–123

controlling display 121–142

frameless applications 128–133, 138–142full-screen applications 128, 131, 133–142kiosk applications 138–142window sizes and modes 121–128

creating 33–37

creating files and folders for Electron-powered

applications 35–37

creating files and folders for NW.js-powered

applications 33–35installing Electron 33installing NW.js 33creating icons 76–79in Linux OS 78–79in Mac OS 76–77in Microsoft Windows OS 78enhancing navigation in 68–74

loading at folder path 71making current folder path clickable 68–71opening files with default applications

71–74

folders 55–61

handling double-clicks on 58–61refactoring code 55–58

implementing quick search 62–68

adding in-memory search libraries 63–64adding search fields to toolbars 62–63adding search functionality to UI 64–68

implementing start screen 38–53

displaying user's personal folders in

toolbars 38–42

Console tab

Developer Tools window 269in NW.js 277

console.log statements 94, 98, 277const variable 19contenteditable attribute 205context menus 165–175adding icons 170–171creating 153–175with Electron

adding 174–175creating 171–174with NW.js 169–170

contextmenu event 170convertFolderPathIntoLinks function 69–70Copy command, Edit menu 155copying and pasting, contents from

clipboards 210–218

copyPhraseToClipboard function 213CSS (cascading style sheets)

adding for personal folders 39–40using to match user's OS style 183–186

Linux 184Lion CSS UI Kit 184Metro UI 183Photon 185–186React Desktop 186

Cucumber

overview 258–259testing Electron applications with 260–263

cucumber-js command 262cuke.js file 262currentFile variable 277current-folder element 59–60, 70currentState variable 229Cut command, Edit menu 155

D

Dahl, Ryan 91data persistence 204data, storing 199–209

choosing from available options 199–200creating applications using LocalStorage

API 200–206

porting to-do list web applications

206–209

debugging 264, 270–290

Electron applications 284–290identifying root cause 265–270resolving performance issues 279–283

Network tab 279–280Profiles tab 282–283Timeline tab 280–281

with browser development tools 267–270

showing user's files and folders in UI 42–53

320

INDEX

desktop applications (continued)

Node.js 4–7overview 4–6packaging for distribution 79–85

setting icons on applications 81–85using build tools for Electron 80–81using build tools for NW.js 79preparing for distribution 76–79setting icons 81–85

in Linux OS 85in Mac OS 81–82in Microsoft Windows OS 82–84

shipping 75–88

packaging for distribution 79–85preparing for distribution 76–79testing on multiple OSs 86–88

testing 245–263

approaches to 246–249functional testing 255–256integration testing 258–263levels of 248–249on Linux OS 87on Mac OS 87–88on Microsoft Windows OS 86–87on multiple OSs 86–88TDD 246–247unit testing 249–255

See also applications

desktop notifications 234–242detecting OS

in Electron 182–183in NW.js 181–182

Console tab 277Elements tab 276Sources tab 277–279See also browser development tools

development dependencies, installing 104Devtron, debugging Electron applications

with 285–290

Event Listeners 287IPC 288–289Linting 289–290Require Graph 286–287

directory type 47displayFile function 57, 59, 65, 72displayFolderPath function 59, 68, 70–71displayImageInIconSet function 178–179displayNote function 147, 151distributing

packaging desktop applications for

79–85setting icons on applications 81–85using build tools for Electron 80–81using build tools for NW.js 79

developer tools, debugging in NW.js 275–279

163–164

preparing desktop applications for

76–79

div element 48, 51, 170, 189, 221–222done function 252dotfiles 52drag-and-drop functionality, using with files 176,

180–186

with Electron 180with NW.js 177–179

draggable apps 135drawSnake function 226

E

E2E (end-to-end testing) 258Electron 3–17, 24–30

application creation with

accessing clipboard 215–218desktop notification applications

235–239

for Linux OS 313–315for Mac OS 309–311for Windows OS 294–296, 304–306frameless applications 137–138kiosk applications 140–142tray applications 149–152using LocalStorage API 201–204Watchy application 235–239

application window menus

creating for Linux OS 163–164creating for Mac OS 155–157creating for Microsoft Windows OS

applications created with 24–30

Hyper 29–30Light Table 25Macaw 28Slack 24

building Node.js desktop applications 4–7

overview of desktop applications 4–6versus web applications 6–7

capturing photos with HTML5 Media

Capture API 194–198components of 113–114

App folder 113Browser folder 113Common folder 114Renderer folder 113

configuring window dimensions in

applications 123–124

constraining window dimensions in

126–128

context menus

adding 174–175creating 171–174

INDEX

321

Electron (continued)

creating global keyboard shortcuts with

fileMenuSubMenu 161–162fileRead event 174files

debugging applications 284–290dragging and dropping files onto applications

clicking on 72–74creating for Electron-powered applications

231–233

with 180

exploring 108–117features of 23–24full-screen applications in 131–133Hello World application in 18–22history of 7–9installing 33interacting with Node.js 115–117Node.js used within 116–117overview 112–114porting TodoMVC web app with 208–209running applications 114setting content to clipboard with 218testing applications with

Cucumber 260–263Spectron 256–258, 260–263

using build tools for 80–81versus NW.js 17–18electron-packager 313Elements tab

Developer Tools window 268in NW.js 276

encodeURIComponent method 116err object 94EULA (End User License Agreement) 87event emitters 114Event Listeners menu, in Devtron 287event loops, integrating main 111EventEmitter module 99EventMachine 99events, in Node.js 99–100executables

creating for Linux OS 311–315

with Electron 313–315with NW.js 312

creating for Mac OS 306–311

with Electron 309–311with NW.js 306–308

creating for Windows OS 292–296

building .exe with NW.js 293–294installing virtual machine 292–293with Electron 294–296with NW.js 292

executeMove function 225

F

Facebomb-Electron 188Facebomb-NW.js 188file type 47

35–37

creating for NW.js-powered applications 33–35dragging and dropping onto applications 176,

180–186with Electron 180with NW.js 177–179

opening with default applications 71–74user's personal, showing in UI 42–53

fileSave event 174fileSystem module 58fileSystem.js file 55filterResults function 66, 255find function 64, 254folderExplorer.test.js file 256folders 55–61

creating for Electron-powered applications

35–37

creating for NW.js-powered applications 33–35handling double-clicks on 58–61looking at path 71making current path clickable 68–71refactoring code 55–58user's personal

adding CSS for 39–40adding HTML for 38–39discovering with Node.js 40–42displaying in toolbars 38–42showing in UI 42–53Font Awesome library 171forked dependencies 110form element 237forward slash 69frame property 134frameless applications 128–133, 138–142

creating in NW.js 134–137creating with Electron 137–138

free RAM 95front-end code 55fs.createReadStream method 98–99fs.fileRead function 98fs.readFile method 97fs.stat function 45full-screen applications 128–142

in Electron 131–133in NW.js 128–131

fullscreenable property 131functional testing 249, 255–256

in practice 255with ChromeDriver 256with NW.js 256

322

G

Game Dev Tycoon 26–27games

Electron, creating global keyboard shortcuts

with 231–233

NW.js

229–230

creating global keyboard shortcuts with

creating with 220–230implementing window focus keyboard short-

cuts with 227–229

Gantt charts 94getFilesInFolder function 44, 56getUsersHomeFolder method 43, 56Giannattasio, Tom 28Gifrocket 177GitHub 113, 123, 137Gitter 27, 122global object 116globalShortcut API 231–232goFullScreen function 130Granger, Chris 25Grunt-build-atom-shell 313GUI library, NW.js 159gui.Window.get() function 160

H

hasEatenItself function 223hasPoint function 222height property 194Hello World application

creating 10–13in Electron 18–22in NW.js 9–13

creating Hello world application 10–13installing NW.js 10

hello-world-nwjs folder 11–12Herbert, Frank 96hidden folders 52HTML (Hypertext Markup Language) 38–39HTML5 Media Capture API, capturing photos

with 187–198

using Electron 194–198using NW.js 188–193

Hyper terminal app 29–30, 133Hypertext Markup Language. See HTML

I

icon attribute 171Iconic app 177Iconic Electron app 180icon.icns file 82

INDEX

icons

adding to context menus 170–171creating for desktop applications 76–79

in Linux OS 78–79in Mac OS 76–77in Microsoft Windows OS 78

setting on desktop applications 81–85

in Linux OS 85in Mac OS 81–82in Microsoft Windows OS 82–84

tray, adding menus to 145–149

iConvert Icons 77–78icudtl.dat file 312identifying bugs 265–270

267–270

location of 266

debugging with browser developer tools

image_steps.js file 261img element 65IndexedDB 200index.html file 34Info.plist file 157init command 221initialize function 168, 190–191, 196–197, 205, 227in-memory search libraries, adding 63–64innerHTML function 70Inno Setup 297, 299input element 188–189, 191, 195–196input field 237input tag 62inspectAndDescribeFile function 56install command 102installing

development-only dependencies 104Electron 33Node.js 316NW.js 10, 33virtual machine 292–293

integration testing 249, 258–263

with Cucumber 260–263with Spectron 260–263

interceptDroppedFile function 178IPC (inter-process communication) 288–289ipcMain module 114, 172ipcRenderer module 114, 151, 172, 232isFullscreen function 130

J

jank 281JavaScript

accessing API via 14accessing OS native UI via 14bridging context between Node.js and

Chromium 112

INDEX

323

creating submenus 160–163setting icons on applications in 85standalone applications for

with Electron 313–315with NW.js 312

testing desktop applications on 87

Lion CSS UI Kit 184loadDirectory function 59–60, 65loadedmetadata event 190, 196loadFolder function 69loadMenuForMac OS function 164loadMenuForWindowsAndLinux function 164LocalStorage API, creating application using

200–206

with Electron 201–204with NW.js 204–206

lodash module 103–104loops. See event loopsLorikeet app 250Lorikeet file explorer 32–33Lorikeet wireframe 38lorikeet-electron folder 35lorikeet.exe file 83lorikeet-test-nwjs 250Lovefield 200lunr.js 63

M

Mac OS (operating system)

creating application executables for 306–311

creating application window menus

with Electron 309–311with NW.js 306–308

with Electron 155–157with NW.js 154–155

creating desktop application icons for 76–77setting icons on applications in 81–82testing desktop applications on 87–88

JetBrains 183JSON.parse() function 206, 208JSON.stringify() function 206, 208

K

keyboard shortcuts 140binding on 219–233

creating games with NW.js 220–230creating global keyboard shortcuts with

Electron 231–233

global

creating with Electron 231–233creating with NW.js 229–230

window focus, implementing with NW.js

227–229

keyup event 64kiosk mode applications 138–142

creating in NW.js 138–140creating with Electron 140–142

Kitematic 133Klug, Daniel 26Klug, Patrick 26

L

leaveFullscreen function 130leaveKioskMode function 139Let Me Remember application

creating with Electron 201–204creating with NW.js 204–206

let variable 19let-me-remember-electron 200let-me-remember-nwjs 200LevelDB 200libchromiumcontent 113libffmpegsumo.so file 312libraries

adding in-memory search 63–64loading via require function 101–102

libuv 92, 109Light Table 25link tag 182linting code 285

in Devtron 289–290

Linux OS (operating system)

creating application executables for 311–315

creating application window menus 158–164

with Electron 313–315with NW.js 312

with Electron 163–164with NW.js 158

Macaw 28main process 18main property 36makeFoodItem function 223manifest file 33max_height property 125max_width property 125menu bars, creating 158–160Menu object 146, 154menuBar 161menuItem objects 146–147menu.popup function 170menus

creating desktop application icons for

78–79

creating menu bars 158–160

adding to tray icons 145–149choosing which to render based on OS 164See also application window menus

324

INDEX

message passing 116MessageLoop 111MessagePump 111Metro UI CSS 183Microsoft Windows OS (operating system)

building .exe of NW.js applications for

293–294

creating application window menus 158–164

with Electron 163–164with NW.js 158

creating desktop application icons for 78creating Electron application executables

for 294–296

creating menu bars 158–160creating NW.js application executable for 292creating setup installer for applications

296–306with Electron 304–306with NW.js 296–304

creating submenus 160–163setting icons on applications in 82–84testing desktop applications on 86–87

min_height property 125Minimize command, Window menu 155Minimongo 200min_width property 125Mocha, writing tests with 249–251module 151module.exports, creating public API methods

with 100–101

modules

in Node.js 100–102

creating public API methods with

module.exports 100–101

loading libraries via require function

101–102

packaging with npm 105–107publishing to npm 106–107tracking installed with package.json 103–104

moveSnake function 225

N

navigation, in desktop applications 68–74

loading at folder path 71making current folder path clickable 68–71opening files with default applications

71–74NeDB 200Network tab, Developer Tools window 269New Bamboo 63, 219Nightingale, Oliver 63node debug command 274Node debug, in Node.js 272–273node package manager. See npm

node_bindings feature 116Node.js

and Chromium, bridging JavaScript context

between 112

common API methods in 116context accessible to all windows 115–116desktop applications 4–7

overview 4–6versus web applications 6–7

discovering personal folders with 40–42drawbacks of using in NW.js 115–116

common API methods in Chromium 116common API methods in Node.js 116Node.js context accessible to all

windows 115–116

events 99–100in NW.js architecture 115installing 316interacting with Electron 115–117interacting with NW.js 115–117modules 100–102

creating public API methods with

module.exports 100–101

loading libraries via require function

101–102npm 102–107

finding packages for applications 103packaging applications with 105–107packaging modules with 105–107tracking installed modules with

package.json 103–104

overview 92–102synchronous programming versus asynchro-

nous programming 92–94

used within Electron 116–117using debugger 271–275Node debug 272–273remotely 273–275

using in Electron 91–107using in NW.js 91–107using modules inside applications 14–16using streams to handle data 95–99node_modules folder 41, 63, 102–106node-webkit 7–9, 110note object 147notifications, desktop 234–242

creating applications in Electron 235–239creating applications in NW.js 239–242

npm (node package manager) 102–107finding packages for applications 103packaging applications with 105–107controlling dependency versions in

package.json 105–106

publishing applications to npm 106–107publishing modules to npm 106–107

npm (node package manager) (continued)

packaging modules with 105–107

controlling dependency versions in

package.json 105–106

publishing applications to npm 106–107publishing modules to npm 106–107

publishing applications to 106–107publishing modules to 106–107tracking installed modules with

package.json 103–104installing development-only

dependencies 104

npm command 41npm init command 215npm install command 201, 240npm module 157npm run command 305npm run dist command 310npm shrinkwrap command 106npm start command 213, 215, 236nw command 160, 162, 207, 270nwbuild command 16, 79, 84nw-builder tool 16, 79NW.js 3–9, 16–30

application creation with

accessing clipboard 211–215desktop notification applications 239–242for Linux OS 312for Mac OS 306–308for Windows OS 292frameless applications 134–137kiosk applications 138–142tray applications 144–149using LocalStorage API 204–206Watchy application 239–242

application window menus

creating for Linux OS 158creating for Mac OS 154–155creating for Microsoft Windows OS 158

applications created with 24–30

Game Dev Tycoon 26–27Gitter 27Light Table 25Macaw 28

applications, creating files and folders for

33–35

INDEX

325

capturing photos with HTML5 Media Capture

API 188–193

configuring window dimensions in

applications 122–123

constraining window dimensions in 124–126context menus 169–170creating games with 220–230

creating global keyboard shortcuts 229–230implementing window focus keyboard

shortcuts 227–229

creating setup installer for Windows

applications 296–304

with 177–179

drawbacks of using Node.js in 115–116

common API methods in Chromium 116common API methods in Node.js 116context accessible to all windows 115–116

exploring 108–117features of 14–16

accessing API via JavaScript 14accessing OS native UI via JavaScript 14building applications for multiple OSs from

single codebase 16

using Node.js modules inside

applications 14–16

using npm modules inside applications

14–16

full-screen applications in 128–131functional testing with 256Hello World application in 9–13

creating Hello world application 10–13installing NW.js 10

history of 7–9installing 10, 33integrating main event loop 111interacting with Node.js 115–117overview 109–112porting TodoMVC web app with 207–208using build tools for 79using developer tools to debug

applications 275–279Console tab 277Elements tab 276Sources tab 277–279

using V8 110versus Electron 17–18

using modules inside applications 14–16

dragging and dropping files onto applications

architecture of, Node.js in 115bridging JavaScript context between Node.js

nw.pak file 312nwsaveas attribute 188–189, 195

and Chromium 112

building .exe of applications for Windows

OS 293–294

building Node.js desktop applications 4–7

overview of desktop applications 4–6versus web applications 6–7

O

ondragover event 178ondrop event 178onKeyUp attribute 206

326

INDEX

openFile function 72–73openSUSE 12OS (operating system)

accessing native UI via JavaScript 14building applications for multiple from single

codebase 16

choosing which menu to render based on 164detecting 181

in Electron 182–183in NW.js 181–182

mimicking native look of

detecting user's OS 181using CSS 183–186using OS detection in Electron 182–183using OS detection in NW.js 181–182multiple, testing desktop applications on

86–88

See also specific operating systems

osenv module 40–41os.release() function 182

P

package.json

controlling dependency versions in 105–106tracking installed modules with 103–104

package.nw file 294packages, finding for applications 103packaging

applications 291–315

for Linux OS 311–315for Mac OS 306–311for Windows OS 292–306

applications with npm 105–107

controlling dependency versions in

package.json 105–106

publishing applications to npm 106–107publishing modules to npm 106–107

desktop applications for distribution 79–85

setting icons on applications 81–85using build tools for Electron 80–81using build tools for NW.js 79

modules with npm 105–107

controlling dependency versions in

package.json 105–106

publishing applications to npm 106–107publishing modules to npm 106–107

Paste command, Edit menu 155pasting. See copying and pastingpath class 70path separator 69pauseKeyOptions variable 230Pearls application, creating

with Electron 215–218with NW.js 211–215

performance, resolving issues with 279–283

Network tab 279–280Profiles tab 282–283Timeline tab 280–281

photoData variable 189–190, 196Photon 185–186photos, capturing with HTML5 Media Capture

API 187–198

using Electron 194–198using NW.js 188–193

Pimenov, Sergey 183Pixelmator 145plugins 29.png icon 145porting

to-do list web applications 206–209TodoMVC web applicationwith Electron 208–209with NW.js 207–208

PouchDB 200preventDefault function 178process.exit function 162process.hrtime function 98process.memoryUsage function 98Profiles tab, Developer Tools window 269prompt() function 175

Q

quick search, implementing 62–68

adding in-memory search libraries 63–64adding search fields to toolbars 62–63adding search functionality to UI 64–68

quit() function 203, 205quitAppMenuItem 161–162

R

rcedit 296React Desktop 186React framework 207readdir function 43, 94readdirSync function 93readFile function 97, 99README.md file 10, 18readText function 218red-green refactoring 246Redo command, Edit menu 155refactoring code 55–58Renderer folder, in Electron 113renderer process 18rendering menus, choosing based on

OS 164

require function 101–102, 116Require Graph, in Devtron 286–287

require method 101, 270resetFilter function 66, 255resetIndex function 64, 255Resource Hacker 82–84Resources tab, Developer Tools window 269root cause analysis 265RTF (Rich Text Format) 97

S

saveFile variable 196saveNotes function 203, 206savePhoto function 196–197sayHelloMenuItem 161–162Schlueter, Isaac 40screens. See start screensscript tag 159Script Wizard 297–298, 301–303scripts field 236search

adding in-memory library 63–64adding to UI 64–68fields, adding to toolbars 62–63See also quick search

search function 238–239search.test.js file 253Select All command, Edit menu 155SemVer (semantic versioning) 34setBreakpoint() function 273setItem function 206setTimeout method 116setup installer, creating for Windows OS

applications 296–306with Electron 304–306with NW.js 296–304

shipping desktop applications 75–88

packaging for distribution 79–85preparing for distribution 76–79testing on multiple OSs 86–88

Shortcut class 230shortcuts. See keyboard shortcutsshowSaveDialog function 197Slack 24, 122Snake game

Electron, creating global keyboard shortcuts

with 231–233

NW.js

229–230

creating global keyboard shortcuts with

creating with 220–230implementing window focus keyboard short-

cuts with 227–229

snake-electron 220snake-nwjs 220Socketstream 206

INDEX

327

Sources tab

Developer Tools window 269in NW.js 277–279

span tag 69–70Spectron

automatically testing 260–263overview 24testing Electron applications with 256–258

SQLite 200standalone applications, creating for Linux OS

with Electron 313–315with NW.js 312

start function 112, 215, 227–228start screens, implementing 38–53

displaying user's personal folders in

toolbars 38–42

showing user's files and folders in UI

42–53

startTime variable 98storing data 199–209

choosing from available options 199–200creating applications using LocalStorage

API 200–206with Electron 201–204with NW.js 204–206

porting to-do list web applications 206–209

porting TodoMVC with Electron

208–209

porting TodoMVC with NW.js 207–208streams, with Node.js to handle data 95–99structured data, storing 208stub out 252stylesheets, CSS 180styling 50submenus, creating 160–163Synaptic 311synchronous programming, versus asynchronous

programming 92–94

T

takePhoto function 190, 197TDD (test-driven-development) 246–247template tag 212termFound variable 97testing

approaches to

BDD 247–248Electron applications with Spectron

256–258

desktop applications 245–263

on Linux OS 87on Mac OS 87–88on multiple OSs 86–88on Windows Microsoft OS 86–87

328

testing (continued)

Electron applications with Spectron

256–258

functional testing 255–256

in practice 255with ChromeDriver 256with NW.js 256

integration testing 258–263

automatically testing Electron applications

with Cucumber 260–263

automatically testing Electron applications

with Spectron 260–263

introducing Cucumber 258–259

levels of 248–249unit testing 249–255

implementing 251–255writing with Mocha 249–251

textarea element 202–203, 205–206Thoughtbot 63, 219Timeline tab, Developer Tools window 269<title> element 35to-do list web applications, porting 206–209porting TodoMVC with Electron 208–209porting TodoMVC with NW.js 207–208

TodoMVC web application

porting with Electron 208–209porting with NW.js 207–208toggleFullScreen function 130toggleKiosk function 141togglePauseState function 229, 232toolbars

adding CSS for 39–40adding HTML for 38–39adding search fields to 62–63displaying user's personal folders

in 38–42adding CSS for personal folders 39–40adding CSS for toolbars 39–40adding HTML for personal folders

38–39

adding HTML for toolbars 38–39discovering personal folders with

Node.js 40–42

touch command 34touch search.js command 63tracking, installed modules with

package.json 103–104

tray applications

building initial skeleton 149–152creating 143–152

with Electron 149–152with NW.js 144–149

tray icons, adding menus to 145–149Tumbleweed edition, OpenSUSE 163TypeScript 103

INDEX

U

UI (user interface)

adding search functionality to 64–68designing 176–186showing files and folders in 42–53

Undo command, Edit menu 155unit testing 249–255

implementing 251–255writing with Mocha 249–251

updateScore function 222useContentSize attribute 194–195userInterface.js file 55–57, 59–60, 64, 66,

68–72

users

displaying personal folders in toolbars

38–42adding CSS 39–40adding HTML 38–39discovering personal folders with

Node.js 40–42

showing files and folders in UI 42–53

UX (user experience) 7

V

V8, using with NW.js 110variable declaration 19video element 189virtualization tools 87VMs (virtual machines)

installing 292–293overview 86

W

Watchy application

creating in Electron 235–239creating in NW.js 239–242

web applications

porting to-do lists 206–209TodoMVC

porting with Electron 208–209porting with NW.js 207–208

versus Node.js desktop applications

6–7

webcams, capturing photos with 187–198

using Electron 194–198using NW.js 188–193

webContents module 232webkit-app-region property 136webpack 103WebSocket class 115WebTorrent 5–6, 133width property 194

window object 252window.document 57window.onload function 197, 277window-resizing-nwjs 122windows

configuring dimensions for Electron

applications 123–124

configuring dimensions for NW.js

applications 122–123

constraining dimensions in Electron 126–128constraining dimensions in NW.js 124–126

Windows OS. See Microsoft Windows OS

INDEX

329

wireframes 32writeText function 218WYSIWYG editor 28, 165, 277

Y

YaST tool 311Yum tool 311

Z

Zhao, Cheng 8, 175

MORE TITLES FROM MANNING

Secrets of the JavaScript Ninja, Second Editionby John Resig, Bear Bibeault, and Josip Maras

ISBN: 9781617292859 464 pages$44.99 August 2016

Get Programming with JavaScript by John R. Larsen

ISBN: 9781617293108432 pages$39.99 August 2016

Sails.js in Actionby Mike McNeil and Irl Nathan

ISBN: 9781617292613488 pages$49.99 January 2017

For ordering information go to www.manning.com

MORE TITLES FROM MANNING

Node.js in Actionby Mike Cantelon, Marc Harter,

T.J. Holowaychuk, and Nathan RajlichISBN: 9781617290572 416 pages$44.99 October 2013

Node.js in Practiceby Alex Young and Marc Harter

ISBN: 9781617290930424 pages$49.99 December 2014

Getting MEAN with Mongo, Express, Angular, and Node, Second Editionby Simon D. Holmes

ISBN: 9781617294754450 pages$44.99 March 2018

For ordering information go to www.manning.com

MORE TITLES FROM MANNING

Express in ActionWriting, building, and testing Node.js applicationsby Evan M. Hahn

ISBN: 9781617292422256 pages$39.99 April 2016

Angular 2 Development with TypeScriptby Yakov Fain and Anton Moiseev

ISBN: 9781617293122456 pages$44.99 December 2016

Grokking AlgorithmsAn illustrated guide for programmers and other curious peopleby Aditya Y. Bhargava

ISBN: 9781617292231 256 pages$44.99 May 2016

For ordering information go to www.manning.com

JAVASCRIPT/WEB DEVELOPMENTCross-Platform Desktop Applications

Paul B. Jensen

SEE INSERT

「You will be shocked by

how easy it is to write

a desktop app!」

—From the Foreword by Cheng

Zhao, Creator of Electron

—Stephen Byrne, Dell

「Write-once/run-anywhere just became a real thing.」「The deﬁ nitive guide Indispensable.」

to two paradigm-shifting JavaScript frameworks.

—Clive Harber, Distorted Thinking

that will help you write

「Packed full of examples using JavaScript.」

—Jeff Smith, Ascension

cross-platform desktop apps

D esktop application development has traditionally

required high-level programming languages and special-ized frameworks. With Electron and NW.js, you can apply your existing web dev skills to create desktop applica-tions using only HTML, CSS, and JavaScript. And those applications will work across Windows, Mac, and Linux, radically reducing development and training time.Cross-Platform Desktop Applications guides you step by step through the development of desktop applications using Electron and NW.js. This example-ﬁ lled guide shows you how to create your own ﬁ le explorer, and then steps through some of the APIs provided by the frameworks to work with the camera, access the clipboard, make a game with keyboard controls, and build a Twitter desktop notiﬁ cation tool. You'll then learn how to test your applications, and debug and package them as binaries for various OSs.

What's Inside

● Create a selﬁ e app with the desktop camera● Learn how to test Electron apps with Devtron● Learn how to use Node.js with your application

Written for developers familiar with HTML, CSS, and JavaScript.

Paul Jensen works at Starcount and lives in London, UK.

To download their free eBook in PDF, ePub, and Kindle formats,

owners of this book should visit

www.manning.com/books/cross-platform-desktop-applications

M A N N I N G

$49.99 / Can $65.99 [INCLUDING eBOOK]


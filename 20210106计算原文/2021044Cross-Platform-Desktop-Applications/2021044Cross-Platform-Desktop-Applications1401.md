 Adding keyboard shortcuts to a 2D game Adding global hotkey shortcuts

Power users of applications (and users of Vim) will tell you that learning keyboardshortcuts is invaluable for using apps in a fast and productive manner. For otherapps, like arcade games, they can also be an essential interface method.

Programmatically binding keyboard shortcuts to your desktop app in Electronand NW.js offers your users faster ways to perform common tasks, takes some of UIscanning out of the user experience, and makes your apps easier and more pleas-ant to use. In this chapter, we'll explore how to add keyboard shortcuts to a videogame known as Snake.

Years ago, I built the Snake game as a Christmas/New Year project at a Ruby onRails consultancy called New Bamboo (now part of Thoughtbot) and wrote up atutorial about it on their site. Step forward to now, and what better example than tore-create the same game as a desktop app.

219

220

CHAPTER 14 Binding on keyboard shortcuts

Although you could port the original source code of the game from the repositoryI created six years ago, it would be better to create it fresh, learning from how it wasdeveloped. That way you can better understand the mechanics of the game as well ashow you can use Electron and NW.js's keyboard shortcuts APIs to bind direction keysto the movement of the snake. If you want to see the app in action, you can grab theapp's source code for snake-nwjs and snake-electron from the book's GitHub reposi-tory at http://mng.bz/kxdd and http://mng.bz/Wis3.

14.1 Creating the Snake game with NW.js

First off, create a new folder called snake-nwjs, and generate some default boilerplatecode for it:

mkdir snake-nwjscd snake-nwjstouch app.jstouch app.csstouch index.htmltouch package.json

You next need to put some initial configuration into the package.json file. Add the fol-lowing code to it:

{ "name": "snake-nwjs", "version": "1.0.0", "description": "A Snake game in NW.js for 'Cross Platform Desktop

Applications'",

"main": "index.html", "scripts": { "start": "node_modules/.bin/nw .", "test": "echo \"Error: no test specified\" && exit 1" }, "keywords": [ "snake", "nwjs" ], "author": "Paul Jensen <paulbjensen@gmail.com>", "license": "MIT", "window": { "width": 840, "height": 470, "toolbar": false }, "dependencies": { "nw": "^0.15.3" }}

IS THERE ANOTHER WAY TO CREATE THE PACKAGE.JSON FILE? Yes. If you getbored with creating the package.json file from scratch, there's a convenience

Creating the Snake game with NW.js

221

command from npm called init. It will ask you a bunch of questions fromthe CLI and create the package.json file for you. To use it, open a Terminalor Command Prompt and type npm init in the location where you would likethe package.json file to exist. To find out more about npm init, check outhttps://docs.npmjs.com/cli/init.

Now, turn your attention to the index.html file and put the following code in it:

<html> <head> <title>Snake</title> <link href="app.css" rel="stylesheet" /> <script src="app.js"></script> </head> <body> </body></html>

Now, you can start building the game. The first decision is what content you want todisplay for the Snake game. A few items should be displayed visually:

 The score The game area, the snake inside it, and the item that the snake eats Buttons for starting, pausing, and restarting the game.

We'll focus on the UI first and then flesh out various bits of the game. Let's define themain scoreboard and the game area in the UI.

First, define the game area and the scoreboard. For the game area, you'll use acanvas element, a simple div element for the scoreboard, and a bar element contain-ing the buttons to pause, resume, and restart the game. Inside the body element of theindex.html file, add the following snippet:

<div id="scoreboard"> <span id="label">Score:</span> <span id="score"></span> <div id="bar">  <div id="play_menu">  <button onclick="pause();">Pause</button> </div>  <div id="pause_menu">  <button onclick="play();">Resume</button>  <button onclick="restart();">Restart</button>  </div> <div id="restart_menu">  <button onclick="restart();">Restart</button> </div> </div></div> <canvas></canvas>

222

CHAPTER 14 Binding on keyboard shortcuts

The canvas tag will be used to render the area in which the snake will move, as well aswhere the food will appear. You'll add some styling to it to make it look presentable,too. In the app.css file, add the following styling:

body { margin: 1em; padding: 0; background: #111; color: white; font-family: helvetica;}

canvas { border: solid 1px red; width: 800px; height: 400px;}

#scoreboard { padding-bottom: 1em}

#label, #score, #bar { float: left; padding: 8px;}

#pause_menu, #restart_menu { display: none;}

Now you have the area for the snake to move around in, as well as the scoreboard, sonow you need a snake moving around and eating food. You'll use the HTML5 canvasAPI to handle rendering the snake. In the app.js file, add the following code:

'use strict';

let canvas, ctx, gridSize, currentPosition, snakeBody, snakeLength,

direction, score, suggestedPoint, allowPressKeys, interval, choice;

function updateScore () { score = (snakeLength - 3) * 10; document.getElementById('score').innerText = score;}

The updateScore function is a simple UI helper function that updates the div ele-ment, displaying the current score. Add the following code:

function hasPoint (element) { return (element[0] === suggestedPoint[0] && element[1] === suggestedPoint[1]);}

The hasPoint function is a helper function to check whether a given element's x andy coordinates match a suggested point's x and y coordinates, which are stored as an

Creating the Snake game with NW.js

223

array. The suggested point is where to place the food item that the snake will eat. Now,add the following:

function makeFoodItem () { suggestedPoint =

[Math.floor(Math.random()*(canvas.width/gridSize))*gridSize, Math.floor(Math.random()*(canvas.height/gridSize))*gridSize];

if (snakeBody.some(hasPoint)) { makeFoodItem(); } else { ctx.fillStyle = 'rgb(10,100,0)'; ctx.fillRect(suggestedPoint[0], suggestedPoint[1], gridSize, gridSize); }}

makeFoodItem does what it says—makes the food items for the snake to eat. It finds arandom point on the canvas and checks if it is currently occupied by the snake. If it is,it calls itself in order to find another spot. If not, it creates the food item at that spot.Add the following code:

function hasEatenItself (element) { return (element[0] === currentPosition.x && element[1] === currentPosition.y);}

Another semantically named function, hasEatenItself, checks whether the snakehas managed to wander into its own path. Now add this code:

function leftPosition(){ return currentPosition.x - gridSize; }

function rightPosition(){ return currentPosition.x + gridSize;}

function upPosition(){ return currentPosition.y - gridSize; }

function downPosition(){ return currentPosition.y + gridSize;}

These helper functions report back the edge of the snake's head, depending on thedirection in which the snake is heading. It's used to track the next coordinate thatthe snake would occupy on the axis so you can check if it's about to hit the edgeof the movement area, or eat a food item, or itself. Insert the following:

function whichWayToGo (axisType) { if (axisType === 'x') { choice = (currentPosition.x > canvas.width / 2) ? moveLeft() : moveRight();

224

CHAPTER 14 Binding on keyboard shortcuts

} else { choice = (currentPosition.y > canvas.height / 2) ? moveUp() : moveDown(); }}

A slight variation on the original Snake game, now, when the snake hits the edge ofthe movement area, it will go sideways rather than continue from the opposing endof the movement area. The idea is that the snake will move in the general direction ofwhere most of the space is, so if the snake is toward the bottom limit of the movementarea and hits the right side, then the snake will move upward—that's where the spaceis. Add the following:

function moveUp(){ if (upPosition() >= 0) { executeMove('up', 'y', upPosition()); } else { whichWayToGo('x'); }}

function moveDown(){ if (downPosition() < canvas.height) { executeMove('down', 'y', downPosition());  } else { whichWayToGo('x'); }}

function moveLeft(){ if (leftPosition() >= 0) { executeMove('left', 'x', leftPosition()); } else { whichWayToGo('y'); }}

function moveRight(){ if (rightPosition() < canvas.width) { executeMove('right', 'x', rightPosition()); } else { whichWayToGo('y'); }}

These functions will execute moving in a given direction, so long as there's space todo so. It will then move the snake in that direction. Now, add more code:

function executeMove(dirValue, axisType, axisValue) { direction = dirValue; currentPosition[axisType] = axisValue; drawSnake();}

Creating the Snake game with NW.js

225

The executeMove function handles setting the direction of the snake, its current position,and then drawing the body of the snake onto the movement area. Next, add this code:

function moveSnake(){ switch (direction) { case 'up':  moveUp();  break;

case 'down':  moveDown();  break;

case 'left':  moveLeft();  break;

case 'right':  moveRight();  break; }}

moveSnake handles moving the snake, based on the direction given. Next, you want toadd the buttons for restarting, pausing, and resuming the game. Insert the following:

function restart () { document.getElementById('play_menu').style.display='block'; document.getElementById('pause_menu').style.display='none'; document.getElementById('restart_menu').style.display='none'; pause(); start();}

function pause(){ document.getElementById('play_menu').style.display='none'; document.getElementById('pause_menu').style.display='block'; clearInterval(interval); allowPressKeys = false;}

function play(){ document.getElementById('play_menu').style.display='block'; document.getElementById('pause_menu').style.display='none'; interval = setInterval(moveSnake,100); allowPressKeys = true;}

Now, the player can restart, pause, and play the game. Now add this:

function gameOver(){ pause(); window.alert('Game Over. Your score was ' + score); ctx.clearRect(0,0, canvas.width, canvas.height);

226

CHAPTER 14 Binding on keyboard shortcuts

document.getElementById('play_menu').style.display='none'; document.getElementById('restart_menu').style.display='block';

}

When the game is finished, the player is shown what their score is, and the movementarea resets. Now you'll add the animation function:

function drawSnake() { if (snakeBody.some(hasEatenItself)) { gameOver(); return false; } snakeBody.push([currentPosition.x, currentPosition.y]); ctx.fillStyle = 'rgb(200,0,0)'; ctx.fillRect(currentPosition.x, currentPosition.y, gridSize, gridSize); if (snakeBody.length > snakeLength) { let itemToRemove = snakeBody.shift(); ctx.clearRect(itemToRemove[0], itemToRemove[1], gridSize, gridSize); } if (currentPosition.x === suggestedPoint[0] && currentPosition.y ===

suggestedPoint[1]) {

makeFoodItem(); snakeLength += 1; updateScore(); }}

The drawSnake function is the most complex of all of the functions in terms of thenumber of things it needs to do, which include the following:

 Check whether the snake has eaten itself, and if it has, end the game Track where the snake is in terms of coordinates Draw the snake's body on the canvas Clear areas where the snake was, and draw areas where the snake now is, giving

the illusion of the snake moving around in the area.

 Track whether the snake has eaten the food item, and if so, make another food

item, make the snake that much bigger, and update the score

Add this to start a new game:

function start () { ctx.clearRect(0,0, canvas.width, canvas.height); currentPosition = {'x':50, 'y':50}; snakeBody = []; snakeLength = 3; updateScore(); makeFoodItem(); drawSnake(); direction = 'right'; play(); }

Creating the Snake game with NW.js

227

The start function takes care of kicking off the game, setting up the initial state ofthe game, and then calling play in order to get the game going. Add the following toget the game to load and begin from the start:

function initialize () { canvas = document.querySelector('canvas'); ctx = canvas.getContext('2d'); gridSize = 10; start();}

window.onload = initialize;

The initialize function runs when the app loads. It takes care of initializing theHTML5 canvas object for interaction and calls the start function to begin the game. This is quite a sizeable amount of code, but now you have most of the game imple-mented. If you were to open the game and run it with NW.js, you should see some-thing like figure 14.1.

Figure 14.1 The Snake game running, but no keyboard controls implemented yet

The game is functional, but you can't control the snake yet—it's going to go roundand round in circles. You need to implement keyboard controls.

14.1.1 Implementing window focus keyboard shortcuts with NW.js

If you need to control the app when the window is in focus, you can add keyboardshortcuts to JavaScript in the app without using NW.js's keyboard shortcuts API. Youcan use browser-specific JavaScript to handle that.

228

CHAPTER 14 Binding on keyboard shortcuts

Add this code to the app.js file above the start function:

window.document.onkeydown = function(event) { if (!allowPressKeys){ return null; } let keyCode; if(!event) { keyCode = window.event.keyCode; } else { keyCode = event.keyCode; }

switch(keyCode) { case 37:  if (direction !== 'right') {  moveLeft();  }  break;

case 38:  if (direction !== 'down'){  moveUp();  }  break;

case 39:  if (direction !== 'left'){  moveRight();  }  break;

case 40:  if (direction !== 'up'){  moveDown();  }  break;

default:  break; }};

Here, you add an event listener for any keypress. You then look at which key ispressed, and if it's a keycode for a direction key, then you move the snake in thatdirection. If you were to save this file and reload the app with nw on the Terminal, youcould play the game by using the up, down, left, and right keys.

This is okay in the context of playing a video game, but what if you want to trigger

a command from the keyboard without the app window necessarily being in focus?

Creating the Snake game with NW.js

229

This is where NW.js's keyboard shortcuts API comes into action. You can linkglobal keyboard shortcuts to the game so users can pause the game, even when thewindow isn't in focus.

14.1.2 Creating global keyboard shortcuts with NW.js

NW.js's keyboard shortcuts API is used to create global shortcuts for apps that executeeven when the app window isn't in focus; for example, the media keys on your desktopmusic player app, which you can use to pause music even when the music player isn'tin focus.

Let's say, for the sake of putting the API to use, that you want to be able to pausethe Snake game, even when the app window isn't in focus. You propose that pressingCtrl-P will pause the game, or resume it if it was paused.

You'll start by adding a variable for tracking whether the game is currently in play,

or is paused:

let currentState;

Next, add a function to handle toggling between the play and pause states of the gameso you can press a key combination that will either pause or resume the game, depend-ing on the current state:

function togglePauseState () { if (currentState) { if (currentState === 'play') {  pause();  currentState = 'pause'; } else {  play();  currentState = 'play'; } } else { pause(); currentState = 'play'; }}

Upon the first attempt to run the code, the currentState variable hasn't been set, soyou set it to play (as the game app automatically plays when it's started) and thenpause the game. If the variable is then set to pause, you call the play command andset the current state to that, and vice versa.

The functionality of the togglePauseState function means you can bind the Ctrl-P keys to this command, keeping the binding nice and simple. To attach this functionto the Ctrl-P keypresses, you insert this little bit of code:

const pauseKeyOptions = { key:'Ctrl+P', active: togglePauseState, failed: () => {

230

CHAPTER 14 Binding on keyboard shortcuts

console.log('An error occurred'); }};

The pauseKeyOptions variable specifies the key combination, what action to runwhen the key combo is triggered, and a function to execute if it fails for any reason.You then pass this variable to a new instance of NW.js's Shortcut class:

const pauseShortcut = new nw.Shortcut(pauseKeyOptions);

To confirm that this key combo works with the OS, add this line of code:

nw.App.registerGlobalHotKey(pauseShortcut);

This ensures that the OS will recognize the key combination and trigger the pause/resume action on combo keypress. You could leave it there and say that's all thatneeds to be done, but one thing to bear in mind is that you need to release thisglobal hotkey combination when the game is closed. For this, add one final snippetof code:

process.on('exit', () => { nw.App.unregisterGlobalHotKey(pauseShortcut);});

This snippet ensures that when the app is about to be closed, the hotkey combina-tion is released. If you now save the file and reload the app from the Terminal, youshould now find that pressing Ctrl-P pauses the game, even when the window is notin focus.

Ctrl-P keys work as Command-P on Macs, why?This is a bit odd, but NW.js treats the Ctrl key specified in the keyboard shortcuts APIas the Command key on Mac OS; even though you specified the Ctrl-P key combo inthe example, it triggers with Command-P on the Mac.

Macs use the Command key rather than the Control key for shortcuts (for example,Command-C for copy on Macs is equivalent to Ctrl-C for copy on Windows).

The use case given is perhaps a bit unusual, but it demonstrates how you can useNW.js to work with your keyboard even when an app window isn't in focus. Apps thatwould use this include music-playing apps, and even screen-recording software, whichdo not depend on the mouse to click a button to start and stop recording.

We'll now take a look at how Electron handles implementing keyboard shortcuts.

Creating global shortcuts for the Snake game with Electron

231

14.2 Creating global shortcuts for the Snake game

with ElectronTo compare how Electron implements keyboard shortcuts, you'll re-create the gamewith Electron. If you want to skip ahead to a working version of the game, you can checkout the source code on the book's GitHub repository for the snake-electron app.

The two versions of the app share a lot of similar code, but how they go aboutimplementing support for keyboard shortcuts differs quite a bit. Not only are the APImethods different, but the way in which they're accessed also needs to be taken intoconsideration.

To illustrate this, I'll skip showing the identical files and focus exclusively on the

parts of the app that involve implementing the global keyboard shortcuts.

The index.html and app.css files look exactly the same. The bits that have changesin them are the app.js and main.js files. You'll start with the main.js file, which isimportant because it's the place from which you'll call Electron's globalShortcutAPI. The following listing shows the main.js file.

Registersthekeyboardshortcut

Listing 14.1 The main.js file in the Snake Electron app

'use strict';

const {app, globalShortcut, BrowserWindow} = require('electron');

let mainWindow = null;

app.on('window-all-closed', () => { if (process.platform !== 'darwin') app.quit();});

Requires the globalShortcut dependency from Electron

app.on('ready', () => { mainWindow = new BrowserWindow({ width: 840, height: 470, useContentSize: true }); mainWindow.loadURL(`file://${__dirname}/index.html`); mainWindow.on('closed', () => { mainWindow = null; }); const pauseKey = globalShortcut.register('CommandOrControl+P', () => {  mainWindow.webContents.send('togglePauseState');     }); if (!pauseKey) alert('You will not be able to pause the game from the

When keyboardshortcut is triggered,emits event toapp window

keyboard');

});

app.on('will-quit', () => { globalShortcut.unregister('CommandOrControl+P'); });

If you couldn't register keyboard shortcut, alerts user

When app quits, unregisters keyboard shortcut from computer

The globalShortcut API is available from the main process in Electron, so yourequire it from the main.js file and then use it to register a keyboard shortcut. Once

232

CHAPTER 14 Binding on keyboard shortcuts

the module is required, you're then able to add and remove keyboard shortcuts bycalling the register and unregister API methods. What's different with Electron'sapproach to creating keyboard shortcuts is that the string passed for the keyboardshortcut binding says "CommandOrControl" rather than "Ctrl" in NW.js. This reflectsthe way in which Mac OS favors the use of Command as the main keyboard shortcutkey, and Windows and Linux favor the Ctrl key. Electron is smart enough to detectwhich OS the app is running on and use the appropriate keyboard shortcut.

Because the keyboard shortcut is registered in the main process, you need a way topass the message on to the renderer process where the app window is so the game canbe paused there. To do this, you need to use the webContents module to send a mes-sage to the app window so the message can be received by the renderer process andacted on. To demonstrate how this works, here's the bit of code that handles this inthe app.js file.

Listing 14.2 The app.js file for the Snake Electron app

const ipcRenderer = require('electron').ipcRenderer;

function togglePauseState () {  if (currentState) { if (currentState === 'play') {  pause();  currentState = 'pause'; } else {  play();  currentState = 'play'; } } else { pause(); currentState = 'play'; }}

Function to trigger when keyboard shortcut is pressed

ipcRenderer.on('togglePauseState', togglePauseState);

Loads ipcRenderer module from Electron via ES2015 shorthand

When message with event name「togglePauseState」is received, triggers that function

The ipcRenderer module receives events emitted via the webContents module in themain process. When the Ctrl (or Command) and P keyboard combination is pressed,the webContents.send call sends an event with the name togglePauseState. Thisevent is then received by the ipcRenderer module in the app window, which is thenable to trigger the function of the same name.

Comparing the different approaches of NW.js and Electron in implementing thisfeature in the game, you can see that Electron involves a bit more code in order tofacilitate using the globalShortcut API via IPC. This is where NW.js's sharedJavaScript context between the back end and front end makes implementing this fea-ture simpler.

If you want to read more about the globalShortcut API in Electron, the docu-

mentation for it is available at http://electron.atom.io/docs/api/global-shortcut/.

14.3 Summary

Summary

233

In this chapter, we've looked at how keyboard shortcuts can be added to a 2D gamewith both NW.js and Electron and studied how each of them approaches implement-ing shortcuts. We also looked at how global hotkeys can be added that can be accessedat any time on the computer, even when the desktop app isn't in focus. Some of thekey takeaways from the chapter include the following:

 You can use the document.onkeydown event to listen for keystrokes in an app, as

you would in a web page.

 When it comes to implementing global hotkeys in NW.js, the Ctrl key refers to

the Command key on Mac OS.

 Make sure to unregister global hot keys if you use the keyboard shortcuts API in

your app; otherwise, other apps' keyboard shortcuts will be overridden.

In chapter 15, we'll look at another way to interact more closely with the OS—throughemitting desktop notifications.

Making desktopnotifications

This chapter covers Seeing how Electron supports desktop

notifications through a third-party npm module

 Using the HTML5 notification API to make

desktop notifications in NW.js

 Working with Twitter to create a live tweet


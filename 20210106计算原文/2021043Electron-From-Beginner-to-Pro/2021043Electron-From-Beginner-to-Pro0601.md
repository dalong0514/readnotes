Understanding the IPC Module

We briefly saw the use of the inter-process communication (IPC) module as one solution for having contextual menus in our application. In this chapter, we are going to explore this module in greater depth. Now, this is not the most glamorous part of API, but it is certainly the workhorse that much of our real-world applications will rely upon.

Getting Started

Since Electron applications are broken into two separate processes (main and render), we need a system to communicate between them. That system is in the IPC module. This module allows you to send and receive synchronous and asynchronous messages between the processes. Each process has a specific module: ipcRenderer and ipcMain (Figure 6-1).

Main Process

Renderer Process

IPC

Figure 6-1. The IPC API provides a communication bridge between the processes.

Let's clone a fresh copy of Electron.

git clone https://github.com/electron/electron-quick-start ipc-example

Next, change your active directory to electron-quick-start.

cd ipc-example

Now, we need to install the dependencies:

npm install

Finally, reset Git with

git init

With our fresh copy of Electron, let's begin exploring the various IPC solutions.

© Chris Griffith, Leif Wells 2017 C. Griffith, L. Wells, Electron: From Beginner to Pro, https://doi.org/10.1007/978-1-4842-2826-5_6

93

Chapter 6 ■ Understanding the ipC ModUle

Synchronous IPC Messaging

Let's begin by defining a few quick styles for our button and response field, the result of this can be seen in Figure 6-2. Open the index.html file and place this style block within our <head> tag:

<style> p { font-family: sans-serif; border: 1px solid #ccc; border-radius: 4px; padding: .5rem; background-color: #ddd; box-shadow: inset 0 0 2px #aaa; }

button { color: rebeccapurple; font-family: sans-serif; font-weight: bold; padding: .5rem; background-color: #ccc; box-shadow: 2px 2px 2px #ccc; }</style>

Next, replace the content within the <body> tag with the following:

<button id="sendSyncMsgBtn">Ping Main Process</button><p id="syncReply">Awaiting response</p>

94

Chapter 6 ■ Understanding the ipC ModUle

Figure 6-2. Our Electron application with our button

Now, let's open the renderer.js to add the code that will be triggered when we click our button, as well as

the code needed to accept the response back.

First, we need to import the correct IPC module. Since this code will be executed in the Renderer

process, we will use the IPCRenderer module.

const ipc = require('electron').ipcRenderer

Next, we need to get the reference to our button.

const syncMsgBtn = document.getElementById('sendSyncMsgBtn')

With our reference, we can attach our event listener to it:

syncMsgBtn.addEventListener('click', function () {

})

95

Chapter 6 ■ Understanding the ipC ModUle

Working with IPC, is much like Isaac Newton's Third Law of motion (for every action, there is an equal

and opposite reaction), for every IPC send there must be an IPC receive method.

The basic structure of this call is

ipcRenderer.sendSync (channel, [, arg1][, arg2], [,...})

The channel value is a string that is used as a message identifier. It is this identifier that the companion

method will be listening for. You can optionally send additional values as arguments. These can be any JavaScript primitive (string, number, arrays, objects). In the spirit of communications, let's have our function send the famous words from Alexander Graham Bell:

syncMsgBtn.addEventListener('click', function () { const reply = ipc.sendSync('synchronous-message', 'Mr. Watson, come here.')})

Whenever, we are working with IPC events, once we write our sending function, we switch to the other

process and write the companion stub function. So, let's switch to the main.js file and do this.

The Main process will also need to import the IPC module as well.

const ipc = electron.ipcMain

Now, we can write our receiver function. The function is straightforward, and we define which channel

it should listen on, and a function to execute.

ipc.on('synchronous-message', function (event, arg) {

})

often when coding electron application, we have multiple files open at the same time. More than

■ Note once, we have forgotten to save all the files and wonder why our code does not work. You might want to start to learn the key command to perform a save all to ensure all the files are saved and your code will execute properly.

The callback function has two arguments: the event object and the arguments. While the arguments

will contain the data that our sending function passed over, the event object has some special functions. The event object has the built-in ability to respond to the sender. Meaning, there is no need to write another set of listeners and receivers to communicate a response.

For synchronous IPC messages, the method is

event.returnValue

96

Chapter 6 ■ Understanding the ipC ModUle

This value can be a string, a number or an object. For this example, let's just keep it a string.

ipc.on('synchronous-message', function (event, arg) { event.returnValue = 'I heard you!'})

Switching back to the renderer.js file, we can now add the code to handle this returned value. The value

that we sent over from the main process will be stored in the reply.

syncMsgBtn.addEventListener('click', function () { const reply = ipc.sendSync('synchronous-message', 'Mr. Watson, come here.') console.log(reply)})

We will then craft a simple message that we will display. Let's use the new templating feature in ES6 to

do this. This is done using the $() syntax, so the message can be written as such:

const message = `Synchronous message reply: ${reply}`

If you have not used the ${} syntax before, it greatly improves the readability of your concatenated

strings. You will also note we are using ` or back ticks instead of ' or ". This is another new habit to try to pick up. The advantage of using ` is you can now have your string extend for more than one line. However, in this case we don't need it.

With our message string constructed, we can update the innerHTML our paragraph:

document.getElementById('syncReply').innerHTML = message

Here is the complete code:

syncMsgBtn.addEventListener('click', function () { const reply = ipc.sendSync('synchronous-message', 'Mr. Watson, come here.') console.log(reply) const message = `Synchronous message reply: ${reply}` document.getElementById('syncReply').innerHTML = message})

97

Chapter 6 ■ Understanding the ipC ModUle

Save all the files and run the application. Click the button, and our message should appear in the

window (Figure 6-3).

Figure 6-3. The result of our IPC call being displayed

This is the basics of using synchronous IPC within Electron. Now, let's explore using IPC messaging in

an asynchronous fashion.

Asynchronous IPC Messaging

Often, the event that we trigger by sending our IPC message might take a noticeable amount of time for the method to finish and the response returned to the renderer process. This will leave our renderer process nonfunctioning. Certainly not the best user experience for your application. For these situations, we can use the asynchronous IPC methods instead.

Let's add two more elements to our HTML file, the result of this can be seen in Figure 6-3:

<button id="sendAsyncMsgBtn">Ping Main Process Async</button><p id="asyncReply">Awaiting async response</p>

98

Chapter 6 ■ Understanding the ipC ModUle

Figure 6-4. Our Electron application with the async UI ready

Switching to our renderer.js file, we will get the reference to our new button:

const asyncMsgBtn = document.getElementById('sendAsyncMsgBtn')

then like before, we will create an event listener for the button click:

asyncMsgBtn.addEventListener('click', function () {

})

99

Chapter 6 ■ Understanding the ipC ModUle

There are two key differences in working with asynchronous IPC messages. The first is instead of using

the sendSync method, we use the send method instead.

asyncMsgBtn.addEventListener('click', function () { ipc.send('asynchronous-message', ''That's one small step for man')})

The other difference is that we now need to explicitly write the callback function that will handle the

response from the Main process.

ipc.on('asynchronous-reply', function (event, arg) { const message = `Asynchronous message reply: ${arg}` document.getElementById('asyncReply').innerHTML = message})

The IPC code in the Main process changes slightly as well in the main.js file. The actual listener does

remain the same, but the method to respond changes. Instead of calling the returnValue method on the Event object, we now use event.sender.send to respond.

ipc.on('asynchronous-message', function (event, arg) { if (arg === 'That's one small step for man') { event.sender.send('asynchronous-reply', ', one giant leap for mankind.') }})

if we are using a different channel name for our asynchronous response, this allows us to have

■ Note multiple ipC messaging flows occurring.

Go ahead and save the files and run the application. You should be able trigger both styles of IPC

messaging (Figure 6-5).

100

Chapter 6 ■ Understanding the ipC ModUle

Figure 6-5. Our Electron application, showing the results of our IPC call

Managing Event Listeners

Much like we probably heard as a child about cleaning up after yourself, the same holds true for any event listener or IPC listener we might create within our Electron application. The IPC modules have the same syntax for either the sync or async process. If we want to remove a single listener from the method on the Main process, the syntax is:

ipcMain.removeListener( channel name, function)

and from the Renderer process:

ipcRenderer.removeListener( channel name, function)

The function should be the reference to the function that was executed by the on method.

101

Chapter 6 ■ Understanding the ipC ModUle

If you need to remove all the listeners on a specific channel, you can use the removeAllListeners

method to do so. Here is the basic syntax:

ipcMain.removeAllListeners(channel)

and

ipcRenderer.removeAllListeners(channel)

In both of our earlier examples, our two event listeners had their functions defined within the listener itself. For example, if our Main process needed to know if a user had logged into our system, we could have this event shell:

function userDidLogin() { ipcRenderer.on('userLogin', this.handleLoginSuccess);}

function userDidLogout() { ipcRenderer.removeListener('userLogin', this.handleLoginSuccess);}

function handleLoginSuccess(event, args) { console.log('data', args.data);}

This could be tied to changing a Menu Item based on the user's login status, or some other method. For this example, once we have had the state change, there is no need to keep listening for that event. By removing it, that is one less thing our application must concern itself with.

Electron's IPC module provides one more useful methods along these same lines. That method is:

ipc.once(channel, listener)

This method is available for both the Main and Renderer process. The method will listen on the

specific channel. Once it has received the event, it will execute the listener function, then remove itself from the IPC listeners.

Summary

Although the IPC module does not have a lot of methods – just variations of sending and receiving – it is the backbone for our Electron processes to coexist. You will use this module to possibly start a third-party Node library in the Main process from a user action in the Renderer process. In our next chapter, we will be leveraging them quite a bit to work with Electron's dialog module.

102

CHAPTER 7


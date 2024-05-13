# 0601. Understanding the IPC Module

We briefly saw the use of the inter-process communication (IPC) module as one solution for having contextual menus in our application. In this chapter, we are going to explore this module in greater depth. Now, this is not the most glamorous part of API, but it is certainly the workhorse that much of our real-world applications will rely upon.

## 6.1 Getting Started

Since Electron applications are broken into two separate processes (main and render), we need a system to communicate between them. That system is in the IPC module. This module allows you to send and receive synchronous and asynchronous messages between the processes. Each process has a specific module: ipcRenderer and ipcMain (Figure 6-1).

1『原来是靠 IPC module 来连接 electron 的两大核心部分：main process and render process。（2021-03-27）』

Main Process <=>  Renderer Process

Figure 6-1. The IPC API provides a communication bridge between the processes.

Let's clone a fresh copy of Electron.

```
git clone https://github.com/electron/electron-quick-start ipc-example
```

1-2『这里第二次拷这种类似命令了，才意识的 GitHub 的一个仓库里其实是可以放不同的版本的「仓库」的。有时间去研究下如何实现的。（2021-03-27）』—— 未完成

Next, change your active directory to electron-quick-start.

```
cd ipc-example
```

Now, we need to install the dependencies:

```
npm install
```

Finally, reset Git with:

```
git init
```

1『

初始化后弹出的信息：

```
Reinitialized existing Git repository in /Users/Daglas/dalong.electron/ipc-example/.git/
```

不过一直没弄明白这里的「初始化」有啥用。（2021-03-27）

』

With our fresh copy of Electron, let's begin exploring the various IPC solutions.

## 6.2 Synchronous IPC Messaging

Let's begin by defining a few quick styles for our button and response field, the result of this can be seen in Figure 6-2. Open the index.html file and place this style block within our `<head>` tag:

```html
    <style> 
      p { 
        font-family: sans-serif; 
        border: 1px solid #ccc; 
        border-radius: 4px; 
        padding: .5rem; 
        background-color: #ddd; 
        box-shadow: inset 0 0 2px #aaa; 
      }
      button { 
        color: rebeccapurple; 
        font-family: sans-serif; 
        font-weight: bold; 
        padding: .5rem; 
        background-color: #ccc; 
        box-shadow: 2px 2px 2px #ccc; 
      }
    </style>
```

Next, replace the content within the `<body>` tag with the following:

```html
    <button id="sendSyncMsgBtn">Ping Main Process</button>
    <p id="syncReply">Awaiting response</p>
```

Figure 6-2. Our Electron application with our button

1『

自己的源码：

```html
  <body>
    <button id="sendSyncMsgBtn">Ping Main Process</button>
    <p id="syncReply">Awaiting response</p>
    <!-- <h1>Hello World!</h1> -->
    <!-- We are using Node.js <span id="node-version"></span>,
    Chromium <span id="chrome-version"></span>,
    and Electron <span id="electron-version"></span>. -->

    <!-- You can also require other files to run in this process -->
    <script src="./renderer.js"></script>
  </body>
```

』

Now, let's open the renderer.js to add the code that will be triggered when we click our button, as well as the code needed to accept the response back.

First, we need to import the correct IPC module. Since this code will be executed in the Renderer process, we will use the IPCRenderer module.

```js
const ipc = require('electron').ipcRenderer
```

Next, we need to get the reference to our button.

```js
const syncMsgBtn = document.getElementById('sendSyncMsgBtn')
```

With our reference, we can attach our event listener to it:

```js
syncMsgBtn.addEventListener('click', function () {
})
```

Working with IPC, is much like Isaac Newton's Third Law of motion (for every action, there is an equal and opposite reaction), for every IPC send there must be an IPC receive method.

The basic structure of this call is

```js
ipcRenderer.sendSync (channel, [, arg1][, arg2], [,...})
```

The channel value is a string that is used as a message identifier. It is this identifier that the companion method will be listening for. You can optionally send additional values as arguments. These can be any JavaScript primitive (string, number, arrays, objects). In the spirit of communications, let's have our function send the famous words from Alexander Graham Bell:

```js
syncMsgBtn.addEventListener('click', function () { 
    const reply = ipc.sendSync('synchronous-message', 'Mr. Watson, come here.')
})
```

Whenever, we are working with IPC events, once we write our sending function, we switch to the other process and write the companion stub function. So, let's switch to the main.js file and do this.

The Main process will also need to import the IPC module as well.

```js
const ipc = electron.ipcMain
```

Now, we can write our receiver function. The function is straightforward, and we define which channel it should listen on, and a function to execute.

```js
ipc.on('synchronous-message', function (event, arg) {

})
```

Note: often when coding electron application, we have multiple files open at the same time. More than once, we have forgotten to save all the files and wonder why our code does not work. You might want to start to learn the key command to perform a save all to ensure all the files are saved and your code will execute properly.

The callback function has two arguments: the event object and the arguments. While the arguments will contain the data that our sending function passed over, the event object has some special functions. The event object has the built-in ability to respond to the sender. Meaning, there is no need to write another set of listeners and receivers to communicate a response.

For synchronous IPC messages, the method is `event.returnValue`. This value can be a string, a number or an object. For this example, let's just keep it a string.

```jd
ipc.on('synchronous-message', function (event, arg) {
  event.returnValue = 'I heard you!'
})
```

Switching back to the renderer.js file, we can now add the code to handle this returned value. The value that we sent over from the main process will be stored in the reply.

```js
syncMsgBtn.addEventListener('click', function () {
    const reply = ipc.sendSync('synchronous-message', 'Mr. Watson, come here.')
    console.log(reply)
})
```

We will then craft a simple message that we will display. Let's use the new templating feature in ES6 to do this. This is done using the `$()` syntax, so the message can be written as such:

```js
const message = `Synchronous message reply: ${reply}`
```

If you have not used the `${}` syntax before, it greatly improves the readability of your concatenated strings. You will also note we are using \` or back ticks instead of ' or ". This is another new habit to try to pick up. The advantage of using \` is you can now have your string extend for more than one line. However, in this case we don't need it.

With our message string constructed, we can update the innerHTML our paragraph:

```js
document.getElementById('syncReply').innerHTML = message
```

Here is the complete code:

```js
syncMsgBtn.addEventListener('click', function () {
    const reply = ipc.sendSync('synchronous-message', 'Mr. Watson, come here.')
    console.log(reply)
    const message = `Synchronous message reply: ${reply}`
    document.getElementById('syncReply').innerHTML = message
})
```

Save all the files and run the application. Click the button, and our message should appear in the window (Figure 6-3).

Figure 6-3. The result of our IPC call being displayed

This is the basics of using synchronous IPC within Electron. Now, let's explore using IPC messaging in an asynchronous fashion.

1-2『

跑不通，报错找不到 ipc 对象，说明没引用出来，还在看了下墨菲写数据流 electron 的代码，发现现在引用的方式改了，

```js
const {app, BrowserWindow, ipcMain} = require('electron')
const path = require('path')

ipcMain.on('synchronous-message', function (event, arg) {
  event.returnValue = 'I heard You'
})
```

目前还是跑步起来。（2021-03-27）

』—— 未完成


## 6.3 Asynchronous IPC Messaging

Often, the event that we trigger by sending our IPC message might take a noticeable amount of time for the method to finish and the response returned to the renderer process. This will leave our renderer process nonfunctioning. Certainly not the best user experience for your application. For these situations, we can use the asynchronous IPC methods instead.

Let's add two more elements to our HTML file, the result of this can be seen in Figure 6-3:

```html
<button id="sendAsyncMsgBtn">Ping Main Process Async</button>
<p id="asyncReply">Awaiting async response</p>
```

Figure 6-4. Our Electron application with the async UI ready

Switching to our renderer.js file, we will get the reference to our new button:

```js
const asyncMsgBtn = document.getElementById('sendAsyncMsgBtn')
```

then like before, we will create an event listener for the button click:

```js
asyncMsgBtn.addEventListener('click', function () {

})
```

There are two key differences in working with asynchronous IPC messages. The first is instead of using the sendSync method, we use the send method instead.

```js
asyncMsgBtn.addEventListener('click', function () { 
  ipc.send('asynchronous-message', ''That's one small step for man')
})
```

The other difference is that we now need to explicitly write the callback function that will handle the response from the Main process.

```js
ipc.on('asynchronous-reply', function (event, arg) { 
    const message = `Asynchronous message reply: ${arg}` 
    document.getElementById('asyncReply').innerHTML = message
})
```

The IPC code in the Main process changes slightly as well in the main.js file. The actual listener does remain the same, but the method to respond changes. Instead of calling the returnValue method on the Event object, we now use event.sender.send to respond.

```js
ipc.on('asynchronous-message', function (event, arg) { 
    if (arg === "That's one small step for man") { 
        event.sender.send('asynchronous-reply', ', one giant leap for mankind.') 
    }
})
```

Note: if we are using a different channel name for our asynchronous response, this allows us to have multiple ipC messaging flows occurring.

Go ahead and save the files and run the application. You should be able trigger both styles of IPC messaging (Figure 6-5).

Figure 6-5. Our Electron application, showing the results of our IPC call

## 6.4 Managing Event Listeners

Much like we probably heard as a child about cleaning up after yourself, the same holds true for any event listener or IPC listener we might create within our Electron application. The IPC modules have the same syntax for either the sync or async process. If we want to remove a single listener from the method on the Main process, the syntax is:

```js
ipcMain.removeListener( channel name, function)
```

and from the Renderer process:

```js
ipcRenderer.removeListener( channel name, function)
```

The function should be the reference to the function that was executed by the on method.

If you need to remove all the listeners on a specific channel, you can use the removeAllListeners method to do so. Here is the basic syntax:

```js
ipcMain.removeAllListeners(channel)
```

and

```js
ipcRenderer.removeAllListeners(channel)
```

In both of our earlier examples, our two event listeners had their functions defined within the listener itself. For example, if our Main process needed to know if a user had logged into our system, we could have this event shell:

```js
function userDidLogin() { 
  ipcRenderer.on('userLogin', this.handleLoginSuccess);
}

function userDidLogout() { 
  ipcRenderer.removeListener('userLogin', this.handleLoginSuccess);
}

function handleLoginSuccess(event, args) { 
  console.log('data', args.data);
}
```

This could be tied to changing a Menu Item based on the user's login status, or some other method. For this example, once we have had the state change, there is no need to keep listening for that event. By removing it, that is one less thing our application must concern itself with.

Electron's IPC module provides one more useful methods along these same lines. That method is:

```js
ipc.once(channel, listener)
```

This method is available for both the Main and Renderer process. The method will listen on the specific channel. Once it has received the event, it will execute the listener function, then remove itself from the IPC listeners.

## Summary

Although the IPC module does not have a lot of methods – just variations of sending and receiving – it is the backbone for our Electron processes to coexist. You will use this module to possibly start a third-party Node library in the Main process from a user action in the Renderer process. In our next chapter, we will be leveraging them quite a bit to work with Electron's dialog module.
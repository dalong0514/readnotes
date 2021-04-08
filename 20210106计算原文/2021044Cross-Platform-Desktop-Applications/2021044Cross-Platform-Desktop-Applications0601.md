 Building with NW.js's shared-context approach Sharing state by passing messages

Although NW.js and Electron consist of the same software components, and ChengZhao has influenced the development of both, the two frameworks have evolveddifferent approaches to how they function under the hood. Analyzing how theyoperate internally will help you understand what's going on when you're runningan app and demystify the software.

In this chapter, we'll look at how NW.js and Electron function internally. We'lltake a look at NW.js first to see how it combines Node.js with Chromium (becausethat was the first Node.js desktop app framework) and then explore how Electrontook a different approach to combining those software components. Following that,we'll look at the frameworks' different approaches to context and state. I'll then

108

6.1

How does NW.js work under the hood?

109

elaborate a bit on Electron's use of message passing to transmit data as state betweenthe processes in a desktop app.

We'll also look at some resources for further reading. The goal is that you'll be in agood position to understand how the two frameworks differ in their internal architec-ture and the implications this has on building desktop apps with them.

How does NW.js work under the hood?From a developer's view, NW.js is a combination of a programming framework(Node.js) with Chromium's browser engine through their common use of V8. V8 is aJavaScript engine created by Google for its web browser, Google Chrome. It's writtenin C++ and was designed with the goal of speeding up the execution of JavaScript inthe web browser.

When Node.js was released in 2009, a year after Google Chrome, it combined amultiplatform support library called libuv with the V8 engine and provided a way towrite asynchronous server-side programs in JavaScript. Because both Node.js andChromium use V8 to execute their JavaScript, it provided a way to combine the twopieces of software, which Roger Wang came to understand and figure out. Figure 6.1shows how those components are combined.

Blink rendering engine

npm

Operating

systembindings

Node.js

Sharedcontext

V8

index.html

app.css

app.js

Figure 6.1 Overview of NW.js's component architecture in relation to loading an app

Looking at figure 6.1, you can see that Node.js is used in the back end to handle work-ing with the OS, and that Blink (Chromium's rendering engine) is used to handlerendering the front-end part of the app, the bit that users see. Between them, bothNode.js and Blink use V8 as the component that handles executing JavaScript, and it's

110

CHAPTER 6 Exploring NW.js and Electron's internals

this bit that's crucial in getting Node.js and Chromium to work together. There arethree things necessary for Node.js and Chromium to work together:

 Make Node.js and Chromium use the same instance of V8 Integrate the main event loop Bridge the JavaScript context between Node and Chromium

NW.js and its forked dependenciesNW.js, a combination of Node.js and the WebKit browser engine, used to be knownas node-webkit. Recently, both components were forked: Google created a fork ofWebKit called Blink, and in October 2014 a fork of Node.js called IO.js emerged. Theywere created for different reasons, but as projects that received more regularupdates and features, NW.js opted to switch to using them.

As node-webkit no longer used Node.js and WebKit (but IO.js and Blink instead), itwas suggested that the project should be renamed; hence, the project was renamedto NW.js.

In May 2015, the IO.js project agreed to work with the Node.js foundation to mergeIO.js back into Node.js. NW.js has switched back to using Node.js since.

6.1.1 Using the same instance of V8

Both Node.js and Chromium use V8 to handle executing JavaScript. Getting them towork together requires that a couple of things happen in order. The first thing NW.jsdoes is load Node.js and Chromium so that both of them have their JavaScript con-texts loaded in the V8 engine. Node's JavaScript context will expose global objects andfunctions such as module, process, and require, to name a few. Chromium's Java-Script context will expose global objects and functions like window, document, andconsole. This is illustrated in figure 6.2 and involves some overlap because both Nodeand Chromium have a console object.

When this is done, the JavaScript context for Node.js can be copied into the

JavaScript context for Chromium.

Although that sounds quite easy, the reality is that there's a bit more glue involvedfor Node.js and Chromium to work together—the main event loop used by both hasto be integrated.

How does NW.js work under the hood?

111

Node.js' JavaScript context

process

require

Buffer

b

When NW.js loads,Node.js' global objectsare copied from theirJavaScript context intothe context of the Blinkrendering engine, sothat they exist in oneplace.

Blink's JavaScript context

window

document

console

module

console

process

require

Buffer

module

c

When a JavaScript ﬁle (example.js)runs, it has access to all the objects inBlink's JavaScript context, includingthe sever-side objects from Node.js

example.js

var fs = require('fs');

document.write('<ul>');

Legend of global objects

Native object

Shared object

Copied object

fs.readdir('/home', function(err, files){

files.foreach(function (file){

document.write('<li>'+file+'</li>)

});

});

document.write('<ul>');

Figure 6.2 How NW.js handles copying the JavaScript context for Node.js into Chromium's JavaScript context

6.1.2

Integrating the main event loopAs discussed in section 5.1.3, Node.js uses the event loop programming pattern tohandle executing code in a non-blocking, asynchronous fashion. Chromium also usesthe event loop pattern to handle the asynchronous execution of its code.

But Node.js and Chromium use different software libraries (Node.js uses libuv, andChromium uses its own custom C++ libraries, known as MessageLoop and Message-Pump). To get Node.js and Chromium to work together, their event loops have to beintegrated, as illustrated in figure 6.3.

When the JavaScript context for Node.js is copied into Chromium's JavaScript con-text, Chromium's event loop is adjusted to use a custom version of the MessagePumpclass, built on top of libuv, and in this way, they're able to work together.

112

CHAPTER 6 Exploring NW.js and Electron's internals

Node.js event loop

Chromium event loop

libuv

MessagePump

MessageLoop

Figure 6.3 NW.js integrates the event loops of Node.js and Chromium by making Chromium use a custom version of MessagePump, built on top of libuv.

6.1.3 Bridging the JavaScript context between Node and Chromium

The next step to completing the integration of Node with Chromium is to integrateNode's start function with Chromium's rendering process. Node.js kicks off with astart function that handles executing code. To get Node.js to work with Chromium,the start function has to be split into parts so that it can execute in line with Chro-mium's rendering process. This is a bit of custom code within NW.js that's used tomonkey-patch the start function in Node.

Once this is done, Node is able to work inside of Chromium. This is how NW.js isable to make Node.js operate in the same place as the front-end code that's handledby Chromium.

That rounds up a bit about how NW.js operates under the hood. In the next sec-

tion, we'll explore the different approach taken by Electron.

How does Electron work under the hood?Electron's approach shares some similarities in terms of the components used to pro-vide the desktop framework, but differs in how it combines them. It's best to start bylooking at the components that make up Electron. To see an up-to-date source codedirectory, take a look at http://mng.bz/ZQ2J.

Figure 6.4 shows a representation of that architecture at a less-detailed level. Elec-tron's architecture emphasizes a clean separation between the Chromium source codeand the app. The benefits of this are that it makes it easier to upgrade the Chromiumcomponent, and it also means that compiling Electron from the source code becomesthat much simpler.

6.2

Electron

Atom

App

Browser

Renderer

Common

Chromium source code

Figure 6.4 Electron's source code architecture. This diagram shows the main blocks of components that make up Electron.

How does Electron work under the hood?

113

The Atom component is the C++ source code for the shell. It has four distinct parts(covered in section 6.2.2). Finally, there's Chromium's source code, which the Atomshell uses to combine Chromium with Node.js.

How does Electron manage to combine Chromium with Node.js if it doesn't rely

on patching Chrome to combine the event loops for Chromium and Node.js?

6.2.1

Introducing libchromiumcontent

Electron uses a single shared library called libchromiumcontent to load Chromium'scontent module, which includes Blink and V8. Chromium's content module is respon-sible for rendering a page in a sandboxed browser. You can find this library on GitHubat https://github.com/electron/libchromiumcontent.

You use the Chromium content module to handle rendering web pages for the appwindows. This way, there's a defined API for handling the interaction between the Chro-mium component and the rest of Electron's components.

6.2.2

Electron's components

Electron's code components are organized inside Electron's Atom folder into thesesections:

 App Browser Renderer Common

We'll look at what each of those folders contains in a bit more detail.

APPThe App folder is a collection of files written in C++11 and Objective-C++ that handlescode that needs to load at the start of Electron, such as loading Node.js, loading Chro-mium's content module, and accessing libuv.

BROWSERThe Browser folder contains files that handle interacting with the front-end part ofthe app, such as initializing the JavaScript engine, interacting with the UI, and bind-ing modules that are specific to each OS.

RENDERERThe Renderer folder contains files for code that runs in Electron's renderer processes.In Electron, each app window runs as a separate process, because Google Chrome runseach tab as a separate process, so that if a tab loads a heavy web page and becomesunresponsive, that tab can be isolated and closed without killing the browser and therest of the tabs with it.

Later in this book, we'll look at how Electron handles running code in a main pro-

cess, and how app windows have their own renderer processes that run separately.

114

CHAPTER 6 Exploring NW.js and Electron's internals

COMMONThe Common folder contains utility code that's used by both the main and rendererprocesses for running the app. It also includes code that handles integrating the mes-saging for Node.js' event loop into Chromium's event loop.

Now you have an idea of how Electron's architecture is organized. In the next sec-tion, we'll look at how Electron handles rendering app windows in a process that'sseparate from the main app process.

6.2.3 How Electron handles running the app

Electron handles running apps differently than NW.js. In NW.js, the back-end andfront-end parts of the desktop app share state by having the Node.js and Chromiumevent loops integrated and by having the JavaScript context copied from Node.js intoChromium. One of the consequences of this approach is that the app windows of anNW.js app end up sharing the same reference to the JavaScript state.

With Electron, any sharing of state from the back-end part of the app to the front-end part and vice versa has to go through the ipcMain and ipcRenderer modules. Thisway, the JavaScript contexts of the main process and the renderer process are keptseparate, but data can be transmitted between the processes in an explicit fashion.

The ipcMain and ipcRenderer modules are event emitters that handle interpro-cess communication between the back end of the app (ipcMain), and the front-endapp windows (ipcRenderer), as shown in figure 6.5.

Application

ipcmain

Application window

Application window

ipcRenderer

ipcRenderer

Figure 6.5 How Electron passes state via messaging to and from the app windows. In Electron, each app window has its own JavaScript state, and communicating state to and from the main app process happens via interprocess communication.

This way, you have greater control over what state exists in each app window as well ashow the main app interacts with the app windows.

Regardless of which desktop framework you choose to build your app with, keepin mind how you want data to be accessed and altered within your app. Dependingon what your app does, you may find that one framework is better suited to yourneeds than the other, and in cases where you're working with those desktop appframeworks already, you'll want to keep in mind how NW.js and Electron handleJavaScript contexts.

Now let's take a closer look at how Electron and NW.js make use of Node.js.

How does Node.js work with NW.js and Electron?

115

6.3

How does Node.js work with NW.js and Electron?Node.js interacts with the hybrid desktop environments of NW.js and Electron simi-larly to server-side apps. But to understand the few differences, we'll look at the wayNode.js is integrated into NW.js.

6.3.1 Where Node.js fits into NW.js

NW.js's architecture consists of a number of components, Node.js being one of them.NW.js uses Node.js to access the computer's file system and other resources that wouldotherwise not be available due to web browser security. It also provides a way to accessa large number of libraries through npm (figure 6.6).

Access to computerresources in Node.js

Visual renderingof app in Blink

browser component

Node.js

Blink

V8

npm

Figure 6.6 How Node.js is used within NW.js for desktop apps

NW.js makes Node.js available through the context of the embedded web browser,which means you can script JavaScript files that access both Node.js's API and APImethods related to the browser's JavaScript namespace—such as the WebSocketclass, for example. In earlier examples in the book, you've written code that hasaccessed Node.js's file system API in the same file that also accesses the DOM in thescreen.

This is possible through the way that NW.js has merged the JavaScript namespacesof Node.js and the Blink rendering engine, as well as merged the main event loops ofboth, allowing them to operate and interact in a shared context.

6.3.2 Drawbacks of using Node.js in NW.js

Because of how NW.js merges the JavaScript contexts of the Blink rendering engineand Node.js, you should be aware of some of the consequences that come with thisapproach. I'll describe what those things are and how you can handle them so thatthey don't trip you up.THE NODE.JS CONTEXT IS ACCESSIBLE TO ALL WINDOWSI've talked about Node.js and Blink sharing the same JavaScript context, but how doesthat work in the context of an NW.js app where there are multiple windows?

In Blink, each window has its own JavaScript context, because each window loads aweb page with its own JavaScript files and DOM. The code in one window will operate

116

CHAPTER 6 Exploring NW.js and Electron's internals

in the context of that window only, and not have its context leak into another win-dow—otherwise, this would cause issues with maintaining state in the windows as wellas security issues. You should expect the state that exists in one window to be isolatedto that window and not leak.

That said, NW.js introduces a way to share state between windows via the waythat Node.js's namespace is loaded into the namespace of Blink to create a sharedJavaScript context. Even though each window has its own JavaScript namespace,they all share the same Node.js instance and its namespace. This means there's away to share state between windows through code that operates on Node.js'snamespace properties (such as the API methods), including via the require func-tion that's used to load libraries. Should you need to share data between windowsin your desktop app, you'll be able to do this by attaching data to the global objectin your code.

COMMON API METHODS IN CHROMIUM AND NODE.JSYou may know that both Node.js and Blink have API methods with the same name andthat work in the same way (for example, console, setTimeout, encodeURIComponent).How are these handled? In some cases, Blink's implementation is used, and in othercases, Node.js's implementation is used. NW.js opts to use Blink's implementation ofconsole, and for setTimeout, the implementation used depends on whether the fileis loaded from a Node.js module or from the desktop app. This is worth keeping inmind when you're using those functions, because although they're consistent in theirimplementations of inputs and outputs, there might be a slight difference in speedof execution.

6.3.3 How Node.js is used within Electron

Electron uses Node.js along with Chromium, but rather than combining the eventloops of Node.js and Chromium together, Electron uses Node.js's node_bindings fea-ture. This way, the Chromium and Node.js components can be updated easily withoutthe need for custom modification of the source code and subsequent compiling.

Electron handles the JavaScript contexts of Node.js and Chromium by keeping theback-end code's JavaScript state separate from that of the front-end app window'sstate. This isolation of the JavaScript state is one of the ways Electron is different fromNW.js. That said, Node.js modules can be referenced and used from the front-endcode as well, with the caveat that those Node.js modules are operating in a separateprocess to the back end. This is why data sharing between the back end and app win-dows is handled via inter-process communication, or message passing.

If you're interested in learning more about this approach, check out this site from

GitHub's Jessica Lord: http://jlord.us/essential-electron/#stay-in-touch.

Summary

117

6.4

SummaryIn this chapter, we've exposed some differences between NW.js and Electron by explor-ing how their software components work under the hood. Some of the key takeawaysfrom the chapter include the following:

 In NW.js, Node.js and Blink share JavaScript contexts, which you can use for

sharing data between multiple windows.

 This sharing of JavaScript state means that multiple app windows for the same

NW.js app can share the same state.

 NW.js uses a compiled version of Chromium with custom bindings, whereas

Electron uses an API in Chromium to integrate Node.js with Chromium.

 Electron has separate JavaScript contexts between the front end and the

back end.

 When you want to share state between the front end and back end in Electron

apps, you need to use message passing via the ipcMain and ipcRenderer APIs.

In the next chapter, we'll look at how to use the various APIs of NW.js and Electron tobuild desktop apps—specifically, at the way in which you can craft an app's look andfeel. It will be more visual, and hopefully more fun.

Part 3

Mastering Node.jsdesktop applicationdevelopment

Many APIs are available in desktop application frameworks to help pro-

vide features like accessing the webcam and clipboard, opening and saving filesto the hard disk, and more. This part explores the various ways in which NW.jsand Electron allow you to add a number of features to your desktop apps.

Chapters 7, 8, and 9 look at ways to control the look and feel of your desktopapps, from controlling the window dimensions and full-screen behavior, throughto creating menus and making tray apps.

Chapter 10 explores how to implement drag-and-drop functionality in yourapps through HTML5 APIs, and chapter 11 shows you how to integrate webcamfunctionality for taking photos from your computer's webcam and saving themto disk.

Chapters 12 and 13 deal with different ways you can store and access app data

and how to access data in the OS clipboard.

Toward the end of this part of the book, we'll look at using keyboard short-cuts to implement controls for a game, and how to integrate a real-time Twitterfeed into a desktop notifications app.

Controlling how yourdesktop app is displayed


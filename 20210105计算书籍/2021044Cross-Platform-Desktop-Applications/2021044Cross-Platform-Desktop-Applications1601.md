 Debugging Electron apps with Devtron

Humans write programs, and humans make mistakes, even ones that automatedtesting tools won't capture. If you're lucky, you'll be able to get ahold of a stacktrace that reports what error occurred and where it happened in the code.

However, some bugs are subtler and won't necessarily result in an error. Tofind these bugs, you need to use tools that can help to diagnose what's going onin the code, as well as how the app is performing on the computer. Performanceis a feature.

In this chapter, I'll take you through how to use the available debugging tools;I'll show how to identify and resolve bottlenecks in your front-end code with thedeveloper tools available in both Electron and NW.js, as well as debugging tools for

264

Knowing what you're debugging

265

Node.js that can be used to debug errors and analyze performance. I'll also show youtools for tracking errors that are occurring in your apps as customers use them. Let'smurder some bugs (code ones, not the ones with legs).

17.1 Knowing what you're debugging

The first thing you must do when debugging a Node.js desktop app is identify whatthe problem is before you can determine where it's happening in your app. Varioustechniques can be deployed to identify the problem, such as root cause analysisusing the five whys, or trying to read the stack trace of the bug (if you're lucky enoughto get one).

Debugging a Node.js desktop app is an interesting challenge because the bug/per-

formance issue could be in any of the following areas:

 Quirks with Chromium's browser and its approach to rendering and executing

HTML, CSS, and JavaScript

 Front-end bugs and performance issues Node.js bugs and performance issues If you're using NW.js, the way NW.js handles sharing state between the app win-

dows and the app process

 If you're using Electron, the way Electron keeps state separate between the

app windows

 The bugs, quirks, and performance issues of each of those desktop frameworks The app's source code

That's quite a lot of ground to cover, and unless you're a memory champion, chancesare you won't have a complete and comprehensive knowledge of all the issues in allthose areas. In that case, your best course of action is to apply root cause analysis.

Let's walk through an example. Say you spot a bug in a CRM app; clicking a con-tact's email does not open up the computer's email client with a new message for thecontact. In this case, you know what the expected result is, and because you know whataction would trigger it, you can begin a process of working through it, as illustrated infigure 17.1.

You can establish how to go about debugging the issue based on working througha set of questions. The questions in figure 17.1 are tailored to the questions a devel-oper would ask when debugging the issue, but a more generic approach would be toask「Why?」at least five times, in order to establish what's going wrong.

266

CHAPTER 17 Improving app performance with debugging

Input

CRM app

John Smith

john.smith@example.com

Expected output

Email client

To:

john.smith@example.com

Subject:

What does the click do?

How does this happen?

It opens a link.

Where is that code?

A bit of code opens the mail client

with a prefilled recipient field.

In the app.js file.

Is that loaded directly

in the app's html?

Yes.

Figure 17.1 Identifying the location of the issue's root cause so you can choose which tool to debug it with

Ok. Debug the issue using the

browser's developer tools.

17.1.1 Identifying the location of the root cause

Debugging a Node.js desktop app is an interesting scenario, because the Node.js con-text is shared between the client-side and server-side parts of your app. The best way towork in this scenario is to identify what the root cause is—and where it is—before youopen any debugging tools and start poking around. Knowing where in the code theroot cause is will help you to determine which debugging tool you should use to diag-nose the problem.

If the code is directly loaded by the app's HTML in a script tag, then you'll want todebug the problem using the front-end developer tools (Chrome's Developer Tools).However, if the code is not directly loaded by the client (say, it's a Node.js module, ora script loaded via require), then you might want to use Node.js debugging tools toget to the root cause.

When you know where your root cause lies, you can begin debugging it. Let's move

on to how to debug a client-side error with the browser developer tools.

Knowing what you're debugging

267

17.1.2 Debugging with the browser developer tools

As you develop a desktop app using NW.js, you'll notice there's a pesky little toolbarthat displays above the app, much like the toolbar shown in a web browser (becausethat's effectively what the app is running in—a custom web browser). This toolbarcontains a few goodies that you'll now appreciate. If you don't see this toolbar, checkthat the setting for the window toolbar in your app's package.json file is set to true, asin the following code snippet:

{ "window": { "toolbar": true }}

With the app window toolbar enabled, you now have access to the app window'sdebugging tools, which are identical to the developer tools available in GoogleChrome. To access them, click the cog icon to the right of the address field, as shownin figure 17.2.

Developertools button

Figure 17.2 The toolbar in an NW.js app. Notice the cog icon to the right of the address field. When things are slow or broken in your NW.js app, this cog is your friend.

Clicking the cog icon brings up the developer tools window, which looks like figure 17.3. This is how debugging works in NW.js. As for Electron, there's a differentapproach. In keeping with Electron's modular architecture, to load the ChromeDeveloper Tools in an Electron app, you need to make a call on the app's browserwindow, like so:

new BrowserWindow({width: 800, height: 600}).webContents.openDevTools();

This will show Google Chrome's Developer Tools, similar to what you see in figure 17.3.

268

CHAPTER 17 Improving app performance with debugging

Tabs fordifferent tools

The app's CSS

The app's HTML

Figure 17.3 The Developer Tools window for an NW.js app. If you've done front-end web development before, this window might look familiar to you. It's identical to the developer tools that you get in Google Chrome.

What if my app doesn't have a window?Luckily, there's another way to run the debugger without needing to click the cog icon.You can run the NW.js app with remote debugging enabled by passing the followingparameters when running your app from the command line:

--remote-debugging-port=PORT

This will enable you to open a web browser on the port you specified, and you'll beable to view the Developer Tools from that page.

The Developer Tools window provides a number of handy little tabs, as shown in fig-ure 17.4, that enable the following:

 The Elements tab allows you to browse the HTML of the app and see what CSS

styling and JavaScript events are attached to HTML elements in the page.

Knowing what you're debugging

269

 The Network tab shows you the time it takes and the order in which the files are

loaded by the app.

 The Sources tab allows you to edit the source files live, so that you can debug

your app code as the app is running.

 The Timeline tab lets you see how much time is spent by the browser executingdifferent parts of the JavaScript, or rendering elements in the page, or theamount of memory consumed.

 The Profiles tab profiles the CPU to see where in the code the most CPU cycles

are being spent.

 The Resources tab explores what data resources are used by the app, such as

local storage data.

 The Audits tab performs an audit of the app to find ways you can improve the

app's performance.

 The Console tab allows you to access the current JavaScript context via a console.

Figure 17.4 The tabs in the Developer Tools window

Table 17.1 shows a breakdown of what each tab in figure 17.4 does and how it can beused.

Table 17.1 What the Developer Tools tabs do

Developer Tool tab

What it does

Allows you to inspect and edit the DOM of the app. Useful for making visual changes on the fly and for fixing visual bugs (usually involving CSS).

Shows how long the app's files take to load, and the order that they load in. Useful for optimizing app load times.

Shows the source code of the files that are loaded by your app and allows you to insert breakpoints and edit the source code live, rather than having to reload the app after making the change in your text editor or IDE.

Allows you to see how much time the browser spends doing low-level tasks for the app, from executing the JavaScript code to rendering different DOM elements on the page. Great for deep-level analysis of your app's performance.

Records profiling data about your app's CPU profile or memory usage. Good for spotting processing bottlenecks in your app's code, or memory leaks that can occur as well.

Shows you both the contents of files loaded by the app and data that's stored by the app, such as local storage, cookies, session information, and even Web SQL (though that's a deprecated standard). Good for inspecting data stored by the app.

Elements

Network

Sources

Timeline

Profiles

Resources

270

CHAPTER 17 Improving app performance with debugging

Table 17.1 What the Developer Tools tabs do (continued)

Developer Tool tab

What it does

Audits

Console

Analyzes your app to see if there are any changes you can make to improve per-formance, and makes recommendations. A handy tool for helping you make improvements, and it's free.

Provides a console for running JavaScript code. Useful for testing some lines of JavaScript, inspecting the DOM, and checking out the app state.

Table 17.1 gives you an idea of the available options in the Developer Tools windowwhen debugging issues in the client-side code. Later in the chapter, you'll dive intousing these tools to help spot performance issues in your code so that you can resolvethem. For now, we'll turn our attention to the first purpose of debugging: fixing bugs.

CAN'T I USE DEVELOPER TOOLS TO DEBUG THE WHOLE APP? Yes, but only if yourapp isn't loading any other Node.js modules. If it is, then you have to useother debugging tools to see what's going on inside them. This is becausethere's a bug in the Developer Tools toolbar where the Sources tab isn't ableto show Node.js modules that have been loaded. This bug is known by theNW.js team.

17.2 Fixing bugs

Bugs are a part of software. In an ideal world, they'd never exist because the humanswho wrote the code wouldn't make mistakes. But we do make mistakes (ask anyonewho's accidentally filled up their car with the wrong kind of gasoline), so we have tospot them, and then we have to fix them.

When it comes to building desktop apps with Electron or NW.js, if your bug raisesa JavaScript error object, then you're in luck. You'll be able to debug it from either theConsole tab on the app window's Developer Tools window, or from the command-lineoutput that appears when running the app locally (if your app is running with NW.js).Say you add a file called beetle.js to an app that you're currently working on, and thefile has faulty code that reads like this:

check.line;

Then, you load the beetle.js file into the app.js file via a simple require statement:

require('./beetle');

Load the app from the command line as shown in figure 17.5 (the nw command), andnote the output from the app.

The stack trace in the Terminal can be a bit of an eyeful to read and figure out.Thankfully, you can also see the error in the Console tab in a more readable format, asshown in figure 17.6.

Fixing bugs

271

The error message

The command you ran

Figure 17.5 The error occurring in an app, and the stack trace that it produces

The stack trace

The error message, andan easier-to-digest trace

Figure 17.6 The same error as displayed by the Console tab on the Developer Tools window

In this simple example, the error is easy to spot because it raises a JavaScript errorobject. If you're lucky, any bugs that you encounter in your desktop apps will raiseJavaScript errors, providing you with a stack trace that you can read, and thereforedebug the error easily.

But not all bugs will raise a JavaScript error. In those cases, you need to have a fewmore tools at your disposal to determine what's going on. The next section showsextra tools to help you do this.

17.2.1 Using Node.js's debugger to debug your app

In NW.js, you can implement debugging either from the command line or from theDeveloper Tools, depending on whether the code you're looking to debug is loadedvia the client or via Node.js. In Electron, you can debug the Node.js process witheither Node.js's debugging support or by using the Node Inspector module.

272

CHAPTER 17 Improving app performance with debugging

As frameworks that run Node.js, both NW.js and Electron provide the added bene-fit of the debugging tools available in the Node.js ecosystem. Over the years, the tool-ing has evolved to enable developers to get a good understanding of what exactly isgoing on under the hood, providing stack traces at a simple level, and going rightdown to flame graphs at a more in-depth level.

Table 17.2 shows what tools are on offer, what they work with, and what they're

used for.

Table 17.2 Node.js debugging tools

Node.js debugging option

Works with

Used for

Node Debug

Node Inspector

React Inspector

NW.js, Electron

NW.js, Electron

Electron

Back-end code

Back-end code

Isomorphic React apps

NODE DEBUGNode.js ships with debugging tools by default. These tools let you pause the executionof your code by adding breakpoints in the code, and you can iterate the execution ofyour code step by step. This is useful when you're investigating your code, and whenthe cause of a bug isn't clear.

For standard vanilla Node.js apps, if you want to use the debugger, first append this

line of code in the place where you'd like the debugger to pause code execution:

debugger;

Then, when executing your Node.js app, pass the following commands to the com-mand line:

node debug <NAME_OF_FILE>

This brings up an interactive REPL once the app has reached the debugger call. Youthen have the ability to step through the code by passing the commands shown intable 17.3 to the interactive REPL.

Table 17.3 Commands to pass to the interactive REPL

Key

Command

What it does

Continue

Next

Step in

Step out

Pause

Continues executing the code

Steps to the next line of execution

Steps into the line of execution to see where it goes

Steps out of the line of execution to where it is called

Pauses execution of the program

c

n

s

o

pause

Fixing bugs

273

You can use these commands to control the flow of execution in the app and see stepby step what the program's doing, which is handy with a hard-to-spot bug.

The difficulty with this approach is that there may be a point deep in your codewhere you would like to pause execution, but to stop at each line of code being exe-cuted before reaching it will take a lot of time (and a lot of key presses). Imagine afairly small app with 20 files, each being 100 lines of code—you probably wouldn'twant to have to press c for continue that many times. Plus, if you try to press c for con-tinue, then you may end up going past the line where you wanted the program topause. For this job, you need breakpoints.

Breakpoints are a way of getting the code to stop at a particular point in the code-base. Rather than step through the code line by line to debug an app at differentpoints of execution, you can insert breakpoints to pause execution, allowing you toinspect the state of the code.

When you're debugging the app in the interactive debugger REPL, you'll have

extra global functions available to you, listed in table 17.4.

Table 17.4 Available global functions

Function

What it does

setBreakpoint()

setBreakpoint(line)

Sets the breakpoint on the current line that the app is on

Sets the breakpoint on a given line number in the cur-rent file

setBreakpoint(fn())

Sets the breakpoint on the calling of a named function

setBreakpoint(filename, line)

Sets the breakpoint on a given filename and line number

clearBreakpoint(filename, line)

Clears the breakpoint on the given filename and line number

This is a brief overview of what's involved with using Node.js's built-in debuggingtools. In the context of NW.js, debugging involves a bit more work. That's becausewhen you execute an NW.js app, multiple Node.js processes are happening in thebackground. You can connect to an existing Node.js process with the debugger, butwhich process should you connect to, and how do you connect to it remotely?DEBUGGING THE APP REMOTELYNode.js's debugger doesn't necessarily have to run inside the same process as the app;it can be attached to an external Node.js process that's already running. You can dothis by running the following command:

node debug –p PROCESS_ID

This allows you to connect a debugger to a running Node.js app. You need to get theprocess ID of the app that NW.js runs and pass it into the preceding command, in

274

CHAPTER 17 Improving app performance with debugging

place of the PROCESS_ID text. There are a couple of ways to do it on Mac OS/Linuxplatforms, and one on Windows:

 On Windows, use Task Manager On Mac OS, use Activity Monitor On Linux, use Task Manager (or ps from the command line)

The easiest way to get the process ID (regardless of what OS you're on) is to open upthe tool that shows the list of running apps/processes. On Windows, this is the TaskManager app; on Mac OS, it's the Activity Monitor app; on the various flavors of LinuxGnome, users know it as the System Monitor app; and for KDE users, it's the SystemActivity app.

On Mac OS's Activity Monitor app, type in the name node, and you'll see a list ofprocesses running that match that term, as shown in figure 17.7. The process ID inthis figure shows that the NW.js app's node process is running with a process ID of10169. Put this process ID into the node debug command, which lets you attach thedebugger to the running NW.js app's node process:

node debug –p 10169

Figure 17.7 Mac OS's Activity Monitor app. The app's process that's running is highlighted, and you can record the process ID in the PID column (10169 in this case).

Fixing bugs

275

This means you can go debug the NW.js app's node process remotely. In the next sec-tion, we'll look at ways in which you can debug errors on the client.

17.2.2 Using NW.js's developer tools to debug your app

The Developer Tools window in NW.js is identical to Google Chrome's DeveloperTools. Google Chrome's Developer Tools have gone a long way toward helping devel-opers debug their web apps, and reuse knowledge and techniques to debug theirNW.js apps.

To use the developer tools with NW.js, install the SDK version of NW.js. You caneither visit the NW.js website and install the SDK version of NW.js from there, or installthe SDK version of NW.js via npm:

npm install nwjs --nwjs_build_type=sdknode_modules/.bin/nw install 0.16.1-sdknode_modules/nw/bin/nw

Originally, with versions 0.12 of NW.js and earlier, the SDK was a built-in part of NW.js,but latter versions of NW.js separated this component out. Although this means thereare extra steps involved in developing your NW.js app, the benefit is that you can builda smaller version of your app for the binary that doesn't include the developer tools,saving megabytes on the binary size.

Once you have the SDK version of the app installed, you can run your app andopen the developer tools by either pressing F12 on your keyboard for Windows andLinux, or by pressing the Command-Alt-I on Mac OS. You can expect to see the Devel-oper Tools window shown in figure 17.8.

Figure 17.8 The Developer Tools window for NW.js

276

CHAPTER 17 Improving app performance with debugging

ELEMENTS TABWhen you bring up the Developer Tools window on an NW.js app, the Elements tab isselected by default, as shown in figure 17.8. This tab lets you inspect the DOM, in casethere's a bug in the HTML, a mistyped path for an asset, or a styling bug on the app(see figure 17.9).

Figure 17.9 The Element tab on the Developer Tools window. On the left, you see the HTML for the app, and on the right are the CSS styles that affect the selected DOM element (in this case, the body tag).

The Elements tab also allows you to inspect the CSS styles that are applied to a DOMelement and edit them inline so that you can fix visual bugs that are occurring in theapp. You can edit the DOM here as well, so you can try out changes before makingthem in the app code.

If you're trying to debug an issue with the JavaScript code, you have two options:

 You can use the Console tab to interact with the app and inspect the JavaScript

context there.

 You can use the Sources tab to insert breakpoints and watch variables to see

what values they have at different points of the app's execution.

Fixing bugs

277

CONSOLE TABIf you've ever done any form of front-end web development and needed to debug anissue with the JavaScript on the front end, chances are you've seen the Console taband played with it a bit. Figure 17.10 shows what you can expect to see.

Figure 17.10 The Console tab in the Developer Tools window. If you call window.onload in the Console tab, you can see the code for that function on display. Also, any console.log statements in the code will output their content here.

The purpose of the Console tab is to be able to interactively debug your app's JavaScriptstate without needing to resort to inserting breakpoints and pausing/resuming theapp's execution.

If you open up the developer tools for the Cirrus app and click the Console tab,

you can type in statements to execute and see what happens.

SOURCES TABThe Sources tab has a lot of handy features crammed into it for debugging, as you cansee in figure 17.11.

The key debugging tools in the Sources tab are on the right-hand panel. Here, youcan insert breakpoints to stop code execution when it reaches a particular point. Theother nice thing you can do is look out for the value of variables in the code, such asthe value of the currentFile variable in the app.js file, which is used to store the filepath for the HTML file that's opened by the WYSIWYG editor. If you wanted to checkfor the current value of that variable, you could add a watch expression to the app byclicking the + button on the Watch Expression header and then typing currentFileas the variable name to watch out for.

After doing this, if you've used the app, you should see the value of the current-File variable set to the file path of the file that you were editing in the WYSIWYG edi-tor. In this case, my screen looks like figure 17.12.

278

CHAPTER 17 Improving app performance with debugging

Your application'sfiles are here.

The file sourcecode is displayedand editable here.

Debugging optionsare here in the right-hand panel.

Figure 17.11 The Sources tab on the Developer Tools window

With the Watch Expressions tool, youcan look at the current value of thecurrentFile variable, and see if it iswhat you expect.

Figure 17.12 Observing a variable's current value

Resolving performance issues

279

As you run the app, you can click the refresh button in the Watch Expressions headerto show what the current value of a variable is at intervals.

A nice touch to the developer tools is that in Chrome you can edit your sourcecode directly from the Source tab; but, unfortunately, this feature doesn't work onNW.js, so for the moment you'll need to make do with editing the files in your text edi-tor of choice.

Being able to add breakpoints, inspect for JavaScript errors, and observe the valueof variables allows developers to spot bugs in their app and resolve them. The otherkind of issue that can occur isn't necessarily a bug (depending on whom you ask), butmore an issue of speed: performance. The next section looks at ways you can diagnoseperformance issues and how to resolve them.

17.3 Resolving performance issues

The issues that affect the performance of desktop apps are the same issues that affectthe performance of web apps:

 How quickly content assets are loaded by the browser How much memory and CPU are consumed by executing the JavaScript The frame rate at which the browser is able to render the page

Performance optimization tends to be an afterthought until the app is live and perfor-mance issues are impacting app usability. The plus is that it's easy to spot the error,resolve it quickly, and deploy the changes to users quickly.

With a desktop app, the user is stuck with that version, unless it has self-updatingfunctionality enabled. Either way, there's a greater pressure to get it right the first time(because your users might not be as patient). In this section, we'll explore what eachof the tabs on the Developer Tools window does and what it's useful for when you'retrying to spot performance issues with your desktop app.

17.3.1 Network tab

With performance issues, the first place to look is how long it takes to load the HTML,CSS, and JavaScript files that make the app. In the Developer Tools window, the Net-work tab shows how long it takes for those assets to load, be parsed, and render in thebrowser, as shown in figure 17.13.

For web apps, the Network tab is useful because it shows you how long it takes forthe assets to load and gives you a benchmark to measure against. As you can see in fig-ure 17.13, the app looks like it loads pretty quickly (128 ms—the blue, right-mostline), which is due in part to the fact that the assets are being loaded from the com-puter's hard disk, rather than from a web server on the internet. Nevertheless, theNetwork tab is useful for building desktop apps:

 You can see the size of the files, whether they're getting too big, and whether

they should be minified and gzipped to reduce their size.

 You can see how many assets are being loaded by the app and check whether

concatenating them together will improve the performance of the app.

280

CHAPTER 17 Improving app performance with debugging

This line indicates whenthe files finished loading.

The order in which files areloaded by the application.

Figure 17.13 The Network tab panel

This line indicates whenthe HTML is parsed andrendered.

This tab gives a good indication of whether your app is becoming bloated; if so, you'llnotice the number of assets loaded by the app grows and begins to impact the loadingtime. Keep an eye on the loading metric as your app grows.

Once the app has loaded, the next step is to look at how it performs. For this, you

have some other tabs in the Developer Tools window that can help out.

17.3.2 Timeline tab

Next to the Network tab is the Timeline tab—the Swiss army knife of the DeveloperTools window because it has so many ways to display performance data. It's a helpfultab when it comes to optimizing the performance of your app with regard to the fol-lowing:

 Tracking how much memory is used in the JS heap Seeing how long the app spends performing various browser-based tasks Seeing what browser-rendering events are causing jank

This tab provides lots of data-visualization features to explore, but you need to recordthe performance data first. Click the Timeline tab, and then click the red record but-ton, as shown in figure 17.14.

Resolving performance issues

281

Click on this tobegin recordingperformance data.

Figure 17.14 The record button on the Timeline tab

Once you've clicked the record button, you're recording performance data. At thispoint, you can use the app like you normally would, or if there's a particular actionthat you've noticed is slow or janky, perform that action in the app.

Jank refers to when the browser animation and renderingWHAT IS JANK?drops below 60 frames per second and you begin to notice that the page ren-dering judders and has some stutter in rendering elements on the screen.

When you're happy that you've recorded the relevant performance data for what youwanted to measure, click the record button again to stop recording the performancedata, and you should now see a screen with lots of data, like in figure 17.15.

You'll now have a lot of data to play with and inspect. Figure 17.15 has drilled downon a particular point in the timeline where the JS heap jumps up rapidly, indicatingthat there's a point where something happens to cause this. If you explore the eventsthat occur during the use of the app, you'll see that clicking from the design view tothe code view is responsible for triggering the spike. You now have enough informa-tion to target where you explore the code and optimize it.

As you check and uncheck different options in the Timeline tab, different visual-izations of the data are displayed for you. I recommend browsing those tools to get afeel for them, as there's a lot to do in that tab alone. Next, we'll check out the Pro-files tab.

282

CHAPTER 17 Improving app performance with debugging

Here you can see JavaScriptevents and memory useover time.

Here you can see wheretime is spent in the app.The white part of the piechart is idle time.

Here you can see memoryobject counts over time,including when they spike.

Figure 17.15 The Timeline tab displaying performance data

17.3.3 Profiles tab

The Profiles tab offers the ability to trace the following performance areas:

 Where the app is spending its time (in terms of CPU cycles) executing code What the memory usage is like as the app is used, and what kinds of memory

objects are being created over time

 Where potential memory leaks may be occurring in the code

When you click the Profiles tab, you're presented with three options, shown in table 17.5.

Resolving performance issues

283

Table 17.5 Profile tab options

Option

What it does

Collect JavaScript CPU Profile

Shows where your app is spending time executing code

Take Heap Snapshot

Takes a snapshot of the current memory heap in the app

Record Heap Allocations

Records memory heap over a period of time

Depending on the nature of your performance problem, you'll want to try out the dif-ferent options and see what data you get back. To use one of the options listed on thetab, click the Start button shown on the tab (let's choose the CPU profile in this case)and use the app. When you're finished, you'll see something like figure 17.16.

Here you can see where the CPUspends its time executing functionsin the application's code

Figure 17.16 The Profiles tab with the CPU profile results

The results from doing a CPU profile analysis can also be displayed as a flame chart.Click the toolbar drop-down to change how the results are displayed, and you shouldsee something like figure 17.17.

The flame graph shows you where time is being spent by your app and helps to

spot any bottlenecks.

Being able to analyze the performance qualities of your desktop app comes inhandy when you're trying to make sure that your product works for your customersbefore it goes out there.

Having now covered NW.js's developer tools, let's look at what Electron has to offer.

284

CHAPTER 17 Improving app performance with debugging

Figure 17.17 The CPU profile results displayed as a flame chart

17.4 Debugging Electron apps

Like NW.js, Electron uses Chrome's Developer Tools under the hood. Electron pro-vides access to the developer tools either from the View menu in the app's main menuor by pressing Ctrl-Shift-I (Command-Shift-I on Mac OS).

If you try to open the developer tools in one of your Electron apps, you'll see a new

window pop up, looking like figure 17.18.

Figure 17.18 Electron's Developer Tools window. The nice thing about Chrome's Developer Tools is that it detects browser features used in your app and emits warnings in the console about them being deprecated in the near future.

Debugging Electron apps

285

The Developer Tools window is almost the same as the one shown in NW.js, but theorder of the tabs is different, though they're the same as the ones in NW.js. In thatrespect, it's nice because you can use the same tools to debug both NW.js and Elec-tron apps.

That said, Electron's approach to rendering app windows as separate processesrather than all in a single app process makes it a bit more involved in terms of debug-ging what's happening in each app window. Fear not, though—Electron has a dedi-cated debugging tool for handling this, called Devtron.

17.4.1 Introducing Devtron for debugging Electron apps

Devtron is a debugging tool for Electron apps that allows you to inspect some of themore intricate aspects of your Electron apps, such as the following:

 How your app loads dependencies in both the main back-end process and in

each renderer front-end process

 Inspecting data messages that are passed between the main and renderer

processes

 Linting the code to make sure you haven't incorrectly scoped a variable or omit-

ted a break command in a case statement

 Showing what events are occurring in the Electron app so you can see whethercertain things are happening, such as when a window is closed or when an appregisters itself as being ready

Devtron is built on top of Chrome's Developer Tools, so installing it is a two-step pro-cess. First, install it as a development dependency for your Electron app via npm:

npm i devtron --save-dev

Next, complete the installation process by running your Electron app. Once you'vegot your Electron app up and running, open the developer tools, either by pressingCtrl-Shift-I (Command-Alt-I for Mac OS) to view the tools, or by clicking the Viewmenu and selecting Toggle Developer Tools, as shown in figure 17.19.

Figure 17.19 Opening the developer tools from an Electron app's main toolbar

286

CHAPTER 17 Improving app performance with debugging

With the developer tools open, click the Console tab and run the following command:

require('devtron').install()

You should see a new tab appear (the Devtron tab) in the Developer Tools window, asshown in figure 17.20.

Figure 17.20 The Devtron tab at the end of the Developer Tools

The Devtron tab is built as an extension of the developer tools, which means you canrun it alongside the rest of the Developer Tools for the app. If you click it, you canexpect to see something like figure 17.21.

Figure 17.21 The Devtron tab in the Developer Tools

In the sidebar on the left of the Developer Tools window, you have five menu items.You'll go through each of them one by one, with the exception of the last menu item(which is information and not a debugging option).

REQUIRE GRAPHThe Require Graph item is used to list how npm module dependencies are loadedin the renderer and main processes by the app. The idea is that by looking at thedependency graph information, you can see not only the order in which the mod-ules are loaded by the main/renderer process, but also see how big they are (andtherefore how much they contribute to the whole size of the app). You can also

Debugging Electron apps

287

search through the modules by their name and filename with the search input fieldat the top.

To begin using Require Graph, you first need to check whether you want to visual-ize the dependency graph for the main process or the renderer process, and click thetab that represents the process you choose. Then, click Load Graph in the top right ofthe window. When you do this on the renderer process for the Lorikeet app, you cansee the information presented in the dependency graph shown in figure 17.22.

Figure 17.22 The dependency graph for the renderer process in Lorikeet Electron. Notice that the app's total file size is 355 KB—not bad for a simple file explorer app.

The Require Graph tab shows that the index.html file loads first, followed by Electronloading its required files, and then the rest of Lorikeet's files are loaded. The size ofthe files is also relatively small, which is nice because it shows that you can pack quite abit of functionality into the desktop app without making it monolithic.

EVENT LISTENERSThe Event Listeners menu item shows events emitted during the app's lifecycle andallows you to see what the code looks like for binding on them. The idea is that youcan see what events are occurring and where they're triggered in terms of Elec-tron's APIs.

To view them, click the Event Listeners menu item in the left sidebar and thenclick the Load Listeners button in the top right of the window. The Developer toolswindow should then look like figure 17.23.

In the window, you can see the names of the events that are being emitted on eachpart of Electron's APIs, as well as events that are being emitted by Node.js. This allows youto check that the events you expect to be happening in the app are in fact happening.

288

CHAPTER 17 Improving app performance with debugging

Figure 17.23 The Event Listeners pane in the Devtron tab

IPCThe IPC menu item shows what inter-process communication is occurring betweenthe main process and the renderer process of the Electron app. It's useful when youwant to see what data messages are being passed between the processes.

When you want to see what's happening, click the IPC menu item in the left side-bar of the Devtron tab pane and then use the buttons in the top-right pane to handlerecording IPC messages and clearing them, as shown in figure 17.24.

Figure 17.24 The IPC buttons for the IPC pane in the Devtron tab. The idea is that you can record IPC messages that occur when the app is running.

The Record button handles recording IPC messages occurring in the app, includingthe ones used by Electron's internal modules to transmit data between the main pro-cess and the renderer process. To start recording these IPC messages, click the Recordbutton in the top right, and when you use the app, you should start to see IPC mes-sages pouring into the window, as in figure 17.25.

Debugging Electron apps

289

Figure 17.25 IPC messages being recorded in the Lorikeet app. In this case, some internal Electron messages are being sent on three different channels with various data arguments.

The IPC messages can be used to see how Electron triggers internal features, such asdisplaying a dialog on the renderer process with a message to the user when an erroroccurs. To filter out Electron's internal IPC messages, click the Ignore Internal buttonto hide them; and to clear all messages, click Clear. Also, don't forget to click Recordagain to stop recording IPC messages.

LINTINGThe Linting menu item is useful for doing some cleanup tasks on your Electron app.It will do the following:

 Check what version of Electron you're running and inform you if there's a

more up-to-date version available to use

 Check whether you're using an asar archive or not to load your app quicker Check whether you're handling exceptions in your app or ignoring them Check whether your app has crash handling installed to capture when your

app crashes

 Check whether the app window has an event handler for when the app window

becomes unresponsive

Click Linting in the left sidebar, and then click the Lint App button at the top right.The Linting pane will then flag up useful suggestions, as figure 17.26 illustrates.

You can think of the Linting tab as a way of sweeping through issues in the app

before you start preparing it for shipping.

We've covered a number of Devtron features that can be used to debug parts ofElectron, such as its use of IPC messages and the way it uses events. When it comesto building Electron apps, Devtron is a handy tool for debugging and improvingyour app. To find out more about Devtron, check out the project at http://electron.atom.io/devtron/.

290

CHAPTER 17 Improving app performance with debugging

Figure 17.26 The Linting pane in the Devtron tab. The Lorikeet app can make improvements to be that little bit better.

17.5 Summary

In this chapter, we've looked at the tools available to use when you're fixing bugs inyour apps, as well as tools that can help you spot performance problems and see howto address them. Here are some of the key takeaways from the chapter:

 Root cause analysis is the first tool you should use when trying to diagnose thecause of a problem, as you will want to save time by avoiding going down deadends in your analysis.

 The developer tools at your disposal are the same ones available in the GoogleChrome web browser (the Chrome Developer Tools), and will come in handy ifyou work with web apps as well as desktop apps.

 You can use Node.js's remote debugging capabilities to debug a live runningapp on the fly without having to close it down and then painstakingly replicatethe conditions in which a bug has occurred.

 Try to keep the number of assets that your app must load to a minimum. The Sources tab in the Developer Tools window is handy for analyzing an app's

state when you need to fix a bug.

 The Profiles tab is handy for analyzing the performance of your app. Devtron is a great tool for debugging your Electron apps.

In chapter 18, we'll look at how you can package the app for shipping to the widerworld on Mac OS, Windows, and Linux.

Packaging the applicationfor the wider world

This chapter covers Creating Mac binaries of your app  Creating Windows .exe files of your app  Using builders to help automate creating the app Creating Linux executables for your app Creating Mac and Windows setup installers for


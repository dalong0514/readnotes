
Part 1 Welcome to Node.js desktop application development

Two frameworks prevail when it comes to building desktop applications with Node.js: NW.js and Electron. In the first part of the book, you'll be introduced to those frameworks and what advantages they have compared to other app frameworks, build a quick Hello World application with both NW.js and Electron, and then see what kinds of applications have been built.

In chapter 2, we'll begin to put those frameworks to use by building a file explorer app. We'll flesh out the skeleton of the app and add features to it, and explore the different approaches that NW.js and Electron take.

In chapter 3, we'll continue to iterate on the file explorer app by adding more features such as search and opening files. We'll then round up the app in chapter 4 by building executable versions for Mac OS, Windows, and Linux. By the end of part 1, you'll have gotten to know both NW.js and Electron, and put your knowledge to practical use in a real-world application.

# 0101. Introducing Electron and NW.js

This chapter covers: 1) Understanding why Node.js desktop apps are the rage these days. 2) Previewing Node.js desktop application frameworks Electron and NW.js. 3) Using these frameworks to build cross-platform desktop apps with Node.js. 4) Comparing the frameworks. 5) Identifying real-world applications built with Electron and NW.js.

Node.js is known as a programming framework that lets developers build server-side applications in JavaScript. Since its creation in 2009, it has spawned a variety of popular web frameworks like Express and Hapi, as well as real-time web frameworks like Meteor and Sails. It has also allowed developers to create isomorphic web apps using tools like Facebook's React, a UI library that has had a huge impact on web development in recent years. It's fair to have the impression that Node.js is purely about web apps, but the truth is that Node.js is far more than that.

Node.js can be used to build cross-platform desktop apps, and chances are you're using one of them today. If you've ever used Slack at work, edited code using Atom from GitHub, or watched a movie using Popcorn Time, then you've used a Node.js desktop app. It's becoming a popular choice for developers, in particular web developers with little experience in desktop application development — even Microsoft has built and shipped an IDE (Visual Studio Code) using Node.js.

In the Node.js ecosystem, there are two major frameworks for creating desktop apps: NW.js and Electron. Both are supported by major businesses (NW.js by Inteland Gnor Tech, and Electron by GitHub), both have large communities around them, and both share similar approaches to building desktop apps. This book shows how to build cross-platform desktop apps with both Electron and NW.js. You may be pleasantly surprised by how much they have in common — in fact, they have some-thing of a shared history, but we'll get to that later. For now, we'll explore some of the reasons why Node.js desktop apps have taken off and where they might be useful for you and your work.

## 1.1 Why build Node.js desktop applications?

To answer this question, you have to see how software has changed over the past generation and visualize where it is going.

### 1.1.1 Desktop to web and back

At the beginning of 2000, most software was available as desktop apps in shrink-wrapped boxes that you could buy from stores like Best Buy. You'd need to check the system requirements and make sure that it would work on the operating system (OS) you were running (which was Windows, for the majority of people). You'd then grab a CD-ROM out of the box, and install the software on your computer that way.

Over time, that began to change: improvements in web browsers, greater internet speeds and access, and the movement toward open source software resulted in a major shift in how software was created and distributed. The advent of AJAX spawned a new era of delivering software as web apps. These apps didn't require downloading anything onto the computer, and they could run across multiple OSs. Companies like Google and Facebook signaled the rise of the web as a powerful platform in the industry, and as people became accustomed to using apps online for a monthly fee, traditional software houses adapted and began to offer their software online.

It seemed like the web had won, but then mobile computing came along, leading to the rise of native apps for Apple iPhone and Android mobile devices. The industry changed again, and developers found themselves needing to adapt their business to support those devices too.

If reflecting on 16 years of software development shows anything, it's that there's a lot of change in the industry, and that we as developers will probably find ourselves supporting multiple computing platforms for years to come: desktop, web, mobile, and more. We're in the age of multiplatform computing.

Where does that leave desktop apps? Desktop apps have become one of a numberof computing platforms that we use in our day-to-day activities. But what has changedsince the 2000s is that where Microsoft Windows was the dominant OS for desktopcomputers back then, Apple has pared back that dominance with the popularity of itscomputers among creatives and professionals. Not only that, but Google's Chrome-books were the best-selling laptops in the U.S. in the first quarter of 2016. The year ofthe Linux desktop may have finally arrived. The point is this: you can't afford todevelop desktop apps that work on only Windows these days — there's a need for devel-oping apps that work across Mac OS and Linux as well.








Cross-platform desktop apps aren't a new concept; frameworks like Mono and Qthave provided a way to develop desktop apps that run across all three of the majorOSs. Usually, developers with a background in programming languages like C, C++,and C# could come to grips with these frameworks and develop software for them.Other developers, like web developers, would need to learn a new language alongsidea framework, and this would be a barrier to them developing desktop apps.

When NW.js and Electron came about, they offered an opportunity to build desk-top apps with the same code used to create web apps — and not only that, these desktopapps could operate across Windows, Mac OS, and Linux. It was a massive win for bothcode and skills reusability and unleashed a wave of new apps.

In addition, the popularity of Node.js has meant that developers have been able toleverage a huge ecosystem of open source libraries to build their apps with. Node.jsdevelopers and web developers alike could suddenly make desktop apps, and some ofthe apps out there are truly fantastic. One that comes to mind is WebTorrent by FerossAboukhadijeh, shown in figure 1.1.

Figure 1.1 WebTorrent by Feross Aboukhadijeh

WebTorrent is a desktop app that allows you to upload files for other users to down-load, much in the same fashion as BitTorrent. It uses WebRTC to enable peer-to-peerconnections, and to show you how portable the code is, the library used in the desk-top app is the same as the one you can use in a web browser. It's a truly fantastic pieceof work.

The ability to support multiple OSs but write the software in a common and popu-lar language has lots of pros because, as mentioned, desktop computing is still a majorpart of how people use computers today, even as new mobile computing platformsemerge. That's why Node.js desktop apps have become an interesting way to deliversoftware. The next section elaborates on some of the reasons why you may considerbuilding Node.js desktop apps over web apps.

### 1.1.2 What Node.js desktop apps offer over web apps

Web apps have thrived for a number of reasons:

 Internet speeds improved and access increased, and, importantly, the cost ofinternet access went down, making the user base grow massively, unlike mostother communication channels.

 Web browsers have benefitted from increased competition. As appealing alter-natives to Internet Explorer emerged, new features were added to those brows-ers, which in turn enabled web apps to do new things.

 The relative ease of learning HTML, CSS, and JavaScript lowered the barrier ofentry for developers to make web apps, as opposed to learning lower-level lan-guages like C and C++.

 The rise of open source software meant that the cost of distributing and obtain-ing software declined significantly, meaning that developers with a bit of cash,time, and the right level of skill could build their own web apps.

When you look at all this, you can see why the web is such an important platform fordevelopers to make software for. That said, there are still things that challenge andlimit the ability of web apps today:

 Internet access is not always available. If you're on a train and you go under atunnel, chances are you'll lose internet access. If your web app depends on sav-ing data, hopefully it will be able to store a local copy of the changes and allowfor them to be synchronized via the internet when access resumes.

 If your app has a lot of features, the amount of data it will need to transfer overthe internet to run the app could be large and may slow down the loading ofthe app. If it takes too long, people load something else — something proven byresearch into the impact that slow web page loading times have on e-commercetransactions.

 If you're working with large files (such as high-resolution images and videos)that are sitting on your desktop computer, then it might not make sense forthem to be uploaded to the internet in order for a web app to edit them.

The origins of NW.js and Electron

 Because of the security policy of the web browser, there are limits to what hard-

ware/software features of the computer the web app can access.

 You have no control over what web browsers a user may use to visit your web app.You have to use feature detection to cater to different web browsers, which restrictswhat features your app can use. The user experience (UX) can vary wildly.

Web apps are essentially restricted by the limits of internet access and browser fea-tures. It is in these circumstances that a desktop app may be preferable to a web app.Some of the benefits include the following:

 You don't require internet access to start and run the app. Desktop apps start instantly, without having to wait for resources to download

from the internet.

 Desktop apps have access to the computer's OS and hardware resources, includ-

ing access to the files and folder on the user's computer.

 You have greater control over the UX with the software. You don't have to worryabout how different browsers handle CSS rules and what JavaScript featuresthey support.

 Once a desktop app is installed on a user's computer, it's there. It doesn'tdepend on you running web servers to support the app, where you need tooffer 24/7 support in case your web app goes down, or worse, your web-hostingprovider encounters technical difficulties.

Usually, desktop apps have required developers to be proficient in languages like C++,Objective-C, or C#, and knowing frameworks like .NET, Qt, Cocoa, or GTK. For somedevelopers, that can be a barrier to entry and may discourage them from consideringthe possibility of building a desktop app.

The great thing about Node.js desktop application frameworks like Electronand NW.js is that they have significantly lowered that barrier of entry for develop-ers. By allowing developers to create apps using HTML, CSS, and JavaScript, they'veopened the door for web developers to also be desktop app developers, with theadded benefit of being able to use the same code across both the web app and desk-top app platforms.

Now it's time to introduce the frameworks. As mentioned earlier in the chapter,Electron and NW.js have something of a shared history, so I'll touch on the origins ofboth frameworks and then cover each in some detail.

1.2

The origins of NW.js and ElectronBack in 2011, Roger Wang managed to find a way to combine WebKit (the browserengine behind Safari, Konqueror, and Google Chrome at the time) with Node.js, sothat you could access Node.js modules from the JavaScript code running inside a webpage. This Node.js module was given the name node-webkit. He continued to work onthe project at Intel's Open Source Technology Center in China, which gave its support to the project by letting Roger work on it full time. Not only that, he was allowed tohire others to work on it too.

In the summer of 2012, a senior college student named Cheng Zhao joined Intelas an intern to work on node-webkit. He worked with Roger to help improve its inter-nal architecture, which involved changing how Node.js and WebKit were combined.As the code evolved, node-webkit moved from being a mere Node.js module to becom-ing a framework for desktop apps. Node-webkit was given interesting uses within third-party apps. The Light Table editor was the first to make use of node-webkit to deliverits functionality and helped to promote the framework to other developers.

In December of the same year, Cheng left Intel to work at GitHub as a contractor.He was tasked with helping to port GitHub's Atom editor from using ChromiumEmbedded Framework and native JavaScript bindings to using node-webkit.

The efforts to port Atom to node-webkit encountered difficulties (see https://github.com/atom/atom/pull/100), so they abandoned that approach. Instead, theydecided to create a new native shell for Atom, which they called Atom Shell. Thisapproach to combining WebKit with Node.js differed from the approach taken bynode-webkit. Cheng Zhao focused all of his efforts into working on Atom Shell, whichGitHub later open sourced shortly after open sourcing its text editor, Atom.

During this time, Node.js was going through a period of splintering — members ofthe Node.js community created a fork of Node.js called IO.js in order to get updatesinto the project faster, and in the WebKit community, Google announced that it wasgoing to fork the WebKit project for Google Chrome into a variant called Blink. Thecombination of these changes led to renaming node-webkit as NW.js, and GitHubrenamed the Atom Shell framework as Electron. Over time, Electron quickly acquireda number of admirers and was being used in high-profile apps like Slack and VisualStudio Code. It eventually became a juggernaut of its own creation, distinct from itsoriginal purpose as a tool for delivering Atom.

Although NW.js was the first Node.js desktop application framework, Electron hasquickly emerged as a popular framework that has overshadowed NW.js, although bothhave been heavily worked on by the same developer at different points in time andshare a lot of common code in terms of how users use their APIs for creating app fea-tures. Each has evolved a different approach to its internal architecture and hasspawned separate communities that actively promote their respective projects.

In this respect, this book essentially covers two frameworks that do the same thingin slightly different ways. It's a fairly unique situation in that the frameworks share somuch history and are similar enough to merit being evaluated together. There's a nat-ural inclination to pick whichever is the bigger of the two and go with that, and theanswer to that would be Electron (if you go by popularity and momentum), but someprefer NW.js to Electron for its relative simplicity in how you execute code and loadthe app, as well as for supporting computing platforms like Google Chromebooks,and because of other matters of programming opinion. I prefer to provide the infor-mation and let you decide what you want to use. It's more ground to cover, but you'llbe better informed.

If you're interested in digging into the history of both projects a bit more, the fol-

lowing links provide helpful pointers:

 http://cheng.guru/blog/2016/05/13/from-node-webkit-to-electron-1-0.html https://github.com/electron/electron/issues/5172#issuecomment-210697670

If you're looking for posts that compare and contrast the frameworks, here are somegood links to look at as well:

 http://electron.atom.io/docs/development/atom-shell-vs-node-webkit/ http://tangiblejs.com/posts/nw-js-and-electron-compared-2016-edition

That's a brief history of the two projects and how their paths have formed over time.We'll now dive into each framework, starting with the first framework to emerge onthe scene: NW.js.

Introducing NW.jsTo recap, NW.js is a framework for building desktop apps with HTML, CSS, andJavaScript. It was created back in November 2011 by Roger Wang at Intel's OpenSource Technology Center in China. The idea was that by combining Node.js withWebKit (the web browser engine behind Chromium, an open source version ofGoogle Chrome), you could create desktop apps using web technologies. This was thebasis for the framework's original name, node-webkit.

By combining Node.js with Chromium, Roger found a way to create apps thatcould not only load an HTML file with CSS and JavaScript inside an app window, butalso could interact with the OS via a JavaScript API. This JavaScript API could thencontrol visual aspects like window dimensions, toolbar, and menu items as well as pro-vide access to local files on the desktop — things web apps couldn't do.

To give you an idea of what this looks like, let's walk through an example Hello

World app for NW.js.

1.3

1.3.1

A Hello World app in NW.jsThis example application will give you a better understanding of what Node.js desktopapps are like with NW.js. Figure 1.2 show a design of the app we'll build.

Figure 1.2 Design for the Hello World app we'll build

The code for this app is available in the GitHub repository for this book at http://mng.bz/4W7Y.

If you want to get the code to run the app and see it in action, follow the instruc-tions in the README.md file there. It's ready-made to go. But if you want to see howthe sausage is made, then read on and we'll build the app from scratch.

The first step is to check whether you have Node.js installed. If you already do,great — move on to the next section,「Installing NW.js,」but if not, you'll find instruc-tions for installing Node.js in the appendix.INSTALLING NW.JSNode.js comes with a package management tool called npm that handles installinglibraries for Node.js, and NW.js can be installed using it. On your computer, open thecommand-line program for your OS (Command Prompt or PowerShell on Windows,and Terminal on both Mac OS and Linux).

After you've opened your command-line program, run the following command:

npm install –g nw

This will install NW.js on your computer as a Node.js module available to all of yourNode.js desktop apps. CREATING THE HELLO WORLD APPThe app is so small that you can create the files by hand. At the bare minimum, youonly need two files:

 A file named package.json — This contains configuration information about the

app, and is required by NW.js.

 An HTML file — This file will be loaded by the package.json file and displayed inthe app window. In this case, it's a file called index.html (but it can be namedsomething else, such as app.html or main.html).

Start by creating a folder for the app's file. On your computer, go where you like tostore your project source code and create a folder named hello-world-nwjs. Then youcan create the package.json file that will be stored inside the hello-world-nwjs folder.

In your text editor/IDE, create a file named package.json inside the hello-world-

nwjs folder and insert the following code into it:

{ "name" : "hello-world-nwjs", "main" : "index.html", "version" : "1.0.0"}

The package.json file consists of some configuration information about the app: itsname, the main file to load when the app starts, and its version number. These fieldsare required by NW.js (though the version field is required by npm). The name fieldmust contain lowercase alphanumeric characters only — there can be no space charac-ters in the name.

Introducing NW.js

11

The main field contains the file path for the entry point of your app. In the case ofNW.js, you have the option of loading either a JavaScript file or an HTML file, butHTML files tend to be the common choice for NW.js apps. The HTML file is loadedinto the app window, and to demonstrate this, you'll create an HTML file calledindex.html that will be loaded.

Inside the hello-world-nwjs folder, create a file named index.html and insert the

code in the following listing.

Listing 1.1 Code for the Hello World app's index.html file

<html> <head> <title>Hello World</title>   <style>            body {  background-image: linear-gradient(45deg, #EAD790 0%, #EF8C53 100%);  text-align: center;  }

Inline stylesheet included to give background and button element a nice look

Sets title of app window with title element

button {  background: rgba(0,0,0,0.40);  box-shadow: 0px 0px 4px 0px rgba(0,0,0,0.50);  border-radius: 8px;  color: white;  padding: 1em 2em;  border: none;  font-family: 'Roboto', sans-serif;  font-weight: 100;  font-size: 14pt;  position: relative;  top: 40%;  cursor: pointer;  outline: none;  }

button:hover {  background: rgba(0,0,0,0.30);  } </style> <link href='https://fonts.googleapis.com/css?family=Roboto:300' Links to font provided by Google fonts for the button

rel='stylesheet' type='text/css'>

<script>         function sayHello () {  alert('Hello World');  } </script> </head> <body>           <button onclick="sayHello()">Say Hello</button> </body></html>

JavaScript function embedded that prints「Hello World」in alert dialog

Body element contains button element that calls JS function sayHello when clicked

12

CHAPTER 1 Introducing Electron and NW.js

Once you've saved the index.html file on your computer, you can run the app onyour computer. Inside the hello-world-nwjs folder, run the following commandon your terminal:

nw

If you're running on Mac OS, figure 1.3 shows what you should see.

Figure 1.3 The Hello World app running on Mac OS. This screenshot of the app is almost identical to the design, the only difference being size dimensions.

If you're running Linux, figure 1.4 shows the same app running on openSUSE 13.2(Linux has many distributions, and openSUSE is one of the well-known distributions).

Figure 1.4 The Hello World app running on openSUSE 13.2. It looks fairly identical to the Mac OS variant of the app, although the window title bar looks different, the color profiling is slightly different, and the font rendering is noticeably different.

Introducing NW.js

13

The Windows 10, Mac OS, and Linux versions of NW.js all share the same way to getthe app started, which is handy. Type the same command in your Command Prompt,and you should see something like figure 1.5 on a Windows 10 computer.

Figure 1.5 The Hello World app running on Windows 10. The app looks almost identical to the app running on openSUSE Linux (minus the app window and a slight difference in font rendering).

If you click the Say Hello button in the middle of the app screen, you'll see an alertdialog that says「Hello World.」If you were to take the index.html file and load it in aweb browser such as Google Chrome, Microsoft Edge, or Mozilla Firefox, you wouldsee the same screen and get the same result. That's the point — you can take an HTMLpage for a website and turn it into a desktop app with NW.js without having to changethe code.

At this point you might say,「Well, if that's the case, why don't I use a desktop apptemplate that renders an HTML page inside a window and make do with that?」That'snot a bad question, and some apps have taken this approach.

The reasons against such an approach could boil down to ease of development.You might not know C++, or if you do, you may not want to be compelled to compilecode every time you make a feature change. Also, you might want to use features thatare only available natively to the desktop framework and are beyond what an HTMLfile embedded inside of an app window shell would be able to access. The other majorreason is that as desktop app frameworks, both Electron and NW.js provide a rich fea-ture set to support you in developing desktop apps, covered in the next section.

14


### 1.3.2 What features does NW.js have?

NW.js has a set of features that makes it appealing for developers to use when buildingdesktop apps. In a generic overview, they are as follows:

 A JavaScript API for creating and accessing native UIs and APIs to the OS: con-trol windows, add menu items, tray menus, read/write files, access the clip-board, and more

 The ability to use Node.js inside your app as well as install and use a huge

library of Node.js modules via npm

 Being able to build executables of the app for each OS from a single codebase

I'll explain each bullet point in more detail in the next sections.

ACCESSING OS NATIVE UI AND API VIA JAVASCRIPTA good desktop app integrates well into the user's OS: a music app will work with themedia keyboard shortcuts on a user's keyboard, a chat app may have a menu icon inthe tray area of the OS, and a productivity app may provide notifications when actionshave completed.

NW.js provides a large API for getting access to OS features, which do the following:

 Control the size and behavior of the app's window  Display a native toolbar on the app window with menu items Add context menus in the app window area on right-click Add a tray app item in the OS's tray menu Access the OS clipboard, read the contents, and even set the contents Open files, folders, and URLs on the computer using their default apps Insert notifications via the OS's notification system

As you can see from the preceding list, there are a lot of things you can do withinNW.js that web browsers cannot do. For example, web browsers don't have directaccess to files on the desktop or the contents of the clipboard due to security restric-tions that web browsers implement to protect users from sites with malicious intent. Inthe case of NW.js, because the app runs on the user's computer, it's granted a level ofaccess where the user trusts the app. This means that you can do things like access thefiles that are on the user's computer, create new files and folders, and more. Thesefeatures allow the developer to create desktop apps that fit well with the user's OS anddo things that web apps can't do (or at least not as easily) — and the user trusts the appto be responsible and not do anything malicious.

USING NODE.JS AND NPM MODULES INSIDE YOUR APPNW.js provides access to the Node.js API in the app, as well as uses modules that areinstalled with npm. This means that you can install npm modules for use with yourdesktop apps, and you can even access them and Node.js core modules from the samecode that's interacting with the front end of the desktop app.

Introducing NW.js

15

For example, you could write a bit of embedded JavaScript in the index.html filethat uses the Node.js filesystem module to get a list of files and folders in a given direc-tory, and then list those files as list items in the HTML. This shared JavaScript contextbetween the front-end and back-end parts of the desktop app is an intriguing aspect ofthe way NW.js combines Node.js with Chromium. It's something to keep in mindwhen you're working with NW.js applications (as opposed to Electron applications).It's quite different from how web apps work, as figure 1.6 demonstrates.

Traditional web app

NW.js desktop app

Computer

Browser engine

Page

Front-end andback-end code

Computer

Browser

Page

Front-end code

Server

Back-end code

Figure 1.6 The difference between a web app and an NW.js desktop app. The separation between front-end and back-end code in an NW.js desktop is blurred, as the JavaScript context is shared between both parts of the code.

To explore this a bit further, consider how traditional web apps work. Web appstend to have a client/server model where the client requests a web page or makes anAPI request, and the server executes some code to then serve that data back to theclient. The client in this case is a computer running a web browser. The web browserthen loads the data, where, if it's HTML, the rendering engine turns it into a webpage; or, if it's data like XML or JSON, the rendering engine displays it in raw form.The server does its job of executing back-end code to serve HTML pages or APIrequests, and the computer client running the web browser does its job of makingHTML/API requests and rendering the response in the web browser. The webbrowser applies a strict security model to ensure that the front-end code executes

16

CHAPTER 1 Introducing Electron and NW.js

within the context of the web page and nothing else. There's a clear separation ofapplication state and responsibility.

In an NW.js app, the app window is essentially like an embedded web browser,but with the distinct difference that the code inside the web page has access to thecomputer's resources and can execute server-side code. There's no separation ofapp state and responsibility. This means you can write code that's calling out toDOM elements in the web page and executing server-side code accessing the com-puter's filesystem in the same place. Not only that, you'll be able to use npm mod-ules in your code as well.

Being able to install npm modules and require them in your desktop app meansyou have access to over 400,000 libraries (as of January 2017) for use in your code.You'll have plenty of options when it comes to using third-party libraries in your app.In fact, both NW.js and Electron have spawned a number of dedicated libraries for usewith desktop apps, all of which you'll be able to find at http://npmjs.com, and athttps://github.com/nw-cn/awesome-nwjs and https://github.com/sindresorhus/awe-some-electron.

BUILDING YOUR APP FOR MULTIPLE OSS FROM A SINGLE CODEBASEOne of the most useful features of NW.js is that from a single codebase for yourdesktop app, you can build native executable apps for Windows, Mac OS, andLinux. This is a time saver when you're developing an app that has to work acrossmultiple platforms. It also means you can have greater control over how the applooks and feels, more so than you can when trying to support a website for multipleweb browsers.

The native executable is able to run on its own and doesn't require the user tohave any other software installed on their computer. This makes it easy to distributethe app to users, including on stores like Apple's App store and the Steam store,where some NW.js apps and games are sold.

The process of building an app for a specific OS involves a few command-line argu-ments, but there are some tools that simplify the process for you, such as the nw-buildertool, illustrated in figure 1.7.

Taking an example desktop app, I'm able to use nw-builder's nwbuild command instep 1 to automate the steps of turning our desktop app's code into executable bina-ries for both Mac OS and Windows, as shown in step 3. This can save a lot of time (ifyou have to make both 32-bit and 64-bit builds of the app) and prevent mistakes whenbuilding the app.

In the next section, we'll turn our attention to Electron: how an example app

works and looks with it, and what features it has.

Introducing Electron

17

app

Terminal

$> npm install -g nw-builder

build

app.css

$> nwbuild app/

my-nwjs-app

app.js

index.html

package.json

Take the existing app as you have it.

Install nw-builder, and run the nwbuild commandon your app's folder to build the app for multipleoperating systems and bit modes.

A build folder is created with the app built forMac OS X and Windows. You can also buildfor Linux with some extra arguments to thenwbuild command

osx32

my-nwjs-app

osx64

my-nwjs-app

win32

my-nwjs-app.exe

win64

my-nwjs-app.exe

Figure 1.7 The nw-builder tool can build native executables of an NW.js app for both 32-bit and 64-bit versions of Mac OS and Windows.

1.4

Introducing ElectronElectron is a desktop app framework from GitHub. It was built for GitHub's text edi-tor Atom and was originally known as Atom Shell. It allows you to build cross-platformdesktop apps using HTML, CSS, and JavaScript. Since its release back in November2013, it has become popular and is used by a number of startups and large businessesfor their apps. Electron is used not only in Atom but also in the desktop clients of achat app called Slack (www.slack.com), a startup that was valued at `$3.8` billion as of April 2016.

1.4.1 How does Electron work and differ from NW.js?

One of the things that Electron did differently from NW.js was the way it got Chro-mium and Node.js to work together. In NW.js, Chromium is patched so that Node.jsand Chromium are sharing the same JavaScript context (or state, as you may call it inprogramming). In Electron, there's no patching of Chromium involved; instead, it'scombined with Node.js through Chromium's content API and the use of Node.js'snode_bindings.

1.4.2

The implication of this approach is that Electron works differently from NW.js interms of how it handles JavaScript contexts. Where NW.js maintains a single sharedJavaScript context, Electron has separate JavaScript contexts — one for the back-endprocess that kicks off running the app window (referred to as the main process), andone for each app window (referred to as the renderer process). This is an important dif-ference between the frameworks, and one that will be elaborated on further in thebook through various examples.

Another important difference between NW.js and Electron is that where NW.jsusually uses an HTML file as the entry point for loading a desktop app, Electron usesa JavaScript file instead. Electron delegates the responsibility of loading an app win-dow to code that's executed inside the JavaScript file. You'll see this in greater detail aswe explore the Hello World app in Electron in the next section.

A Hello World app in ElectronLike the Hello World app in NW.js, I've also created the app that we'll run throughnow. If you want to boot that up and play with it, you can grab a copy of the source athttp://mng.bz/u4C0.

Follow the instructions in the README.md file to get the app up and running.Alternatively, if you want to bake the cake rather than merely eat it at the end, we'llwalk through that now.

Assuming that you've already installed Node.js on your computer (if not, see「Installing Node.js」in the appendix of this book), let's start by downloading a copy ofElectron via npm. In your terminal or at the Command Prompt, run the followingcommand:

npm install –g electron

This will install Electron as a global npm module, meaning that it will be available toother Node.js applications where you want to use it. Once you have installed the Elec-tron module, we can take a look at what an example Hello World app's files consist of.Here's the bare minimum number of files required to run an Electron app:

 index.html main.js package.json

You can create a folder named hello-world-electron to store the app's files. Create afolder with the suggested name, and then you'll add the required files inside it.

We'll start with the package.json. Here's what an example package.json looks like:

{ "name" : "hello-world", "version" : "1.0.0", "main" : "main.js"}

Createsreference toElectron'sBrowser-Windowclass

Add eventlistenerthat quitsthe appwhen allwindowsare closed(except inMac OS)

Introducing Electron

19

You might notice that package.json looks almost identical to the package.json file usedto load the Hello World app in NW.js. The only difference is that where an NW.js app'spackage.json field expects the main property to specify an HTML file as the app'sentry point, Electron expects the main property to specify a JavaScript file.

In Electron, the JavaScript file is responsible for loading an app's windows, traymenus, and other items, as well as handling any system-level events that occur in theOS. For the Hello World example, it looks like the following.

Listing 1.2 main.js file for the Hello World Electron app

'use strict';

const electron = require('electron'); const app = electron.app;        const BrowserWindow = electron.BrowserWindow;

let mainWindow = null;

app.on('window-all-closed', () => { if (process.platform !== 'darwin') app.quit(); });

Loads Electron module from npm

Creates reference to Electron's application object

mainWindow variable stores reference to app's window

Creates new app window and assigns it to main window variable to prevent it being closed by Node.js garbage collection

app.on('ready', () => {       mainWindow = new BrowserWindow(); mainWindow.loadURL(`file://${__dirname}/index.html`);   mainWindow.on('closed', () => { mainWindow = null; }); });

Loads index.html file in app window

When app window is closed, unassigns appwindow from main window variable

What you can see in listing 1.2 is that where NW.js points to an HTML file in the pack-age.json file, Electron requires a bit of code configuration to achieve the same result.

The JavaScript code looks a bit funnyIf you're fairly new to Node.js and haven't touched JavaScript in a while, you maynotice some new language features like the use of const and let for variable decla-ration, as well as => as a function shorthand. This is the next version of JavaScript,also known as ES6. It's a fairly new version of JavaScript that's now integrated intoNode.js and is actively used in Electron. To learn more about ES6, you can visithttps://babeljs.io/learn-es2015/, http://es6-features.org, and https://es6.io/.

If you prefer the traditional style of writing JavaScript, you can continue to use it foryour Electron applications. The internet is full of opinions, but that doesn't meanthat you have to adopt them. My suggestion is to find what works for you and gofrom there.

20

CHAPTER 1 Introducing Electron and NW.js

Having created the main.js file that's the entry point to your app, you'll now create theindex.html file that the main.js file loads in an app window. Create a file namedindex.html, and insert the code shown next.

Listing 1.3 index.html for the Hello World Electron app

<html> <head> <title>Hello World</title> <style>  body {  background-image: linear-gradient(45deg, #EAD790 0%, #EF8C53 100%);  text-align: center;  }

button {  background: rgba(0,0,0,0.40);  box-shadow: 0px 0px 4px 0px rgba(0,0,0,0.50);  border-radius: 8px;  color: white;  padding: 1em 2em;  border: none;  font-family: 'Roboto', sans-serif;  font-weight: 300;  font-size: 14pt;  position: relative;  top: 40%;  cursor: pointer;  outline: none;  }

button:hover {  background: rgba(0,0,0,0.30);  } </style> <link href='https://fonts.googleapis.com/css?family=Roboto:300'

rel='stylesheet' type='text/css' />

<script>  function sayHello () {  alert('Hello World');  } </script> </head> <body> <button onclick="sayHello()">Say Hello</button> </body></html>

This is the HTML file that will be loaded into the browser window by the main.js file.It's the same code that's used in the NW.js example app's index.html file (so we cancompare the examples across both frameworks). With the files saved in the applica-tion folder, you can now run the app from the command line.

Introducing Electron

21

To execute the app from the command line, cd into the hello-world-electron direc-

tory, and run the following command:

electron .

Once you've run the command, click the Hello World button, and you can expect tosee something like figure 1.8.

Figure 1.8 The Hello World example app running with Electron on Mac OS. It looks almost identical to the NW.js equivalent, except the window dimensions are different.

The app for the most part looks identical to the one running on NW.js, with a fewslight differences. In figure 1.9, you can see how it looks running on OpenSUSELinux 13.2.

The Hello World Electron example app looks a bit different from the version thatruns on a Mac. This is because Mac OS handles displaying menus differently thanWindows and Linux apps do. Where menus are attached to app windows on bothMicrosoft Windows and Linux apps, Mac OS displays a single menu in the OS's tool-bar that applies to all app windows, as shown for the Hello World Electron app's MacOS example in figure 1.10.

22

CHAPTER 1 Introducing Electron and NW.js

Figure 1.9 The Hello World example app running with Electron on OpenSUSE Linux. Notice how the app displays a menu bar with some menu items by default.

Figure 1.10 Application menu on Mac OS. The application menu for the Hello World example app uses the same default menu items.

If you open the app in Windows 10, you can expect to see a result similar to the onedisplayed for the Linux app example, as shown in figure 1.11.

The Hello World app with Electron and Windows 10 again looks quite similar tothe app equivalents on Linux and Mac OS, minus where the application menu is dis-played. The ability to write an app and have it work across three different OSs is a nicefeature to have, though, and it's one of the reasons why developers have been flockingto Electron for their desktop apps.

Besides what's been shown so far, Electron has some other features to offer that

make it a compelling choice, described in the next section.

Introducing Electron

23

Figure 1.11 The Hello World app running on Electron and Windows 10. Like the Linux app example, the Windows example displays a menu in the app window.

1.4.3 What features does Electron have?

Although Electron is relatively young, it has managed to accumulate a number of use-ful APIs and features for building desktop apps:

 Creating multiple application windows with ease, each with its own JavaScript

context

 Integrating with desktop OS features through the shell and screen APIs Tracking the power status of the computer Blocking the OS from going into power-saving mode (useful for presentation

apps)

 Creating tray apps Creating menus and menu items Adding global keyboard shortcuts to the app Updating the app's code automatically through app updates Reporting crashes

24

CHAPTER 1 Introducing Electron and NW.js

 Customizing Dock menu items Operating system notifications Creating setup installers for your app

As you can see, a lot of features are on offer, and that isn't an exhaustive list of all ofthe framework's features. In particular, the crash-reporting feature is unique to Elec-tron — there's currently no equivalent to it in NW.js. Electron has also recently comeup with dedicated tools for app testing and debugging, called Spectron and Devtron,covered in later chapters.

A COOL WAY TO EXPLORE ELECTRON'S FEATURE SET Demonstrating what Elec-tron does and how it does it, the team behind Electron created a desktop appfor demoing Electron's APIs. It's a neat way to browse through Electron'sAPIs in a practical fashion, and can be downloaded from http://electron.atom.io/#get-started.

The next section looks at what apps can be made with NW.js and Electron.

1.5 What apps can you make with NW.js and Election?

Although Electron and NW.js are relatively young in terms of software, their use inprofessional cases is rich and varied. On the NW.js GitHub repository, there's a longlist of example apps that have been built with NW.js, and for Electron there's the Awe-some Electron GitHub repository providing a long list of apps and resources athttps://github.com/sindresorhus/awesome-electron. In this section, I discuss a cou-ple of well-known examples that have been commercially successful, as well as onesthat demonstrate the potential for what Electron and NW.js can do. We'll start withone of the biggest success cases for Electron: Slack.

1.5.1

Slack

Slack (slack.com) is a workplace communication and collaboration tool for busi-nesses. Slack uses Electron to provide the desktop app and is advertising jobs for desk-top app engineers who have experience with using Electron. The desktop userinterface (UI) is practically identical to the web app interface — a shining example ofwhat Electron can achieve. The app has expanded its feature set to allow for audioand video calls. Figure 1.12 shows Slack in use (note, I blanked out some of the mes-sage content and channels for privacy reasons).

Slack recently expanded its offering with support for an app directory for Slack,allowing users to install third-party apps that run inside Slack. The company seems tohave a good future ahead.

What apps can you make with NW.js and Election?

25

Figure 1.12 Slack running on Mac OS

1.5.2

Light TableLight Table (lighttable.com) is a code editor that takes a different approach to theIDE. It was developed by Chris Granger and raised over `$300,000` through a campaignon Kickstarter. It was also the first third-party usage of NW.js and was credited withhelping promote the framework in the early days of the project.

The code editor initially supported Clojure but went on to support JavaScript andPython. The philosophy behind Light Table was to rethink how to approach the taskof editing code. Rather than having to think of code as lines within files, the focusshould be on providing a kind of workspace in which the code is executed live, anddocumentation is displayed in place rather than searched for in another window, asshown in figure 1.13. It was meant to be a kind of workspace for the developer to beable to write code and see the results immediately, rather than in isolation. Originallymade with NW.js, it was recently ported to Electron.

26

CHAPTER 1 Introducing Electron and NW.js

Figure 1.13 Light Table, a live interactive code editor. A 3D visualization written in JavaScript is being edited in the left-hand panel, and the results are being rendered live in the right-hand panel.

1.5.3 Game Dev Tycoon

Game Dev Tycoon is a simulation game in the spirit of old simulations like TransportTycoon and SimCity, but in this case themed around running a game developmentstudio (an irony, given that it was created by a game development company). Behindit is a small company called Greenheart Games, founded in July 2012 by Patrick andDaniel Klug.

The game was unique (and even more ironic) in its attempts to fight off piracy.Patrick anticipated that the game would eventually be pirated and countered this byreleasing a cracked copy of the game onto Torrent sites, but with an interesting twist:people playing the game would find themselves losing in the game. As they played thegame, they would find that suddenly their games would stop making money, becausethey were being pirated. Eventually they would go bankrupt as a result and lose. Thisantipiracy tactic attracted a lot of amusement and attention.

What apps can you make with NW.js and Election?

27

Since its founding, the company has grown to five employees, and the game isbeing sold on the Steam game store. Shown in figure 1.14, it's one of the best show-cases for using NW.js to build a successful commercial project.

Figure 1.14 Game Dev Tycoon, a game studio simulator

1.5.4 Gitter

Gitter is a service that provides chat rooms for open source projects on GitHub,including the official chat room for NW.js. It allows users to sign in with a GitHubaccount and to then access chat rooms based on projects and organizations. It's seenas a popular alternative to Slack.

As a chat service, Gitter is available both via its website (gitter.im), as well as viadesktop apps for Windows and Mac OS, which are built using NW.js. The app's lookand feel is an exact replica of what you see in the web app and well demonstrates theprinciple of code reuse. During the beta period, Gitter attracted almost 25,000 devel-opers to the service, delivering over 1.8 million messages, and is currently hosting over7,000 chat rooms. It now offers paid plans for chat rooms, and the company is workingon getting a version of the app to run on Linux as well.

The main chat room for NW.js can be found on Gitter, a nice example of a product

being used to support itself (figure 1.15).

28

CHAPTER 1 Introducing Electron and NW.js

Figure 1.15 Gitter, a chat room client that's integrated into GitHub

1.5.5 Macaw

Macaw (macaw.co) is an innovative WYSIWYG web design tool. It allows web designersto create a visual design for their websites, as they would normally do in an image edi-tor, and generates the underlying HTML and CSS for that design. It helps eliminatethe step of converting a visual design into a real website by automatically creating thewebsite code. As a WYSIWYG web design tool, Macaw differs from predecessors likeMicrosoft FrontPage and Adobe Dreamweaver by outputting semantic HTML andCSS from the visual design.

Founded by Tom Giannattasio and Adam Christ, the product (figure 1.16) wasfunded through a Kickstarter campaign that raised over $275,000 from more than2,700 backers. Since March 2014, Macaw has gone on to become a product sold directlythrough Macaw's website.

Since I began writing the book, I'm pleased to say that Macaw was acquired byanother web design application company called InVision — yet another example of areal-world desktop app becoming a success story.

What apps can you make with NW.js and Election?

29

Figure 1.16 Macaw, a WYSIWYG web design tool that lets designers create websites using visual design features

1.5.6 Hyper

Hyper (hyper.is) is a minimal-looking terminal app authored by Guillermo Rauch, awell-known figure in the Node.js community for his work on the Node.js websocketlibrary, Socket.io, and for the real-time hosting service Now. As a terminal app writtenin HTML, CSS, and JavaScript, Hyper is an extensible app that can be configured tolook and behave in lots of different ways. Developers have created plugins (such ashyperpower) that animate the text as it's typed into the app and enable users to openURLs from within the terminal window. Figure 1.17 shows Hyper in use.

It's one of the more unique types of desktop apps reimagined with Electron and

shows Electron's minimal style title bar in use.

30

CHAPTER 1 Introducing Electron and NW.js

Figure 1.17 Hyper running on Mac OS

1.6

SummaryThis chapter introduced you to NW.js and Electron and explained how they help webdevelopers build desktop apps. We explored reasons why you might want to preferNode.js desktop apps over building a web app, and how those frameworks help webdevelopers by letting them use the same tools and technologies they're already famil-iar with.

We then looked at the way that a simple Hello World app works and looks with dif-ferent frameworks, across different OSs. This gave you a chance to understand howeasy it is to take a web page and turn it into a desktop app.

We examined the features that make NW.js and Electron great frameworks fordesktop app development, such as their use of the popular Node.js framework andthe npm ecosystem, and the way they provide native executables for the different OSsfrom a single codebase. Finally, we explored a couple of real-life examples of NW.jsand Electron in the wild and saw how apps have been successful in their own domains.This shows you what's possible with Node.js desktop apps, and hopefully providesinspiration for any app ideas that you have.

In the next chapter, we'll get our hands dirty and start building a file explorerdesktop app with both NW.js and Electron. This will help you understand how you goabout building desktop apps with those frameworks as well as how they compare intheir approaches to desktop app development.

Laying the foundationfor your first desktop application

This chapter covers: 1) Building a file explorer in both NW.js and Electron Setting up your application  Structuring your application's files Understanding how the user interface of the application works


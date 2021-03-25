# 2021043Electron-From-Beginner-to-ProR00

## 记忆时间

## 卡片

### 0101. 主题卡 —— Node 的概念

Node.js was initially released in 2009 as an open source project, enabling developers to create server-side applications using JavaScript. What made this project interesting was that it leveraged Google's newly open sourced V8 engine to act as its JavaScript runtime. A top of that runtime, the project added APIs for accessing the local file system, creating servers, as well as the ability to load modules.

Node has enjoyed a tremendous surge of popularity from across the development community. As such, there is a huge collection of modules that are available for use within your Electron application.

1-2『这里的信息让自己对 Node 有了一个初步的了解，Node 原来也是一种后端语言，基于 JS 的后端语言。那么之前听耗子哥说的，「JS 是唯一前后端通吃的语言」，此时才算理解。Node 的概念做一张主题卡片。（2021-03-25）』

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡 —— Chromium

Chromium is the open source version of Google's Chrome web browser. Although it shares much of the same code base and feature set, there are a few differences (albeit minor) and it is released under a different license. What is included with Electron is technically the Chromium Content Module (CCM). Quite the mouthful, hence why most simply refer it is as Chromium. But what is the Chromium Content Module? It is the core code that makes a web browser a web browser. It includes the Blink rendering engine and its own V8 JavaScript engine. The CCM will handle retrieving and rendering HTML, loading and parsing CSS, and executing JavaScript as well.

The CCM only focuses on the core needs to render a web page. Additional features, like supporting Chrome Extensions, or syncing your Chrome bookmarks, are not supported. Just remember that its core purpose is to render web content.

1『 Chromium，目前的理解是阉割版的 Chrome，而且是开源的。做一张术语卡片。（2021-03-25）』

### 0202. 术语卡 ——

### 0203. 术语卡 ——

### 0301. 人名卡 ——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

### 0401. 金句卡 ——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 行动卡 ——

行动卡是能够指导自己的行动的卡。

### 0601. 数据信息卡 ——

### 0701. 任意卡 ——

最后还有一张任意卡，记录个人阅读感想。

## 0101. Welcome to Electron

GitHub Electron (or simply Electron) allows you to build desktop applications using just HTML, CSS, and JavaScript. Sounds like a pretty ambitious statement to make. But it is indeed true, just as Apache Cordova (also known as PhoneGap) enables you to create mobile applications also with just HTML, CSS, JS, and so does Electron for the desktop.

Originally released in July 2013 by Cheng Zhao, an engineer at Github, it was part of their effort to produce a new code editor, Atom. Initially, the project was known as the Atom Shell but was soon rebranded simply as Electron. Although other solutions existed, this project quickly gained traction within the development community. In fact, Adobe AIR, released back in 2008, originally supported building desktop applications with HTML, CSS, and JavaScript, in addition to ActionScript. So the desire to leverage web technologies beyond the browser is certainly not a new one.

In this book, we will take you through the entire Electron ecosystem from its initial setup, through its key features, like creating native menus and windows and more, and how to deploy our app so it can be distributed to our users. Rather bog you down in understanding some abstract sample applications, we are going to be focusing on the core code needing to make Electron work. So, you don't need to know the latest framework to use Electron, but having some basic knowledge with Node.js is useful.

Here is a brief outline of what we are going to be covering: 1) Setting up Electron. 2) Adding native menus. 3) Implementing native dialogs. 4) Exploring creating the application's window. 5) Creating installable and auto-updating applications. 6) Learning how to interact with the user's system

So, if you are ready to start learning about Electron, let's get started.

### 1.1 What Is Electron?

Electron is a blend of two incredibly popular technologies: Node.js (or simply Node) and Chromium. Thus, any web application you have written can run on Electron. Similarly, any Node application you have written can run on Electron. But the power of Electron is that you can use both solutions together.

This book is about how to use these two technologies together to create rich and engaging desktop applications. For example, we have been developing a simple desktop application that will assist developers generate their `manifest.json` file for their Progressive Web Apps. For those unfamiliar with Progressive Web Apps (PWAs), they are web apps that use modern web capabilities to deliver native app-like experiences within the browser. We could have simply written a Node script that developers could run from the command line. But instead we leverage Electron to create a more compelling desktop application. It is one that allows you to auto-generate the app icons simply by dragging the image on the application, and it will save out the collection for you.

Breaking Electron down into its two components (thankfully the physics naming stopped and we aren't referring to these subparts as quarks), they each have specific functions.

The Node component handles things like file system access, compiled module support, and CommonJS Module support. The Chromium component handles things like rendering HTML and CSS, its own JavaScript engine, and the full suite of Web APIs.

Electron is a straightforward runtime. It is not a massive framework/library like Angular or React, but rather a collection of APIs that we can leverage with those or other frameworks. The structure of an Electron application is also open to personal taste. Usually, the UI framework will have more to say about the directory structure than Electron's requirements. However, there are general guidelines that would be wise to follow when developing.

#### 1.1.1 What Is Node?

Node.js was initially released in 2009 as an open source project, enabling developers to create server-side applications using JavaScript. What made this project interesting was that it leveraged Google's newly open sourced V8 engine to act as its JavaScript runtime. A top of that runtime, the project added APIs for accessing the local file system, creating servers, as well as the ability to load modules.

Node has enjoyed a tremendous surge of popularity from across the development community. As such, there is a huge collection of modules that are available for use within your Electron application.

1-2『这里的信息让自己对 Node 有了一个初步的了解，Node 原来也是一种后端语言，基于 JS 的后端语言。那么之前听耗子哥说的，「JS 是唯一前后端通吃的语言」，此时才算理解。Node 的概念做一张主题卡片。（2021-03-25）』

#### 1.1.2 What Is Chromium?

Chromium is the open source version of Google's Chrome web browser. Although it shares much of the same code base and feature set, there are a few differences (albeit minor) and it is released under a different license. What is included with Electron is technically the Chromium Content Module (CCM). Quite the mouthful, hence why most simply refer it is as Chromium. But what is the Chromium Content Module? It is the core code that makes a web browser a web browser. It includes the Blink rendering engine and its own V8 JavaScript engine. The CCM will handle retrieving and rendering HTML, loading and parsing CSS, and executing JavaScript as well.

The CCM only focuses on the core needs to render a web page. Additional features, like supporting Chrome Extensions, or syncing your Chrome bookmarks, are not supported. Just remember that its core purpose is to render web content.

1『 Chromium，目前的理解是阉割版的 Chrome，而且是开源的。做一张术语卡片。（2021-03-25）』

### 1.2 Who Is Using Electron?

So many open source projects come and go. Is Electron worth investing your time and energy into learn? Yes. Although, Electron's original purpose was to act as the shell for GitHub's Atom editor, companies large and small found it to be a good solution for their development needs. Since it was backed by a recognizable company, the risks were a bit lower than trusting your next big thing on an unproven project. If you go to atom.electron.io you can see a massive collection of applications that have been released with Electron as its core.

Obviously Github is actively supporting it, as it is the foundation of their Atom editor. But who else? The very popular team messaging application Slack is built atop Electron, enabling them to develop a common UI across the operating systems. If Atom is not your code editor of choice, then Microsoft's Visual Studio Code might be. This popular editor is also built atop Electron. This is currently our editor of choice at the moment. The team at Microsoft has leveraged common development languages of HTML, CSS, and JavaScript to create a very compelling editor tuned for working with TypeScript and more that works across both macOS and Windows.

1『我去啊，VS Code 竟然是用 electron 写的，Postman 也是。（2021-03-25）』

A variety of familiar web tools have also been able to transform themselves into the desktop-based applications. If you are familiar with Yeoman, a web project generator, there is now a version with a user interface instead of the standard command-line version you are probably familiar with. The team at Basecamp, a popular project management tool, now supports an out of browser experience. If you have worked with Zeplin.io to inspect your visual designs, then the desktop version was developed with Electron. The Postman API inspection tool is another great example of what is possible as an Electron application.

These are just some of the examples of some first-class web applications that have been able to break free from the browser and create desktop-centric versions of their applications. If you would like to explore some other applications that have been built with Electron, visit https://electron.atom.io/apps/.

[Electron 应用 | Electron](https://www.electronjs.org/apps)

### 1.3 What Do I Need to Know?

Unlike traditional desktop development, the only skills you need to have to develop with Electron are a good understanding of HTML, CSS, and JavaScript, and a touch of Node. Being comfortable with your command line wouldn't hurt either. The fact that we can leverage our existing skills and take them from the browser on to the desktop is what is exciting about Electron. We will be using Git to seed our starter Electron apps, but nothing more than that is needed. But working with a version control system is always a recommended skill.

This book is going to take a slightly different approach to covering how Electron works. Since it is simply a runtime, it is framework agnostic. So rather than working through an application built in the framework that you don't know, we are going to just stick with vanilla JavaScript. Now, you should have a modest understanding of HTML and CSS. As for your JavaScript skills, if you have a general understanding of modern JavaScript (aka ES6), you will be fine.

Another area that can be helpful to have is some experience with Node. We will be using the module system throughout this book. But we will provide some foundations on these and any advanced topics that we might need to cover in this book.

### 1.4 Why Should I Choose Electron?

We can assume by the fact you have bought this book, that either there is a need to build a desktop application for yourself, a client or your employer, or you are simply curious about it.

If you have done any web application developing, you no doubt understand the challenges of having to support a wide range of browsers, each with different levels of standards support. Don't get us wrong, the browser's standard support has come a long way in recent years. But, there are still workarounds and polyfills needed to properly deploy a web application to the world. For those working with enterprise clients, you may be further handicapped to legacy browsers and operating systems. When you create an Electron application, you embed a copy of the Chromium engine with the application, so you know exactly what features your application and support have and how your content will render. For example, if you want to use Flexbox as part of your layout solution, you safely can do so (Figure 1-1). If using the Service Worker or Fetch API is something needed for your application, you only need to make sure that the build Electron supports it.

Figure 1-1. The FlexBox support table from caniuse.com

No longer will referencing a feature on caniuse.com be disappointing but rather one of possibilities.As a general rule, Electron updates its Chromium module about two weeks after it is released to the public. The Node component typically takes a bit longer to update. As you begin to embark on larger Electron projects, you will want to also monitor the development process of both of these projects. There might be an issue that you need to be aware or feature added that can greatly make your life easier. But, don't worry – once you can package your application, those runtimes are baked into your application.

#### 1.4.1 Electron's Advantages

Electron applications are just like any other desktop application as they are installed locally on the user's hard drive. They can be launched directly from the Windows taskbar or from the OSX Dock, and there is no need to launch a browser and navigate to some url to run your application. When you need to open or save a file, these dialogs are native in appearance and interaction. Your Electron application can support full drag-and-drop interaction with a local file system, or even associate itself with a file type, so when a user double-clicks the associated file your app will open.

We also have the ability have custom application menus that conform to each platform's user interface guidelines. Contextual menus are available that allow your user to control-click or right-click to display your custom menu. We will show you how to add this functionality in a later chapter.

If you need to trigger a system-wide notification, we can leverage Chromium's Notification API to do so. Electron will go even further that traditional window desktop applications, and create applications that only live in the menubar or system tray.

Electron provides a solid framework that will allow you to develop first-class desktop applications.

#### 1.4.2 Beyond the Sandbox

If you have ever worked with an external API, then you are probably familiar with the restrictions that you have to work. We all have fought with Cross Origin Resource Sharing issues, or establishing proxies in order to allow our web application to work correctly.

Electron operates in a much looser environment with regard to security than your browser. The general assumption is that the user has actively chosen to install and run this application. As such, a degree of trust is then assumed between the user and application.

This allows our Electron application much more freedom, but at the same time we have to use this power with caution.

#### 1.4.3 Offline First Design

With typical web application development, you can usually assume the user is online. Now this is changing with the increase in Progressive Web Apps, but some level of online capability is there for your web app to function. Electron applications have to take the opposite approach. You should not assume that you have an Internet connection. In fact, portions of this chapter were written at 35,000 feet on a plane without WiFi. But I was still able to write in a completely offline mode. Even if your application is dependent on communicating with a back end, you can design your application to function in an offline mode, and sync the data once a connection is reestablished. You will need to take some time to consider how this design pattern will affect the interaction and development of your Electron application.

### 1.5 How Does Electron Work?

Electron-based applications run in two distinct processes: the main process and the render process (Figure 1-2). Each of these two processes has a specific responsibility within your application. While Electron provides a good collection of Node modules for use within your application, many of these modules are only available within a specific process. Knowing these restrictions will help you design the code structure of your application. For example, access to the operating system APIs are restricted to just the main process, and access to the system's clipboard is available to both the main and render process. Knowing this dual-process structure is important, as it will define where some aspects of your application's code need to reside.

1『这里看到了熟悉的「Node modules」，一般是用 `npm inatll` 或者 `yarn install` 来安装的。（2021-03-25）』

| Main Process | Renderer Process |
| --- | --- |
| File system access | HTML & CSS Renderer |
| Compiled Module support | Document Object Model (DOM) Access |
| CommonJS Modules | Web API |

Figure 1-2. The two processes that power an Electron application

#### 1.5.1 The Main Process

Within the main process is where your application will handle various system-level activities, like life-cycle events (starting up, preparing to quit, actually quitting, switching between the foreground and background, as just a few examples). This is also the process where application menus are created, as well as any native dialogs, like file open or file save. Our main process is what is used to bootstrap our application. This is the JavaScript file that is referenced within our package.json file, but more on that in the later chapters.

1-3『这里的信息：1）让我想起来学小程序时的知识，它也是分两条线的，一条主程序的挂起等逻辑，另外一条负责渲染页面。2）还有一个关键信息：This is the JavaScript file that is referenced within our package.json file. 原来主程序的实现是放在配置文件里的。（2021-03-25）』

#### 1.5.2 The Render Process

The main process also has another responsibility, which is to spawn any render processes. It is these processes that would display the UI of your application. Each of these render processes will load your content and execute it within its own thread. We can spawn as many windows as we need for our application. Now unlike a standard web app, each of these processes has access to all the installed Node modules, giving you a lot of capabilities.

The render process is isolated from any interaction with any system-level events. Remember, those interactions must be done within the main process. However, Electron does include an interprocess communication system to allow for events and data to be passed back and forth between the main and any renderer process.

One last thing to note, your Electron app actually does not need to have a render process, but it most likely will. This is a perfect option for taking your Node scripts and making them friendlier to use.

#### 1.5.3 Other Solutions

Electron is not the only solution that will enable you to take your web content and enable it to become a desktop application. The most common alternative to using Electron is known as NW.js (originally known as node-webkit). These two projects share some common legacy, remember Cheng Zhao? Well before creating Electron, he was actively involved with the node-webkit project.

Table 1-1 lists some key differences between the projects.

Table 1-1. Project differences

| - |  Electron | NW.JS |
| --- | --- | --- |
| Chromium Type | Current build of Chromium | A forked version of Chromium |
| Node Process design | Separate Node processes | Shared Node process |
| Auto-Updating | Built-in API | Not included |
| Crash Reporting | Built-in API | Not included |
| Windows Support | Windows 7 or later | Windows XP or later |

Some of the key take aways from this table are the fact that NW.js uses a forked (or copy of the original code) version of Chromium. This may introduce issues such as standards support or delays in improvements or fixes within the Chromium module. Some use functions like Auto-Updating and Crash Reporting must be handled with your own custom solution, rather than leveraging the built-in APIs. The Node process design is also worth noting. Since Electron uses separate processes, it should be more performant than an NW.js application that must share the Node process. One of NW.js' advantages is the fact it supports a much older version of Windows. If your target audience might include that legacy operating system, then NW.js would be your only option between the two.

### 1.6 Summary

This chapter has given you a general overview of Electron. We have touched on its two core technologies: Node and Chromium, as well as introduced its dual-process design. You should have an initial sense of what an Electron-based application is capable of.

In the coming chapters, we will begin exploring these capabilities in much more detail, as well as some we did not even mention yet.

## 0201. Installing Electron

Getting your work environment configured to use Electron is fairly straightforward, but there are a couple of items required to get you started. If you are an experienced developer, you probably already have Node and Git installed. If so, feel free to skip to the Install Electron section of this chapter. If not, let's get started by installing Node.


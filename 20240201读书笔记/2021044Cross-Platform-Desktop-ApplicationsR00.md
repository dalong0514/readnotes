## 记忆时间

书籍的 GitHub 源码：[paulbjensen/cross-platform-desktop-applications: Code examples for the book "Cross Platform Desktop Applications"](https://github.com/paulbjensen/cross-platform-desktop-applications)

## 卡片

### 0101. 主题卡 —— 如何新建一个 Electron 项目

官方文档里快速创建 Electron 项目的操作（2021-04-12）：

```
mkdir my-electron-app && cd my-electron-app
npm init -y
npm i --save-dev electron
```

### 0102. 主题卡 —— 安装第三方包时 save 和 save-dev 的区别

[node.js - What is the difference between --save and --save-dev? - Stack Overflow](https://stackoverflow.com/questions/22891211/what-is-the-difference-between-save-and-save-dev)

--save-dev is used to save the package for development purpose. Example: unit tests, minification.

--save is used to save the package required for the application to run.

he difference between --save and --save-dev may not be immediately noticeable if you have tried them both on your own projects. So here are a few examples...

Let's say you were building an app that used the moment package to parse and display dates. Your app is a scheduler so it really needs this package to run, as in: cannot run without it. In this case you would use:

```
npm install moment --save
```

This would create a new value in your package.json

```json
"dependencies": {
   ...
   "moment": "^2.17.1"
}
```

When you are developing, it really helps to use tools such as test suites and may need jasmine-core and karma. In this case you would use

```
npm install jasmine-core --save-dev
npm install karma --save-dev
```

This would also create a new value in your package.json

```json
"devDependencies": {
    ...
    "jasmine-core": "^2.5.2",
    "karma": "^1.4.1",
}
```

You do not need the test suite to run the app in its normal state, so it is a --save-dev type dependency, nothing more. You can see how if you do not understand what is really happening, it is a bit hard to imagine.

By default, NPM simply installs a package under node_modules. When you're trying to install dependencies for your app/module, you would need to first install them, and then add them to the dependencies section of your package.json.

--save-dev adds the third-party package to the package's development dependencies. It won't be installed when someone runs npm install directly to install your package. It's typically only installed if someone clones your source repository first and then runs npm install in it.

--save adds the third-party package to the package's dependencies. It will be installed together with the package whenever someone runs npm install package.

Dev dependencies are those dependencies that are only needed for developing the package. That can include test runners, compilers, packagers, etc. Both types of dependencies are stored in the package's package.json file. --save adds to dependencies, --save-dev adds to devDependencies.

### 0201. 术语卡 —— Node.js

信息源自「0501Using Node.js within NW.js and Electron」

Node.js is a programming framework created by Ryan Dahl back in 2009. It provides a way to write server-side programs with JavaScript and uses an evented architecture to handle the execution of that code. The programming framework combines V8 (a JavaScript engine) with libuv, a library that provides access to the OS libraries in an asynchronous fashion.

Because of this, JavaScript code is executed by Node.js in such a way that code executing on one line doesn't block the execution of the code on the next line. This is distinctly different from other languages where code on one line executes after the code on the previous line has finished executing. It's important to get familiar with how Node.js handles executing code. You'll tackle this in the next section.

1『这里对 Node.js 的解释做一张术语卡片。（2021-04-16）』—— 已完成

5.1 什么是 Node.js

Node.js 是一个由 Ryan Dahl 在 2009 年创建的编程框架。它提供了一种使用 JavaScript 来编写服务端程序的方法，并且使用基于事件的架构来处理代码的执行。该编程框架整合了 V8（一种 JavaScript 引擎）和 libuv（一种编程库），提供了异步的方式来调用操作系统资源。

正因如此，通过 Node.js 执行的 JavaScript 代码之间可以做到不阻塞对方。这是和其他语言相比最大的不同点，在其他语言中，一行代码执行完毕后才能执行下一行代码。了解 Node.js 如何处理代码执行这一点非常重要。下一节会做更多介绍。

信息源自「0601Exploring NW.js and Electron's internals」

From a developer's view, NW.js is a combination of a programming framework (Node.js) with Chromium's browser engine through their common use of V8. V8 is a JavaScript engine created by Google for its web browser, Google Chrome. It's written in C++ and was designed with the goal of speeding up the execution of JavaScript in the web browser.

When Node.js was released in 2009, a year after Google Chrome, it combined a multiplatform support library called libuv with the V8 engine and provided a way to write asynchronous server-side programs in JavaScript. Because both Node.js and Chromium use V8 to execute their JavaScript, it provided a way to combine the two pieces of software, which Roger Wang came to understand and figure out. Figure 6.1 shows how those components are combined.

1-2『这里，node.js 是将 V8 引擎和 libuv 结合起来的一个 JS 后端语言，补充进 node.js 的术语卡片。（2021-04-18）』—— 已完成

### 0301. 任意卡 —— 锁死 node.js 第三方包版本号的两种方法

信息源自「0501Using Node.js within NW.js and Electron」

Notice the ^ preceding the version 1.10.1 of CoffeeScript. You've installed version 1.10.1 of CoffeeScript, but let's say a couple months later someone downloads a copy of the app's code from GitHub and runs npm install to download the dependencies. If CoffeeScript 1.11.0 comes out, or even 1.10.2, those will be downloaded instead of 1.10.1. The caret character indicates that you can install a more up-to-date version of the dependency, so long as the changes are only at patch level (the number of the version after the second dot, indicating a bug fix or change that doesn't affect existing functionality) or minor level (the number after the first dot in the version number, indicating a small change to the module which shouldn't cause breaking changes to your app). If CoffeeScript 2.0.0 is out, it won't install that version because that's a major-level change (indicating new features/changed API and therefore likely to cause breaking changes to your app).

The idea behind this approach is to allow developers to pull in fixes and nonbreaking updates to their dependencies without having to manually update those numbers in the package.json file. This can work as long as the developers of Node.js modules follow the principles of semantic versioning, as well as take care not to introduce bugs during those updates. From a DevOps perspective, this can provide room for production errors to creep in (hence, the need for a comprehensive testing strategy, which I'll cover later in the book). You want control over the version of the dependencies.

How do you lock down the versions of the dependencies? There are two ways you can do this. The first is to remove any ^ or ~ characters from the front of the version numbers of the dependencies listed in the package.json file. If you don't want to do that manually, the alternative approach is to use npm shrinkwrap.

1-2『锁死 node.js 第三方包版本号的两种方法。做一张任意卡片。（2021-04-17）』—— 已完成

npm's shrinkwrap command will lock down the version of dependencies that are installed with the module. Running npm shrinkwrap in the same working directory as the package.json file will produce a file called npm-shrinkwrap.json, a JSON file that has configuration information to specify exactly what version of the module should be installed, which looks like this:

```json
{
    "name": "pkgjson", 
    "version": "1.0.0", 
    "dependencies": { "underscore": { "version": "1.8.3", "from": "underscore@", "resolved": "https://registry.npmjs.org/underscore/-/underscore-1.8.3.tgz" } }
}
```

This file helps npm know exactly what versions of the software should be installed for the module.

Based on my experience working with Node.js since 2010, my suggestion is to use the approach of keeping dependencies in the package.json file up to date, keep the node_modules folder out of version control, and, when needed, use npm shrinkwrap to lock down the dependencies in use.

注意，`^` 在 CoffeeScript 1.10.1 版本号的前面。你已经安装了 1.10.1 版本的 CoffeeScript，不过，假设几个月后，有人从 GitHub 上下载了一份应用代码，并运行 npm install 来安装依赖。如果 CoffeeScript 1.11.0 或者 1.10.2 已经发布了，那么安装的时候就会安装新发布的版本。脱字符号表示你可以安装更新版本的依赖模块，只要该新版本是在补丁级别的（版本号中第二个点后面的那个数字，代表了用于修复漏洞或者不影响功能的改动）或者是小版本级别的（版本号中第一个点后面的那个数字，表示改动不会要求你的应用更新后需要修改代码才能工作）。如果 CoffeeScript 2.0.0 发布了的话，它不会被安装，因为它属于主版本号的改动（意味着有新的功能 / 修改过的 API，会导致和你的应用不兼容，需要你的应用也跟着进行修改）。

之所以使用这种方式是为了让开发者可以直接获得依赖模块的补丁和兼容的更新，而不需要手动在 package.json 中更新版本号来获取更新。只要模块的开发者遵循语义化版本号的原则，并且在更新过程中不引入漏洞，这套方式就可以很好地工作。从 DevOps 的角度来看，这为生产环境中的漏洞滋生提供了温室（因此，我们需要综合的测试策略，本书后续部分会做介绍）。你想要控制依赖模块的版本号。

如何锁定依赖模块的版本号呢？这里有两种方法。第一种方法是将 package.json 文件中列出的依赖模块版本号前的 `^` 和 `~` 符号都去掉。如果你不想手动做的话，还有一个办法就是可以使用 `npm shrinkwrap` 命令。

npm 的 shrinkwrap 命令会将安装的模块版本号锁定。在 package.json 文件同级目录下运行 npm shrinkwrap 命令时会产生一个名为 npm-shrinkwrap.json 文件，这个 JSON 文件包含了一些配置信息，指明了安装模块的具体版本号，如下所示：

上述文件有助于让 npm 知道具体要安装哪个版本的模块。根据我从 2010 年就开始使用 Node.js 到现在的经验，我的建议是，保持 package.json 文件中的模块版本号最新、将 node_modules 文件夹从版本控制中移除以及如有必要，使用 npm shrinkwrap 将依赖的模块版本号锁定。

## 内容简介

1『整本书读下来，翻译的真不错，读起来很舒服。（2021-04-14）』

本书是一本同时介绍 Electron 和 NW.js 的图书，这两者是目前流行的支持使用 HTML、CSS 和 JavaScript 进行桌面应用开发的框架。书中包含大量的编码示例，而且每个示例都是五脏俱全的实用应用，作者对示例中的关键代码都做了非常详细的解释和说明，可让读者通过实际的编码体会使用这两款框架开发桌面应用的切实感受。除此之外，在内容上，本书非常系统，分为 4 大部分：

第 1 部分介绍两个框架的历史背景，并教大家编写第一个桌面应用，让读者对这两个框架有一个初步的感受；第 2 部分深入讲解 NW.js 和 Electron 的内部工作原理，帮助大家剖析这两个框架的底层机制，让读者对它们有更深入的理解；第 3 部分介绍使用框架提供的大量 API 来构建多款实用的桌面应用，全方位地让读者体会使用这两个框架开发桌面应用带来的舒适体验；第 4 部分为大家讲解了，当开发完成后，如何对应用进行测试、跨平台打包和发布。可以说这 4 部分结合起来将开发桌面应用的整个流程系统化地讲解得非常清楚、到位。相信结合书中大量的示例，读者一定能很快掌握并自己使用 Electron 和 NW.js 构建出跨平台的桌面应用。

## 译者序

Stack Overflow 的联合创始人 Jeff Atwood 说过一句非常经典的话：Any application that can be written in JavaScript, will eventually be written in JavaScript，翻译过来就是：任何能使用 JavaScript 来编写的应用，最终都会用 JavaScript 来实现。这句话被誉为 Atwood 定律。事实上，这句话正在不同领域被一次一次地验证。以前 JavaScript 只是运行在浏览器沙箱环境中的脚本语言，而自从 2009 年 Node.js 问世后，JavaScript 在服务器端、物联网领域、移动原生应用开发领域，乃至桌面应用开发领域都大放异彩。

以往要开发桌面应用，针对 Windows、Linux 以及 Mac OS 三大平台要专门去学习各自平台的编程语言和框架，成本高昂而且要做一款支持兼容三种平台的桌面应用非常费时，基本都需要针对不同平台的不同团队才能实现。就我个人而言，几年前我一直想学习 Objective-C 以及 Cocoa 来开发 Mac OS X 桌面应用，但是始终没有成功。现如今，JavaScript 让这一切都变得无比简单。一名 Web 开发者就能开发出兼容三大操作系统的桌面应用。不仅大大降低了学习曲线，而且开发效率可以说呈指数级提升。这要归功于 NW.js 和 Electron 这两款目前最流行的使用 Web 技术开发桌面应用的开发框架。这两款框架将 Chromium 和 Node.js 非常好地结合起来，Chromium 使得 Web 开发技术能够在桌面应用中得以施展，Node.js 则提供了访问操作系统 API 的能力，两者的结合使得使用 JavaScript 开发桌面应用成为可能。

目前，NW.js 和 Electron 这两款框架在全世界各大公司被广泛使用。近几年红遍全球的 Slack 就是使用 Electron 来开发他们的桌面应用的，国内阿里巴巴的企业应用 —— 钉钉桌面应用，就是用 NW.js 来开发的，除此之外，全球范围内越来越多的桌面应用都在采用这两种框架进行开发。

本书是一本专门介绍如何使用 NW.js 和 Electron 框架来开发桌面应用的书。在国内，目前本书应该是第一本同时介绍 NW.js 和 Electron 开发桌面应用的图书。而且本书内容非常系统，从框架的背景介绍、教你开发第一款桌面应用、深入剖析框架内部原理、通过丰富的示例应用介绍框架提供的多个 API，再到应用的测试、调试、跨平台打包、构建和最终的发布，涵盖整个开发到发布流程中的所有环节。而且本书的每一章中都有大量的实用示例，通过实际的编码让你感受使用 NW.js 的 Electron 开发桌面应用的体验。书中每个示例应用都会分别介绍 NW.js 和 Electron 两个版本如何实现、过程中需要注意的地方有哪些，非常有实践价值。总的来说，本书不论是对于初学者还是有一定经验的开发者，都是一本相当好的学习使用 NW.js 和 Electron 开发桌面应用的图书。

最后，非常感谢电子工业出版社计算机出版分社的张春雨编辑对我的信任，将这本书交给我来翻译；感谢本书的责任编辑刘舫对本书的辛苦付出；还要感谢本书的原作者 Paul B. Jensen，翻译过程中遇到模棱两可的地方，通过 Twitter 联系他，他都能及时回复我，并给予详细的解释。

翻译和写书一样，都是需要花费大量精力和时间的事情，自从翻译完上一本《了不起的 Node.js》后，我就对自己说我再也不会干翻译图书的事情了，实在是太累了。但是，当出版社编辑找到我，给我看了原版样书后，我还是没忍住，因为虽然过程很累很苦，但是在书出版的那一刻，除了自己小小的虚荣心能够得到一点满足，更多的是一想到可以帮助到很多学习使用 NW.js 和 Electron 开发桌面应用的开发者，就觉得非常自豪，再累再苦都是值得的！当然，翻译过程中难免会有错误的地方，也希望大家能够多多指正！

谨以此书献给在背后默默支持我的家人，特别是我的两个孩子 —— 木木和一一，希望你们能够健康快乐地成长，爸爸爱你们！

Goddy Zhao

2017 年 12 月 12 日于上海

## Foreword

The Electron framework was born in 2013, when Node.js was just becoming popular. The community was excited about JavaScript running on both the client and serversides, and there were various attempts to write desktop apps using JavaScript.

I was excited about JavaScript, too, and GUI programming was my favorite area. I wrote a few modules for Node.js to provide bindings for popular GUI toolkits withJavaScript, but they were no better than existing tools and didn't attract much attention. Then I found an interesting Node.js module called node-webkit: a simple module that could insert Node.js into WebKit browsers. I had the idea of using it to develop a full-featured desktop framework: I could use Chromium to display web pages as windows, and then use Node.js to control everything!

Development for node-webkit was inactive at that time, so I took over and rewrote the module to make it a complete framework for desktop apps. When I had finished my initial development, it worked incredibly well for small, cross-platform apps.

In the meantime, GitHub was secretly developing the web technology–based Atom editor and was eager to replace Atom's subpar web runtime with a better tool. GitHub tried to migrate Atom to node-webkit but encountered many problems; I met with the developers, and we agreed that I would write a new framework for writing desktop apps with browser techniques and Node.js, and help them migrate Atom to it.

The new framework was initially called atom-shell; it was renamed Electron a yearlater when it became open source. Electron was written from scratch with a completely different foundation than node-webkit, to allow developers to create large, complex apps. (Today, node-webkit is being actively developed and maintained by others. The module is now known as NW.js, and it's used widely.)

Because Electron made it easy to quickly write sophisticated cross-platform desktop apps, it attracted attention from many developers and underwent rapid improvements. Now big brands are releasing products based on Electron, in addition to small startups building their business around the platform.

Writing desktop apps with Electron and NW.js requires developers to understand anumber of new concepts. Desktop development is different from front-end programming in ways that can make it difficult for beginners. That's where this book can help. Cross-Platform Desktop Applications will walk you through the rich APIs of Electron and NW.js and help you get started developing desktop apps. You'll learn the details of desktop development with JavaScript, from building and shipping apps to in-depth tricks for integrating apps with the desktop. The book also covers advanced topics like debugging, profiling, and publishing apps on various platforms — even experienced developers can learn a lot from these pages.

I recommend this book to anyone who wants to work in desktop development.You'll be surprised how easy it is to write a cross-platform desktop app using JavaScriptand the web techniques outlined here.

CHENG ZHAO

CREATOR OF THE ELECTRON FRAMEWORK

Electron 框架诞生于 2013 年，那个时候 Node.js 才刚刚流行起来。整个社区因 JavaScript 能够在客户端和服务器端运行而兴奋不已，并且也在尝试使用 JavaScript 来开发桌面应用。我个人也对 JavaScript 技术很热衷，而且 GUI 编程是我比较喜欢的领域。我自己写过一些 Node.js 的模块，这些模块对主流的 GUI 工具提供了 JavaScript 的绑定，不过都做得一般，也没有引起太多关注。

之后我发现了一个非常有趣的 Node.js 模块，叫作 node-webkit：这个简单的模块可以实现在 WebKit 浏览器中插入执行 Node.js 代码。于是我有了一个点子，可以用它来开发一个具备完整功能的客户端开发框架：我可以用 Chromium 来显示 Web 页面，就像桌面窗口一样，然后其他的都用 Node.js 来控制！

当时 node-webkit 的开发并不活跃，于是我接手了这个项目并进行重写，将它打造成一个完善的用于桌面应用开发的框架。当我完成第一版的时候，它可以用于开发小型的跨平台应用，效果奇好！

与此同时，GitHub 正在秘密开发一款基于 Web 技术的 Atom 编辑器，而且他们非常希望可以有一个更好的工具来替代目前 Atom 不尽如人意的 Web 运行时。GitHub 曾尝试将 Atom 迁移到 node-webkit，但是遇到了很多问题。我和他们的开发者碰了面并且最终我们达成一致：由我来开发一款新的框架，让开发者使用 Node.js 技术和浏览器相关技术就可以开发桌面程序，然后再帮他们把 Atom 迁移过来。

这款新的框架起初命名为 atom-shell；一年后，在正式开源的时候将其改名为 Electron。Electron 是从零开始开发的，并且使用了和 node-webkit 完全不同的底层架构，它可以让开发者开发大型且复杂的桌面端应用。（如今，node-webkit 交由其他开发者在维护开发，项目状态也比较活跃。它现在叫 NW.js，使用也很广泛 。）

因为使用 Electron 可以既简单又快速地构建出复杂的跨平台应用，所以它得到了许多开发者的关注，发展也很迅速。现如今，许多大公司都基于 Electron 开发了他们的桌面端产品，除此之外，小型创业公司也围绕这个平台在构建他们的业务。

使用 Electron 和 NW.js 开发桌面应用要求开发者掌握一些新的概念。桌面应用开发和前端程序开发截然不同，对于初学者来说也更难。不过本书可以帮助到大家。

本书将带你一览 Electron 和 NW.js 丰富的 API、教你如何开发桌面应用。你会学到许多使用 JavaScript 开发桌面应用的技术细节，包括如何构建和分发应用，以及如何将现有应用集成到桌面应用中的一些深度小技巧。本书还涵盖了一些高级话题，如调试、分析以及在不同平台发布应用，哪怕是有经验的开发者也可以从中学到不少东西。

我建议所有想要开发桌面应用的读者都来阅读本书。读完后你会惊讶于使用 JavaScript 和 Web 技术来进行跨平台的桌面应用开发是一件多么简单的事情。

Cheng Zhao

Electron 框架开发者

## Preface

A few years ago, I was at a company called Axisto Media, and for a health conferencewe needed to produce a desktop app that contained videos, session information, and posters from the conference. We developed the app with Adobe AIR. But building the app wasn't simple, and customers had to go through a few steps to get the app running on their computer. There had to be a better way — and, thankfully, there was.

I came to learn about NW.js (back then known as Node WebKit) around the end of 2013. I realized that NW.js could make it easier for customers to use the desktop app because they wouldn't have to install Adobe Flash Player or fiddle with locating files on the USB to load the app. They could simply double-click the app. Not only that, we could also offer support for Linux, and harmonize our tech stack within the business, as we were using Node.js in quite a few places.

I took the opportunity to re-create the desktop app with NW.js, and never looked back. It made things so much simpler, and with the ability to reuse HTML, CSS, and JS from the web app for the conference website, we could make the look and feel of the app more consistent. It was a massive win.

I was so pleased with the framework that I decided to give a presentation about it at the London Node.js User Group meetup in June 2014. I then put the slides online. A couple of months later, I noticed that the slides on SlideShare had quickly accumulated some 20,000 views. It was nice, and I thought that would be that.

But it wasn't.

In December of 2014 I received an email from Erin Twohey at Manning Publica-tions asking me if I'd be interested in writing a book about Node WebKit. It felt too good to pass up. I jumped at the chance and embarked on writing this book.

Lots of things happened during that time. The Node.js community created a fork of the project called IO.js to get features into the platform more quickly, and subse-quently merged the fork back into Node.js. The Node WebKit framework switched tousing IO.js, and as it was using Blink rather than WebKit, was renamed to NW.js. A year passed, and the book was nearing completion, when we noticed that there was another Node.js desktop app framework in the space called Electron. Taking a closer look, we realized that it was quite similar to NW.js, and it turned out that the author of Electron had previously worked on NW.js. We therefore decided to include the frame-work in the book.

Writing a book covering two Node.js desktop app frameworks was a challenge, but here it is. The book covers the fundamentals of building desktop apps across both NW.js and Electron. It doesn't cover everything there is to know about the frameworks, but enough to acquaint you with a wide range of features and uses, so that you can pick a framework that suits your needs and build desktop apps with it.

This is a great time to be a developer, and with tools like NW.js and Electron, it's never been easier to make a desktop app. I hope you enjoy this book, and if you find you want to ask me about the frameworks, you can contact me at paulbjensen@gmail.com.You can also find me at @paulbjensen on Twitter.

PAUL JENSEN

几年前我在一家叫 Axisto Media 的公司工作时，我们需要为一个健康行业大会开发一款桌面应用，用来展示大会的视频、议题信息以及海报。当时这款应用是用 Adobe AIR 开发的。但是开发过程并不容易，而且客户需要进行一些操作才能让应用在他们的计算机中运行起来。好在我们后来找到了更好的解决方案。

我大概从 2013 年年底开始学习 NW.js（那个时候它叫 node-webkit）。我发现使用 NW.js 开发的桌面应用客户用起来更方便，因为他们不再需要安装 Adobe Flash 播放器，也不用把应用文件放到 U 盘里来加载。他们只需双击应用就可以运行了。不仅如此，我们还能提供 Linux 版本，而且其技术栈和我们的业务本身的技术栈很契合，因为我们在其他地方也都使用 Node.js 技术。

我抓住了机会，使用 NW.js 去重新构建这款桌面应用并且摒弃一切，勇往直前。NW.js 让一切都变得更加简单，这得益于它可以从大会网站的 Web 应用重用 HTML、CSS 和 JS 代码，我们可以让桌面应用看上去样式更加统一。这是一个巨大的好处。

我当时对这个框架非常满意，于是决定在 2014 年 6 月的伦敦 Node.js 用户组聚会上进行分享。后来我就把演示稿放到了网上。几个月后，我发现这个演示稿在 SlideShare 网站上很快被查看了 20 000 次。这太棒了，我以为这事就这样了。然而并没有。

2014 年 12 月，我收到了一封来自 Manning 出版社 Erin Twohey 的电子邮件，他问我是否有兴趣写一本关于 node-webkit 的书。这简直太棒了，我立刻就投入到这本书的写作中。

那段时间发生了很多事情。Node.js 社区 fork 了 Node.js 项目并命名为 IO.js，他们加快了平台新特性的开发，后来 IO.js 项目又合并回了 Node.js 项目。node-webkit 框架切换到了 IO.js，并且由于它使用了 Blink 而非 WebKit，因此改名为 NW.js。一年过去了，本书的写作也临近尾声，就在这个时候，我们发现了另外一个可以用 Node.js 开发桌面应用的框架，叫 Electron。仔细一看，我发现 Electron 和 NW.js 很像，而且它的作者以前就是开发 NW.js 的。于是我们决定将 Electron 也写到本书中。

写一本书同时涵盖两种 Node.js 桌面应用开发框架是一个挑战，不过最终还是完成了。本书涵盖了使用 NW.js 和 Electron 开发桌面应用的基础知识。尽管本书没有面面俱到地介绍这两个框架，但是足够让你了解它们的大部分特性以及如何使用的知识，这样你就可以根据你的需求，选择其中一个框架来构建桌面应用。

对于开发者来说这是一个很好的时代，有了像 NW.js 和 Electron 这样的工具，构建桌面应用变得再简单不过。我希望你喜欢这本书，如果对于这两个框架有问题想问我的话，可以通过我的电子邮箱 paulbjensen@gmail.com 或者通过我的 Twitter 账号 @paulbjensen 联系我。

## About this book

NW.js and Electron are desktop application frameworks powered by Node.js. They allow developers to create cross-platform desktop apps using HTML, CSS, and Java-Script. They offer web designers and developers a way to take their existing skills for crafting web apps and interfaces, and apply that to building desktop apps. The frameworks also support shipping apps for Mac OS, Windows, and Linux from the same codebase, meaning that developers can save time and energy when creating desktop apps that all OSs can use.

NW.js and Electron come from a shared history, and have some similar approaches to app features. This book covers both frameworks topic by topic, helping you to see what they have in common, and where they differ in their approaches. This will help you to decide which framework is best for your needs. We'll cover a broad range of apps and features together, to spark your passion and interest, as well as provide ideasfor things you might want to build but don't know how.

I hope you enjoy the book, and that you get to make something great with it.

NW.js 和 Electron 是基于 Node.js 开发的桌面应用框架。它们可以让开发者使用 HTML、CSS 和 JavaScript 来构建跨平台的桌面应用。它们为 Web 设计师和开发者新开辟了一条路，可以让他们将已有的开发 Web 应用和界面的技能同样用于桌面应用的开发。这两个框架还支持将同一份应用代码分发到 Mac OS、Windows 和 Linux，这意味着开发者在构建全平台可用的应用时可以大大节约时间和精力。

NW.js 和 Electron 有一段共同的历史，并且对部分特性的支持有类似的实现方式。本书在介绍每一个主题的时候都会同时介绍这两个框架，帮助你了解两者的共性和区别。这将有助于你判断哪个框架更适合自己的需求。本书会介绍各类应用以及特性，从而激发你的学习热情和兴趣，还会对一些你可能想要开发但又不知如何开发的应用提供建议和想法。

希望你喜欢这本书，也希望你可以用本书中介绍的知识做一些很棒的事情。

### Who should read this book 

Anyone who has experience with HTML, CSS, and JavaScript can pick up this bookand get to grips with it right away. Experience with Node.js is not a requirement, but experience will come in handy. If you're completely new to HTML, CSS, and JavaScript, then it would be best to get acquainted with those technologies before youbegin to read this book.

任何有过 HTML、CSS 和 JavaScript 开发经验的人都可以阅读本书并快速上手。Node.js 的开发经验不是必需的，但是有的话读起来会更加得心应手。如果你对于 HTML、CSS 和 JavaScript 完全陌生，那么在开始阅读本书之前最好先去熟悉一下。

### How this book is organized

This book has 18 chapters, organized into 4 parts.

Part 1 is an introduction to the frameworks:

Chapter 1 introduces NW.js and Electron, describing what they are, how they came about, what a Hello World app looks like in both frameworks, and some of the real-world apps that have been produced with them.

Chapter 2 then explores a direct comparison of the frameworks by building a file explorer application in each one.

Chapter 3 continues to flesh out some features of the file explorer application. 

Chapter 4 rounds off part 1 by building executable versions of the app for different OSs.

By the end of the first part, you'll have seen how to build a full-feature app with both frameworks.

Part 2 (chapters 5-6) looks at understanding the internals of NW.js and Electron from a technical perspective:

Chapter 5 looks at Node.js, the programming framework behind both NW.jsand Electron. It covers how Node.js works, how asynchronous programming is different from synchronous programming, and the use of callbacks, streams, events, and modules.

Chapter 6 looks at how NW.js and Electron operate under the hood in terms of how they combine Chromium with NW.js, and how they handle state betweenthe back end and front end.

This will help demystify the magic that NW.js and Electron perform to make their frame-works operate, and provide a useful guide to Node.js for those new to the framework.

In part 3 of the book, we'll look at how to start fleshing out specific features of desktop apps with NW.js and Electron:

Chapter 7 looks at controlling how the app can be displayed, in terms of the window dimensions and different screen modes, and how to toggle between them.

Chapter 8 explores how to create tray applications that sit in the tray area of desktops.

Chapter 9 shows how to build app and context menus for integrating into your apps.

Chapter 10 introduces dragging and dropping files into your app, and being able to craft the UI to have the same look and feel as other OSs.

Chapter 11 uses your computer's webcam to build a selfie app and to save the photos to your computer.

Chapter 12 looks at ways in which you can store app data for your apps, as well as how to retrieve it.

Chapter 13 shows how to use the clipboard APIs of both NW.js and Electron to copy and paste contents to and from the OS's clipboard.

Chapter 14 uses a 2D game to demonstrate how to add keyboard shortcuts toyour apps, as well as how to program global shortcuts that are accessible acrossthe entire OS.

Chapter 15 rounds off the part by exploring how to implement desktop notifications for a Twitter streaming client.

This part demonstrates a broad range of features that both NW.js and Electron support, helping you to see how the frameworks go about providing those features, and giving you a chance to evaluate which framework suits your needs best.

In the final part of the book, we'll look at things you can do to prepare your app for production: writing tests, debugging code, and finally, producing executable binaries for shipping to your customers:

Chapter 16 looks at ways you can approach testing your desktop apps, and at different levels. It introduces the concepts of unit, functional, and integration testing, using Cucumber to document how your app features work, and using Spectron to automate testing your Electron apps at an integration level.

Chapter 17 explores ways you can debug your code to help spot performance bottlenecks and bugs, and covers tools like Devtron to help inspect your app ingreater detail.

Chapter 18 finishes off the part by looking at various options for building executable binaries of your app, as well as creating setup installers for the different OSs.

By the end of this part, you should be in a position to test your apps, debug any issues that may occur with them, and finally get them built and shipped to your customers.

本书共 18 个章节，分为 4 个部分。

第 1 部分主要介绍框架。

第 1 章介绍 NW.js 和 Electron 的入门知识，介绍它们是什么，缘何而来，介绍用这两个框架开发出来的 Hello World 应用是怎样的，还会介绍一些用它们开发出来的实用的应用。

第 2 章通过构建一个文件浏览器应用来直接对比这两个框架的异同。

第 3 章继续完成文件浏览器应用的部分功能。

第 4 章通过构建可以在不同操作系统中运行的应用来结束第 1 部分的内容。

读完第 1 部分后，你将学会如何使用这两个框架开发一个功能完整的应用。第 2 部分（第 5 章和第 6 章）从技术角度介绍了 NW.js 和 Electron 的内部原理。

第 5 章介绍 Node.js，它是 NW.js 和 Electron 底层使用的编程框架。本章介绍了 Node.js 是如何工作的，异步编程和同步编程的区别以及如何使用回调、流、事件和模块。

第 6 章介绍了 NW.js 和 Electron 是如何将 Chromium 和 Node.js 整合起来的，以及它们是如何处理前后端的状态管理的。

这部分内容揭示了 NW.js 和 Electron 框架的内部机制，同时也有助于对 Node.js 陌生的人理解 Node.js。本书的第 3 部分介绍了如何使用 NW.js 和 Electron 实现桌面应用的特定功能。

第 7 章介绍了如何设置桌面应用的显示、控制窗口大小和屏幕的各种模式以及如何进行不同模式之间的切换。

第 8 章介绍了如何构建在桌面托盘区域显示托盘应用程序。

第 9 章介绍了如何构建应用菜单以及应用内的上下文菜单。

第 10 章介绍了如何在应用内实现拖曳文件以及如何在不同的操作系统中提供一致的样式。

第 11 章介绍了如何使用计算机的摄像头实现一个自拍应用以及如何将拍摄的照片存储到计算机中。

第 12 章介绍了如何存取应用程序的数据。

第 13 章介绍了如何在 NW.js 和 Electron 中使用剪贴板 API 实现应用程序和操作系统之间的内容复制和粘贴。

第 14 章通过构建一个 2D 游戏介绍了如何在应用中支持快捷键，还介绍了如何实现系统级的快捷键操作。

第 15 章通过构建一个推特消息流客户端介绍了如何实现桌面消息提醒，以此来结束第 3 部分的内容。

这部分介绍了绝大部分 NW.js 和 Electron 都支持的特性，可帮助你了解这些特性框架是如何支持以及如何使用的，同时有助于判断到底哪个框架更适合你的需求。本书最后一部分介绍了应用发布前需要做的工作：写测试、调试代码以及最终产出一个可执行的二进制包分发给客户。

第 16 章介绍了如何在不同粒度上测试桌面应用。介绍了单元测试、功能测试以及集成测试的概念，还介绍了使用 Cucumber 编写应用特性需求文档，使用 Spectron 为桌面应用做自动化集成测试。

第 17 章介绍了如何调试代码，以此发现应用的性能瓶颈和缺陷，还介绍了如何使用像 Devtron 这样的工具来更进一步地分析你的应用。

第 18 章介绍了针对不同操作系统为应用程序构建二进制执行文件以及安装文件的多种方式，以此来结束这部分内容。

学完这部分内容后，你应该已经掌握了如何测试自己的应用、调试应用缺陷以及最终完成应用并分发给你的客户。

### About the code

This book contains many examples of source code, both in numbered listings and inline with normal text. In both cases, source code is formatted in a fixed-width font like this to separate it from ordinary text. In many cases, the original source codehas been reformatted; line breaks have been added and indentation reworked as necessary to accommodate the available page space in the book. Additionally, comments in the source code have often been removed from the listings when the code isdescribed in the text. Code annotations accompany many of the listings, highlighting important concepts.

Source code for the book's examples is available for download from the publisher's website at www.manning.com/books/cross-platform-desktop-applications and at http://github.com/paulbjensen/cross-platform-desktop-applications.

1-2『

[Manning | Cross-Platform Desktop Applications](https://www.manning.com/books/cross-platform-desktop-applications)

[paulbjensen/cross-platform-desktop-applications: Code examples for the book "Cross Platform Desktop Applications"](https://github.com/paulbjensen/cross-platform-desktop-applications)

已经下载附件「2021044Cross-Platform-Desktop-Applications附件」并存入书籍附件目录中。（2021-04-08）

』

本书包含诸多示例代码，有标明序号的多行代码，也有直接在正文中的单行代码。不论是哪种形式，代码都是以等宽字体的形式来表示的，以此来和正文进行区分。大多数情况下，源代码都是格式化过的；为了适应书页的空间添加了必要的换行和缩进。除此之外，当有专门解释源代码的文字时，代码注释通常就被去掉了。一般在多行代码以及高亮显示的重要概念时会有代码注解。
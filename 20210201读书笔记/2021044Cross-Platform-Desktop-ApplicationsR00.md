# 2021044Cross-Platform-Desktop-ApplicationsR00

## 记忆时间

## 卡片

### 0101. 主题卡 ——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡 ——

根据反常识，再补充三个证据——就产生三张术语卡。

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

## About this book

NW.js and Electron are desktop application frameworks powered by Node.js. They allow developers to create cross-platform desktop apps using HTML, CSS, and Java-Script. They offer web designers and developers a way to take their existing skills for crafting web apps and interfaces, and apply that to building desktop apps. The frameworks also support shipping apps for Mac OS, Windows, and Linux from the same codebase, meaning that developers can save time and energy when creating desktop apps that all OSs can use.

NW.js and Electron come from a shared history, and have some similar approaches to app features. This book covers both frameworks topic by topic, helping you to see what they have in common, and where they differ in their approaches. This will help you to decide which framework is best for your needs. We'll cover a broad range of apps and features together, to spark your passion and interest, as well as provide ideasfor things you might want to build but don't know how.

I hope you enjoy the book, and that you get to make something great with it.

### Who should read this book 

Anyone who has experience with HTML, CSS, and JavaScript can pick up this bookand get to grips with it right away. Experience with Node.js is not a requirement, but experience will come in handy. If you're completely new to HTML, CSS, and JavaScript, then it would be best to get acquainted with those technologies before youbegin to read this book.

### How this book is organized

This book has 18 chapters, organized into 4 parts.

Part 1 is an introduction to the frameworks:

■ Chapter 1 introduces NW.js and Electron, describing what they are, how they came about, what a Hello World app looks like in both frameworks, and some of the real-world apps that have been produced with them.

■ Chapter 2 then explores a direct comparison of the frameworks by building a file explorer application in each one.

■ Chapter 3 continues to flesh out some features of the file explorer application. 

■ Chapter 4 rounds off part 1 by building executable versions of the app for different OSs.

By the end of the first part, you'll have seen how to build a full-feature app with both frameworks.

Part 2 (chapters 5-6) looks at understanding the internals of NW.js and Electron from a technical perspective:

■ Chapter 5 looks at Node.js, the programming framework behind both NW.jsand Electron. It covers how Node.js works, how asynchronous programming is different from synchronous programming, and the use of callbacks, streams, events, and modules.

■ Chapter 6 looks at how NW.js and Electron operate under the hood in terms of how they combine Chromium with NW.js, and how they handle state betweenthe back end and front end.

This will help demystify the magic that NW.js and Electron perform to make their frame-works operate, and provide a useful guide to Node.js for those new to the framework.

In part 3 of the book, we'll look at how to start fleshing out specific features of desktop apps with NW.js and Electron:

■ Chapter 7 looks at controlling how the app can be displayed, in terms of the window dimensions and different screen modes, and how to toggle between them.

■ Chapter 8 explores how to create tray applications that sit in the tray area of desktops.

■ Chapter 9 shows how to build app and context menus for integrating into your apps.

■ Chapter 10 introduces dragging and dropping files into your app, and being able to craft the UI to have the same look and feel as other OSs.

■ Chapter 11 uses your computer's webcam to build a selfie app and to save the photos to your computer.

■ Chapter 12 looks at ways in which you can store app data for your apps, as well as how to retrieve it.

■ Chapter 13 shows how to use the clipboard APIs of both NW.js and Electron to copy and paste contents to and from the OS's clipboard.

■ Chapter 14 uses a 2D game to demonstrate how to add keyboard shortcuts toyour apps, as well as how to program global shortcuts that are accessible acrossthe entire OS.

■ Chapter 15 rounds off the part by exploring how to implement desktop notifications for a Twitter streaming client.

This part demonstrates a broad range of features that both NW.js and Electron support, helping you to see how the frameworks go about providing those features, and giving you a chance to evaluate which framework suits your needs best.

In the final part of the book, we'll look at things you can do to prepare your app for production: writing tests, debugging code, and finally, producing executable binaries for shipping to your customers:

■ Chapter 16 looks at ways you can approach testing your desktop apps, and at different levels. It introduces the concepts of unit, functional, and integration testing, using Cucumber to document how your app features work, and using Spectron to automate testing your Electron apps at an integration level.

■ Chapter 17 explores ways you can debug your code to help spot performance bottlenecks and bugs, and covers tools like Devtron to help inspect your app ingreater detail.

■ Chapter 18 finishes off the part by looking at various options for building executable binaries of your app, as well as creating setup installers for the different OSs.

By the end of this part, you should be in a position to test your apps, debug any issues that may occur with them, and finally get them built and shipped to your customers.

### About the code

This book contains many examples of source code, both in numbered listings and inline with normal text. In both cases, source code is formatted in a fixed-width font like this to separate it from ordinary text. In many cases, the original source codehas been reformatted; line breaks have been added and indentation reworked as necessary to accommodate the available page space in the book. Additionally, comments in the source code have often been removed from the listings when the code isdescribed in the text. Code annotations accompany many of the listings, highlighting important concepts.

Source code for the book's examples is available for download from the publisher's website at www.manning.com/books/cross-platform-desktop-applications and at http://github.com/paulbjensen/cross-platform-desktop-applications.

1-2『

[Manning | Cross-Platform Desktop Applications](https://www.manning.com/books/cross-platform-desktop-applications)

[paulbjensen/cross-platform-desktop-applications: Code examples for the book "Cross Platform Desktop Applications"](https://github.com/paulbjensen/cross-platform-desktop-applications)

已经下载附件「2021044Cross-Platform-Desktop-Applications附件」并存入书籍附件目录中。（2021-04-08）

』


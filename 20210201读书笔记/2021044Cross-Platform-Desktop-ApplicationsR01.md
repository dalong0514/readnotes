## 记忆时间

## 目录

0101 Introducing Electron and NW.js

0201 Laying the foundation for your first desktop application

## Part 1 Welcome to Node.js desktop application development

Two frameworks prevail when it comes to building desktop applications with Node.js: NW.js and Electron. In the first part of the book, you'll be introduced to those frameworks and what advantages they have compared to other app frameworks, build a quick Hello World application with both NW.js and Electron, and then see what kinds of applications have been built.

In chapter 2, we'll begin to put those frameworks to use by building a file explorer app. We'll flesh out the skeleton of the app and add features to it, and explore the different approaches that NW.js and Electron take.

In chapter 3, we'll continue to iterate on the file explorer app by adding more features such as search and opening files. We'll then round up the app in chapter 4 by building executable versions for Mac OS, Windows, and Linux. By the end of part 1, you'll have gotten to know both NW.js and Electron, and put your knowledge to practical use in a real-world application.

第 1 部分 欢迎来到 Node.js 桌面应用开发的世界

说到使用 Node.js 构建桌面应用就不得不提这两个框架：NW.js 和 Electron。

本书第 1 章将为你介绍这两个框架，以及它们相比其他框架的优势在哪里，还会介绍如何使用 NW.js 和 Electron 快速构建一个 Hello World 应用，然后介绍已有的使用这两个框架构建的应用有哪些。

第 2 章通过构建一个文件浏览器应用，介绍如何使用这两个框架。我们会从头开始构建这个应用，并逐步添加更多的特性，构建过程中会介绍 NW.js 和 Electron 在实现这个应用上的区别。

第 3 章我们会继续为这个文件浏览器应用添加更多的特性，比如，搜索文件和打开文件。随后在第 4 章我们会完成这个应用并针对 Mac OS、Windows 和 Linux 构建应用的可执行版本。读完第 1 部分后，你就会对 NW.js 和 Electron 有所了解，并可以将你学到的知识用于实际应用的开发中。

## 0101. Introducing Electron and NW.js

### Summary

This chapter introduced you to NW.js and Electron and explained how they help web developers build desktop apps. We explored reasons why you might want to prefer Node.js desktop apps over building a web app, and how those frameworks help web developers by letting them use the same tools and technologies they're already familiar with.

We then looked at the way that a simple Hello World app works and looks with different frameworks, across different OSs. This gave you a chance to understand how easy it is to take a web page and turn it into a desktop app.

We examined the features that make NW.js and Electron great frameworks for desktop app development, such as their use of the popular Node.js framework and the npm ecosystem, and the way they provide native executables for the different OSs from a single codebase. Finally, we explored a couple of real-life examples of NW.js and Electron in the wild and saw how apps have been successful in their own domains. This shows you what's possible with Node.js desktop apps, and hopefully provides inspiration for any app ideas that you have.

In the next chapter, we'll get our hands dirty and start building a file explorer desktop app with both NW.js and Electron. This will help you understand how you go about building desktop apps with those frameworks as well as how they compare in their approaches to desktop app development.

本章介绍了 NW.js 和 Electron，以及它们如何帮助开发者构建桌面应用。还分析了为何相比构建 Web 应用更应该使用 Node.js 开发桌面应用的原因以及那些框架是如何通过让 Web 开发者使用他们熟悉的工具和技术帮助他们开发桌面应用的。紧接着，介绍了使用不同框架构建同一个简单的 Hello World 应用，在不同的操作系统中的工作机制和样子。这也为大家展示了把一个 Web 页面嵌入一个桌面应用是多么容易。

我们检视了那些能让 NW.js 和 Electron 成为优秀的桌面应用开发框架的特性，诸如，它们都使用了 Node.js 框架、npm 生态系统以及支持从同一份代码构建出面向不同操作系统的可执行文件。最后，我们一起看了几个业界使用 NW.js 和 Electron 开发的桌面应用，也介绍了这些应用是如何在它们各自的领域取得成功的。这部分为大家展示了 Node.js 桌面应用的潜力，同时也希望可以为大家在开发桌面应用方面带来灵感。

下一章，我们开始动手使用 NW.js 和 Electron 构建一个文件浏览器桌面应用。这将有助于你理解如何着手使用这些框架开发桌面应用，以及这两个框架在桌面应用开发方面有何不同。

### 1.0

This chapter covers: 1) Understanding why Node.js desktop apps are the rage these days. 2) Previewing Node.js desktop application frameworks Electron and NW.js. 3) Using these frameworks to build cross-platform desktop apps with Node.js. 4) Comparing the frameworks. 5) Identifying real-world applications built with Electron and NW.js.

Node.js is known as a programming framework that lets developers build server-side applications in JavaScript. Since its creation in 2009, it has spawned a variety of popular web frameworks like Express and Hapi, as well as real-time web frameworks like Meteor and Sails. It has also allowed developers to create isomorphic web apps using tools like Facebook's React, a UI library that has had a huge impact on web development in recent years. It's fair to have the impression that Node.js is purely about web apps, but the truth is that Node.js is far more than that.

Node.js can be used to build cross-platform desktop apps, and chances are you're using one of them today. If you've ever used Slack at work, edited code using Atom from GitHub, or watched a movie using Popcorn Time, then you've used a Node.js desktop app. It's becoming a popular choice for developers, in particular web developers with little experience in desktop application development — even Microsoft has built and shipped an IDE (Visual Studio Code) using Node.js.

In the Node.js ecosystem, there are two major frameworks for creating desktop apps: NW.js and Electron. Both are supported by major businesses (NW.js by Inteland Gnor Tech, and Electron by GitHub), both have large communities around them, and both share similar approaches to building desktop apps. This book shows how to build cross-platform desktop apps with both Electron and NW.js. You may be pleasantly surprised by how much they have in common — in fact, they have some-thing of a shared history, but we'll get to that later. For now, we'll explore some of the reasons why Node.js desktop apps have taken off and where they might be useful for you and your work.

本章要点：1）介绍为何 Node.js 桌面应用近期热度如此之高。2）Node.js 桌面应用开发框架 Electron 和 NW.js 一览。3）使用 Node.js 以及这两个框架构建跨平台桌面应用。4）介绍两个框架的异同。5）介绍市面上使用 Electron 和 NW.js 开发的应用。

Node.js 是一种编程框架，它可以让开发者使用 JavaScript 来构建服务端应用。自 2009 年诞生以来，它衍生出许多流行的 Web 框架，比如，Express 和 Hapi，还有像 Meteor 和 Sails 这样的构建实时应用的 Web 框架。它还可以让开发者使用像 Facebook 的 React 这样的工具开发复杂的 Web 应用，React 是近几年在 Web 开发领域影响非常大的 UI 库。对 Node.js 的第一印象固然是它是用于 Web 应用开发的，然而事实却是它远不止于此。

Node.js 还可以用来构建跨平台的桌面应用，而且也许你现在就在使用它构建出来的应用。如果你工作的时候用的是 Slack，编辑代码的时候使用的是 GitHub 的 Atom 编辑器，或者看电影的时候用的是 Popcorn Time，那么你实际上就在使用 Node.js 开发的桌面应用。越来越多的开发者，特别是没有桌面应用开发经验的 Web 开发者，开始尝试使用 Node.js 来开发桌面应用 —— 甚至连微软都已经在用 Node.js 开发它的 IDE （Visual Studio Code）了。

在 Node.js 的生态中，有两个主流的桌面应用开发框架： NW.js 和 Electron。这两者都得到了大公司的支持（NW.js 背靠英特尔和 Gnor Tech，Electron 则背靠 GitHub），它们都拥有庞大的社区，而且在实现支持构建桌面应用方面都采用类似的解决方案。也许你会为它们有众多共同点而感到惊讶 —— 实际上，它们有过一段共同的历史，这部分会在后续章节中进行介绍。现在，让我们来看看使用 Node.js 开发桌面应用之所以这么流行其背后的原因到底是什么，以及它们会在你工作的哪些方面起到帮助。

### 1.1 Why build Node.js desktop applications?

To answer this question, you have to see how software has changed over the past generation and visualize where it is going.

要回答这个问题，我们得先来看看软件在过去一代进程中发生了怎样的变化以及它们将会如何发展下去。

#### 1.1.1 Desktop to web and back

At the beginning of 2000, most software was available as desktop apps in shrink-wrapped boxes that you could buy from stores like Best Buy. You'd need to check the system requirements and make sure that it would work on the operating system (OS) you were running (which was Windows, for the majority of people). You'd then grab a CD-ROM out of the box, and install the software on your computer that way.

Over time, that began to change: improvements in web browsers, greater internet speeds and access, and the movement toward open source software resulted in a major shift in how software was created and distributed. The advent of AJAX spawned a new era of delivering software as web apps. These apps didn't require downloading anything onto the computer, and they could run across multiple OSs. Companies like Google and Facebook signaled the rise of the web as a powerful platform in the industry, and as people became accustomed to using apps online for a monthly fee, traditional software houses adapted and began to offer their software online.

It seemed like the web had won, but then mobile computing came along, leading to the rise of native apps for Apple iPhone and Android mobile devices. The industry changed again, and developers found themselves needing to adapt their business to support those devices too.

If reflecting on 16 years of software development shows anything, it's that there's a lot of change in the industry, and that we as developers will probably find ourselves supporting multiple computing platforms for years to come: desktop, web, mobile, and more. We're in the age of multiplatform computing.

Where does that leave desktop apps? Desktop apps have become one of a numberof computing platforms that we use in our day-to-day activities. But what has changedsince the 2000s is that where Microsoft Windows was the dominant OS for desktopcomputers back then, Apple has pared back that dominance with the popularity of itscomputers among creatives and professionals. Not only that, but Google's Chrome-books were the best-selling laptops in the U.S. in the first quarter of 2016. The year ofthe Linux desktop may have finally arrived. The point is this: you can't afford todevelop desktop apps that work on only Windows these days — there's a need for devel-oping apps that work across Mac OS and Linux as well.

Cross-platform desktop apps aren't a new concept; frameworks like Mono and Qt have provided a way to develop desktop apps that run across all three of the major OSs. Usually, developers with a background in programming languages like C, C++, and C# could come to grips with these frameworks and develop software for them. Other developers, like web developers, would need to learn a new language alongside a framework, and this would be a barrier to them developing desktop apps.

When NW.js and Electron came about, they offered an opportunity to build desktop apps with the same code used to create web apps — and not only that, these desktop apps could operate across Windows, Mac OS, and Linux. It was a massive win for both code and skills reusability and unleashed a wave of new apps.

In addition, the popularity of Node.js has meant that developers have been able to leverage a huge ecosystem of open source libraries to build their apps with. Node.js developers and web developers alike could suddenly make desktop apps, and some of the apps out there are truly fantastic. One that comes to mind is WebTorrent by Feross Aboukhadijeh, shown in figure 1.1.

WebTorrent is a desktop app that allows you to upload files for other users to download, much in the same fashion as BitTorrent. It uses WebRTC to enable peer-to-peer connections, and to show you how portable the code is, the library used in the desktop app is the same as the one you can use in a web browser. It's a truly fantastic piece of work.

The ability to support multiple OSs but write the software in a common and popular language has lots of pros because, as mentioned, desktop computing is still a major part of how people use computers today, even as new mobile computing platforms emerge. That's why Node.js desktop apps have become an interesting way to deliver software. The next section elaborates on some of the reasons why you may consider building Node.js desktop apps over web apps.

2000 年年初，绝大多数软件都是以桌面应用的形式存在的，它们被放在一个包装盒里，通过像百思买这样的商店进行售卖。你还得看它对系统的要求，确保它兼容你使用（绝大部分人用 Windows）的操作系统（OS）。然后，从包装盒中取出 CD 光盘，并将它安装到你的计算机中。

随着时代的发展，改变也渐渐开始了：Web 浏览器的崛起，网速的提高，网络访问便捷性的提升，以及软件的开源思潮，都对软件的构建和分发方式产生了巨大的影响。AJAX 的优势，让软件进入了一个以 Web 应用进行分发的新时代。这类应用不需要下载任何东西到你的计算机中，而且还可以在不同的操作系统中运行。像谷歌和脸书这样的公司在业界激发了 Web 应用作为强大平台的崛起，而且随着人们在线免费使用这些应用成为习惯之后，迫使传统软件服务商也开始提供线上版本。

看似 Web 应用已经获胜，然而随着移动设备的兴起，引领了针对苹果的 iPhone 手机和 Android 手机开发的原生应用的潮流。业界又发生了一轮改变，开发者们发现他们需要让他们的产品也支持这样的设备。反观十多年的软件开发进程，你会发现业界发生了巨变，作为开发者，我们渐渐觉得支持多计算平台的时代正在慢慢来临：桌面系统、Web 浏览器、移动设备，甚至更多。我们正处于多平台计算的时代。

那么桌面应用呢？桌面应用已经成为我们在日常生活中使用的计算平台之一。自 21 世纪以来，发生了很多变化。那时，微软的 Windows 系统是桌面计算机操作系统领域绝对的霸主，后来苹果公司的操作系统以它的创新性和专业性削弱了 Windows 的统治力。不仅如此，在 2016 年第一季度，谷歌的 Chromebook 成为全美最畅销的笔记本电脑。或许属于 Linux 系统的时代也终将会到来。关键是：现如今，你已经不能开发只支持 Windows 系统的应用了 —— 还得让你的应用支持 Mac OS 和 Linux。

跨平台的桌面应用并不是什么新鲜的东西；像 Mono 和 Qt 这样的框架早就可以让你开发出支持主流操作系统的应用了。通常，有像 C、C++，以及 C# 这样编程语言经验的开发者会选择这样的框架来开发软件，其他像 Web 开发者，面对这样的框架时则需要新学一门语言，可见开发桌面应用对他们来说多少有些门槛。

NW.js 和 Electron 出来的时候，它们可以让你重用 Web 应用的代码来构建桌面应用 —— 而且不仅如此，构建出来的应用可以同时在 Windows、Mac OS 和 Linux 上运行。这带来一个巨大的好处 —— 代码和技能都可以复用，并且释放了一拨儿新的应用。

除此之外，Node.js 的流行也意味着开发者们在构建他们的桌面应用时也可以受益于 Node.js 巨大的开源生态系统。Node.js 和 Web 开发者们都可以快速构建桌面应用，而且有些应用还真的很不错。其中我第一个想到的就是一款由 Feross Aboukhadijeh 开发的 WebTorrent，如图 1.1 所示。

WebTorrent 和 BitTorrent 很像，它是一款桌面应用，可以让你上传文件供他人进行下载。它使用 WebRTC 技术建立点对点的连接，而且这个桌面应用使用的技术库和 Web 应用所使用的是完全一样的，代码高度复用。这是最妙的地方。

支持多种操作系统，而软件本身可以使用同一种流行的编程语言编写，这种能力可以带来非常多的好处。正如此前所提到的，尽管新的移动计算平台正在崛起，但是桌面计算机至今仍然是人们常用的。这也是为什么使用 Node.js 构建桌面应用正变为一种有意思的分发软件的方式。接下来我将详细介绍为什么你更应该在 Web 应用基础上使用 Node.js 构建桌面应用。

图 1.1 Feross Aboukhadijeh 开发的 WebTorrent 应用

#### 1.1.2 What Node.js desktop apps offer over web apps

Web apps have thrived for a number of reasons:

1 Internet speeds improved and access increased, and, importantly, the cost of internet access went down, making the user base grow massively, unlike most other communication channels. 

2 Web browsers have benefitted from increased competition. As appealing alternatives to Internet Explorer emerged, new features were added to those browsers, which in turn enabled web apps to do new things. 

3 The relative ease of learning HTML, CSS, and JavaScript lowered the barrier of entry for developers to make web apps, as opposed to learning lower-level languages like C and C++. 

4 The rise of open source software meant that the cost of distributing and obtaining software declined significantly, meaning that developers with a bit of cash, time, and the right level of skill could build their own web apps.

When you look at all this, you can see why the web is such an important platform for developers to make software for. That said, there are still things that challenge and limit the ability of web apps today:

1 Internet access is not always available. If you're on a train and you go under a tunnel, chances are you'll lose internet access. If your web app depends on saving data, hopefully it will be able to store a local copy of the changes and allow for them to be synchronized via the internet when access resumes. 

2 If your app has a lot of features, the amount of data it will need to transfer over the internet to run the app could be large and may slow down the loading of the app. If it takes too long, people load something else — something proven by research into the impact that slow web page loading times have on e-commerce transactions. 

3 If you're working with large files (such as high-resolution images and videos) that are sitting on your desktop computer, then it might not make sense for them to be uploaded to the internet in order for a web app to edit them.

4 Because of the security policy of the web browser, there are limits to what hardware/software features of the computer the web app can access.

5 You have no control over what web browsers a user may use to visit your web app.

You have to use feature detection to cater to different web browsers, which restricts what features your app can use. The user experience (UX) can vary wildly.

Web apps are essentially restricted by the limits of internet access and browser features. It is in these circumstances that a desktop app may be preferable to a web app. Some of the benefits include the following:

1 You don't require internet access to start and run the app.

2 Desktop apps start instantly, without having to wait for resources to download from the internet.

3 Desktop apps have access to the computer's OS and hardware resources, including access to the files and folder on the user's computer.

4 You have greater control over the UX with the software. You don't have to worry about how different browsers handle CSS rules and what JavaScript features they support.

5 Once a desktop app is installed on a user's computer, it's there. It doesn't depend on you running web servers to support the app, where you need to offer 24/7 support in case your web app goes down, or worse, your web-hosting provider encounters technical difficulties.

Usually, desktop apps have required developers to be proficient in languages like C++, Objective-C, or C#, and knowing frameworks like .NET, Qt, Cocoa, or GTK. For some developers, that can be a barrier to entry and may discourage them from considering the possibility of building a desktop app.

The great thing about Node.js desktop application frameworks like Electron and NW.js is that they have significantly lowered that barrier of entry for developers. By allowing developers to create apps using HTML, CSS, and JavaScript, they've opened the door for web developers to also be desktop app developers, with the added benefit of being able to use the same code across both the web app and desktop app platforms.

Now it's time to introduce the frameworks. As mentioned earlier in the chapter, Electron and NW.js have something of a shared history, so I'll touch on the origins of both frameworks and then cover each in some detail.

1.1.2 Node.js 桌面应用相比 Web 应用有什么优势

Web 应用的繁荣主要源于以下几个原因：

1、网速的提升以及使用互联网的人越来越多，更重要的是，使用互联网的成本越来越低，使得相比其他通信渠道，互联网的使用人口基数正在大规模增加。

2、Web 浏览器受益于不断加剧的竞争。随着 IE 之外的浏览器不断出现，这些浏览器拥有了新的特性，继而让 Web 应用也可以利用这些新特性做出一些新的东西来。

3、相比学习像 C 和 C++ 这样的底层语言，简单易学的 HTML、CSS 和 JavaScript 降低了开发者制作 Web 应用的准入门槛。

4、开源软件的崛起意味着分发和获取软件的成本大大降低，这就使得开发者哪怕只有有限的资金和精力，只要拥有对应的开发技能都可以构建他们自己的 Web 应用。

通过上述这几点就不难理解，对于开发者而言，为何 Web 是一个非常重要的平台了。不过现如今，还是存在一些因素对 Web 应用产生了一定的制约和挑战：

1、网络不是一直可用的。当你在火车上或者在隧道里的时候，就可能没有网络。如果你的 Web 应用需要保存数据，那么理想状态下应当是先在本地保存一份，然后当网络恢复的时候再同步到云端。

2、如果你的应用有大量特性，那么为了让应用运行起来，需要通过网络传送的数据量可能非常大，而且可能会拖慢应用的加载。如果传输时间太长的话，用户就可能会放弃转而使用其他应用了 —— 有研究表明网页加载速度变慢会影响线上交易。

3、如果你的应用需要处理计算机中的大文件（比如高清图片和视频），那么将它们上传到网上再通过 Web 应用进行编辑操作就不是一个好的方案了。

4、由于 Web 浏览器有安全策略，因此 Web 应用对于访问计算机中的软硬件资源是受限的。

5、你无法控制用户使用哪个浏览器来访问你的 Web 应用，因此不得不使用特性检查的方式来区分不同的浏览器，这会限制应用可用的特性。用户体验（UX）也会区别很大。

Web 应用主要受限于网络和浏览器特性。在这些方面，桌面应用要优于 Web 应用。下面列出了桌面应用的一些优点：

1、启动和运行应用不依赖网络。

2、桌面应用可以即时启动，不需要等待资源从网络下载下来。

3、桌面应用可以访问计算机的操作系统和硬件资源，包括可以读写用户计算机中的文件系统。

4、桌面应用可以更好地控制软件的用户体验。不需要担心不同浏览器处理 CSS 的规则以及哪些 JavaScript 特性是被支持的。

5、一旦桌面应用安装到用户计算机中后，它就在那儿了。它不像 Web 应用那样需要一台 Web 服务器，还要提供 7×24 小时的支持，以防 Web 应用宕机，甚至更糟糕的，Web 服务托管商遇到技术问题。

通常，开发桌面应用要求开发者们精通像 C++、Objective-C，或者 C# 这样的语言以及像 ．NET、Qt、Cocoa 或者 GTK 这样的框架。对于部分开发者而言，准入门槛有点高，很可能会放弃使用这些技术来构建桌面应用。

像 Electron 和 NW.js 这样的 Node.js 桌面应用框架最棒的地方就在于它们大大降低了开发者的准入门槛。支持开发者使用 HTML、CSS 和 JavaScript 开发桌面应用，而且还可以在 Web 应用和桌面应用之间共享同一份代码，这无异于是给 Web 开发者打开了一扇通往成为桌面应用开发者的门。

现在是时候开始介绍这两个框架了。正如前面章节中提到的，Electron 和 NW.js 有过一段共同的历史，所以我先来介绍一下这两个框架的起源，然后再对它们进行详细的介绍。

### 1.2 The origins of NW.js and Electron

Back in 2011, Roger Wang managed to find a way to combine WebKit (the browser engine behind Safari, Konqueror, and Google Chrome at the time) with Node.js, so that you could access Node.js modules from the JavaScript code running inside a web page. This Node.js module was given the name node-webkit. He continued to work on the project at Intel's Open Source Technology Center in China, which gave its support

to the project by letting Roger work on it full time. Not only that, he was allowed to hire others to work on it too.

In the summer of 2012, a senior college student named Cheng Zhao joined Intel as an intern to work on node-webkit. He worked with Roger to help improve its internal architecture, which involved changing how Node.js and WebKit were combined. As the code evolved, node-webkit moved from being a mere Node.js module to becoming a framework for desktop apps. Node-webkit was given interesting uses within third-party apps. The Light Table editor was the first to make use of node-webkit to deliver its functionality and helped to promote the framework to other developers.

In December of the same year, Cheng left Intel to work at GitHub as a contractor. He was tasked with helping to port GitHub's Atom editor from using Chromium Embedded Framework and native JavaScript bindings to using node-webkit.

The efforts to port Atom to node-webkit encountered difficulties (see https:// github.com/atom/atom/pull/100), so they abandoned that approach. Instead, they decided to create a new native shell for Atom, which they called Atom Shell. This approach to combining WebKit with Node.js differed from the approach taken by node-webkit. Cheng Zhao focused all of his efforts into working on Atom Shell, which GitHub later open sourced shortly after open sourcing its text editor, Atom.

During this time, Node.js was going through a period of splintering — members of the Node.js community created a fork of Node.js called IO.js in order to get updates into the project faster, and in the WebKit community, Google announced that it was going to fork the WebKit project for Google Chrome into a variant called Blink. The combination of these changes led to renaming node-webkit as NW.js, and GitHub renamed the Atom Shell framework as Electron. Over time, Electron quickly acquired a number of admirers and was being used in high-profile apps like Slack and Visual Studio Code. It eventually became a juggernaut of its own creation, distinct from its original purpose as a tool for delivering Atom.

Although NW.js was the first Node.js desktop application framework, Electron has quickly emerged as a popular framework that has overshadowed NW.js, although both have been heavily worked on by the same developer at different points in time and share a lot of common code in terms of how users use their APIs for creating app features. Each has evolved a different approach to its internal architecture and has spawned separate communities that actively promote their respective projects.

In this respect, this book essentially covers two frameworks that do the same thing in slightly different ways. It's a fairly unique situation in that the frameworks share so much history and are similar enough to merit being evaluated together. There's a natural inclination to pick whichever is the bigger of the two and go with that, and the answer to that would be Electron (if you go by popularity and momentum), but some prefer NW.js to Electron for its relative simplicity in how you execute code and load the app, as well as for supporting computing platforms like Google Chromebooks, and because of other matters of programming opinion. I prefer to provide the information and let you decide what you want to use. It's more ground to cover, but you'll be better informed.

If you're interested in digging into the history of both projects a bit more, the following links provide helpful pointers:

[From node-webkit to Electron 1.0](http://cheng.guru/blog/2016/05/13/from-node-webkit-to-electron-1-0.html)

[Question: Electron Origins · Issue #5172 · electron/electron](https://github.com/electron/electron/issues/5172#issuecomment-210697670)

If you're looking for posts that compare and contrast the frameworks, here are some good links to look at as well:

http://electron.atom.io/docs/development/atom-shell-vs-node-webkit/

[NW.js & Electron Compared (2016 Edition) - TangibleJS](https://tangiblejs.com/posts/nw-js-and-electron-compared-2016-edition)

That's a brief history of the two projects and how their paths have formed over time. We'll now dive into each framework, starting with the first framework to emerge on the scene: NW.js.

1.2 NW.js 和 Electron 的起源

早在 2011 年，Roger Wang 想要找一个方法将 WebKit（当时是 Safari、Konqueror 以及谷歌的 Chrome 浏览器所使用的浏览器引擎）和 Node.js 整合起来，这样就可以让 Web 页面中的 JavaScript 代码访问到 Node.js 模块了。当时，这个项目作为一个 Node.js 的模块在开发，取名为 node-webkit。Roger Wang 在中国的英特尔开源技术中心做这个项目，公司给予支持让他全职做这个项目。不仅如此，还允许他招聘其他工程师一起来做。

到了 2012 年夏天，一位叫赵成的大学生作为实习生加入了英特尔，参与到了这个项目中。他帮助 Roger Wang 一起改进其内部架构，包括改变了 WebKit 和 Node.js 整合的方案。随着项目的发展，node-webkit 从单纯的 Node.js 模块发展为一个用于构建桌面应用的框架。第三方应用慢慢对 node-webkit 产生了兴趣。Light Table 编辑器是首个使用 node-webkit 开发的应用，并且其开发者还帮助改进了框架本身。

2012 年 12 月，赵成离开了英特尔，为 GitHub 提供外包服务。他的任务是帮助把 GitHub 的 Atom 编辑器从使用嵌入的 Chromium 框架和原生的 JavaScript 绑定迁移到 node-webkit 上。

把 Atom 迁移到 node-webkit 困难重重（可参见 [Port to node-webkit by probablycorey · Pull Request #100 · atom/atom](https://github.com/atom/atom/pull/100) 上的文章），因此他们放弃了这个方案。取而代之的是为其重新开发一个新的原生 shell，取名为 Atom Shell。这个整合了 WebKit 和 Node.js 的方案和 nodewebkit 所使用的不同。赵成倾尽全力在 Atom Shell 这个项目上，后来 GitHub 在开源 Atom 编辑器后很快就开源了 Atom Shell。

那个时候，Node.js 经历了一段分裂期 —— 为了更快地推进 Node.js 项目，社区成员克隆了一份 Node.js 并取名为 IO.js；与此同时，在 WebKit 社区，谷歌声明打算克隆谷歌 Chrome 浏览器的 WebKit 项目并开发一个变种版本 —— Blink。这些变化导致了 node-webkit 也将项目改名为 NW.js，GitHub 也将 Atom Shell 框架改名为 Electron。随着时间的推移，Electron 快速获得了一批粉丝，而且被像 Slack 和 Visual Studio Code 这样知名度很高的应用所使用。最终它发挥出了始料未及的巨大力量，远不是当初仅仅是作为 Atom 背后的工具。

尽管 NW.js 是首个桌面应用开发框架，但是 Electron 还是快速发展为一个流行的框架，风头盖过了 NW.js。尽管两者都是由同样的作者只是在不同时间开发的，并且在用来创建桌面应用的 API 方面共享了许多代码，但它们在内部架构上采用了不一样的方案，而且各自衍生出了各自的社区，社区都积极地帮助改进了各自的项目。

有鉴于此，本书主要介绍这两个框架，因为它们用略微不同的方式完成同一件事情。这两个框架拥有那么多共同的历史，而且实在是太相似了，这种情况也是相当独特的，值得拿出来互相对比。既然是对比，就很自然会想知道哪个更好，这个问题的答案应当是 Electron（从流行度和发展势头），不过也有人更喜欢 NW.js，因为相对而言，它在代码运行和应用加载方面更加简单，而且它还支持像谷歌的 Chromebook 这样的计算平台，也可能是出于其他编程方面的考虑。我更倾向于给你提供客观的信息，把决定权交到你自己手里。相比告诉你使用哪个框架，本书只陈述客观事实供你自己做决定。

如果你想了解更多关于这两个框架的历史细节，可以参阅下面的链接：

[From node-webkit to Electron 1.0](http://cheng.guru/blog/2016/05/13/from-node-webkit-to-electron-1-0.html)

[Question: Electron Origins · Issue #5172 · electron/electron](https://github.com/electron/electron/issues/5172#issuecomment-210697670)

如果你想找一些关于这两个框架对比的文章，可以看看下面的这几篇：

http://electron.atom.io/docs/development/atom-shell-vs-node-webkit/

[NW.js & Electron Compared (2016 Edition) - TangibleJS](https://tangiblejs.com/posts/nw-js-and-electron-compared-2016-edition)

以上就是这两个框架的简史以及它们各自的发展进程。现在我们要深入介绍这两个框架了，首先出场的是 NW.js。

### 1.3 Introducing NW.js

To recap, NW.js is a framework for building desktop apps with HTML, CSS, and JavaScript. It was created back in November 2011 by Roger Wang at Intel's Open Source Technology Center in China. The idea was that by combining Node.js with WebKit (the web browser engine behind Chromium, an open source version of Google Chrome), you could create desktop apps using web technologies. This was the basis for the framework's original name, node-webkit.

By combining Node.js with Chromium, Roger found a way to create apps that could not only load an HTML file with CSS and JavaScript inside an app window, but also could interact with the OS via a JavaScript API. This JavaScript API could then control visual aspects like window dimensions, toolbar, and menu items as well as provide access to local files on the desktop — things web apps couldn't do.

To give you an idea of what this looks like, let's walk through an example Hello World app for NW.js.

1.3 NW.js 介绍

简单来说，NW.js 是一个框架，它支持用 HTML、CSS 和 JavaScript 来构建桌面应用。起初它于 2011 年 11 月，由 Roger Wang 在英特尔中国开源技术中心创建。其背后的想法就是通过整合 Node.js 和 WebKit （Chromium 使用的 Web 浏览器引擎，Chromium 是开源版的谷歌 Chrome 浏览器），支持使用 Web 技术来创建桌面应用。所以一开始它被命名为 node-webkit。

通过整合 Node.js 和 WebKit，Roger 发现不仅可以在应用视窗内载入 HTML、CSS 和 JavaScript 文件，还可以通过 JavaScript API 和操作系统进行交互。通过这个 JavaScript API 可以控制视窗的视觉元素，比如，视窗大小、工具条以及菜单项，而且还可以访问本地文件系统 —— 这些是 Web 应用无法做到的。

为了让你对 NW.js 有一个形象的认识，我们来用 NW.js 构建一个 Hello World 示例应用。

#### 1.3.1 A Hello World app in NW.js

This example application will give you a better understanding of what Node.js desktop apps are like with NW.js. Figure 1.2 show a design of the app we'll build.

The code for this app is available in the GitHub repository for this book at http:// mng.bz/4W7Y.

If you want to get the code to run the app and see it in action, follow the instructions in the README.md file there. It's ready-made to go. But if you want to see how the sausage is made, then read on and we'll build the app from scratch.

The first step is to check whether you have Node.js installed. If you already do, great — move on to the next section, “Installing NW.js,” but if not, you'll find instructions for installing Node.js in the appendix.

INSTALLING NW.JS

Node.js comes with a package management tool called npm that handles installing libraries for Node.js, and NW.js can be installed using it. On your computer, open the command-line program for your OS (Command Prompt or PowerShell on Windows, and Terminal on both Mac OS and Linux).

After you've opened your command-line program, run the following command:

npm install –g nw

This will install NW.js on your computer as a Node.js module available to all of your Node.js desktop apps.

CREATING THE HELLO WORLD APP

The app is so small that you can create the files by hand. At the bare minimum, you only need two files:

1 A file named package.json — This contains configuration information about the app, and is required by NW.js.

2 An HTML file — This file will be loaded by the package.json file and displayed in the app window. In this case, it's a file called index.html (but it can be named something else, such as app.html or main.html).

Start by creating a folder for the app's file. On your computer, go where you like to store your project source code and create a folder named hello-world-nwjs. Then you can create the package.json file that will be stored inside the hello-world-nwjs folder.

In your text editor/IDE, create a file named package.json inside the hello-worldnwjs folder and insert the following code into it:

```json
{
	"name" : "hello-world",
	"version" : "1.0.0",
	"main" : "main.js"
}
```

The package.json file consists of some configuration information about the app: its name, the main file to load when the app starts, and its version number. These fields are required by NW.js (though the version field is required by npm). The name field must contain lowercase alphanumeric characters only — there can be no space characters in the name.

The main field contains the file path for the entry point of your app. In the case of NW.js, you have the option of loading either a JavaScript file or an HTML file, but HTML files tend to be the common choice for NW.js apps. The HTML file is loaded into the app window, and to demonstrate this, you'll create an HTML file called index.html that will be loaded.

Inside the hello-world-nwjs folder, create a file named index.html and insert the code in the following listing.

Once you've saved the index.html file on your computer, you can run the app on your computer. Inside the hello-world-nwjs folder, run the following command on your terminal:

```
nw .
```

If you're running on Mac OS, figure 1.3 shows what you should see.

If you're running Linux, figure 1.4 shows the same app running on openSUSE 13.2 (Linux has many distributions, and openSUSE is one of the well-known distributions).

The Windows 10, Mac OS, and Linux versions of NW.js all share the same way to get the app started, which is handy. Type the same command in your Command Prompt, and you should see something like figure 1.5 on a Windows 10 computer.

Figure 1.5 The Hello World app running on Windows 10. The app looks almost identical to the app running on openSUSE Linux (minus the app window and a slight difference in font rendering).

If you click the Say Hello button in the middle of the app screen, you'll see an alert dialog that says “Hello World.” If you were to take the index.html file and load it in a web browser such as Google Chrome, Microsoft Edge, or Mozilla Firefox, you would see the same screen and get the same result. That's the point — you can take an HTML page for a website and turn it into a desktop app with NW.js without having to change the code.

At this point you might say, “Well, if that's the case, why don't I use a desktop app template that renders an HTML page inside a window and make do with that?” That's not a bad question, and some apps have taken this approach.

The reasons against such an approach could boil down to ease of development. You might not know C++, or if you do, you may not want to be compelled to compile code every time you make a feature change. Also, you might want to use features that are only available natively to the desktop framework and are beyond what an HTML file embedded inside of an app window shell would be able to access. The other major reason is that as desktop app frameworks, both Electron and NW.js provide a rich feature set to support you in developing desktop apps, covered in the next section.

1.3.1 使用 NW.js 构建 Hello World 应用

这个示例应用将帮助你理解使用 Node.js 开发出来的桌面应用是什么样子的。图 1.2 是我们即将构建的示例应用设计稿。

示例应用的代码可以通过本书的 GitHub 仓库进行查看，[cross-platform-desktop-applications/chapter-01/hello-world-nwjs at master · paulbjensen/cross-platform-desktop-applications](https://github.com/paulbjensen/cross-platform-desktop-applications/tree/master/chapter-01/hello-world-nwjs)。

参照里面的 README.md 文件就可以把代码运行起来并看到效果。里面写得很清楚。不过，如果你想知道是怎么构建起来的，那就继续看下面的内容，我们会从头开始把它构建起来。

第一步，你得检查 Node.js 是否已经安装好了。如果已经安装好了，那太棒了，直接移步到本章后面的「安装 NW.js」部分。如果还没安装，可参照本书附录 A 中的安装指南进行安装。

安装 NW.js

Node.js 内置了一款包管理器工具，名字叫 npm，可以用它来安装 Node.js 模块。NW.js 也可以用 npm 来安装。打开操作系统的命令行程序（Windows 用户可以打开命令提示符应用或者 PowerShell，Mac OS 和 Linux 用户可以打开 Terminal）。

打开命令行程序后，输入如下命令：

```
npm install -g nw
```

1-2『这里直接用 brew 安装的 nw.js 套件：`brew cask install nwjs`。顺便知道了查看软件的命名：`brew cask list`。』

完成后，NW.js 会以 Node.js 模块的形式安装在你的计算机中，所有的 Node.js 桌面应用都可以使用。

构建 Hello World 应用

这个应用很小，你可以手动来创建文件。不过你至少需要下面这两个文件。

1 package.json 文件 —— 这个文件是 NW.js 要求必须要有的，其包含了应用的配置信息。

2 一个 HTML 文件 —— 这个文件声明在 package.json 中，会被自动加载并显示在应用视窗中。在本例中，我们将这个文件取名为 index.html （不过你可以随便为它取名字，比如 app.html 或者 main.html）。

先来新建一个应用文件夹。在你的计算机中，找到一个你觉得合适的存储应用代码的位置，新建一个名为 hello-world-nwjs 的文件夹。然后在该目录下就可以新建一个 package.json 文件了。

在 hello-world-nwjs 文件夹中用你的文本编辑器或者 IDE 创建一个名为 package. json 的文件，并插入如下代码：

```json
{
	"name" : "hello-world",
	"version" : "1.0.0",
	"main" : "main.js"
}
```

package.json 文件包含了一些与应用相关的配置信息：应用的名字、应用启动时要加载的主文件以及版本号。这些字段是必需的（其中 version 字段是 npm 要求的）。name 字段只能包含小写的英文字母或者数字，且不能有空格。

main 字段指定了应用入口文件的路径。在 NW.js 中，这个文件可以是 JavaScript 文件也可以是 HTML 文件，不过通常倾向于使用 HTML 文件。HTML 文件会被加载显示到应用视窗中，为了验证，我们来创建一个 index.html 文件。

在 hello-world-nwjs 文件夹中，创建一个名为 index.html 的文件，并插入代码清单 1.1 所示的代码。

代码清单 1.1 Hello World 应用的 index.html 文件的代码

保存 index.html 文件后，就可以在计算机中运行这个应用了。进入 hello-worldnwjs 文件夹，输入如下命令：

nw

1『上

面的命令没用，需要用 `nw .`。但前提需要设置别名和环境变量。

```
# 打开bash_profile环境变量配置文件
vim ~/.bash_profile

# 设置环境变量-nwjs的别名
alias nw="/Applications/nwjs.app/Contents/MacOS/nwjs"

# 应用环境变量
source ~/.bash_profile

#命令行输入 nw 回车启动即可（等同于桌面点击图标启动）
nw
```

不要在 `.bash_profile` 里设置别名，在 `.zshrc` 里设置别名更好。经测试，可以跑起来了。

』

如果使用的是 Mac OS，会看到图 1.3 所示的样子。

图 1.3 运行在 Mac OS 上的 Hello World 应用。这个应用截图和设计稿除了窗口大小之外几乎完全一样

如果在 Linux （openSUSE 13.2）上运行，就会看到如图 1.4 所示的样子（Linux 有很多发行版，openSUSE 是知名的发行版之一）。

图 1.4 运行在 openSUSE13.2 上的 Hello World 应用。它看起来和 Mac OS 上的差不多，视窗标题、颜色以及字体渲染效果略有不同

Windows 10、Mac OS 以及 Linux 版本的 NW.js 采用的启动应用方式相同，都很简便。在 Windows 10 的计算机中，打开命令提示符应用并输入同样的命令，就能看到图 1.5 所示的样子。

图 1.5 运行在 Windows 10 上的 Hello World 应用。它和 openSUSE Linux 上应用的样子几乎一样（除了应用视窗和字体渲染效果略有不同之外）

如果单击屏幕中间的 Say Hello 按钮，会弹出一个写着「Hello World」的警示框。如果使用谷歌的 Chrome、微软的 Edge 或者 Mozilla 的 Firefox 浏览器打开 index.html 文件，也能看到同样的界面，单击按钮后也会看到同样的结果。这就是关键 —— 代码不需要修改，你就可以直接将网站的 HTML 页面转变为 NW.js 开发的桌面应用。

关于这点你也许会说「好吧，那既然这样，我为什么不用这样一个方案呢 —— 用一个桌面应用模版，将 HTML 页面渲染在视窗中？」这个问题问得还不错，有些应用就是这么做的。

但这个方案不好的原因是没有简化开发。因为你可能不懂 C++，又或者你懂，但你也许不想每次做了一点改动都要重新编译代码才能运行。又或者，你可能想用原生桌面应用才有的特性，而这些特性在一个内嵌在应用视窗中的 HTML 文件中无法使用。另外一个主要原因是，作为桌面应用开发框架，Electron 和 NW.js 都为你开发桌面应用提供了丰富的特性，这部分会在接下来的内容中介绍。

#### 1.3.2 What features does NW.js have?

NW.js has a set of features that makes it appealing for developers to use when building desktop apps. In a generic overview, they are as follows:

1 A JavaScript API for creating and accessing native UIs and APIs to the OS: control windows, add menu items, tray menus, read/write files, access the clipboard, and more.

2 The ability to use Node.js inside your app as well as install and use a huge library of Node.js modules via npm.

3 Being able to build executables of the app for each OS from a single codebase.

I'll explain each bullet point in more detail in the next sections.

ACCESSING OS NATIVE UI AND API VIA JAVASCRIPT

A good desktop app integrates well into the user's OS: a music app will work with the media keyboard shortcuts on a user's keyboard, a chat app may have a menu icon in the tray area of the OS, and a productivity app may provide notifications when actions have completed.

NW.js provides a large API for getting access to OS features, which do the following:

1 Control the size and behavior of the app's window. 

2 Display a native toolbar on the app window with menu items.

3 Add context menus in the app window area on right-click.

4 Add a tray app item in the OS's tray menu.

5 Access the OS clipboard, read the contents, and even set the contents.

6 Open files, folders, and URLs on the computer using their default apps.

7 Insert notifications via the OS's notification system.

As you can see from the preceding list, there are a lot of things you can do within NW.js that web browsers cannot do. For example, web browsers don't have direct access to files on the desktop or the contents of the clipboard due to security restrictions that web browsers implement to protect users from sites with malicious intent. In the case of NW.js, because the app runs on the user's computer, it's granted a level of access where the user trusts the app. This means that you can do things like access the files that are on the user's computer, create new files and folders, and more. These features allow the developer to create desktop apps that fit well with the user's OS and do things that web apps can't do (or at least not as easily) — and the user trusts the app to be responsible and not do anything malicious.

USING NODE.JS AND NPM MODULES INSIDE YOUR APP

NW.js provides access to the Node.js API in the app, as well as uses modules that are installed with npm. This means that you can install npm modules for use with your desktop apps, and you can even access them and Node.js core modules from the same code that's interacting with the front end of the desktop app.

For example, you could write a bit of embedded JavaScript in the index.html file that uses the Node.js filesystem module to get a list of files and folders in a given directory, and then list those files as list items in the HTML. This shared JavaScript context between the front-end and back-end parts of the desktop app is an intriguing aspect of the way NW.js combines Node.js with Chromium. It's something to keep in mind when you're working with NW.js applications (as opposed to Electron applications). It's quite different from how web apps work, as figure 1.6 demonstrates.

Figure 1.6 The difference between a web app and an NW.js desktop app. The separation between front-end and back-end code in an NW.js desktop is blurred, as the JavaScript context is shared between both parts of the code.

To explore this a bit further, consider how traditional web apps work. Web apps tend to have a client/server model where the client requests a web page or makes an API request, and the server executes some code to then serve that data back to the client. The client in this case is a computer running a web browser. The web browser then loads the data, where, if it's HTML, the rendering engine turns it into a web page; or, if it's data like XML or JSON, the rendering engine displays it in raw form. The server does its job of executing back-end code to serve HTML pages or API requests, and the computer client running the web browser does its job of making HTML/API requests and rendering the response in the web browser. The web browser applies a strict security model to ensure that the front-end code executes within the context of the web page and nothing else. There's a clear separation of application state and responsibility.

In an NW.js app, the app window is essentially like an embedded web browser, but with the distinct difference that the code inside the web page has access to the computer's resources and can execute server-side code. There's no separation of app state and responsibility. This means you can write code that's calling out to DOM elements in the web page and executing server-side code accessing the computer's filesystem in the same place. Not only that, you'll be able to use npm modules in your code as well.

Being able to install npm modules and require them in your desktop app means you have access to over 400,000 libraries (as of January 2017) for use in your code. You'll have plenty of options when it comes to using third-party libraries in your app. In fact, both NW.js and Electron have spawned a number of dedicated libraries for use with desktop apps, all of which you'll be able to find at http://npmjs.com, and at [nw-cn/awesome-nwjs: Awesome NW.js (node-webkit)](https://github.com/nw-cn/awesome-nwjs) and [sindresorhus/awesome-electron: Useful resources for creating apps with Electron](https://github.com/sindresorhus/awesome-electron).

BUILDING YOUR APP FOR MULTIPLE OSS FROM A SINGLE CODEBASE

One of the most useful features of NW.js is that from a single codebase for your desktop app, you can build native executable apps for Windows, Mac OS, and Linux. This is a time saver when you're developing an app that has to work across multiple platforms. It also means you can have greater control over how the app looks and feels, more so than you can when trying to support a website for multiple web browsers.

The native executable is able to run on its own and doesn't require the user to have any other software installed on their computer. This makes it easy to distribute the app to users, including on stores like Apple's App store and the Steam store, where some NW.js apps and games are sold.

The process of building an app for a specific OS involves a few command-line arguments, but there are some tools that simplify the process for you, such as the nw-builder tool, illustrated in figure 1.7.

Taking an example desktop app, I'm able to use nw-builder's nwbuild command in step 1 to automate the steps of turning our desktop app's code into executable binaries for both Mac OS and Windows, as shown in step 3. This can save a lot of time (if you have to make both 32-bit and 64-bit builds of the app) and prevent mistakes when building the app.

In the next section, we'll turn our attention to Electron: how an example app works and looks with it, and what features it has.

1.3.2 NW.js 有哪些特性

NW.js 为开发者构建桌面应用提供了一些非常好用的特性。概括来说，有以下这几点：

1、一套可以创建和操作原生 UI 的 JavaScript API 以及和操作系统进行交互的 API：控制视窗、添加菜单项、托盘应用菜单、读写文件、访问剪贴板等。

2、支持在应用中使用 Node.js，也可以通过 npm 安装和使用大量的 Node.js 模块。

3、支持为同一套应用代码针对不同的操作系统构建各自可执行的文件。

接下来我会详细介绍上述每一点内容。

通过 JavaScript 访问操作系统原生的 UI 和 API

一款好的桌面应用都和用户的操作系统高度集成：与音乐相关的应用支持用户使用键盘快捷键来控制音乐的播放、聊天应用会在操作系统的托盘区域放置自己的菜单图标，以及与效率相关的应用都可能会在某个动作完成之后进行系统提示。

NW.js 提供了大量访问操作系统特性的 API，支持：1）控制应用视窗的大小和行为。2）在应用视窗中显示带菜单项的工具条。3）在用户右击的时候，在应用视窗中添加上下文菜单。4）在操作系统托盘菜单中添加应用的菜单项。5）访问操作系统的剪贴板，读写其中的内容。6）使用计算机中默认指定的应用打开文件、文件夹以及 URL。7）通过操作系统的通知系统显示通知。

如上述列表中所提到的，使用 NW.js 可以做很多 Web 浏览器不支持的事情。比方说，Web 应用不能直接访问计算机中的文件，也不能访问剪贴板上的数据，这是因为浏览器有安全限制，为了保护用户免受包含恶意内容的网站侵害。在 NW.js 中，由于应用是运行在用户计算机中的，用户等于是信任了这个应用，给予其访问计算机中资源的权限。这意味着可以做诸如访问用户计算机中的文件、创建新文件和文件夹等事情。有了这些特性，开发者们就可以开发出很好贴合用户的系统的应用，并且可以进行一些 Web 应用无法进行（至少没那么容易进行）的操作。而且用户是信任你的应用不会作恶的。

在你的应用中使用 Node.js 和 npm 应用

NW.js 支持在应用中访问 Node.js API 和通过 npm 安装的用户模块。也就是说，你可以在桌面应用中安装 npm 模块，甚至可以使用这些模块以及 Node.js 内置的核心模块，这意味着你的桌面应用代码可以同时访问前后端资源。

举例来说，你可以在 index.html 文件中嵌入一段 JavaScript 代码，这段代码使用 Node.js 的文件系统模块读取指定目录下的文件和目录信息，并且这些信息显示在 HTML 页面中。这段 JavaScript 代码之所以可以共享前后端上下文，正是由于 NW.js 整合了 Node.js 和 Chromium 后的神奇之处。当你用 NW.js 开发桌面应用的时候，这部分信息很重要，一定要牢记在心（不同于 Electron）。如图 1.6 所示，它和 Web 应用的工作机制截然不同。

图 1.6 Web 应用与 NW.js 开发的桌面应用的区别。后者，前后端代码的界限很模糊，因为同一段 JavaScript 代码共享了前后端的上下文

为了更深入地理解图 1.6，我们先来看看传统 Web 应用是怎么工作的。传统 Web 应用通常采用客户端 — 服务器模型，在这种模型中，客户端发起获取 Web 页面的请求或者 API 请求，服务器端执行一些代码并将数据返回给客户端。这里客户端指的就是运行 Web 浏览器的计算机。紧接着 Web 浏览器载入数据，如果该数据是 HTML，则渲染引擎会将它转变为 Web 页面，如果该数据是 XML 或者 JSON 形式的，渲染引擎就会直接以原生数据的形式进行显示。服务器端的职责就是执行后台代码来处理 HTML 页面请求或者 API 请求，运行着 Web 浏览器的客户端的职责就是发送 HTML/API 请求并把响应结果渲染在浏览器中。Web 浏览器遵循一套严格的安全模型来确保 JavaScript 代码只能在当前页面的上下文中被执行，不能干其他事情。在应用状态和职责之间有一个清晰的界限。

在一个 NW.js 应用中，应用视窗就像一个内嵌的 Web 浏览器，不同之处在于，Web 页面中的代码可以访问计算机上的资源，还可以执行服务器端代码。应用状态和职责的界限没有了。这就意味着，你写的代码在同一个地方既可以访问 Web 页面上的 DOM 元素，又可以执行服务器端代码访问计算机的文件系统。不仅如此，还可以在你的代码上使用 npm 模块。

可以在你的桌面应用中安装和使用 npm 模块，这意味着有超过 40 万个 npm 模块（截至 2017 年 1 月）可供使用，当要在你的应用中使用第三方库的时候选择就有很多。实际上，NW.js 和 Electron 都有一些专用库，可以访问 [nw-cn/awesome-nwjs: Awesome NW.js (node-webkit)](https://github.com/nw-cn/awesome-nwjs) 或者 [sindresorhus/awesome-electron: Useful resources for creating apps with Electron](https://github.com/sindresorhus/awesome-electron) 来找到。

同一份代码构建出支持多操作系统的应用

NW.js 提供的最有用的特性之一就是可以通过写一份代码，构建出同时支持 Windows、Mac OS 和 Linux 系统的原生可执行的桌面应用。当你要开发一款支持多平台的应用的时候，这节约了很多时间。这还意味着，在应用的样式方面相比要让一个网站支持多个 Web 浏览器时，现在可以有更好的控制。

所谓原生可执行是指不需要用户在计算机中安装额外的软件就可以将应用运行起来。这让分发应用给用户变得更加简单，包括分发到应用商店，比如，苹果的应用商店以及 Steam 商店，有些 NW.js 应用和游戏都在上面售卖。为特定的操作系统构建应用时需要用到一些命令行参数，不过有些像 nwbuilder 这样的工具可以帮助简化流程，如图 1.7 所示。

图 1.7 nw-builder 工具可以同时为 NW.js 应用构建出 Mac OS、Windows32 位和 64 位系统的原生可执行文件

拿到一个示例桌面应用，在步骤 1 中，可以使用 nw-builder 的 nwbuild 命令自动将我们的桌面应用代码变成 Mac OS 和 Windows 各自平台的可执行二进制文件，如图中第 3 步所示。这大大节约了时间（特别是你还要同时制作 32 位和 64 位版本的时候），而且还可以避免构建应用时发生错误。

接下来，我们会将注意力集中到 Electron，介绍使用 Electron 构建的应用是怎样的以及 Electron 有哪些特性。

### 1.4 Introducing Electron

Electron is a desktop app framework from GitHub. It was built for GitHub's text editor Atom and was originally known as Atom Shell. It allows you to build cross-platform desktop apps using HTML, CSS, and JavaScript. Since its release back in November 2013, it has become popular and is used by a number of startups and large businesses for their apps. Electron is used not only in Atom but also in the desktop clients of a chat app called Slack (www.slack.com), a startup that was valued at `$3.8` billion as of April 2016.

1.4 Electron 介绍

Electron 是 GitHub 开发的桌面应用开发框架。它最早的名字叫 Atom Shell，是为 GitHub 的文本编辑器 Atom 构建的。它支持使用 HTML、CSS 和 JavaScript 来构建跨平台的桌面应用。自它 2013 年 11 月发布以来，越来越流行，不少创业公司和大公司都纷纷用它来构建他们的桌面应用。不仅 Atom 在用 Electron，连聊天应用 Slack（https://www.slack.com）的桌面客户端应用也在用，这家创业公司截至 2016 年 4 月估值已达 38 亿美金。

#### 1.4.1 How does Electron work and differ from NW.js?

One of the things that Electron did differently from NW.js was the way it got Chromium and Node.js to work together. In NW.js, Chromium is patched so that Node.js and Chromium are sharing the same JavaScript context (or state, as you may call it in programming). In Electron, there's no patching of Chromium involved; instead, it's combined with Node.js through Chromium's content API and the use of Node.js's node_bindings.

The implication of this approach is that Electron works differently from NW.js in terms of how it handles JavaScript contexts. Where NW.js maintains a single shared JavaScript context, Electron has separate JavaScript contexts — one for the back-end process that kicks off running the app window (referred to as the main process), and one for each app window (referred to as the renderer process). This is an important difference between the frameworks, and one that will be elaborated on further in the book through various examples.

Another important difference between NW.js and Electron is that where NW.js usually uses an HTML file as the entry point for loading a desktop app, Electron uses a JavaScript file instead. Electron delegates the responsibility of loading an app window to code that's executed inside the JavaScript file. You'll see this in greater detail as we explore the Hello World app in Electron in the next section.

1.4.1 Electron 是如何工作的以及它和 NW.js 的区别是什么

Electron 和 NW.js 的区别之一就是整合 Chromium 和 Node.js 的方式不同。在 NW.js 中，Chromium 是直接被打补丁打进去的，因此 Node.js 和 Chromium 共享了同一个 JavaScript 上下文（或者在编程中叫「状态」）。而在 Electron 中，并不是以补丁形式将 Chromium 整合进去的，而是通过 Chromium 的 Content API 以及使用了 Node.js 的 node_bindings。

这种实现机制使得 Electron 在处理 JavaScript 上下文时和 NW.js 截然不同。NW.js 维护一个共享的 JavaScript 上下文，而 Electron 有多个独立的 JavaScript 上下文 —— 一个是后端进程负责启动运行应用的视窗（叫 main 进程），另外一个负责具体的应用视窗（叫 renderer 进程）。这是两者很重要的区别，在本书后续内容中我们会通过不同的例子来具体解释这种区别。

还有一个重要的区别就是，NW.js 通常使用 HTML 作为入口文件，而 Electron 使用的是 JavaScript 文件。Electron 将加载应用视窗的职责委派给 JavaScript 代码。这在我们接下来介绍使用 Electron 构建 Hello World 应用时会进行详细介绍。

1『解惑了，怪不得 Electron 项目是 main.js 启动的，最开始启动 nw.js 的时候拷错了，也是用 main.js 启动结果启动不了。（2021-04-12）』

#### 1.4.2 A Hello World app in Electron

Like the Hello World app in NW.js, I've also created the app that we'll run through now. If you want to boot that up and play with it, you can grab a copy of the source at http://mng.bz/u4C0.

Follow the instructions in the README.md file to get the app up and running. Alternatively, if you want to bake the cake rather than merely eat it at the end, we'll walk through that now.

Assuming that you've already installed Node.js on your computer (if not, see “Installing Node.js” in the appendix of this book), let's start by downloading a copy of Electron via npm. In your terminal or at the Command Prompt, run the following command:

```
npm install –g electron
```

This will install Electron as a global npm module, meaning that it will be available to other Node.js applications where you want to use it. Once you have installed the Electron module, we can take a look at what an example Hello World app's files consist of. Here's the bare minimum number of files required to run an Electron app: 1) index.html. 2) main.js. 3) package.json.

You can create a folder named hello-world-electron to store the app's files. Create a folder with the suggested name, and then you'll add the required files inside it.

We'll start with the package.json. Here's what an example package.json looks like:

```json
{
  "name": "hello-world",
  "version": "1.0.0",
  "main": "main.js"
}
```

You might notice that package.json looks almost identical to the package.json file used to load the Hello World app in NW.js. The only difference is that where an NW.js app's package.json field expects the main property to specify an HTML file as the app's entry point, Electron expects the main property to specify a JavaScript file.

In Electron, the JavaScript file is responsible for loading an app's windows, tray menus, and other items, as well as handling any system-level events that occur in the OS. For the Hello World example, it looks like the following.

What you can see in listing 1.2 is that where NW.js points to an HTML file in the package.json file, Electron requires a bit of code configuration to achieve the same result.

The JavaScript code looks a bit funny

If you're fairly new to Node.js and haven't touched JavaScript in a while, you may notice some new language features like the use of const and let for variable declaration, as well as => as a function shorthand. This is the next version of JavaScript, also known as ES6. It's a fairly new version of JavaScript that's now integrated into Node.js and is actively used in Electron. To learn more about ES6, you can visit [Learn ES2015 · Babel](https://babeljs.io/docs/en/learn/), [ECMAScript 6: New Features: Overview and Comparison](http://es6-features.org/#Constants), and https://es6.io/.

If you prefer the traditional style of writing JavaScript, you can continue to use it for your Electron applications. The internet is full of opinions, but that doesn't mean that you have to adopt them. My suggestion is to find what works for you and go from there.

Having created the main.js file that's the entry point to your app, you'll now create the index.html file that the main.js file loads in an app window. Create a file named index.html, and insert the code shown next.

This is the HTML file that will be loaded into the browser window by the main.js file. It's the same code that's used in the NW.js example app's index.html file (so we can compare the examples across both frameworks). With the files saved in the application folder, you can now run the app from the command line.

To execute the app from the command line, cd into the hello-world-electron directory, and run the following command:

```
electron .
```

Once you've run the command, click the Hello World button, and you can expect to see something like figure 1.8.

Figure 1.8 The Hello World example app running with Electron on Mac OS. It looks almost identical to the NW.js equivalent, except the window dimensions are different.

The app for the most part looks identical to the one running on NW.js, with a few slight differences. In figure 1.9, you can see how it looks running on OpenSUSE Linux 13.2.

The Hello World Electron example app looks a bit different from the version that runs on a Mac. This is because Mac OS handles displaying menus differently than Windows and Linux apps do. Where menus are attached to app windows on both Microsoft Windows and Linux apps, Mac OS displays a single menu in the OS's toolbar that applies to all app windows, as shown for the Hello World Electron app's Mac OS example in figure 1.10.

Figure 1.9 The Hello World example app running with Electron on OpenSUSE Linux. Notice how the app displays a menu bar with some menu items by default.

Figure 1.10 Application menu on Mac OS. The application menu for the Hello World example app uses the same default menu items.

If you open the app in Windows 10, you can expect to see a result similar to the one displayed for the Linux app example, as shown in figure 1.11.

The Hello World app with Electron and Windows 10 again looks quite similar to the app equivalents on Linux and Mac OS, minus where the application menu is displayed. The ability to write an app and have it work across three different OSs is a nice feature to have, though, and it's one of the reasons why developers have been flocking to Electron for their desktop apps.

Besides what's been shown so far, Electron has some other features to offer that make it a compelling choice, described in the next section.

Figure 1.11 The Hello World app running on Electron and Windows 10. Like the Linux app example, the Windows example displays a menu in the app window.

1.4.2 使用 Electron 开发 HelloWorld 应用

和使用 NW.js 开发 Hello World 应用一样，我也已经创建好了这个应用，现在就可以运行起来。如果你想试试，可以从 http://mng.bz/u4C0 获取到源代码。根据 README.md 文件中的说明就可以将应用运行起来。或者你想知道它是怎么实现的，而不只是看看它运行起来是怎样的，那我们就开始一步一步教你如何实现。

假设你的计算机中已经安装好了 Node.js （如果还没有，可以参看本书的附录 A），那么先通过 npm 安装 Electron。在 terminal 或者 Command Prompt 软件中，运行如下命令：

```
npm install -g electron
```

上述命令会以全局 npm 模块形式安装 Electron，这意味着其他 Node.js 应用也可以使用。安装好 Electron 模块后，我们来看看 Hello World 示例应用包含哪些文件。下面是一个 Electron 应用必要的三个文件：

```
index.html
main.js
package.json
```

你可以创建一个名为 hello-world-electron 的文件夹来存放应用文件。创建完后，把这几个必要的文件放进去。

1-3『

官方文档里快速创建 Electron 项目的操作（2021-04-12）：

```
mkdir my-electron-app && cd my-electron-app
npm init -y
npm i --save-dev electron
```

』

我们从 package.json 文件开始，来看一个例子：

```json
{
  "name": "hello-world",
  "version": "1.0.0",
  "main": "main.js"
}
```

你可能注意到了，这个 package.json 文件和用 NW.js 开发 Hello World 应用的 package.json 看上去差不多。唯一的区别在于 NW.js 应用的 package.json 文件的 main 属性需要指定一个 HTML 文件作为应用入口，而 Electron 则需要指定一个 JavaScript 文件。

在 Electron 中，这个 JavaScript 文件负责启动应用视窗、托盘菜单以及其他，除此之外还负责处理系统级别的事件。在我们的 Hello World 示例应用中，该文件如代码清单 1.2 所示。

代码清单 1.2 Electron Hello World 应用中的 main.js 文件

```js
'use strict'

const {app, BrowserWindow} = require('electron')

// mainWindow 变量保存了对应用窗口的引用
let mainWindow = null

// 监听所有的视窗关闭的事件（Mac OS 不会触发该事件）
app.on('window-all-closed', () => {
  if (process.platform !== 'darwin') app.quit()
})

app.on('ready', () => {
  // 创建一个新的应用窗口并将它赋值给 mainWindow 变量，以防止被 Node.js 进行垃圾回收时将视窗关闭
  mainWindow = new BrowserWindow()
  // 将 index.html 加载进应用视窗
  mainWindow.loadURL(`file://${__dirname}/index.html`)
  // 应用关闭时，释放 mainWindow 变量对应视窗的引用
  mainWindow.on('closed', () => {
    mainWindow =null
  })
})
```

如上述代码所示，NW.js 只要在 package.json 文件中指定一个 HTML 文件就可以了，而在 Electron 中则需要通过一点代码配置才能达到同样的效果。

JavaScript 代码看起来有点意思

如果你是 Node.js 新手或者有段时间不写 JavaScript 了，那么也许注意到了一些新的语言特性，如使用 const 和 let 进行变量声明，以及使用 => 简化函数声明。这是下一代 JavaScript，名为 ES6。这是新版本的 JavaScript，Node.js 已经对其支持并且在 Electron 中大量使用。要了解更多关于 ES6 的内容，可以参阅 [Learn ES2015 · Babel](https://babeljs.io/docs/en/learn/)、[ECMAScript 6: New Features: Overview and Comparison](http://es6-features.org/#Constants) 和 https://es6.io/。

如果你还是更喜欢写传统风格的 JavaScript 代码，也可以在开发 Electron 应用时继续使用它。互联网的世界中充满了选择，你不一定非要接受具体哪一种。我的建议是选择最适合自己的。

完成了应用入口 main.js 文件后，我们现在来创建在 main.js 文件中将其加载进应用视窗的 index.html 文件。新建一个 index.html 文件，并插入代码清单 1.3 所示的代码。

代码清单 1.3 Electron 版 Hello World 应用中的 index.html 文件

```html
<html>
  <head>
    <title>Hello World</title>
    <style>
      body {
        background-image: linear-gradient(45deg, #EAD790 0%, #EF8C53 100%);
        text-align: center;
      }

      button {
        background: rgba(0,0,0,0.40);
        box-shadow: 0px 0px 4px 0px rgba(0,0,0,0.50);
        border-radius: 8px;
        color: white;
        padding: 1em 2em;
        border: none;
        font-family: 'Roboto', sans-serif;
        font-weight: 300;
        font-size: 14pt;
        position: relative;
        top: 40%;
        cursor: pointer;
        outline: none;
      }

      button:hover {
        background: rgba(0,0,0,0.30);
      }
    </style>
    <link href='https://fonts.googleapis.com/css?family=Roboto:300' rel='stylesheet' type='text/css' />
    <script>
      function sayHello () {
        alert('Hello World');
      }
    </script>
  </head>
  <body>
    <button onclick="sayHello()">Say Hello</button>
  </body>
</html>
```

以上就是在 main.js 中被加载进浏览器视窗的 HTML 文件。这个文件的内容和 NW.js 示例中的 index.html 文件内容是一样的（因此我们可以对比这两个框架开发的示例）。在应用文件夹中保存好这个 HTML 文件后，现在就可以通过命令行运行这个应用了。

要从命令行运行应用，先 cd 进入 hello-world-electron 目录，然后执行如下命令：

```
electron .
```

运行完上述命令后，单击应用中的 Say Hello 按钮，就会看到如图 1.8 所示的界面。

1『

有个小插曲，跑步起来。发现是以为配置文件 package.json 太简单了，还是改为系统自动生成的。

```json
{
  "name": "hello-world",
  "version": "1.0.0",
  "description": "A minimal Electron application",
  "main": "main.js",
  "scripts": {
    "start": "electron ."
  },
  "repository": "https://github.com/electron/electron-quick-start",
  "keywords": [
    "Electron",
    "quick",
    "start",
    "tutorial",
    "demo"
  ],
  "author": "GitHub",
  "license": "CC0-1.0",
  "devDependencies": {
    "electron": "^12.0.2"
  }
}
```

命令 `yarn` 安装一下依赖包，然后直接命令 `yarn start` 跑起来。（2021-04-12）

』

除了一些小区别之外，应用大部分看上去都和用 NW.js 开发的差不多。图 1.9 展示了在 Open SUSE Linux 13.2 中运行的效果。

图 1.8 使用 Electron 开发的 Hello World 应用运行在 Mac OS 上的效果。除了窗口大小有点不同之外，其他都和 NW.js 开发的版本差不多

图 1.9 Electron 版 Hello World 示例应用在 OpenSUSE Linux 上的运行效果。注意图中菜单的显示方式以及默认的菜单项

Electron 版本的 Hello World 示例应用在 Windows 和 Linux 中的运行结果和 Mac OS 中有点不同。这是因为 Mac OS 显示菜单的方式和其他两个系统有所不同。在 Windows 和 Linux 上，菜单是直接显示在应用视窗中的，而 Mac OS 是在操作系统的工具条上显示了一排菜单。所有的应用菜单都是显示在这个工具条上的，图 1.10 展示了 Hello World 示例应用的菜单在 Mac 工具条上的显示。

图 1.10 Mac OS 上的应用程序菜单。Hello World 示例应用的菜单也同样是这些默认菜单项

如果用 Windows 10 打开该应用，看上去和 Linux 中的也差不多，如图 1.11 所示。

图 1.11 Electron 版 Hello World 应用在 Windows 10 中的运行效果。和 Linux 版本一样，菜单也显示在应用视窗内

除了应用菜单的显示方式不同外，Electron 版的 Hello World 应用在 Windows 10 中的显示效果和它在 Linux 以及 Mac OS 中也差不多。能够支持开发一款应用可以同时在三个操作系统上运行，这是一个很赞的特性，这也是为什么开发者都喜欢用 Electron 开发桌面应用的原因之一。

除了上述介绍的之外，Electron 还提供了其他一些有竞争力的特性，接下来为大家介绍。

#### 1.4.3 What features does Electron have?

Although Electron is relatively young, it has managed to accumulate a number of useful APIs and features for building desktop apps:

1 Creating multiple application windows with ease, each with its own JavaScript context.

2 Integrating with desktop OS features through the shell and screen APIs.

3 Tracking the power status of the computer.

4 Blocking the OS from going into power-saving mode (useful for presentation apps).

5 Creating tray apps.

6 Creating menus and menu items. 

7 Adding global keyboard shortcuts to the app.

8 Updating the app's code automatically through app updates.

9 Reporting crashes.

10 Customizing Dock menu items.

11 Operating system notifications.

12 Creating setup installers for your app.

As you can see, a lot of features are on offer, and that isn't an exhaustive list of all of the framework's features. In particular, the crash-reporting feature is unique to Electron — there's currently no equivalent to it in NW.js. Electron has also recently come up with dedicated tools for app testing and debugging, called Spectron and Devtron, covered in later chapters.

Demonstrating what Electron does and how it does it, the team behind Electron created a desktop app for demoing Electron's APIs. It's a neat way to browse through Electron's APIs in a practical fashion, and can be downloaded from http://electron .atom.io/#get-started.

A COOL WAY TO EXPLORE ELECTRON'S FEATURE SET

The next section looks at what apps can be made with NW.js and Electron.

1.4.3 Electron 有哪些特性

尽管 Electron 相对还比较「年轻」，但是它已经陆陆续续提供了一些可使用的 API 和特性用于开发桌面应用：

1、支持创建多视窗，而且每个视窗都有自己独立的 JavaScript 上下文。

2、通过 shell 和 screen API 整合了桌面操作系统的特性。

3、支持获取计算机电源状态。

4、支持阻止操作系统进入省电模式（对于演示文稿类应用非常有用）。

5、支持创建托盘应用。

6、支持创建菜单和菜单项。

7、支持为应用增加全局键盘快捷键。

8、支持通过应用更新来自动更新应用代码。

9、支持汇报程序崩溃。

10、支持自定义 Dock 菜单项。

11、支持操作系统通知。

12、支持为应用创建启动安装器。

你也看到了，Electron 支持大量特性，而上述列出来的只是其中一部分。其中，程序崩溃汇报是 Electron 独有的特性 —— NW.js 目前不支持这种特性。Electron 最近还发布了用于应用测试和调试的工具：Spectron 和 Devtron，后续章节会对它们进行介绍。

查看 Electron 特性集的好办法

为了展示 Electron 支持哪些特性以及如何使用这些特性，Electron 开发团队发布了一个用于展示 Electron API 的桌面应用。这种了解 Electron API 的方式真的很新颖，这个应用可以从 https://electron.atom.io/#get-started 进行下载。

接下来的一节我们将介绍哪些应用可以用 NW.js 和 Electron 来构建。

3『

[Electron | 使用 JavaScript，HTML 和 CSS 构建跨平台的桌面应用程序。](https://www.electronjs.org/#get-started)

[Releases · electron/electron-api-demos](https://github.com/electron/electron-api-demos/releases)

』

### 1.5 What apps can you make with NW.js and Election?

Although Electron and NW.js are relatively young in terms of software, their use in professional cases is rich and varied. On the NW.js GitHub repository, there's a long list of example apps that have been built with NW.js, and for Electron there's the Awesome Electron GitHub repository providing a long list of apps and resources at https://github.com/sindresorhus/awesome-electron. In this section, I discuss a couple of well-known examples that have been commercially successful, as well as ones that demonstrate the potential for what Electron and NW.js can do. We'll start with one of the biggest success cases for Electron: Slack.

1.5 NW.js 和 Electron 支持创建哪类应用

作为一款软件，尽管 Electron 和 NW.js 都还相对比较「年轻」，但是它们在专业领域的应用却丰富多样。在 NW.js 的 GitHub 代码仓库中，有一个很长的列表，列举了很多使用 NW.js 开发的应用。对于 Electron 来说，也有一个叫 awesome-electron 的 GitHub 仓库：[sindresorhus/awesome-electron: Useful resources for creating apps with Electron](https://github.com/sindresorhus/awesome-electron)，里面有一长串列表，提供了使用 Electron 开发的应用以及一些有用的资源。在这部分内容中，我会介绍一些知名的应用，包括一些商业上很成功的产品，也包括一些展示 Electron 和 NW.js 潜力的。首先我们从一款使用 Electron 开发的应用开始 —— Slack。

1-3『

[sindresorhus/awesome-electron: Useful resources for creating apps with Electron](https://github.com/sindresorhus/awesome-electron)

第一反应就是找资料列表里推荐的书籍：

Developing an Electron Edge - Preview

Electron in Action

Cross-Platform Desktop Applications

很赞的是第二本和第三本（本书）自己之前就下载了，说明眼光不错，哈哈。已下载书籍「2021058Electron-in-Action」、「2021044Cross-Platform-Desktop-Applications」。第一本书目前没找到。（2021-04-12）

[Developing an Electron Edge – Bleeding Edge Press](https://bleedingedgepress.com/developing-an-electron-edge/)

[adam-lynch/developing-an-electron-edge: The code examples and example apps to go along with the Developing an Electron Edge book by Adam Lynch and Max Gfeller (Bleeding Edge Press).](https://github.com/adam-lynch/developing-an-electron-edge)

』

#### 1.5.1 Slack

Slack (slack.com) is a workplace communication and collaboration tool for businesses. Slack uses Electron to provide the desktop app and is advertising jobs for desktop app engineers who have experience with using Electron. The desktop user interface (UI) is practically identical to the web app interface — a shining example of what Electron can achieve. The app has expanded its feature set to allow for audio and video calls. Figure 1.12 shows Slack in use (note, I blanked out some of the message content and channels for privacy reasons).

Slack recently expanded its offering with support for an app directory for Slack, allowing users to install third-party apps that run inside Slack. The company seems to have a good future ahead.

1.5.1 Slack

Slack（slack.com）是一款企业沟通协作工具。它的桌面客户端是用 Electron 开发的，而且还打广告招聘有 Electron 开发经验的工程师。其用户界面（UI）和 Web 版的一样 —— 充分展现了 Electron 的能力。它还支持音频和视频通话，图 1.12 展示了 Slack 使用中的样子 （注意，出于对隐私的保护，我隐藏了一些聊天内容和频道）。

图 1.12 运行在 Mac OS 上的 Slack

Slack 最近增加了一个新功能 —— 支持应用渠道，允许用户在 Slack 中安装和运行第三方应用。看来这家公司前途无量。

#### 1.5.2 Light Table

Light Table (lighttable.com) is a code editor that takes a different approach to the IDE. It was developed by Chris Granger and raised over `$300,000` through a campaign on Kickstarter. It was also the first third-party usage of NW.js and was credited with helping promote the framework in the early days of the project.

The code editor initially supported Clojure but went on to support JavaScript and Python. The philosophy behind Light Table was to rethink how to approach the task of editing code. Rather than having to think of code as lines within files, the focus should be on providing a kind of workspace in which the code is executed live, and documentation is displayed in place rather than searched for in another window, as shown in figure 1.13. It was meant to be a kind of workspace for the developer to be able to write code and see the results immediately, rather than in isolation. Originally made with NW.js, it was recently ported to Electron.

Figure 1.13 Light Table, a live interactive code editor. A 3D visualization written in JavaScript is being edited in the left-hand panel, and the results are being rendered live in the right-hand panel.

1.5.2 Light Table

Light Table（lighttable.com），这是一款代码编辑器，它和普通的 IDE 有所不同。它是由 Chris Granger 开发的，并在 Kickstarter 募集了超过 30 万美金的资金。它同时也是第一款使用了 NW.js 的第三方应用，在项目早期还帮助改进了 NW.js。

这款代码编辑器最早支持 Clojure，后来又支持了 JavaScript 和 Python。Light Table 背后的哲学就是重新思考如何进行代码的编写。不同于只是在文件中逐行编写代码，Light Table 觉得重点应该在提供一个工作空间，在里面可以即时地执行编写的代码，而且文档也是直接显示在代码旁边，而不是还要去其他窗口查询文档，如图 1.13 所示。它提供了一种工作空间，开发者在里面可以边写代码边看执行结果，两者不是独立分开的。Light Table 最早是用 NW.js 开发的，最近切换到了 Electron 上。

图 1.13 Light Table，一款在线交互式代码编辑器。图中展示了一个使用 JavaScript 编写的 3D 视觉效果，代码编辑在左侧完成，右侧直接显示渲染结果

#### 1.5.3 Game Dev Tycoon

Game Dev Tycoon is a simulation game in the spirit of old simulations like Transport Tycoon and SimCity, but in this case themed around running a game development studio (an irony, given that it was created by a game development company). Behind it is a small company called Greenheart Games, founded in July 2012 by Patrick and Daniel Klug.

The game was unique (and even more ironic) in its attempts to fight off piracy. Patrick anticipated that the game would eventually be pirated and countered this by releasing a cracked copy of the game onto Torrent sites, but with an interesting twist: people playing the game would find themselves losing in the game. As they played the game, they would find that suddenly their games would stop making money, because they were being pirated. Eventually they would go bankrupt as a result and lose. This antipiracy tactic attracted a lot of amusement and attention.

Since its founding, the company has grown to five employees, and the game is being sold on the Steam game store. Shown in figure 1.14, it's one of the best showcases for using NW.js to build a successful commercial project.

Figure 1.14 Game Dev Tycoon, a game studio simulator

Game Dev Tycoon 是一款模拟类游戏，有点像 Transport Tycoon 和 SimCity 这两款经典的模拟类游戏，不过这款游戏设计的场景是运营一个游戏开发工作室（这款游戏本身就是一家游戏开发工作室开发的，所以这个设定挺有意思）。开发这款游戏的是一家名为 Greenheart Games 的小公司，该公司由 Patrick 和 Daniel Klug 在 2012 年 7 月创立。

这款游戏非常特别（而且更具讽刺意义），它旨在反击盗版。Patrick 知道迟早这款游戏都会被盗版的，于是为了解决盗版问题，他自己先在种子下载网站发布了破解版，不过破解版中有一个很有意思的设定：玩破解版的用户最终会发现自己没法赢。因为当他们玩的时候，他们会发现游戏中自己做的游戏很快就不赚钱了，因为游戏被盗版了。最终他们游戏中的工作室会破产倒闭。这种反盗版的做法非常具有娱乐性，吸引了很多玩家。

自成立以来，这家公司现在拥有 5 名员工，而且游戏也在 Steam 游戏商店中售卖。如图 1.14 所示，这是展现使用 NW.js 开发成功商业应用最好的例子之一了。

图 1.14 Game Dev Tycoon，一款游戏工作室模拟游戏

#### 1.5.4 Gitter

Gitter is a service that provides chat rooms for open source projects on GitHub, including the official chat room for NW.js. It allows users to sign in with a GitHub account and to then access chat rooms based on projects and organizations. It's seen as a popular alternative to Slack.

As a chat service, Gitter is available both via its website (gitter.im), as well as via desktop apps for Windows and Mac OS, which are built using NW.js. The app's look and feel is an exact replica of what you see in the web app and well demonstrates the principle of code reuse. During the beta period, Gitter attracted almost 25,000 developers to the service, delivering over 1.8 million messages, and is currently hosting over 7,000 chat rooms. It now offers paid plans for chat rooms, and the company is working on getting a version of the app to run on Linux as well.

The main chat room for NW.js can be found on Gitter, a nice example of a product being used to support itself (figure 1.15).

Gitter 是一种服务，为 GitHub 上的开源项目提供聊天室功能，NW.js 项目的官方聊天室也使用 Gitter。它可以让用户使用其 GitHub 账户登录，然后访问项目或者组织的聊天室。它被视为 Slack 替代品中最受欢迎的一款。

作为聊天服务，Gitter 不仅有网页版本（gitter.im），还为 Windows 和 Mac OS 提供了桌面应用，应用开发使用的是 NW.js。桌面应用看上去以及用起来和 Web 应用简直一模一样，这也充分体现了代码复用的原则。在公测阶段，Gitter 吸引了约 25 000 名开发者，发送了 180 万条消息，而且截至目前，一共有超过 7000 间聊天室。现在它还提供了付费版的聊天室，同时公司也正在开发 Linux 版本。

NW.js 项目的聊天室可以在 Gitter 上找到，这是一个很好的例子，一款产品自己做出来自己用（参见图 1.15）。

图 1.15 Gitter，一款集成 GitHub 的聊天室客户端

#### 1.5.5 Macaw

Macaw (macaw.co) is an innovative WYSIWYG web design tool. It allows web designers to create a visual design for their websites, as they would normally do in an image editor, and generates the underlying HTML and CSS for that design. It helps eliminate the step of converting a visual design into a real website by automatically creating the website code. As a WYSIWYG web design tool, Macaw differs from predecessors like Microsoft FrontPage and Adobe Dreamweaver by outputting semantic HTML and CSS from the visual design.

Founded by Tom Giannattasio and Adam Christ, the product (figure 1.16) was funded through a Kickstarter campaign that raised over `$275,000` from more than 2,700 backers. Since March 2014, Macaw has gone on to become a product sold directly through Macaw's website.

Since I began writing the book, I'm pleased to say that Macaw was acquired by another web design application company called InVision — yet another example of a real-world desktop app becoming a success story.

Figure 1.16 features

Macaw, a WYSIWYG web design tool that lets designers create websites using visual design

Macaw（macaw.co）是一款创新的所见即所得（WYSIWYG）的 Web 设计工具。它可以让 Web 设计师直接为他们的网站做视觉设计，而以往，他们都要先在图片编辑软件中做好，然后再生成对应的 HTML 和 CSS 代码。它可以直接自动生成网站代码，省去了将视觉设计稿转成网站代码这一步。作为一款所见即所得的 Web 设计工具，Macaw 和微软的 FrontPage 以及 Adobe 的 Dreamweaver 不同，它从视觉设计稿输出的是语义化的 HTML 和 CSS 代码。

这款产品（参见图 1.16）由 Tom Giannattasio 和 Adam Christ 创建，并且通过 Kickstarter 从超过 2700 位支持者中募集了超过 275 000 美元。自 2014 年 3 月起，Macaw 开始通过其官方网站进行销售。

在开始写这本书的时候，我很高兴地获悉 Macaw 被另外一家名为 InVision 的 Web 设计应用公司收购了 —— 这又是一个桌面应用走向成功的例子。

图 1.16 Macaw，一款所见即所得的 Web 设计工具，它可以让设计师使用视觉设计的特性来制作网站

#### 1.5.6 Hyper

Hyper (hyper.is) is a minimal-looking terminal app authored by Guillermo Rauch, a well-known figure in the Node.js community for his work on the Node.js websocket library, Socket.io, and for the real-time hosting service Now. As a terminal app written in HTML, CSS, and JavaScript, Hyper is an extensible app that can be configured to look and behave in lots of different ways. Developers have created plugins (such as hyperpower) that animate the text as it's typed into the app and enable users to open URLs from within the terminal window. Figure 1.17 shows Hyper in use.

It's one of the more unique types of desktop apps reimagined with Electron and shows Electron's minimal style title bar in use.

Figure 1.17 Hyper running on Mac OS

Hyper（hyper.is）是一款极简的终端应用，作者是 Guillermo Rauch，他在 Node 社区很出名，因为著名的 Node.js websocket 库 ——Socket.io 以及实时托管服务 ——Now 都是他开发的。作为一款用 HTML、CSS 和 JavaScript 开发的终端程序，Hyper 自身可扩展，可以对其外观和功能进行定制。开发者开发了插件（如 hyperpower）可以在输入文字时增加动画效果，还能支持在终端窗口中直接打开网站链接。图 1.17 展示了使用中的 Hyper 应用。

这是一款使用 Electron 开发的非常独特的桌面应用，同时也展示了如何使用 Electron 配置极简的视窗标题条。

图 1.17 运行在 Mac OS 上的 Hyper

## 0201. Laying the foundation for your first desktop application

### Summary

In this chapter, you began using NW.js and Electron for building the type of application that many people use with their computers on a daily basis. You've walked through the process of creating the applications from scratch and understand how you can approach the task of building an application feature-by-feature. Here are some of the things the chapter covered:

1 The best way to approach a wireframe is to tackle it one feature at a time.

2 Good semantics is encouraged as a way to relate features to the underlying code that supports it.

3 CSS is the prime way to style UI elements in NW.js and Electron desktop apps. 

4 You can use Node.js and other third-party libraries with ease in your desktop application.

5 The approaches of NW.js and Electron allow for them to use almost the same code, but Electron requires a bit more code and a slightly different configuration in the package.json file.

What's been great is that in using the same code across both NW.js and Electron variants of the Lorikeet app, you've been able to see how similar the desktop application frameworks are, as well as notice the areas where they're different. This should give you the confidence that should you choose one framework for your application and find that it's not the right one for you, then it won't be too difficult to switch to using the other framework.

Another takeaway here is that you're able to use the same skills for building websites as for creating the UI for a desktop application, and that means getting up to speed quickly when building a desktop application.

In the next chapter, we'll expand on the work done here by adding the meaty parts of the application. We'll begin to explore the APIs of NW.js and Electron to add features such as browsing through folders, searching the files and folders by name, and opening files.

在本章中，我们介绍了使用 NW.js 和 Electron 构建一款许多人都会在他们的计算机中使用的应用。还从头开始介绍了构建一款应用的流程以及如何逐个实现应用的功能。下面是本章介绍过的内容：

1、实现线框图最好的办法是，一个功能一个功能地去实现。

2、具备良好语义的代码可以更好地表达它要实现的功能。

3、在 NW.js 和 Electron 应用中，CSS 是主要定义界面元素样式的方式。

4、在你的桌面应用中使用 Node.js 以及其他第三方库是非常容易的。

5、由于 NW.js 和 Electron 的实现思路，它们互相之间可以共享代码，不过在 package.json 配置文件方面，Electron 会要求更多的代码，稍微有一些区别。

最棒的就是，对于 NW.js 和 Electron 版的 Lorikeet 应用，它们可以使用同样的代码，你也看到了使用这两个框架构建出来的应用是多么相似，当然你也留意到了它们不同的部分。这就意味着，就算此前你为你的应用所选择的框架是错误的，切换到另外一个框架也不是什么难事。

还值得一提的是，你可以用构建 Web 网站的技术去构建桌面应用的界面，这就意味着可以很快地构建桌面应用。在下一章中，我们会继续扩展本章中的应用，增加更实用的功能。我们将会介绍 NW.js 和 Electron 的 API，并使用它们实现诸如浏览文件夹内容、通过名字查询文件和文件夹，以及打开文件这样的功能。

### 2.0

This chapter covers: 1) Building a file explorer in both NW.js and Electron. 2) Setting up your application. 3) Structuring your application's files. 4) Understanding how the user interface of the application works. 5) Accessing the filesystem in Node.js.

As developers, we often forget how lucky we are to work in an industry where the tools are readily available and free or relatively inexpensive to get ahold of. In this chapter, we'll get to grips with building desktop applications through creating a file explorer application. We'll look at how the app is built with both NW.js and Electron so that we can compare and contrast the ways in which they approach desktop applications.

Grab a cup of tea or coffee, a pen and paper, and settle in for some programming.

为你的首款桌面应用搭建基础架构

本章要点：1）使用 NW.js 和 Electron 分别构建一个文件浏览器应用。2）对应用进行设置。3）组织应用程序文件。4）理解应用界面的工作原理。5）使用 Node.js 访问文件系统。

作为开发者，我们经常会忘却自己身处在一个这样幸福的环境中：许多工具都是现成的，可以免费或者以相对较低的成本就能够获取到。在本章中，我们将会通过构建一个文件浏览器应用了解如何构建桌面应用。我们会用 NW.js 和 Electron 分别构建同一个应用，从而来比较使用这两个框架在构建桌面应用时有何异同。

准备一杯茶或者咖啡、一支笔、一张纸，我们这就开始编程吧。

### 2.1 What we're going to build

Whether you use a Windows PC, a Mac, or Linux, there are a few things common to all of them — they store files organized in folders, and they all have their own take on how to organize files in folders, as well as how you find and display those files to the user. This isn't a problem for people who use only one OS, but those who have to learn to use a new OS (such as when going to work at a new organization) can struggle to get their head around how to do simple tasks like rename a folder, or find out where the file that they saved to their computer is located.

It feels fitting to approach the idea of making a file explorer that works the same across all OSs, so that's what we'll build: a file explorer.

2.1 我们将构建什么应用

不论你用的是 Windows 或者 Mac 又或者是 Linux，它们都有一些共同之处 —— 它们都以文件夹的形式来组织文件，都有各自组织文件的方式，以及都有如何查询和显示那些文件给用户的方法。这对于只用一种操作系统的人来说不是什么问题，但对那些还得学用新系统的人（比如到了新的工作环境时）而言，诸如如何对文件夹进行重命名、如何找到保存在计算机中的文件这样简单的操作都可能会让他们头痛不已。

这样看来，做一款跨系统的文件浏览器是一个不错的主意，是的，没错，这正是我们准备要做的：一款文件浏览器应用。

#### 2.1.1 Introducing Lorikeet, the file explorer

There's a common joke in developer circles that says naming things is the second hard problem in computer science (caching being the first hard problem). Sometimes it's nice to take inspiration from nature, so we'll name the file explorer Lorikeet, after the colorful native Australian bird.

Lorikeet is a file explorer with the following goals: 1) Allow users to browse folders and find files. 2) Allow users to open the file(s) with their default app.

These are relatively simple goals, but implementing features to support them will provide enough scope to help you become familiar with building a desktop application. Building Lorikeet will also help demonstrate the different approaches that NW.js and Electron offer for developing desktop applications.

Building a desktop application is a lengthy process consisting of many steps: constructing user journeys, creating wireframes, writing tests, fleshing out the wireframes, writing code, and making sure that the app works as intended. For the sake of learning about NW.js and Electron, we'll work off of the basis that we have some user journeys and wireframes for the file explorer and focus on building a functional version of it.

You'll flesh out the features in the wireframes one by one, which helps to provide a natural flow to building the app, and gives you a chance to see where the code lives and what it does. Figure 2.1 shows a wireframe.

Figure 2.1 Wireframe of the file explorer app you'll build

With this wireframe, you take the app and break it down into separate features, helping you to implement the app one feature at a time. The first feature to work on is where the user begins to use the app — in this case, the start screen. But before you can do that, you need to create an app to store the code in.

文件浏览器 —— Lorikeet 介绍

程序员界有一个从熟知的玩笑是这样说的：命名是计算机科学中第二难的事情（缓存是头等难题）。有时候，从大自然获取灵感是很不错的思路，所以我们将这款文件浏览器命名为 Lorikeet，来源于澳大利亚的一种漂亮的小鹦鹉。

Lorikeet 这款文件浏览器将具备以下功能：1）用户浏览文件夹和查找文件。2）用户可以使用默认的应用程序打开文件。

尽管这些功能听上去很简单，但要实现它们需要大量的相关技术知识，这将帮助你熟悉如何构建一个桌面应用。构建 Lorikeet 的过程中也会展示 NW.js 和 Electron 在开发桌面应用方面的异同之处。

构建一个桌面应用工序繁杂：构建用户使用路径、创建线框图、编写测试、更新线框图、编码、确认应用工作正确。考虑到以学习 NW.js 和 Electron 为主，我们不介绍如何构建用户路径以及线框图这些基本的东西，关注在构建一个可用的版本。

线框图会随着功能的增加相应地进行修改，这有助于你了解真实情况下构建应用的流程，也能让你明白具体代码的作用。图 2.1 展示了线框图。

根据这个线框图，我们将应用划分为几个功能，这样有助于我们逐个功能地去实现。首先我们要实现的功能是用户使用应用的入口 —— 在本例中就是我们的启动界面。不过在动手做之前，先得创建应用来存放代码。

图 2.1 即将构建的文件浏览器应用的线框图

### 2.2 Creating the app

As you saw in chapter 1, it's relatively easy to get started with creating desktop applications with either NW.js or Electron. Regardless of which framework you begin to build the app with, you'll need to have Node.js installed (a quick and simple process you can do in a minute). To see how to install Node.js on your computer, see “Installing Node.js” in the appendix.

Once you have Node.js installed on your computer, the next step is to install both of the desktop application frameworks on your computer (if you haven't already).

2.2 创建应用

如第 1 章中所介绍的，不论是用 NW.js 或是 Electron，创建一个桌面应用都是比较简单的。不管你用哪个框架构建应用，都需要先安装 Node.js （这非常容易，1 分钟就可装完）。要了解如何在你的计算机中安装 Node.js，可以参见附录 A。安装好 Node.js 后，接下来就要在你的计算机中安装桌面应用开发框架了（如果你还没有安装的话）。

#### 2.2.1 Installing NW.js and Electron

If you've already installed NW.js and Electron as explained in chapter 1, please skip to section 2.2.2. If not, you can run the following commands in the Terminal. For NW.js, run the following command to install NW.js as a global module:

```
npm install -g nw
```

For Electron, run the following command to install Electron as a global module:

```
npm install -g electron
```

Once they're installed, you can proceed to build the NW.js version of the Lorikeet application.

2.2.1 安装 NW.js 和 Electron

如果像第 1 章介绍的那样，你已经安装好了 NW.js 和 Electron，那请直接跳至 2.2.2 节。如果还没有，你可以在终端程序中运行如下命令。对于 NW.js，运行如下命令来全局安装 NW.js：

```
npm install -g nw
```

对于 Electron，运行如下命令来全局安装 Electron：

```
npm install -g electron
```

安装好之后，我们开始用 NW.js 来构建 NW.js 版本的 Lorikeet 应用。

#### 2.2.2 Creating the files and folders for the NW.js-powered app

The next step is to create a folder that will store the code for your app. Choose a location on your computer where you like to store your code work, and run the following command to create a folder named lorikeet-nwjs:

```
mkdir lorikeet-nwjs
```

Once the folder (or directory, as some developers call it) is created, the next step is to create a package.json file for the app. This is Node.js's equivalent of a manifest file, where you store configuration information for the app. First, create the file inside the application folder:

```
cd lorikeet-nwjs touch package.json
```

Running on Windows?

If so, there isn't a touch command. What you can do instead is simply create the file using a code editor such as Notepad++ or even GitHub's Atom.

Now that you have a package.json file that you can edit, you can use whatever text editor you like to open the package.json file and insert the following code into it:

The package.json file follows the same conventions used for creating modules that are then used in Node.js applications via npm. The name field has the name of the application, and must not contain spaces. The version field contains the version of the software, which we call 1.0.0 in accordance with a versioning format known as semantic versioning (also known as SemVer). The main field is used to tell NW.js what file to load when it's booted — in this case, the index.html file. These are the minimum requirements that NW.js has for the package.json file before it can load an application. You haven't yet created the web page that's loaded by NW.js, so you should probably create that next.

The index.html file is a pretty standard example for the moment. To create it, run the following command in your command-line tool (or create the file with Notepad++/Atom in Windows):

```
touch index.html
```

Once that's done, using your favorite text editor, insert the code in the following listing into the index.html file.

Listing 2.1

Adding the index.html file's contents for the NW.js app

```html
<html> 
  <head> 
    <title>Lorikeet</title> 
  </head> 
  <body> 
    <h1>Welcome to Lorikeet</h1> 
  </body> 
</html>
```

Now that the index.html file is created, you're in a position to make NW.js run the app. To do that, simply run the following command in the Terminal, or your Command Prompt/PowerShell in Windows:

This will load the NW.js app. Because no further arguments were passed to the command, NW.js will inspect the files located in the current working directory where the command was run (in this case, the lorikeet-nwjs folder) and search for a package.json file. When it finds the package.json file, it will then load that file. The package.json file's main field will indicate to NW.js to load the index.html file in the app, which it then does, and you should see the screen shown in figure 2.2.

Figure 2.2 NW.js running a bare-minimum app. The app displays the contents of the index.html file, which means it's working as expected so far. Later in the chapter, you'll replace this simple HTML with the UI that makes up the app.

The title of the app window is loaded from the value inside the `<title>` element in the index.html file. You can edit the value of that field, save the change to the file, and run the application again from the command line to see the changes.

Can I load the index.html file in a web browser?

You can try, but any code that's calling out to NW.js's APIs or to Node.js code will result in a JavaScript error, so it's best not to. Even though NW.js apps appear to be running inside an embedded web browser, the app is more sophisticated because it has access to both Node.js/NW.js APIs and the DOM in the same JavaScript context.

With one folder and two files in that folder, you have the main skeleton code that will get a bare-bones version of the application up and running. At this point, you can adjust the contents of the index.html file to change the UI that's displayed by the application, but before you do any more on the NW.js version of the application, let's take a look at how you can achieve the same bare-bones application version with Electron.

2.2.2 为 NW.js 版本的应用创建文件和文件夹

接下来，为应用创建一个文件夹来存放代码。在你的计算机中选择一个你喜欢存放代码的位置，运行如下命令创建一个名为 lorikeet-nwjs 的文件夹：

```
mkdir lorikeet-nwjs
```

文件夹（有些开发者称之为「目录」）创建好后，接下来为应用创建 package. json 文件。在 Node.js 中，这和 manifest 文件一样，用来保存应用的配置信息。首先，在应用文件夹中创建一个文件：

```
cd lorikeet-nwjs
touch package.js
```

在 Windows 上运行

如果你用的是 Windows，那么是没有 touch 命令的。你可以用诸如 Notepad++ 或者 GitHub 的 Atom 代码编辑器来创建文件。

现在可以为 package.json 文件添加内容了，你可以用你喜欢的文本编辑器打开 package.json 文件，并插入如下内容：

这里的 package.json 文件和在 Node.js 应用中创建 npm 模块时一样，遵循同样的规则。name 字段表示应用的名字，不能包含空格。version 字段表示应用的版本号，本例中是 1.0.0，版本号命名规则遵循语义化版本（大家熟知的 SemVer）。main 字段表示了 NW.js 需要加载的应用启动文件 —— 本例中为 index.html 文件。要让 NW.js 启动应用程序，至少要在 package.json 文件中包含以上这些字段。接下来我们来创建 NW.js 需要加载的 Web 页面。

一般我们会将页面命名为 index.html 文件。使用命令行工具（或者在 Windows 系统中使用 Notepad++ 或者 Atom）运行如下命令即可创建：

```
touch index.html
```

完成后，使用你喜欢的文本编辑器，将代码清单 2.1 中的内容插入 index.html 文件。

代码清单 2.1 为 NW.js 应用添加 index.html 文件内容

现在 index.html 文件创建好了，接下来要让 NW.js 将应用程序运行起来。这很简单，只要在终端、Windows 系统中的命令提示符下或者 PowerShell 中运行如下命令即可：

```
nw .
```

该命令会加载 NW.js 应用。如果没有为该命令指定任何参数，NW.js 就会在执行上述命令所在的当前工作目录中（本例中就是 lorikeet-nwjs 文件夹）查找 package. json 文件。找到 package.json 文件后，就会加载该文件。package.json 中的 main 字段会告诉 NW.js 去加载应用中的 index.html 文件，加载完成后就会看到图 2.2 所示的界面。

图 2.2 NW.js 正在运行一个很简单的应用。应用显示了 index.html 文件的内容，意味着目前为止工作正常。在本章后续部分，我们会将这个简单的 HTML 替换为应用所需的 UI

视窗的标题是通过 index.html 页面中的 `<title>` 标签中的内容指定的。你可以编辑该字段值，保存文件，并从命令行再次运行应用来查看修改后的效果。

我可以通过 Web 浏览器加载 index.html 文件吗

你可以试试，但是任何使用了 NW.js API 以及 Node.js 代码的都会导致 JavaScript 错误，所以最好还是不要这样操作。尽管 NW.js 应用看起来是运行在一个内嵌的 Web 浏览器中的，不过它本身复杂得多，因为它在同一个 JavaScript 上下文中既访问了 Node.js/NW.js API，又访问了 DOM。

有了一个文件夹和其中的两个文件，就拥有了最主要的基础代码，可以让一个最简单的应用运行起来了。接下来，可以修改 index.html 文件内容来改变应用的 UI，不过在动手进一步修改这个 NW.js 版本的应用前，让我们先来使用 Electron 创建一个同样的最简单的应用。

#### 2.2.3 Creating the files and folders for the Electron-powered app

The Electron version of the application starts off very much in the same fashion. You'll begin by creating a folder named lorikeet-electron. You can do this by running this command in the Terminal/Command Prompt:

```
mkdir lorikeet-electron
```

This will create a folder named lorikeet-electron. This is the main application folder for the application, and inside it will be the application's files. Now you'll create the next file needed by the application, the package.json file. In your terminal or via your text editor, create a file named package.json inside the lorikeet-electron folder:

```
cd lorikeet-electron touch package.json
```

Once you have an empty package.json file, you'll move on to populating the file with the configuration needed by Electron. Inside the package.json file, add the following JSON configuration:

1『

在自动生成的配置上修改后的：

```
{
  "name": "lorikeet-electron",
  "version": "1.0.0",
  "description": "",
  "main": "main.js",
  "scripts": {
    "start": "electron .",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "electron": "^12.0.2"
  }
}
```

修改的地方：`"main": "main.js"` 以及 `"start": "electron ."`。（2021-04-12）

』

The package.json file looks almost identical to the package.json file used by the NW.js version of the application, with one exception: the main property is different. In NW.js, the file that's loaded is an HTML file. In Electron, the file that's loaded is a JavaScript file. The file you load in the case of the Electron version of the application is called main.js.

The main.js file is responsible for loading the Electron application and any browser windows that it will display as part of that application. In your terminal or your text editor, create the file main.js and insert the following content.

```js
'use strict'

const {app, BrowserWindow} = require('electron')

// mainWindow 变量保存了对应用窗口的引用
let mainWindow = null

// 监听所有的视窗关闭的事件（Mac OS 不会触发该事件）
app.on('window-all-closed', () => {
  if (process.platform !== 'darwin') app.quit()
})

app.on('ready', () => {
  // 创建一个新的应用窗口并将它赋值给 mainWindow 变量，以防止被 Node.js 进行垃圾回收时将视窗关闭
  mainWindow = new BrowserWindow()
  // 将 index.html 加载进应用视窗
  mainWindow.loadURL(`file://${__dirname}/index.html`)
  // 应用关闭时，释放 mainWindow 变量对应视窗的引用
  mainWindow.on('closed', () => {
    mainWindow =null
  })
})
```

The main.js file will result in loading the index.html file. Here, you create the index.html file and put the following contents into it:

```html
<html> 
  <head> 
    <title>Lorikeet</title> 
  </head> 
  <body> 
    <h1>Welcome to Lorikeet</h1> 
  </body> 
</html>
```

Once you've saved the index.html file, you're in a position to run the Electron application from the command line. Go to the Terminal or Command Prompt and type the following command inside the lorikeet-electron folder to run the application:

```
cd lorikeet-electron 
electron .
```

If you run the application now, you should see something like figure 2.3.

Figure 2.3 The Lorikeet app running on Electron. This is what Electron apps look like by default — pretty much like the NW.js variant.

The Electron app looks almost identical to the NW.js app. The index.html file is exactly the same as the one used for the NW.js variant of the Lorikeet app, and to load the application from the command line is practically the same.

Having built the Lorikeet app's bare-bones application structure in both NW.js and Electron, you can see that they share some similar coding conventions — after all, as mentioned, Cheng Zhao worked on both NW.js and Electron. But they differ in terms of how they go about loading the app.

So far, I've shown you how to build and set up the Lorikeet app's skeleton of files and folders with both frameworks. The next stage is to start working on the first feature of the application that the user sees, as shown back in figure 2.1.

We'll continue to compare and contrast the approaches taken with both frameworks but share code where it's possible.

2.2.3 为 Electron 版本的应用创建文件和文件夹

创建 Electron 版的应用的步骤与用 NW.js 创建的非常相似。首先创建一个 lorikeet-electron 文件夹。可以在终端程序或者命令提示符应用中运行如下命令进行创建：

```
mkdir lorikeet-electron
```

上述命令会创建一个名为 lorikeet-electron 的文件夹。这是应用程序的主文件夹，在该文件夹中放置应用文件。接下来，创建应用所需的 package.json 文件。使用你的终端应用或者文本编辑器，在 lorikeet-electron 文件夹中创建一个名为 package. json 的文件：

```
cd lorikeet-electron
touch package.json
```

有了空的 package.json 文件后，接下来为该文件添加 Electron 应用所需的配置信息。在 package.json 文件中添加如下 JSON 格式的配置信息：

这里的 package.json 文件和 NW.js 版本所用的 package.json 文件大致相同，除了 main 属性有所不同。在 NW.js 中需要指定一个 HTML 文件。而在 Electron 中，则是一个 JavaScript 文件。在本例中，该文件为 main.js。

main.js 文件负责加载 Electron 应用以及任何应用所需的浏览器视窗。使用你的终端应用或者编辑器，创建 main.js 文件并插入代码清单 2.2 中的内容。

代码清单 2.2 Electron 版应用的 main.js 文件

main.js 文件最终会加载 index.html 文件。所以，创建 index.html 文件，并插入如下内容：

保存 index.html 文件后，就可以从命令行运行 Electron 应用了。在 lorikeetelectron 文件夹中使用终端应用或者命令提示符应用，输入如下命令来运行应用：

```
cd lorikeet-electron
electron .
```

运行后会看到如图 2.3 所示的样子。

Electron 版的应用和 NW.js 版的应用非常相似。其中 index.html 文件和 NW.js 版的完全一样，而且从命令行加载应用的方式也完全一致。

图 2.3 Electron 版的 Lorikeet 应用。这是 Electron 应用默认的样子 —— 和 NW.js 版的非常相似

使用 NW.js 和 Electron 构建了最简单的 Lorikeet 应用后，你可以发现它们有相同的编码规范 —— 值得一提的是，毕竟赵成在 NW.js 和 Electron 项目上都参与过开发。不过它们加载应用的方式有所不同。

至此，我已经给大家展示了如何使用两个框架构建最简单的 Lorikeet 应用。如此前图 2.1 所示，接下里我们开始实现应用的第一个功能。

在实现过程中，我们还会继续比较两个框架的异同，必要的时候也还会复用代码。

### 2.3 Implementing the start screen

The start screen has a number of components to it. We'll start with the display of the personal folder, as shown in figure 2.4.

Figure 2.4 The Lorikeet wireframe. Notice the circled item in the wireframe. This is the item you want to build first.

This is the first feature you'll flesh out in the UI and then implement in both versions of the Lorikeet app.

2.3 实现启动界面

启动界面由几个部分组成。我们先从展示用户个人文件夹信息开始，如图 2.4 所示。

图 2.4 Lorikeet 线框图。注意其中画圈的部分，我们先来实现这部分

这是我们要实现的第一个功能，会在两个版本的 Lorikeet 应用中都进行实现。

#### 2.3.1 Displaying the user's personal folder in the toolbar

Three parts comprise this feature:

1 The HTML that makes up the toolbar and the personal folder.

2 The CSS that applies the layout and styling of the toolbar and the personal folder.

3 The JavaScript that will discover what the user's personal folder is and display it in the UI.

The good news is that the HTML, CSS, and even the JavaScript needed for this feature are exactly the same in both the NW.js and Electron versions of the Lorikeet app. In this case, you'll be able to show it once but use the same code in both applications. Let's start with the HTML.

ADDING THE HTML FOR THE TOOLBAR AND PERSONAL FOLDER

The index.html file is the main screen for both the NW.js and Electron versions of our applications. For both versions of the application, open the index.html file in a text editor and change it to what you see in the next listing.

Once you've done this for both applications, we can move on to creating the CSS stylesheets that will manage the layout and styling of the toolbar and personal folder.

ADDING THE CSS FOR THE TOOLBAR AND PERSONAL FOLDER

Styling desktop applications is no different than styling web pages. CSS can be embedded inside the HTML for a page, but it's better to put it into a separate file so that you can see all the CSS styling in one place, as well as keep the index.html file readable.

Start by creating a file in the application called app.css at the same folder level as the index.html file. Next, add the CSS in the following listing to the app.css file.

Listing 2.4 Adding the toolbar and personal folder CSS to the app.css file

Now, you need to make sure that the app.css file will be loaded by the index.html file. In the index.html file, add a line to the index.html file so that it reads like the following listing.

After you've saved the index.html file with this change, you can either reload the NW.js and Electron applications (if you have them open and running) or load them again from the Terminal/Command Prompt with this:

cd lorikeet-electron && electron . cd lorikeet-nwjs && nw

Once you have reloaded the applications with the new code, you'll see that the UI is starting to take shape, as shown in figures 2.5 and 2.6.

Figure 2.5 The Lorikeet NW.js app with the toolbar and personal folder. The personal folder listing is blank, but we'll get around to making it appear soon.

Figure 2.6

The Lorikeet Electron app with the toolbar and personal folder

The toolbar and the personal folder are visible and styled, but what remains is to be able to discover what the path for the user's personal folder is and display that in the UI. This is the next step we'll take.

DISCOVERING THE USER'S PERSONAL FOLDER WITH NODE.JS

To display the path of the user's personal folder, you need a way to discover it, one that works across all OSs. On Mac OS, the user's personal folder tends to be located in the /Users/<username> folder with their username (mine is /Users/pauljensen). On Linux, the user's personal folder tends to be in the /home/<username> folder, and on Windows 10 the it's located in the C: drive under the Users/<username> folder. If only OSs operated in a common, standard fashion!

Thankfully, this is accommodated in Node.js's ecosystem on npm packages. An npm module called osenv by Isaac Schlueter (former Node.js lead maintainer and the founder of npm) has a function that discovers and returns the user's personal folder (or home folder, as it's also known). To use this, you need to install the npm module in the application. Run the following command in the Terminal or Command Prompt to install the library (make sure to do this for both versions of the Lorikeet app):

```
npm install osenv --save
```

The –-save flag at the end of the command tells the npm command to add the module as a dependency in the package.json manifest file. If you open the package.json manifest file (say, in this case, for the NW.js variant of the application), you'll see the change, as shown next.

Listing 2.6

The modified package.json file

```
{

"name": "lorikeet", "version": "1.0.0", "main": "index.html", "dependencies": { "osenv": "^0.1.3" }

The new dependencies property, with osenv listed as module dependency for app

}
```

You'll also notice that there's a new folder that appears in the application folders for both applications, a folder called node_modules. This folder contains any locally installed npm modules that are installed for the application. If you browse the node_modules folder, you'll see a folder named osenv. This is where the osenv module's code has been installed.

With the osenv module installed, you now want to load the user's personal folder and display it in the personal folder UI element in the index.html file. This demonstrates one of the unique aspects of NW.js and Electron as Node.js desktop application frameworks: you can execute Node.js code directly in the index.html file. Don't believe me? Try this. Modify the index.html file so that the code looks like the next listing.

Listing 2.7

Displaying the user's personal folder to the index.html file

Make sure the index.html file is changed to this in both the NW.js and Electron versions of the Lorikeet app.

After you save the files, reload the applications using the technique shown earlier:

cd lorikeet-electron && electron . cd lorikeet-nwjs && nw

You can expect to see your personal folder listed in the personal folder UI element of the app, as shown in figures 2.7 and 2.8.

Figure 2.7 NW.js app

The user's personal folder displayed in the Lorikeet

Figure 2.7 is impressive. You can call Node.js directly in a script tag in the index.html file. How about Electron? Does it do the same? Check out figure 2.8.

Figure 2.8

The user's personal folder displayed in the Lorikeet Electron app

It does. Not only have you been able to call Node.js code inside a script tag in the index.html file, but you've been able to use a Node.js module from npm in the frontend part of your code. Plus, you've been able to use identical code across both NW.js and Electron so far, which goes to show how compatible they are, as well as why some projects have been so successful in being ported from NW.js to Electron (such as Light Table, for example).

Now that you've implemented the display of the user's personal folder in the toolbar, we should move on to implementing the next feature in the UI: the display of the user's files and folders in their personal folder.

2.3.1 在工具条中展示用户个人文件夹信息

实现该功能可分为三部分内容：1）HTML 负责构建工具条和用户个人文件夹信息。2）CSS 负责布局工具条和用户个人文件夹展示上的布局以及样式。3）JavaScript 负责找到用户个人文件夹信息在哪里并在 UI 上展示出来。

好在实现这个功能所用到的 HTML、CSS 和 JavaScript 内容在 NW.js 版本和 Electron 版本的 Lorikeet 应用中是一样的。在本例中，你将能够展示一次这部分代码，但在两个版本的应用中使用的是相同的代码。让我们从 HTML 代码开始。

添加展示工具条和个人文件夹的 HTML 代码

index.html 是用于展示我们 NW.js 和 Electron 两个版本应用的主屏幕。在文本编辑器中打开两个版本应用中的 index.html 文件，并将内容改为代码清单 2.3 所示的那样。

代码清单 2.3 在 index.html 文件中添加展示工具条和与用户个人文件夹信息相关的内容

```html
<html> 
  <head> 
    <title>Lorikeet</title> 
  </head> 
  <body> 
    <div id="toolbar">
      <div id="current-folder"></div>
    </div>
  </body> 
</html>
```

在两个版本的应用中都修改完成后，我们来创建 CSS 代码来控制工具条和用户个人文件夹信息展示时候的布局和样式。

为工具条和用户个人文件夹信息添加 CSS 代码

为桌面应用添加样式和为 Web 页面添加样式没什么区别。CSS 可以直接内嵌在页面的 HTML 中，不过最好还是把它放在另外一个单独的文件中，这样既可以在同一个地方看到所有的 CSS 代码，也可以保持 index.html 的可读性。

我们先来创建一个名为 app.css 的文件，将其放在存放 index.html 文件的目录中。然后，将代码清单 2.4 中的内容插入 app.css 文件。

```css
body {
  padding: 0;
  margin: 0;
  font-family: 'Helvetica', 'Arial', 'sans';
}

#toolbar {
  position: absolute;
  background: red;
  width: 100%;
  padding: 1em;
}

#current {
  float: left;
  color: white;
  background: rgba(0, 0, 0, 0.2);
  padding: 0.5em 1em;
  min-width: 10em;
  border-radius: 0.2em;
}
```

代码清单 2.4 在用于工具条和用户个人信息的 CSS 代码添加到 app.css 文件中

现在要确保 app.css 文件会被 index.html 文件加载。在 index.html 文件中，如代码清单 2.5 所示添加一行代码。

代码清单 2.5 在 index.html 文件中添加一个 link 标签，指向 app.css 文件

```html
<html> 
  <head> 
    <title>Lorikeet</title> 
    <link rel="stylesheet" href="app.css">
  </head> 
  <body> 
    <div id="toolbar">
      <div id="current-folder"></div>
    </div>
  </body> 
</html>
```

保存修改完的 index.html 文件，接下来你可以重新加载 NW.js 和 Electron 版应用（如果已经在运行了的话）或者从终端应用或者命令提示符应用输入如下命令再次运行：

```
cd lorikeet-electron && electron .
cd lorikeet-nwjs && nw
```

使用最新代码重新运行后，你会看到界面发生了变化，如图 2.5 和图 2.6 所示。

图 2.5 NW.js 版本的 Lorikeet 应用，包含了一个工具条和用户个人文件夹信息。其中用户个人文件夹信息还是空白的，不过我们很快就会让它显示内容

图 2.6 Electron 版的 Lorikeet 应用，包含了工具条和用户个人文件夹信息

工具条和用户个人文件夹信息都显示出来了，而且也有指定的样式，不过还需要找到用户个人文件夹的路径并将其显示在界面上。这部分内容接下来会做介绍。

通过 Node.js 找到用户个人文件夹所在的路径

要显示用户个人文件夹的路径，我们先得想办法获取到该路径，而且该方法要支持所有操作系统。在 Mac OS 中，用户个人文件夹位于 `/Users/<username>`，这里 username 是用户名（我的是 `/Users/pauljensen`）。在 Linux 中，用户个人文件夹位于 `/home/<username>`，在 Windows 10 中，则位于 C 盘的 `/Users/<username>`。不同操作系统位置不同！

幸运的是，这个问题已经在 Node.js 生态中通过 npm 模块解决了。有一个 Isaac Schlueter （前 Node.js 维护者以及 npm 作者）开发的模块，叫 osenv，其中有一个函数会返回用户个人文件夹（或者叫 home 目录）。要使用该模块，你需要先在应用中安装它，在终端应用或者命令提示符应用中运行如下命令可进行安装（别忘了在两个版本的 Lorikeet 应用中都执行如下命令）：

```
npm install osenv --save
```

1『

改用：`yarn add osenv --save`。（2021-04-12）

```json
{
  "name": "lorikeet-electron",
  "version": "1.0.0",
  "description": "",
  "main": "main.js",
  "scripts": {
    "start": "electron .",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "electron": "^12.0.2"
  },
  "dependencies": {
    "osenv": "^0.1.5"
  }
}
```

』

命令最后的 `--save` 标志是告诉 npm 将该模块作为依赖的模块添加到 package. json 文件中。如果你打开 package.json 文件（以 NW.js 版本的应用为例），就会看到其内容发生了改变，如代码清单 2.6 所示。

代码清单 2.6 修改后的 package.json 文件

你还会发现在两个版本的应用文件夹下都多了一个新的名为 `node_modules` 的文件夹。所有为应用安装的本地 npm 模块都会放在这个文件夹中。如果打开 `node_modules` 文件夹，就会看到一个名为 osenv 的文件夹，这就是 osenv 模块安装的位置。

安装好 osenv 模块后，我们就可以找到用户个人文件夹并将其信息在 index.html 文件中对应的界面上显示出来。这也证明了 NW.js 和 Electron 作为 Node.js 桌面应用开发框架独特的功能之一：可以在 index.html 文件中直接执行 Node.js 代码。不信？那就试试吧。将 index.html 文件修改为代码清单 2.7 所示的内容。

代码清单 2.7 在 index.html 文件中显示用户个人文件夹信息

```html
<html> 
  <head> 
    <title>Lorikeet</title> 
    <link rel="stylesheet" href="app.css">
  </head> 
  <body> 
    <div id="toolbar">
      <div id="current-folder">
        <script>
          document.write(require('osenv').home())
        </script>
      </div>
    </div>
  </body> 
</html>
```

确保 NW.js 和 Electron 版的 Lorikeet 应用的 index.html 都修改了。保存修改后，根据此前介绍过的，运行如下命令重新启动应用：

```
cd lorikeet-electron && electron .

cd lorikeet-nwjs && nw
```

现在应该能看到你的个人文件夹信息已经显示在应用中对应的界面上了，如图 2.7 和图 2.8 所示。

图 2.7 NW.js 版的 Lorikeet 应用显示的用户个人文件夹信息

图 2.7 显示得超赞。你可以在 index.html 的 `<script>` 标签中直接调用 Node.js。那么 Electron 怎么样的？是否也一样呢？请看图 2.8。

图 2.8 Electron 版的 Lorikeet 应用显示的用户个人文件夹信息

没错。正如你所见，不仅可以在 index.html 文件中的 `<script>` 标签中调用 Node.js 代码，还可以在前端代码中使用通过 npm 安装的 Node.js 模块。不仅如此，至此我们的 NW.js 和 Electron 都用了同样的代码，由此可见两者兼容性有多好，这也是为什么很多项目都可以很方便地从 NW.js 切换到 Electron（比如，Light Table 应用）。

现在已经实现了在工具条中显示用户个人文件夹信息了，接下来实现下一个功能：将用户个人文件夹中的文件和文件夹显示出来。

1『

路径没显示出来，目前不知道为啥。待解决。（2021-04-12）

解决方案：[javascript - Electron require() is not defined - Stack Overflow](https://stackoverflow.com/questions/44391448/electron-require-is-not-defined)

mian.js 里修改：

```js
  mainWindow = new BrowserWindow({
    webPreferences: {
      nodeIntegration: true,
      contextIsolation: false,
    }
  })
```

其实原书的代码里也出给了解决答案，之前自己没去看。

』

#### 2.3.2 Showing the user's files and folders in the UI

In the preceding section, we started off by creating the UI elements first and then populated the user's personal folder path in the UI element. For this feature, we'll work on getting ahold of a list of the user's files and folders first and then figure out from there how we display them in the UI of the application. For a quick reminder, figure 2.9 shows the UI element we're looking to implement.

Figure 2.9

The UI element we're looking to implement next in the app

To implement this UI feature, you need to do the following:

Get the list of files and folders at the user's personal folder path For each file/folder listing, find out if it's a file or a folder Pass that list of files/folders to the UI to be rendered as files with icons

You already have a way to get at the user's personal folder path. Now what you need is a way to get ahold of the list of files and folders at that path. Luckily for you, Node.js implements a standard library for querying the computer's filesystem, called fs. One of the functions available to get a list of files and folders is the readdir function, as documented at http://mng.bz/YR5B.

For both the NW.js and Electron versions of the Lorikeet app, you'll create an app.js file. This file will contain JavaScript code that can call Node.js as well as interact with the DOM. You'll use this file to help store the code that will display the list of files for you.

First, create an app.js file at the same folder level as the index.html and app.css files. Next, you'll move the code that loads the user's personal folder path into it. Add the following code to the app.js file:

'use strict'; const osenv = require('osenv'); function getUsersHomeFolder() { return osenv.home(); }

After adding the code to the app.js file, the next step is to include the app.js file as a script tag in the index.html and call the getUsersHomeFolder method in the DOM in place of the current call to the osenv module's home function. Change the index.html file so that it looks like the next listing.

Listing 2.8

Adding the app.js file to the index.html file

Includes app.js as script tag in index.html

Calls app.js's getUsersHomeFolder function in place of direct call to Osenv module's home function

If you reload the applications, you'll see that they behave the same, which is exactly what you want. You can now start to add code to the app.js file for getting the list of the files. You'll start by requiring Node.js's filesystem module, which comes as part of Node.js's standard library, and then adding a new function called getFilesInFolder that will retrieve the files in the folder passed to it. After that, you'll create a function called main that will pass the user's personal folder into that function, and from the resulting list of files log the absolute paths for them out in the console.

Change the code in the app.js file so that it looks like the following.

Listing 2.9

Logging the list of files and folders in the user's personal folder

After saving the app.js file, the next step is to see what happens when you run the code. Reload the application. In the case of Electron, if you toggle showing the developer tools for the application, you can expect to see the list of files in the Console tab, as shown in figure 2.10.

Figure 2.10 The Lorikeet Electron app showing the list of files being logged to the Console tab. To see the list of files on your computer, click View > Toggle Developer Tools.

You now know that you can get at the list of files in the user's personal folder. The next challenge is to figure out what the name and file/folder type is for each file in the list and to then display these items in the UI as a list of files and folders with icons.

Your goal is to be able to take a list of files and pass them through another function in Node.js's file system API. This will identify whether they're files or directories, as well as what their names and full file paths are. Do the following:

Use the fs.stat function method, as documented at http://mng.bz/46U5. Use the async module to handle calling a series of asynchronous functions and collecting their results.

Pass the list of results to another function that will handle their display.

In the app.js file for both variants of the Lorikeet app, install the async module via the Terminal or Command Prompt:

npm install async --save

After installing the async module to both applications, the next step is to change the app.js code so that it will detect what the files in the user's personal folder are. Change the code to that shown next.

Listing 2.10

Changing the app.js code to detect file types

With the app.js file saved to the computer and the applications reloaded, you'll see something like figure 2.11 in the developer tools.

Not only do you now have the application returning the list of files in the user's personal folder, but you have it in a data structure that has the filename and file type included as well. This sets you up perfectly for the next step in implementing the UI feature: displaying filenames and icons in the application's UI.

VISUALLY DISPLAYING THE FILES AND FOLDERS

In the previous code for the app.js file, you created a function called displayFiles. You want to use this function to handle displaying the files as names and icons in the UI. Because there are many files to be rendered in the UI, you'll use an HTML template for each file and then render an instance of that template to the UI.

You'll start by adding the HTML template to the index.html file, as well as a div element to contain the files that are being displayed. Change the index.html file so that it looks like the following listing.

Listing 2.11

Adding the file template and main area to the index.html file

The purpose of the template element is to hold a copy of the HTML that you'd like to render for each file, and the div element is where the template instances will be rendered and stored for each file that you find in the user's personal folder. You'll then add some JavaScript to the app.js file that will handle creating an instance of the template and adding it to the UI. Adjust the app.js file so that the code reads like the next listing.

Listing 2.12

Rendering the template instances in the UI via the app.js file

Now that HTML is being added to the app to handle the display of the files and the folders in the application, you want to make sure that the list of files and folders look styled and are displayed in a grid fashion. In the app.css file, change the CSS to match the following code.

Listing 2.13

Adding styling to the app.css file for displaying the files

This CSS will ensure that the items are displayed in a clear and grid-like fashion and that the toolbar will remain in a fixed position, visible above the files in the app as the main area div element is scrolled by the user.

You're almost there. All that's left to do is add the icons for the different file types to the application folder. Create a folder called images in the application folders with these commands in either the Terminal or the Command Prompt:

cd lorikeet-electron mkdir images cd ../lorikeet-nwjs mkdir images

Now, you can add some images for the file and directory icons. Inside the images folder, you'll insert two images named file.svg and directory.svg. The files are sourced from the OpenClipArt.org site from these URLs:

 https://openclipart.org/detail/137155/folder-icon  https://openclipart.org/detail/83893/file-icon

Save the files in the images folder (under the names file.svg for the file icon and directory.svg for the folder icon) and reload the application, and you should see something like figures 2.12 and 2.13.

Figure 2.12 The Lorikeet NW.js app showing the files and folders. Here, you see the beginnings of what looks like a file explorer application.

The file type property of the files is used to determine whether the icon is for a file or for a directory. This helps you easily distinguish files from folders. You'll also see that the file/folder names are displayed in alphanumerical order. In figure 2.12, dotfiles and hidden folders can be seen that would otherwise be hidden by other file explorer applications. Figure 2.13 shows the Electron Lorikeet app.

Figure 2.13

The Lorikeet Electron app showing files and folders

The Electron variant of the Lorikeet app looks almost identical to the NW.js version. All in all, the results look good, and that's the end of the exercise for this chapter.

2.3.2 显示用户个人文件夹中的文件和文件夹

在前面的内容中，我们先创建界面元素，然后将用户个人文件夹信息显示在界面上。对于这次这个功能，我们先要获取到用户个人文件夹中的文件和文件夹信息，再想办法把它们显示在界面上。回忆一下，图 2.9 显示的是我们要实现的样子。

图 2.9 我们接下来要实现的样子

要实现该功能，我们需要做以下这些事情：

1、获取到用户个人文件夹中的文件和文件夹列表信息。

2、对每个文件或者文件夹，判断它是文件还是文件夹。

3、将文件或文件夹列表信息显示到界面上，并用对应的图标区分出来。

你已经获取到用户个人文件夹的路径了，现在需要做的就是想办法获取到该路径下的文件和文件夹列表信息。幸运的是，Node.js 提供了一个名为 fs 的标准库，可用来查询计算机中的文件系统。该标准库中有一个方法叫 readdir，用它来获取某个路径下的文件和文件夹信息，具体文档参见 [File System | Node.js v6.17.1 Documentation](https://nodejs.org/dist/latest-v6.x/docs/api/fs.html#fs_fs_readdir_path_options_callback)。

对 NW.js 和 Electron 版的 Lorikeet 应用都创建一个 app.js 文件。该文件中的 JavaScript 代码可以调用 Node.js，也可以操作 DOM。我们将获取文件和文件夹列表信息的代码就放在这个文件中。

首先，在 index.html 和 app.css 同目录下创建一个 app.js 文件。然后将获取用户个人文件夹信息的代码移到该文件中。将如下代码插入 app.js 文件：

```js
'use strict'

const osenv = require('osenv')

function getUsersHomeFolder() {
  return osenv.home()
}
```

添加完上述代码后，接下来在 index.html 中用一个 `<script>` 标签将 app.js 文件加载进来，并在 DOM 位置调用 app.js 中的 getUsersHomeFolder 方法。将 index.html 修改为如代码清单 2.8 所示的内容。

代码清单 2.8 将 app.js 添加到 index.html 文件中

```html
<html> 
  <head> 
    <title>Lorikeet</title> 
    <link rel="stylesheet" href="app.css">
    <script src="app.js"></script>
  </head> 
  <body> 
    <div id="toolbar">
      <div id="current-folder">
        <script>
          document.write(getUsersHomeFolder())
        </script>
      </div>
    </div>
  </body> 
</html>
```

重启应用就会发现，它们没有任何区别，和预期的一样。现在可以往 app.js 中添加代码来获取文件列表了。首先加载 Node.js 的文件系统模块，它是 Node.js 标准库的一部分，紧接着添加一个新的函数叫 getFilesInFolder，用来获取传进来的文件夹下面的文件列表信息。然后再创建一个 main 函数，调用该函数并将用户个人文件夹路径作为参数传递进去，再将获取到的包含所有文件绝对路径的列表在控制台打印出来。

将 app.js 文件修改为如代码清单 2.9 所示的内容。

代码清单 2.9 将用户个人文件夹下的文件和文件夹列表打印出来

```js
'use strict'

// Node.js’s fs module loads in the app
const osenv = require('osenv')
const fs = require('fs')

function getUsersHomeFolder() {
  return osenv.home()
}

// Simple wrapper around the fs.readdir function for getting list of files
function getFilesInFolder(folderPath, cb) {
  fs.readdir(folderPath, cb)
}

// Function that combines user’s personal folder path with getting its list of files
function main() {
  const folderPath = getUsersHomeFolder()
  getFilesInFolder(folderPath, (err, files) => {
    // Simple message to display in case of error loading folder’s files
    if (err) return alert('Sorry, we could not load your home folder')
    // For each file in list, logs full path for file to console
    files.forEach(file => {
      console.log(`${folderPath}/${file}`)
    })
  })
}

main()
```

保存好 app.js 文件后，接下来重启应用来看看效果。在 Electron 应用中，如果打开应用的开发者工具，就能在其 Console 选项卡中看到打印出来的文件列表，如图 2.10 所示。

现在你已经知道如何获取用户个人文件夹下的文件列表了。接下来的问题是如何获取到文件名以及文件类型（是文件还是文件夹），并将它们以不同的图标在界面上显示出来。

你的目标是能够接收文件列表作为参数并将它们传递给 Node.js 文件系统 API 中的另一个函数。该函数能够识别是文件还是文件夹以及它们的名字和完整的路径。你需要完成下面三件事情：

1、使用 fs.stat 函数，具体文档参见 [File System | Node.js v6.17.1 Documentation](https://nodejs.org/dist/latest-v6.x/docs/api/fs.html#fs_fs_stat_path_callback)。

2、使用 async 模块来处理调用一系列异步函数的情况并收集它们的结果。

3、将结果列表传递给另外一个函数将它们显示出来。

图 2.10 Electron 版的 Lorikeet 应用在 Console 选项卡中将文件列表信息打印了出来。要在你的计算机中查看，单击 View => Toggle Developer Tools。

在两个版本的 Lorikeet 应用的 app.js 文件中，通过终端应用或者命令提示符应用安装 async 模块：

```
npm install async --save

yarn add async --save
```

为两个版本的应用都安装好 async 模块后，接下来修改 app.js 的代码，以实现获取用户个人文件夹中有哪些文件和文件夹的功能。将 app.js 的代码修改为如代码清单 2.10 所示的内容。

代码清单 2.10 修改 app.js 代码实现检查文件类型的功能

```js
'use strict'

// Node.js’s fs module loads in the app
const osenv = require('osenv')
const fs = require('fs')
const async = require('async')
const path = require('path')

function getUsersHomeFolder() {
  return osenv.home()
}

// Simple wrapper around the fs.readdir function for getting list of files
function getFilesInFolder(folderPath, cb) {
  fs.readdir(folderPath, cb)
}

// Uses path module to get name for file
function inspectAndDescribeFile(filePath, cb) {
  let result = {
    file: path.basename(filePath),
    path: filePath,
    type: ''
  }
  // fs.stat call supplies an object you can query to find out file’s type
  fs.stat(filePath, (err, stat) => {
    if (err) cb(err)
    if (stat.isFile()) result.type = 'file'
    if (stat.isDirectory()) result.type = 'directory'
    cb(err, result)
  })
}

// Uses async module to call asynchronous function and collects results together
function inspectAndDescribeFiles(folderPath, files, cb) {
  async.map(files, (file, asyncCb) => {
    let resolvedFilePath = path.resolve(folderPath, file)
    inspectAndDescribeFile(resolvedFilePath, asyncCb)
  }, cb)
}

// Creates displayFiles function to be end point where files will end up being displayed
function displayFiles(err, files) {
  if (err) return alert('Sorry, we could not display your files')
  files.forEach(file => console.log(file))
}

// Function that combines user’s personal folder path with getting its list of files
function main() {
  const folderPath = getUsersHomeFolder()
  getFilesInFolder(folderPath, (err, files) => {
    // Simple message to display in case of error loading folder’s files
    if (err) return alert('Sorry, we could not load your home folder')
    inspectAndDescribeFiles(folderPath, files, displayFiles)
  })
}

main()
```

保存 app.js 并重启应用后，就会从开发者工具中看到图 2.11 所示的结果。

你现在不仅获取到了用户个人文件夹下的文件列表信息，而且还将文件名以及文件类型都保存在了数据结构中。有了这些，接下来实现将它们以对应的图标展示在界面上就变得事半功倍了。

图 2.11 开发者工具中的 Console 选项卡显示了文件列表信息。注意第一个展开的对象包含的类型是文件，第二个则是目录

视觉上显示文件和文件夹

在此前 app.js 的代码中，你创建了一个名为 displayFiles 的函数。打算用这个函数处理将文件名字以及对应的图标展示在界面上。由于要展示的文件很多，我们将为每个文件定义一套模板，然后为每个文件创建一个该模板的实例再渲染到界面上。

先在 index.html 文件中添加 HTML 模板，模板中包含一个 div 元素，其中包含了要显示的文件信息。把 index.html 文件修改为如代码清单 2.11 所示的样子。

代码清单 2.11 在 index.html 文件主内容区添加为展示文件信息的模板

```html
<html> 
  <head> 
    <title>Lorikeet</title> 
    <link rel="stylesheet" href="app.css">
    <script src="app.js"></script>
  </head> 
  <body>
    <template id="item-template">
      <div class="item">
        <img class="icon">
        <div class="filename"></div>
      </div>
    </template>
    <div id="toolbar">
      <div id="current-folder">
        <script>
          document.write(getUsersHomeFolder())
        </script>
      </div>
    </div>
    <div id="main-area"></div>
  </body> 
</html>
```

上述 template 元素的目的是为每一个要渲染的文件信息定义一套 HTML 模板，真正被渲染的是模板实例中的 div 元素，它会将用户个人文件夹中的每个文件信息都显示出来。接下来需要在 app.js 中添加一些 JavaScript 代码，用来创建模板实例并添加到界面上。将 app.js 文件修改为如代码清单 2.12 所示的内容。

代码清单 2.12 通过 app.js 文件在界面上渲染模板实例

新增的代码：

```js
// Adds new function called displayFile that handles rendering template instance
function displayFile(file) {
  const mainArea = document.getElementById('main-area')
  const template = document.querySelector('#item-template')
  // Creates copy of template instance
  let clone = document.importNode(template.content, true)
  // Alters instance to include file’s name and icon
  clone.querySelector('img').src = `images/${file.type}.svg`
  clone.querySelector('.filename').innerText = file.file
  // Appends template instance to "mainarea" div element
  mainArea.appendChild(clone)
}

// Creates displayFiles function to be end point where files will end up being displayed
function displayFiles(err, files) {
  if (err) return alert('Sorry, we could not display your files')
  files.forEach(displayFile)
}
```

现在 HTML 已经添加好了，可以在应用中显示文件和文件夹信息了。接下来确保文件和文件夹信息以正确的样式显示，并且显示在栅格布局中。在 app.css 文件中，修改 CSS 代码为代码清单 2.13 所示的内容。

代码清单 2.13 在 app.css 文件中添加 CSS 代码，为显示的文件和文件夹信息定义样式

```css
body {
  padding: 0;
  margin: 0;
  font-family: 'Helvetica', 'Arial', 'sans';
}

#toolbar {
  top: 0px;
  position: absolute;
  background: red;
  width: 100%;
  padding: 1em;
  z-index: 2;
}

#current {
  float: left;
  color: white;
  background: rgba(0, 0, 0, 0.2);
  padding: 0.5em 1em;
  min-width: 10em;
  border-radius: 0.2em;
  margin: 1em;
}

#main-area {
  clear: both;
  margin: 2em;
  margin-top: 3em;
  z-index: 1;
}

.item {
  position: relative;
  float: left;
  padding: 1em;
  margin: 1em;
  width: 6em;
  height: 6em;
  text-align: center;
}

.item .filename {
  padding-top: 1em;
  font-size: 10pt;
}
```

上述 CSS 代码确保了列表项显示在一个整洁的栅格布局中，其中工具条始终固定在顶部，在显示文件列表的主区域 div 元素的上方，用户可以对主区域进行滚动。

马上就要完成了。剩下的任务是在应用文件夹中为不同类型的文件添加对应的图标。使用终端应用或者命令提示符应用，通过运行如下命令，在应用文件夹中创建一个名为 images 的文件夹：

```
cd lorikeet-electron
mkdir images

cd ../lorikeet-nwjs
mkdir images
```

现在，你可以为文件和文件夹添加对应的图标了。在 images 文件夹中，添加两张名为 file.svg 和 directory.svg 的图片。这两张图片来自 OpenClipArt.org 网站，可以通过如下 URL 获取：

[Folder icon - Openclipart](https://openclipart.org/detail/137155/folder-icon)

[File icon - Openclipart](https://openclipart.org/detail/83893/file-icon)

在 images 文件夹中保存这两张图片（文件图标使用 file.svg，文件夹图标使用 directory.svg），然后重启应用就会看到如图 2.12 和图 2.13 所示的样子了。

图 2.12 NW.js 版的 Lorikeet 应用展示了文件和文件夹信息。这看上去像一个文件浏览器应用的样子了

1『跑起来图标显示不出来，发现是两个图的命令问题，图片的文件名必须与 main.js 里 svg 的图片名一直，一个是 file.svg 一个是 directory.svg。（2021-04-13）』

文件类型属性是用来决定使用文件图标还是文件夹图标的，这有助于你对文件和文件夹进行区分，而且文件和文件夹的名字是按照字母顺序进行排序的。在图 2.12 中，文件名以点开始的文件以及隐藏文件都显示出来了，而这些在其他文件浏览器应用中一般都不会显示。图 2.13 显示的是 Electron 版的 Lorikeet 应用。

图 2.13 Electron 版的 Lorikeet 应用显示了文件和文件夹信息

Electron 版和 NW.js 版的 Lorikeet 应用看上去几乎一模一样。总的来说，看上去还不错，至此，本章的练习就结束了。
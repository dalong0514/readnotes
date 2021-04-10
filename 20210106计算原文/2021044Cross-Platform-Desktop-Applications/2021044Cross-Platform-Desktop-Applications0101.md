
Part 1 Welcome to Node.js desktop application development

Two frameworks prevail when it comes to building desktop applications with Node.js: NW.js and Electron. In the first part of the book, you'll be introduced to those frameworks and what advantages they have compared to other app frameworks, build a quick Hello World application with both NW.js and Electron, and then see what kinds of applications have been built.

In chapter 2, we'll begin to put those frameworks to use by building a file explorer app. We'll flesh out the skeleton of the app and add features to it, and explore the different approaches that NW.js and Electron take.

In chapter 3, we'll continue to iterate on the file explorer app by adding more features such as search and opening files. We'll then round up the app in chapter 4 by building executable versions for Mac OS, Windows, and Linux. By the end of part 1, you'll have gotten to know both NW.js and Electron, and put your knowledge to practical use in a real-world application.

第 1 部分 欢迎来到 Node.js 桌面应用开发的世界

说到使用 Node.js 构建桌面应用就不得不提这两个框架：NW.js 和 Electron。

本书第 1 章将为你介绍这两个框架，以及它们相比其他框架的优势在哪里，还会介绍如何使用 NW.js 和 Electron 快速构建一个 Hello World 应用，然后介绍已有的使用这两个框架构建的应用有哪些。

第 2 章通过构建一个文件浏览器应用，介绍如何使用这两个框架。我们会从头开始构建这个应用，并逐步添加更多的特性，构建过程中会介绍 NW.js 和 Electron 在实现这个应用上的区别。

第 3 章我们会继续为这个文件浏览器应用添加更多的特性，比如，搜索文件和打开文件。随后在第 4 章我们会完成这个应用并针对 Mac OS、Windows 和 Linux 构建应用的可执行版本。读完第 1 部分后，你就会对 NW.js 和 Electron 有所了解，并可以将你学到的知识用于实际应用的开发中。

# 0101. Introducing Electron and NW.js

## Summary

This chapter introduced you to NW.js and Electron and explained how they help web developers build desktop apps. We explored reasons why you might want to prefer Node.js desktop apps over building a web app, and how those frameworks help web developers by letting them use the same tools and technologies they’re already familiar with.

We then looked at the way that a simple Hello World app works and looks with different frameworks, across different OSs. This gave you a chance to understand how easy it is to take a web page and turn it into a desktop app.

We examined the features that make NW.js and Electron great frameworks for desktop app development, such as their use of the popular Node.js framework and the npm ecosystem, and the way they provide native executables for the different OSs from a single codebase. Finally, we explored a couple of real-life examples of NW.js and Electron in the wild and saw how apps have been successful in their own domains. This shows you what’s possible with Node.js desktop apps, and hopefully provides inspiration for any app ideas that you have.

In the next chapter, we’ll get our hands dirty and start building a file explorer desktop app with both NW.js and Electron. This will help you understand how you go about building desktop apps with those frameworks as well as how they compare in their approaches to desktop app development.

本章介绍了 NW.js 和 Electron，以及它们如何帮助开发者构建桌面应用。还分析了为何相比构建 Web 应用更应该使用 Node.js 开发桌面应用的原因以及那些框架是如何通过让 Web 开发者使用他们熟悉的工具和技术帮助他们开发桌面应用的。紧接着，介绍了使用不同框架构建同一个简单的 Hello World 应用，在不同的操作系统中的工作机制和样子。这也为大家展示了把一个 Web 页面嵌入一个桌面应用是多么容易。

我们检视了那些能让 NW.js 和 Electron 成为优秀的桌面应用开发框架的特性，诸如，它们都使用了 Node.js 框架、npm 生态系统以及支持从同一份代码构建出面向不同操作系统的可执行文件。最后，我们一起看了几个业界使用 NW.js 和 Electron 开发的桌面应用，也介绍了这些应用是如何在它们各自的领域取得成功的。这部分为大家展示了 Node.js 桌面应用的潜力，同时也希望可以为大家在开发桌面应用方面带来灵感。

下一章，我们开始动手使用 NW.js 和 Electron 构建一个文件浏览器桌面应用。这将有助于你理解如何着手使用这些框架开发桌面应用，以及这两个框架在桌面应用开发方面有何不同。

## 1.0

This chapter covers: 1) Understanding why Node.js desktop apps are the rage these days. 2) Previewing Node.js desktop application frameworks Electron and NW.js. 3) Using these frameworks to build cross-platform desktop apps with Node.js. 4) Comparing the frameworks. 5) Identifying real-world applications built with Electron and NW.js.

Node.js is known as a programming framework that lets developers build server-side applications in JavaScript. Since its creation in 2009, it has spawned a variety of popular web frameworks like Express and Hapi, as well as real-time web frameworks like Meteor and Sails. It has also allowed developers to create isomorphic web apps using tools like Facebook's React, a UI library that has had a huge impact on web development in recent years. It's fair to have the impression that Node.js is purely about web apps, but the truth is that Node.js is far more than that.

Node.js can be used to build cross-platform desktop apps, and chances are you're using one of them today. If you've ever used Slack at work, edited code using Atom from GitHub, or watched a movie using Popcorn Time, then you've used a Node.js desktop app. It's becoming a popular choice for developers, in particular web developers with little experience in desktop application development — even Microsoft has built and shipped an IDE (Visual Studio Code) using Node.js.

In the Node.js ecosystem, there are two major frameworks for creating desktop apps: NW.js and Electron. Both are supported by major businesses (NW.js by Inteland Gnor Tech, and Electron by GitHub), both have large communities around them, and both share similar approaches to building desktop apps. This book shows how to build cross-platform desktop apps with both Electron and NW.js. You may be pleasantly surprised by how much they have in common — in fact, they have some-thing of a shared history, but we'll get to that later. For now, we'll explore some of the reasons why Node.js desktop apps have taken off and where they might be useful for you and your work.

本章要点：1）介绍为何 Node.js 桌面应用近期热度如此之高。2）Node.js 桌面应用开发框架 Electron 和 NW.js 一览。3）使用 Node.js 以及这两个框架构建跨平台桌面应用。4）介绍两个框架的异同。5）介绍市面上使用 Electron 和 NW.js 开发的应用。

Node.js 是一种编程框架，它可以让开发者使用 JavaScript 来构建服务端应用。自 2009 年诞生以来，它衍生出许多流行的 Web 框架，比如，Express 和 Hapi，还有像 Meteor 和 Sails 这样的构建实时应用的 Web 框架。它还可以让开发者使用像 Facebook 的 React 这样的工具开发复杂的 Web 应用，React 是近几年在 Web 开发领域影响非常大的 UI 库。对 Node.js 的第一印象固然是它是用于 Web 应用开发的，然而事实却是它远不止于此。

Node.js 还可以用来构建跨平台的桌面应用，而且也许你现在就在使用它构建出来的应用。如果你工作的时候用的是 Slack，编辑代码的时候使用的是 GitHub 的 Atom 编辑器，或者看电影的时候用的是 Popcorn Time，那么你实际上就在使用 Node.js 开发的桌面应用。越来越多的开发者，特别是没有桌面应用开发经验的 Web 开发者，开始尝试使用 Node.js 来开发桌面应用 —— 甚至连微软都已经在用 Node.js 开发它的 IDE （Visual Studio Code）了。

在 Node.js 的生态中，有两个主流的桌面应用开发框架： NW.js 和 Electron。这两者都得到了大公司的支持（NW.js 背靠英特尔和 Gnor Tech，Electron 则背靠 GitHub），它们都拥有庞大的社区，而且在实现支持构建桌面应用方面都采用类似的解决方案。也许你会为它们有众多共同点而感到惊讶 —— 实际上，它们有过一段共同的历史，这部分会在后续章节中进行介绍。现在，让我们来看看使用 Node.js 开发桌面应用之所以这么流行其背后的原因到底是什么，以及它们会在你工作的哪些方面起到帮助。

## 1.1 Why build Node.js desktop applications?

To answer this question, you have to see how software has changed over the past generation and visualize where it is going.

要回答这个问题，我们得先来看看软件在过去一代进程中发生了怎样的变化以及它们将会如何发展下去。

### 1.1.1 Desktop to web and back

At the beginning of 2000, most software was available as desktop apps in shrink-wrapped boxes that you could buy from stores like Best Buy. You'd need to check the system requirements and make sure that it would work on the operating system (OS) you were running (which was Windows, for the majority of people). You'd then grab a CD-ROM out of the box, and install the software on your computer that way.

Over time, that began to change: improvements in web browsers, greater internet speeds and access, and the movement toward open source software resulted in a major shift in how software was created and distributed. The advent of AJAX spawned a new era of delivering software as web apps. These apps didn't require downloading anything onto the computer, and they could run across multiple OSs. Companies like Google and Facebook signaled the rise of the web as a powerful platform in the industry, and as people became accustomed to using apps online for a monthly fee, traditional software houses adapted and began to offer their software online.

It seemed like the web had won, but then mobile computing came along, leading to the rise of native apps for Apple iPhone and Android mobile devices. The industry changed again, and developers found themselves needing to adapt their business to support those devices too.

If reflecting on 16 years of software development shows anything, it's that there's a lot of change in the industry, and that we as developers will probably find ourselves supporting multiple computing platforms for years to come: desktop, web, mobile, and more. We're in the age of multiplatform computing.

Where does that leave desktop apps? Desktop apps have become one of a numberof computing platforms that we use in our day-to-day activities. But what has changedsince the 2000s is that where Microsoft Windows was the dominant OS for desktopcomputers back then, Apple has pared back that dominance with the popularity of itscomputers among creatives and professionals. Not only that, but Google's Chrome-books were the best-selling laptops in the U.S. in the first quarter of 2016. The year ofthe Linux desktop may have finally arrived. The point is this: you can't afford todevelop desktop apps that work on only Windows these days — there's a need for devel-oping apps that work across Mac OS and Linux as well.

Cross-platform desktop apps aren’t a new concept; frameworks like Mono and Qt have provided a way to develop desktop apps that run across all three of the major OSs. Usually, developers with a background in programming languages like C, C++, and C# could come to grips with these frameworks and develop software for them. Other developers, like web developers, would need to learn a new language alongside a framework, and this would be a barrier to them developing desktop apps.

When NW.js and Electron came about, they offered an opportunity to build desktop apps with the same code used to create web apps — and not only that, these desktop apps could operate across Windows, Mac OS, and Linux. It was a massive win for both code and skills reusability and unleashed a wave of new apps.

In addition, the popularity of Node.js has meant that developers have been able to leverage a huge ecosystem of open source libraries to build their apps with. Node.js developers and web developers alike could suddenly make desktop apps, and some of the apps out there are truly fantastic. One that comes to mind is WebTorrent by Feross Aboukhadijeh, shown in figure 1.1.

WebTorrent is a desktop app that allows you to upload files for other users to download, much in the same fashion as BitTorrent. It uses WebRTC to enable peer-to-peer connections, and to show you how portable the code is, the library used in the desktop app is the same as the one you can use in a web browser. It’s a truly fantastic piece of work.

The ability to support multiple OSs but write the software in a common and popular language has lots of pros because, as mentioned, desktop computing is still a major part of how people use computers today, even as new mobile computing platforms emerge. That’s why Node.js desktop apps have become an interesting way to deliver software. The next section elaborates on some of the reasons why you may consider building Node.js desktop apps over web apps.

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

### 1.1.2 What Node.js desktop apps offer over web apps

Web apps have thrived for a number of reasons:

 Internet speeds improved and access increased, and, importantly, the cost of internet access went down, making the user base grow massively, unlike most other communication channels.  Web browsers have benefitted from increased competition. As appealing alternatives to Internet Explorer emerged, new features were added to those browsers, which in turn enabled web apps to do new things.  The relative ease of learning HTML, CSS, and JavaScript lowered the barrier of entry for developers to make web apps, as opposed to learning lower-level languages like C and C++.  The rise of open source software meant that the cost of distributing and obtaining software declined significantly, meaning that developers with a bit of cash, time, and the right level of skill could build their own web apps.

When you look at all this, you can see why the web is such an important platform for developers to make software for. That said, there are still things that challenge and limit the ability of web apps today:

 Internet access is not always available. If you’re on a train and you go under a tunnel, chances are you’ll lose internet access. If your web app depends on saving data, hopefully it will be able to store a local copy of the changes and allow for them to be synchronized via the internet when access resumes.  If your app has a lot of features, the amount of data it will need to transfer over the internet to run the app could be large and may slow down the loading of the app. If it takes too long, people load something else — something proven by research into the impact that slow web page loading times have on e-commerce transactions.  If you’re working with large files (such as high-resolution images and videos) that are sitting on your desktop computer, then it might not make sense for them to be uploaded to the internet in order for a web app to edit them.

 Because of the security policy of the web browser, there are limits to what hardware/software features of the computer the web app can access.

 You have no control over what web browsers a user may use to visit your web app.

You have to use feature detection to cater to different web browsers, which restricts what features your app can use. The user experience (UX) can vary wildly.

Web apps are essentially restricted by the limits of internet access and browser features. It is in these circumstances that a desktop app may be preferable to a web app. Some of the benefits include the following:

 You don’t require internet access to start and run the app.

 Desktop apps start instantly, without having to wait for resources to download from the internet.

 Desktop apps have access to the computer’s OS and hardware resources, including access to the files and folder on the user’s computer.

 You have greater control over the UX with the software. You don’t have to worry about how different browsers handle CSS rules and what JavaScript features they support.

 Once a desktop app is installed on a user’s computer, it’s there. It doesn’t depend on you running web servers to support the app, where you need to offer 24/7 support in case your web app goes down, or worse, your web-hosting provider encounters technical difficulties.

Usually, desktop apps have required developers to be proficient in languages like C++, Objective-C, or C#, and knowing frameworks like .NET, Qt, Cocoa, or GTK. For some developers, that can be a barrier to entry and may discourage them from considering the possibility of building a desktop app.

The great thing about Node.js desktop application frameworks like Electron and NW.js is that they have significantly lowered that barrier of entry for developers. By allowing developers to create apps using HTML, CSS, and JavaScript, they’ve opened the door for web developers to also be desktop app developers, with the added benefit of being able to use the same code across both the web app and desktop app platforms.

Now it’s time to introduce the frameworks. As mentioned earlier in the chapter, Electron and NW.js have something of a shared history, so I’ll touch on the origins of both frameworks and then cover each in some detail.

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

## 1.2 The origins of NW.js and Electron

Back in 2011, Roger Wang managed to find a way to combine WebKit (the browser engine behind Safari, Konqueror, and Google Chrome at the time) with Node.js, so that you could access Node.js modules from the JavaScript code running inside a web page. This Node.js module was given the name node-webkit. He continued to work on the project at Intel’s Open Source Technology Center in China, which gave its support

to the project by letting Roger work on it full time. Not only that, he was allowed to hire others to work on it too.

In the summer of 2012, a senior college student named Cheng Zhao joined Intel as an intern to work on node-webkit. He worked with Roger to help improve its internal architecture, which involved changing how Node.js and WebKit were combined. As the code evolved, node-webkit moved from being a mere Node.js module to becoming a framework for desktop apps. Node-webkit was given interesting uses within third-party apps. The Light Table editor was the first to make use of node-webkit to deliver its functionality and helped to promote the framework to other developers.

In December of the same year, Cheng left Intel to work at GitHub as a contractor. He was tasked with helping to port GitHub’s Atom editor from using Chromium Embedded Framework and native JavaScript bindings to using node-webkit.

The efforts to port Atom to node-webkit encountered difficulties (see https:// github.com/atom/atom/pull/100), so they abandoned that approach. Instead, they decided to create a new native shell for Atom, which they called Atom Shell. This approach to combining WebKit with Node.js differed from the approach taken by node-webkit. Cheng Zhao focused all of his efforts into working on Atom Shell, which GitHub later open sourced shortly after open sourcing its text editor, Atom.

During this time, Node.js was going through a period of splintering — members of the Node.js community created a fork of Node.js called IO.js in order to get updates into the project faster, and in the WebKit community, Google announced that it was going to fork the WebKit project for Google Chrome into a variant called Blink. The combination of these changes led to renaming node-webkit as NW.js, and GitHub renamed the Atom Shell framework as Electron. Over time, Electron quickly acquired a number of admirers and was being used in high-profile apps like Slack and Visual Studio Code. It eventually became a juggernaut of its own creation, distinct from its original purpose as a tool for delivering Atom.

Although NW.js was the first Node.js desktop application framework, Electron has quickly emerged as a popular framework that has overshadowed NW.js, although both have been heavily worked on by the same developer at different points in time and share a lot of common code in terms of how users use their APIs for creating app features. Each has evolved a different approach to its internal architecture and has spawned separate communities that actively promote their respective projects.

In this respect, this book essentially covers two frameworks that do the same thing in slightly different ways. It’s a fairly unique situation in that the frameworks share so much history and are similar enough to merit being evaluated together. There’s a natural inclination to pick whichever is the bigger of the two and go with that, and the answer to that would be Electron (if you go by popularity and momentum), but some prefer NW.js to Electron for its relative simplicity in how you execute code and load the app, as well as for supporting computing platforms like Google Chromebooks, and because of other matters of programming opinion. I prefer to provide the information and let you decide what you want to use. It’s more ground to cover, but you’ll be better informed.

If you’re interested in digging into the history of both projects a bit more, the following links provide helpful pointers:

[From node-webkit to Electron 1.0](http://cheng.guru/blog/2016/05/13/from-node-webkit-to-electron-1-0.html)

[Question: Electron Origins · Issue #5172 · electron/electron](https://github.com/electron/electron/issues/5172#issuecomment-210697670)

If you’re looking for posts that compare and contrast the frameworks, here are some good links to look at as well:

http://electron.atom.io/docs/development/atom-shell-vs-node-webkit/

[NW.js & Electron Compared (2016 Edition) - TangibleJS](https://tangiblejs.com/posts/nw-js-and-electron-compared-2016-edition)

That’s a brief history of the two projects and how their paths have formed over time. We’ll now dive into each framework, starting with the first framework to emerge on the scene: NW.js.

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

## 1.3 Introducing NW.js

To recap, NW.js is a framework for building desktop apps with HTML, CSS, and JavaScript. It was created back in November 2011 by Roger Wang at Intel’s Open Source Technology Center in China. The idea was that by combining Node.js with WebKit (the web browser engine behind Chromium, an open source version of Google Chrome), you could create desktop apps using web technologies. This was the basis for the framework’s original name, node-webkit.

By combining Node.js with Chromium, Roger found a way to create apps that could not only load an HTML file with CSS and JavaScript inside an app window, but also could interact with the OS via a JavaScript API. This JavaScript API could then control visual aspects like window dimensions, toolbar, and menu items as well as provide access to local files on the desktop — things web apps couldn’t do.

To give you an idea of what this looks like, let’s walk through an example Hello World app for NW.js.

1.3 NW.js 介绍

简单来说，NW.js 是一个框架，它支持用 HTML、CSS 和 JavaScript 来构建桌面应用。起初它于 2011 年 11 月，由 Roger Wang 在英特尔中国开源技术中心创建。其背后的想法就是通过整合 Node.js 和 WebKit （Chromium 使用的 Web 浏览器引擎，Chromium 是开源版的谷歌 Chrome 浏览器），支持使用 Web 技术来创建桌面应用。所以一开始它被命名为 node-webkit。

通过整合 Node.js 和 WebKit，Roger 发现不仅可以在应用视窗内载入 HTML、CSS 和 JavaScript 文件，还可以通过 JavaScript API 和操作系统进行交互。通过这个 JavaScript API 可以控制视窗的视觉元素，比如，视窗大小、工具条以及菜单项，而且还可以访问本地文件系统 —— 这些是 Web 应用无法做到的。

为了让你对 NW.js 有一个形象的认识，我们来用 NW.js 构建一个 Hello World 示例应用。

### 1.3.1 A Hello World app in NW.js

This example application will give you a better understanding of what Node.js desktop apps are like with NW.js. Figure 1.2 show a design of the app we’ll build.

The code for this app is available in the GitHub repository for this book at http:// mng.bz/4W7Y.

If you want to get the code to run the app and see it in action, follow the instructions in the README.md file there. It’s ready-made to go. But if you want to see how the sausage is made, then read on and we’ll build the app from scratch.

The first step is to check whether you have Node.js installed. If you already do, great — move on to the next section, “Installing NW.js,” but if not, you’ll find instructions for installing Node.js in the appendix.

INSTALLING NW.JS

Node.js comes with a package management tool called npm that handles installing libraries for Node.js, and NW.js can be installed using it. On your computer, open the command-line program for your OS (Command Prompt or PowerShell on Windows, and Terminal on both Mac OS and Linux).

After you’ve opened your command-line program, run the following command:

npm install –g nw

This will install NW.js on your computer as a Node.js module available to all of your Node.js desktop apps.

CREATING THE HELLO WORLD APP

The app is so small that you can create the files by hand. At the bare minimum, you only need two files:

 A file named package.json — This contains configuration information about the app, and is required by NW.js.

 An HTML file — This file will be loaded by the package.json file and displayed in the app window. In this case, it’s a file called index.html (but it can be named something else, such as app.html or main.html).

Start by creating a folder for the app’s file. On your computer, go where you like to store your project source code and create a folder named hello-world-nwjs. Then you can create the package.json file that will be stored inside the hello-world-nwjs folder.

In your text editor/IDE, create a file named package.json inside the hello-worldnwjs folder and insert the following code into it:

```json
{
	"name" : "hello-world",
	"version" : "1.0.0",
	"main" : "main.js"
}
```

The package.json file consists of some configuration information about the app: its name, the main file to load when the app starts, and its version number. These fields are required by NW.js (though the version field is required by npm). The name field must contain lowercase alphanumeric characters only — there can be no space characters in the name.

The main field contains the file path for the entry point of your app. In the case of NW.js, you have the option of loading either a JavaScript file or an HTML file, but HTML files tend to be the common choice for NW.js apps. The HTML file is loaded into the app window, and to demonstrate this, you’ll create an HTML file called index.html that will be loaded.

Inside the hello-world-nwjs folder, create a file named index.html and insert the code in the following listing.

Once you’ve saved the index.html file on your computer, you can run the app on your computer. Inside the hello-world-nwjs folder, run the following command on your terminal:

nw

If you’re running on Mac OS, figure 1.3 shows what you should see.

If you’re running Linux, figure 1.4 shows the same app running on openSUSE 13.2 (Linux has many distributions, and openSUSE is one of the well-known distributions).

The Windows 10, Mac OS, and Linux versions of NW.js all share the same way to get the app started, which is handy. Type the same command in your Command Prompt, and you should see something like figure 1.5 on a Windows 10 computer.

Figure 1.5 The Hello World app running on Windows 10. The app looks almost identical to the app running on openSUSE Linux (minus the app window and a slight difference in font rendering).

If you click the Say Hello button in the middle of the app screen, you’ll see an alert dialog that says “Hello World.” If you were to take the index.html file and load it in a web browser such as Google Chrome, Microsoft Edge, or Mozilla Firefox, you would see the same screen and get the same result. That’s the point — you can take an HTML page for a website and turn it into a desktop app with NW.js without having to change the code.

At this point you might say, “Well, if that’s the case, why don’t I use a desktop app template that renders an HTML page inside a window and make do with that?” That’s not a bad question, and some apps have taken this approach.

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

完成后，NW.js 会以 Node.js 模块的形式安装在你的计算机中，所有的 Node.js 桌面应用都可以使用。

构建 Hello World 应用

这个应用很小，你可以手动来创建文件。不过你至少需要下面这两个文件。

1 package.json 文件 —— 这个文件是 NW.js 要求必须要有的，其包含了应用的配置信息。

2 一个 HTML 文件 —— 这个文件声明在 package.json 中，会被自动加载并显示在应用视窗中。在本例中，我们将这个文件取名为 index.html （不过你可以随便为它取名字，比如 app.html 或者 main.html）。

先来新建一个应用文件夹。在你的计算机中，找到一个你觉得合适的存储应用代码的位置，新建一个名为 hello-world-nwjs 的文件夹。然后在该目录下就可以新建一个 package.json 文件了。

在 hello-world-nwjs 文件夹中用你的文本编辑器或者 IDE 创建一个名为 package. json 的文件，并插入如下代码：






package.json 文件包含了一些与应用相关的配置信息：应用的名字、应用启动时要加载的主文件以及版本号。这些字段是必需的（其中 version 字段是 npm 要求的）。name 字段只能包含小写的英文字母或者数字，且不能有空格。

main 字段指定了应用入口文件的路径。在 NW.js 中，这个文件可以是 JavaScript 文件也可以是 HTML 文件，不过通常倾向于使用 HTML 文件。HTML 文件会被加载显示到应用视窗中，为了验证，我们来创建一个 index.html 文件。

在 hello-world-nwjs 文件夹中，创建一个名为 index.html 的文件，并插入代码清单 1.1 所示的代码。

代码清单 1.1 Hello World 应用的 index.html 文件的代码

保存 index.html 文件后，就可以在计算机中运行这个应用了。进入 hello-worldnwjs 文件夹，输入如下命令：

nw

如果使用的是 Mac OS，会看到图 1.3 所示的样子。

图 1.3 运行在 Mac OS 上的 Hello World 应用。这个应用截图和设计稿除了窗口大小之外几乎完全一样

如果在 Linux （openSUSE 13.2）上运行，就会看到如图 1.4 所示的样子（Linux 有很多发行版，openSUSE 是知名的发行版之一）。

图 1.4 运行在 openSUSE13.2 上的 Hello World 应用。它看起来和 Mac OS 上的差不多，视窗标题、颜色以及字体渲染效果略有不同

Windows 10、Mac OS 以及 Linux 版本的 NW.js 采用的启动应用方式相同，都很简便。在 Windows 10 的计算机中，打开命令提示符应用并输入同样的命令，就能看到图 1.5 所示的样子。

图 1.5 运行在 Windows 10 上的 Hello World 应用。它和 openSUSE Linux 上应用的样子几乎一样（除了应用视窗和字体渲染效果略有不同之外）

如果单击屏幕中间的 Say Hello 按钮，会弹出一个写着「Hello World」的警示框。如果使用谷歌的 Chrome、微软的 Edge 或者 Mozilla 的 Firefox 浏览器打开 index. html 文件，也能看到同样的界面，单击按钮后也会看到同样的结果。这就是关键 —— 代码不需要修改，你就可以直接将网站的 HTML 页面转变为 NW.js 开发的桌面应用。

关于这点你也许会说「好吧，那既然这样，我为什么不用这样一个方案呢 —— 用一个桌面应用模版，将 HTML 页面渲染在视窗中？」这个问题问得还不错，有些应用就是这么做的。

但这个方案不好的原因是没有简化开发。因为你可能不懂 C++，又或者你懂，但你也许不想每次做了一点改动都要重新编译代码才能运行。又或者，你可能想用原生桌面应用才有的特性，而这些特性在一个内嵌在应用视窗中的 HTML 文件中无法使用。另外一个主要原因是，作为桌面应用开发框架，Electron 和 NW.js 都为你开发桌面应用提供了丰富的特性，这部分会在接下来的内容中介绍。

### 1.3.2 What features does NW.js have?

NW.js has a set of features that makes it appealing for developers to use when building desktop apps. In a generic overview, they are as follows:

 A JavaScript API for creating and accessing native UIs and APIs to the OS: control windows, add menu items, tray menus, read/write files, access the clipboard, and more  The ability to use Node.js inside your app as well as install and use a huge

library of Node.js modules via npm  Being able to build executables of the app for each OS from a single codebase

I’ll explain each bullet point in more detail in the next sections.

ACCESSING OS NATIVE UI AND API VIA JAVASCRIPT

A good desktop app integrates well into the user’s OS: a music app will work with the media keyboard shortcuts on a user’s keyboard, a chat app may have a menu icon in the tray area of the OS, and a productivity app may provide notifications when actions have completed.

NW.js provides a large API for getting access to OS features, which do the following:

 Control the size and behavior of the app’s window  Display a native toolbar on the app window with menu items  Add context menus in the app window area on right-click  Add a tray app item in the OS’s tray menu  Access the OS clipboard, read the contents, and even set the contents  Open files, folders, and URLs on the computer using their default apps  Insert notifications via the OS’s notification system

As you can see from the preceding list, there are a lot of things you can do within NW.js that web browsers cannot do. For example, web browsers don’t have direct access to files on the desktop or the contents of the clipboard due to security restrictions that web browsers implement to protect users from sites with malicious intent. In the case of NW.js, because the app runs on the user’s computer, it’s granted a level of access where the user trusts the app. This means that you can do things like access the files that are on the user’s computer, create new files and folders, and more. These features allow the developer to create desktop apps that fit well with the user’s OS and do things that web apps can’t do (or at least not as easily) — and the user trusts the app to be responsible and not do anything malicious.

USING NODE.JS AND NPM MODULES INSIDE YOUR APP

NW.js provides access to the Node.js API in the app, as well as uses modules that are installed with npm. This means that you can install npm modules for use with your desktop apps, and you can even access them and Node.js core modules from the same code that’s interacting with the front end of the desktop app.

For example, you could write a bit of embedded JavaScript in the index.html file that uses the Node.js filesystem module to get a list of files and folders in a given directory, and then list those files as list items in the HTML. This shared JavaScript context between the front-end and back-end parts of the desktop app is an intriguing aspect of the way NW.js combines Node.js with Chromium. It’s something to keep in mind when you’re working with NW.js applications (as opposed to Electron applications). It’s quite different from how web apps work, as figure 1.6 demonstrates.

Figure 1.6 The difference between a web app and an NW.js desktop app. The separation between front-end and back-end code in an NW.js desktop is blurred, as the JavaScript context is shared between both parts of the code.

To explore this a bit further, consider how traditional web apps work. Web apps tend to have a client/server model where the client requests a web page or makes an API request, and the server executes some code to then serve that data back to the client. The client in this case is a computer running a web browser. The web browser then loads the data, where, if it’s HTML, the rendering engine turns it into a web page; or, if it’s data like XML or JSON, the rendering engine displays it in raw form. The server does its job of executing back-end code to serve HTML pages or API requests, and the computer client running the web browser does its job of making HTML/API requests and rendering the response in the web browser. The web browser applies a strict security model to ensure that the front-end code executes within the context of the web page and nothing else. There's a clear separation of application state and responsibility.

In an NW.js app, the app window is essentially like an embedded web browser, but with the distinct difference that the code inside the web page has access to the computer’s resources and can execute server-side code. There's no separation of app state and responsibility. This means you can write code that's calling out to DOM elements in the web page and executing server-side code accessing the computer’s filesystem in the same place. Not only that, you’ll be able to use npm modules in your code as well.

Being able to install npm modules and require them in your desktop app means you have access to over 400,000 libraries (as of January 2017) for use in your code. You’ll have plenty of options when it comes to using third-party libraries in your app. In fact, both NW.js and Electron have spawned a number of dedicated libraries for use with desktop apps, all of which you’ll be able to find at http://npmjs.com, and at https://github.com/nw-cn/awesome-nwjs and https://github.com/sindresorhus/awesome-electron.

BUILDING YOUR APP FOR MULTIPLE OSS FROM A SINGLE CODEBASE

One of the most useful features of NW.js is that from a single codebase for your desktop app, you can build native executable apps for Windows, Mac OS, and Linux. This is a time saver when you’re developing an app that has to work across multiple platforms. It also means you can have greater control over how the app looks and feels, more so than you can when trying to support a website for multiple web browsers.

The native executable is able to run on its own and doesn’t require the user to have any other software installed on their computer. This makes it easy to distribute the app to users, including on stores like Apple’s App store and the Steam store, where some NW.js apps and games are sold.

The process of building an app for a specific OS involves a few command-line arguments, but there are some tools that simplify the process for you, such as the nw-builder tool, illustrated in figure 1.7.

Taking an example desktop app, I’m able to use nw-builder’s nwbuild command in step 1 to automate the steps of turning our desktop app’s code into executable binaries for both Mac OS and Windows, as shown in step 3. This can save a lot of time (if you have to make both 32-bit and 64-bit builds of the app) and prevent mistakes when building the app.

In the next section, we’ll turn our attention to Electron: how an example app works and looks with it, and what features it has.

## 1.4 Introducing Electron

Electron is a desktop app framework from GitHub. It was built for GitHub’s text editor Atom and was originally known as Atom Shell. It allows you to build cross-platform desktop apps using HTML, CSS, and JavaScript. Since its release back in November 2013, it has become popular and is used by a number of startups and large businesses for their apps. Electron is used not only in Atom but also in the desktop clients of a chat app called Slack (www.slack.com), a startup that was valued at `$3.8` billion as of April 2016.

### 1.4.1 How does Electron work and differ from NW.js?

One of the things that Electron did differently from NW.js was the way it got Chromium and Node.js to work together. In NW.js, Chromium is patched so that Node.js and Chromium are sharing the same JavaScript context (or state, as you may call it in programming). In Electron, there’s no patching of Chromium involved; instead, it’s combined with Node.js through Chromium’s content API and the use of Node.js’s node_bindings.

The implication of this approach is that Electron works differently from NW.js in terms of how it handles JavaScript contexts. Where NW.js maintains a single shared JavaScript context, Electron has separate JavaScript contexts — one for the back-end process that kicks off running the app window (referred to as the main process), and one for each app window (referred to as the renderer process). This is an important difference between the frameworks, and one that will be elaborated on further in the book through various examples.

Another important difference between NW.js and Electron is that where NW.js usually uses an HTML file as the entry point for loading a desktop app, Electron uses a JavaScript file instead. Electron delegates the responsibility of loading an app window to code that’s executed inside the JavaScript file. You’ll see this in greater detail as we explore the Hello World app in Electron in the next section.

### 1.4.2 A Hello World app in Electron

Like the Hello World app in NW.js, I’ve also created the app that we’ll run through now. If you want to boot that up and play with it, you can grab a copy of the source at http://mng.bz/u4C0.

Follow the instructions in the README.md file to get the app up and running. Alternatively, if you want to bake the cake rather than merely eat it at the end, we’ll walk through that now.

Assuming that you’ve already installed Node.js on your computer (if not, see “Installing Node.js” in the appendix of this book), let’s start by downloading a copy of Electron via npm. In your terminal or at the Command Prompt, run the following command:

npm install –g electron

This will install Electron as a global npm module, meaning that it will be available to other Node.js applications where you want to use it. Once you have installed the Electron module, we can take a look at what an example Hello World app’s files consist of. Here’s the bare minimum number of files required to run an Electron app:

 index.html  main.js  package.json

You can create a folder named hello-world-electron to store the app’s files. Create a folder with the suggested name, and then you’ll add the required files inside it.

We’ll start with the package.json. Here’s what an example package.json looks like:

{

"name" : "hello-world", "version" : "1.0.0", "main" : "main.js"

}

You might notice that package.json looks almost identical to the package.json file used to load the Hello World app in NW.js. The only difference is that where an NW.js app’s package.json field expects the main property to specify an HTML file as the app’s entry point, Electron expects the main property to specify a JavaScript file.

In Electron, the JavaScript file is responsible for loading an app’s windows, tray menus, and other items, as well as handling any system-level events that occur in the OS. For the Hello World example, it looks like the following.

What you can see in listing 1.2 is that where NW.js points to an HTML file in the package.json file, Electron requires a bit of code configuration to achieve the same result.

The JavaScript code looks a bit funny

If you’re fairly new to Node.js and haven’t touched JavaScript in a while, you may notice some new language features like the use of const and let for variable declaration, as well as => as a function shorthand. This is the next version of JavaScript, also known as ES6. It’s a fairly new version of JavaScript that's now integrated into Node.js and is actively used in Electron. To learn more about ES6, you can visit https://babeljs.io/learn-es2015/, http://es6-features.org, and https://es6.io/.

If you prefer the traditional style of writing JavaScript, you can continue to use it for your Electron applications. The internet is full of opinions, but that doesn’t mean that you have to adopt them. My suggestion is to find what works for you and go from there.

Having created the main.js file that’s the entry point to your app, you’ll now create the index.html file that the main.js file loads in an app window. Create a file named index.html, and insert the code shown next.

This is the HTML file that will be loaded into the browser window by the main.js file. It’s the same code that’s used in the NW.js example app’s index.html file (so we can compare the examples across both frameworks). With the files saved in the application folder, you can now run the app from the command line.

To execute the app from the command line, cd into the hello-world-electron directory, and run the following command:

electron .

Once you’ve run the command, click the Hello World button, and you can expect to see something like figure 1.8.

Figure 1.8 The Hello World example app running with Electron on Mac OS. It looks almost identical to the NW.js equivalent, except the window dimensions are different.

The app for the most part looks identical to the one running on NW.js, with a few slight differences. In figure 1.9, you can see how it looks running on OpenSUSE Linux 13.2.

The Hello World Electron example app looks a bit different from the version that runs on a Mac. This is because Mac OS handles displaying menus differently than Windows and Linux apps do. Where menus are attached to app windows on both Microsoft Windows and Linux apps, Mac OS displays a single menu in the OS’s toolbar that applies to all app windows, as shown for the Hello World Electron app’s Mac OS example in figure 1.10.

Figure 1.9 The Hello World example app running with Electron on OpenSUSE Linux. Notice how the app displays a menu bar with some menu items by default.

Figure 1.10 Application menu on Mac OS. The application menu for the Hello World example app uses the same default menu items.

If you open the app in Windows 10, you can expect to see a result similar to the one displayed for the Linux app example, as shown in figure 1.11.

The Hello World app with Electron and Windows 10 again looks quite similar to the app equivalents on Linux and Mac OS, minus where the application menu is displayed. The ability to write an app and have it work across three different OSs is a nice feature to have, though, and it’s one of the reasons why developers have been flocking to Electron for their desktop apps.

Besides what’s been shown so far, Electron has some other features to offer that make it a compelling choice, described in the next section.

Figure 1.11 The Hello World app running on Electron and Windows 10. Like the Linux app example, the Windows example displays a menu in the app window.

### 1.4.3 What features does Electron have?

Although Electron is relatively young, it has managed to accumulate a number of useful APIs and features for building desktop apps:

 Creating multiple application windows with ease, each with its own JavaScript context  Integrating with desktop OS features through the shell and screen APIs  Tracking the power status of the computer  Blocking the OS from going into power-saving mode (useful for presentation

apps)  Creating tray apps  Creating menus and menu items  Adding global keyboard shortcuts to the app  Updating the app’s code automatically through app updates  Reporting crashes

 Customizing Dock menu items  Operating system notifications  Creating setup installers for your app

As you can see, a lot of features are on offer, and that isn’t an exhaustive list of all of the framework’s features. In particular, the crash-reporting feature is unique to Electron — there’s currently no equivalent to it in NW.js. Electron has also recently come up with dedicated tools for app testing and debugging, called Spectron and Devtron, covered in later chapters.

Demonstrating what Electron does and how it does it, the team behind Electron created a desktop app for demoing Electron’s APIs. It’s a neat way to browse through Electron’s APIs in a practical fashion, and can be downloaded from http://electron .atom.io/#get-started.

A COOL WAY TO EXPLORE ELECTRON’S FEATURE SET

The next section looks at what apps can be made with NW.js and Electron.

## 1.5 What apps can you make with NW.js and Election?

Although Electron and NW.js are relatively young in terms of software, their use in professional cases is rich and varied. On the NW.js GitHub repository, there’s a long list of example apps that have been built with NW.js, and for Electron there’s the Awesome Electron GitHub repository providing a long list of apps and resources at https://github.com/sindresorhus/awesome-electron. In this section, I discuss a couple of well-known examples that have been commercially successful, as well as ones that demonstrate the potential for what Electron and NW.js can do. We’ll start with one of the biggest success cases for Electron: Slack.

### 1.5.1 Slack

Slack (slack.com) is a workplace communication and collaboration tool for businesses. Slack uses Electron to provide the desktop app and is advertising jobs for desktop app engineers who have experience with using Electron. The desktop user interface (UI) is practically identical to the web app interface — a shining example of what Electron can achieve. The app has expanded its feature set to allow for audio and video calls. Figure 1.12 shows Slack in use (note, I blanked out some of the message content and channels for privacy reasons).

Slack recently expanded its offering with support for an app directory for Slack, allowing users to install third-party apps that run inside Slack. The company seems to have a good future ahead.

### 1.5.2 Light Table

Light Table (lighttable.com) is a code editor that takes a different approach to the IDE. It was developed by Chris Granger and raised over `$300,000` through a campaign on Kickstarter. It was also the first third-party usage of NW.js and was credited with helping promote the framework in the early days of the project.

The code editor initially supported Clojure but went on to support JavaScript and Python. The philosophy behind Light Table was to rethink how to approach the task of editing code. Rather than having to think of code as lines within files, the focus should be on providing a kind of workspace in which the code is executed live, and documentation is displayed in place rather than searched for in another window, as shown in figure 1.13. It was meant to be a kind of workspace for the developer to be able to write code and see the results immediately, rather than in isolation. Originally made with NW.js, it was recently ported to Electron.

Figure 1.13 Light Table, a live interactive code editor. A 3D visualization written in JavaScript is being edited in the left-hand panel, and the results are being rendered live in the right-hand panel.

1.5.3 Game Dev Tycoon

Game Dev Tycoon is a simulation game in the spirit of old simulations like Transport Tycoon and SimCity, but in this case themed around running a game development studio (an irony, given that it was created by a game development company). Behind it is a small company called Greenheart Games, founded in July 2012 by Patrick and Daniel Klug.

The game was unique (and even more ironic) in its attempts to fight off piracy. Patrick anticipated that the game would eventually be pirated and countered this by releasing a cracked copy of the game onto Torrent sites, but with an interesting twist: people playing the game would find themselves losing in the game. As they played the game, they would find that suddenly their games would stop making money, because they were being pirated. Eventually they would go bankrupt as a result and lose. This antipiracy tactic attracted a lot of amusement and attention.

Since its founding, the company has grown to five employees, and the game is being sold on the Steam game store. Shown in figure 1.14, it’s one of the best showcases for using NW.js to build a successful commercial project.

Figure 1.14

Game Dev Tycoon, a game studio simulator

1.5.4 Gitter

Gitter is a service that provides chat rooms for open source projects on GitHub, including the official chat room for NW.js. It allows users to sign in with a GitHub account and to then access chat rooms based on projects and organizations. It’s seen as a popular alternative to Slack.

As a chat service, Gitter is available both via its website (gitter.im), as well as via desktop apps for Windows and Mac OS, which are built using NW.js. The app’s look and feel is an exact replica of what you see in the web app and well demonstrates the principle of code reuse. During the beta period, Gitter attracted almost 25,000 developers to the service, delivering over 1.8 million messages, and is currently hosting over 7,000 chat rooms. It now offers paid plans for chat rooms, and the company is working on getting a version of the app to run on Linux as well.

The main chat room for NW.js can be found on Gitter, a nice example of a product being used to support itself (figure 1.15).

1.5.5 Macaw

Macaw (macaw.co) is an innovative WYSIWYG web design tool. It allows web designers to create a visual design for their websites, as they would normally do in an image editor, and generates the underlying HTML and CSS for that design. It helps eliminate the step of converting a visual design into a real website by automatically creating the website code. As a WYSIWYG web design tool, Macaw differs from predecessors like Microsoft FrontPage and Adobe Dreamweaver by outputting semantic HTML and CSS from the visual design.

Founded by Tom Giannattasio and Adam Christ, the product (figure 1.16) was funded through a Kickstarter campaign that raised over $275,000 from more than 2,700 backers. Since March 2014, Macaw has gone on to become a product sold directly through Macaw’s website.

Since I began writing the book, I’m pleased to say that Macaw was acquired by another web design application company called InVision — yet another example of a real-world desktop app becoming a success story.

Figure 1.16 features

Macaw, a WYSIWYG web design tool that lets designers create websites using visual design

1.5.6 Hyper

Hyper (hyper.is) is a minimal-looking terminal app authored by Guillermo Rauch, a well-known figure in the Node.js community for his work on the Node.js websocket library, Socket.io, and for the real-time hosting service Now. As a terminal app written in HTML, CSS, and JavaScript, Hyper is an extensible app that can be configured to look and behave in lots of different ways. Developers have created plugins (such as hyperpower) that animate the text as it’s typed into the app and enable users to open URLs from within the terminal window. Figure 1.17 shows Hyper in use.

It’s one of the more unique types of desktop apps reimagined with Electron and shows Electron’s minimal style title bar in use.

Figure 1.17 Hyper running on Mac OS


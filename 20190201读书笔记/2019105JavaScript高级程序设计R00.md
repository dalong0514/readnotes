## 记忆时间

## 卡片

### 0101. 反常识卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡——

根据反常识，再补充三个证据——就产生三张术语卡。

### 0202. 术语卡——

### 0203. 术语卡——

### 0301. 人名卡——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

### 0401. 金句卡——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 任意卡——

最后还有一张任意卡，记录个人阅读感想。

## 序言

JavaScript 是基于 Java 的一种非常松散的面向对象语言，也是 Web 开发中极受欢迎的一门语言。JavaScript，尽管它的语法和编程风格与 Java 都很相似，但它却不是 Java 的「轻量级」版本。JavaScript 是一种全新的动态语言，它植根于全球数亿网民都在使用的 Web 浏览器之中，致力于增强网站和 Web 应用程序的交互性。

1『JavaScript 是动态语言。』

在本书中，我们将对 JavaScript 追根溯源，从它在最早的 Netscape 浏览器中诞生谈起，一直谈到今天的它对 DOM 和 Ajax 的强大支持。读者将通过本书掌握如何运用和扩展这门语言，从而更好地满足自己的需求，以及如何实现客户端与服务器的无缝通信，而又不必求助于 Java 或隐藏的网页框架（frame 元素）。一言以蔽之，本书将教会你在面对各种常见的 Web 开发问题时，如何拿出自己的 JavaScript 解决方案。

1『对 Ajax 的支持，标志着 Web 1.0（静态网页）迈向 Web 2.0（动态网页）。』

3『

[AJAX - 维基百科，自由的百科全书](https://zh.wikipedia.org/wiki/AJAX)

[AJAX - 廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/1022910821149312/1023022332902400)

』

本书首先介绍了 JavaScript 的起源及其发展现状，随后讨论了构成 JavaScript 实现的各个组成部分，重点讲解了 ECMAScript 和 DOM 标准。此外，还对不同 Web 浏览器的 JavaScript 实现之间存在的差异，给出了相应的说明。

在此基础上，本书从讲解 JavaScript 的基本概念入手，探讨了 JavaScript 面向对象程序设计和继承的方式，以及如何在 HTML 等标记语言中使用它。在深入剖析了事件和事件处理之后，又解释了各种浏览器检测技术。本书还探讨了 HTML5、Selectors API 和 File API 等一系列新 API。本书最后一部分专门讨论了高级主题，涉及性能和内存优化、最佳实践以及对 JavaScript 未来的展望。

第 1 章「JavaScript 简介」，讲述了 JavaScript 的起源：因何而生，如何发展，现状如何。涉及的概念主要有 JavaScript 与 ECMAScript 之间的关系、DOM（Document Object Model，文档对象模型）、BOM（Browser Object Model，浏览器对象模型）。此外，还将讨论 ECMA（European Computer Manufacturer's Association，欧洲计算机制造商协会）和 W3C（World Wide Web Consortium，万维网联盟）制定的一些相关标准。

1『BOM 是一些对象的集合。是负责处理与浏览器自身有关的交互操作的对象集合，比如对象 window、document、location、navigator 和 screen。』

第 2 章「在 HTML 中使用 JavaScript」，介绍了如何在 HTML 中使用 JavaScript 创建动态网页。这一章不仅展示了在网页中嵌入 JavaScript 的各种方式，还讨论了 JavaScript 内容类型（content-type）及其与 script 元素的关系。

第 3 章「基本概念」，讨论了 JavaScript 语言的基本概念，包括语法和流控制语句。这一章也分析了 JavaScript 与其他基于 C 的语言在语法上的相同和不同之处，还介绍了与内置操作符有关的类型转换问题。

第 4 章「变量、作用域和内存问题」，探讨了 JavaScript 如何处理其松散类型的变量。这一章还讨论了原始值和引用值之间的差别，以及与变量有关的执行环境的相应内容。最后，通过介绍 JavaScript 的垃圾收集机制，解释了变量在退出作用域时释放其内存的问题。

第 5 章「引用类型」，详尽介绍了 JavaScript 内置的所有引用类型，如 Object 和 Array。这一章对 ECMA-262 规范中描述的每一种引用类型既做了理论上的阐释，又从浏览器实现的角度给出了 介绍。

第 6 章「面向对象的程序设计」，讲述了在 JavaScript 中如何实现面向对象的程序设计。由于 JavaScript 没有类的概念，因此这一章从对象创建和继承的层面上展示了一些流行的技术。此外，这一章还讲解了函数原型的概念，并对函数原型与整个面向对象方法的关系进行了探讨。

第 7 章「函数表达式」，集中介绍了 JavaScript 中最为强大的一个特性 —— 函数表达式。相关的内容涉及闭包、this 对象的角色、模块模式和创建私有对象成员等。

第 8 章「BOM」，介绍 BOM（Browser Object Model，浏览器对象模型），即负责处理与浏览器自身有关的交互操作的对象集合。这一章全面介绍了每一个 BOM 对象，包括 window、document、location、navigator 和 screen。

第 9 章「客户端检测」，讨论了检测客户端机器及其支持特性的各种手段，包括特性检测及用户代理字符串检测的不同技术。这一章还就每种手段的优缺点及适用情形给出了详细说明。

第 10 章「DOM」，介绍 DOM（Document Object Model，文档对象模型），即 DOM1 规定的 JavaScript 中的 DOM 对象。这一章也简要介绍了 XML 及其与 DOM 的关系，为深入探讨所有 DOM 规范及其定义的操作网页的方式奠定了基础。

第 11 章「DOM 扩展」，介绍了其他 API 以及浏览器本身为 DOM 添加的各种功能。涉及内容包括 Selectors API、Element Traversal API 和 HTML5 扩展。

第 12 章「DOM2 和 DOM3」，在前两章的基础上继续探讨了 DOM2 和 DOM3 中新增的 DOM 属性、方法和对象。这一章还讨论了 IE 与其他浏览器的兼容性问题。

第 13 章「事件」，解释了 JavaScript 中事件的本质，对遗留机制的支持，以及 DOM 对事件机制的重新定义。这一章讨论了多种设备，包括 Wii 和 iPhone。

第 14 章「表单脚本」，讲述如何使用 JavaScript 增强表单的交互性，突破浏览器的局限性。这一章的讨论主要围绕单个表单元素如文本框、选择框，以及围绕数据验证和操作展开。

第 15 章「使用 Canvas 绘图」，讨论了 <canvas> 标签以及如何通过它来动态绘图。不仅涵盖 2D 上下文，也将讨论 WebGL（3D）上下文，可以为创建动画和游戏夯实基础。

第 16 章「HTML5 脚本编程」，介绍了 HTML5 规定的 JavaScript API，涉及跨文档传递消息、拖放 API 和以编程方式控制 <audio> 和 <video> 元素，以及管理历史状态。

第 17 章「错误处理与调试」，讨论浏览器如何处理 JavaScript 代码错误，并展示了一些处理错误的方式。这一章针对每种浏览器分别讨论了相应的调试工具和技术，还给出了简化调试工作的建议。

第 18 章「JavaScript 与 XML」，展示了 JavaScript 中用于读取和操作 XML（eXtensible Markup Language，可扩展标记语言）的特性。这一章分析了不同浏览器提供的 XML 支持和对象的差异，给出了编写跨浏览器代码的简易方法。此外，这一章还介绍了用于在客户端转换 XML 数据的 XSLT（eXtensible Stylesheet Language Transformations，可扩展样式表语言转换）技术。

第 19 章「E4X」，讨论了 E4X（ECMAScript for XML，ECMAScript 中的 XML 扩展）；设计 E4X 的出发点是简化 XML 处理任务。这一章探讨了在处理 XML 时，使用 E4X 与使用 DOM 相比有哪些 优势。

第 20 章「JSON」，介绍了作为 XML 替代格式的 JSON，包含浏览器原生支持的 JSON 解析和序列化，以及使用 JSON 时要注意的安全问题。

第 21 章「Ajax 与 Comet」，讲解了常用的 Ajax 技术，包括使用 XMLHttpRequest 对象及 CORS（Cross-Origin Resource Sharing，跨来源资源共享）API 实现跨域 Ajax 通信。这一章展示了浏览器在实现与支持方面存在的差异，同时也给出了一些使用建议。

第 22 章「高级技巧」，深入讲解了一些 JavaScript 中较复杂的模式，包括函数科里化（currying）、部分函数应用和动态函数。这一章还讨论了如何创建自定义的事件框架和使用 ECMAScript 5 创建防篡改对象。

第 23 章「离线应用与客户端存储」，讨论了如何检测应用离线以及在客户端机器中存储数据的各种技术。先从受到最广泛支持的特性 cookie 谈起，继而介绍了新兴的客户端存储技术，如 Web Storage 和 IndexedDB。

第 24 章「最佳实践」，探讨了在企业级环境中使用 JavaScript 的各种方式。其中，着眼于提高可维护性的内容包括编码技巧、格式化和通用编程实践。这一章还介绍了改善代码执行性能及速度优化的一些技术。最后讨论了部署问题，包括如何创建构建过程。

第 25 章「新兴的 API」，介绍了为增强浏览器中的 JavaScript 而创建的新 API。虽然这些 API 还没有得到完整或全面的支持，但它们已经崭露头角，有些浏览器也已经部分地实现了这些 API。这一章的内容主要是 Web 计时和文件 API。

## 01. JavaScript 简介

### 1. 逻辑脉络

JavaScript 是专为与网页（web）交互而设计的脚本语言，三大核心：ECMAScript、DOM 和 BOM。ECMAScript 提供核心语言功能；DOM 提供访问和操作网页内容的方法和接口；BOM 提供与浏览器交互的方法和接口。

### 2. 摘录及评论

JavaScript 是一种专为与网页交互而设计的脚本语言，由下列三个不同的部分组成：

1. ECMAScript，由 ECMA-262 定义，提供核心语言功能；

2. 文档对象模型（DOM），提供访问和操作网页内容的方法和接口；

3. 浏览器对象模型（BOM），提供与浏览器交互的方法和接口。

1『再往上抽象一层，前端的三大核心：JavaScript、 HTML 和 CSS。JavaScript 是与网页交互的脚本语言；HTML 是网页的格式（web 的核心语言）；CSS 是网页的样式。』

3『文档对象模型（DOM，Document Object Model）是针对 XML 但经过扩展用于 HTML 的应用程序编程接口（API，Application Programming Interface）。DOM 把整个页面映射为一个多层节点结构。HTML 或 XML 页面中的每个组成部分都是某种类型的节点，这些节点又包含着不同类型的数据。通过 DOM 创建的这个表示文档的树形图，开发人员获得了控制页面内容和结构的主动权。借助 DOM 提供的 API，开发人员可以轻松自如地删除、添加、替换或修改任何节点。』

3『使用 BOM 可以控制浏览器显示的页面以外的部分。而 BOM 真正与众不同的地方（也是经常会导致问题的地方），还是它作为 JavaScript 实现的一部分但却没有相关的标准。这个问题在 HTML5 中得到了解决，HTML5 致力于把很多 BOM 功能写入正式规范。HTML5 发布后，很多关于 BOM 的困惑烟消云散。由于没有 BOM 标准可以遵循，因此每个浏览器都有自己的实现。虽然也存在一些事实标准，例如要有 window 对象和 navigator 对象等，但每个浏览器都会为这两个对象乃至其他对象定义自己的属性和方法。现在有了 HTML5，BOM 实现的细节有望朝着兼容性越来越高的方向发展。』

JavaScript 的这三个组成部分，在当前五个主要浏览器（IE、Firefox、Chrome、Safari 和 Opera）中都得到了不同程度的支持。其中，所有浏览器对 ECMAScript 第 3 版的支持大体上都还不错，而对 ECMAScript 5 的支持程度越来越高，但对 DOM 的支持则彼此相差比较多。对 HTML5 已经正式纳入标准的 BOM 来说，尽管各浏览器都实现了某些众所周知的共同特性，但其他特性还是会因浏览器而异。

JavaScript 诞生于 1995 年。当时，它的主要目的是处理以前由服务器端语言（如 Perl）负责的一些输入验证操作。在 JavaScript 问世之前，必须把表单数据发送到服务器端才能确定用户是否没有填写某个必填域，是否输入了无效的值。Netscape Navigator 希望通过 JavaScript 来解决这个问题。在人们普遍使用电话拔号上网的年代，能够在客户端完成一些基本的验证任务绝对是令人兴奋的。毕竟，拨号上网的速度之慢，导致了与服务器的每一次数据交换事实上都成了对人们耐心的一次考验。

自此以后，JavaScript 逐渐成为市面上常见浏览器必备的一项特色功能。如今，JavaScript 的用途早已不再局限于简单的数据验证，而是具备了与浏览器窗口及其内容等几乎所有方面交互的能力。今天的 JavaScript 已经成为一门功能全面的编程语言，能够处理复杂的计算和交互，拥有了闭包、匿名（lamda，拉姆达）函数，甚至元编程等特性。作为 Web 的一个重要组成部分，JavaScript 的重要性是不言而喻的，就连手机浏览器，甚至那些专为残障人士设计的浏览器等非常规浏览器都支持它。当然，微软的例子更为典型。虽然有自己的客户端脚本语言 VBScript，但微软仍然在 Internet Explorer 的早期版本中加入了自己的 JavaScript 实现 1。

JavaScript 从一个简单的输入验证器发展成为一门强大的编程语言，完全出乎人们的意料。应该说，它既是一门非常简单的语言，又是一门非常复杂的语言。说它简单，是因为学会使用它只需片刻功夫；而说它复杂，是因为要真正掌握它则需要数年时间。要想全面理解和掌握 JavaScript，关键在于弄清楚它的本质、历史和局限性。

1『学习 JavaScript 的一个脉络：抓住其本质、历史和局限性。』

在 Web 日益流行的同时，人们对客户端脚本语言的需求也越来越强烈。那个时候，绝大多数因特网用户都使用速度仅为 28.8 kbit/s 的「猫」（调制解调器）上网，但网页的大小和复杂性却不断增加。为完成简单的表单验证而频繁地与服务器交换数据只会加重用户的负担。想象一下：用户填写完一个表单，单击「提交」按钮，然后等待 30 秒钟，最终服务器返回消息说有一个必填字段没有填好…… 当时走在技术革新最前沿的 Netscape 公司，决定着手开发一种客户端语言，用来处理这种简单的验证。

3『

原以为 web 是网页的意思。更正下，web 是万维网的简称，信息来源于《2018182世界是数字的》的第 10 章。

[网页 - 维基百科，自由的百科全书](https://zh.wikipedia.org/wiki/%E7%B6%B2%E9%A0%81)

网页（英语：web page）是一个适用于万维网和网页浏览器的文件，它存放在世界某个角落的某一部或一组计算机中，而这部计算机必须是与互联网相连。网页经由网址（URL）来识别与访问，当我们在网页浏览器输入网址后，经过一段复杂而又快速的程序，网页文件会被传送到用户家的计算机，然后再通过浏览器解释网页的内容，再展示给用户。是网络中的一「页」，通常是 HTML 格式，但现今已经有愈来愈多、各色各样的网页格式和标准出现。网页通常用图像档来提供图画。网页要透过网页浏览器来阅读。

网页通常有以下元素：文字数据、图像文件、Applet（在页面内运行的副程序）、超链接、客户端脚本、层叠样式表，网页的合成体称为网站，一个网站的开始点称为主页。

创建网页只需一个普通的文本编辑器，或特别的 HTML 编辑器即可。若要发布到万维网，便须 FTP 程序上传页面到网站服务器。也可用专门的工具软件。

当要将网页存入自己的电脑内，网页浏览器通常提供以下的选择：

1. 只存储网页的文字部分。

2. 完装封装，即连同该网页（HTML）所要用到的图像、Applet 和 JavaScript 等文件也一并封装存储。

3. 只有 HTML，不作任何改动；如果网页内的链接是相对链接，可能会令图片消失。

4. 只有 HTML，但将网页内链接到的文件改成绝对定义。

5. 有些网页浏览器容许在打印网页前预览，并可选择印底色与否，甚至放大、缩小。

』

当时就职于 Netscape 公司的布兰登·艾奇（Brendan Eich），开始着手为计划于 1995 年 2 月发布的 Netscape Navigator 2 开发一种名为 LiveScript 的脚本语言 —— 该语言将同时在浏览器和服务器中使用（它在服务器上的名字叫 LiveWire）。为了赶在发布日期前完成 LiveScript 的开发，Netscape 与 Sun 公司建立了一个开发联盟。在 Netscape Navigator 2 正式发布前夕，Netscape 为了搭上媒体热炒 Java 的顺风车，临时把 LiveScript 改名为 JavaScript。

微软推出其 JavaScript 实现意味着有了 3 个不同的 JavaScript 版本：Netscape Navigator 中的 JavaScript、Internet Explorer 中的 Jscript 和 ScriptEase 中的 CEnvi。与 C 及其他编程语言不同，当时还没有标准规定 JavaScript 的语法和特性，3 个不同版本并存的局面已经完全暴露了这个问题。随着业界担心的日益加剧，JavaScript 的标准化问题被提上了议事日程。

1997 年，以 JavaScript 1.1 为蓝本的建议被提交给了欧洲计算机制造商协会（Ecma，European Computer Manufacturers Association）。该协会指定 39 号技术委员会（TC39，Technical Committee #39）负责「标准化一种通用、跨平台、供应商中立的脚本语言的语法和语义」。TC39 由来自 Netscape、Sun、微软、Borland 及其他关注脚本语言发展的公司的程序员组成，他们经过数月的努力完成了 ECMA-262—— 定义一种名为 ECMAScript（发音为「ek-ma-script」）的新脚本语言的标准。

1『ECMAScript 是一个标准，其诞生是为了统一 JavaScript 脚本的语法和语义。』

第二年，ISO/IEC（International Organization for Standardization and International Electrotechnical Commission，国标标准化组织和国际电工委员会）也采用了 ECMAScript 作为标准（即 ISO/IEC-16262）。自此以后，浏览器开发商就开始致力于将 ECMAScript 作为各自 JavaScript 实现的基础，也在不同程度上取得了成功。

虽然 JavaScript 和 ECMAScript 通常都被人们用来表达相同的含义，但 JavaScript 的含义却比 ECMA-262 中规定的要多得多。没错，一个完整的 JavaScript 实现应该由下列三个不同的部分组成：核心（ECMAScript）；文档对象模型（DOM）；浏览器对象模型（BOM）。

1『原来 JavaScript 的范畴比 ECMAScript 要大。』

由 ECMA-262 定义的 ECMAScript 与 Web 浏览器没有依赖关系。实际上，这门语言本身并不包含输入和输出定义。ECMA-262 定义的只是这门语言的基础，而在此基础之上可以构建更完善的脚本语言。我们常见的 Web 浏览器只是 ECMAScript 实现可能的宿主环境之一。宿主环境不仅提供基本的 ECMAScript 实现，同时也会提供该语言的扩展，以便语言与环境之间对接交互。而这些扩展 —— 如 DOM，则利用 ECMAScript 的核心类型和语法提供更多更具体的功能，以便实现针对环境的操作。前面介绍过的 Node 以及众所周知的 Adobe Flash 也都是宿主环境。ECMAScript 就是对实现该标准规定的各个方面内容的语言的描述。JavaScript 实现了 ECMAScript，Adobe ActionScript 同样也实现了 ECMAScript。

1『Adobe Flash 如同浏览器一般，也可以在里面运行基于 ECMAScript 构建的脚本语言，其对应的脚本语言为 Adobe ActionScript。JavaScript 也是基于 ECMAScript 构建的脚本语言，但它专门为浏览器服务的。』

ECMAScript 的不同版本又称为版次，以第 x 版表示（即描述特定实现的 ECMA-262 规范的第 x 个版本）。ECMA-262 的最近一版是第 5 版，发布于 2009 年。而 ECMA-262 的第 1 版本质上与 Netscape 的 JavaScript 1.1 相同 —— 只不过删除了所有针对浏览器的代码并作了一些较小的改动：ECMA-262 要求支持 Unicode 标准（从而支持多语言开发），而且对象也变成了平台无关的（Netscape JavaScript 1.1 的对象在不同平台中的实现不一样，例如 Date 对象）。这也是 JavaScript 1.1 和 1.2 与 ECMA-262 第 1 版不一致的主要原因。

1『ECMA-262 第 1 版，是剔除 JavaScript 1.1 中与浏览器有关的代码后形成的标准。』

ECMA-262 第 2 版主要是编辑加工的结果。这一版中内容的更新是为了与 ISO/IEC-16262 保持严格一致，没有作任何新增、修改或删节处理。因此，一般不使用第 2 版来衡量 ECMAScript 实现的兼容性。

ECMA-262 第 3 版才是对该标准第一次真正的修改。修改的内容涉及字符串处理、错误定义和数值输出。这一版还新增了对正则表达式、新控制语句、try-catch 异常处理的支持，并围绕标准的国际化做出了一些小的修改。从各方面综合来看，第 3 版标志着 ECMAScript 成为了一门真正的编程语言。

ECMA-262 第 4 版对这门语言进行了一次全面的检核修订。由于 JavaScript 在 Web 上日益流行，开发人员纷纷建议修订 ECMAScript，以使其能够满足不断增长的 Web 开发需求。作为回应，ECMA TC39 重新召集相关人员共同谋划这门语言的未来。结果，出台后的标准几乎在第 3 版基础上完全定义了一门新语言。第 4 版不仅包含了强类型变量、新语句和新数据结构、真正的类和经典继承，还定义了与数据交互的新方式。

与此同时，TC39 下属的一个小组也提出了一个名为 ECMAScript 3.1 的替代性建议，该建议只对这门语言进行了较少的改进。这个小组认为第 4 版给这门语言带来的跨越太大了。因此，该小组建议对这门语言进行小幅修订，能够在现有 JavaScript 引擎基础上实现。最终，ES3.1 附属委员会获得的支持超过了 TC39，ECMAS-262 第 4 版在正式发布前被放弃。

ECMAScript 3.1 成为 ECMA-262 第 5 版，并于 2009 年 12 月 3 日正式发布。第 5 版力求澄清第 3 版中已知的歧义并增添了新的功能。新功能包括原生 JSON 对象（用于解析和序列化 JSON 数据）、继承的方法和高级属性定义，另外还包含一种严格模式，对 ECMAScript 引擎解释和执行代码进行了补充说明。

1『ECMAScript 3.1 胜出 ECMAScript 4，成为 ECMAScript 5，即 ES5。』

ECMA-262 给出了 ECMAScript 兼容的定义。要想成为 ECMAScript 的实现，则该实现必须做到：

1. 支持 ECMA-262 描述的所有「类型、值、对象、属性、函数以及程序句法和语义」（ECMA-262 第 1 页）；

2. 支持 Unicode 字符标准。

此外，兼容的实现还可以进行下列扩展：

1. 添加 ECMA-262 没有描述的「更多类型、值、对象、属性和函数」。ECMA-262 所说的这些新增特性，主要是指该标准中没有规定的新对象和对象的新属性。

2. 支持 ECMA-262 没有定义的「程序和正则表达式语法」。（也就是说，可以修改和扩展内置的正则表达式语法。）

上述要求为兼容实现的开发人员基于 ECMAScript 开发一门新语言提供了广阔的空间和极大的灵活性，这也从另一个侧面说明了 ECMAScript 受开发人员欢迎的原因。

文档对象模型（DOM，Document Object Model）是针对 XML 但经过扩展用于 HTML 的应用程序编程接口（API，Application Programming Interface）。DOM 把整个页面映射为一个多层节点结构。HTML 或 XML 页面中的每个组成部分都是某种类型的节点，这些节点又包含着不同类型的数据。看下面这个 HTML 页面：

通过 DOM 创建的这个表示文档的树形图，开发人员获得了控制页面内容和结构的主动权。借助 DOM 提供的 API，开发人员可以轻松自如地删除、添加、替换或修改任何节点。

在 Internet Explorer 4 和 Netscape Navigator 4 分别支持的不同形式的 DHTML（Dynamic HTML）基础上，开发人员首次无需重新加载网页，就可以修改其外观和内容了。然而，DHTML 在给 Web 技术发展带来巨大进步的同时，也带来了巨大的问题。由于 Netscape 和微软在开发 DHTML 方面各持己见，过去那个只编写一个 HTML 页面就能够在任何浏览器中运行的时代结束了。

对开发人员而言，如果想继续保持 Web 跨平台的天性，就必须额外多做一些工作。而人们真正担心的是，如果不对 Netscapet 和微软加以控制，Web 开发领域就会出现技术上两强割据，浏览器互不兼容的局面。此时，负责制定 Web 通信标准的 W3C（World Wide Web Consortium，万维网联盟）开始着手规划 DOM。

DOM1 级（DOM Level 1）于 1998 年 10 月成为 W3C 的推荐标准。DOM1 级由两个模块组成：DOM 核心（DOM Core）和 DOM HTML。其中，DOM 核心规定的是如何映射基于 XML 的文档结构，以便简化对文档中任意部分的访问和操作。DOM HTML 模块则在 DOM 核心的基础上加以扩展，添加了针对 HTML 的对象和方法。

请读者注意，DOM 并不只是针对 JavaScript 的，很多别的语言也都实现了 DOM。不过，在 Web 浏览器中，基于 ECMAScript 实现的 DOM 的确已经成为 JavaScript 这门语言的一个重要组成部分。

1『DOM 如同 ECMAScript 一样，不仅仅只针对 web 浏览器的脚本语言 JavaScript。』

如果说 DOM1 级的目标主要是映射文档的结构，那么 DOM2 级的目标就要宽泛多了。DOM2 级在原来 DOM 的基础上又扩充了（DHTML 一直都支持的）鼠标和用户界面事件、范围、遍历（迭代 DOM 文档的方法）等细分模块，而且通过对象接口增加了对 CSS（Cascading Style Sheets，层叠样式表）的支持。DOM1 级中的 DOM 核心模块也经过扩展开始支持 XML 命名空间。

1『首次出现了 CSS 概念，cascading style sheets。』

DOM3 级则进一步扩展了 DOM，引入了以统一方式加载和保存文档的方法 —— 在 DOM 加载和保存（DOM Load and Save）模块中定义；新增了验证文档的方法 —— 在 DOM 验证（DOM Validation）模块中定义。DOM3 级也对 DOM 核心进行了扩展，开始支持 XML 1.0 规范，涉及 XML Infoset、XPath 和 XML Base。

在阅读 DOM 标准的时候，读者可能会看到 DOM0 级（DOM Level 0）的字眼。实际上，DOM0 级标准是不存在的；所谓 DOM0 级只是 DOM 历史坐标中的一个参照点而已。具体说来，DOM0 级指的是 Internet Explorer 4.0 和 Netscape Navigator 4.0 最初支持的 DHTML。

在 DOM 标准出现了一段时间之后，Web 浏览器才开始实现它。微软在 IE5 中首次尝试实现 DOM，但直到 IE5.5 才算是真正支持 DOM1 级。在随后的 IE6 和 IE7 中，微软都没有引入新的 DOM 功能，而到了 IE8 才对以前 DOM 实现中的 bug 进行了修复。

Netscape 直到 Netscape 6（Mozilla 0.6.0）才开始支持 DOM。在 Netscape 7 之后，Mozilla 把开发重心转向了 Firefox 浏览器。Firefox 3 完全支持 DOM1 级，几乎完全支持 DOM2 级，甚至还支持 DOM3 级的一部分。（Mozilla 开发团队的目标是构建与标准 100% 兼容的浏览器，而他们的努力也得到了回报。）目前，支持 DOM 已经成为浏览器开发商的首要目标，主流浏览器每次发布新版本都会改进对 DOM 的支持。下表列出了主流浏览器对 DOM 标准的支持情况。

Internet Explorer 3 和 Netscape Navigator 3 有一个共同的特色，那就是支持可以访问和操作浏览器窗口的浏览器对象模型（BOM，Browser Object Model）。开发人员使用 BOM 可以控制浏览器显示的页面以外的部分。而 BOM 真正与众不同的地方（也是经常会导致问题的地方），还是它作为 JavaScript 实现的一部分但却没有相关的标准。这个问题在 HTML5 中得到了解决，HTML5 致力于把很多 BOM 功能写入正式规范。HTML5 发布后，很多关于 BOM 的困惑烟消云散。

从根本上讲，BOM 只处理浏览器窗口和框架；但人们习惯上也把所有针对浏览器的 JavaScript 扩展算作 BOM 的一部分。下面就是一些这样的扩展：弹出新浏览器窗口的功能；移动、缩放和关闭浏览器窗口的功能；提供浏览器详细信息的 navigator 对象；提供浏览器所加载页面的详细信息的 location 对象；提供用户显示器分辨率详细信息的 screen 对象；对 cookies 的支持；像 XMLHttpRequest 和 IE 的 ActiveXObject 这样的自定义对象。

由于没有 BOM 标准可以遵循，因此每个浏览器都有自己的实现。虽然也存在一些事实标准，例如要有 window 对象和 navigator 对象等，但每个浏览器都会为这两个对象乃至其他对象定义自己的属性和方法。现在有了 HTML5，BOM 实现的细节有望朝着兼容性越来越高的方向发展。第 8 章将深入讨论 BOM。

作为 Netscape「继承人」的 Mozilla 公司，是目前唯一还在沿用最初的 JavaScript 版本编号序列的浏览器开发商。在 Netscape 将源代码提交给开源的 Mozilla 项目的时候，JavaScript 在浏览器中的最后一个版本号是 1.3。（如前所述，1.4 版是只针对服务器的实现。）后来，随着 Mozilla 基金会继续开发 JavaScript，添加新的特性、关键字和语法，JavaScript 的版本号继续递增。下表列出了 Netscape/Mozilla 浏览器中 JavaScript 版本号的递增过程：

实际上，上表中的编号方案源自 Firefox 4 将内置 JavaScript 2.0 这一共识。因此，2.0 版之前每个递增的版本号，表示的是相应实现与 JavaScript 2.0 开发目标还有多大的距离。虽然原计划是这样，但 JavaScript 的这种发展速度让这个计划成为不再可行。目前，JavaScript 2.0 还没有目标实现。

请注意，只有 Netscape/Mozilla 浏览器才遵循这种编号模式。例如，IE 的 JScript 就采用了另一种版本命名方案。换句话说，JScript 的版本号与上表中 JavaScript 的版本号之间不存在任何对应关系。而且，大多数浏览器在提及对 JavaScript 的支持情况时，一般都以 ECMAScript 兼容性和对 DOM 的支持情况为准。

## 02. 在 HTML 中使用 JavaScript

### 1. 逻辑脉络

JavaScript 插入到 HTML 页面中要使用 script 元素。使用这个元素可以把 JavaScript 嵌入到 HTML 页面中，让脚本与标记（HTML）混合在一起而不会影响页面在其他浏览器中的呈现效果；也可以包含外部的 JavaScript 文件。

### 2. 摘录及评论

把 JavaScript 插入到 HTML 页面中要使用 script 元素。使用这个元素可以把 JavaScript 嵌入到 HTML 页面中，让脚本与标记混合在一起；也可以包含外部的 JavaScript 文件。而我们需要注意的地方有：

1. 在包含外部 JavaScript 文件时，必须将 src 属性设置为指向相应文件的 URL。而这个文件既可以是与包含它的页面位于同一个服务器上的文件，也可以是其他任何域中的文件。

2. 所有 script 元素都会按照它们在页面中出现的先后顺序依次被解析。在不使用 defer 和 async 属性的情况下，只有在解析完前面 script 元素中的代码之后，才会开始解析后面 script 元素中的代码。

3. 由于浏览器会先解析完不使用 defer 属性的 script 元素中的代码，然后再解析后面的内容，所以一般应该把 script 元素放在页面最后，即主要内容后面，</body> 标签前面。

4. 使用 defer 属性可以让脚本在文档完全呈现之后再执行。延迟脚本总是按照指定它们的顺序执行。

5. 使用 async 属性可以表示当前脚本不必等待其他脚本，也不必阻塞文档呈现。不能保证异步脚本按照它们在页面中出现的顺序执行。

另外，使用 <noscript> 元素可以指定在不支持脚本的浏览器中显示的替代内容。但在启用了脚本的情况下，浏览器不会显示 <noscript> 元素中的任何内容。

1『JavaScript 的代码在 HTML 里，都必须在 <script></script> 构成的框架里。』

只要一提到把 JavaScript 放到网页中，就不得不涉及 Web 的核心语言 ——HTML。在当初开发 JavaScript 的时候，Netscape 要解决的一个重要问题就是如何做到让 JavaScript 既能与 HTML 页面共存，又不影响那些页面在其他浏览器中的呈现效果。经过尝试、纠错和争论，最终的决定就是为 Web 增加统一的脚本支持。而 Web 诞生早期的很多做法也都保留了下来，并被正式纳入 HTML 规范当中。

向 HTML 页面中插入 JavaScript 的主要方法，就是使用 script 元素。这个元素由 Netscape 创造并在 Netscape Navigator 2 中首先实现。后来，这个元素被加入到正式的 HTML 规范中。HTML 4.01 为 script 定义了下列 6 个属性。

1. async：可选。表示应该立即下载脚本，但不应妨碍页面中的其他操作，比如下载其他资源或等待加载其他脚本。只对外部脚本文件有效。

2. charset：可选。表示通过 src 属性指定的代码的字符集。由于大多数浏览器会忽略它的值，因此这个属性很少有人用。

3. defer：可选。表示脚本可以延迟到文档完全被解析和显示之后再执行。只对外部脚本文件有效。IE7 及更早版本对嵌入脚本也支持这个属性。

4. language：已废弃。原来用于表示编写代码使用的脚本语言（如 JavaScript、JavaScript1.2 或 VBScript）。大多数浏览器会忽略这个属性，因此也没有必要再用了。

5. src：可选。表示包含要执行代码的外部文件。

6. type：可选。可以看成是 language 的替代属性；表示编写代码使用的脚本语言的内容类型（也称为 MIME 类型）。虽然 text/javascript 和 text/ecmascript 都已经不被推荐使用，但人们一直以来使用的都还是 text/javascript。实际上，服务器在传送 JavaScript 文件时使用的 MIME 类型通常是 application/x–javascript，但在 type 中设置这个值却可能导致脚本被忽略。另外，在非 IE 浏览器中还可以使用以下值：application/javascript 和 application/ecmascript。考虑到约定俗成和最大限度的浏览器兼容性，目前 type 属性的值依旧还是 text/javascript。不过，这个属性并不是必需的，如果没有指定这个属性，则其默认值仍为 text/javascript。

1『HTML 规范专门为 script 定义的 6 个属性。』

使用 script 元素的方式有两种：直接在页面中嵌入 JavaScript 代码和包含外部 JavaScript 文件。在使用 script 元素嵌入 JavaScript 代码时，只须为 script 指定 type 属性。然后，像下面这样把 JavaScript 代码直接放在元素内部即可：

```
<script type="text/javascript">
  function sayHi(){ 
    alert("Hi!"); } 
</script>
```

包含在 script 元素内部的 JavaScript 代码将被从上至下依次解释。就拿前面这个例子来说，解释器会解释到一个函数的定义，然后将该定义保存在自己的环境当中。在解释器对 script 元素内部的所有代码求值完毕以前，页面中的其余内容都不会被浏览器加载或显示。在使用 script 嵌入 JavaScript 代码时，记住不要在代码中的任何地方出现 "</script>" 字符串。例如，浏览器在加载下面所示的代码时就会产生一个错误：

因为按照解析嵌入式代码的规则，当浏览器遇到字符串 "</script>" 时，就会认为那是结束的 </script> 标签。而通过转义字符「\」把这个字符串分隔为两部分可以解决这个问题，例如：

像这样分成两部分来写就不会造成浏览器的误解，因而也就不会导致错误了。

如果要通过 script 元素来包含外部 JavaScript 文件，那么 src 属性就是必需的。这个属性的值是一个指向外部 JavaScript 文件的链接，例如：

    <script type="text/javascript" src="example.js"></script>

在这个例子中，外部文件 example.js 将被加载到当前页面中。外部文件只须包含通常要放在开始的 script 和结束的 </script> 之间的那些 JavaScript 代码即可。与解析嵌入式 JavaScript 代码一样，在解析外部 JavaScript 文件（包括下载该文件）时，页面的处理也会暂时停止。如果是在 XHTML 文档中，也可以省略前面示例代码中结束的 </script> 标签，例如：

    <script type="text/javascript" src="example.js" />

但是，不能在 HTML 文档使用这种语法。原因是这种语法不符合 HTML 规范，而且也得不到某些浏览器（尤其是 IE）的正确解析。

按照惯例，外部 JavaScript 文件带有 .js 扩展名。但这个扩展名不是必需的，因为浏览器不会检查包含 JavaScript 的文件的扩展名。这样一来，使用 JSP、PHP 或其他服务器端语言动态生成 JavaScript 代码也就成为了可能。但是，服务器通常还是需要看扩展名决定为响应应用哪种 MIME 类型。如果不使用 .js 扩展名，请确保服务器能返回正确的 MIME 类型。

1『直觉上这是一个关键点。』

需要注意的是，带有 src 属性的 script 元素不应该在其 script 和 </script> 标签之间再包含额外的 JavaScript 代码。如果包含了嵌入的代码，则只会下载并执行脚本文件，嵌入的代码会被忽略。

另外，通过 script 元素的 src 属性还可以包含来自外部域的 JavaScript 文件。这一点既使 script 元素倍显强大，又让它备受争议。在这一点上，script 与 <img> 元素非常相似，即它的 src 属性可以是指向当前 HTML 页面所在域之外的某个域中的 URL，例如：

    <script type="text/javascript" src="http://www.somewhere.com/afile.js"></script>

这样，位于外部域中的代码也会被加载和解析，就像这些代码位于加载它们的页面中一样。利用这一点就可以在必要时通过不同的域来提供 JavaScript 文件。不过，在访问自己不能控制的服务器上的 JavaScript 文件时则要多加小心。如果不幸遇到了怀有恶意的程序员，那他们随时都可能替换该文件中的代码。因此，如果想包含来自不同域的代码，则要么你是那个域的所有者，要么那个域的所有者值得信赖。

无论如何包含代码，只要不存在 defer 和 async 属性，浏览器都会按照 script 元素在页面中出现的先后顺序对它们依次进行解析。换句话说，在第一个 script 元素包含的代码解析完成后，第二个 script 包含的代码才会被解析，然后才是第三个、第四个……












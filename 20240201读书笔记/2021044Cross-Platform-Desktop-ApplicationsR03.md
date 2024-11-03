## 记忆时间

## 目录

0501 Using Node.js within NW.js and Electron

0601 Exploring NW.js and Electron's internals

## Part 2 Diving deeper

After building a file explorer app with both NW.js and Electron, we'll take a step back and cast our eyes on the programming framework behind them: Node.js. You'll learn about its origins, how it works, and how it implements asynchronous programming. Then, we'll explore some of Node.js's key concepts such as callbacks, streams, events, and modules.

In chapter 6, we'll continue on this theme by looking at how NW.js and Electron operate under the hood. You'll see how the frameworks approach integrating Node.js with Chromium, how they handle managing state between the frontend and back-end parts of the app, and how they're structured.

By the end of this part, you should be a in a good position to put Node.js to use in your desktop app as well as other Node.js apps, and you'll understand how NW.js and Electron differ in their approaches to desktop app development.

第 2 部分 深度剖析

使用 NW.js 和 Electron 构建完文件浏览器应用后，我们后退一步，把目光放到这两个框架背后的编程框架 Node.js 上。你会学到关于它的「身世」、工作原理，以及它是如何实现异步编程的。然后我们还会介绍一些 Node.js 中的关键概念，如，回调、流、事件以及模块。在第 6 章中，我们会继续讨论这个主题，来看看 NW.js 和 Electron 的工作原理。你会了解到这两个框架是如何将 Node.js 和 Chromium 结合在一起的、它们是如何管理应用中前后端代码的状态以及如何组织代码的。通过这部分内容的学习，你就可以使用 Node.js 来开发桌面应用以及其他 Node.js 应用了。除此之外，你还会了解到 NW.js 和 Electron 在实现桌面应用开发方式上有何不同。

## 0501. Using Node.js within NW.js and Electron

### Summary

This chapter presented a broad introduction to Node.js. Now you have a better understanding of what it's like to use as a programming framework, and you'll be able to start implementing it in your apps. Things that you'll want to take away from this chapter include the following:

1 Node.js uses asynchronous programming. Make sure to structure your code to use callbacks and streams when interacting with Node.js' APIs and modules.

2 Streams are an effective way to read/write data without using much memory.

3 Some of the browsers' APIs overlap with Node.js's APIs. Note when you use them because they will have subtle differences.

4 Use npm modules to install libraries that will help you build app features faster. 

5 You can publish modules to npm to share your libraries with the community.

In chapter 6, we'll turn our attention back to NW.js and Electron and take a look at how they operate under the hood, so you can understand how they work differently.

本章介绍了 Node.js 的知识。通过本章讲述的内容，你已经对 Node.js 作为一门编程框架，如何使用它有了一个很好的理解，而且你也可以用它来开发你的应用了。本章你学到的内容包括：

1、Node.js 使用了异步编程模式。当使用 Node.js 的 API 以及模块的时候，确保将你的代码组织成使用回调函数以及流。

2、流是一种高效读写数据的方式，而且不会占用太多内存。

3、在 Node.js API 中，有些 API 和浏览器的 API 是有重合的。当使用这些 API 的时候要注意，因为它们实际上会有一点不同。

4、使用 npm 安装模块可以帮助你更快地开发应用功能。

5、可以通过 npm 进行模块发布，将它分享给社区。

在第 6 章，我们会将注意力回到 NW.js 和 Electron 上，介绍它们背后的运行机制是怎样的，这样你会对它们工作方式的不同有更好的认识。

### 5.0

This chapter covers: 1) Exploring Node.js. 2) Understanding the asynchronous nature of Node.js. 3) Managing events and streams. 4) Installing and using npm modules. 5) Packaging your apps with npm.

Long before NW.js and Electron, a programming framework called Node.js was demoed by Ryan Dahl at JSConf in Berlin, showing a way to write and execute server-side JavaScript. Since that demo back in 2009, Node.js has spawned a huge ecosystem of libraries, applications, utilities, and frameworks (including NW.js and Electron). As a programming framework, it offers a different approach compared with other programming languages and their frameworks.

For those new to the world of Node.js, this chapter offers a gentle introduction to the programming framework and a chance to learn how to apply it not only when developing desktop apps, but also in other projects such as web apps. For those already familiar with Node.js, this chapter covers a lot of the ground that you might already be familiar with (the event loop, callbacks, streams, and node modules), so feel free to skip it.

One of the underrated features of both NW.js and Electron is the massive collection of packages available through Node.js's package management tool, npm, that can be used for building desktop apps. This chapter will show how you can put Node.js to use when developing your desktop apps, as well as for organizing your code.

在 NW.js 和 Electron 中使用 Node.js

本章要点：1）介绍 Node.js。2）理解 Node.js 中的异步特性。3）管理事件和流。4）安装并使用 npm 模块。5）使用 npm 打包你的应用。

早在 NW.js 和 Electron 出现之前，Ryan Dahl 在柏林的 JSConf 大会上演示了一款名为 Node.js 的编程框架，展示了一种书写和执行服务端 JavaScript 的方法。自 2009 年那个演示之后，Node.js 已经衍生出了一个庞大的生态系统，其中包含用它开发的库、应用、工具以及框架（其中包括 NW.js 和 Electron）。作为一个编程框架，相比其他的编程语言及框架，Node.js 提供了一种不同的思路。

对 Node.js 完全陌生的读者，本章会对该编程框架做一个简单的介绍，还会介绍如何在开发桌面应用时以及其他诸如 Web 应用这样的项目中使用 Node.js。对 Node.js 熟悉的读者，本章介绍的很多基本概念（事件循环、回调、流以及 node 模块）你可能都已经了解了，那你可以跳过本章。

NW.js 和 Electron 中一项被人低估的特性就是有大量可以通过 Node.js 包管理工具 npm 安装的模块，这些都可以在构建桌面应用的时候使用。本章将介绍如何在开发桌面应用的过程中使用 Node.js 以及如何组织你的代码。

### 5.1 What is Node.js?

Node.js is a programming framework created by Ryan Dahl back in 2009. It provides a way to write server-side programs with JavaScript and uses an evented architecture to handle the execution of that code. The programming framework combines V8 (a JavaScript engine) with libuv, a library that provides access to the OS libraries in an asynchronous fashion.

Because of this, JavaScript code is executed by Node.js in such a way that code executing on one line doesn't block the execution of the code on the next line. This is distinctly different from other languages where code on one line executes after the code on the previous line has finished executing. It's important to get familiar with how Node.js handles executing code. You'll tackle this in the next section.

1『这里对 Node.js 的解释做一张术语卡片。（2021-04-16）』—— 已完成

5.1 什么是 Node.js

Node.js 是一个由 Ryan Dahl 在 2009 年创建的编程框架。它提供了一种使用 JavaScript 来编写服务端程序的方法，并且使用基于事件的架构来处理代码的执行。该编程框架整合了 V8（一种 JavaScript 引擎）和 libuv（一种编程库），提供了异步的方式来调用操作系统资源。

正因如此，通过 Node.js 执行的 JavaScript 代码之间可以做到不阻塞对方。这是和其他语言相比最大的不同点，在其他语言中，一行代码执行完毕后才能执行下一行代码。了解 Node.js 如何处理代码执行这一点非常重要。下一节会做更多介绍。

#### 5.1.1 Synchronous versus asynchronous

To clearly differentiate between synchronous and asynchronous programming, let's revisit the case of reading the contents of a folder using Node.js and compare it to how it can be done with Ruby. Ruby is a programming language with a simple syntax that works in a synchronous fashion, making it a good example to compare Node.js against. Here's an example written in Ruby:

```c
files = Dir.entries '/Users/pauljensen' 
puts files.length
```

This is a nice example that demonstrates the appeal of Ruby — the clean syntax. In this case, the first line executes, and then the second line executes when the first line has finished. This is known as blocking. If I were to insert the following between lines 1 and 3,

```
sleep 5
```

that line would cause the program to block for 5 seconds before printing out the number of files in the list. Figure 5.1 illustrates how that executes in time.

We refer to this as synchronous programming — each operation waits on the previous operation to complete. There may be cases where you want to start doing something else while you're waiting for the list of files to be counted, but can't because the previous line hasn't finished yet.

Figure 5.1 synchronous

A diagram showing how Ruby's execution of code is

The following listing shows you can do the same thing as the Ruby example in a synchronous fashion in Node.js.

Listing 5.1 Synchronous files count in Node.js

```js
const fs = require('fs')
// Gets the list of files in the directory
const files = fs.readdirSync('/Users/pauljensen') 
// Counts how many files there are
console.log(files.length)
```

Though this isn't as elegant as the Ruby code example, it does exactly the same thing. Notice that the call to the file system API's readdirSync function has the word Sync attached to the end of it. This is to make clear that the function operates in a synchronous fashion. You would still have the issue of blocking code that delays the execution of other code until it has completed its operation.

What is needed is a way to fire off an operation, let it go off and do what it's doing, and then when it's ready to return some data, send that data to another function, or a callback, as it's commonly referred to in Node.js. The next listing shows an example of the same task using asynchronous Node.js.

Listing 5.2 Asynchronous files count in Node.js

You can see that the code to log out the number of files in the folder is inside a function (the callback). This function will execute the moment the readdir function has either returned an error (as the err object) or the list of files. Figure 5.2 shows an alternative way to visualize it.

1 Look up the directory.

2 Start doing other things that aren't waiting on the results of the directory look-up.

3 Get the results of the directory look-up.

4 Great! Pass those results to the function that was waiting to process them.

Figure 5.2 Asynchronous programming's flow of execution

1『上图的信息其实不是按顺序来的，原书里有一个图。（2021-04-16）』

Any code that's placed after the callback function on the next line will execute immediately. For example, you can place a simple line to log out a message after the callback, such as this:

```js
const fs = require('fs')

fs.readdir('/Users/pauljensen', (err, files) => {
  if (err) return err.message
  console.log(files.length)
})
console.log('hi')
```

When you run this with Node.js, you should see the following result in Terminal or Command Prompt:

```
hi 

56
```

You'll notice that the console.log statement executed before the file count did, even though it was placed after it in the code. This is one of the aspects of asynchronous programming that newcomers to Node.js initially struggle to get their head around. The best way to illustrate it is with a diagram like figure 5.3.

If you've worked with Gantt charts in project management, figure 5.3 might be familiar to you. Whereas synchronous execution mirrors the typical waterfall flow of a sub-optimal project plan, asynchronous execution mirrors the flow of a project where multiple tasks can run in parallel, and the project completes faster as a result. It's important to keep this in mind when working with Node.js. It's one of the bigger concepts to digest when you first start working with it — otherwise, the code will execute in an order different from what you expect, and that can lead to confusion and loss of time.

Figure 5.3 Comparison of the ways in which synchronous and asynchronous differ in the time order of executing code.

5.1.1 同步与异步

为了更好地区分同步编程和异步编程，我们再来回忆一下使用 Node.js 读取文件夹内容的例子，将它和 Ruby 版本的进行对比。Ruby 是一门语法简练的同步编程语言，用它来和 Node.js 进行对比再好不过了。下面是一个 Ruby 写的例子：

这个例子充分展现了 Ruby 的魅力  —  —  简练的语法。在上述代码中，第一行代码执行完毕后，第二行代码才能开始执行。这就是所谓的阻塞。如果我在第一行和第三行代码中间插入如下代码：

```
sleep 5
```

上述代码在代码实现打印出文件列表个数之前让程序阻塞了 5 秒。图 5.1 展示了其执行时序。

我们将其称为同步编程  —  —  每一个操作都必须等上一个操作完成后才能开始。有的时候，你可能在读取文件列表的过程中还想做点别的操作，但这在同步编程中无法实现，因为你必须要等上一行代码执行完才能继续下一行。

图 5.1 展示了 Ruby 是如何同步执行代码的

代码清单 5.1 展示了如何通过同样的同步方式在 Node.js 中实现与 Ruby 代码同样的功能。

代码清单 5.1 在 Node.js 中以同步的方式获取文件列表个数

尽管上述代码没有 Ruby 代码那么优雅，但是效果是完全一样的。注意，上述代码中调用文件系统 API 的 readdirSync 函数，其后缀有一个 Sync 单词。这是为了清楚地表达该函数是以同步方式执行的。所以还是会有阻塞的情况发生，其他代码必须要等到该操作完成后才能开始。

理想的情况是，触发读取目录内容的操作，然后就让它去处理吧，我们可以继续进行其他操作。当该操作结束后，将数据返回到另外一个函数中，也叫回调，在 Node.js 中通常这么称呼。代码清单 5.2 展示了使用 Node.js 以异步的方式完成相同的操作。

代码清单 5.2 Node.js 读取文件数量的异步版本

在上述代码中你可以看到，打印出文件夹中的文件数量这部分代码是写在函数（回调函数）里面的。该函数会在 readdir 函数结束后，不管是发生了错误（err 对象）或者成功获取到了文件列表后执行。图 5.2 以另一种形式展示了上述代码的执行情况。

图 5.2 代码异步执行流程

任何在回调函数下面的代码会立即被执行。举一个例子，你可以直接在回调函数下方简单地打印一段消息，就像这样：

当使用 Node.js 运行上述代码时，你能从终端程序或者命令提示符程序中看到如下结果：

你会发现 console.log 这行语句在打印文件数量之前就执行了，尽管这行代码是写在后面的。这只是异步编程的特点之一，对于 Node.js 新手来说往往会不太适应。图 5.3 很好地展示了异步代码的执行情况。

如果你用过软件管理中的甘特图，那么对图 5.3 应该不会陌生。同步执行类似于典型的项目计划中的瀑布流模型，而异步执行类似于项目开发流程中的多任务并行模型，这种方式最终可以加快项目进度。这个概念在 Node.js 编程中是非常重要的。当你刚开始接触 Node.js 时，这点是需要搞清楚的概念之一，否则代码不按照你的预期执行，会让你陷入困惑，浪费很多时间。

图 5.3 同步执行和异步执行代码时序区别对比图

#### 5.1.2 Streams as first-class citizens

Another aspect of Node.js is the way that it encourages you to use streams as a method of handling data within your apps. This has the benefit of allowing you to handle transmitting and processing large amounts of data without requiring large amounts of memory. Cases where you would want to do this include uploading large files to Amazon S3 or reading a big JSON file containing addresses and filtering the data to return only a subset that's then written to a file. When developing any kind of app, it's important to ensure that it's efficient in its memory usage — otherwise, it will slow down the computer it's running on and eventually stop working, as illustrated in figure 5.4.

In figure 5.4, you can see how loading entire files into memory can become problematic. Now, you might say that there's little chance you'll be loading a file that's bigger than the amount of RAM on a server, but when a server's amount of free RAM is used up over time, a small file bigger than the amount of free RAM can end up being the straw that breaks the camel's back.

1 You have a large log file that fits on the server's hard disk.

2 The server has enough disk space to keep the file, but not enough RAM to load it into memory.

3 Someone runs a job to process the file, which loads the file into memory. The process fails when the server runs out of memory.

Figure 5.4 How loading a large file for processing creates pitfalls if the file is larger than total RAM available or the amount of memory free in the server

1『上图里的信息其实不是按顺序来的，原书里有一个图。（2021-04-16）』

What can you do about this? You can use streams to load the file, a bit at a time, as you can see by looking at the following example of using streams in Node.js.

Let's say you have a text document that you want to scan the contents of for a particular term, but it's large, and loading all of it in memory isn't ideal. What you would like to do is load the text document in chunks and scan each chunk for the term. If the term is found, you record that the term is in the text document — otherwise, you conclude that you have yet to find the term in the text document. This is a live search of a text document, where the contents of the text document are not indexed.

Find a book you like that's available online — I'll pick Frank Herbert's Dune (a great book). Let's take a phrase from the end of the book, in this case, history will call you wives. You want to scan the book for this term, but you don't want to load the whole book's contents into memory in order to find it. Instead, you'll load it chunk by chunk until you come across the term and can verify that it appears in the book. (You can get a copy of the book from http://mng.bz/9sOS.)

1-3『又获得了一个免费图书的网站：[Internet Archive: Digital Library of Free & Borrowable Books, Movies, Music & Wayback Machine](https://archive.org/)。』

You can use Node's file system API to help you read the contents of the file as a stream with the following code.

Listing 5.3 Streaming a book's contents

```js
'use strict'

const fs = require('fs')

// Creates readable stream of book file

const filePath = '/Users/pauljensen/Desktop/Frank-Herbert-Dune.rtfd/TXT.rtf'

const fileReader = fs.createReadStream(filePath, {encoding:'utf8'})
let termFound = false

fileReader.on('data', (data) => { 
  if (data.match(/history will call you wives/) !== null) termFound = true
})

fileReader.on('end', (err) => { 
  if (err) return err
  console.log('term found:',termFound)
})
```

You create a readable stream for a rich text file, and tell it to expect the contents of the file to be encoded in UTF-8. Then, you attach a callback function to the data event so that every time a piece of data is read from the file, you check whether the term is contained in that piece of data. If it is, you set the termFound variable to true — otherwise, it remains set to false.

When the readable stream has finished reading the contents of the file, it will emit an end event, to which you attach a callback function where you either return an error object or log whether the term was found.

If you run the example code along with the text of the book in your terminal, you can expect to see the following result in your terminal:

```
$> node findTerm.js 
=> term found: true
```

1『这里学到了一个关键知识点：Node 环境里可以直接跑 JS 文件，大赞。（2021-04-17）』


What you've achieved here is a way to read a Rich Text Format (RTF) document and find a term within. But you could have done the same thing with less code by using the file system API's readFile function, with the code shown next.

Listing 5.4 Term finding with Node.js's fs.readFile function

```js
'use strict'

const fs = require('fs')
const filePath = '/Users/pauljensen/Desktop/Frank-Herbert-Dune.rtfd/TXT.rtf'
let termFound = false

fs.readFile(filePath, {encoding: 'utf8'}, (err, data) => { 
  if (err) return err
  if (data.match(/history will call you wives/) !== null) termFound = true
  console.log('term found:',termFound)
})
```

This example achieves the same result but only requires one callback function rather than two callbacks for the readable stream version. So, why would you use streams over the simpler fs.readFile method? 98

The answer is speed. Streaming the contents of a file with fs.createReadStream completes faster than attempting to read the contents of a file with fs.readFile. You can try this out by using Node's process.hrtime function to measure the time it takes for the process to complete. Adjust the previous examples so they include the following line at the top of each file:

```js
const startTime = process.hrtime()
```

Then, include the following lines after the console.log statement printing whether the term was found:

```js
const diff = process.hrtime(startTime)
console.log('benchmark took %d nanoseconds', diff[0] * 1e9 + diff[1])
```

Here, calling the process.hrtime function without any arguments records a timestamp, which you store as the startTime variable. After creating this variable, you compare it to a later time, after the code has finished reading the contents of the Rich Text Format document and printed out whether the term was found. By passing the startTime variable into the process.hrtime function, you get back the difference between now and that startTime as a tuple of seconds and nanoseconds. You then print the time difference using console.log, allowing you to see how long it took to read the contents of the document with both approaches.

Your results may vary, but in running them on my laptop (a 13-inch mid-2014 MacBook Pro with 16 GB RAM and a 3 GHz processor), I get the results shown in table 5.1.

Table 5.1 Streaming saves time

| API function | Time taken |
| --- | --- |
| fs.readFile | 62.61 milliseconds |
| fs.createReadStream | 21.59 milliseconds |

You can see that in this test run, the streaming function is almost three times as fast as the fs.fileRead function (usually, for reliable metrics you would do lots of test runs and measure the standard deviation and variance between each function's results, but that's beyond the scope of this book). This result varies only slightly between multiple test runs.

Structuring your code to make use of streams will allow for it to execute faster and be more efficient with memory. You can see this for yourself by tracking the memory usage of both approaches using Node's process.memoryUsage function in the code examples. In the code examples, after they have finished reading the data of the document, insert the following line of code:

```js
console.log(process.memoryUsage())
```

When you add this line to both the streaming-read and full-read examples and then run them, you should see this output for the full fs.readFile example:

```json
{ rss: 36184064, heapTotal: 20658336, heapUsed: 16310280 }
```

And for the streaming file example:

```json
{ rss: 18276352, heapTotal: 6163968, heapUsed: 2869000 }
```

What's noticeable already is that the memory usage numbers are smaller in the streaming file code than in the full readFile code (49% smaller RSS, 70% smaller heapTotal, and 82% smaller heapUsed). Not only are streams faster, they're more memory efficient, too.

5.1.2 流是一等公民

Node.js 中还有一个概念就是它鼓励在应用中进行流式（steam）数据处理的方式。这种方式有一个好处就是当你要对大量数据进行转换和处理的时候，不需要大量的内存。举一个例子，上传一个大文件到亚马逊 S3 平台或者读取一个包含地址信息的大 JSON 文件并对其进行过滤后将结果保存到磁盘文件中。在进行应用部署的时候，确保内存的高效使用是非常重要的，否则会拖慢计算机的运行并最终导致暂停工作，如图 5.4 所示。

如图 5.4 所示，将整个文件加载到内存中会有很多问题。你可能会反驳说，在服务器上加载一个比服务器内存还要大的文件，这种情况非常少，但是，在服务器可用内存过度使用的情况下，任何一个小文件，只要超过可用内存大小都会成为压死骆驼的最后那根稻草。

图 5.4 当加载一个大小超过服务器内存或者可用内存的文件时，会引发问题

面对这种情况该怎么办呢？你可以使用流来加载文件，一次加载一部分，通过下面在 Node.js 中使用流的例子，你会对其有更深入的了解。

假设有一个文本文件，你想在其中搜索某个特定的关键词，但是这个文件非常大，将它完全加载到内存中再处理不现实。更好的办法是加载文本文件其中的一块数据，然后对这块数据进行扫描。如果找到了，就认为该文档中包含这个关键词，反之，则表示文档中没有该关键词。这是实时查询，并没有对文档内容进行索引。

在网上找一本你喜欢的书 —— 我选 Frank Herbert 的《沙丘》（一本非常好的书）。我们从书的结尾部分选择一段话，history will call you wives。你想要从书中搜索这段话，但又不想将整本书的内容加载到内存中后再进行搜索。取而代之的是，你把数据一块一块地进行加载，直到找到这段话即认为它在书中出现了（可以从 http://mng.bz/9sOS 下载到这本书）。

可以使用 Node.js 的文件系统 API 来帮助你以流的方式读取文件内容，如代码清单 5.3 所示。

代码清单 5.3 使用流来获取书的内容

在上述代码中，针对富文本文件创建了一个可读的流，并告知文件内容的编码方式为 UTF-8。紧接着，监听了流的 data 事件，传递了一个回调函数，这样就可以对每一块内容进行检查，是否包含要查找的句子。如果找到了，就将 termFound 设置为 true—— 反之，则设置为 false。

当可读流读取完文件内容之后，它会发出一个 end 事件，你可以监听该事件并传递一个回调函数，并在函数中要么返回抛出的错误，要么将查找结果打印出来。

如果在终端程序中运行上述示例代码，就会在终端程序中看到如下结果：

你已经学会了如何读取一个富文本文件的内容并在其中查找特定的句子。事实上，你可以使用文件系统 API 中的 readFile 函数，以更少的代码来完成同样的功能，如代码清单 5.4 所示。

代码清单 5.4 使用 Node.js 的 fs.readFile 函数来查找特定的句子

上述例子完成了同样的功能，但是相比可读流版本用到了两个回调函数，这个版本只用了一个回调函数。那么为什么我们还要用流而不是更简单的 fs.readFile 方法呢？

答案是为了速度。使用 fs.createReadStream 来对文件内容进行流式处理要比使用 fs.readFile 读取文件内容更快。你可以通过 Node.js 的 process.hrtime 函数来测试所需要的时间。修改上述两段代码，在每个文件的顶部添加如下代码：

然后，在 console.log 打印查找结果的语句下方添加如下代码：

这里，不带任何参数调用 process.hrtime 函数会生成一个时间戳，将其保存在 startTime 变量中。创建完这个变量后，将它和后续的一个时间点进行比较，该时间点为读完富文本文件内容并打印出查找结果的时间。通过将 startTime 传递给 process.hrtime 函数，你会得到当前时间点和 startTime 的差值，单位为秒或纳秒。然后通过 console.log 将这段时间打印出来，这样就能看到这两种方案读取文档内容分别需要多长时间。

结果可能会因机器而异，我在我的笔记本电脑中（13 英寸，2014 年中期的 MacBook Pro，配备 16GB 内存和 3 GHz 的处理器）运行后，得到了表 5.1 所示的结果。

表 5.1 流更节约时间

从这个测试结果不难看出，使用流所需的时间几乎是使用 fs.readFile 函数所需时间的 1/3 （通常，为了得到更可靠的数据，你要进行更多的测试，然后计算每次结果之间的标准差和方差，不过这已经超过了本书的范畴）。多次测试结果其实也差不了多少。

将代码写成使用流的方式是为了执行更快，更高效地使用内存。你也可以对示例代码中的两种方案，通过使用 Node.js 中的 process.memoryUsage 函数来追踪各自内存的使用情况。在示例代码中，在完成读取文档内容代码的下方，添加如下代码：

将上述代码分别添加到使用流的示例代码和使用 fs.readFile 的示例代码中，然后运行示例代码，可以看到，使用 fs.readFile 版本的结果为：

使用流方式的版本，结果为：

正如此前提过的，使用流这种方式比使用 readFile 方式时少使用了很多内存（RSS 少了 49%,heapTotal 少了 70%,heapUsed 少了 82%）。使用流不仅速度快，内存使用也更高效。

#### 5.1.3 Events

Another kind of API interface that Node.js exposes to developers is the event pattern. Those who have used jQuery or addEventListener in browser-based JavaScript will be familiar with this pattern, and the fs.createReadStream example discussed in the last few pages also exposes an events API interface where functions can be executed when a chunk of data is read, when the file has finished streaming, or when an error occurs reading the file.

This fits with the way that Node.js's code is executed: it makes use of the event loop. This involves executing non-blocking code when an event is triggered, meaning that other events can occur at the same time. In various programming languages such as Ruby and Python, there's a way to run code in an asynchronous fashion within an event loop, but this requires using libraries that are structured to execute non-blocking code, such as EventMachine for Ruby, and Twisted for Python. With Node.js, there's no external library to load and execute — the programming framework has a built-in event loop that it automatically begins executing when it starts.

Not only do various API functions in Node.js expose an events interface, but Node.js also provides a library for creating your own event interfaces using the EventEmitter module. Here's an example of using the EventEmitter module to greet someone with a message when the welcome event is emitted:

```js
'use strict'

const greeter = new events.EventEmitter()
greeter.on('welcome', function () { 
  console.log('hello')
})

greeter.emit('welcome')
```

An event emitter instance called greeter is created, and you create an event on it with the name 'welcome', which when emitted will log 'hello'. You then emit the event 'welcome' on the greeter object. If you run the code in your Node.js REPL, you can see that the message "hello" is printed in the Terminal.

As you work through NW.js's and Electron's APIs, you'll see the event pattern in use and get a chance to work with it as you go through the examples in the book.

5.1.3 事件

Node.js 提供给开发者的另外一类 API 接口是与事件相关的。对于那些用过 jQuery 或者浏览器端的 addEventListener 这样的 JavaScript 代码的人来说应该比较熟悉，而且此前提到的 fs.createReadStream 同样也提供了一些事件 API。比如，当一部分数据收到的时候执行一个指定的函数，还有当文件数据读取完毕的时候，又或者当读取文件发生错误时。

这和 Node.js 执行代码的方式是吻合的：它使用了事件循环。这牵涉到，当事件被触发时，执行非阻塞代码，意味着同一时间也有可能有其他的事件被触发。在不同的编程语言中，比如，Ruby 和 Python，也可以在一个事件循环中异步执行代码，但是它们都需要额外代码库的支持，比如 Ruby 需要 EventMachine，Python 需要 Twisted。但在 Node.js 中，不需要额外的代码库 —— 编程框架本身就内置了事件循环，当程序运行起来的时候，事件循环会自动开始。

除了很多 Node.js 中的 API 函数提供了事件接口，Node.js 本身还提供了一个 EventEmitter 模块，可以让你创建自己的事件接口。下面是一个使用 EventEmitter 的例子，当 welcome 事件被触发的时候，会打印出一段欢迎语：

上述代码创建了一个名为 greeter 的事件触发实例，并且在该实例上创建了一个名为 'welcome' 的事件，当该事件被触发的时候，会打印出 'hello'。紧接着，在 greeter 对象上触发了 'welcome' 事件。如果使用 Node.js 的 REPL 程序运行上述代码，就可以在终端应用中看到 "hello" 的消息了。

当使用 NW.js 和 Electron API 的时候，你会发现也能看到事件模式的身影，在本书后续的例子中会进行相应介绍。

#### 5.1.4 Modules

Structuring code into reusable libraries is an important part of any programming language's ecosystem, and a good package system goes a long way toward helping developers be productive. In Node.js, groups of functions are organized into modules, and these modules can be easily created and reused in other places.

Node.js uses a module format called CommonJS. The CommonJS spec in brief is a standard for creating nonbrowser JavaScript libraries that can work with each other, but has also been applied to browser-based JavaScript libraries as well.

Let's work through an example of creating a module in order to get a better feel for it.

Creating Public API Methods With Module.exports

To make functions, objects, and other values publicly available in a JavaScript file, the developer has to use either one of two specific expressions: exports or module .exports. Say you have a function for performing some business logic in your file, and you want to be able to load the file and call the following function:

```js
function applyDiscount (discountCode, amount) { 
  let discountCodes = { 
    summer20: (amt) => { return amt * 0.8 }, 
    bigone: (amt) => { 
      if (amt > 10000) return amt - 10000
      else return amt
    } 
  }

  if (discountCodes[discountCode]) return discountCodes[discountCode](amount)
  else return amount
}
```

If you want to make this a publicly available function on the file, you can do that like so:

```js
exports.applyDiscount = applyDiscount
```

Or like this:

```js
module.exports = { applyDiscount: applyDiscount }
```

Or if the file has only one function that you want to call, you could export the function like this:

```js
module.exports = applyDiscount
```

These methods don't have to expose only functions or objects; they can be used to export any kind of value in JavaScript. This allows you to organize your code as you like and make it easily reusable. The next stage is to be able to load libraries together, via the require method.

Loading Libraries Via Require

Once you have a file that has publicly available functions or values, you can then include it in other files by use of the require function. For example, say you turned the bit of business logic for applying discounts into a file called discount.js. You could include that file in another place, say at the same location as the discount.js file in the app's folder, like this:

```js
const discount = require('./discount')
```

You would now have the file's exported functions or objects loaded and attached to the discount variable in your file. You can then call the applyDiscount function in your file like so:

```js
discount.applyDiscount('summer20', 4999)
```

This allows you to structure your code into small, reusable libraries that are easy to understand and easy to use elsewhere. This is a key philosophy of Node.js — to use and combine lots of little modules when developing rather than create large files that are difficult to read through and understand.

The require function isn't used only to load local files; it can be used to load modules, as well. The Node.js API contains a set of modules that can be loaded explicitly by using a require function that's passed either the name of a module or the relative file path to the module, like this example:

```js
const os = require('os')
```

That code loads Node's OS module. Node.js provides a number of modules in its core, and you can load them without having to install them. A few of the modules are loaded as global objects in Node.js's namespace, and the rest have to be loaded via the require function. The list of modules that Node.js provides by default can be viewed at https://nodejs.org/api.

Apart from Node.js's core modules, there's also the ability to install and use modules via npm (which stands for Node Package Manager). npm is a free central repository that lets you publish and download modules to use in your apps. You can search for and find modules via https://npmjs.com and then install them (for example, request) via this command on the Terminal:

```
npm install request
```

This will download a copy of the request module (a library used to make HTTP requests), and place it in a folder called node_modules. Then you'll be able to load that module within your code as a locally installed module as you would with Node's main modules, like this:

```js
const request = require('request')
```

This will load the request module that's located in the node_modules folder. If you open that folder, you'll see the folder for the request module there. The require function in Node.js is designed to work so that if you pass the name of a module, it will look up the modules that are either available in Node.js' core, or installed globally, or installed locally in the node_modules folder.

You can also install npm modules globally, meaning that they're not installed in the app's node_modules folder but instead in a folder where they're available to any Node.js process that loads via require. Examples of npm modules installed globally tend to be build tools like Grunt and Bower. To install them globally, append a –g argument to the npm install command, like this:

```
npm install –g grunt-cli
```

The reason for installing grunt-cli globally in this case is so you only have to install it once, not once per app you use it with. Also, npm modules can have binary commands, and installing an npm module globally allows you to run that binary command without having to install the npm package each time. The same can be said for installing NW.js and Electron as global npm modules.

This is something of a quick overview of what Node.js offers from a developer's perspective. Given that we've been discussing installing third-party modules, we'll look at the mechanism behind installing third-party modules — the package manager known as npm.

5.1.4 模块

对于任何一门编程语言的生态系统而言，支持将代码组织为复用的代码库是非常重要的一部分，并且一个好的包管理系统可以让开发者更加高效。在 Node.js 中，一组函数可以组织成一个模块，这些模块可以很容易地被创建出来，并在其他地方被使用。

Node.js 遵循了名为 CommonJS 的模块规范。CommonJS 规范简而言之就是一种创建非浏览器 JavaScript 代码库的标准，互相之间可以使用，而且也被应用在基于浏览器的 JavaScript 代码库中。

让我们通过一个创建模块的例子来更好地感受一下 Node.js 中的模块。

通过 module.exports 创建公有 API 的方法

在一个 JavaScript 文件中，要想将方法、对象或者其他值暴露出来，开发者有两种方式：exports 或者 module.exports。假设在你的文件中有一个函数，用于处理一些与商业逻辑相关的操作，而且你想加载这个文件的时候，可以调用该函数：

如果想让上述函数暴露出来，可以使用如下方式：

```js
exports.applyDiscount = applyDiscount
```

或者像这样：

```js
module.exports = { applyDiscount: applyDiscount }
```

或者，如果只需要暴露一个函数，那么也可以这样：

```js
module.exports = applyDiscount
```

上述方法不仅可以用于暴露函数或者对象，还可以用于暴露 JavaScript 中的任意类型的值。它可以让你随心所欲地组织你的代码，并且让你轻而易举地实现代码的复用性。接下来我们要通过 require 方法将该代码库加载进来。

通过 require 加载代码库

准备好包含暴露函数的值的文件后，接下来就可以使用 require 函数来加载该文件了。举一个例子，假设你将上述代码保存到了一个名为 discount.js 的文件中。接下来你想在和该文件同级目录（app 文件夹）的另外一个文件中加载该文件，可以这样操作：

```js
const discount = require('./discount')
```

现在你已经将该文件暴露出来的函数或对象赋值给了 discount 变量。接下来就可以通过如下方式来调用 applyDiscount 函数了：

```js
discount.applyDiscount('summer20', 4999)
```

这种方式可以让你将代码组织成小的可复用的代码库，极容易理解又方便在其他地方被使用。Node.js 中有一条很关键的编程哲学 —— 在开发过程中，宁愿通过组装大量小模块，也不要将所有逻辑都包含在一个大文件中，这样既难读也不容易理解。

require 函数不仅可以用于加载本地文件，它也可以用于加载模块。Node.js API 中内置了一系列模块，可以通过 require 函数，传递模块名或者是相对路径来显示加载它们，像下面这样：

```js
const os = require('os')
```

上述代码加载了 Node.js 的 OS 模块。Node.js 内核中包含了一些模块，无须安装就可以直接加载这些模块。其中有一些是直接加载好挂在 Node.js 命名空间中的全局对象上的，其他则是需要 require 函数进行加载的。关于 Node.js 内置模块的信息可以查看这个链接了解详情：https://nodejs.org/api。

除了 Node.js 提供的核心模块之外，还可以通过 npm （Node Package Manager, Node 包管理器）安装和使用模块。npm 是一个免费的中心仓库，可以让你发布模块以及在你的应用中下载模块来使用。你可以通过 https://npmjs.com 搜索要安装的模块，然后在终端应用中通过如下命令进行安装（比如要安装 request 模块）：

```
npm install request
```

上述命令会下载一份 request 模块（一个用于发送 HTTP 请求的代码库）的副本，并将它放在一个名为 node_modules 的文件夹中。接下来你就可以在你的 Node 主模块中将它作为本地安装的模块进行加载了，就像下面这样：

```js
const request = require('request')
```

上述代码会加载位于 node_modules 文件夹中的 request 模块。如果你打开 node_modules 文件夹，会发现 request 模块对应的文件夹就在那里。Node.js 中的 require 被设计为只需要接收一个模块名就可以找到该模块并加载。它会通过三个地方进行查找，分别是 Node.js 内核中的模块、全局安装的模块以及本地安装的位于 node_modules 文件夹中的模块。

你也可以全局安装 npm 模块，这意味着这些模块不是安装在应用的 node_modules 文件夹中，而是在另外一个文件夹中，任何一个 Node 进程都可以通过 require 函数加载这些模块。通常全局安装的 npm 模块都是像 Grunt 和 Bower 这样的构建工具。要全局安装，只需在 install 命令后加上 - g 参数，就像下面这样：

```
npm install –g grunt-cli
```

上述例子中之所以将 grunt-cli 模块安装为全局模块，理由是，你只需要安装一次，而不需要为每个应用都安装一次。而且，有的 npm 模块包含一些二进制命令，全局安装后就可以直接使用这些命令了，不需要每次都进行安装。将 NW.js 和 Electron 安装为全局模块也是一样的道理。

以上就是从开发者角度对 Node.js 进行了快速介绍。既然我们正在讨论安装第三方模块，那么接下来就来看看安装第三方模块背后的机制 —— 包管理器 npm。

### 5.2 Node Package Manager (npm)

Node Package Manager (or npm) is the tool used by Node.js developers to handle installing libraries. It's built into Node.js by default and has proven to be a popular tool, maintaining a central repository of over 400,000 packages to date. It allows developers to download modules for use in their apps as well as publish modules for others to use.

5.2 Node 包管理器

Node 包管理器（npm）是一种工具，用来处理安装模块的事宜。它默认是集成在 Node.js 中的，而且被证明是一个非常流行的工具，截至目前，它维护了一个包含超过 40 万个模块的中心仓库。开发者可以用它来下载模块，以及发布模块供其他人使用。

#### 5.2.1 Finding packages for your app

Visit npmjs.com, and you'll be able to find out more information about npm and what it does, besides finding modules that may be of interest, such as webpack and TypeScript. You can search for packages by typing in a term that matches the name, description, or keywords used for those modules. Alternatively, you can click the most popular packages and see whether they're of use to you.

Once you've found a package you want to use in your app (or experiment with), you can install it via the command line like so:

```
npm install lodash
```

You'll now have the lodash module installed inside the node_modules folder in the current directory that your command-line terminal is in, and you'll be able to use it in your code like this:

```js
const _ = require('underscore')
```

Now, any places in your code where require('lodash') is called will have the module already loaded, and reuse it from require's module cache, rather than go through the process of loading the module from scratch.

1-3『又意外发现一个宝藏：[npm](https://www.npmjs.com/)。很多 npm 三方包的用法可以在这个官网上查资料。』

5.2.1 寻找应用需要的模块

通过访问 [npm](https://www.npmjs.com/)，可以了解到更多关于 npm 的信息以及它的用途。除此之外，还可以在上面找到你感兴趣的模块，比如像 webpack 和 TypeScript。你可以通过关键词来搜索模块，只要模块的名字、描述包含该关键词就可以搜索到。或者你也可以单击最受欢迎的模块来看看是否有符合你需求的模块可用。

一旦找到了应用要使用（或者只是测试性质的）的模块，就可以通过如下命令进行安装了：

```
npm install lodash
```

上述代码会将 lodash 模块安装在和你运行上述命令所处的同级目录的 node_modules 文件夹中，接下来就可以通过如下方式使用该模块了：

```js
const _ = require('underscore');
```

现在，在你代码的任何位置调用 require ('lodash')，都会将该模块加载进来，后续会直接从 require 模块缓存中获取出来使用，而不是每次都重新加载该模块。

#### 5.2.2 Tracking installed modules with package.json

After a while, you'll be using a bunch of modules in your app, and you'll want to keep a record of what they are, as well as which version of them you're using. You'll need a manifest file. npm uses a manifest file called package.json as the way to describe an npm module, as well as what module dependencies it has. In the previous example, you installed the lodash module but did not append its information to a package.json file.

Create a package.json file to track your dependencies. You can start that process by running this command in your terminal:

```
npm init
```

This triggers the process of creating a package.json file by asking a bunch of questions in the command line and populating the package.json file's contents as a result. By the end of the question process, you should see a package.json file that resembles this:

This creates a package.json file that can store configuration information for your app and that also contains information about the module, what file it should load when required as a dependency, any script commands it has, and what software license it has.

Now that you've got a package.json file to work with, you can track your module dependencies. Run the following command in your terminal:

```
npm install lodash --save
```

Not only will it install the lodash module, it will also add the following configuration information to the package.json file:

```
"dependencies": { "lodash": "^4.15.0" }
```

The name and version of the module are now stored in the package.json file, meaning that you can track your app's modules and versions.

Now, if you use version control for your app (like Git) and want to allow other developers to set up the app quickly on their computer, they'll be able to install all of the app's module dependencies by running the following command at the same working directory as the package.json file:

```
npm install
```

When passed no arguments, npm install will look for the package.json file and install all the module dependencies that are listed in the file.

#### Installing Development-only Dependencies

There are some module dependencies that you want to use only for development purposes and not as part of the app, such as testing libraries like Mocha and Karma. You can install these modules as development dependencies using the following command from your terminal:

```
npm install mocha –-save-dev
```

This will install the Mocha module into the node_modules folder and will add the following JSON to the package.json file:

```json
"devDependencies": { "mocha": "^3.0.2" }
```

Being able to separate dependencies required for the app to run from dependencies used to test and build the app helps developers ship smaller binaries of the app.

5.2.2 使用 package.json 记录安装的模块

应用开发了一段时间后，你会用到很多模块，这时你想将这些模块以及对应的版本号记录下来。你需要一个清单文件。npm 使用名为 package.json 的文件作为清单文件，该文件用于描述一个 npm 模块，包括该模块依赖的那些模块。在此前的例子中，你安装了 lodash 模块，但并没有将这个信息记录在 package.json 文件中。

创建一个 package.json 文件来记录依赖的模块。在终端应用中运行如下命令来创建该文件：

```
npm init
```

上述代码会触发一个创建 package.json 文件的流程，它会在命令行中问你一些问题，并最终生成对应的 package.json 文件的内容。提问题环节结束后，就会看到如下所示的 package.json 文件内容：

这样就创建了一个 package.json 文件，该文件中可以保存一些应用的配置信息以及模块的一些信息，比如，当模块被加载的时候需要首先加载哪个文件、还有没有其他脚本命令以及使用的软件协议是哪一个。

现在你已经有 package.json 文件可以用来记录依赖的模块了。在终端应用中运行如下命令：

```
npm install lodash –save
```

上述命令不仅会安装 lodash 模块，还会在 package.json 文件中添加如下配置信息：

模块名和版本号都已经保存在 package.json 文件中了，这意味着你已经可以记录你的应用所依赖的模块和版本号了。

现在，如果你的应用代码使用版本控制（就像 Git），并且想让其他开发者也可以在他们的计算机中快速将应用构建起来，让他们在 package.json 同级目录下运行如下命令就可以将所有应用依赖的模块都安装好：

```
npm install
```

当上述命令不传递任何参数的时候，npm install 会找到 package.json 文件并将其中罗列出来的所有模块都安装好。

只安装开发过程中需要的模块

有的模块你只用于开发过程中，而并非应用本身需要，比如像 Mocha 和 Karma 这样的测试框架。你可以使用终端应用通过如下命令来安装这些模块作为开发过程中的依赖：

```
npm install mocha –-save-dev
```

上述命令会将 Mocha 模块安装到 node_modules 文件夹中，而且会在 package. json 文件中添加如下配置信息：

将应用所必须依赖的模块和开发时或者用于测试依赖的模块分开的好处就是可以帮助开发者分发出尺寸更小的应用。

#### 5.2.3 Packaging your modules and apps with npm

One of the major factors in collaborating successfully on an npm module is how easy it is for other developers to install and get running on their local development machine. Packaging your modules and apps so that they install and run seamlessly from one machine to another is key to this.

#### Controlling Depenency Versons In Package.json

When it comes to installing an app that has Node.js modules, there's first a question of what to track in version control. There are two things that can be done: either the developer has the Node.js modules and all their files checked into version control, or they check the package.json file into version control (which will track what dependencies the app has) and exclude the node_modules folder from being tracked by version control.

Developers tend to go for the latter approach for two reasons. The first is that there are fewer files to track in version control (making it easier to use the version control tool to look through only the app files). The second is for compatibility with multiple OSs. There are some Node.js modules that use extensions written in C++, and for those Node.js modules to be installed, they need to be compiled on the developer's machine. If the Node.js module is compiled on Mac OS and then checked into version control, and then someone else wants to use it but on a different computer (Linux or Windows), then the Node.js module will fail to work because it has been compiled to work against a different OS.

My personal preference is to not only track the package.json file of your app, but also lock down the version of the dependencies in that package.json file. To explain: When a Node.js module is added to the package.json file via npm install, you'll notice that the dependency listing in the package.json will show a caret character (^) before the version number of the module. The ^ indicates to npm that when installing that dependency, it can install a more up-to-date version, so long as it's compatible with the major version specified in the package.json file. As an example, say you install a version of CoffeeScript for use in your app:

```
npm install coffee-script --save
```

If you look at the package.json file, you'll see something like this:

```json
"dependencies": { "coffee-script":"^1.10.1" }
```

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

#### Publishing Applications and Modules to npm

Once you've created a module or an app and begun tracking its dependencies, you may want to make it available for others to download and use. You can do that through npm. You'll need to create a free account with npm (unless you have one already) by going to npmjs.com and clicking the signup link. Fill in your details, and once you've set up your account, in your command-line terminal, run the following command:

```
npm login
```

Once you've logged in, you'll be able to publish modules from the command line up to npm. Say you've created a module that you want to be able to install via npm. In the same working directory as the package.json for the module, run the following command:

```
npm publish
```

That will push a copy of the module up to npm, and you'll then be able to install it via npm install. You'll also be able to publish updates to your package using this command, and incrementing the version number of the module in the package.json file.

5.2.3 使用 npm 打包模块和应用

开发 npm 模块有一个优点，就是在协同开发的时候，它能很容易地让其他开发者在他们的本地开发环境中将依赖模块安装好，并将应用运行起来。将模块和应用打包好，这样在不同机器上就可以无缝地安装和运行，这是关键。

在 package.json 中控制依赖模块的版本号

当需要安装一个依赖 Node.js 模块的应用时，首先就会有一个问题 —— 当使用版本控制的时候，这些模块怎么处理。这里有两个办法：要么开发过程中把所有依赖的模块都添加到版本控制中，要么只将 package.json 文件（记录了应用依赖的模块）添加到版本控制中，并将 node_modules 文件夹从版本控制中移除。

开发者通常倾向于后者，原因有两个。第一个原因是这样添加到版本控制中的文件会少很多（通过版本控制可以更容易地查看应用代码）。另外一个原因是为了多操作系统下的兼容性。有些 Node.js 模块使用 C++ 编写，这些 Node.js 模块安装的时候，需要在开发者机器上进行编译。如果这类 Node.js 模块在 Mac OS 中编译后提交到版本控制中，紧接着其他人想在其他计算机中（Linux 或者 Windows）使用，这时该模块将无法工作，原因是它是在其他操作系统上编译的。

我个人倾向于不仅将 package.json 添加到版本控制中，还要将 package.json 文件中声明的依赖模块的版本号进行锁定。解释一下：当通过 npm install 安装 Node.js 模块并添加到 package.json 文件中时，你会发现在 package.json 中罗列出依赖模块的地方，在版本号前会有一个脱字符号（`^`）。`^` 的意思是告诉 npm 在安装该模块的时候，可以安装更新的版本，只要保证主版本号和 package.json 中声明的主版本号一致就可以。举一个例子，假设你要在应用中安装一个 CoffeeScript 模块：

```
npm install coffee-script –save
```

上述代码会在 package.json 文件中添加如下配置信息：

注意，`^` 在 CoffeeScript 1.10.1 版本号的前面。你已经安装了 1.10.1 版本的 CoffeeScript，不过，假设几个月后，有人从 GitHub 上下载了一份应用代码，并运行 npm install 来安装依赖。如果 CoffeeScript 1.11.0 或者 1.10.2 已经发布了，那么安装的时候就会安装新发布的版本。脱字符号表示你可以安装更新版本的依赖模块，只要该新版本是在补丁级别的（版本号中第二个点后面的那个数字，代表了用于修复漏洞或者不影响功能的改动）或者是小版本级别的（版本号中第一个点后面的那个数字，表示改动不会要求你的应用更新后需要修改代码才能工作）。如果 CoffeeScript 2.0.0 发布了的话，它不会被安装，因为它属于主版本号的改动（意味着有新的功能 / 修改过的 API，会导致和你的应用不兼容，需要你的应用也跟着进行修改）。

之所以使用这种方式是为了让开发者可以直接获得依赖模块的补丁和兼容的更新，而不需要手动在 package.json 中更新版本号来获取更新。只要模块的开发者遵循语义化版本号的原则，并且在更新过程中不引入漏洞，这套方式就可以很好地工作。从 DevOps 的角度来看，这为生产环境中的漏洞滋生提供了温室（因此，我们需要综合的测试策略，本书后续部分会做介绍）。你想要控制依赖模块的版本号。

如何锁定依赖模块的版本号呢？这里有两种方法。第一种方法是将 package.json 文件中列出的依赖模块版本号前的 `^` 和 `~` 符号都去掉。如果你不想手动做的话，还有一个办法就是可以使用 `npm shrinkwrap` 命令。

npm 的 shrinkwrap 命令会将安装的模块版本号锁定。在 package.json 文件同级目录下运行 npm shrinkwrap 命令时会产生一个名为 npm-shrinkwrap.json 文件，这个 JSON 文件包含了一些配置信息，指明了安装模块的具体版本号，如下所示：

上述文件有助于让 npm 知道具体要安装哪个版本的模块。

根据我从 2010 年就开始使用 Node.js 到现在的经验，我的建议是，保持 package.json 文件中的模块版本号最新、将 node_modules 文件夹从版本控制中移除以及如有必要，使用 npm shrinkwrap 将依赖的模块版本号锁定。

将应用以及模块发布到 npm

当你创建好了一个模块或者应用，并且记录了它依赖的模块，接下来你可能希望将它提供给其他人下载使用。你可以通过 npm 来实现这个需求。前往 npmjs.com 网站并单击注册链接来免费创建一个 npm 账号（如果还没有账号的话）。输入一些关于你的详细信息，完成注册后，通过命令行终端应用，运行如下命令：

```
npm login
```

登录后，你就可以通过命令行将模块发布到 npm。假设你已经创建好了一个模块，并希望通过 npm 安装这个模块。这时在 package.json 文件的同级目录下，运行如下命令：

```
npm publish
```

上述命令会将模块的一份副本发布到 npm 仓库中，然后你就可以通过 npm install 来安装它了。这个命令也可以用来发布模块的更新，你也可以将 package. json 文件中的版本号进行递增。

## 0601. Exploring NW.js and Electron's internals

### Summary

In this chapter, we've exposed some differences between NW.js and Electron by exploring how their software components work under the hood. Some of the key takeaways from the chapter include the following:

1 In NW.js, Node.js and Blink share JavaScript contexts, which you can use for sharing data between multiple windows. 

2 This sharing of JavaScript state means that multiple app windows for the same NW.js app can share the same state. 

3 NW.js uses a compiled version of Chromium with custom bindings, whereas Electron uses an API in Chromium to integrate Node.js with Chromium. 

4 Electron has separate JavaScript contexts between the front end and the back end. 

5 When you want to share state between the front end and back end in Electron apps, you need to use message passing via the ipcMain and ipcRenderer APIs.

In the next chapter, we'll look at how to use the various APIs of NW.js and Electron to build desktop apps — specifically, at the way in which you can craft an app's look and feel. It will be more visual, and hopefully more fun.

在本章中，通过介绍 NW.js 和 Electron 内部各组件的工作机制介绍了两者的不同。下面是本章的关键内容：

1、在 NW.js 中，Node.js 和 Blink 共享 JavaScript 上下文，可以在多视窗间共享数据。

2、共享 JavaScript 状态意味着在同一个 NW.js 的多视窗应用中，可以共享同一个状态。

3、NW.js 使用了编译后的 Chromium 版本以及自定义绑定，而 Electron 则使用了 Chromium 中的 API 将 Chromium 和 Node.js 整合在一起。

4、Electron 将前后端的 JavaScript 上下文进行了隔离。

5、当你想在 Electron 应用的前后端进行数据共享时，需要通过 ipcMain 和 ipcRenderer 这两个 API 进行消息传递来实现。

在下一章中，我们会介绍如何使用 NW.js 和 Electron 提供的 API 来构建桌面应用 —— 着重介绍如何改变应用的界面部分。这部分和视觉更相关，也应该更加有趣。

### 6.0

This chapter covers: 1) Understanding how NW.js and Electron combine Node.js and Chromium. 2) Developing with Electron's multi-process approach. 3) Building with NW.js's shared-context approach. 4) Sharing state by passing messages.

Although NW.js and Electron consist of the same software components, and Cheng Zhao has influenced the development of both, the two frameworks have evolved different approaches to how they function under the hood. Analyzing how they operate internally will help you understand what's going on when you're running an app and demystify the software.

In this chapter, we'll look at how NW.js and Electron function internally. We'll take a look at NW.js first to see how it combines Node.js with Chromium (because that was the first Node.js desktop app framework) and then explore how Electron took a different approach to combining those software components. Following that, we'll look at the frameworks' different approaches to context and state. I'll then elaborate a bit on Electron's use of message passing to transmit data as state between the processes in a desktop app.

We'll also look at some resources for further reading. The goal is that you'll be in a good position to understand how the two frameworks differ in their internal architecture and the implications this has on building desktop apps with them.

探索 NW.js 和 Electron 的内部机制

本章要点：1）理解 NW.js 和 Electron 是如何整合 Node.js 和 Chromium 的。2）使用 Electron 多进程特性进行开发。3）使用 NW.js 共享上下文机制进行开发。4）通过消息传递来共享状态。

尽管 NW.js 和 Electron 都包含相同的软件组件，而且赵成参与了这两个框架的开发，但是这两个框架内部的工作方式采用了不同的方式。分析它们内部的工作方式有助于你理解应用运行的背后是怎样工作的。

本章会介绍 NW.js 和 Electron 的内部工作机制。我们先介绍 NW.js 是如何整合 Node.js 和 Chromium 的（因为它是首款 Node.js 桌面应用开发框架），然后再来看 Electron 是如何整合那些软件组件的。紧接着，会介绍这两个框架在上下文和状态管理上采用了什么不同的方式。最后我会花点篇幅介绍使用 Electron 在桌面应用的不同进程间进行消息传递。

我们还会介绍一些扩展阅读的资源。目标是让你理解这两个框架内部架构的不同之处以及使用它们构建桌面应用时的不同点。

### 6.1 How does NW.js work under the hood?

From a developer's view, NW.js is a combination of a programming framework (Node.js) with Chromium's browser engine through their common use of V8. V8 is a JavaScript engine created by Google for its web browser, Google Chrome. It's written in C++ and was designed with the goal of speeding up the execution of JavaScript in the web browser.

When Node.js was released in 2009, a year after Google Chrome, it combined a multiplatform support library called libuv with the V8 engine and provided a way to write asynchronous server-side programs in JavaScript. Because both Node.js and Chromium use V8 to execute their JavaScript, it provided a way to combine the two pieces of software, which Roger Wang came to understand and figure out. Figure 6.1 shows how those components are combined.

1-2『这里，node.js 是将 V8 引擎和 libuv 结合起来的一个 JS 后端语言，补充进 node.js 的术语卡片。（2021-04-18）』—— 已完成

Figure 6.1 Overview of NW.js's component architecture in relation to loading an app

Looking at figure 6.1, you can see that Node.js is used in the back end to handle working with the OS, and that Blink (Chromium's rendering engine) is used to handle rendering the front-end part of the app, the bit that users see. Between them, both Node.js and Blink use V8 as the component that handles executing JavaScript, and it's this bit that's crucial in getting Node.js and Chromium to work together. There are three things necessary for Node.js and Chromium to work together: 1) Make Node.js and Chromium use the same instance of V8. 2) Integrate the main event loop. 3) Bridge the JavaScript context between Node and Chromium.

#### NW.js and its forked dependencies

NW.js, a combination of Node.js and the WebKit browser engine, used to be known as node-webkit. Recently, both components were forked: Google created a fork of WebKit called Blink, and in October 2014 a fork of Node.js called IO.js emerged. They were created for different reasons, but as projects that received more regular updates and features, NW.js opted to switch to using them.

As node-webkit no longer used Node.js and WebKit (but IO.js and Blink instead), it was suggested that the project should be renamed; hence, the project was renamed to NW.js.

In May 2015, the IO.js project agreed to work with the Node.js foundation to merge IO.js back into Node.js. NW.js has switched back to using Node.js since.

6.1 NW.js 内部是如何工作的

从一个开发者的角度来看，NW.js 将一门编程框架（Node.js）和 Chromium 的浏览器引擎通过它们共用的 V8 整合起来。V8 是 Google 为其 Web 浏览器 Google Chrome 开发的 JavaScript 引擎。它是用 C++ 编写的，设计目标就是在 Web 浏览器中加快 JavaScript 的执行。

在 Google Chrome 发布一年后，2009 年 Node.js 发布，它将多平台支持代码库 libuv 和 V8 引擎进行了整合，并提供了一种使用 JavaScript 书写服务端异步程序的方式。由于 Node.js 和 Chromium 都使用 V8 来执行，Roger Wang 就想出了一个将它们整合在一起的方法。图 6.1 展示了这两个软件是如何整合在一起的。

图 6.1 和加载应用相关的 NW.js 组件架构一览

如图 6.1 所示，你可以看到 Node.js 在后端主要负责和操作系统交互，Blink （Chromium 的渲染引擎）则用来渲染应用的前端部分，也就是用户肉眼看到的那部分。在这两者中间，Node.js 和 Blink 都使用 V8 来执行 JavaScript 代码，并且这也是能让 Node.js 和 Chromium 一起工作的很重要的一点。要让 Node.js 和 Chromium 一起工作，必须满足如下三点要求：1）Node.js 和 Chromium 要使用同一份 V8 实例。2）将主要的事件循环进行集成。3）在 Node.js 和 Chromium 之间桥接 JavaScript 上下文。

NW.js 以及它的那些被克隆的依赖

NW.js 以前叫 node-webkit，由 Node.js 和 WebKit 渲染引擎组合而成。近期，这两个组件都被克隆了：Google 克隆了 WebKit 并取名为 Blink，而且在 2014 年，Node.js 的一个克隆项目 IO.js 浮现出来。它们出于不同的原因被创建出来，但是随着项目得到了更多的更新和具有更多特性，NW.js 也开始切换到使用这些克隆的项目上来。

由于 node-webkit 不再使用 Node.js 和 WebKit（而是 IO.js 和 Blink），于是有人建议对它也要进行改名，于是，它就被改名为 NW.js。

2015 年 5 月，IO.js 项目同意和 Node.js 基金会合作，将 IO.js 合并回 Node.js。自那以后，NW.js 也再一次切换回使用 Node.js。

#### 6.1.1 Using the same instance of V8

Both Node.js and Chromium use V8 to handle executing JavaScript. Getting them to work together requires that a couple of things happen in order. The first thing NW.js does is load Node.js and Chromium so that both of them have their JavaScript contexts loaded in the V8 engine. Node's JavaScript context will expose global objects and functions such as module, process, and require, to name a few. Chromium's JavaScript context will expose global objects and functions like window, document, and console. This is illustrated in figure 6.2 and involves some overlap because both Node and Chromium have a console object.

When this is done, the JavaScript context for Node.js can be copied into the JavaScript context for Chromium.

Although that sounds quite easy, the reality is that there's a bit more glue involved for Node.js and Chromium to work together — the main event loop used by both has to be integrated.

1 When NW.js loads, Node.js' global objects are copied from their JavaScript context into the context of the Blink rendering engine, so that they exist in one place.

2 When a JavaScript ﬁle (example.js) runs, it has access to all the objects in Blink's JavaScript context, including the sever-side objects from Node.js.

Figure 6.2 How NW.js handles copying the JavaScript context for Node.js into Chromium's JavaScript context

6.1.1 使用同一个 V8 实例

Node.js 和 Chromium 都使用 V8 来执行 JavaScript。要让这两者能够在一起工作，要求以下几件事要依次发生：首先，NW.js 要做的就是加载 Node.js 和 Chromium，这样它们各自的 JavaScript 上下文就能载入 V8 引擎了。Node.js 的 JavaScript 上下文会暴露一些全局对象和函数，比如 module、process、require 等。Chromium 的 JavaScript 上下文也会暴露一些像 window、document 以及 console 这样的全局对象和函数。如图 6.2 所示，两者之间还有一些重合，因为 Node 和 Chromium 都有 console 对象。

这部分完成后，Node.js 的 JavaScript 上下文可以被复制到 Chromium 的 JavaScript 上下文中。

尽管这听起来很简单，实际上要让 Node.js 和 Chromium 在一起工作还需要做一些事情 —— 要将两者所使用的事件循环进行集成。

图 6.2 NW.js 是如何将 Node.js 的 JavaScript 上下文复制到 Chromium 的 JavaScript 上下文的

#### 6.1.2 Integrating the main event loop

As discussed in section 5.1.3, Node.js uses the event loop programming pattern to handle executing code in a non-blocking, asynchronous fashion. Chromium also uses the event loop pattern to handle the asynchronous execution of its code.

But Node.js and Chromium use different software libraries (Node.js uses libuv, and Chromium uses its own custom C++ libraries, known as MessageLoop and MessagePump). To get Node.js and Chromium to work together, their event loops have to be integrated, as illustrated in figure 6.3.

When the JavaScript context for Node.js is copied into Chromium's JavaScript context, Chromium's event loop is adjusted to use a custom version of the MessagePump class, built on top of libuv, and in this way, they're able to work together.

Figure 6.3 NW.js integrates the event loops of Node.js and Chromium by making Chromium use a custom version of MessagePump, built on top of libuv.

6.1.2 集成主事件循环

正如在 5.1.3 节中讨论的，Node.js 使用了事件循环的模式，以异步非阻塞的方式来执行代码。Chromium 也使用这种方式异步执行代码。

但是 Node.js 和 Chromium 使用的是不同的软件代码库（Node.js 使用 libuv, Chromium 使用的则是自定义的 C++ 代码库，名为 MessageLoop 以及 MessagePump）。要让 Node.js 和 Chromium 在一起工作，必须将这两个事件循环进行集成，如图 6.3 所示。

当 Node.js 的 JavaScript 上下文复制到 Chromium 的 JavaScript 上下文的时候，Chromium 的事件循环会被调整为使用一个自定义版本的 MessagePump，它是构建在 libuv 之上的，这样一来，它们就可以在一起工作了。

图 6.3 NW.js 通过让 Chromium 使用一个构建在 libuv 之上的自定义版本的 MessagePump 实现将 Node.js 和 Chromium 的事件循环集成在一起

#### 6.1.3 Bridging the JavaScript context between Node and Chromium

The next step to completing the integration of Node with Chromium is to integrate Node's start function with Chromium's rendering process. Node.js kicks off with a start function that handles executing code. To get Node.js to work with Chromium, the start function has to be split into parts so that it can execute in line with Chromium's rendering process. This is a bit of custom code within NW.js that's used to monkey-patch the start function in Node.

Once this is done, Node is able to work inside of Chromium. This is how NW.js is able to make Node.js operate in the same place as the front-end code that's handled by Chromium.

That rounds up a bit about how NW.js operates under the hood. In the next section, we'll explore the different approach taken by Electron.

6.1.3 桥接 Node.js 和 Chromium 的 JavaScript 上下文

要完成 Node 和 Chromium 的整合，下一步需要将 Node 的 start 函数和 Chromium 的渲染进程进行集成。Node.js 通过执行一个 start 函数来处理代码的执行。要让 Node.js 和 Chromium 在一起工作，需要将 start 函数分割成多个部分，这样才能在 Chromium 的渲染进程中进行执行。这部分牵涉 NW.js 自己实现的代码，对 Node.js 的 start 函数打了一些补丁。

这部分完成后，Node 就可以和 Chromium 一起工作了。NW.js 就是通过这种方式让 Node.js 代码在由 Chromium 负责的前端代码中也可以工作。

以上就是 NW.js 内部工作机制的大致情况。下一节，我们会介绍 Electron 的内部工作机制。

### 6.2 How does Electron work under the hood?

Electron's approach shares some similarities in terms of the components used to provide the desktop framework, but differs in how it combines them. It's best to start by looking at the components that make up Electron. To see an up-to-date source code directory, take a look at http://mng.bz/ZQ2J.

Figure 6.4 shows a representation of that architecture at a less-detailed level. Electron's architecture emphasizes a clean separation between the Chromium source code and the app. The benefits of this are that it makes it easier to upgrade the Chromium component, and it also means that compiling Electron from the source code becomes that much simpler.

Figure 6.4 Electron's source code architecture. This diagram shows the main blocks of components that make up Electron.

The Atom component is the C++ source code for the shell. It has four distinct parts (covered in section 6.2.2). Finally, there's Chromium's source code, which the Atom shell uses to combine Chromium with Node.js.

How does Electron manage to combine Chromium with Node.js if it doesn't rely on patching Chrome to combine the event loops for Chromium and Node.js?

3『

[开发 | Electron](https://www.electronjs.org/docs/development)

[源码目录结构 | Electron](https://www.electronjs.org/docs/development/source-code-directory-structure)

』

6.2 Electron 内部是如何工作的

在为了提供桌面应用开发框架而使用到的组件这方面，Electron 采用的方案和 NW.js 类似，但整合这些组件的方式不同。最好的办法就是从组成 Electron 的组件开始来看。通过 [源码目录结构 | Electron](https://www.electronjs.org/docs/development/source-code-directory-structure) 可以看到 Electron 最新的代码结构。

图 6.4 展示了 Electron 的大致架构。Electron 的架构将 Chromium 源代码和应用切分得很清楚。这样做的好处就是使升级 Chromium 组件变得很容易，同时这也意味着通过源代码编译 Electron 也很容易。

Atom 组件是由 C++ 代码编写的。它由 4 个不同的部分组成（在 6.2.2 中会介绍）。最后还有 Chromium 的源代码，Atom shell 用于将 Chromium 和 Node.js 进行整合。在不通过对 Chrome 打补丁来集成 Chromium 和 Node.js 的事件循环的情况下，Electron 是如何对 Chromium 和 Node.js 进行整合的呢？

图 6.4 Electron 的源代码架构。图中展示了组成 Electron 的主要组件

#### 6.2.1 Introducing libchromiumcontent

Electron uses a single shared library called libchromiumcontent to load Chromium's content module, which includes Blink and V8. Chromium's content module is responsible for rendering a page in a sandboxed browser. You can find this library on GitHub at [electron/libchromiumcontent: Shared library build of Chromium’s Content module](https://github.com/electron/libchromiumcontent).

You use the Chromium content module to handle rendering web pages for the app windows. This way, there's a defined API for handling the interaction between the Chromium component and the rest of Electron's components.

6.2.1 libchromiumcontent 介绍

Electron 使用了一个名为 libchromiumcontent 的代码库来加载 Chromium 的 content 模块，该模块包含了 Blink 和 V8。Chromium 的 content 模块负责将页面渲染在浏览器的沙箱环境中。你可以通过 GitHub 的 https://github.com/electron/libchromiumcontent 找到该项目的代码。

可以使用 Chromium 的 content 模块来渲染应用视窗中的 Web 页面。通过这种方式，有既定的 API 来处理 Chromium 组件和 Electron 其他组件之间的交互。

#### 6.2.2 Electron's components

Electron's code components are organized inside Electron's Atom folder into these sections: 1) App. 2) Browser. 3) Renderer. 4) Common.

We'll look at what each of those folders contains in a bit more detail.

APP: The App folder is a collection of files written in C++11 and Objective-C++ that handles code that needs to load at the start of Electron, such as loading Node.js, loading Chromium's content module, and accessing libuv.

BROWSER: The Browser folder contains files that handle interacting with the front-end part of the app, such as initializing the JavaScript engine, interacting with the UI, and binding modules that are specific to each OS.

RENDERER: The Renderer folder contains files for code that runs in Electron's renderer processes. In Electron, each app window runs as a separate process, because Google Chrome runs each tab as a separate process, so that if a tab loads a heavy web page and becomes unresponsive, that tab can be isolated and closed without killing the browser and the rest of the tabs with it.

Later in this book, we'll look at how Electron handles running code in a main process, and how app windows have their own renderer processes that run separately.

COMMON: The Common folder contains utility code that's used by both the main and renderer processes for running the app. It also includes code that handles integrating the messaging for Node.js' event loop into Chromium's event loop.

Now you have an idea of how Electron's architecture is organized. In the next section, we'll look at how Electron handles rendering app windows in a process that's separate from the main app process.

6.2.2 Electron 中的组件

Electron 的代码组件位于 Electron 的 Atom 文件夹中，包含如下几个部分：App、Browser、Renderer、Common。我们会针对每个部分进行详细介绍。

App：App 文件夹中包含了由 C++ 和 Objective-C 编写的代码文件，负责处理 Electron 启动时的加载工作，如加载 Node.js、Chromium 的 content 模块以及访问 libuv。

Browser：Browser 文件夹中的代码文件负责处理应用前端部分的交互，诸如，初始化 JavaScript 引擎、界面上的交互以及绑定针对不同操作系统模块。

Renderer：Renderer 文件夹中包含运行在 Electron 的 renderer 进程中的代码文件。在 Electron 中，每个视窗都是一个独立的进程，这是因为 Google Chrome 将每个标签都以独立的进程来运行。这样的话，当一个标签加载一个非常大的页面导致无法响应的时候，这个标签页面是被隔离的，可以独立被关闭而不需要关掉整个浏览器或者其他标签页。本书后续部分会介绍 Electron 是如何在 main 进程中运行代码以及应用视窗是如何在互相隔离的、独立的进程中运行的。

Common：Common 文件夹包含了工具类代码，这部分代码当应用运行起来后会被 main 和 renderer 进程用到。还包括了处理将 Node.js 的事件循环整合进 Chromium 的事件循环的代码。

#### 6.2.3 How Electron handles running the app

Electron handles running apps differently than NW.js. In NW.js, the back-end and front-end parts of the desktop app share state by having the Node.js and Chromium event loops integrated and by having the JavaScript context copied from Node.js into Chromium. One of the consequences of this approach is that the app windows of an NW.js app end up sharing the same reference to the JavaScript state.

With Electron, any sharing of state from the back-end part of the app to the frontend part and vice versa has to go through the ipcMain and ipcRenderer modules. This way, the JavaScript contexts of the main process and the renderer process are kept separate, but data can be transmitted between the processes in an explicit fashion.

The ipcMain and ipcRenderer modules are event emitters that handle interprocess communication between the back end of the app (ipcMain), and the front-end app windows (ipcRenderer), as shown in figure 6.5.

Figure 6.5 How Electron passes state via messaging to and from the app windows. In Electron, each app window has its own JavaScript state, and communicating state to and from the main app process happens via interprocess communication.

This way, you have greater control over what state exists in each app window as well as how the main app interacts with the app windows.

Regardless of which desktop framework you choose to build your app with, keep in mind how you want data to be accessed and altered within your app. Depending on what your app does, you may find that one framework is better suited to your needs than the other, and in cases where you're working with those desktop app frameworks already, you'll want to keep in mind how NW.js and Electron handle JavaScript contexts.

Now let's take a closer look at how Electron and NW.js make use of Node.js.

6.2.3 Electron 是如何将应用运行起来的

Electron 处理应用的运行方式和 NW.js 不同。在 NW.js 中，通过将 Node.js 和 Chromium 的事件循环集成起来，把 Node.js 的 JavaScript 上下文复制到 Chromium 的 JavaScript 上下文中，可以让桌面应用中的前后端代码进行状态共享。这种方案带来的一个结果就是使用 NW.js 开发的应用中的视窗可以共享对 JavaScript 状态的同一份引用。

而在 Electron 中，不论是想在前端代码中共享后端代码的状态，或者反过来，都需要经过 ipcMain 和 ipcRenderer 模块。这种方式意味着 main 进程中的 JavaScript 上下文和 renderer 进程中的 JavaScript 上下文是互相隔离的，但是数据可以通过一种显式的方式在两个进程之间进行传递。

ipcMain 和 ipcRenderer 模块其实都是事件分发器，负责在应用后端代码（ipcMain）和前端代码（ipcRenderer）之间进行通信，如图 6.5 所示。

图 6.5 展示 Electron 是如何通过消息传递来让应用视窗和后端部分进行通信的。在 Electron 中，每个应用视窗都有自己的 JavaScript 状态，和 main 进程之间进行状态通信是通过进程间通信来完成的

这种方式使你可以对每个应用视窗的状态以及 mian 进程和视窗进程间的通信有更强的控制力。

不论你选择哪种框架来开发桌面应用，都要留意在应用中如何进行数据的访问和修改。根据应用的类型，可以找到一个更符合你应用需求的框架。如果你已经在使用这两个框架开发桌面应用了，要记住 NW.js 和 Electron 是如何处理 JavaScript 上下文的。

现在，我们来看一下 Electron 和 NW.js 是如何使用 Node.js 的。

### 6.3 How does Node.js work with NW.js and Electron?

Node.js interacts with the hybrid desktop environments of NW.js and Electron similarly to server-side apps. But to understand the few differences, we'll look at the way Node.js is integrated into NW.js.

6.3 Node.js 是如何与 NW.js 以及 Electron 一起工作的

Node.js 在 NW.js 和 Electron 这样混合的桌面开发环境中扮演的角色和其在服务端应用中扮演的角色类似。不过要搞清楚它们的区别，我们需要了解 Node.js 是如何被集成进 NW.js 的。

#### 6.3.1 Where Node.js fits into NW.js

NW.js's architecture consists of a number of components, Node.js being one of them. NW.js uses Node.js to access the computer's file system and other resources that would otherwise not be available due to web browser security. It also provides a way to access a large number of libraries through npm (figure 6.6).

1 Access to computer resources in Node.js

2 Visual rendering of app in Blink browser component

Figure 6.6 How Node.js is used within NW.js for desktop apps

NW.js makes Node.js available through the context of the embedded web browser, which means you can script JavaScript files that access both Node.js's API and API methods related to the browser's JavaScript namespace — such as the WebSocket class, for example. In earlier examples in the book, you've written code that has accessed Node.js's file system API in the same file that also accesses the DOM in the screen.

This is possible through the way that NW.js has merged the JavaScript namespaces of Node.js and the Blink rendering engine, as well as merged the main event loops of both, allowing them to operate and interact in a shared context.

6.3.1 Node.js 集成在 NW.js 的哪个位置

NW.js 的架构中包含了几个组件，Node.js 就是其中之一。NW.js 使用 Node.js 来访问计算机中的文件系统以及其他在 Web 页面中由于安全限制无法访问到的资源。通过 Node.js 还可以访问大量 npm 上的模块，如图 6.6 所示。

图 6.6 NW.js 是如何将 Node.js 运用在桌面应用中的

NW.js 使得在内嵌的 Web 浏览器中可以使用 Node.js，这意味着你书写的 JavaScript 代码既可以访问 Node.js 的 API 还可以访问浏览器中提供的 JavaScript 命名空间 —— 比如 WebSocket 类。在本书此前的例子中，你在同一个文件中写的代码既可以访问 Node.js 的文件系统 API，又可以访问 DOM。之所以可以这样，是因为 NW.js 已经将 Node.js 的 JavaScript 命名空间整合到了 Blink 渲染引擎中，而且将两者的事件循环也集成在一起了，可以让两者在同一个共享上下文中进行交互。

#### 6.3.2 Drawbacks of using Node.js in NW.js

Because of how NW.js merges the JavaScript contexts of the Blink rendering engine and Node.js, you should be aware of some of the consequences that come with this approach. I'll describe what those things are and how you can handle them so that they don't trip you up.

THE NODE.JS CONTEXT IS ACCESSIBLE TO ALL WINDOWS

I've talked about Node.js and Blink sharing the same JavaScript context, but how does that work in the context of an NW.js app where there are multiple windows?

In Blink, each window has its own JavaScript context, because each window loads a web page with its own JavaScript files and DOM. The code in one window will operate in the context of that window only, and not have its context leak into another window — otherwise, this would cause issues with maintaining state in the windows as well as security issues. You should expect the state that exists in one window to be isolated to that window and not leak.

That said, NW.js introduces a way to share state between windows via the way that Node.js's namespace is loaded into the namespace of Blink to create a shared JavaScript context. Even though each window has its own JavaScript namespace, they all share the same Node.js instance and its namespace. This means there's a way to share state between windows through code that operates on Node.js's namespace properties (such as the API methods), including via the require function that's used to load libraries. Should you need to share data between windows in your desktop app, you'll be able to do this by attaching data to the global object in your code.

COMMON API METHODS IN CHROMIUM AND NODE.JS

You may know that both Node.js and Blink have API methods with the same name and that work in the same way (for example, console, setTimeout, encodeURIComponent). How are these handled? In some cases, Blink's implementation is used, and in other cases, Node.js's implementation is used. NW.js opts to use Blink's implementation of console, and for setTimeout, the implementation used depends on whether the file is loaded from a Node.js module or from the desktop app. This is worth keeping in mind when you're using those functions, because although they're consistent in their implementations of inputs and outputs, there might be a slight difference in speed of execution.

6.3.2 在 NW.js 中使用 Node.js 的缺点

NW.js 采用的是将 Blink 渲染引擎和 Node.js 的 JavaScript 上下文整合的方式，要注意这种方式带来的一些结果。下面我会介绍具体带来的结果是什么以及如何解决和避免。

在所有视窗中都可以访问 Node.js 上下文

我讲过，Node.js 和 Blink 是共享同一个 JavaScript 上下文的，那么当 NW.js 应用中有多个视窗的时候又是怎样的情况呢？

在 Blink 中，每个视窗都有自己的 JavaScript 上下文，因为每个视窗都加载一个 Web 页面，该页面拥有自己的 JavaScript 文件和 DOM。该视窗中的代码仅在该视窗的上下文中进行操作，不会将它的上下文泄露到其他视窗中 —— 否则，会带来状态维护以及安全问题。一个视窗的状态应当和其他视窗的状态是隔离的，而且不会泄露出去。

换句话说，NW.js 通过将 Node.js 命名空间载入 Blink 的命名空间创建了一个共享的 JavaScript 上下文，从而引入了一种在视窗间共享状态的方式。尽管每个视窗拥有自己的 JavaScript 命名空间，但它们都共享同一个 Node.js 实例以及它的命名空间。也就是说，通过操作 Node.js 命名空间上的属性（如 API 方法），包括通过用于载入代码库的 require 函数，是可以实现视窗间共享状态的。如果你需要在桌面应用中进行视窗间的数据共享，那么可以在代码中通过 global 对象来传递数据。

Chromium 和 Node.js 有相同的 API 方法

你可能已经知道了，Node.js 和 Blink 有一些同名且功能一样的 API 方法（如，console、setTimeout、encodeURIComponent）。那这些方法怎么处理呢？有的情况下，会使用 Blink 的实现，而有的时候会用 Node.js 的实现。对于 console，NW.js 会采用 Blink 的实现，而对于 setTimeout，使用哪一个取决于代码文件是通过 Node.js 模块载入的还是直接从桌面应用载入的。使用这些方法的时候要注意，尽管它们的执行结果肯定是相同的，但在执行效率方面是有差异的。

#### 6.3.3 How Node.js is used within Electron

Electron uses Node.js along with Chromium, but rather than combining the event loops of Node.js and Chromium together, Electron uses Node.js's node_bindings feature. This way, the Chromium and Node.js components can be updated easily without the need for custom modification of the source code and subsequent compiling.

Electron handles the JavaScript contexts of Node.js and Chromium by keeping the back-end code's JavaScript state separate from that of the front-end app window's state. This isolation of the JavaScript state is one of the ways Electron is different from NW.js. That said, Node.js modules can be referenced and used from the front-end code as well, with the caveat that those Node.js modules are operating in a separate process to the back end. This is why data sharing between the back end and app windows is handled via inter-process communication, or message passing.

If you're interested in learning more about this approach, check out this site from GitHub's Jessica Lord: [Essential Electron](http://jlord.us/essential-electron/#stay-in-touch).

1-2『上面的资源：[Essential Electron](http://jlord.us/essential-electron/#stay-in-touch)，一定要去研读，作为本书的一个附件。（2021-04-16）』—— 未完成

6.3.3 Electron 是怎么使用 Node.js 的

Electron 也在 Chromium 中使用 Node.js，但不同于将两者的事件循环进行整合，Electron 使用的是 Node.js 的 `node_bindings` 功能。使用这种方式，Chromium 和 Node.js 的升级都会很容易，不需要对源代码进行修改也不需要再进行编译。

Electron 通过将后端代码的 JavaScript 状态和应用视窗前端代码的 JavaScript 状态隔离开来处理 Node.js 和 Chromium 的 JavaScript 上下文。这种将 JavaScript 状态隔离的方式也是 Electron 有别于 NW.js 的地方之一。也就是说，前端代码可以使用 Node.js 模块，不过要澄清的是，这些 Node.js 模块是在后端一个独立的进程中执行的。这也是为什么在应用视窗和后端要进行数据共享需要通过进程间通信或者消息传递来实现。

如果你对这部分内容有兴趣，想了解更多，可以访问来自 GitHub 上 Jessica Lord 的网站：http://jlord.us/essential-electron/#stay-in-touch。
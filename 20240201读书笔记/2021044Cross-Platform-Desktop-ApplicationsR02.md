## 记忆时间

## 目录

0301 Building your first desktop application

## 0301. Building your first desktop application

### Summary

In this chapter, you built on the beginnings of a desktop app and created some rich features that make the app a usable, minimally viable product. You also had a chance to explore how you can evolve a desktop app's codebase to remain readable, and how you can organize the code for a desktop app (because there's no convention-overconfiguration approach to doing this currently).

Things we've covered include the following:

1 Refactoring the code by using Node.js's module functionality.

2 Using third-party libraries to implement search features.

3 Applying Electron and NW.js's shell API to handle opening files with their default applications.

4 Improving app navigation to make the desktop app more usable.

The main thing to take away from this chapter is that with a couple-hundred lines of code and some external files, you can build an app that replicates what a native desktop app can do (and one that has relatively complex functionality). Not only that, you've been able to use third-party libraries like lunr.js to help provide this functionality, and structured the code in such a way that it can be used in web apps and allow for building apps for both the web and desktop from the same source code.

In chapter 4, you'll prepare the app for distribution: you'll hide the app developer toolbar, give the app its own icon, and build it so that it can be run as a native app on each of the operating systems.

在本章中，我们为一款桌面应用添加了一些功能，使其变得可用并满足了最小化可用产品的标准。我们还学到了如何提高一款桌面应用代码的可读性，以及如何组织代码。

本章包含如下内容：1）使用 Node.js 的模块功能重构了代码。2）使用第三方代码库实现了搜索功能。3）使用 Electron 和 NW.js 的 shell API 实现了使用系统默认的应用打开文件。4）实现了应用内的导航，使其更可用。

本章中你最受益的是如何通过几百行代码以及一些外部文件，就可以构建出一个应用，并具备和原生桌面应用一样的功能（还实现了一个相对复杂的功能）。除此之外，你还学会了如何使用像 lunr.js 这样的第三方代码库来实现它提供的功能，以及学会了组织代码的方式，能让代码同时可以被 Web 应用使用，即使用相同的代码同时构建 Web 应用和桌面应用。

在第 4 章中，我们要为应用分发做准备了：隐藏开发者工具、添加应用图标、对应用进行构建，使其可以在不同的操作系统中像原生桌面应用那样运行起来。

### 3.0

This chapter covers: 1) Opening files from the file explorer. 2) Accessing the filesystem. 3) Refactoring code using Node.js's module functionality. 4) Implementing search features in the desktop app.

Building an app is a journey of creating an initial skeleton of the app and progressively adding to the skeleton until it begins to resemble a complete product. The moment when the product comes alive with features is often, for me, the moment I get excited, and in this chapter those moments shall arrive.

In chapter 2, you began a journey of building a file explorer called Lorikeet and got to a stage where you had the UI for a working desktop application. In this chapter, you'll continue that journey and add features that will result in a file explorer app you can call a minimally viable product.

The goal is that not only will you have made the app's features by the end of the chapter, but you'll understand exactly how Electron and NW.js let you do that. The process will give you enough experience to start using those desktop app frameworks in other places as well. Chances are, your mind will open up with lots of ideas for things you can do that you didn't know how to do before. Excited? Good! Get comfortable and settle in for round two.

构建你的首款桌面应用

本章要点：1）实现从文件浏览器中打开文件。2）访问文件系统。3）使用 Node.js 模块功能重构代码。4）实现桌面应用中的查询功能。

构建一款应用无法一蹴而就，从最初的应用原型，到持续地对它进行改进，直到成为一个成品为止。通常，对我来说，当完成产品功能并上线的时刻，是最激动的时刻。本章也将给你带来这一激动的时刻。在第 2 章中，我们构建了一款名为 Lorikeet 的文件浏览器应用，而且已经完成了应用的界面和部分功能。在本章中，我们将继续完成新的功能，最终完成一款最小化可行的 Lorikeet 文件浏览器产品。

我们的目标不仅是在本章结束的时候完成应用的功能，你还要理解如何使用 NW.js 和 Electron 完成这些功能。这个过程也会让你积累足够的经验使用这些桌面应用开发框架去开发其他应用。你的脑子里总会迸发出很多奇思妙想，以前你不知道如何实现，现在你可以了。激动吗？好，准备一下，让我们进入第二回合。

### 3.1 Exploring the folders

The main ingredients for making this happen are now in place: the files and folders for a given path can now be displayed visually in the window. Next you need to build the functionality so that when the user double-clicks a folder in the main area, the app navigates to that folder and displays its contents in the main area.

3.1 浏览文件夹

实现这一功能的条件都已经满足了：指定路径下的文件和文件夹都已经显示在视窗中了。接下来，你需要实现这样一个功能：当用户在主区域中单击某个文件夹的时候，应用需要在主区域进一步显示该文件夹下的内容。

#### 3.1.1 Refactoring the code

If you look at the app.js file now, you'll notice that it's beginning to look a bit muddled, and at this point it's worth refactoring the code so that it doesn't become overwhelming and difficult to manage. Refactoring the file requires organizing the code into logical groups, as shown in figure 3.1.

app.js =>

```
app.js

fileSystem.js

userInterface.js
```

Figure 3.1 You'll start breaking out the code into logical groups of functionality so that the code is more readable and easier to work with.

In figure 3.1, the app.js file will be turned into three files. There will still be an app.js file as the main entry point for the front-end code, but there will also be two other files. The fileSystem.js file will contain code that handles interacting with the files and folders on the user's computer, and the userInterface.js file will hold functions that handle UI interactions. These are two distinct logical groups, and they will allow you to keep the code orderly.

Create two files in the Lorikeet folder at the same level as the app.js file: fileSystem.js and userInterface.js. In the fileSystem.js file, insert the code shown here.

Listing 3.1 The code for the fileSystem.js file

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

module.exports = {
  getUsersHomeFolder,
  getFilesInFolder,
  inspectAndDescribeFiles
}
```

The fileSystem.js file contains the getUsersHomeFolder, getFilesInFolder, inspectAndDescribeFile, and inspectAndDescribeFiles functions from the app.js file. The extra bit of code at the bottom exposes some of the functions that need to be accessed by other files through the use of the module.exports function call, a CommonJS JavaScript convention for exposing public code items in libraries. This is an important factor in the way you organize and make your code usable across multiple projects.

In the userInterface.js file, insert the code shown in the following listing.

Listing 3.2 The code for the userInterface.js file

```js
'use strict'

let document

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

function bindDocument (window) {
  if (!document) document = window.document
}

module.exports = {
  bindDocument,
  displayFiles
}
```

1『这里导出函数模块的写法很值得借鉴。（2021-04-14）』

Here, you expose the bindDocument and displayFiles functions in the code. The bindDocument function is used to pass the window.document context to the user-Interface.js file — otherwise, the file will not be able to access the DOM in the NW.js variant of the app (Electron is unaffected). The displayFiles function is used to display all the files, and because there's no need to call the displayFile function separate from the displayFiles function, you don't expose the displayFile function as a public API.

Now that the code that was in the app.js file has been moved into the fileSystem.js and userInterface.js files, you can replace the app.js file with the code shown here.

Listing 3.3 The code for the app.js file

```js
'use strict'

// Node.js’s fs module loads in the app
const fileSystem = require('./fileSystem')
const userInterface = require('./userInterface')

// Function that combines user’s personal folder path with getting its list of files
function main() {
  userInterface.bindDocument(window)
  const folderPath = fileSystem.getUsersHomeFolder()
  fileSystem.getFilesInFolder(folderPath, (err, files) => {
    // Simple message to display in case of error loading folder’s files
    if (err) return alert('Sorry, we could not load your home folder')
    fileSystem.inspectAndDescribeFiles(folderPath, files, userInterface.displayFiles)
  })
}

main()
```

1『

这个拆解函数的重构真赞，舒服。（2021-04-14）

跑的时候报错，发现漏掉了一行代码：

```js
userInterface.bindDocument(window)
```

』

The app.js file is now 17 lines of code and is much more readable. Here, you can see that there are two Node.js modules included in the code (fileSystem and userInterface), and that the main function is identical to how it was in the app.js file, with the exception of calling functions from the Node.js modules instead.

The last change left is to alter the index.html file so that the function that calls the user's personal folder is calling the fileSystem file module. Change the index.html file so that it looks like the following code.

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
          document.write(fileSystem.getUsersHomeFolder())
        </script>
      </div>
    </div>
    <div id="main-area"></div>
  </body> 
</html>
```

Save the changes to the files. The refactoring is almost complete. The next feature you want to add is the ability to navigate folders by double-clicking them in the file explorer.

3.1.1 重构代码

如果现在打开 app.js 文件，你会发现代码看起来开始有点混乱了，现在是时候对它进行重构了，避免它越来越臃肿从而难以维护。重构这部分代码需要把代码进行逻辑分组，如图 3.1 所示。

图 3.1 你将开始对代码从功能层面进行逻辑分组，这样代码会更加可读也更好维护

如图 3.1 所示，app.js 将会被分成三个文件。app.js 仍然是前端代码的主入口，不过还会有另外两个文件。fileSystem.js 负责处理对用户计算机中的文件和文件夹进行操作，userInterface.js 则负责处理界面上的交互。这是两个不同的逻辑分组，这样代码将更加有序。

在 Lorikeet 文件夹中与 app.js 文件同层级的位置创建两个文件：fileSystem.js 和 userInterface.js。在 fileSystem.js 文件中，插入代码清单 3.1 所示的代码。

fileSystem.js 文件包含了 getUsersHomeFolder、getFilesInFolder、inspectAndDescribeFile 以及 inspectAndDescribeFiles 这几个来自 app.js 文件的函数。文件最后那些代码通过使用 module.exports（这是一个名为 CommonJS 的模块化规范定义的将库中的公共方法暴露出来的方法）将一些函数暴露出去供其他文件调用。这是一种非常重要的组织代码的方式，而且它可以让你的代码在跨项目时也能得到复用。

在 userInterface.js 文件中，插入代码清单 3.2 所示的代码。

在上述代码中，我们将 bindDocument 和 displayFiles 这两个函数暴露了出来。bindDocument 函数的作用是将 window.document 上下文传递给 userInterface.js 文件，否则，该文件无法在 NW.js 版应用中访问 DOM（Electron 版的应用不受影响）。displayFiles 函数的作用是将所有的文件显示出来，并且因为 displayFiles 函数只会被 displayFiles 函数调用，因此没有必要将 displayFiles 函数作为一个公共的 API 暴露出来。

现在代码已经从 app.js 文件中移到 fileSystem.js 和 userInterface.js 文件中了，接下来将 app.js 替换为代码清单 3.3 所示的内容。

现在 app.js 文件只有 17 行代码，可读性更好了。如上述代码所示，app.js 中使用到了两个 Node.js 模块（fileSystem 和 userInterface），main 函数和此前 app.js 文件中的是一样的，唯一的区别是这次调用了来自这两个 Node.js 模块中的函数。

最后需要修改 index.html 文件，让它调用 fileSystem 模块来获取用户个人文件夹。将 index.html 修改为代码清单 3.4 所示的内容。

保存修改后的文件内容。重构快完成了。接下来要支持当用户在文件浏览器中双击文件夹时，能显示该文件夹中的内容。

#### 3.1.2 Handling double-clicks on folders

One of the common features of using a file explorer is navigating folders by doubleclicking the folder icon. You'll add this functionality to the Lorikeet app.

When you double-click a folder, the UI of the app updates so that the following things happen:

1 The current folder changes to that of the folder that's clicked.

2 The files that were displayed in the file explorer are updated to show the files for the folder path that was clicked.

3 When you click another folder, the same behavior occurs again.

You also want to make sure that double-clicking a folder behaves as you expect, and that double-clicking a file opens that file in its default application. To achieve that, you'll do the following:

1 Create a function in the userInterface.js file called displayFolderPath, which will update the current folder path displayed in the UI.

2 Add another function in the userInterface.js file called clearView, which will remove the files and folders that are currently displayed in the main area.

3 Create a function called loadDirectory, which will handle querying the computer for the files and folders at a given folder path and then display the files and folders in the main area. This code is effectively moved out of the app.js file.

4 Alter the displayFile function so that it attaches an event listener to a folder icon to trigger loading that folder.

5 Change the app.js file so that it calls the loadDirectory function of the user-Interface.js file.

6 Remove the script tag inside the current-folder element in the index.html file, because it's no longer needed.

In the userInterface.js file, change the code to look like the next listing.

Listing 3.5 Changing the userInterface.js file

```js
'use strict'

let document
const fileSystem = require('./fileSystem')

// Adds function to display current folder
function displayFolderPath(folderPath) {
  document.getElementById('current-folder').innerText = folderPath
}

// Clears items out of main-area div element
function clearView() {
  const mainArea = document.getElementById('main-area')
  let firstChild = mainArea.firstChild
  while (firstChild) {
    mainArea.removeChild(firstChild)
    firstChild = mainArea.firstChild
  }
}

// loadDirectory changes current folder path and updates main area
function loadDirectory(folderPath) {
  return (window) => {
    if (!document) document = window.document
    displayFolderPath(folderPath)
    fileSystem.getFilesInFolder(folderPath, (err, files) => {
      clearView()
      if (err) return alert('Sorry, you could not load your folder')
      fileSystem.inspectAndDescribeFiles(folderPath, files, displayFiles)
    })
  }
}

// Adds new function called displayFile that handles rendering template instance
function displayFile(file) {
  const mainArea = document.getElementById('main-area')
  const template = document.querySelector('#item-template')
  // Creates copy of template instance
  let clone = document.importNode(template.content, true)
  // Alters instance to include file’s name and icon
  clone.querySelector('img').src = `images/${file.type}.svg`
  // Adds double-click event listener to icon if it’s for a directory
  if (file.type === 'directory') {
    clone.querySelector('img')
      .addEventListener('dblclick', () => {
        loadDirectory(file.path)()
      }, false)
  }
  clone.querySelector('.filename').innerText = file.file
  // Appends template instance to "mainarea" div element
  mainArea.appendChild(clone)
}

// Creates displayFiles function to be end point where files will end up being displayed
function displayFiles(err, files) {
  if (err) return alert('Sorry, we could not display your files')
  files.forEach(displayFile)
}

function bindDocument (window) {
  if (!document) document = window.document
}

// Makes sure loadDirectory function is exposed as public API
module.exports = {
  bindDocument,
  displayFiles,
  loadDirectory
}
```

Next, amend the app.js file so that it calls the loadDirectory function from the user-Interface.js file. Change the app.js file to look like the following code.

Listing 3.6 Changing the app.js file for folder clicks

```js
'use strict'

// Node.js’s fs module loads in the app
const fileSystem = require('./fileSystem')
const userInterface = require('./userInterface')

// Function that combines user’s personal folder path with getting its list of files
function main() {
  userInterface.bindDocument(window)
  const folderPath = fileSystem.getUsersHomeFolder()
  userInterface.loadDirectory(folderPath)(window)
}

// Calls main function after HTML for app has loaded in window
window.onload = main()
```

One more change left to do. You can now remove the script tag from inside the currentfolder div element. Change the current-folder div element in the index.html file so that it looks like this:

```
<div id="current-folder"></div>
```

With those files changed, reload the app. Now, when you double-click an app folder, you'll see that the folder path changes in the toolbar, and the files and folders on display in the main area change as well. An example of this is shown in Electron in figure 3.2.

Figure 3.2 The Lorikeet app in Electron after navigating to a list of files inside of a folder, three levels away from the starting folder path

And figure 3.3 shows the same result in NW.js with the same file changes.

Figure 3.3 The Lorikeet app in NW.js, navigating to a hidden folder inside of my home folder

1『

报错：`innerText  of null`

找了很久很久才发现有一行代码写错了。（2021-04-14）

```js
window.onload = main()
```

应该是：

```js
window.onload = main
```

』

You can see here that you've been able to use plain vanilla JavaScript, HTML, and CSS to implement what is beginning to feel like a real desktop app. So far so goodbut it's not mission complete yet. You're going to add quick search functionality to the app.

3.1.2 处理对文件夹的双击操作

作为文件浏览器，其中一个非常常见的功能就是双击文件夹图标能够查看文件夹中的内容。接下来，我们也将给 Lorikeet 应用加入这个功能。

当双击某个文件夹时，应用界面需要做出如下改变：1）当前的文件夹改为双击的那个文件夹。2）文件浏览器中需要显示当前双击的文件夹中的文件。3）当双击其他文件夹时，重复上述的改变。

还要确保双击文件夹后的行为和预期的一致，并且当双击文件时，需要用默认的应用打开该文件。要实现这样的功能，需要完成如下这些事情：

1、在 userInterface.js 文件中新增一个 displayFolderPath 函数，该函数的作用是更新界面中的当前文件夹路径。

2、在 userInterface.js 文件中再增加一个 clearView 函数，其作用是将显示在主区域中的当前文件夹中的文件和文件夹清除。

3、还需要新增一个 loadDirectory 函数，作用是根据指定的文件夹路径，获取计算机中该路径下的文件和文件夹信息，并将其显示在应用界面主区域中。

4、修改 displayFiles 函数，在文件夹图标上监听一个事件来触发加载该文件夹中的内容。

5、修改 app.js 文件，在其中调用 userInterface.js 文件中的 loadDirectory 函数。

6、移除 index.html 文件中 current-folder 元素中的 script 标签，因为这已经不需要了。

将 userInterface.js 文件修改为代码清单 3.5 所示的内容。

代码清单 3.5 修改 userInterface.js 文件

接下来修改 app.js，让它调用 userInterface.js 文件中的 loadDirectory 函数。将 app.js 文件修改为代码清单 3.6 所示的内容。

代码清单 3.6 修改 app.js 支持文件夹双击操作

还需要改一个地方。现在可以将 current-folder div 元素中的 `<script>` 标签移除了。将 index.html 文件中的 current-folder div 元素修改为如下内容：

```html
<div id= "current-folder"></div>
```

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
      <div id="current-folder"></div>
    </div>
    <div id="main-area"></div>
  </body> 
</html>
```

这些文件修改完成后，重启应用。现在，当你双击应用中的某个文件夹时，就能看到工具条中当前文件夹路径改变了，而且该文件夹中的文件和文件夹也会显示在应用主区域中。图 3.2 所示的是一个 Electron 版的例子。

图 3.2 在 Electron 版的 Lorikeet 应用中，双击距离起始文件夹三层的某个文件夹后，界面显示了其中的文件列表

图 3.3 显示了在 NW.js 版本中同样的效果。

图 3.3 NW.js 版的 Lorikeet 应用，浏览了用户个人文件夹中的某个隐藏目录中的内容

如你所见，你已经可以使用原生的 JavaScript、HTML 以及 CSS 实现一款看上去是真正的桌面应用了。在目前为止一切都不错，不过任务还没完成。接下来要为应用增加快速搜索功能。

### 3.2 Implementing quick search

Figure 3.4 The quick search feature that you want to implement in the app

Figure 3.4 shows a preview of what you'll add next: quick search functionality.

If you have a folder containing lots of files, searching through the entire list of them can be tedious. In the wireframe, the toolbar features a search field in the top right, and to implement an in-directory search feature is relatively easy. You'll need to do the following:

1 Add a search field to the top right of the toolbar.

2 Add an in-memory search library.

3 Add the list of files and folders in the current folder to the search index. 

4 When the user begins searching, filter the files displayed in the main area.

3.2 实现快速搜索

图 3.4 展示了我们接下来要实现的：快速搜索功能的样子。

图 3.4 接下来要在应用中实现快速搜索的功能

如果一个文件夹中包含非常多的文件，那么要在这些文件中查找某个文件是一件非常麻烦的事情。在线框图中，工具条的右上角增加了一个搜索框，要实现文件夹内的搜索功能相对比较容易。只需完成以下几件事情即可：1）在工具条的右上角增加一个搜索框。2）引入一个内存搜索库。3）将当前文件夹中的文件和文件夹信息加入搜索索引。4）用户开始搜索时，对主区域显示的文件进行过滤。

#### 3.2.1 Adding the search field in the toolbar

The first thing you need to do is add some HTML for the search field in the top toolbar. Insert the following HTML snippet into the index.html file, after the currentfolder div element:

```html
<input type="search" id="search" results="5" placeholder="Search" />
```

This adds an input tag with the type search and some extra attributes that give it the visual style of a search field. The next step is to add the following CSS to the app.css stylesheet:

```css
#search {
  float: right; 
  padding: 0.5em; 
  min-width: 20em; 
  border-radius: 3em; 
  margin: 2em 1em; 
  border: none; 
  outline: none;
}
```

Once this is done, the search field appears as shown in figure 3.5.

Figure 3.5 The search field in the top toolbar, like the wireframe in figure 3.4. Interestingly, the results attribute on an input element with the type search inserts a magnifying glass inside the text field.

3.2.1 在工具条中增加搜索框

首先要做的是增加一点 HTML 代码，在工具条的右上角显示一个搜索框。在 index.html 中的 current-folder div 元素后面插入如下代码：

上述代码添加了一个 search 类型的 `<input>` 标签以及一些其他的属性来改变搜索框样式。接下来在 app.css 中添加如下 CSS 样式：

完成后，搜索框的样子如图 3.5 所示。

图 3.5 上方工具条中的搜索框，和图 3.4 所示的线框图中的类似。有意思的是，search 类型的 input 标签中的 results 属性给文本框里面加入了一个放大镜图标

#### 3.2.2 Adding an in-memory search library

Now that the search field exists, you need a way to perform searching on the list of files and folders with a searching library. Thankfully, you don't need to write one, as this is a common need that has already been satisfied.

lunr.js is a client-side search library, written by Oliver Nightingale (a colleague of mine when we both worked at New Bamboo, now part of Thoughtbot). It allows you to create an index for the list of the files and folders and perform searches with that index.

You can install lunr.js with npm from the command line:

```
npm install lunr --save

yarn add lunr --save
```

This will install lunr.js inside the node_modules folder and save it as a dependency to the package.json file. Now, you need to create a new file at the same level as the app.js file, called search.js. You can create it either on the command line with the command touch search.js or via your text editor. Once it exists, add the code shown in the next listing to the search.js file.

Listing 3.7 Inserting code into the search.js file

```js
'use strict'

const lunr = require('lunr')
let index

// resetIndex function resets search index
function resetIndex() {
  index = lunr(() => {
    this.field('file')
    this.field('type')
    this.ref('path')
  })
}

// Adds file to index for searching against
function addToIndex(file) {
  index.add(file)
}

// Queries index for a given file here
function find(query, cb) {
  if (!index) resetIndex()
  const results = index.search(query)
  cb(results)
}

// Exposes some functions for public API
module.exports = {
  addToIndex,
  find,
  resetIndex
}
```

1『

这里不能用箭头函数，不知道为哈。

```js
// resetIndex function resets search index
function resetIndex() {
  index = lunr(function () {
    this.field('file')
    this.field('type')
    this.ref('path')
  })
}
```

』

The code implements three functions: addToIndex allows you to add files to the index, find allows you to query the index, and resetIndex resets the index when you need to view a new folder and clear the existing index. You expose these functions through module.exports so that you can load the file in app.js and access those functions.

Once you've created and saved the search.js file, you need to attach it to the search field in the UI, as well as get it to change what files are displayed in the main area.

3.2.2 引入一个内存搜索库

现在有输入框了，你需要想一个办法能够通过一个搜索库来对文件和文件夹列表进行搜索。值得感激的是，你不需要自己去写，作为一种常见的需求，已经有这样的库供你使用了。

lunr.js 是一款由 Oliver Nightinggale（他是我在 New Bamboo—— 现在属于 Thoughtbot 公司 —— 工作时的同事） 开发的客户端搜索库。它支持对文件和文件夹列表进行索引，然后可以通过索引进行搜索。

你可以通过如下 npm 命令来安装 lunr.js：

```
npm install lunr --save
```

上述命令会将 lunr.js 安装在 `node_modules` 文件夹中，并将这一依赖保存到 package.json 文件中。现在需要在与 app.js 同级目录中新建一个名为 search.js 的文件。你可以通过命令行 touch search.js 或者编辑器来创建该文件。创建好后，将代码清单 3.7 中的代码插入 search.js 文件。

代码清单 3.7 将代码插入 search.js 文件

上述代码实现了三个函数：addToIndex 的作用是将文件添加到索引中，find 支持对索引进行查询，resetIndex 的作用是重置索引，当你需要浏览一个新文件夹时，需要将现有的索引全部清除。通过 module.exports 将这些函数都暴露出来，这样在 app.js 中就可以载入这个文件并访问到它们。

#### 3.2.3 Hooking up the search functionality with the UI 

To have the search field trigger searching the file names, you need to be able to intercept the event of typing the query in the field. You can do this by adding a function to the userInterface.js file called bindSearchField, which will attach an event listener to the search field. In the userInterface.js file, add the following function to the file:

```js
function bindSearchField(cb) {
  document.getElementById('search').addEventListener('keyup', cb, false)
}
```

This code will intercept any events where the user has typed in the search field, and the key on the keyboard is back up (hence, the event name keyup). You also add this function to the module.exports object at the bottom of the userInterface.js file so that you can expose it to the app.js file, as shown here:

```js
// Makes sure function is exposed as public API
module.exports = {
  bindDocument,
  displayFiles,
  loadDirectory,
  bindSearchField
}
```

This function will be used to attach a function to the search field in the UI that triggers each time the user presses a key on the keyboard while typing into the search field.

Here, you'll inspect the value that exists inside the search field. If it's blank, then you don't want to filter any files. But if it has another value, then you want to filter the files that are displayed in the main area. To achieve that, you need to do the following:

1 Before you load a folder path in the main area, you reset the search index.

2 When a file is added to the main area, you add it to the search index.

3 When the search field is empty, you make sure that all files are on show.

4 When the search field has a term, you filter the display of the files based on that term.

But first, you should include the search module at the top of the dependencies list of the userInterface.js file. Change the top of the userInterface.js file so that it looks like this:

```js
'use strict'

let document
const fileSystem = require('./fileSystem')
const search = require('./search')
```

This provides you with access to the search module. Following the inclusion of the search module, the first change you want to make is to the loadDirectory function. You want it to reset the search index every time it's called so it only searches for files that are in the current folder path. Change the loadDirectory function's code to match the next listing.

Listing 3.8 Resetting the search index when calling loadDirectory

```js
// loadDirectory changes current folder path and updates main area
function loadDirectory(folderPath) {
  return function (window) {
    if (!document) document = window.document
    // Adds the call to reset the search index
    search.resetIndex()
    displayFolderPath(folderPath)
    fileSystem.getFilesInFolder(folderPath, (err, files) => {
      clearView()
      if (err) return alert('Sorry, you could not load your folder')
      fileSystem.inspectAndDescribeFiles(folderPath, files, displayFiles)
    })
  }
}
```

Once that's done, the next thing you want to adjust is the displayFile function below the loadDirectory function. The function will handle adding the file to the search index as well as making sure that the img element contains a reference to the file's path so that the file can be filtered visually without needing to add/remove elements from the DOM. Change the displayFile function's code to look like the following.

Listing 3.9 Adding files to the search index in the displayFile function

```js
// Adds new function called displayFile that handles rendering template instance
function displayFile(file) {
  const mainArea = document.getElementById('main-area')
  const template = document.querySelector('#item-template')
  // Creates copy of template instance
  let clone = document.importNode(template.content, true)
  // Adds file to search index here
  search.addToIndex(file)
  // Alters instance to include file’s name and icon
  clone.querySelector('img').src = `images/${file.type}.svg`
  // Attaches file’s path as data attribute to image element
  clone.querySelector('img').setAttribute('data-filePath', file.path)
  // Adds double-click event listener to icon if it’s for a directory
  if (file.type === 'directory') {
    clone.querySelector('img')
      .addEventListener('dblclick', () => {
        loadDirectory(file.path)()
      }, false)
  }
  clone.querySelector('.filename').innerText = file.file
  // Appends template instance to "mainarea" div element
  mainArea.appendChild(clone)
}
```

Next, add a function for filtering the results visually. This function uses a function to look at the file paths for the files and folders on display in the main area and check whether any of them matches with the search results for the term typed into the search field. After the bindSearchField function, add the function shown in the next listing to the userInterface.js file.

Listing 3.10 Adding the filterResults function to the userInterface.js file

```js
function filterResults(results) {
  // Collects file paths for search results so you can compare them
  const validFilePaths = results.map((result) => { return result.ref })
  const items = document.getElementsByClassName('item')
  for (let i = 0; i < items.lengths; i++) {
    let item = items[i]
    let filePath = item.getElementsByTagName('img')[0]
      .getAttribute('data-filepath')
    // Does file’s path match with one of the search results?
    // If so, make sure file is visible
    if (validFilePaths.indexOf(filePath) !== -1) item.style = null
    // If not, hide file
    item.style = 'display:none;'
  }
}
```

You can add a small utility function to handle the case of resetting the filter. This occurs when the search field is blank. Add the following function after the filterResults function that was added to the userInterface.js file:

```js
function resetFilter() {
  const items = document.getElementsByClassName('item')
  for (let i = 0; i < items.lengths; i++) items[i].style = null
}
```

Here, you use a selector to select all div elements that have a CSS class of item, and make sure they're visible by removing any custom style attributes that would have marked them as hidden. Also, you want to make sure that the filterResults and resetFilter functions are publically available via the module API. Change the module .exports object at the bottom of the userInterface.js file so that it looks like this:

```js
// Makes sure function is exposed as public API
module.exports = {
  bindDocument,
  displayFiles,
  loadDirectory,
  bindSearchField,
  filterResults,
  resetFilter
}
```

That's all the changes to make to the userInterface.js file for now. Next, turn your attention to the app.js file and change it so that:

1 It binds on the search field in the user interface.

2 It passes the search field's term to the search tool lunr.

3 It then passes the results from the search tool back to the UI for rendering.

Change the code in the app.js file so that it looks like the code shown next.

Listing 3.11 Integrating the search feature into the app.js file

```js
// Function that combines user’s personal folder path with getting its list of files
function main() {
  userInterface.bindDocument(window)
  let folderPath = fileSystem.getUsersHomeFolder()
  userInterface.loadDirectory(folderPath)(window)
  // Listens for changes to search field’s value
  userInterface.bindSearchField((event) => {
    const query = event.target.value
    // If search field is blank, resets filter in UI
    if (query === '') userInterface.resetFilter()
    // If search field has a value, passes it to search module’s find function and filters results in UI
    search.find(query, userInterface.filterResults)
  })
}
```

After saving this file along with the previous files, reload the app. The app loads like before, but this time you'll find that when you type a term into the search field, the files and folders in the main area of the app are filtered to show only those that match the search term. If you then type a blank value into the search field, all the files and folders inside the current folder path are shown. Even as you double-click a folder and navigate into it to see its files and folders, the search field will work on that current folder and filter its contents, as shown in figure 3.6.

Figure 3.6 The search field filtering files based on their name inside Atom's hidden folder

With about six handcrafted files totaling no more than 281 lines of code and some npm modules, you've managed to build a file explorer. The file explorer can show the files in a folder, traverse the folders, and filter the files based on the name of the file as indicated in the original wireframe. Not bad, given the relatively small size of the code.

Next, you want to improve navigating through the app as well as getting files to open with their default application.

1『

没实现，问题应该是出在函数 `addToIndex`，lunr 升版后语法有改动。

[javascript - Can't add documents to lunr index after assignment (TypeError: idx.add is not a function) - Stack Overflow](https://stackoverflow.com/questions/44050415/cant-add-documents-to-lunr-index-after-assignment-typeerror-idx-add-is-not-a)

[Upgrading : Lunr](https://lunrjs.com/guides/upgrading.html)

0.x/1.x 
```js
var idx = lunr(function () {
  this.ref('id')
  this.field('text')
})

idx.add({ id: 1, text: 'hello' })
```

2.x
```js
var idx = lunr(function () {
  this.ref('id')
  this.field('text')
  this.add({ id: 1, text: 'hello' })
})
```

原书里的代码是旧语法的，所有 Chrome 调试台报错 `index.add is not a function`。

```js
// Adds file to index for searching against
function addToIndex(file) {
  index.add(file)
}
```

现在最新的：

```
"lunr": "^2.3.9",
```

试着改了下写法：

```js
// Adds file to index for searching against
function addToIndex(file) {
  // index.add(file)
  index = lunr(function () {
    this.field('file')
    this.ref('path')
    this.add(file)
  })
}
```

报错没了，但搜索无效，接着查了下书籍源码，发现 lunr 用的老版本：

```
"lunr": "^0.7.2",
```

在配置文件里将版本号改为 0.7.2，接着 `yarn` 更新一下依赖。报错也没了，但还是无法搜索。

到时意外发现了 2 个 bug 需引起警示！之前因为读「重构」的原因，喜欢将条件分支语句重构简化，但遇到 else 语句时，不能省略 else 的，否者逻辑都变了。除非前面的分支条件语句直接执行的是「出口」return，这种情况下即「卫语句」，后面的 else 是可以省略的。

```js
    // If search field is blank, resets filter in UI
    if (query === '') userInterface.resetFilter()
    // If search field has a value, passes it to search module’s find function and filters results in UI
    else search.find(query, userInterface.filterResults)
```

真是吐血了，总算找到 bug 了。解决思路：先把原书附件的代码整体拷进自己的项目里，跑了下，可行。接着一个文件一个文件的放弃修改，最后定位到 `userInterface.js` 文件的问题。接着一个个放弃里面函数的修改，定位待函数 `filterResults` 问题。一行行核对，竟然是循环语句里 `items.length` 写成了 `items.lengths`，你说 2 不 2。（2021-04-16）

试着用新版的 lunr 语法改写，搜索无效，目前未实现。待探索。（2021-04-16）

』

3.2.3 在界面上触发搜索功能

要让搜索框触发对输入的文件名进行搜索，你需要监听用户在搜索框中输入的事件。你可以通过在 userInterface.js 中添加一个名为 bindSearchField 的函数来实现，该函数在搜索框中绑定了一个事件监听器。在 userInterface.js 文件中，增加如下函数：

上述代码当用户在搜索框中输入内容后、释放按键的时候就会捕获到该事件（所以名字叫 keyup），你还需要将该函数添加到 userInterface.js 文件最后的 module.exports 对象中，这样就可以把该函数暴露给 app.js 文件了，如下所示：

这个函数的作用是当用户每次在搜索框中按键输入的时候都会执行一个函数。

这里你需要获取输入框中的值。如果值为空，不需要进行文件搜索。如果有值，需要对显示在主区域的文件列表进行过滤。要实现这部分功能，需要完成以下事情：

1、将文件夹的内容显示到主区域前，重置搜索索引。

2、当有新文件要显示在主区域时，需要将它添加到索引中。

3、当搜索框中的内容为空时，确保所有的文件都显示在主区域中。

4、当搜索框中有内容时，根据该搜索内容对文件进行过滤并显示。

不过首先，你应该将 search 模块作为依赖添加到 userInterface.js 文件内容的顶部。将 userInterface.js 文件顶部内容修改为如下所示：

这样就可以访问 search 模块了。加载了 search 模块后，接下来要修改的是 loadDirectory 函数。该函数每次被调用的时候都需要重置搜索索引，这样就能实现只针对当前文件夹内容进行搜索。将 loadDirectory 函数修改为代码清单 3.8 所示的内容。

代码清单 3.8 loadDirectory 函数被调用时重置搜索索引

完成之后，接下来需要修改 loadDirectory 函数下面的 displayFile 函数。修改后该函数要负责将文件添加到搜索索引中，同时也要确保 img 元素中保存了文件的路径，这样过滤搜索结果的时候就不需要再进行添加和删除 DOM 元素的操作了。将 displayFile 函数修改为代码清单 3.9 所示的内容。

代码清单 3.9 在 displayFile 函数中将文件添加到搜索索引中

接下来，新增一个函数用于处理在界面上显示搜索结果。该函数获取在主区域中显示的文件或者文件夹路径，判断该路径是否满足用户在搜索框中输入的搜索条件。在 userInterface.js 文件中的 bindSearchField 函数后面新增一个函数，如代码清单 3.10 所示。

代码清单 3.10 在 userInterface.js 文件中新增 filterResults 函数

你可以增加一个函数用于处理重置过滤结果的情况。这在搜索框中内容为空的时候会用到。将如下所示的函数添加到 userInterface.js 文件中的 filterResults 函数后面：

在上述代码中，使用了一个选择器将所有包含 item 的 CSS 类名的 div 元素都找到，并将所有设置将它们隐藏起来的样式属性清除，确保它们会显示出来。同时你还要确保 f ilterResults 和 resetFilter 这两个函数通过 module API 暴露出来。将 userInterface.js 文件底部的 module.exports 对象修改为如下内容：

到目前为止，所有对 userInterface.js 的修改都完成了。接下来，把注意力转移到 app.js 文件上，将其修改为：

1、在界面上需要监听搜索框。

2、将搜索关键词传给 lunr 搜索工具。

3、将搜索工具处理完的结果显示到界面上。

将 app.js 文件修改为代码清单 3.11 所示的内容。

代码清单 3.11 在 app.js 文件中集成搜索功能

将修改过的文件都进行保存后，重启应用。应用看起来和之前没区别，不过这次你会发现当在搜索框中输入关键词的时候，主区域中只会显示与之匹配的文件和文件夹。如果把搜索框中的内容清空，当前文件夹路径下所有的内容又都会显示出来。哪怕你通过双击某个文件夹进入该文件夹，搜索功能对当前文件夹也依然起作用，如图 3.6 所示。

通过 6 个手写的文件，其中不超过 281 行代码以及一些 npm 模块，你已经构建了一个文件浏览器应用。它可以展示文件夹中的内容、浏览具体的文件夹内容以及像线框图设计的那样针对文件名进行搜索。这么少的代码实现这样的功能，还算不错！

接下来，你要改进在应用内的导航功能，以及实现用默认应用打开某个文件。

图 3.6 对 Atom 隐藏文件夹中的内容针对文件名进行搜索

### 3.3 Enhancing navigation in the app

You've gotten to a stage where you can display the contents of the user's personal folder and allow them to traverse through those folders to see what other files and folders exist on their computer, as well as filter the files and folders by a search query. Now you'll help the user navigate backward as well, as there isn't currently a way to do that in the app.

To do this, you'll give the user the ability to navigate the folders via the current folder path — you'll make it a clickable path, with each folder in the path going to that folder's location on the computer.

3.3 改进应用内的导航功能

你已经实现了显示用户个人文件夹内容、浏览文件夹中的具体内容、通过搜索来过滤要展示的文件夹和文件的功能。现在还需要支持回退，目前应用中还没有这个功能。要实现这个功能，你需要支持让用户单击显示当前文件夹路径的时候回退到上一级内容 —— 要将显示路径中每个表示文件夹的部分都变成可单击的。

#### 3.3.1 Making the current folder path clickable

Figure 3.7 shows what you want to do.

Figure 3.7 When clicking any path in the current folder path in the top toolbar, you want to display the contents of the folder in the main area.

The current folder is currently a line of text that's displayed in the UI in the toolbar, but it can be used to do so much more. In this case, you're looking to change it so that it looks the same as it looks now but allows the user to load a different folder path by clicking a folder name in the path, like clicking a link in a web page, as shown in figure 3.8.

Let's begin by looking at the code that handles the display of the current folder in the toolbar, the displayFolderPath function in the userInterface.js file. You'll need to modify this function so that instead of returning the current folder path, it passes the folder path to another function, which will convert that folder path into a set of

Figure 3.8 How clicking a path item in the current folder path will end up loading that path in the app

span HTML elements. The span tags will contain not only the name of the folder, but also a data attribute referring to the path of that folder. This is so that when the folder is selected, you can pass that folder to the loadFolder function and load the folder in the app.

Let's begin by creating a function that will receive a folder name and return the folder as a list of HTML span tags, with the path for that folder added as an attribute on the span tag. Call this function convertFolderPathIntoLinks and place it in the userInterface.js file. First, you need to add a module dependency at the top of the file (after the search module require) to load Node.js's path module:

```js
const path = require('path');
```

The path module is used to return the path separator used by the operating system. In Mac OS and Linux, the path separator is a forward slash (/), but on Windows it's a backward slash (\). This will be used by the function to create the folder path for each folder as well as to display the full path for the current folder. In the convertFolderPathIntoLinks function, the following code is used:

```js
function convertFolderPathIntoLinks(folderPath) {
  const folders = folderPath.split(path.sep)
  const contents = []
  let pathAtFolder = ''
  folders.forEach((folder) => {
    pathAtFolder += folder + path.sep
    contents.push(`<span class="path" data-path="${pathAtFolder.slice(0,-1)}">${folder}</span>`)
  })
  return contents.join(path.sep).toString()
}
```

The function takes the path for the folder and turns it into a list of folders by splitting it on the folder path separator. With this list of folders in the current folder path, you can begin to create the span tags for each one. Each span tag will have a class attribute with a value of path, a data-path attribute that contains the path for that folder, and, finally, the name of the folder as the text inside the span tag.

Once the span tags are created, the HTML is joined together and returned as a string. This HTML is then used by the displayFolderPath function. It receives the current folder path and returns the HTML to be inserted into the toolbar. As a result, you'll need to update the function to insert HTML instead of text. Adjust the displayFolderPath function to this code:

```js
// Adds function to display current folder
function displayFolderPath(folderPath) {
  document.getElementById('current-folder')
    .innerHTML= convertFolderPathIntoLinks(folderPath)
}
```

The function now uses innerHTML to insert the HTML into the current-folder element in the screen, and the convertFolderPathIntoLinks function receives the folder path passed to the displayFolderPath function and returns HTML in its place. The nice thing about this change is how you only had to change a small part of the displayFolderPath function, rather than lots of changes in multiple places. This is a desirable goal with coding: construct it so that it can be altered with ease. With this change accomplished, you now need to handle clicking a folder name in the toolbar and having the screen navigate to that folder.

In the userInterface.js file, you'll add another function that will bind on a user clicking a folder name (in this case, any span element with a class of path) and return the folder path to a callback function. The callback function can then use the folder path to pass that to the code that handles loading a folder. Add the following code to the userInterface.js file, roughly toward the bottom of the file, but before the module .exports object:

```js
function bindCurrentFolderPath() {
  const load = (event) => {
    const folderPath = event.target.getAttribute('data-path')
    loadDirectory(folderPath)()
  }
  const paths = document.getElementsByClassName('path')

  for (let i = 0; i < paths.length; i++) {
    paths[i].addEventListener('click', load, false)
  }
}
```

You then want to call this function as part of the displayFolderPath function. Change the displayFolderPath function to this:

```js
// Adds function to display current folder
function displayFolderPath(folderPath) {
  document.getElementById('current-folder')
    .innerHTML= convertFolderPathIntoLinks(folderPath)
  bindCurrentFolderPath()
}
```

The userInterface.js file is easily extended to include extra functionality for handling clicks on path items in the current folder path — which is nice, because it allows you to easily alter your code without having to rewire whole swathes of the codebase.

3.3.1 实现当前文件夹路径可单击

图 3.7 显示了最终的效果。

图 3.7 当单击工具条上的当前文件夹路径时，需要在主区域中显示单击的文件夹的内容

当前文件夹路径现在在工具条上只是显示为一行文字，但它可以用来做更多的事情。在本例中，你需要将它改成样子上还是当前的样子，但当单击路径上的文件夹名的时候，需要显示文件夹中的内容，就像在网页上单击某个链接一样，如图 3.8 所示。

图 3.8 单击当前文件夹路径中的文件夹名会将其内容显示在应用中

我们先来看一下处理工具条上显示当前文件夹路径的代码 —— userInterface.js 文件中的 displayFolderPath 函数。你需要将该函数改成不再只是返回当前文件夹的路径，而是将文件夹路径传递给另外一个函数，这个函数将接收路径并返回一系列 HTML 的 span 元素。span 标签不仅包含文件夹的名字，还有一个 data 属性指向该文件夹的路径。这样当该文件夹名字被单击的时候，你就可以将该文件夹路径传递给 loadFolder 函数，将该文件夹内容在应用中显示出来。

我们从创建一个函数开始，该函数接收文件夹名字作为参数，并返回一系列包含了文件夹名的 span 标签，在 span 标签上还通过属性保存了文件夹所在的路径。将该函数取名为 convertFolderPathIntoLinks 并将它放在 userInterface.js 中。首先你需要在文件顶部（在加载 search 模块后面）增加一个模块依赖，用来加载 path 模块：

```
const path = require('path');
```

path 模块是用来获取操作系统的路径分隔符。在 Mac OS 和 Linux 中，路径分隔符是斜杠（/），但在 Windows 中，它是反斜杠（\）。这将在函数中用于为每个文件夹创建对应的路径，以及显示当前文件夹完整路径的时候用到。在 convertFolderPathIntoLinks 函数中，插入如下代码：

上述函数接收文件夹的路径作为参数，根据该路径上的分隔符将其转变为一个包含路径上文件名的列表。有了这个列表，就可以对其中每个文件夹名创建 span 标签。每个 span 标签包含一个名为 path 的类名以及一个 data-path 属性保存当前文件夹的路径，最后文件夹的名字以文本的形式被包含在 span 标签中。

span 标签创建好后，这些 HTML 内容就以字符串的形式连起来并返回。这段 HTML 内容会被 displayFolderPath 函数使用。该函数接收当前文件夹路径作为参数，然后获取到要插入工具条的 HTML 代码。最后你需要将该函数修改为插入 HTML 内容而不是文本内容。将 displayFolderPath 函数修改为如下内容：

上述函数现在使用 innerHTML 将 HTML 代码片段插入界面上的 current-folder 元素中，其中 convertFolderPathIntoLinks 函数接收传递给 displayFolderPath 函数的文件夹路径作为参数，并将最终的 HTML 返回来。这部分改动最妙的地方就在于你只需要修改一小部分 displayFolderPath 函数内容而不需要对多处进行大量代码的修改。这也是编程的理想目标：将代码重构，使其变得更容易修改。这部分修改完毕后，你现在需要处理当工具条上的文件夹名字被单击后，需要在界面上显示该文件夹的内容。

在 userInterface.js 文件中，你需要再增加一个函数，该函数用于监听用户单击文件夹名（本例中就是所有带 path 类名的 span 元素）的操作，并将被单击的文件夹路径传递给回调函数。该回调函数接收到文件夹路径后，将其传递给负责显示文件夹内容的函数。在 userInterface.js 文件底部的位置，但要在 module.exports 对象前，插入如下代码：

接下来要在 displayFolderPath 函数中调用上述函数。将 displayFolderPath 函数修改为如下内容：

userInterface.js 文件很容易就扩展出了新功能，可以处理当用户单击当前文件夹路径上的文件名的情况了 —— 这真是很棒，因为只是对代码进行了简单的修改而不是大刀阔斧的改动就达到了目的。

#### 3.3.2 Getting the app to load at the folder path

This simple one-line change enables the functionality to work, and the last code change you want to do before you put it into action is to make the span elements show a pointer when the cursor passes over them. Add the following code to the app.css file:

```css
span.path:hover { 
  opacity: 0.7; 
  cursor: pointer; 
}
```

With these changes saved, you can now reload the app, click through folders as normal, and then go back by clicking a folder in the current folder path. This ensures that users can navigate back to other folders, because otherwise they would be stuck. What you've done so far is replicate a feature that's common to all native file explorers across the operating systems (navigating folders via paths), but you added a twist to it so that the paths are clickable — not all file explorers do this. This shows how with Electron or NW.js you have the power to not only re-create desktop experiences using web technologies, but also combine them in ways to do new things that haven't been done in desktop apps before.

Now that you've added that feature, the next step is to handle opening files with their default application.

3.3.2 让应用随着文件夹路径的改变显示对应的文件夹内容

简单地修改一行代码就可以实现这个功能，同时也是最后需要修改的代码，那就是当鼠标光标悬停在 span 元素上的时候，将鼠标光标显示为手的形状。将如下代码添加到 app.css 文件中：

保存上述修改后，现在可以重启应用了。像往常一样单击某个文件夹，然后通过单击当前文件夹路径上的某个文件夹名字再回去。这个功能确保了用户可以再去访问其他文件夹，否则他就只能一直在当前文件夹中进行访问。到目前为止，你实现的功能是所有跨平台的文件浏览器应用都会有的功能（通过路径访问文件夹），不过你还实现了让文件夹路径变得可以被单击 —— 并非所有文件浏览器应用都这样处理。这也展示了，有了 Electron 或 NW.js，你不仅可以使用 Web 技术来构建桌面应用，而且还可以将两者结合实现以前桌面应用没有做的新东西。

现在你已经完成了这个功能，接下来要实现用系统默认的应用打开对应的文件。

#### 3.3.3 Opening files with their default application

So far in the app, you've focused a lot on interacting with folders, but now you need to look at how you can make the file explorer open files like images, videos, documents, and other items.

In order to implement this feature, you'll need to do the following:

1 Handle clicking on a file as opposed to a folder.

2 Pass the file path for that file to NW.js/Electron's way of opening external files.

We'll look at handling clicking a file first.

CLICKING A FILE

You'll probably remember from earlier on in the chapter that you detected whether the file you were rendering to the main area was a folder, and attached an event to it when it was double-clicked. You'll use the same pattern again to handle doubleclicking files.

In the userInterface.js file is the displayFile function that handles displaying the individual files and folders in the main area, as well as attaching events to them. Change the function so that it looks like the following listing.

Listing 3.12 Adding file double-clicking to the displayFile function

```js
function displayFile(file) {
  const mainArea = document.getElementById('main-area')
  const template = document.querySelector('#item-template')
  // Creates copy of template instance
  let clone = document.importNode(template.content, true)
  // Adds file to search index here
  search.addToIndex(file)
  // Alters instance to include file’s name and icon
  clone.querySelector('img').src = `images/${file.type}.svg`
  // Attaches file’s path as data attribute to image element
  clone.querySelector('img').setAttribute('data-filePath', file.path)
  // Adds double-click event listener to icon if it’s for a directory
  if (file.type === 'directory') {
    clone.querySelector('img')
      .addEventListener('dblclick', () => {
        loadDirectory(file.path)()
      }, false)
  } else {
    // Not a directory, therefore a file, so you can attach an event to it
    clone.querySelector('img')
      .addEventListener('dblclick', () => {
        fileSystem.openFile(file.path)
      }, false)
  }
  clone.querySelector('.filename').innerText = file.file
  // Appends template instance to "mainarea" div element
  mainArea.appendChild(clone)
}
```

The couple of extra lines of code allow you to listen to the file being double-clicked and attach it to a new function called openFile in the fileSystem.js module, which you'll now create.

The openFile function in the fileSystem.js module is going to call out to either Electron or NW.js's shell API. The shell API is able to open URLs, files, and folders in their default applications. To show you how compatible Electron and NW.js are as desktop app frameworks, you'll write one item of code that can be used across both frameworks without any need for modification.

In the fileSystem.js file, add the following snippet of code toward the top of the file, below the dependency declarations:

```js
let shell;

if (process.versions.electron) { 
  shell = require('electron').shell; 
} else {
  shell = window.require('nw.gui').Shell; 
}
```

1『

因为自己只用 Electron 开发，那么这里的代码从简，只有：

```js
const shell = require('electron').shell
```

或者更简洁的解构形式：

```js
const { shell } = require('electron')
```

』

This snippet of code can run on either an Electron app or an NW.js app, which means less code for you to have to write/adjust. Notice how Electron and NW.js call out to a shell object (though NW.js calls it via the GUI API, and with a title-cased name). If the app is running as an Electron application, it will load Electron's shell API, and if running NW.js, it will load NW.js' shell API.

With the shell API loaded for the given Node.js desktop app framework, you now call out to the shell API's method for opening files. Add the function shown in the following listing to the fileSystem.js file, right before the module.exports object.

Listing 3.13 Adding the openFile function to the fileSystem.js file

```js
// Calls the shell API’s openItem function with the file path
function openFile(filePath) {
  shell.openItem(filePath)
}
```

Notice anything funny? The shell API's function name for opening files is the same across both Electron and NW.js. It's a pleasant surprise that may seem unexpected unless you know a bit about NW.js and Electron's shared history.

With this new function, all you need to do now is make sure it's available as a public API function in the fileSystem.js file. Amend the module.exports object so that it includes the function, as shown in the following code:

```js
module.exports = {
  getUsersHomeFolder,
  getFilesInFolder,
  inspectAndDescribeFiles,
  openFile
}
```

I'd almost say you're done, but there's one more thing (to borrow a phrase from the late Steve Jobs). You want to give the app a visual indicator that the files and the folders can be clicked when the cursor is hovering over them. You can extend the last CSS rule you added earlier to the app.css file. As a reminder, it looked like this:

```css
span.path:hover { 
  opacity: 0.7; 
  cursor: pointer; 
}
```

Extend it so that it also applies to the file and folder icons in the main area:

```css
span.path:hover, img:hover { 
  opacity: 0.7; 
  cursor: pointer; 
}
```

With those changes saved, reload the app and have a go at double-clicking files in the Lorikeet app. You'll see that those files end up opening in their default applications.

Fantastic! You now have a functional file explorer that can open files, as well as explore folders and filter the view by name.

1『

跑起来后报错：`shell.openItem is not a function`。在官方文档里找到解决方案（2021-04-16）。

[shell | Electron](https://www.electronjs.org/docs/api/shell)

shell.openPath(path)

path String

Returns `Promise<String>` — Resolves with a string containing the error message corresponding to the failure if a failure occurred, otherwise "".

以桌面的默认方式打开给定的文件。所以只需将方法 `openItem` 更改为 `openFile` 即可。

』

3.3.3 实现使用默认应用打开对应的文件

到目前为止，我们大部分精力都在如何和文件夹进行交互上，现在需要实现如何能够让文件浏览器打开诸如图片、视频、文档以及其他类型的文件。

要实现这个功能，需要完成以下事情：1）处理单击文件的情况。2）以 NW.js/Electron 打开外部文件的方式将文件路径传递给它。

我们先来处理单击文件。

你可能还记得在此前的章节中，我们介绍了如何判断在主区域中渲染的是文件夹，并监听双击文件夹的事件。我们也将使用同样的方法来处理双击文件的情况。

在 userInterface.js 文件中，是 displayFile 函数负责在主区域中显示文件和文件夹以及监听对它们的操作。将该函数修改为代码清单 3.12 所示的内容。

代码清单 3.12 在 displayFile 函数中添加处理双击文件的操作

上述添加的这部分代码，可以实现监听文件的双击事件，并在回调函数中调用 fileSystem.js 模块中的 openFile，接下来你需要实现 openFile 函数。

fileSystem.js 模块中的 openFile 函数需要调用 Electron 或者 NW.js 的 shell API。shell API 能够使用系统默认的应用打开 URL、文件以及文件夹。为了考虑兼容性，你写的代码需要在两个框架中都能工作，这样可以避免后续的改动。

在 fileSystem.js 文件中，在加载依赖之后添加如下代码：

上述代码在 Electron 版和 NW.js 版的应用中都可以运行，这意味着后续不需要对这部分代码进行改动。这里要注意是如何获取 Electron 和 NW.js 中 shell 对象的（NW.js 是通过 GUI API 调用它的，并且 shell 这个名字也是首字母大写的）。如果应用运行在 Electron 环境中，就会加载 Electron 的 shell API，如果是运行在 NW.js 中，就会加载 NW.js 的 shell API。

指定 Node.js 桌面应用开发框架中的 shell API 加载好后，你现在就可以调用 shell API 上的方法来打开文件了。将代码清单 3.13 中的代码添加到 fileSystem.js 文件中 module.exports 对象前的位置。

代码清单 3.13 在 fileSystem.js 文件中添加 openFile 函数

注意到有意思的东西了吗？不管是 Electron 还是 NW.js，用于打开文件的 shell API 的函数名都是一样的。这对于不了解 NW.js 和 Electron 那段共享的历史的人来说，多少是有点惊讶的：

实现了这个新函数后，接下来需要将它以公共 API 的形式在 fileSystem.js 文件中暴露出来。在 module.exports 对象中将该函数添加进去，如下所示：

快完成了，但还有一件事情（借鉴自 Steve Jobs 的名言）。当鼠标光标移动到文件或文件夹上的时候，你需要在视觉上显示它们是可以单击的。你可以通过扩展上次在 app.css 文件中添加的 CSS 规则来实现。提醒一下，上次添加的内容如下所示：

```css
span.path:hover { 
  opacity: 0.7; 
  cursor: pointer; 
}
```

将其扩展为对主区域中的文件和文件夹图标都有效：

```css
span.path:hover, img:hover { 
  opacity: 0.7; 
  cursor: pointer; 
}
```

保存上述修改后，重启应用，在 Lorikeet 应用中双击文件的时候，你就会发现它们最终会被系统默认的应用打开。

太棒了！我们现在已经完成一个功能完备的文件浏览器了，它可以打开文件，可以浏览文件夹，还可以根据名字进行搜索。
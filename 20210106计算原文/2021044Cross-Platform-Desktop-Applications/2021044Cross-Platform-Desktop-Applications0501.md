 Managing events and streams Installing and using npm modules Packaging your apps with npm

Long before NW.js and Electron, a programming framework called Node.js wasdemoed by Ryan Dahl at JSConf in Berlin, showing a way to write and executeserver-side JavaScript. Since that demo back in 2009, Node.js has spawned a hugeecosystem of libraries, applications, utilities, and frameworks (including NW.js andElectron). As a programming framework, it offers a different approach comparedwith other programming languages and their frameworks.

For those new to the world of Node.js, this chapter offers a gentle introductionto the programming framework and a chance to learn how to apply it not onlywhen developing desktop apps, but also in other projects such as web apps. Forthose already familiar with Node.js, this chapter covers a lot of the ground that you

91

92

CHAPTER 5 Using Node.js within NW.js and Electron

might already be familiar with (the event loop, callbacks, streams, and node modules),so feel free to skip it.

One of the underrated features of both NW.js and Electron is the massive collec-tion of packages available through Node.js's package management tool, npm, that canbe used for building desktop apps. This chapter will show how you can put Node.js touse when developing your desktop apps, as well as for organizing your code.

5.1 What is Node.js?

Node.js is a programming framework created by Ryan Dahl back in 2009. It provides away to write server-side programs with JavaScript and uses an evented architecture tohandle the execution of that code. The programming framework combines V8 (aJavaScript engine) with libuv, a library that provides access to the OS libraries in anasynchronous fashion.

Because of this, JavaScript code is executed by Node.js in such a way that code exe-cuting on one line doesn't block the execution of the code on the next line. This isdistinctly different from other languages where code on one line executes after thecode on the previous line has finished executing. It's important to get familiar withhow Node.js handles executing code. You'll tackle this in the next section.

5.1.1

Synchronous versus asynchronous

To clearly differentiate between synchronous and asynchronous programming, let'srevisit the case of reading the contents of a folder using Node.js and compare it tohow it can be done with Ruby. Ruby is a programming language with a simple syntaxthat works in a synchronous fashion, making it a good example to compare Node.jsagainst. Here's an example written in Ruby:

files = Dir.entries '/Users/pauljensen'puts files.length

This is a nice example that demonstrates the appeal of Ruby—the clean syntax. In thiscase, the first line executes, and then the second line executes when the first line has fin-ished. This is known as blocking. If I were to insert the following between lines 1 and 3,

sleep 5

that line would cause the program to block for 5 seconds before printing out the num-ber of files in the list. Figure 5.1 illustrates how that executes in time.

We refer to this as synchronous programming—each operation waits on the previousoperation to complete. There may be cases where you want to start doing somethingelse while you're waiting for the list of files to be counted, but can't because the previ-ous line hasn't finished yet.

What is Node.js?

93

files = Dir.entries '/Users/pauljensen'sleep 5puts files.length

Figure 5.1 A diagram showing how Ruby's execution of code is synchronous

The following listing shows you can do the same thing as the Ruby example in a syn-chronous fashion in Node.js.

Listing 5.1 Synchronous files count in Node.js

const fs = require('fs');const files = fs.readdirSync('/Users/pauljensen'); console.log(files.length);

Gets the list of files in the directory

Counts how many files there are

Though this isn't as elegant as the Ruby code example, it does exactly the same thing.Notice that the call to the file system API's readdirSync function has the word Syncattached to the end of it. This is to make clear that the function operates in a synchro-nous fashion. You would still have the issue of blocking code that delays the executionof other code until it has completed its operation.

What is needed is a way to fire off an operation, let it go off and do what it's doing,and then when it's ready to return some data, send that data to another function, or acallback, as it's commonly referred to in Node.js. The next listing shows an example ofthe same task using asynchronous Node.js.

Listing 5.2 Asynchronous files count in Node.js

const fs = require('fs');fs.readdir('/Users/pauljensen', (err, files) => { if (err) { return err; } console.log(files.length); });

Counts how many files there are

Gets list of files in directory

If there's an error, returns the error

94

CHAPTER 5 Using Node.js within NW.js and Electron

You can see that the code to log out the number of files in the folder is inside a func-tion (the callback). This function will execute the moment the readdir function haseither returned an error (as the err object) or the list of files. Figure 5.2 shows analternative way to visualize it.

b

Look up the directory.

c

Start doing other things thataren't waiting on the resultsof the directory look-up.

d

e

Get the results of thedirectory look-up.

Great! Pass those results tothe function that was waitingto process them.

Figure 5.2 Asynchronous programming's flow of execution

Any code that's placed after the callback function on the next line will execute imme-diately. For example, you can place a simple line to log out a message after the call-back, such as this:

const fs = require('fs');fs.readdir('/Users/pauljensen', (err, files) => {if (err) { return err.message; }  console.log(files.length);});console.log('hi');

When you run this with Node.js, you should see the following result in Terminal orCommand Prompt:

hi56

You'll notice that the console.log statement executed before the file count did, eventhough it was placed after it in the code. This is one of the aspects of asynchronousprogramming that newcomers to Node.js initially struggle to get their head around.The best way to illustrate it is with a diagram like figure 5.3.

If you've worked with Gantt charts in project management, figure 5.3 might befamiliar to you. Whereas synchronous execution mirrors the typical waterfall flow ofa sub-optimal project plan, asynchronous execution mirrors the flow of a projectwhere multiple tasks can run in parallel, and the project completes faster as a result.It's important to keep this in mind when working with Node.js. It's one of the biggerconcepts to digest when you first start working with it—otherwise, the code will exe-cute in an order different from what you expect, and that can lead to confusion andloss of time.

What is Node.js?

95

Synchronous execution

fs.readdirSyncconsole.log(files)console.log('hi');

Asynchronous execution

fs.readdirconsole.log(files)console.log('hi');

Figure 5.3 Comparison of the ways in which synchronous and asynchronous differ in the time order of executing code.

5.1.2

Streams as first-class citizensAnother aspect of Node.js is the way that it encourages you to use streams as a methodof handling data within your apps. This has the benefit of allowing you to handletransmitting and processing large amounts of data without requiring large amounts ofmemory. Cases where you would want to do this include uploading large files to Ama-zon S3 or reading a big JSON file containing addresses and filtering the data to returnonly a subset that's then written to a file. When developing any kind of app, it's impor-tant to ensure that it's efficient in its memory usage—otherwise, it will slow down thecomputer it's running on and eventually stop working, as illustrated in figure 5.4.

In figure 5.4, you can see how loading entire files into memory can become prob-lematic. Now, you might say that there's little chance you'll be loading a file that's big-ger than the amount of RAM on a server, but when a server's amount of free RAM isused up over time, a small file bigger than the amount of free RAM can end up beingthe straw that breaks the camel's back.

96

CHAPTER 5 Using Node.js within NW.js and Electron

Server with10 TB disk

and

64 GB RAM

b

You have a large log file thatfits on the server's hard disk.

100 GBlog file

c

The server has enough disk spaceto keep the file, but not enoughRAM to load it into memory.

Error: Out of

memory

Process log file

d

Someone runs a job to processthe file, which loads the file intomemory. The process fails whenthe server runs out of memory.

Figure 5.4 How loading a large file for processing creates pitfalls if the file is larger than total RAM available or the amount of memory free in the server

What can you do about this? You can use streams to load the file, a bit at a time, as youcan see by looking at the following example of using streams in Node.js.

Let's say you have a text document that you want to scan the contents of for a par-ticular term, but it's large, and loading all of it in memory isn't ideal. What you wouldlike to do is load the text document in chunks and scan each chunk for the term. Ifthe term is found, you record that the term is in the text document—otherwise, youconclude that you have yet to find the term in the text document. This is a live searchof a text document, where the contents of the text document are not indexed.

Find a book you like that's available online—I'll pick Frank Herbert's Dune (a greatbook). Let's take a phrase from the end of the book, in this case, history will call youwives. You want to scan the book for this term, but you don't want to load the wholebook's contents into memory in order to find it. Instead, you'll load it chunk by chunkuntil you come across the term and can verify that it appears in the book. (You can geta copy of the book from http://mng.bz/9sOS.)

You can use Node's file system API to help you read the contents of the file as a

stream with the following code.

Listing 5.3 Streaming a book's contents

'use strict';const fs = require('fs');const filePath = '/Users/pauljensen/Desktop/Frank-Herbert-Dune.rtfd/TXT.rtf'; const fileReader = fs.createReadStream(filePath, {encoding:'utf8'});let termFound = false;

Creates readablestream of book file

What is Node.js?

97

fileReader.on('data', (data) => {        if (data.match(/history will call you wives/) !== null) {  termFound = true; }});

fileReader.on('end', (err) => {  if (err) { return err; } console.log('term found:',termFound);});

After reading file, reports errors or whether term was found

For each chunk of data . . .

. . . checks if there's a match for that term

You create a readable stream for a rich text file, and tell it to expect the contents ofthe file to be encoded in UTF-8. Then, you attach a callback function to the data eventso that every time a piece of data is read from the file, you check whether the term iscontained in that piece of data. If it is, you set the termFound variable to true—other-wise, it remains set to false.

When the readable stream has finished reading the contents of the file, it will emitan end event, to which you attach a callback function where you either return an errorobject or log whether the term was found.

If you run the example code along with the text of the book in your terminal, you

can expect to see the following result in your terminal:

$> node findTerm.js=> term found: true

What you've achieved here is a way to read a Rich Text Format (RTF) document andfind a term within. But you could have done the same thing with less code by using thefile system API's readFile function, with the code shown next.

Listing 5.4 Term finding with Node.js's fs.readFile function

'use strict';

const fs = require('fs');const filePath = '/Users/pauljensen/Desktop/Frank-Herbert-Dune.rtfd/TXT.rtf';let termFound = false;

fs.readFile(filePath, {encoding: 'utf8'}, (err, data) => {  if (err) { return err; }           if (data.match(/history will call you wives/) !== null) {  termFound = true; } console.log('term found:',termFound); });

Reports back if term is found

Checks whether term is found

Loads file's contents in full

Checks for error and returns if that's the case

This example achieves the same result but only requires one callback function ratherthan two callbacks for the readable stream version. So, why would you use streamsover the simpler fs.readFile method?

98

CHAPTER 5 Using Node.js within NW.js and Electron

The answer is speed. Streaming the contents of a file with fs.createReadStreamcompletes faster than attempting to read the contents of a file with fs.readFile. Youcan try this out by using Node's process.hrtime function to measure the time it takesfor the process to complete. Adjust the previous examples so they include the follow-ing line at the top of each file:

const startTime = process.hrtime();

Then, include the following lines after the console.log statement printing whether theterm was found:

const diff = process.hrtime(startTime);console.log('benchmark took %d nanoseconds', diff[0] * 1e9 + diff[1]);

Here, calling the process.hrtime function without any arguments records a time-stamp, which you store as the startTime variable. After creating this variable, youcompare it to a later time, after the code has finished reading the contents of the RichText Format document and printed out whether the term was found. By passing thestartTime variable into the process.hrtime function, you get back the differencebetween now and that startTime as a tuple of seconds and nanoseconds. You thenprint the time difference using console.log, allowing you to see how long it took toread the contents of the document with both approaches.

Your results may vary, but in running them on my laptop (a 13-inch mid-2014MacBook Pro with 16 GB RAM and a 3 GHz processor), I get the results shown intable 5.1.

Table 5.1 Streaming saves time

API function

Time taken

fs.readFile

fs.createReadStream

62.61 milliseconds

21.59 milliseconds

You can see that in this test run, the streaming function is almost three times as fast asthe fs.fileRead function (usually, for reliable metrics you would do lots of test runsand measure the standard deviation and variance between each function's results, butthat's beyond the scope of this book). This result varies only slightly between multipletest runs.

Structuring your code to make use of streams will allow for it to execute faster andbe more efficient with memory. You can see this for yourself by tracking the memoryusage of both approaches using Node's process.memoryUsage function in the codeexamples. In the code examples, after they have finished reading the data of the doc-ument, insert the following line of code:

console.log(process.memoryUsage());

What is Node.js?

99

When you add this line to both the streaming-read and full-read examples and thenrun them, you should see this output for the full fs.readFile example:

{ rss: 36184064, heapTotal: 20658336, heapUsed: 16310280 }

And for the streaming file example:

{ rss: 18276352, heapTotal: 6163968, heapUsed: 2869000 }

What's noticeable already is that the memory usage numbers are smaller in the stream-ing file code than in the full readFile code (49% smaller RSS, 70% smaller heapTotal,and 82% smaller heapUsed). Not only are streams faster, they're more memory effi-cient, too.

5.1.3

Events

Another kind of API interface that Node.js exposes to developers is the event pattern.Those who have used jQuery or addEventListener in browser-based JavaScript will befamiliar with this pattern, and the fs.createReadStream example discussed in the lastfew pages also exposes an events API interface where functions can be executed whena chunk of data is read, when the file has finished streaming, or when an error occursreading the file.

This fits with the way that Node.js's code is executed: it makes use of the event loop.This involves executing non-blocking code when an event is triggered, meaning thatother events can occur at the same time. In various programming languages such asRuby and Python, there's a way to run code in an asynchronous fashion within anevent loop, but this requires using libraries that are structured to execute non-blockingcode, such as EventMachine for Ruby, and Twisted for Python. With Node.js, there'sno external library to load and execute—the programming framework has a built-inevent loop that it automatically begins executing when it starts.

Not only do various API functions in Node.js expose an events interface, butNode.js also provides a library for creating your own event interfaces using theEventEmitter module. Here's an example of using the EventEmitter module to greetsomeone with a message when the welcome event is emitted:

'use strict';

const greeter = new events.EventEmitter();

greeter.on('welcome', function () {  console.log('hello');});

greeter.emit('welcome');

An event emitter instance called greeter is created, and you create an event on it withthe name 'welcome', which when emitted will log 'hello'. You then emit the event

100

CHAPTER 5 Using Node.js within NW.js and Electron

'welcome' on the greeter object. If you run the code in your Node.js REPL, you cansee that the message「hello」is printed in the Terminal.

As you work through NW.js's and Electron's APIs, you'll see the event pattern in

use and get a chance to work with it as you go through the examples in the book.

5.1.4 Modules

Structuring code into reusable libraries is an important part of any programming lan-guage's ecosystem, and a good package system goes a long way toward helping devel-opers be productive. In Node.js, groups of functions are organized into modules, andthese modules can be easily created and reused in other places.

Node.js uses a module format called CommonJS. The CommonJS spec in brief is astandard for creating nonbrowser JavaScript libraries that can work with each other,but has also been applied to browser-based JavaScript libraries as well.

Let's work through an example of creating a module in order to get a better feel

for it.

CREATING PUBLIC API METHODS WITH MODULE.EXPORTSTo make functions, objects, and other values publicly available in a JavaScript file,the developer has to use either one of two specific expressions: exports or module.exports. Say you have a function for performing some business logic in your file,and you want to be able to load the file and call the following function:

function applyDiscount (discountCode, amount) { let discountCodes = { summer20: (amt) => {  return amt * 0.8; }, bigone: (amt) => {  if (amt > 10000) {  return amt - 10000;  } else {  return amt;  } } };

if (discountCodes[discountCode]) { return discountCodes[discountCode](amount); } else { return amount; }}

If you want to make this a publicly available function on the file, you can do thatlike so:

exports.applyDiscount = applyDiscount;

What is Node.js?

101

Or like this:

module.exports = { applyDiscount: applyDiscount};

Or if the file has only one function that you want to call, you could export the func-tion like this:

module.exports = applyDiscount;

These methods don't have to expose only functions or objects; they can be used toexport any kind of value in JavaScript. This allows you to organize your code as youlike and make it easily reusable. The next stage is to be able to load libraries together,via the require method.LOADING LIBRARIES VIA REQUIREOnce you have a file that has publicly available functions or values, you can theninclude it in other files by use of the require function. For example, say you turnedthe bit of business logic for applying discounts into a file called discount.js. You couldinclude that file in another place, say at the same location as the discount.js file in theapp's folder, like this:

const discount = require('./discount');

You would now have the file's exported functions or objects loaded and attached tothe discount variable in your file. You can then call the applyDiscount function inyour file like so:

discount.applyDiscount('summer20', 4999);

This allows you to structure your code into small, reusable libraries that are easy tounderstand and easy to use elsewhere. This is a key philosophy of Node.js—to use andcombine lots of little modules when developing rather than create large files that aredifficult to read through and understand.

The require function isn't used only to load local files; it can be used to load mod-ules, as well. The Node.js API contains a set of modules that can be loaded explicitlyby using a require function that's passed either the name of a module or the relativefile path to the module, like this example:

const os = require('os');

That code loads Node's OS module. Node.js provides a number of modules in itscore, and you can load them without having to install them. A few of the modules areloaded as global objects in Node.js's namespace, and the rest have to be loaded via therequire function. The list of modules that Node.js provides by default can be viewedat https://nodejs.org/api.

102

CHAPTER 5 Using Node.js within NW.js and Electron

Apart from Node.js's core modules, there's also the ability to install and use mod-ules via npm (which stands for Node Package Manager). npm is a free central reposi-tory that lets you publish and download modules to use in your apps. You can searchfor and find modules via https://npmjs.com and then install them (for example,request) via this command on the Terminal:

npm install request

This will download a copy of the request module (a library used to make HTTPrequests), and place it in a folder called node_modules. Then you'll be able to loadthat module within your code as a locally installed module as you would with Node'smain modules, like this:

const request = require('request');

This will load the request module that's located in the node_modules folder. If youopen that folder, you'll see the folder for the request module there. The requirefunction in Node.js is designed to work so that if you pass the name of a module, it willlook up the modules that are either available in Node.js' core, or installed globally, orinstalled locally in the node_modules folder.

You can also install npm modules globally, meaning that they're not installed inthe app's node_modules folder but instead in a folder where they're available to anyNode.js process that loads via require. Examples of npm modules installed globallytend to be build tools like Grunt and Bower. To install them globally, append a –gargument to the npm install command, like this:

npm install –g grunt-cli

The reason for installing grunt-cli globally in this case is so you only have to install itonce, not once per app you use it with. Also, npm modules can have binary com-mands, and installing an npm module globally allows you to run that binary commandwithout having to install the npm package each time. The same can be said for install-ing NW.js and Electron as global npm modules.

This is something of a quick overview of what Node.js offers from a developer'sperspective. Given that we've been discussing installing third-party modules, we'lllook at the mechanism behind installing third-party modules—the package man-ager known as npm.

5.2

Node Package Manager (npm)Node Package Manager (or npm) is the tool used by Node.js developers to handleinstalling libraries. It's built into Node.js by default and has proven to be a populartool, maintaining a central repository of over 400,000 packages to date. It allows devel-opers to download modules for use in their apps as well as publish modules for othersto use.

Node Package Manager (npm)

103

5.2.1

Finding packages for your appVisit npmjs.com, and you'll be able to find out more information about npm and whatit does, besides finding modules that may be of interest, such as webpack and Type-Script. You can search for packages by typing in a term that matches the name,description, or keywords used for those modules. Alternatively, you can click the mostpopular packages and see whether they're of use to you.

Once you've found a package you want to use in your app (or experiment with),

you can install it via the command line like so:

npm install lodash

You'll now have the lodash module installed inside the node_modules folder in thecurrent directory that your command-line terminal is in, and you'll be able to use it inyour code like this:

const _ = require('underscore');

5.2.2

Now, any places in your code where require('lodash') is called will have the modulealready loaded, and reuse it from require's module cache, rather than go throughthe process of loading the module from scratch.

Tracking installed modules with package.jsonAfter a while, you'll be using a bunch of modules in your app, and you'll want to keepa record of what they are, as well as which version of them you're using. You'll need amanifest file. npm uses a manifest file called package.json as the way to describe an npmmodule, as well as what module dependencies it has. In the previous example, youinstalled the lodash module but did not append its information to a package.json file.

Create a package.json file to track your dependencies. You can start that process by

running this command in your terminal:

npm init

This triggers the process of creating a package.json file by asking a bunch of questionsin the command line and populating the package.json file's contents as a result. Bythe end of the question process, you should see a package.json file that resembles this:

{ "name": "pkgjson", "version": "1.0.0", "description": "My testbed for playing with npm", "main": "index.js", "scripts": { "test": "echo \"Error: no test specified\" && exit 1" }, "author": "", "license": "ISC"}

104

CHAPTER 5 Using Node.js within NW.js and Electron

This creates a package.json file that can store configuration information for yourapp and that also contains information about the module, what file it should loadwhen required as a dependency, any script commands it has, and what softwarelicense it has.

Now that you've got a package.json file to work with, you can track your module

dependencies. Run the following command in your terminal:

npm install lodash --save

Not only will it install the lodash module, it will also add the following configurationinformation to the package.json file:

"dependencies": { "lodash": "^4.15.0"}

The name and version of the module are now stored in the package.json file, meaningthat you can track your app's modules and versions.

Now, if you use version control for your app (like Git) and want to allow otherdevelopers to set up the app quickly on their computer, they'll be able to install all ofthe app's module dependencies by running the following command at the same work-ing directory as the package.json file:

npm install

When passed no arguments, npm install will look for the package.json file and installall the module dependencies that are listed in the file.

INSTALLING DEVELOPMENT-ONLY DEPENDENCIESThere are some module dependencies that you want to use only for development pur-poses and not as part of the app, such as testing libraries like Mocha and Karma. Youcan install these modules as development dependencies using the following com-mand from your terminal:

npm install mocha –-save-dev

This will install the Mocha module into the node_modules folder and will add the fol-lowing JSON to the package.json file:

"devDependencies": { "mocha": "^3.0.2"}

Being able to separate dependencies required for the app to run from dependenciesused to test and build the app helps developers ship smaller binaries of the app.

5.2.3

Node Package Manager (npm)

105

Packaging your modules and apps with npmOne of the major factors in collaborating successfully on an npm module is how easyit is for other developers to install and get running on their local developmentmachine. Packaging your modules and apps so that they install and run seamlesslyfrom one machine to another is key to this.CONTROLLING DEPENDENCY VERSIONS IN PACKAGE.JSONWhen it comes to installing an app that has Node.js modules, there's first a question ofwhat to track in version control. There are two things that can be done: either the devel-oper has the Node.js modules and all their files checked into version control, or theycheck the package.json file into version control (which will track what dependencies theapp has) and exclude the node_modules folder from being tracked by version control. Developers tend to go for the latter approach for two reasons. The first is thatthere are fewer files to track in version control (making it easier to use the versioncontrol tool to look through only the app files). The second is for compatibility withmultiple OSs. There are some Node.js modules that use extensions written in C++,and for those Node.js modules to be installed, they need to be compiled on the devel-oper's machine. If the Node.js module is compiled on Mac OS and then checked intoversion control, and then someone else wants to use it but on a different computer(Linux or Windows), then the Node.js module will fail to work because it has beencompiled to work against a different OS.

My personal preference is to not only track the package.json file of your app, butalso lock down the version of the dependencies in that package.json file. To explain:When a Node.js module is added to the package.json file via npm install, you'llnotice that the dependency listing in the package.json will show a caret character (^)before the version number of the module. The ^ indicates to npm that when installingthat dependency, it can install a more up-to-date version, so long as it's compatiblewith the major version specified in the package.json file. As an example, say you installa version of CoffeeScript for use in your app:

npm install coffee-script --save

If you look at the package.json file, you'll see something like this:

"dependencies": { "coffee-script":"^1.10.1"}

Notice the ^ preceding the version 1.10.1 of CoffeeScript. You've installed version 1.10.1of CoffeeScript, but let's say a couple months later someone downloads a copy of theapp's code from GitHub and runs npm install to download the dependencies. IfCoffeeScript 1.11.0 comes out, or even 1.10.2, those will be downloaded instead of1.10.1. The caret character indicates that you can install a more up-to-date versionof the dependency, so long as the changes are only at patch level (the number of theversion after the second dot, indicating a bug fix or change that doesn't affect existing

106

CHAPTER 5 Using Node.js within NW.js and Electron

functionality) or minor level (the number after the first dot in the version number,indicating a small change to the module which shouldn't cause breaking changes toyour app). If CoffeeScript 2.0.0 is out, it won't install that version because that's amajor-level change (indicating new features/changed API and therefore likely tocause breaking changes to your app).

The idea behind this approach is to allow developers to pull in fixes and non-breaking updates to their dependencies without having to manually update thosenumbers in the package.json file. This can work as long as the developers of Node.jsmodules follow the principles of semantic versioning, as well as take care not to intro-duce bugs during those updates. From a DevOps perspective, this can provide roomfor production errors to creep in (hence, the need for a comprehensive testing strat-egy, which I'll cover later in the book). You want control over the version of thedependencies.

How do you lock down the versions of the dependencies? There are two ways youcan do this. The first is to remove any ^ or ~ characters from the front of the versionnumbers of the dependencies listed in the package.json file. If you don't want to dothat manually, the alternative approach is to use npm shrinkwrap.

npm's shrinkwrap command will lock down the version of dependencies that areinstalled with the module. Running npm shrinkwrap in the same working directory asthe package.json file will produce a file called npm-shrinkwrap.json, a JSON file thathas configuration information to specify exactly what version of the module should beinstalled, which looks like this:

{ "name": "pkgjson", "version": "1.0.0", "dependencies": { "underscore": {  "version": "1.8.3",  "from": "underscore@",  "resolved": "https://registry.npmjs.org/underscore/-/underscore-1.8.3.tgz" } }}

This file helps npm know exactly what versions of the software should be installed forthe module.

Based on my experience working with Node.js since 2010, my suggestion is to usethe approach of keeping dependencies in the package.json file up to date, keep thenode_modules folder out of version control, and, when needed, use npm shrinkwrapto lock down the dependencies in use.PUBLISHING APPLICATIONS AND MODULES TO NPMOnce you've created a module or an app and begun tracking its dependencies, you maywant to make it available for others to download and use. You can do that through npm.You'll need to create a free account with npm (unless you have one already) by going to

Summary

107

npmjs.com and clicking the signup link. Fill in your details, and once you've set up youraccount, in your command-line terminal, run the following command:

npm login

Once you've logged in, you'll be able to publish modules from the command line up tonpm. Say you've created a module that you want to be able to install via npm. In the sameworking directory as the package.json for the module, run the following command:

npm publish

That will push a copy of the module up to npm, and you'll then be able to install it vianpm install. You'll also be able to publish updates to your package using this com-mand, and incrementing the version number of the module in the package.json file.

5.3

SummaryThis chapter presented a broad introduction to Node.js. Now you have a better under-standing of what it's like to use as a programming framework, and you'll be able tostart implementing it in your apps. Things that you'll want to take away from thischapter include the following:

 Node.js uses asynchronous programming. Make sure to structure your code to

use callbacks and streams when interacting with Node.js' APIs and modules. Streams are an effective way to read/write data without using much memory. Some of the browsers' APIs overlap with Node.js's APIs. Note when you use

them because they will have subtle differences.

 Use npm modules to install libraries that will help you build app features faster. You can publish modules to npm to share your libraries with the community.

In chapter 6, we'll turn our attention back to NW.js and Electron and take a look athow they operate under the hood, so you can understand how they work differently.

Exploring NW.jsand Electron's internals

This chapter covers Understanding how NW.js and Electron combine

Node.js and Chromium

 Developing with Electron's multi-process

approach


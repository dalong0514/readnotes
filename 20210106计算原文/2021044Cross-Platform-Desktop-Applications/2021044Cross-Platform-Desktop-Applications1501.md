notification app

When working day-to-day with computers, users tend to have a number of appsopen and running while focusing on one app at a time. Applications such as chatapps, file downloaders, and music players may have activity, but if the user doesn'thave them in direct view or focus, they might miss that activity.

One feature provided by OSs is allowing notifications to be displayed as smalldialogs that overlay all open and focused windows, usually in the top-right corner ofthe desktop window, helping users stay informed of important activity. Both NW.jsand Electron provide notification APIs to ensure that your apps can communicateevents using the OS's notifications system.

234

Creating the Watchy app in Electron

235

15.1 About the app you'll make

In the world of social media, events need to be monitored and tracked in real time. Asbusy users of our computers, we can't afford to be glued to our screens waiting for anevent to happen. Say, for example, your app monitors mentions of a topical item, andyou want your app to display the contents of any tweet that mentions that topic. You'dlike to alert the user that someone mentioned X, whether it's a laundry detergentbrand (after seeing an amusing TV ad that made them laugh), or a tweet about arather slow football game, and the user wants to know when a goal is scored.

For this use case, I've created an app called Watchy. You type in a term that youwant to monitor mentions of on Twitter, and the app connects to Twitter's StreamingAPI, displaying as desktop notifications any tweets mentioning the term.

If you'd like the Electron version of the app, you can download the source codefor it from the watchy-electron app in the book's GitHub repository at http://mng.bz/URx8.

We'll first look at how you can make this app in Electron, and then look at NW.js's

implementation.

15.2 Creating the Watchy app in Electron

Watchy is a small app that combines the use of Twitter and a third-party library fordesktop notifications. You'll start by creating the app folder. Create a folder namedwatchy-electron, and then create the package.json file shown next.

Listing 15.1 The package.json file for the Watchy Electron app

{ "name": "watchy-electron", "version": "1.0.0", "description": "A Twitter client for monitoring topics, built with Electron

for the book 'Cross Platform Desktop Applications'",

"main": "main.js", "scripts": { "start": "node_modules/.bin/electron .", "test": "echo \"Error: no test specified\" && exit 1" }, "keywords": [ "electron", "twitter" ], "author": "Paul Jensen <paulbjensen@gmail.com>", "license": "MIT", "dependencies": { "electron-notifications": "0.0.3", "electron ": "^1.3.7", "twitter": "^1.3.0" }}

236

CHAPTER 15 Making desktop notifications

The package.json file has a few more app dependencies than other apps—you have adependency on the Twitter API client, as well as on the electron-notifications module,documented at https://github.com/blainesch/electron-notifications.

You also download the Electron dependency, which you use in the scripts field toboot the app via npm start. This means you can simply start the app from the com-mand line with a standard approach that's also used for the NW.js apps, as well asNode.js apps in general.

You'll take a look at the main.js file next, because that's what Electron boots first inthe app. The main.js file contains the code for the configuration of the Twitter clientand the code that uses Twitter's Streaming API to search for a query and provide tweetsmentioning that query. These tweets are then hooked up with the desktop notifications. Create a main.js file inside the watchy-electron folder and put the code shown in

the next listing inside it.

Listing 15.2 The main.js file for the Watchy Electron app

'use strict';

const {app, ipcMain, BrowserWindow} = require('electron');const notifier = require('electron-notifications');   const config = require('./config');const Twitter = require('twitter');const client = new Twitter(config);

Creates Twitter client that uses your Twitter API credentials

let mainWindow = null;

app.on('window-all-closed', () => { if (process.platform !== 'darwin') app.quit();});

Loads electron-notifications module for app

Listens for events to monitor a term, such as「breakfast」

ipcMain.on('monitorTerm', (event, term) => {       client.stream('statuses/filter', {track: term}, (stream) => {   stream.on('data', (tweet) => {         let notification = notifier.notify('New tweet', {  icon: tweet.user.profile_image_url,  message: tweet.text  }); }); stream.on('error', (error) => {  console.log(error.message); }); });});

When you receive tweet with term, creates notification with tweet's contents

Passes the term to Twitter's streaming API to get tweets mentioning that term

app.on('ready', () => { mainWindow = new BrowserWindow({ width: 370, height: 90, useContentSize: true }); mainWindow.loadURL(`file://${__dirname}/index.html`); mainWindow.on('closed', () => { mainWindow = null; });});

Creating the Watchy app in Electron

237

The main.js file is responsible for hooking up the Twitter client to the notificationsmodule so that you can monitor for tweets that contain a term and display them asnotifications. To do this, you need to create an instance of the Twitter client with yourAPI credentials, which are stored in the config.js file. The config.js file is created froma copy of the config.example.js file, as shown in the following code:

module.exports = { consumer_key: null, consumer_secret: null, access_token_key: null, access_token_secret: null};

The config.example.js file is an object with keys that have null values. The idea is tomake a copy of the file, save it as config.js, and then populate the API credentials foryour app from Twitter.

To get API credentials from Twitter, you'll need to create a Twitter app, which youcan do at https://apps.twitter.com. Then, copy the following API credentials into theconfig.js file:

 Application consumer key Application consumer secret Access token key Access token secret

Now, you can implement the front-end part of the app. The app loads an index.htmlfile for the front end, and the next listing shows what the code looks like.

Listing 15.3 The index.html file for the Watchy Electron app

<html> <head> <title>Watchy</title> <link rel="stylesheet" href="app.css"/> <script src="app.js"></script> </head> <body> <form onsubmit="search();">  <input type="text" placeholder="Monitor tweets about..." />  <button type="submit">Monitor</button> </form> </body></html>

The index.html's UI is a simple use of the HTML form element, an input field forwhere the user will type in the term of interest, and a button element they can clickto submit the term. An app.css stylesheet is loaded to apply styling to the UI, and anapp.js file handles passing the term to the back end. Let's take a look at the app.cssfile first.

238

CHAPTER 15 Making desktop notifications

Listing 15.4 The app.css file for the Watchy Electron app

body { margin: 0px; padding: 0px; font-family: 'Helvetica Neue', 'Arial'; background: #55acee;}

input, button { padding: 1em; font-size: 12pt; border-radius: 10px; border: none; outline: none;}

button { background: linear-gradient(0deg, #bbb, #fff); cursor: pointer;}

form { margin: 1em;}

The styling produces a small app, as shown in figure 15.1.

Figure 15.1 Watchy running on Electron and Windows 10

With the UI styled, the main question now is how you get the term entered in theform sent to the back end, where the Twitter client can receive it and stream relatedtweets as desktop notifications.

In the index.html file, you see that submitting the form triggers a JavaScriptfunction named search, which is located in the app.js file, the code for which isshown next.

Listing 15.5 The app.js file for the Watchy Electron app

'use strict';

const {ipcRenderer} = require('electron');

Loads Electron's ipcRenderer module so you can send data to back end

function search () { const formInput = window.document.querySelector('form input');

Creating the Watchy app in NW.js

239

const term = formInput.value;      ipcRenderer.send('monitorTerm', term);  return false;}

Gets ahold of term that was typed into form

Sends that term to back end via ipcRenderer module

The search function used by the form gets ahold of the term that was typed into theform and sends it to the back end, where the Twitter client is, via Electron's ipcRen-derer module.

Now, if you try to run the app using npm start from the command line, the appshould boot up. If you then type in a term that you want to search for and pressEnter, you should see notifications appearing in the top-right corner, as shown infigure 15.2.

Figure 15.2 Watchy displaying a tweet that mentioned「breakfast」

What you can expect to see is a stream of tweets being displayed as notifications in thetop-right corner of the desktop, depending on what term you typed into the app (youmay find a nonstop selection of tweets appearing if your term is popular).

This demonstrates how to build a term-monitoring tool with Twitter and desktopnotifications support with Electron. In the next section, we'll take a look at how toimplement the same app with NW.js.

15.3 Creating the Watchy app in NW.js

NW.js's approach to implementing desktop notifications differs from Electron's, andthe implementation has been in flux since the upgrade from 0.12 to 0.14, as well asfrom Google Chrome adding support for desktop notifications.

Between versions 0.12 and 0.14, NW.js switched from using native notificationsto using Google Chrome's desktop notifications API. This means you can use the

240

CHAPTER 15 Making desktop notifications

Notifications API as documented at https://developer.mozilla.org/en-US/docs/Web/API/Notification. To use it in NW.js, though, there's a tiny little difference I'll showyou—and it's important because quite a few people have had problems using notifica-tions in NW.js. But first I'll walk you through creating the app. If you want to cut to thechase, the source code for the app can be found in the watchy-nwjs app in the book'sGitHub repository at http://mng.bz/UD6r.

The best place to start is with the package.json file, shown next.

Listing 15.6 The package.json file for the Watchy NW.js app

{ "name": "watchy-nwjs", "version": "1.0.0", "description": "A Twitter client for monitoring topics, built with NW.js

for the book 'Cross Platform Desktop Applications'",

"main": "index.html", "scripts": { "start": "node_modules/.bin/nw .", "test": "echo \"Error: no test specified\" && exit 1" }, "keywords": [ "twitter", "nwjs" ], "window": { "toolbar": true, "width": 370, "height": 80 }, "author": "Paul Jensen <paulbjensen@gmail.com>", "license": "MIT", "dependencies": { "nw": "^0.15.3", "twitter": "^1.3.0" }}

The package.json file has a couple of npm dependencies, as well as a conveniencemethod for booting up the app via npm start on the command line. Next, installthe dependencies via npm install, and then add the index.html file, which is iden-tical to the file shown in listing 15.3 for the Electron version of the app. Theindex.html file loads the app.css file (which, again, is the same as the code shown incode listing 15.4 for the Electron app), and then add the app.js file, the code forwhich is shown here.

Creating the Watchy app in NW.js

241

Listing 15.7 The app.js file for the Watchy NW.js app

'use strict';

const Twitter = require('twitter');const config = require('./config');let term;const client = new Twitter(config);  let notify = Notification;

Makes JS variable referring to Notification global variable

Loads Twitter client with config for API credentials

function notifyOfTweet (tweet) { new notify(`New tweet about ${term}`,    {  body: tweet.text,        icon: tweet.user.profile_image_url  } );}

Refers to that variable when creating new notification

Passes tweet's text and user's profile image as body and icon for notification

function search () { const formInput = window.document.querySelector('form input'); term = formInput.value; client.stream('statuses/filter', {track: term}, (stream) => { stream.on('data', notifyOfTweet);    stream.on('error', (error) => {  alert(error.message); }); }); return false;}

After subscribing to streaming API, passes any tweets to notify Tweet function

You've almost finished writing all the code for the app. The last thing to do is create acopy of the config.example.js file, save it with the file name config.js, and add yourTwitter API credentials to it:

module.exports = { consumer_key: null, consumer_secret: null, access_token_key: null, access_token_secret: null};

Once you've copied your Twitter app's API credentials into that file, you can run theapp with npm start. When the app starts, type in a term, and you should see notifica-tions start to appear on the right-hand side of the screen, as in figure 15.3.

Because NW.js has a shared context between the front-end and back-end parts ofthe app, there isn't any need to pass data via inter-process communication. The Twit-ter client can be loaded in the same place the search function is defined, which getsthe term from the UI. In some ways, it makes the app simpler because you don't needto worry about passing data between separate processes, but at the same time, in large

242

CHAPTER 15 Making desktop notifications

Figure 15.3 Watchy NW.js on Windows 10. Note how the desktop notifications are displayed on the right-hand side and look exactly the same as Google Chrome's desktop notifications.

desktop apps, the code can become disorganized quickly if it isn't refactored andcleaned up over time.

15.4 Summary

In this chapter, you implemented a live tweet-monitoring app in both Electron andNW.js. You looked at how each framework has different approaches to implementingdesktop notifications and creating them. Some of the key takeaway points from thechapter are as follows:

 To use desktop notifications in Electron, you want to make use of the electron-

notifications module via npm.

 With NW.js 0.14, there was a switch to using Google Chrome's notifications API.

Previous versions of NW.js had been using another implementation.

 Be careful when using desktop notifications—they're a useful feature, but youdon't want to spam your user's screens with notifications (as I found out tryingto monitor tweets about NFL with the Watchy app).

In chapter 16, we'll move away from developing apps and look at how you can testthem so you can add features and change code with confidence and build apps theright way.

Part 4

Getting ready to release

Once a desktop application is feature complete, there remain the last few

steps of making sure the code is fully tested, issues are identified and fixed, andthe app is built for various operating systems. This part shows how to write testsfor your desktop apps, how to debug them and spot performance issues, andhow to generate binary executables for your applications.

In chapter 16, we'll look at ways you can go about testing desktop apps, usingtools like Mocha, Cucumber, and Devtron. We'll then continue to prepare yourapp for release by using debugging tools to help spot performance bottlenecksand root them out. In the final chapter of the book, I'll show the various ways inwhich you can prepare your app for installing on Windows, Mac, and Linux.

Testing desktop apps

This chapter covers Understanding why testing desktop apps is

essential

 Exploring different approaches to testing your app Writing unit tests with Mocha Testing Electron apps with Spectron Doing behavior-driven development with

Cucumber

When I started programming back in 2006, I had no idea how to test software, orwhy I should. Then, one day I was getting ready to deliver a product demo to a client,making some code changes 20 minutes before the demo. When I demoed the appto the client, it crashed. Perhaps if I had written some tests for the app, I wouldhave foreseen that the app would crash, and I wouldn't have suffered that embar-rassment. This is one of many reasons you don't want to write code without tests(or, for that matter, make last-minute changes before a product demo).

Thankfully, my colleague Matt Ford (who runs the digital consultancy Bit Zesty)sat down with me and introduced me to unit testing with RSpec in Ruby. From

245

246

CHAPTER 16 Testing desktop apps

there, I was able to improve the quality of my work by writing tests for my code in atest-driven-development fashion.

I wasn't alone in being oblivious to the world of testing apps, and in my career Ifound places where testing was either unknown or sadly disregarded by people who「don't have time for tests」(as one product manager once told me). I can tell you fromexperience that apps written without tests don't stand the test of time. Besides, wouldyou be comfortable flying on an airplane if the software powering it wasn't tested? Whatabout apps that store data that's important to you—what if they keep crashing, or worse,lose your data? Testing is a safety net that you want when creating an app and a sane wayto help others work on the app without causing unintentional breakages.

We'll look at different ways in which you can approach testing desktop apps. We'llstart with a basic task—unit testing parts of your code with Mocha, a testing tool forNode.js. Then, we'll work up to testing functional components and test how the appworks from a user's perspective with Cucumber. We'll also look at Spectron, a dedi-cated tool for testing Electron apps. You'll get an idea of what kind of software land-scape to expect when you're testing apps.

The goal is that you gain a good understanding of how you can go about testingdesktop apps. There's no point in building apps if they're going to be flaky and fallover on the user—users will give up on the app and try an alternative that works.

Ready to dive in? Great.

16.1 Different approaches to testing apps

There are different ways to approach testing apps—for example, test-driven develop-ment and behavior-driven development. What are they, and should you use them?The next couple of sections will answer those questions. You'll gain enough under-standing of software testing to find an approach that works for you. If you alreadyknow about these techniques, feel free to skip ahead to section 16.2.

16.1.1 Test-driven-development (TDD)

Test-driven development involves developing a feature by first writing the code to testit. The tests will fail (because no code for the feature has been written yet). Then thedeveloper writes code for the feature, which causes the tests to pass. Once the tests arepassing, the developer can refine the code (if it needs improving) and then work onimplementing the next feature. This process, called red-green refactoring, is illustratedin figure 16.1.

The idea behind the red-green cycle is to enhance developer productivity by pro-viding a structured approach to developing software. It requires thinking and disci-pline to write tests before any product code is written. Once you have tests written forthe app, then you're in a position to write the app code. Which part of the app codeyou choose to write first depends on what the tests require. This helps you make deci-sions about what to implement first, and reducing the number of decisions you haveto make helps you stay focused and productive.

Different approaches to testing apps

247

Write tests

Refactor

code

Tests fail

Tests pass

Add/modify

code

Figure 16.1 The red-green refactor cycle. First, you write the tests; then, they fail; then, you write/modify the app code; then, the tests pass and the feature is implemented; and finally, you can refactor, safe in the knowledge that the tests will fail if you break the feature.

As the code is written, the tests begin to pass, and as long as the tests sufficiently coverwhat things need to be implemented, the developer can have the confidence to refinetheir existing code and improve it via refactoring. If the tests still pass, then the solu-tion is good—but if the tests fail, the developer can determine why they're failing andmake the necessary adjustments. It's a safety net to help the developer.

TDD isn't to everyone's taste, admittedly. In 2014, David Heinemeier Hansson (thecreator of Ruby on Rails) wrote a blog post called「TDD is dead. Long live testing.」Hedescribed his experiences using TDD over the years and how he'd come to the conclu-sion that it was impacting his ability to design good software. It's worth a read athttp://mng.bz/sXUJ. The discussions that followed online with Kent Beck and MartinFowler are covered at http://mng.bz/Iy3O.

The interesting thing about the debate around TDD is that it shows that well-respected, accomplished members of the software community can hold differentopinions about software—that there isn't necessarily a single right answer aboutthese things.

So should you use TDD for building your apps? My suggestion is to give it a try andsee if it works for you. If it doesn't, don't worry—there are other options, such as theone we'll look at next. The important thing is to find what works for you and for thosearound you.

16.1.2 Behavior-driven development (BDD)

Behavior-driven development, a variation on the concept of TDD, was influenced bythe ideas behind acceptance testing (whereby you check with end users that the soft-ware does what they expect). Whereas TDD is focused on the workflow of the devel-oper, BDD takes an interest in not just the developer's workflow, but also that of otherstakeholders (such as the end user). Its goal is to aid collaboration between thesestakeholders through the use of a common language to describe the requirements of

248

CHAPTER 16 Testing desktop apps

the software. Figure 16.2 is a process chart showing how a product's feature require-ments are gathered and implemented.

User storiesworkshop.

Flesh outuser story.

Write tests

for user story.

Implement tests

and featuresfor user story.

Figure 16.2 Process of gathering feature requirements and implementing them with BDD. Used in conjunction with an agile process, BDD complements the process shown by helping flesh out user stories, writing tests for them in a common language, and implementing those tests with tools like Cucumber.

From figure 16.2, we'll look at how BDD helps flesh out user stories. In a fashion simi-lar to acceptance testing, BDD encourages the collection of user stories to help gatherrequirements for the app. These user stories, written in plain English, help describehow the feature in question should work. Take, for example, this feature:

Feature: Search  In order to locate a file quickly  As a user  I want to filter files by their name

Given I have opened the application  And I am browsing the contents of my「documents」folder  When I type「expenses」into the search bar  Then I should see a file called「expenses」 And I should not see「invoices」

This example of a user story is based on the Lorikeet app you made earlier in thebook. It describes in simple terms how the app feature works from the perspective ofthe user and helps provide some acceptance criteria for the feature. With this userstory, you're able to write code that can test the app—the documentation of how thefeature works drives how the app is tested. This confirms that the product worksaccording to the specification of the person who is actually going to use the product,something that's often known to be problematic in software development.

BDD allows developers to approach implementing the tests for their apps in a waythat ensures that the feature does what the client expected. That said, testing an appisn't just a case of「write tests and make sure they pass.」There are different levels atwhich software can be tested. In the next section, we'll go into more depth about howto approach these levels of testing.

16.1.3 Different levels of testing

For software developers writing tests for an app, there are three levels of testing thatcan occur:

 Unit testing Functional testing Integration testing

Unit testing

249

Unit testing is at the level of the individual functions in the code that are public APImethods. Functional testing is at the level where the combination of those functions ischecked (mainly as components). Integration testing is at the level where the compo-nents combine to support a user feature. Figure 16.3 shows an illustration of the dif-ferent levels.

Integration testing

Application feature

Functional testing

Component

Component

Component

Unit testing

Function

Function

Function

Function

Function

Function

Figure 16.3 How the different levels of software testing stack up. Unit testing covers software at the smallest element of functionality. Functional testing builds on this by testing the interaction between those elements, at the level of components. The pattern repeats at the integration testing level, where interaction between app components is tested.

You can see from figure 16.3 that at the bottom of the stack is unit testing, whichchecks that each function works as expected. At the next level, functional testingchecks that the functions within a component work well together. To ensure that thecomponents themselves work together as expected, integration testing at the level ofapp features is performed.

In the next section, we'll explore these different levels of testing in greater detail,

starting with unit testing.

16.2 Unit testing

Unit testing is the process of testing whether individual functions work. It's a bit likechecking that each piece that makes up a car is in good working order. When it comesto unit-testing desktop apps— Node.js testing in general—the most widely used testframework is Mocha. In the next section, you'll find out what Mocha is and how youcan use it for unit-testing your apps.

16.2.1 Writing tests with Mocha

Mocha is a testing framework for Node.js. It can run on both the server and the client(it's ideal for testing Node.js desktop apps) and offers a lot of features.

250

CHAPTER 16 Testing desktop apps

Say you wanted to unit test one of the functions provided in the Lorikeet fileexplorer app you built earlier. In the GitHub repository for the book, there's a copy ofboth the NW.js and Electron versions of the Lorikeet file explorer app: lorikeet-test-nwjs and lorikeet-test-electron.

These apps have the test code already, so you can run them and see what to expect.Follow the instructions in the README.md files to run the tests. If you want to writethe tests yourself, you can revert to a point in the source code before the tests wereadded by checking out this git commit via the following command:

cd cross-platform-desktop-applications/chapter-16git checkout -b before-tests-added

Feel free to use either app to run through the testing example with (the codebasesare practically identical), and then we'll walk through implementing some unit testswith Mocha.

Navigate to the folder path of the Lorikeet app in your command-line Terminalprogram and run the following command to install mocha as a development depen-dency in the Lorikeet folder:

npm install mocha --save-dev

Now create a folder, called test, for storing your test code. There are two reasons forcalling it test: it's pretty obvious what files are contained in that folder, and mocha looksfor tests in the test folder by default when it's executed.

Next, you'll look at a particular file in the Lorikeet app and test one of its functionsto ensure that it works as expected: the search.js file that handles filtering the files.You want to write a test that ensures that the following are true:

 A search returns results that match the term provided. That same search doesn't return results that don't match the term provided.

Create a file inside the test folder called search.test.js, and then insert the followingsnippet of code.

Listing 16.1 Writing a test using Mocha's API

'use strict';

const lunr = require('lunr');const search = require('../search');

describe('search', () => {      describe('#find', () => { it('should return results when a file matches a term');  });});

describe function comes from Mocha and defines the context of the test

it function comes from Mocha as well and defines a test case

I'll go through the DSL of Mocha now. At the top of the file, you have the usual decla-ration of libraries to load, and then the function describe, whose job is to receive astring with the name of the thing you're testing, and then a function that will execute

Unit testing

251

either another nested describe or a set of tests to run using the keyword it. The itfunction is responsible for executing a test and is first passed the description of whatit's testing. Because you haven't yet written the test implementation code, you leave itbe, as it is now—a pending test.

If you now run the node_modules/.bin/mocha command on the Terminal, you

should see the output shown in figure 16.4.

The command thatyou run to executethe tests

The test that isrunning, and theresult of running it

The results ofrunning the tests

Figure 16.4 The Mocha tests running. Notice how there is a test marked in light blue text—this color indicates that the test is pending. (If you're looking at the printed book in grayscale, the light blue text says「should return results when a file matches a term」and「1 pending.」)

You can see in figure 16.4 that there are no passing tests yet, and one pending test.The next thing to do is to start implementing that pending test.

16.2.2 From pending test to passing test

To test that finding a file based on a search term works, you need to follow the steps infigure 16.5.

b

Add some filesto the search index.

c

Perform a searchwith the find function.

d

Inspect the resultsthat you get back.

+

Assert that you don't get resultsfor the files you did not want.

Assert that you get a resultfor the file that you want.

≠

=

Figure 16.5 Process flow of the unit test. Test the search feature by getting it to index some example files, perform a search against that, check that the search results returned are to be expected, and ensure that you don't get back anything you shouldn't get back.

252

CHAPTER 16 Testing desktop apps

To implement the test code, start by requiring Node.js's assert library for performingassertions in the tests:

const assert = require('assert');

This library is used for doing the checks on the acceptance criteria being met for thetest. If one of the criteria items is met, the library function returns true, and if not, itthrows an error.

Next, look at providing some global scope for Lunr.js to bind to:

global.window = {};global.window.lunr = lunr;

Because Lunr.js is a client-side library, it needs to attach to the window object, so youstub out (create a stand-in version of) the window object in Mocha to make sure thatthe library can be accessed and inspected. After that, add a function to the pendingtest to hold the test code, as shown next.

Listing 16.2 Setting up a Mocha test to be executed rather than be pending

it('should return results when a file matches a term', (done) => {         });

Where you'll insert your test code

Here, you extend the initial pending test to include a callback function named done.The done callback function is called once all the asynchronous code inside the test hasfinished. Inside the function, you add a few code comments to track the flow of thetest code, fleshed out in the following listing.

Listing 16.3 Fleshing out the Mocha test with test code

it('should return results when a file matches a term', (done) => {

Example data (seed file references), for search feature to index

const seedFileReferences = [      {  file: 'john.png',  type: 'image/png',   path: '/Users/pauljensen/Pictures/john.png'  },  {  file: 'bob.png',  type: 'image/png',  path: '/Users/pauljensen/Pictures/bob.png'  },  {  file: 'frank.png',  type: 'image/png',  path: '/Users/pauljensen/Pictures/frank.png'  } ];

Unit testing

253

Performs asearch forterm ‘frank'and checksresults

search.resetIndex();         seedFileReferences.forEach(search.addToIndex);

search.find('frank', (results) => {    assert(results.length === 1);  assert.equal(seedFileReferences[2].path, results[0].ref);  done(); }); });

Resets search index to make sure it's clean before adding seed file references to search index

The final file for the search.test.js file should now look like the next listing.

Listing 16.4 The search.test.js file for the Lorikeet app

'use strict';

const assert = require('assert');const lunr = require('lunr');const search = require('../search');

global.window = {};global.window.lunr = lunr;

describe('search', () => { describe('#find', () => {

it('should return results when a file matches a term', (done) => {

const seedFileReferences = [  {   file: 'john.png',   type: 'image/png',   path: '/Users/pauljensen/Pictures/john.png'  },  {   file: 'bob.png',   type: 'image/png',   path: '/Users/pauljensen/Pictures/bob.png'  },  {   file: 'frank.png',   type: 'image/png',   path: '/Users/pauljensen/Pictures/frank.png'  }  ];

search.resetIndex();  seedFileReferences.forEach(search.addToIndex);

search.find('frank', (results) => {  assert(results.length === 1);  assert.equal(seedFileReferences[2].path, results[0].ref);  done();  });

});

});});

254

CHAPTER 16 Testing desktop apps

Here, you create some seed file references (which represent the kind of data that youwant to pass to the module). You then pass these file references into the search mod-ule's addToIndex function, to populate the search index with them. Next, you call thefind function (the bit that you want to test) with the term 'frank' and check that youget back exactly one result, and that the result reference matches exactly with the filethat has the name frank.png, by comparing the file paths. If that passes, you call thetest's done function to let it know that you're finished.

If you now try to run this test, you can expect to see the result shown in figure 16.6.

The command thatyou run to executethe tests

The test that isrunning, and theresult of running it(now passing)

The result ofrunning the tests,and the time ittook to run them

Figure 16.6 The unit test is now passing. The previously blue section is now green and has a tick against it. This means it's passing, and you can move on to testing other functions or refactoring the function to make its implementation better.

This is a simple example of implementing a unit test for the desktop app. What I hopeyou've been able to take away from this practical example is how you can go aboutunit testing a piece of functionality at the level of just a single JavaScript functionusing Mocha, because this will help you test your code at the simplest level. When itcomes to writing tests, I suggest first making notes about what you want to test as codecomments inside the test. Then, flesh them out once you know how to go aboutimplementing that unit test.

Are there alternatives to Mocha?Mocha is one of the more common testing libraries used in Node.js, but it's not theonly one out there. A couple of other options are worth investigating. Jasmine, a long-standing JavaScript testing framework from Pivotal Labs that worksin JavaScript environments, has a DSL almost identical to Mocha's. You can readmore about Jasmine at https://github.com/jasmine/jasmine.Another option is Ava from Sindre Sorhus. Ava is a test runner for Node.js that exe-cutes tests faster by making them run in parallel as separate processes. The ideais that the state for each test is specific to that test only—meaning the test can berun in a separate process alongside other tests, and so the tests run faster. Seehttps://github.com/avajs/ava for more.

Functional testing

255

Next, we'll go up the testing stack and look at functional testing.

16.3 Functional testing

Functional testing is similar in style to unit testing, but the key difference is that youtest how functions work together in a component. You could argue that the exampleyou did for unit testing is technically a functional test, because, although you testedjust one function, that function depends on a number of other functions (the reset-Index function, the addToIndex function, and behind all that, the Lunr.js library)working properly. That said, functional testing is about checking that a group of func-tions work together as expected, whereas a unit test cares only about how a singlefunction works. Functional testing is like checking that the disc brakes on a car areinstalled correctly and work when the brake pedal is applied.

You need to track where changes to functions in one module impact functions inother modules. To illustrate, say you have a desktop publishing tool. New featuresarrive, other members of the team implement those features, and there's a chancethat existing code needs to change to accommodate those features. For example, theintroduction of an extensions feature into the app allows third-party developers to cre-ate extensions that put buttons in the toolbar. Then, someone else comes along andrefactors the toolbar implementation, changing the access API. This breaks the third-party extensions because the API for adding buttons to the toolbar has changed.These are the kinds of breaking changes that functional testing is designed to reveal.

16.3.1 Functional testing in practice

The challenge of functional testing is being able to track which components interactwith each other across modules/contexts and knowing how to go about testing them.In the example for the unit test for the search function, you stubbed out the windowobject, which would be available by default in the browser. In functional testing, you'lluse as many the real-world components as possible. In the Lorikeet file explorer app,most of the modules have been architected so as to be unaware of each other. Theapp.js file is the point at which the interactions between modules occur, so this is thepart you're interested in testing.

You'll continue on the theme of search and test that the search field in the toolbarfilters the files that are displayed in the main area. This tests the following elements ofthe app:

 The userInterface.js file's bindSearchField, resetFilter, and filterResults

functions

 The search.js file's find function

You'll need to test this in an environment where the app is running (rather thanattempt to stub out environment parts like the DOM). You need a way to test this inthe app and a way to automatically fill in the search field and inspect the results visiblein the main area.

256

CHAPTER 16 Testing desktop apps

16.3.2 Testing with ChromeDriver and NW.js

Testing NW.js apps via ChromeDriver is a complicated and developer-unfriendlyexperience. It requires a lot of tinkering. In older versions of NW.js (0.12), there wasa functioning example of testing NW.js apps with ChromeDriver, but since then,updates to various libraries have led to a state where existing test suites have broken,and fixing them is prohibitively time-consuming. You don't want to fight with sup-porting tools and libraries when you're trying to develop and test apps. In light ofthis, I won't talk about how to do functional testing with NW.js, and instead will optto solely cover Electron.

Hopefully, in the future, testing NW.js apps will become easier.

16.4 Testing Electron apps with Spectron

Some developers find that trying to get ChromeDriver and WebDriver set up to playball is a painful process, especially in terms of finding documentation and a workingexample. In the Electron community, dedicated tooling has evolved that combinesChromeDriver and WebDriver in a Node.js module, providing a relatively easy way totest desktop apps. This tool is Spectron, and its documentation can be found athttp://electron.atom.io/spectron/.

Spectron is available as an npm module and can be installed with the following

command in the lorikeet-electron app:

npm install spectron --save-dev

Now, you can create a file for testing one of the Lorikeet app's functions: double-clicking folders to see their contents. You'll put this file in the test folder and name itfolderExplorer.test.js.

To use Spectron, you need to require it in the test code and do some setup to get

the app booting up. In the folderExplorer.test.js file, add the code shown next.

Listing 16.5 Getting the folderExplorer.test.js file started

'use strict';

const Application = require('spectron').Application; const assert = require('assert');const osenv = require('osenv');const path = require('path');

Loads Spectron as module dependency in test file

Creates referenceto path whereElectron binary is

let app;let electronPath = path.join(__dirname, '../node_modules/.bin/electron');let entryPointPath = path.join(__dirname, '../main.js'); if (process.platform === 'win32') electronPath += '.cmd';

Creates reference to entry point (main.js) for app

If on Windows, appends.cmd file extension forElectron binary path

Testing Electron apps with Spectron

257

In the preceding listing you load dependencies for the file, which includes Node.js'sassert module as well as the path module. The Spectron library is loaded as a module,and you use the Application module to help with booting up the app with Chrome-Driver and WebdriverIO behind the scenes. The following listing shows the code thathandles booting up the Electron app.

Listing 16.6 Booting the Electron app with Spectron

describe('exploring folders', () => {

beforeEach(() => { return app = new Application({   path: electronPath,         args: [entryPointPath]  }); });});

Absolute file path to the app's entry point is passed to Application class

Initializes instance of Spectron's Application class

Path to Electron binary is passed

This is essentially a wrapper around loading the app via ChromeDriver, with the Elec-tron binary path and app entry point passed to it. This is the bare minimum requiredto set up the functional test loading the app, but more options are available for config-uring (see https://github.com/electron/spectron#application-api).

Now, you need the app to run the code that checks if you can double-click afolder and navigate to that folder path. The app instance returned from Spectron'sApplication class is a wrapper around WebDriver's client API (see http://webdriver.io/api.html for more). It's worth a brief glance at the documentation to get a feelfor what the code in the test will do. The API methods let you carry out a number ofuser actions.

You want to boot up the app, double-click a folder named Documents, and checkthat you've navigated to that Documents folder. If all those conditions are satisfied,the test passes. You'll write the test using Mocha's syntax style and combine it withSpectron's approach, which involves using Promises. The next listing shows the codefor the test.

Listing 16.7 Testing that folders can be navigated with a double click

it('should allow the user to navigate folders by double-clicking on them',

Documentspath used tofind imagefolder todouble-clickand verifythe test

Triggersstarting app

function (done) {

function finish (error) {    app.stop();  return done(error); }

Creates convenience function to stop error and execute Mocha's callback

let documentsFilePath = path.join(osenv.home(),'/Documents');

Sets 10-second timeout (for slower machine boots)

this.timeout(10000);          app.start().then(() => {       return app.browserWindow.isVisible();

Checks that app loads app window and you can see it

258

CHAPTER 16 Testing desktop apps

}).then((isVisible) => {  assert.equal(isVisible, true); }).then(() => {          return app.client.doubleClick(`//img[@data-

filepath="${documentsFilePath}"]`);

Finds img element with Documents folder path and double-clicks it

}).then(() => {  return app.client.getText('#current-folder');  }).then((currentFolder) => {  assert.equal(documentsFilePath, currentFolder);   }) .then(finish)     .catch(finish);  });

If condition satisfied, test passes, and finish function called

If not, throws error, intercepted by finish function

Gets text for current folder element in toolbar

Checks text is same as double-clicked folder path

If you now use npm test to run the test, you'll find that the app opens, double-clickson a folder, checks that the folder is being viewed in the app, and then closes downagain after the test has finished. This shows you how relatively easy it is in Electron toimplement a functional test that actually opens the app and uses it the same way a realuser would, allowing you to create tests that check real-world conditions.

Now, let's look at the top level—integration testing.

16.5 Integration testing

Also called end-to-end testing (E2E), integration testing is a level of testing where theentire user journey is turned into a set of tests that examine how the entire solutionruns, with nothing stubbed and nothing isolated. Everything runs and everything istested. It's the most comprehensive form of testing that can be done on an app. Insome cases, integration testing is the only form of testing done on an app (functionaland unit tests are ignored because more of the app's code can be covered by an inte-gration test).

What's an example of an integration test? Well, for example, a Lorikeet user mightwant to find an image file and open it using their preferred image-editing app. They'llneed to open the app, possibly type in the name of the image, and then double-clickit. This tests a number of features across the app and, like functional testing, needs torun as close to the real scenario as possible.

As mentioned and demonstrated earlier, it's possible to use a combination ofMocha, Selenium, and WebDriver to help automate this testing, but one problem withthis approach is that developers are the only ones who'll understand this method. Amiddle ground is needed to help product owners, users, and developers come to acommon understanding of what the app does and how it can be acceptance tested.Enter Cucumber.

16.5.1 Introducing Cucumber

Cucumber is referred to as「the world's most misunderstood testing tool」by its cre-ator, Aslak Hellesøy. Cucumber is a tool for helping developers describe how a piece

Integration testing

259

of software should work, using plain English. The goal is to provide a common under-standing among developers, product owners, and users (among other stakeholders)about how that software should function. This provides a source of software documen-tation clearly defining customer expectations and developer specifications.

What does Cucumber look like to a developer? Well, the starting point usuallystems from feature requirements defined by the project-management process, fromthe perspective of the user/consumer. Returning to the earlier example, say you wantto test the feature of opening image files in a folder. You could capture those require-ments in the following user story:

In order to see photos that I'm currently interested inAs a UserI want to open images from the application

This user story captures the context around the feature: who it's for, what it's aimingto achieve, and finally, what feature is needed to achieve this. From that, you can cre-ate a feature file that will describe what the feature does.

In the folder containing the Lorikeet electron app, create a folder called features.This folder will contain Cucumber feature files that will be used to document how thesoftware tests, drive automated tests, and provide a shared, common understanding ofhow the app should work.

Now, to create your first Cucumber feature file, create a file named images.feature

and insert the following text into that file:

Feature: Images  In order to see photos that I'm currently interested in  As a User  I want to open images from the application

Scenario: Open a PNG image   Given I have the application open and running   When I search for "Pictures"   And I click on the "Pictures" folder   And I double click on "Pictures/app with set icons.png"   Then I should see the "Pictures/app with set icons.png" file   ➥ opened in a photo app

Here, you can read the text and see what looks like plain English instructions on howto use an app feature—hopefully, they make sense straight off the bat. The idea is thatregardless of whether you're a developer, product owner, user, or other stakeholder inthe project, you'll be able to read this and have the same understanding of the featureas everyone else.

With this feature in place, you can now look at using this plain English document

to test the app feature.

260

CHAPTER 16 Testing desktop apps

16.5.2 Automatically testing your Electron app with Cucumber

and SpectronThis section shows you how to use Cucumber.js to run integration tests for your appvia Spectron. The code for the Cucumber example is available in the GitHub reposi-tory for the book, but I'll also walk you through the code here to help you understandhow it works.

First off, install cucumber.js; run the command to install the module via npm:

npm install cucumber --save-dev

Once you have Cucumber.js installed in the development dependencies for the Lori-keet Electron app, you can set up the required files for the app. You already have theimages.feature file inside the features folder, so next you want to set up a hooks.js fileinside the features/support folder. This hooks.js file in the following listing containsthe code that's responsible for the setup and teardown of the Spectron library boot-ing the app.

Listing 16.8 The hooks.js file for the Lorikeet Electron app

'use strict';

const Application = require('spectron').Application;const path = require('path');let electronPath = path.join(__dirname, '../../node_modules/.bin/electron');const entryPointPath = path.join(__dirname, '../../main.js');if (process.platform === 'win32') electronPath += '.cmd';const {defineSupportCode} = require('cucumber');

defineSupportCode(function ({Before, After}) {

Before(function (scenario, callback) {   this.app = new Application({  path: electronPath,  args: [entryPointPath] }); callback(); });

After(function (scenario, callback) {  this.app.stop(); callback(); });});

Before hook is called before Cucumber feature files run and boots app via Spectron

After hook is called when Cucumber feature file is finished and closes app

The hooks.js file contains code that's used to drive booting the app with Spectron, aswell as to shut the app down once it has finished running the Cucumber featurefiles. Binding the Spectron app instance on the context for the Cucumber scenariomeans that you can reference the app variable not only in the After hook when itcomes to shutting the app down, but also when you want to flesh out the step defini-tions and use the app instance to do things like click UI elements in the app. This

Integration testing

261

leads to the next file that you want to add in the features/step_definitions folder: theimage_steps.js file.

The image_steps.js file, shown in the next listing, is used to store the step defini-

tions that you want to match in the Cucumber feature file.

Listing 16.9 The image_steps.js file for the Lorikeet Electron app

'use strict';

const assert = require('assert');const fs = require('fs');const osenv = require('osenv');const path = require('path');const {defineSupportCode} = require('cucumber');

defineSupportCode(  function({Then, When, Given}) {

Given(/^I have the app open and running$/, {timeout: 20 * 1000},

function (callback) {

const self = this;

self.app.start().then(() => {   return self.app.browserWindow.isVisible();   }).then((isVisible) => {   assert.equal(isVisible, true);   callback();   })

});

When(/^I search for "([^"]*)"$/, function (term, callback) {   this.app.client.setValue('#search', term)   .then(() => { callback(); });  });

When(/^I double click on the "([^"]*)" folder$/, function (folderName,

callback) {

const folderPath = path.join(osenv.home(),folderName);   this.app.client.doubleClick(`//img[@data-filepath="${folderPath}"]`)   .then(() => { callback(); });  });

When(/^I double click on "([^"]*)"$/, function (fileName, callback) {   const filePath = path.join(osenv.home(),fileName);   this.app.client.doubleClick(`//img[@data-filepath="${filePath}"]`)   .then(() => { callback(); });  });

Then(/^I should see the "([^"]*)" file opened in a photo app$/,

function (fileName, callback) {

const filePath = path.join(osenv.home(),fileName);   setTimeout(function () {   fs.stat(filePath, function (err, stat) {    const timeDifference = Date.now() - stat.atime.getTime();    assert.equal(null, err);    assert(timeDifference < 3000);

262

CHAPTER 16 Testing desktop apps

callback(err);   });   }, 3000);  });

When(/^I wait (\d+) seconds$/, (numberOfSeconds, callback) => {   setTimeout(callback, numberOfSeconds * 1000);  });

});

You'll notice that the API for triggering UI interactions is simple. With this code inplace, you're able to run the tests via running this command in the Terminal:

NODE_ENV=test node_modules/.bin/cucumber-js

If you're using Windows to run the tests, you'll want to run the cucumber-js.cmd com-mand that's present in the same .bin folder. To allow for running tests in either aUnix/Linux or Windows environment, you can write a simple script that will handleboth. Create a file called cuke.js, and put the following code in it:

'use strict';

const exec = require('child_process').exec;const path = require('path');

let command = 'node_modules/.bin/cucumber-js';if (process.platform === 'win32') command += '.cmd';

exec(path.join(process.cwd(), command), (err, stdout, stderr) => { console.log(stdout); console.log(stderr);});

That code snippet uses Node.js's child_process module to allow you to execute a com-mand in a separate process. The command that you want to run is called cucumber-js,and it's in the node_modules/.bin folder. On the line following the definition of thecommand, check whether the script is running on a Windows computer. If it is, addthe .cmd to the command, which then points to running the Windows binary forCucumber.js. Execute this command and log its contents out to the Terminal. If youwant to run this command, you now run the following in the Terminal:

NODE_ENV=test node cuke.js

If all goes well, you should see the tests passing on your terminal, and that meansit worked.

Given all the available tools for testing your desktop apps, it's fair to ask,「So, whattools should I use for my app」? This is a tricky one because there's no single rightanswer—you have to discover what works best for you and your team. My advice is tryunit testing first, because it's the easiest form of testing to implement. Once you

Summary

263

become comfortable with it, you can proceed up the levels of the testing stack, and dofunctional testing to check that components work together as you expect. Eventually,you can progress to integration testing.

Alternatively, if your biggest concern is checking that everything works at the levelof the UX, I recommend starting with integration testing first. It will take a bit more toget to grips with, but the end result is worth it, and usually you can then filter downto performing unit testing only if it's needed. Testing is about making sure softwareworks—never forget that.

16.6 Summary

There's a lot in this chapter, but the key things to take away from it are as follows:

 Writing tests for your apps from the start is the best way to avoid spending your

time fixing bugs and to prevent an unfavorable UX.

 Unit testing individual functions is the quickest and easiest way to learn how

to test.

 The best way to provide the greatest level of test coverage for your app is to start

with integration testing.

 If you want to involve stakeholders in helping to document and test your app,

use tools like Cucumber.

 Mocha is a great tool for writing your unit and functional tests due to its simple

API and semantic syntax.

In chapter 17, we'll explore ways to sort out weird issues and avoid performance prob-lems through the power of debugging tools available toó NW.js and Electron.

Improvingapp performancewith debugging

This chapter covers Debugging errors on the client with Chrome

Developer Tools

 Debugging errors on the server in Node.js Profiling UI performance and memory usage Using flame graphs to spot performance

bottlenecks


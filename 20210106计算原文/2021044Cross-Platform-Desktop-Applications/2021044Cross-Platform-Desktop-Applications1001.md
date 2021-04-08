user's OS

The UI of an app is one of the most important things to get right, as it's the firstthing people see when using your app. People can and will judge whether to use anapp based purely on how the UI looks. But it's not only about the UI; you also haveto think about the user experience.

When drag-and-drop was introduced to computer users way back in the twenti-eth century, it helped to make computers friendlier. It's become a key behavior thatspans across most computing devices today, including small-form devices likephones and tablets. It's therefore appropriate to show you how to implement drag-and-drop functionality in your desktop apps.

We'll also look at how to style the UI to mimic the look and feel of the user's OS.

10.1 Dragging and dropping files onto the app

Most users of computers are familiar with organizing their files by dragging anddropping them between file explorer windows and the desktop. In recent years, theintroduction of the file API in web browsers has meant that this functionality has

176

Dragging and dropping files onto the app

177

found its way into web apps as well, typically with forms requiring files to be uploadedto the web app. This is useful in cases like converting a file into another format, suchas the app Gifrocket (which uses NW.js). Gifrocket generates an animated GIF from avideo, and the interface for kicking off the process is to drag-and-drop the video fileonto the screen of the app, as shown in figure 10.1.

Figure 10.1 Gifrocket in action: convert a video to an animated GIF by dragging a video file to the app and dropping it in the middle of the app screen.

10.1.1 Dragging and dropping files to an app with NW.js

Say you have a feature in an app that requires processing a file (or set of files), andyou'd like to make use of NW.js's drag-and-drop file support. How do you do that?

A good example is an icon generator. You want to take a large-scale image and con-vert it into lots of different sizes to generate an app icon that works on Mac OS. Bril-liant—after all, it's a common need for building cross-platform desktop apps. Youhave the app at a stage where it will take an image and display that image at variousicon sizes. Now you want to enable the UI to receive an image file via dragging the fileto the app and dropping it onto the app screen. This exercise explores how you canadd drag-and-drop functionality to an existing app.

To save time, I've built a rough prototype app called Iconic, which you can getfrom the book's GitHub repository at http://mng.bz/jKmw. Grab a copy of the code,and I'll show you how to add the drag-and-drop functionality.

Notice what the app looks like when it starts (see figure 10.2).

Figure 10.2 Iconic: the initial screen suggests dropping an image file onto the screen area, which you will implement support for.

178

CHAPTER 10 Dragging and dropping files and crafting the UI

The app is code complete, so we'll walk through the code and see the interesting bitsthat relate to adding drag-and-drop support to an app.

In the app.js file, there's an important snippet of code you use to capture any

attempts to drag-and-drop a file onto the screen area:

function stopDefaultEvent (event) { event.preventDefault(); return false;}

window.ondragover = stopDefaultEvent;window.ondrop = stopDefaultEvent;

The default behavior of a web browser when a file is dragged and dropped onto apage area is to load that file in the browser. That's not what you want to happenhere, though. Instead you want to prevent that from happening by calling thepreventDefault function on the event. You then bind this on the ondragover andondrop events.

Next, you need to get the path of the file that's dropped onto the screen area andpass that to another function, displayImageInIconSet, which will load it into variousimg elements on the page. Getting that file path involves the following:

1 Intercept the drop event on the initial app screen.2 Hide the initial screen.3 Show the screen that displays the icons at different sizes.

Create a function called interceptDroppedFile that has the following code:

function interceptDroppedFile () { const interceptArea = window.document.querySelector('#load-icon-holder'); interceptArea.ondrop = function (event) { event.preventDefault(); if (event.dataTransfer.files.length !== 1) {  window.alert('you have dragged too many files into the app. Drag just 1

file'); } else {  interceptArea.style.display = 'none';  displayIconsSet();  const file = event.dataTransfer.files[0];  displayImageInIconSet(file.path); } return false; };}

A couple of things are happening in this function. For a start, you need to get ahold ofthe div that shows the content of the initial app screen and attach a function to theondrop event that will execute whenever a file is dropped onto it. You do a sanitycheck to make sure the user hasn't dragged more than one file onto the area (becausea user can drag multiple files). If they haven't, you hide the intercept area, display the

Dragging and dropping files onto the app

179

screen that shows the icons, and pass the path of the dragged file to the display-ImageInIconSet function so that it then is rendered in the screen. You also need toadd in a function for displaying that screen above the function you inserted:

function displayIconsSet () { const iconsArea = window.document.querySelector('#icons'); iconsArea.style.display = 'block';}

And you want to ensure that the initial screen stretches the entire width and height ofthe app, with the following code in the app.css file:

#load-icon-holder { padding-top: 10px; text-align: center; top: 0px; left: 0px; bottom: 0px; right: 0px; width: 100%;}

If all goes according to plan with all the changes saved, when you drag an image file(such as the example.png file in the images folder) into the app's initial screen, youshould see something like figure 10.3.

Figure 10.3 The Iconic app rendering an app icon at different size dimensions

This demonstrates how easy it is to add drag-and-drop functionality into an existingapp—and what kind of potential app UIs you can build with it.

Is Electron any different in its approach? Let's find out.

180

CHAPTER 10 Dragging and dropping files and crafting the UI

10.1.2 Implementing drag-and-drop with Electron

If you take a look at the iconic-electron app in the book's GitHub repository, you'll seethat the only differences in the code are in the way the app starts up. The app.js fileand index.html files are identical to the ones in the iconic-nwjs variant of the app.This is fantastic, because both apps are using the HTML5 file API for web browsers toprovide this functionality, and it demonstrates how easy it is to reuse web APIs whenbuilding desktop apps. Figure 10.4 shows what the app looks like running on Windows10 with Electron.

Figure 10.4 The Iconic Electron app running on Windows 10: different Node.js desktop application framework, different OS, but the same app functionality.

This also highlights one of the great aspects of developing desktop apps with NW.js orElectron: the fact that you can reuse code written for websites and apps to build desk-top apps, saving time when you add drag-and-drop to your desktop apps.

Now that we've covered how drag-and-drop functionality can be added to desktopapps, we'll turn our focus to how you can replicate the look and feel of the user's OSin your desktop apps.

10.2 Mimicking the native look of the OS

A common concern of people creating desktop apps with Electron and NW.js is howto make their apps look exactly like a native app with the UI controls and elementsmatching what the OS uses.

This can be achieved by detecting the user's OS and version and using CSS

stylesheets to tailor the style of your app.

Mimicking the native look of the OS

181

10.2.1 Detecting the user's OS

If you're looking to match the UI style of an OS, you need to be able to detect whichversion of which OS is running, which you can do using Node.js's OS API. The snippetof code in the next listing will find out what platform is being run, and print out a logmessage saying what OS it detected.

Listing 10.1 JavaScript for detecting the user's OS

'use strict';

const os   = require('os');const platform  = os.platform();

switch (platform) { case 'darwin': console.log('Running Mac OS'); break; case 'linux': console.log('Running Linux'); break; case 'win32': console.log('Running Windows'); break; default: console.log('Could not detect OS for platform',platform);}

If you copy this code and paste it into a Node.js REPL, you should see a message say-ing what OS your computer is running (in the case of my laptop, it's Mac OS).

10.2.2 Using OS detection in NW.js

If you're using NW.js, you can include the code in listing 10.1 in the JavaScript filesloaded by the index.html file. You can use that code to load different stylesheets tai-lored for each OS. Say you have an app that has three different stylesheets (one forWindows, one for Mac, and one for Linux), and you want to be able to load thestylesheet that matches the OS of the user. You can do this with the code shown next.

Listing 10.2 Applying different styles for each OS

'use strict';

const os   = require('os');const platform  = os.platform();

function addStylesheet (stylesheet) { const head = document.getElementsByTagName('head')[0]; const link = document.createElement('link'); link.setAttribute('rel','stylesheet'); link.setAttribute('href',stylesheet+'.css'); head.appendChild(link);}

182

CHAPTER 10 Dragging and dropping files and crafting the UI

switch (platform) { case 'darwin': addStylesheet('mac'); break; case 'linux': addStylesheet('linux'); break; case win32: addStylesheet('windows'); break; default: console.log('Could not detect OS for platform',platform);}

That code is a slight modification of the code in listing 10.1. Here, you create a func-tion called addStylesheet that inserts a link tag to the head element's inner HTML,and the link tag loads the stylesheet, given the name of the OS that's detected.

This example can take care of most cases, but if you need to go deeper and detectdifferent versions of a specific OS (such as detecting which version of Windows a useris running), you can repeat the pattern but instead call os.release(). Note, though,you need to make sure to check the call on each version of the OS that you're lookingto detect, because the release number is a number for technical reference, anddoesn't always match the number that's printed in marketing materials (for example,calling os.release on Mac OS Mavericks will return a value of 14.3.0, which is differ-ent from the OS's reported version of 10.10.3).

10.2.3 Using OS detection in Electron

Although there are separate Node.js contexts for the main process and the rendererprocess, the funny thing is that you can still call out to Node.js modules in the app.jsfile, so you can use the OS API to detect the user's OS. The code for this example is inthe Detect OS Electron app in the book's GitHub repository. The code for the app.jsfile is shown next.

Listing 10.3 The Detect OS Electron app's app.js file

'use strict';

function addStylesheet (stylesheet) { const head = document.getElementsByTagName('head')[0]; const link = document.createElement('link'); link.setAttribute('rel','stylesheet'); link.setAttribute('href',stylesheet+'.css'); head.appendChild(link);}

function labelOS (osName) { document.getElementById('os-label').innerText = osName;}

Mimicking the native look of the OS

183

function initialize () { const os   = require('os'); const platform  = os.platform();

switch (platform) { case 'darwin':  addStylesheet('mac');  labelOS('Mac OS');  break; case 'linux':  addStylesheet('linux');  labelOS('Linux');  break; case 'win32':  addStylesheet('windows');  labelOS('Microsoft Windows');  break; default:  console.log('Could not detect OS for platform',platform); }}

window.onload = initialize;

The app.js file is almost identical to the one featured in the NW.js variant. You aretherefore able to detect the user's OS from the renderer process in Electron.

Now, let's look at the options available for replicating the look and feel of the

user's OS in terms of CSS libraries.

10.2.4 Using CSS to match a user's OS style

Giving desktop apps a look and feel that matches the user's OS means making a webbrowser page look exactly like a native desktop app. The best way to pull that off is touse CSS stylesheets to tailor the look and feel of the app to the user's OS.

As suggested in the previous section, there's a way to detect the user's OS and ver-

sion and load a stylesheet that's OS-specific. What stylesheets and tips are available?

METRO UIWith Windows 8 and the Surface tablet, Microsoft introduced a bold change to its UIwith a new tile-based design called Metro. The change didn't merely redesign how theUI elements look, but also how app layouts are structured.

Sergey Pimenov, a programmer in Kiev, Ukraine, created a CSS framework calledMetro UI CSS (https://metroui.org.ua) that allows developers to create HTML-basedapps styled according to the guidelines of Metro (figure 10.5). Since the project wascreated, it has been used by JetBrains in its IDE PhpStorm.

184

CHAPTER 10 Dragging and dropping files and crafting the UI

Figure 10.5 Metro UI CSS, a CSS framework for building web apps using Microsoft's Metro UI

MAC OS LION CSS UI KITVille V. Vanninen, a minimalist visual designer, created a UI kit called Lion CSS UI Kit(http://sakamies.github.io/Lion-CSS-UI-Kit/) for mocking up native Mac OS apps inthe browser. The purpose of the UI kit is to create authentic-looking mockups of Macapps in the browser, as opposed to using a UI kit in graphics tools like Photoshop,Illustrator, and Sketch.

Although the UI kit passes as a Mac OS app, the entire UI is made from HTMLand CSS—perfect for using with a desktop app that uses HTML, CSS, and JavaScript.That said, recent versions of Mac OS are altering the look and feel of the OS, so bearthis in mind if you do consider using this CSS framework (figure 10.6).LINUXUnfortunately, I wasn't able to find a Linux UI CSS kit. Also, Linux has so many distri-butions (not to mention different graphical desktop environments with their ownUIs) that to apply native UI styling with a UI kit would require a lot of effort. I recom-mend you avoid custom-styling the UI form elements because Chromium uses GTK asthe UI toolkit, so any themes picked by the computer user will be applied to thebrowser's native UI elements as well.

These are CSS frameworks, but if you're looking for CSS libraries that also inte-grate with other JavaScript libraries and frameworks, then more options appear onthe table.

Mimicking the native look of the OS

185

Figure 10.6 Example app UI generated with Lion UI CSS Kit

PHOTONPhoton (http://photonkit.com) is a UI framework for Electron that allows you to buildapps with UIs that look identical to native Mac OS apps. The UI framework providesan extensive list of components that can be combined to create comprehensive UIs, asshown in figure 10.7.

Figure 10.7 Photon rendering what looks like Mac OS's Finder window

186

CHAPTER 10 Dragging and dropping files and crafting the UI

If you're using React for your front end and would like to use Photon with React,there's a useful wrapper library available at https://github.com/react-photonkit/react-photonkit.REACT DESKTOPReact Desktop (http://reactdesktop.js.org) is another React-based UI library thatallows you to create apps that look like either Mac OS or Windows 10, and it doesn'trequire you to create two sets of front-end code for the UI. Figure 10.8 shows an exam-ple of React Desktop in action.

Figure 10.8 React Desktop rendering a Windows 10 demo example

10.3 Summary

In this chapter, we've explored ways to use the various GUI APIs of Electron and NW.jsfor handling drag-and-drop. You also learned how to make desktop apps look like theyhave the exact same UI as the UI controls in the user's OS. Some of the main take-aways from this chapter include the following:

 Implementing drag-and-drop in Node.js desktop apps is identical to workingwith the HTML5 implementation in web apps, making it easy to repurpose web-based code that is designed for the same purpose.

 Users can drag multiple files into the app, so bear this in mind if you want your

app to handle only one file at a time.

 Apart from the app menu and tray apps, Electron and NW.js don't providenative UI elements; you have to use OS detection and a CSS UI kit to make anapp achieve a native look.

 When you detect a user's OS, remember that the release number of an app

won't always match the number given to its market name.

In chapter 11, we'll look at how you can build apps that interact more closely with theOS. We'll start by looking at how to display video and images from the user's webcaminto a desktop app for a photo booth app.

Using a webcam inyour application


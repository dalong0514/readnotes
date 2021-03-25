Auto Updating Your Application

Now that we have successfully built an app that we can distribute, we need to begin to think long term. How do we inform the user that a new feature has been added to your awesome app (or worse, you had to fix a bug)? Electron includes an auto-update module that we can leverage to assist in the tasks needing to check for an update, and properly install them. This process can be broken down into three primary tasks: the base code we need to include in our Electron application, the modifications needed for the build process, and the proper distribution of the app.

Electron has an auto-updater module that is part of the core framework. This module is just an interface

to Squirrel (https://github.com/Squirrel). It is this framework that handles the tasks of checking for a new version, downloading, it and performing the actual upgrade. However, both macOS and Windows interact with this module in different ways. Unfortunately, Linux-based Electron apps cannot use this module to auto update themselves.

Before we begin adding this functionality to your Electron app, we strongly recommend that you work

through the process with a sample app first, rather than add this to an existing Electron application. This will let you quickly test out the workflow and configurations without the overhead that your full Electron application might have. We will continue to extend the sample app from the previous chapter, as we will need to be using packaged Electron applications in order to test the auto-updating feature.

Auto Updating macOS

The auto updating functionality on macOS is built atop Squirrel.Mac. As such, there is a minimal amount of work we need to do to support this on the client side. First, we need to include the Auto Update module in our main.js file:

const autoUpdater =electron.autoUpdater

This module broadcasts four events:

•	•	•	•

checking-for-update

update-available

update-not-available

error

Using these events, we can manage the life cycle of auto updating. Let's add these to our app:

autoUpdater.addListener("update-available", function(event) { console.log('Update Available')})

© Chris Griffith, Leif Wells 2017 C. Griffith, L. Wells, Electron: From Beginner to Pro, https://doi.org/10.1007/978-1-4842-2826-5_16

245

Chapter 16 ■ auto updating Your appliCation

autoUpdater.addListener("update-downloaded", function(event, releaseNotes, releaseName, releaseDate, updateURL) { console.log("Update Downloaded") console.log('releaseNotes', releaseNotes) console.log('releaseNotes', releaseName) console.log('releaseNotes', releaseDate) console.log('releaseNotes', updateURL)

})

autoUpdater.addListener("error", function(error) { console.log(Error, error)})

autoUpdater.addListener("checking-for-update", function(event) { console.log('releaseNotes', 'Checking for Update')})

autoUpdater.addListener("update-not-available", function(event) { console.log('releaseNotes', 'Update Not Available')})

We can use these events to provide feedback to the user on the status of the auto-update process. Next,

we need to configure our Electron application where to check for a new version.

Squirrel for Mac will ping a remote url and then handle the response. If the server responds with an

HTTP status of 204, the Auto Updater will understand that no update is available. If the server responds with an HTTP status of 200, an update is available and a bit of JSON is sent back. Here is a sample response:

{  "url": "http://mycompany.com/myapp/releases/myrelease",  "name": "My Release Name",  "notes": "These are some release notes",  "pub_date": "2017-03-18T12:29:53+01:00"}

This JSON response needs to contain at a minimum the url to the update. The other properties are

optional. The Auto Updater will use this url value to automatically download the update for us.

To set the url that the Auto Update will check against, we use the setFeedURL method. Once this is set,

we can then call the checkForUpdates method and perform the actual check. Here is some sample code that will get the app's current version, and then call our custom endpoint to perform the auto-update check.

let appVersion = app.getVersion()

let updateUrl = 'https://apress-electron-manager.herokuapp.com/updates/latest?v=' + appVersion

Then within the createWindow function, add this snippet of code:if (process.platform === 'darwin') { autoUpdater.setFeedURL(updateUrl) autoUpdater.checkForUpdates()}

246

User FeedbackLet's update those event handlers to provide some feedback to the user about the auto-update process. These dialogs should be familiar to you from the earlier chapter on dialogs.

Chapter 16 ■ auto updating Your appliCation

const dialog = electron.dialog

autoUpdater.addListener("update-available", function (event) { console.log('Update Available') dialog.showMessageBox({ type: "info", title: "Update Available", message: 'There is an update available.' + appVersion, buttons: ["Update", "Skip"] }, function (index) { console.log(index) })})

autoUpdater.addListener("update-downloaded", function (event, releaseNotes, releaseName, releaseDate, updateURL) { console.log('releaseNotes', "Update Downloaded") console.log('releaseNotes', releaseNotes) console.log('releaseNotes', releaseName) console.log('releaseNotes', releaseDate) console.log('releaseNotes', updateURL)

dialog.showMessageBox({ type: "info", title: "Update Downloaded", message: "Update has downloaded", detail: releaseNotes, buttons: ["Install", "Skip"] }, function (index) { if (index === 0) {  autoUpdater.quitAndInstall() } autoUpdater.quitAndInstall() })})

autoUpdater.addListener("error", function (error) { console.log('Error') console.log(error) dialog.showMessageBox({ type: "warning", title: "Update Error", message: 'An error occurred. ' + error, buttons: ["OK"] })})

247

Chapter 16 ■ auto updating Your appliCation

autoUpdater.addListener("checking-for-update", function (event) { console.log('releaseNotes', 'Checking for Update')})

autoUpdater.addListener("update-not-available", function (event) { console.log('releaseNotes', 'Update Not Available') dialog.showMessageBox({ type: "warning", title: "No Updates", message: 'No update available at this time.', buttons: ["OK"] })})

You will probably want to adjust these for a better user experience.

Auto Update Server OptionsThere are several prebuilt solutions available for you to use. The Auto Update module's documentation lists these as options:

•

•

•

•

nuts: A smart release server for your applications, using GitHub as a back end. Auto updates with Squirrel (Mac & Windows). [https://github.com/GitbookIO/nuts]

electron-release-server: A fully featured, self-hosted release server for electron applications, compatible with auto updater. [https://github.com/ArekSredzki/electron-release-server]

squirrel-updates-server: A simple node.js server for Squirrel.Mac and Squirrel.Windows that uses GitHub releases. [https://github.com/Aluxian/squirrel-updates-server]

squirrel-release-server: A simple PHP application for Squirrel.Windows that reads updates from a folder. Supports delta updates. [https://github.com/Arcath/squirrel-release-server]

However, there is not too much to the server-side code, so let's set up our own server using Heroku.

Now, this is completely optional; so if you are comfortable working with servers, then please feel free to skip to the next section.

Setting Up HerokuHeroku is a platform as a service (PaaS) that enables developers to build, run, and operate applications entirely in the cloud. It offers a free development option, so we can test out our Auto Update engine without needing to have to pay for a server.

If you do not have a Heroku account, go to https://signup.heroku.com/login and create one. Select

Node.js as the primary development language.

Once, you have completed the signup process, you will be able to create a new Heroku app. Give your

app a custom name, and then select the region you wish the app to run from.

Heroku offers several deployment methods: the Heroku CLI, GitHub, or Dropbox. Feel free to use

whatever method you are the most comfortable with. Let's get the code together that will power our auto update server.

248

Chapter 16 ■ auto updating Your appliCation

The Auto-Update ServerWhat we are doing is running a simple Express server on Heroku that will take the application's version number as a parameter. Our server will check this value, and return the proper response. You certainly could run your own server, but rather than take on the responsibility of being a server admin, using a service like Heroku takes care of that issue. Here is the complete app.js file that will power our server:

'use strict'const fs = require('fs')const express = require('express')const path = require('path')const app = express()

app.get('/updates/latest', function (req, res) { const latest = getLatestRelease() const clientVersion = req.query.v

if (clientVersion === latest) {  res.status(204).end() } else {  let baseURL = getBaseUrl()  let updateURL = baseURL + '/releases/darwin/' + latest + '/electron.zip'

res.json({   url: updateURL,   name: "My Release Name",   notes: "These are some release notes",   pub_date: "2017-04-18T12:29:53+01:00"

}) }})

let getLatestRelease = () => { const dir = __dirname + '/releases/darwin'

const versionsDesc = fs.readdirSync(dir).filter((file) => {  const filePath = path.join(dir, file)  return fs.statSync(filePath).isDirectory() }).reverse()

return versionsDesc[0];}

let getBaseUrl = () => { if (process.env.NODE_ENV === 'development') { return 'http://localhost:3000' } else { return 'http://your-company.com' }}

249

Chapter 16 ■ auto updating Your appliCation

app.listen(process.env.PORT || 3000, () => { console.log(`Express server listening on port ${process.env.PORT || 3000}`)});

There are just a few to note in this code block that you need to be aware of. First, the server resolves the

latest version of your app by traversing the /releases/darwin/ directory. Within the darwin directory, you will have addition directories, one for each release. Since this will be our first release, we have a directory named 1.0.0. In order for a git repo to store a directory, it needs to have a file within it. This can be either a .gitkeep file or just a dummy file. Otherwise, our version directory structure will not be captured, and thus not transferred to the Heroku server. As we add new releases of our app, we need to update this directory structure to reflect our new version.

The other note about this code block is the url that is returned in the JSON to where the actual update is stored. This can be on a traditional server, hosted on S3 or GitHub. That choice is up to you to determine. You will need to modify getBaseUrl function to point to the base url, as well as the updateURL's path. This code sample shows a self-hosted solution.

Once you have finished updating your code to point to where you will host your update, deploy this

server code to your Heroku account.

Testing Our Auto UpdateOnce you have deployed your server code to Heroku, let's test it in our browser. Simply go to https://<your=app-name>.herokuapp.com/updates/latest?v=1.0.0

and you should see the following in the window:

{"url":"http://your-company.com/releases/darwin/1.0.0/electron.zip","name":"My Release Name","notes":"These are some release notes","pub_date":"2017-04-18T12:29:53+01:00"}

This means our server is running and responding properly. We can now return to our Electron code and

complete the changes we need to make.

Signing Your ApplicationTo have auto updating function properly, our Electron applications need to be signed. Otherwise, the auto-updating mechanism will not function. For self-distributed apps and testing, we can generate our own certificate by using the Keychain Access tool, found in the /Applications/Utilities directory.

Create new certificate:Keychain Access ➤ Certificate Assistant ➤ Create a Certificate…Give your certificate a name and select Code Signing as the Certificate Type. Next, we need to set the

trust level. To do this, locate the newly created certificate in the panel, and double-click to open it. Then change the When using this certificate to Always Trust. This will allow our Electron application to be properly signed.

We need to now set the CSC_NAME environment variable, so the signing can occur when we build our

application. In your terminal and in our application's active directory, run

export CSC_NAME="Certificate Name"

Now, when we build our application it will be signed and auto updating will function.If you are planning to distribute through the macOS store, you will need a signing certificate from Apple.

For more on this process see: https://github.com/electron/electron/blob/master/docs/tutorial/mac-app-store-submission-guide.md

250

Chapter 16 ■ auto updating Your appliCation

Building the Application - macOSWith our update server in place and running, and our signing certificate generated and installed, we are ready to build the first version of our app. In the main.js file, you will need to update the updateURL variable to reflect your Heroku server before proceeding. To reduce our build times, let's only build for macOS. Adjust the dist script in the package.json file to:

"dist": "build -m"

Now, let's build our application.

npm run dist

After a few moments, we should have our .dmg file, our .app file, as well as out .zip of our application.

Go ahead and run the application. Once it launches, the Auto Update module will ping our server. Since we only have version 1.0.0 of our app, it will report back that there is no update (Figure 16-1).

Figure 16-1. Our app informing the user that no update is available

Generating an UpdateTo generate an update, we need to do three things. First, build a new version of the application with a new version number. To do this, we just need to change the version number in our package.json file:

"version": "1.0.1"

Then, just rebuild our app. Although we did not make any code changes, the app will still respond as

version 1.0.1.

Second, we need to upload our new build to where we store the application.Third, we need to update our Heroku server to respond correctly based on the proper version number.

Just duplicate our 1.0.0 directory and rename it to match our app's new version. Then upload the new structure to Heroku, and have the server restart.

With all three steps complete, go ahead and run the app. After a few moments, the app should inform

you that an update is available (Figure 16-2).

251

Chapter 16 ■ auto updating Your appliCation

Figure 16-2. The Auto Update module has detected an update

Click the Update button to update the application (Figure 16-3).

Figure 16-3. The Auto Update module has downloaded the update and is ready to apply it

The app will automatically quit and then relaunch. With that, we have a working auto-update system for

our macOS Electron applications.

Auto Updating Windows Applications

The auto-update module for Windows is also based on Squirrel; however, it takes a different approach to how it manages the updates. Unlike the Mac, where a custom server response is needed, auto updating on Windows relies on delta packages and a special RELEASES file. We will show how to properly create these files, so auto updating can occur on Windows.

In addition to having Electron Builder installed, we also need to install another node module, Electron

Builder Squirrel Windows:

npm install electron-builder-squirrel-windows --save-dev

This is a plug-in module for use by Electron Builder.In the previous chapter, we built our Electron application to be built using the NSIS format.

252

Chapter 16 ■ auto updating Your appliCation

if you need to target x32-based Windows platforms, continue to use the nSiS distribution format. if you

■ Note are targeting x64-based Windows platforms, you can use the Squirrel-based distribution format without issue.

Now, we want to have Electron Builder use Squirrel as our target. In the package.json, change

"win": {  "target": [  "nsis"  ],

to

"win": {  "target": [  "squirrel"  ],

You also might want to temporarily change the build flags to only generate Windows builds. This will

save some time while you are learning the process. To do this set the dist script to

"dist": "build -w --x64"

Now, when we execute npm run dist in our terminal, electron builder will generate three files for us:

•	•	•

Electron Demo Setup 1.0.1.exe

autoupdatedemo-1.0.1-full.nupkg

RELEASES

The first file is the installer that you can distribute. It contains both the Squirrel runtime and your

application. The second file is your application's source code stored within a special binary. As we generate new versions of our application, Squirrel will reference the .nupkg files to create delta packages. We will touch on this shortly. The final file is a text that contains a listing of all the app versions, along with checksums and the file name of the *.nupkgs.

this build process can be done on macoS, provided you have install Wine. See this guide for more

■ Note information on how to install it: https://www.davidbaumgold.com/tutorials/wine-mac/ as well as the previous chapter.

To build for Squirrel, we need to add a new attribute, squirrelWindows, within our build object in the

package.json file:

"build": { "appId": "com.ajsoftware.electronapp", "copyright": "Copyright © 2017 Chris Griffith", "productName": "Electron Demo", "electronVersion": "1.4.1", "win": {  "target": [

253

Chapter 16 ■ auto updating Your appliCation

"squirrel"  ] }, "squirrelWindows": {

} }

Before we generate our first release of our application, there are several attributes we need to define.

The first is the app icon. Just like in the previous chapter, we can set the icon attribute to an .ico file.

"win": {  "target": [  "squirrel"  ],  "icon": "./build/icon.ico" }

Signing Your Windows ApplicationLike building auto-updating apps for macOS, Windows apps must also be signed. Otherwise, anti-virus/malware scanners might flag your application, or Windows SmartScreen may require special actions to enable to run it. We doubt this is the user experience you want. There are a variety of third-party certificate vendors that can issue you a certificate that will allow you to formally sign your application. Unfortunately, these options are not free. Thankfully, there is a method to generate your own certificate for development and testing purposes. If you plan to release your application to the public, you will need to formally sign your application.

To generate your own .pfx file, which Electron Builder uses to sign your application, you will need to use

OpenSSL. What is OpenSSL, from their website:

OpenSSL is an open source project that provides a robust, commercial-grade, and full-featured toolkit for the Transport Layer Security (TLS) and Secure Sockets Layer (SSL) protocols.

If you are building your application on a macOS computer, OpenSSL is already installed. If you are building your Electron application on a Windows computer, you will need to download an installer from https://wiki.openssl.org/index.php/Binaries.

To generate our *.pfx file, we need to first generate a private key and certificate. OpenSSL will allow us to

do all three steps. With OpenSSL installed, and then launch your terminal to first generate our private key:

openssl genrsa -aes128 -out privateKey.key 2048

You will be prompted to enter a passphrase for the key. Enter something that you will remember, and

store it in a safe place. This information cannot be recovered.

Next, we can use that key to generate our certificate:

openssl req -new -x509 -days 365 -key privateKey.key -out certificate.crt

It will prompt you to enter the passphrase you just created for the key file. It will then ask you a series of

questions that it will use to identify the certificate. Here is a sample of those questions.

You are about to be asked to enter information that will be incorporated

254

Chapter 16 ■ auto updating Your appliCation

into your certificate request.

What you are about to enter is what is called a Distinguished Name or a DN.There are quite a few fields but you can leave some blankFor some fields there will be a default value,If you enter '.', the field will be left blank.-----Country Name (2 letter code) [AU]:YORU COUNTRYState or Province Name (full name) [Some-State]:YOUR STATELocality Name (eg, city) []:YOUR CITYOrganization Name (eg, company) [Internet Widgits Pty Ltd]:YOUR COMPANYOrganizational Unit Name (eg, section) []:YOUR UNITCommon Name (e.g. server FQDN or YOUR name) []:YOUR NAMEEmail Address []:your-name@somewhere.com

Now, with our private key and certificate generated, we can combine them into a .pfx file by using this

command:

openssl pkcs12 -export -out certificate.pfx -inkey privateKey.key -in certificate.crt

You will once again be prompted for the passphrase for your privateKey. Then you will be asked for the

password that will be used to unlock the pfx file. Safely store all three files, as they are uniquely generated. With our pfx file created, we can modify the package.json to enable signing of our Windows application. We place our *.pfx file in a cert directory within our general development directory. Set the certificateFile to the location of the *.pfx file, and the certificatePassword to the export password.

"win": {  "target": [  "squirrel"  ],  "certificateFile": "./certificate.pfx",  "certificatePassword": "your-password",  "icon": "./build/icon.ico" },

Customizing the Squirrel InstallerUnlike the NSIS installer, using the Squirrel installer actually has very few configurations. The first item we can set is the icon for the generated setup.exe file. Typically, this will be the same as your application's icon. But unlike, the application icon, the location of this file must be remotely hosted. We typically place it in the same directory that we stored the Windows updates.

"squirrelWindows": {  "iconUrl": "http://your-company.com/releases/win/icon.ico", }

Next, we can modify the loading animation that is displayed by Squirrel as it silently installs your

application. The default image looks like Figure 16-4, albeit animated.

255

Chapter 16 ■ auto updating Your appliCation

Figure 16-4. Default Squirrel Loading GIF

You can easily replace with your own gif file. Simply set the loadingGif to a file. You do not need to have

this image be animated.

"squirrelWindows": {  "iconUrl": "http://your-company.com/releases/win/icon.ico",  "loadingGif": "./build/loader.gif" }

The next item to adjust is a subtle one. When Squirrel installs your application, it places it within the AppData directory. It will create a new directory based either on your app ID or the name attribute. When Squirrel creates the folder to install your application, and by default it will use your app ID. However, since your app ID will probably follow the pattern of com.company-name.app-name, Windows will truncate the directory name to just com. Instead, we recommend using your name attribute instead. To do this, add useAppIdAsId and set it to false.

"squirrelWindows": {  "iconUrl": "http://your-company.com/releases/win/icon.ico",  "loadingGif": "./build/loader.gif",  "useAppIdAsId": false }

This will now enable us to build our Windows application, but we need to make some additional

changes to the main.js file to support auto updating with Squirrel. First, we need to set a new updateURL to check for any updates. Here is the new code block for this.

if (process.platform === 'darwin') { autoUpdater.setFeedURL(updateUrl) autoUpdater.checkForUpdates()} else { updateUrl = "http://your-company.com/releases/win/" autoUpdater.setFeedURL(updateUrl) autoUpdater.checkForUpdates()}

256

Chapter 16 ■ auto updating Your appliCation

Since our app is now dependent on Squirrel to manage itself, we need to properly handle those events before our application creates its window. These events center around the various installation or uninstall steps that might need to occur. Here is a complete code sample that handles each of the Squirrel events that should be added to the main.js file:

if (handleSquirrelEvent()) { // squirrel event handled and app will exit in 1000ms, so don't do anything else return}

function handleSquirrelEvent() { if (process.argv.length === 1) { return false }

const ChildProcess = require('child_process') const path = require('path')

const appFolder = path.resolve(process.execPath, '..') const rootAtomFolder = path.resolve(appFolder, '..') const updateDotExe = path.resolve(path.join(rootAtomFolder, 'Update.exe')) const exeName = path.basename(process.execPath)

const spawn = function (command, args) { let spawnedProcess, error

try {  spawnedProcess = ChildProcess.spawn(command, args, { detached: true }) } catch (error) { }

return spawnedProcess }

const spawnUpdate = function (args) { return spawn(updateDotExe, args) }

const squirrelEvent = process.argv[1] switch (squirrelEvent) { case '--squirrel-install': case '--squirrel-updated':  // Optionally do things such as:  // - Add your .exe to the PATH  // - Write to the registry for things like file associations and  // explorer context menus

// Install desktop and start menu shortcuts  spawnUpdate(['--createShortcut', exeName])

setTimeout(app.quit, 1000)  return true

257

Chapter 16 ■ auto updating Your appliCation

case '--squirrel-uninstall':  // Undo anything you did in the --squirrel-install and  // --squirrel-updated handlers

// Remove desktop and start menu shortcuts  spawnUpdate(['--removeShortcut', exeName])

setTimeout(app.quit, 1000)  return true

case '--squirrel-obsolete':  // This is called on the outgoing version of your app before  // we update to the new version - it's the opposite of  // --squirrel-updated

app.quit()  return true }}

You might be wondering about the spawn code that is referenced in this sample. If you recall, Squirrel installs our app with the AppData folder. Unfortunately, it does not auto generate a shortcut for the user and place it on their desktop. That spawn code will do this as part of the install or update process. Our standard auto-update events will still be triggered, so we need to have the code in place to allow Squirrel to perform its tasks.

Generating Our First BuildWith our app's code updated to handle the Squirrel events and the url to check for any updates, let's properly generate our application. From the terminal:

npm run dist

This process will take a few moments to complete. Once it has completed, go ahead and launch the

xxx-setup.exe on a Windows machine. You should see your screen loading gif, then a shortcut created on the desktop. The auto-update check should also run (Figure 16-5).

Figure 16-5. The No Update dialog

Since we have not provided any update files, you will see a dialog informing you that no updates are

available. So, let's make an update!

258

Chapter 16 ■ auto updating Your appliCation

Generating an UpdateTo properly generate an update and the associated files, we need to follow some simple steps. First, those three files that we generated for our first release need to be uploaded to the server that our auto update url is pointing to.

You technically don't need to use a remote server. if you run a local server, say using express, you

■ Note can reference that url instead.

Second, we need to update the package.json file to inform Electron Builder where to reference our

remote releases.

"squirrelWindows": {  "iconUrl": "http://your-company.com/releases/win/icon.ico",  "remoteReleases": "http://your-company.com/releases/win/",  "loadingGif": "./build/loader.gif",  "useAppIdAsId": false }

This url should be the same as our auto-update URL in our application code. Now when we build our new application, electron builder will use the files hosted there to generate our *-delta.nupkg file, as well as update the RELEASES file with the new data.

Finally, you need to update the version number in the package.json. If you want to make a simple

change to the index.html, you can do that as well.

With those changes in place, execute the npm run dist command again. The process will take a bit

longer as the remote files are accessed. When it is complete, we will have several new files alongside of the files from the first build:

autoupdatedemo-1.0.0-full.nupkg

autoupdatedemo-1.0.1-delta.nupkg

autoupdatedemo-1.0.1-full.nupkg

Electron Demo Setup 1.0.0.exe

Electron Demo Setup 1.0.1.exe

RELEASES

Upload these new files, along with the RELEASES file to the server. Once they have transferred, launch

the application again on your Window machine. This time, there will be an update available (Figure 16-6).

259

Chapter 16 ■ auto updating Your appliCation

Figure 16-6. The AutoUpdate dialog

Click the Update button, and the update will be downloaded for us (Figure 16-7).

Figure 16-7. The AutoUpdate Downloaded dialog

Once that is done, we can install it and relaunch our application. Our application is now up to date! You

now have the framework in place to auto update your Electron application on Windows.

Alternative SolutionsNow, using Electron Builder is not the only option to create packaged Electron application. The Electron team also has a Windows installer module. The package can be found at https://github.com/electron/windows-installer. This module does expose more settings for your Squirrel instance. You might want to consider looking at this solution if your application needs additional parameters configured, like a custom-loading Gif.

260

Chapter 16 ■ auto updating Your appliCation

Another option you might also explore is Electron Forge (https://beta.electronforge.io/).

Developed by the same team as Electron Builder, this project aims to be a single command-line interface for Electron. It supports packaging to a wide range of platforms. What is interesting is, it uses Electron's Windows Installer for any Squirrel packages. This effort is very intriguing, and it could be a nice solution to for your Electron development workflow.

Finally, we want to touch on Electron Builder itself. If you spend some time reading the documentation, you might notice it has a section on auto updating. Instead of using Electron's built-in Auto Update module, it instead relies on their own electron-updater module. There may be advantages to using this solution instead of the built-in solution, but you will need to make that call yourself.

Summary

You should have the framework in place to enable auto updating for both macOS and Windows. Both platforms require unique solutions to enable this functionality. Now that you have built these exploration apps, you can fold the code into your actual application.

You can also improve the dialog messaging and user interaction of the update process. A common improvement would be to allow the user to check for an update via a menu item. You may also wish to provide some feedback that the update is being downloaded.

261

CHAPTER 17


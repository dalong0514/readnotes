# 0701. Working with the Dialog Module

The Electron dialog module provides us with the ability to display native system-level dialogs, including file open, file save, and various alerts. If you have written traditional web apps, you will know that these types of dialogs are not all available to you. In this chapter, we will look at the three dialog types and many of the parameters we can control.

The Dialog module is restricted to the Main process, meaning to interact with it we will either need to call its methods from a menu event, via the Inter-Process Communication (IPC) module from the Renderer process, or by using the Remote module (as seen in a previous chapter).

## 7.1 Getting Started

Let's clone a fresh copy of Electron so we have a clean starting point for exploring interacting with the Dialog Module.

git clone https://github.com/electron/electron-quick-start dialog-example

Next, change your active directory to electron-quick-start.

cd dialog-example

Now, we need to install the dependencies:

npm install

Finally, reset Git with

git init

The File Open Dialog

Unlike using the File API to open and read a file, as we would in a traditional web app, in Electron we will use a combination of the Dialog module and Node's FS module. The basic method to display a File Open dialog is dialog.showOpenDialog.

We will begin by opening the index.html file and replace the content within the <body> tag with

<button id="select-directory">Choose a directory</button><textarea id="selectedItem"></textarea>

This will give us control to trigger our File Open Dialog, and a container to display the results of the

interaction. For a touch of style, add this CSS (within the <head> tag) as well:

<style> button { color: rebeccapurple; font-family: sans-serif; font-weight: bold; padding: .5rem; background-color: #ccc; box-shadow: 2px 2px 2px #ccc; display: block; margin: 1em; }

textarea { width: 90%; }</style>

Next, switch to the renderer.js file. Here we need to attach an event listener to the button to

communicate to the Main process. Since we are going to be using the IPC module, we need to import it.

const ipc = require('electron').ipcRenderer

Now, we need the reference to the button

const selectDirBtn = document.getElementById('select-directory')

Finally, we can define our event listener for this button:

selectDirBtn.addEventListener('click', function (event) { ipc.send('open-directory-dialog')})

We will use the synchronous IPC call, since the application is basically ‘frozen' while the dialog is being

displayed.

Turning to the main.js file, we need to write the companion listener for the IPC event we just made.

Again, we need to import the IPC module into our code. Additionally, the Dialog module will be needed as well. These should go at the beginning of the code:

const ipc = electron.ipcMainconst dialog = electron.dialog

With both the IPC module and Dialog module defined, we can write the event listener. The event

listener is simply:

ipc.on('open-directory-dialog', function (event) {})

Within this function, we will make our call to the Dialog module to display the File Open dialog. This

method has three optional parameters, but two of them will almost always be used.

The first parameter is a reference to the BrowserWindow object. On macOS, it is common for dialogs to

appear as connected sheets to the active window, and not appear detached. We will look at this parameter later in the chapter. For now, we can ignore it from our parameters.

The second parameter that can be passed into method is an object that contains the various dialog

settings. We will explore these after we have our first dialog up and running. For this initial sample, we need to set the properties that the Open Dialog can have. Table 7-1 lists the attributes that can be set.

Table 7-1. The Dialog Module showOpenDialog properties

Property name

Dialog Action

openFileopenDirectorymultiSelectionscreateDirectoryshowHiddenFiles

Will allow files to be selected.Will allow directories to be selected.Will allow multiple items to be selected.Will add a ‘New Folder' button to the dialog (macOS only).Will display normally hidden system files.

promptToCreate

Will prompt for the creation of a file path if entered by the user (Windows only).

These properties can be combined and passed in as an array, or as a string if only one property is

needed.

On Windows and Linux an open dialog cannot be both a file selector and a directory selector, so if you

set properties to [‘openFile', ‘openDirectory'] on these platforms, a directory selector will be shown.

For our code, we will allow selecting a directory. Our options object is simply:

{ properties: ['openDirectory']}

The final parameter is the callback function, assuming you want to do something with the selection. This callback will be passed in either a string or an array of strings, each representing the file path to the selected item(s). For this sample code, we will simply take the result and use the IPC module to send it to the Renderer process. Here is the completed code:

ipc.on('open-directory-dialog', function (event) { dialog.showOpenDialog({ properties: ['openDirectory'] }, function (files) { if (files) event.sender.send('selectedItem, files) })})

One final thing to add to our demo is to write the event listener for the ‘selected-directory' IPC event in

the Renderer.

ipc.on('selectedItem, function (event, path) { document.getElementById('selectedItem').innerHTML = �You selected: ${path}�})

This function will then write out the path to our textarea.

Save the files and run our application using npm start.Clicking the ‘Choose a directory' button, then select a directory on your computer. The path

information will then be sent from the Main process to the Renderer process and be displayed in the text area, as shown in Figure 7-1.

Figure 7-1. The select directory style dialog

Additional Open Dialog PropertiesThe showOpenDialog has several other properties that can be set within the options object. The first is the title property.

On Windows, this string will be displayed on the top of the dialog as shown in Figure 7-2.

Figure 7-2. The title property being displayed

■ Note

the title property is ignored on macoS.

The next property that can be set allows you to define an initial path that the dialog will open to. This can

be very useful to pre-navigate the user to the proper directory. You will need to pass a properly constructed path. If we wanted to have our dialog start at our Documents directory, the call would look like this.

dialog.showOpenDialog({ title: 'Select a workspace...', properties: [ 'openFile'], defaultPath: '/Users/<username>/Documents/',}, function (files) { if (files) event.sender.send('selectedItem, files)})

Of course you will need to switch the path based on the platform. For example, here we define the user's document directory based on the platform. That's why you should prefer the use of dirname or ./, and use the path module rather than hard-code the default path.

let startPath = ''if (process.platform === 'darwin') { let startPath = '/Users/<username>/Documents/'}

You can also change the label text on the default button by setting the buttonLabel property. This will

override the default ‘Open' label from the system dialog.

dialog.showOpenDialog({ title: 'Select a workspace...', properties: [ 'openFile'], defaultPath: '/Users/<username>/Documents/', buttonLabel: "Select..."}, function (files) { if (files) event.sender.send('selected-directory', files)})

Selecting a FileInstead of selecting a directory, let's see how to select a specific file from the local file system. In the index.html file, let's add a new button after our Choose a directory button:

<button id="select-file">Choose an image file</button>

In the renderer.js file, get the reference to this button:

const selectFileBtn = document.getElementById('select-file')and also add the event listenerselectFileBtn.addEventListener('click', function (event) { ipc.send('open-file-dialog')})

Now, let's turn to the main.js file and add our initial code:

ipc.on('open-file-dialog', function (event) { let startPath = ''

if (process.platform === 'darwin') { startPath = '/Users/<username>/Documents/' }

dialog.showOpenDialog({ title: 'Select a workspace...', properties: ['openFile'], defaultPath: startPath,

buttonLabel: "Select...", }, function (files) { if (files) event.sender.send('selectedItem', files) })})

This should look almost identical to the directory code from earlier. The only change is that the

properties array is now set to openFile instead of openDirectory.

The last property you might want to include is to set a file filter. This allows you to control the files that the user can select from within the dialog. This is the array of objects that defines the display label and the allowable file extensions. When defining the extensions, you only need to include the extension and not the dot nor the wildcard element (e.g., ‘.jpg' and ‘*.jpg'). So, our code will now look like this:

ipc.on('open-file-dialog', function (event) { let startPath = '';

if (process.platform === 'darwin') { startPath = '/Users/chrisgriffith/Documents/' }

dialog.showOpenDialog({ title: 'Select a file...', properties: ['openFile'], defaultPath: startPath, buttonLabel: "Select...", filters: [  { name: 'Images', extensions: ['jpg', 'png', 'gif'] } ] }, function (files) { if (files) event.sender.send('selectedItem', files) })})

On Windows, this information will be shown as a drop-down menu that will allow you to switch the

filters (Figure 7-3).

Figure 7-3. The Save as type option being displayed

On macOS, this control is not shown, but the filter is still applied to the dialog. Please note we've

changed the ‘openDirectory' property to ‘openFile' in this instance.

The BrowserWindow ParameterWe skipped the initial parameter that the showOpenDialog supports since it is optional. On macOS, it is quite common to have the Open dialog attach itself to the actual application window and not have it open in a separate window, as shown in Figure 7-4.

Figure 7-4. The Open File dialog on macOS attached to the Application Window

If you choose to not attach the dialog to the application window, note that the file dialog is not automatically centered, and you will need to programmatically position it. To attach a dialog to the application window, simply pass in the reference to the application window into the dialog's show method. Here is the basic code needed to display the dialog to select a file. Once the user has selected a file, the code will emit an IPC event to the renderer process with information on the selected files.

dialog.showOpenDialog(mainWindow, { title: 'Select a file...', properties: ['openFile'], defaultPath: '/Users/<username>/Documents/', buttonLabel: "Select...", filters: [ { name: 'Images', extensions: ['jpg', 'png', 'gif'] }, { name: 'Text', extensions: ['txt'] } ]}, function (files) { if (files) event.sender.send('selected-directory', files)})

Just remember, if your application is going to support multiple windows, you need to ensure that you

are referencing the correct window instance to attach the dialog to.

A Brief Look at Node's FS ModuleThe reading and writing of files is handled using one of Node's core modules, FS (aka File System). This module provides both synchronous as well as asynchronous versions of each of its methods. As a rule, is it better to use the asynchronous option over the synchronous option. By doing so, we should not block our user interaction, since the code's execution thread will not be blocked. The basic functions available to us are the following:

•	 Open or create a file•	 Get file status and information•	 Write content to a file•	•	 Close a file•	 Delete a file

Read a file's contents

To use the fs module, import it using the standard method:

const fs = require('fs')

Opening a FileFor most operations, you will not need to manually open and close the file you are working with. The standard read and write commands will do this automatically for you. However, if you are working with streaming content or needing to access specific blocks within the file, you will need to use this method to properly work with that file. Each of the parameters for the fs module is described in Table 7-2.

fs.open(path, flags[, mode], callback)

Table 7-2. The FS Module's open method's parameters

Parameter

Description

pathflagsmode

This string is the full file path and file name.Controls the interactions with the file (see Table 7-3).Optional parameter that defines the permissions.

callback

This function receives two arguments: the error code and the file descriptor.

The FS module's flag's parameter supports several different access settings to the file, and these are

listed in Table 7-3.

112

Chapter 7 ■ Working With the Dialog MoDule

Table 7-3. FS Modules' access flag values

Flag

Description

r

r+rsrs+w

wxw+

aa+ax

ax+

Opens the file for reading.

Opens the file for reading and writing.Opens the file for reading, synchronous mode.Opens the file for reading and writing, synchronous mode.Opens the file for writing. If the file does not exist, it will be created. If the file does exist, it will be overwritten.Opens the file for writing. If the file does exist, the function will fail.Opens the file for reading and writing. If the file does not exist, it will be created. If the file does exist, it will be overwritten.Open file for appending. The file is created if it does not exist.Open file for reading and appending. The file is created if it does not exist.Opens the file for appending. If the file does exist, the function will fail.

Open file for reading and appending. If the file does exist, the function will fail.

Getting File InformationIf you need to get information about a file, use the fs.stats method. This is quite useful in determining if the file is a real file or if it is a directory. Here is a snippet that takes in a file path, then outputs to the console, the file information:

fs.stat(filePath, function (err, stats) { if (err) {  return console.error(err) } console.log(stats) console.log("Got file info successfully!")

// Check file type console.log("isFile ? " + stats.isFile()) console.log("isDirectory ? " + stats.isDirectory())})

gives us:

fs.Statsatime: Mon Mar 13 2017 15:13:31 GMT-0700 (PDT)birthtime: Mon Mar 13 2017 15:09:16 GMT-0700 (PDT)blksize: 4096blocks: 8ctime: Mon Mar 13 2017 15:13:12 GMT-0700 (PDT)dev: 16777220gid: 1859252656ino: 30007351mode: 33188mtime: Mon Mar 13 2017 15:13:12 GMT-0700 (PDT)

nlink: 1rdev: 0size: 603uid: 224974590

Got file info successfully!isFile ? trueisDirectory ? false

Writing a FileTo write a file to the user's file system, simply use the fs.writeFile method. The parameters for this module are shown in Table 7-4.

fs.writeFile(file, data[, options], callback)

fs.writeFile(fileName, content, function (err) { if(err){  console.log("An error occurred creating the file "+ err.message) } else {  console.log ("The file has been successfully saved") }})

Table 7-4. The FS Module's parameters

Parameter

Description

pathflagsmode

This string is the full file path and file name.Controls the interactions with the file (see Table 7-3).Optional parameter holds details about encoding, mode, and flag. By default, the values of encoding are utf8, mode is octal value 0666, and flag is ‘w'.

callback

This function receives two arguments: the error code and the file descriptor.

Reading FilesTo read a file from a user's computer, it can be done in two variations: reading the complete file or partially reading the file. The more common method will be reading the complete file. Here is a code snippet to do this:

fs.readFile(filepath, 'utf-8', function (err, data) {  if(err){   alert("An error occurred reading the file :" + err.message)   return  }  //Display the file contents  console.log("The file content is : " + data)})

If you want to read the file in synchronous mode, use fs.readFileSync() instead. If you need to perform a

partial read of a file, refer to the documentation for the fs module, available at <nodejs.org/api/fs.html>.

Deleting a FileIf you need to delete a file on the user's computer, then you will use the fs.unlink() method. Since these commands are based on the standard POSIX functions (a standard command set for manipulating files and directories), the delete function is referred to as unlink. As a good measure, you should use the fs.existsSync () method to test if the file exists before attempting to delete it.

if ( fs.existsSync(filePath) ) { fs.unlink(filepath,function(err){ if(err){  console.log("An error ocurred updating the file"+ err.message)  return } console.log("File succesfully deleted") })}

Watching for UpdatesAnother useful method available in the fs module is the fs.watch() method.

fs.watch(fileName, { persistent: true}, function(event, filename) { console.log(event + " event occurred on " + filename)})

Working DirectoriesIn all the previous examples, we were working with just files. The fs module also supports working with directories as well. To create a new directory, use the fs.mkdir() method.

fs.mkdir(myDir, function(err){ if (err) {  console.log('mkdir err:'+err) }

console.log('New Directory Created')})

Reading the Directory ContentsOften, reading the entire contents of a directory is needed. To perform this action, use the fs.readdir() or fs.readdirSync() methods. The result of calling either method will be an array for files and directories contained within the parent directory. If we read the electron-quick-start directory using this code:

fs.readdir('./', function(err, files){ if (err) {  console.log(‘readdir err:'+err)  return } console.log(files)})

we will get the following array back:

[".git", ".gitignore", "LICENSE.md", "README.md", "index.html", "main.js", "node_modules", "package.json", "renderer.js"]

Deleting a DirectoryWhen you need to remove a directory from the user's computer, the fs.rmdir() or fs.rmdirSync() methods can be used. Simply pass in the path to the directory to the methods. It will not prompt the user about the action.

fs.rmdir(myDir, function(err){ if (err) {  console.log('rmdir err:'+err)  return } console.log('deleted the directory')})

For more about this module, refer to the Node documentation as there are many other methods you

should be aware of.

The File Save Dialog

The showSaveDialog method is like the openFileDialog, just with fewer parameters. Let's add a new button to our index.html:

<button id="save-file">Save</button>

and in the render.js file add this code:

const saveFileBtn = document.getElementById('saveFile')

saveFileBtn.addEventListener('click', function (event) { ipc.send('save-file-dialog')})

Finally, in the main.js, we will add our IPC listener:

ipc.on('save-file-dialog', function (event) {})

Let's explore the parameters we can set in the showSaveDialog. Just like its companion, the first

parameter is the reference to the application window. This parameter is optional; if it is included then the dialog will appear as an attached sheet (Figure 7-5).

Figure 7-5. The dialog with the sheet option enabled

The Save Dialog has four options that can be set: title, defaultPath, buttonLabel, and filters. These

parameters should be familiar from the File Open dialog.

ipc.on('save-file-dialog', function (event) { let startPath = '';

if (process.platform === 'darwin') { startPath = '/Users/<username>/Documents/' }

dialog.showSaveDialog({ title: 'Save file...',  defaultPath: '/Users/<username>/Documents/highscores.txt',  buttonLabel: "Save",  filters: [  { name: 'Text', extensions: ['txt'] } ] }, function (file) { console.log(file)

})})

There are a few minor differences to be aware of. The first difference is the defaultPath string. If you simply pass in just a path, the dialog will default to use ‘Untitled' as the filename. If you want to send this dialog with a suggested filename, include it as part of the defaultPath.

The second difference is that the file will inherit the extension from the last time in the FileFilter array

(if one is set). So, if you do not set the default name, you might want to take care to set the preferred extension via the filters. Note, if the Hide Extension option is enabled, the filename will not show the extension, regardless of the FileFilter setting.

The result of this method will be the full file path that the user selected.

/Users/<username>/Documents/highscores.txt

The actual writing of the file would be done via the Node FS module ]. For this simple example, we will

save a small text string as our high score data. Here is the complete File Save dialog

ipc.on('save-file-dialog', function (event) { let startPath = "";

if (process.platform === 'darwin') { startPath = '/Users/<username>/Documents/' }

dialog.showSaveDialog({ title: 'Save file...', defaultPath: startPath +'highscores.txt', buttonLabel: "Save", filters: [  { name: 'Text', extensions: ['txt'] } ] }, function (file) { console.log(file); if (file) {  let theData = "Chris,10000"  FS.writeFile(file, theData, function (err) {  if (err === null) {   console.log('It\'s saved!');

} else {   //ERROR OCCURRED   console.log(err);  }  }); } })})

The Message Dialog

In addition to the tandem File Open and File Save methods, the Dialog API also supports displaying a Message Dialog (Figure 7-6). These dialogs are often referred to as Alert Dialogs.

Figure 7-6. A sample Message Dialog

The showMessageBox method also follows the same general parameter sequence: browserWindow, options, and the callback function. There are four variations of the MessageBox; info, error, question, and none. These are defined by setting the type property in the options object. On macOS, there is no difference in display of these MessageBox types, but on Windows, the icon will change to reflect the type (see Figures 7-7 through 7-10).

Figure 7-7. The Info type MessageBox on Windows

Figure 7-8. The error type MessageBox on Windows

Figure 7-9. The Warning type MessageBox on Windows

Figure 7-10. The none type MessageBox on Windows

Let's extend our Electron Dialog sample to support displaying these types.In our index.html, we will add four buttons, one for each type:

<h2>Message Box</h2><button id="info">Info Type Dialog</button><button id="error">Error Type Dialog</button><button id="question">Question Type Dialog</button><button id="none">None Type Dialog</button>

In our renderer.js file, we will get the references to each of the buttons:

const infoDialogBtn = document.getElementById('info')const errorDialogBtn = document.getElementById('error')const questionDialogBtn = document.getElementById('question')const noneDialogBtn = document.getElementById('none')

then create the click EventListeners for each button:

infoDialogBtn.addEventListener('click', function (event) { ipc.send('display-dialog', 'info')})

errorDialogBtn.addEventListener('click', function (event) { ipc.send('display-dialog', 'error')})

questionDialogBtn.addEventListener('click', function (event) { ipc.send('display-dialog', 'question')})

noneDialogBtn.addEventListener('click', function (event) { ipc.send('display-dialog', 'none')})

We will use the fact that we can send additional arguments in our IPC call to pass along the dialog type

we want to display. In the main.js file we can create this starter listener.

ipc.on('display-dialog', function (event, dialogType) { console.log(dialogType)})

Let's expand out the properties in the options parameter for our dialog. The first property to set will be defining the custom button labels. This property will accept either a string for the label or an array of strings for labels. On macOS, the order of the button is laid out from the right to the left. On Windows, the buttons are laid out vertically. So, setting our dialog buttons to this array to:

dialog.showMessageBox({  buttons: ['Save', 'Cancel', 'Don\'t Save']})

This will cause our dialogs to look like this (without the title or description, as they haven't been added

yet) in Figure 7-11.

Figure 7-11. A Message Dialog on macOS

Another thing to note, on Windows: if this array contains the string ‘Cancel' or ‘No', then it will

automatically be positioned along the bottom of the dialog.

The next property you can set is the defaultId. This integer will tell the dialog which item in the button

array to set as the default button. Since we want the Save button to be the default action, we can set this value to 0, although, without this parameter, the default value would also be 0.

defaultId: 0

The canceled property is only used on the Windows platform, and only if the buttons array does not

contain either ‘Cancel' or ‘No'. Since Windows message dialogs also contain a close button in the upper right, this is the index value we can assign to the element. If your buttons array does contain either string, that button will return the same value as the displayed Cancel or No button.

With our buttons defined, we can turn our attention to the text in the dialog. The dialog method has

three separate text elements: title, message, and detail.

The title property is only used on Windows, and it is displayed along the top of the dialog box.The next display property is the message string. This is text that is displayed in a larger font and bold on

the preceding Mac OSX example.

The final text display property is the detail string. This is what is shown in the body of the dialog. Here is

our showMessageBox code so far:

dialog.showMessageBox({ type: dialogType, buttons: ['Save', 'Cancel', 'Don\'t Save'], defaultId: 0, cancelId: 1, title: 'Save Score', message: 'Backup your score file?', detail: 'Message detail'})

This code will create a dialog that looks like Figure 7-12.

Figure 7-12. The Message Dialog Box

Custom IconsOn Mac, the icon that is displayed with each dialog type is the application icon. If you want to have a custom icon, say a warning icon with your app icon overlaid over it, see what is shown in Figure 7-13.

Figure 7-13. A sample custom icon

First, we need to import the nativeImage module from Electron in our main.js file.

const nativeImage = electron.nativeImage

This module will allow us to work with the icons in a more convenient fashion. Here we will reference

the custom icon:

let warningIcon= nativeImage.createFromPath('images/warning.png')

Then in the dialog options, we can set the icon property to this value:

ipc.on('display-dialog', function (event, dialogType) {dialog.showMessageBox({ type: dialogType, buttons: ['Save', 'Cancel', 'Don\'t Save'], defaultId: 0, cancelId: 1, title: 'Save Score', message: 'Backup your score file?', detail: 'Message detail', icon: warningIcon }, function (index) { console.log(index) });})

So, now when we display our dialog, our custom icon is displayed instead of the default icon (Figure 7-14).

Figure 7-14. The dialog using our custom icon

You might consider writing your dialog method to be more generic in nature, switching out icons,

labels, and button text as needed via input parameters.

Handling the ResponseThe callback function will accept the index value of the response from the dialog.

ipc.on('display-dialog', function (event, dialogType) { console.log(dialogType) dialog.showMessageBox({ type: dialogType, buttons: ['Save', 'Cancel', 'Don\'t Save'], defaultId: 0, cancelId: 1, title: 'Save Score', message: 'Backup your score file?', detail: 'Message detail', icon: warningIcon }, function (index) { console.log(index) })})

Depending on how you structure your code, you might handle the response within this function, or

send back an ipc message to the Renderer process to handle it.

Error Dialogs

Although the showMessageBox does have an error type, there is an additional method we can call for when the app has yet to emit its ready event. This is the showErrorBox method; see Figure 7-15 for a sample of this. This method takes in two parameters: a title and its content. Custom icons are not supported at this time.

dialog.showErrorBox('Frak!', 'Cyclons reported on the port hanger deck!')

Figure 7-15. The Error message dialog. It will use the application's icon by default.

This method does not support custom icons nor changing buttons options (there is a default ‘OK'

button that will dismiss the box but cannot be customized). Also, note there is no callback function, since there is only the single response that can occur.

## Summary

In this chapter, we explore the File Save and File Open dialogs and their display options. We also looked at the Message dialog as well. The variations of this method were examined, so you can display the proper type per the platform's user interface guidelines. Finally, we demonstrated the simple Error dialog method.
your app

Once you've gotten to a stage with your app where it's ready for people to use, thenext step is to consider how you want to package it for running on your users' com-puters so that users can install it. There are lots of different ways to do this, anddepending on the app you're building and who your audience is, it's good to knowwhich options exist and how you can make use of them.

In this chapter, we'll explore those options and show how to package your appas executable binaries for Mac OS, Microsoft Windows, and Linux (Ubuntu), includ-ing creating Windows installers for your Electron apps.

First, we'll look at some options for protecting your source code and the pros

and cons of those approaches.

291

292

CHAPTER 18 Packaging the application for the wider world

18.1 Creating executables for your app

When you're ready to ship your app to the wider world, start by making sure it's avail-able in a format for users to download and run on their computer. For this, you needto create executables for each OS you want to support. The good news is that you cando this from a single codebase, and the only negative is that there's a bit of fiddly workto produce executables for all the OSs. Luckily, there are some tools out there to takecare of this work, and this section shows you how to use them to create executables foreach OS.

We'll start by looking at creating apps for Microsoft Windows.

18.1.1 Creating an NW.js app executable for Windows

The world's most popular OS, Microsoft Windows, has had quite a journey in the lastfew years. Following the release of Windows 7, Microsoft was trying to compete withApple in the tablet market. It released Windows 8, a version of Windows with a touch-friendly UI that could work on both personal computers and tablets. It was a boldmove, but unfortunately it didn't go down well with users of Windows; the removal ofthe Start button from the desktop was a major stumbling block. Windows 8.1 shortlycame out and reintroduced the much-loved Start button back to the desktop, and lastyear Windows 10 was introduced as a free upgrade to existing users of Windows 7, 8,and 8.1.

Although Windows isn't as dominant as it was in the 1990s and early 2000s, the OSstill has the largest market share out there, with Windows 7 being the frontrunner.There are quite a few versions of the OS in use today (including, believe it or not,Windows XP), but building a .exe file for Windows tends to work seamlessly across themajor versions of the OS.

For the sake of simplicity, I'll assume you have Windows 10 running on your com-puter. It's a free upgrade for users, but if you're running Mac OS or even Linux, don'tdespair, because there are other options. You can install virtual machine software andimages that will allow you to run a copy of Windows 10 to test your app against.

18.1.2 Installing a virtual machine

Table 18.1 lists some virtual machine software and image options.

Table 18.1 Popular virtual machine software

Virtual machine

Platform

URL

Cost

VirtualBox

VMware Fusion

Parallels

Windows/Mac/Linux

virtualbox.org

Mac

Mac

vmware.com/products/fusion

parallels.com

Free

$89

$95

Creating executables for your app

293

Once you have virtual machine software you're happy with, find a virtual machineimage running the version of Windows that you want to test against. A quick search onGoogle will reveal options for you.

When you've got a virtual machine running Windows (or you have a computerrunning Windows natively), you can proceed to build and test an executable versionof your app for that OS.

18.1.3 Building a .exe of an NW.js app for Windows

For this exercise, you'll turn to one of the existing apps you built earlier in this book—a file explorer app called Lorikeet—and look at how to turn that into an executableapp. In chapter 4, you covered generating a Windows version of the NW.js app using atool called nw-builder. You could repeat that step here, but instead I'll show you what'sgoing on when you create a binary executable of the app on Windows. That way, you canunderstand how the sausage is made, rather than getting the sausage and eating it.

Let's grab a copy of the Lorikeet app that you built from GitHub:

git clone git://github.com:/paulbjensen/cross-platform-desktop-applications/chapter-04/lorikeet-nwjs

Now, install the dependencies, and you'll be ready to build a copy of the app as a Win-dows executable:

cd lorikeet-nwjsnpm install

Start by creating a zip file of the contents of the Lorikeet folder. This can be done eas-ily in Windows by selecting all the contents of the folder name and choosing Send to >Compressed (zipped) folder, as shown in figure 18.1.

Figure 18.1 Creating a zip file of the contents of the Lorikeet folder. Make sure you create a zip folder of the contents of the Lorikeet folder, rather than of the Lorikeet folder itself.

Next, name the zip file package.nw, rather than a name followed by .zip. You shouldsee a dialog asking if you want to do this, warning that the file may become unusable.Click Yes to the dialog shown in figure 18.2.

294

CHAPTER 18 Packaging the application for the wider world

Figure 18.2 Renaming the zip file to package.nw so the app can be packaged right for the Windows executable.

You now need to combine package.nw with the NW.exe file. Assuming you have aglobally installed copy of NW.js sitting on your computer (via having run npm install-g nw), copy the package.nw file to the same location as the nw.exe file (mine is shownhere):

C:\Users\paulb_000\AppData\Roaming\npm\node_modules\nw\nwjs\nw.exe

Copy the package.nw app to the same folder as the nw.exe file, and then run the fol-lowing command to generate the exe file:

copy /b nw.exe+package.nw lorikeet.exe

This should generate a standalone lorikeet.exe file that you could put on anotherWindows machine and run right off the bat. That's all it takes to make an NW.js appinto a Windows executable file.

The next section looks at how to create a Windows executable for an Electron app.

18.1.4 Creating an Electron app executable for Windows

Electron follows a similar pattern for creating standalone executable versions of anapp for Windows. The first thing to do is get ahold of the source code for an Electronapp. You can take an example app from this repository on GitHub: https://github.com/paulbjensen/cross-platform-desktop-applications.

Grab the Hello World Electron app from chapter 1, and you'll turn that into a stand-alone .exe file. After you've grabbed the source code for the app, you'll install a utilitylibrary for Electron called asar. Asar is a tool for packaging your app into an asararchive, which resolves the following issues:

 It makes sure that long file paths are shortened so you don't run into issues with

Windows' 256-character limit on file paths.

 It speeds up Node.js's require function a bit. It doesn't expose all your files in the app to anyone who wants to poke around

in the source code.

Creating executables for your app

295

First, install asar via npm on the command line:

npm install –g asar

Now, you'll be able to turn your app's source code into an asar archive. As an example,you'll take the Hello World Electron app's source code and turn it into an asararchive. cd the folder containing the app's folder, and then run the asar archive com-mand in the Command Prompt/Terminal:

cd cross-platform-desktop-applications/chapter-01asar pack hello-world-electron app.asar

The second command listed will generate an app.asar file that's an asar archive con-sisting of the contents of the hello-world-electron directory. After this, you'll combinethe app.asar file with the Electron app.

Grab a copy of the prebuilt binary for Electron from the GitHub repository forElectron from https://github.com/electron/electron/releases. Download a copy thatcorresponds to the OS and CPU version, which in the case of this example is v1.4.15-win32-x64.zip, available at http://mng.bz/yH23.

Unzip the file, and you should have a folder named electron-v1.4.15-win32-x64.The folder will contain another folder called resources. Put the app.asar file inside theresources folder. Then, you can change directory into the parent folder and double-clickthe electron.exe file to run the app. You should then see something like figure 18.3.

Figure 18.3 The Hello World app running as a standalone executable. Note that the Windows app doesn't have the default menu toolbar that shows when the app is running from the Electron command line, and the Electron icon shows in the taskbar.

296

CHAPTER 18 Packaging the application for the wider world

This is good, but you'll probably want to rename the electron.exe file to one thatmatches your app name (for example, hello-world.exe) and change the app icon. Tochange the app icon, you can use a tool called rcedit (a command-line resource edi-tor). Install rcedit via the command line with npm:

npm install –g rcedit

You can now edit the icon and version numbers for the app. Provided you have an appicon available in .ico format, you can run the following command on your command-line prompt to change the app icon used on the electron.exe file:

rcedit electron.exe --set-icon「my-app-icon.ico」

Using rcedit, you can then give the app its own unique look and feel.

ARE THERE ANY OTHER PACKAGING TOOLS THAT CAN HELP? Yes, there's a goodtool for Electron called electron-packager that you can install via npm. Itallows you to create builds of your Electron app for Windows, Mac OS, andLinux. It's similar to NW.js's nw-builder library, and details of its full API andcapabilities can be found at www.npmjs.com/package/electron-packager.

This covers setting up a standalone executable app on Windows, but what if you wantto create a setup installer for your Windows app? Well, good news—you can. The nextsection walks through how to do that.

18.2 Creating a setup installer for your Windows app

Although standalone executables for Windows run fine, most users of Windowsapps are used to installing them via setup installers. Setup installers take care of put-ting the app and its contents in the right places on the user's computer, as well asmaking sure that Desktop and Start menu shortcuts are installed for the app. Setupinstallers work by double-clicking the setup.exe file and clicking through the setupinstaller to make sure the app is installed in the right place and with the right userpermissions.

What are the options for NW.js and Electron?

18.2.1 Creating a Windows setup installer with NW.js

Creating a Windows setup installer for a standalone NW.js app is a little bit of a dance,but the good news is that it is possible. Here are the various options that exist for cre-ating a Windows setup installer:

 NSIS from Nullsoft Inno Setup WinRAR

Creating a setup installer for your Windows app

297

I'll show you how to create a Windows installer with Inno Setup. I've found it to workabsolutely fine, and it's not too difficult to use. The software tool is available at www.jrsoftware.org/isinfo.php. Visit the website and download a copy to run on Windows.

Once you've installed Inno Setup on your Windows computer, you can begin theprocess of creating a Windows installer for your app. Run Inno Setup on your com-puter. You should see a screen like figure 18.4.

Figure 18.4 Inno Setup's initial screen

In Inno Setup's Welcome dialog box, the New File section shows two options:

 Create a new empty script file Create a new script file using the Script Wizard

For new users, the second option is best. Select the second option and click OK. Youshould see the Inno Setup Script Wizard dialog, as shown in figure 18.5.

Click Next to proceed to the Application Information screen. Here, you'll provideinformation about the app such as its name, version number, the app publisher'sname, and the app's website, as shown in figure 18.6.

298

CHAPTER 18 Packaging the application for the wider world

Figure 18.5 The Inno Setup Script Wizard

Figure 18.6 The Application Information screen in the Script Wizard

Creating a setup installer for your Windows app

299

Fill in your app's information, and click Next to proceed with the Application Folderscreen. Here, you'll configure what the app's folder is named and where it will beinstalled on the user's computer by default (usually in the Program Files folder in theC: drive). You should see a screen like figure 18.7.

Figure 18.7 The Application Folder options screen in the Setup Wizard

I've decided to use the Windows version of the Lorikeet app, so I'll name the folderLorikeet. You can also configure whether the app needs a folder in the Program Filesfolder, as well as whether the user will be allowed to change the name of the folderwhen installing the app.

Once you've provided the name of the app folder you want, click Next to pro-ceed to the next screen, which in this case is the Application Files screen shown infigure 18.8. Here is where you provide the files that make up your built NW.js app,so the Setup Wizard will be able to compile those into the setup.exe file created byInno Setup.

The dialog in figure 18.8 shows a few options: The app's main executable file Whether the user should be offered the chance to run the app immediately

after they have installed it

 Whether to include other files and folders to be installed in the setup installer

300

CHAPTER 18 Packaging the application for the wider world

Figure 18.8 The Application Files screen in the Setup Wizard

The first and third options are the most important because this is where you add thefiles/folders of your NW.js's Windows app. If you built the Windows app as a singleexecutable, you can select that .exe file for including in the setup installer. But ifyou've built your Windows app with nw-builder and you find that there are multiplefiles to go with the Windows app, then you can include those by adding the folder thatcontains all those files.

Once you've added the app's main file (and any other additional files), click Nextto move on to the next screen in the Setup Wizard, the Application Shortcuts screen,shown in figure 18.9.

The Application Shortcuts screen shows configurations options for the icon short-cuts being placed in various places on the user's computer, such as the Start Menu, theDesktop, and even in the Quick Launch bar on older computers.

The default options specified here are fine (though you're welcome to adjust themas you like for your app). Once you've made your choices, click Next to move on tothe next screen. The Wizard presents the configuration options for displaying licens-ing information to the user as they install the app. Figure 18.10 shows the options.

You don't necessarily have to provide anything here, but it's recommended thatyou include software licensing information in your app. Here is where you can pro-vide licensing information for the user to agree to before they can use the software, aswell as release notes and other information to display before the software getsinstalled (and after).

Creating a setup installer for your Windows app

301

Figure 18.9 The Application Shortcuts screen in the Setup Wizard

Figure 18.10 Application Documentation configurations in the Script Wizard

302

CHAPTER 18 Packaging the application for the wider world

If you're happy to proceed, click Next to see options for the languages you want thesetup installer to support in the next screen, as shown in figure 18.11.

Figure 18.11 The Setup Languages screen in the Script Wizard

When you're happy with your language options, click Next to see the Compiler Set-tings screen, shown in figure 18.12. There you can configure the following:

 Where the setup.exe file will be output to What the filename of the setup installer will be What icon the setup installer should have (if any) Whether the setup installer should require the user to input a password before

the installer will install software.

When you've filled in this screen, click Next again and click through to the end of theScript Wizard as shown in figure 18.13, where you can compile the script and createthe setup installer executable.

With the setup installer created, you can distribute that file to users who want to

install your NW.js app via a Windows installer executable.

COULD I USE THE SAME TECHNIQUE FOR ELECTRON .EXE APPS? Yes. There's noreason you can't use Inno Setup 5 for creating a Windows installer for anElectron app. That said, Electron has a lot of packaging tools that enable youto use some of Electron's more advanced features, such as being able to auto-matically update apps through Electron's Squirrel framework.

Creating a setup installer for your Windows app

303

Figure 18.12 The Compiler Settings screen in the Script Wizard

Figure 18.13 The last screen you should see when you finish with the Script Wizard

304

CHAPTER 18 Packaging the application for the wider world

This pretty much covers how to set up a Windows setup installer for an NW.js app. ForElectron, there is a different, though simpler, process, covered in the next section.

18.2.2 Creating a Windows setup installer with Electron

Electron offers a number of ways to create a Windows setup installer for your Electronapp. A quick search on Google will return a number of approaches and libraries toinstall. Here are some libraries available to help build a Windows installer:

 Grunt-Electron-Installer Electron-installer-squirrel-windows electron-packager electron-builder

I'll cover using one of them, the npm module electron-builder. It not only takes careof building your Electron app for multiple platforms, it also handles some platform-specific issues:

 Packaging your app to support applying app updates Being able to sign the code as a security measure for Mac and Windows app

stores

 Managing versioned builds of the app Compiling native modules for each OS platform

To install electron-builder, run the following command in the Command Prompt/Terminal:

npm install -g electron-builder

This will install electron-builder on your computer as a global npm module. Now, let'swalk through an example of using it to help you generate a Windows installer for anElectron app.

First, grab a copy of the Hello World Electron app from GitHub:

git clone https://github.com/paulbjensen/book-examples.gitcd book-examples/chapter-18/hello-world-electron

The Electron app is going to be packaged with electron-builder so you can create aversion of the app that has a Windows installer.

electron-builder relies on build configuration information being present in theapp's package.json file, like how NW.js and Electron look for their configuration infor-mation in that file. electron-builder requires that the following fields are present inthe package.json file:

 Name Description Version Author

Creating a setup installer for your Windows app

305

Here's an example of what those fields should look like:

{ "name": "hello-world", "description":"A hello world Electron application", "version": "1.0.0", "author" : "Paul Jensen <paul@anephenix.com>"}

In the Hello World Electron app's package.json file, the description and author fieldsare not present. Add those to the package.json file (and amend as you'd like). Thenext step is to add some more build configuration information to the package.jsonfile about the Windows icon to be used.

When specifying the Windows .ico file for the app, you need to provide a public URL

to access the file, rather than a local file. You can put the file in a number of places:

 As a file that's served from Amazon S3 As a file that's served from a Dropbox folder As a file that exists in a public GitHub repository

Wherever you choose to host that file, make sure anyone can reach it (test in a webbrowser running in private/incognito mode). Here's a URL for a .ico file that you can usefor this walkthrough: https://github.com/paulbjensen/lorikeet/raw/master/icon.ico.

In the package.json file for the app, insert the following code:

{ "build": { "iconUrl":" https://github.com/paulbjensen/lorikeet/raw/master/icon.ico" }}

Make sure that a copy of that icon file is present inside a build folder in the app. Afterdoing that, add these script commands to the package.json file:

"scripts": { "pack": "build", "dist": "build"}

These script commands can be run using npm run on the command line. Finally, youneed to ensure that Electron is installed as a development dependency. You can dothat by running the following command:

npm i electron –save-dev

If you were to run npm run pack at the command-line prompt, you'd see that the appexecutables are packaged in the newly created dist folder. When you browse the distfolder, you'll see that the Electron app has been turned into .exe files for differentprocessor architectures (ia32 and x86-64).

306

CHAPTER 18 Packaging the application for the wider world

At this point, electron-builder then wraps another npm module that handlesbuilding the Electron app as a Windows installer. This is a module called electron-windows-installer, with documentation here: https://github.com/electronjs/windows-installer#usage.

If you rename the name field of the package.json file to hello and run npm run dist,

electron-builder creates the following Windows-based installer items for the app:

 A nupkg file for installing the app via the NuGet package manager A .exe file A Microsoft Setup Installer (.msi) file named setup.msi

With these files, you can install the app on other computers via a single file.

That covers creating a Windows setup installer for Electron. Now, we'll look at

options for creating both executable versions of the app for Mac OS.

18.3 Creating an NW.js app executable for Mac OS

You have a few options for how to proceed, but by far the simplest is to use nw-builderto create the executable, and for another npm module called appdmg to wrap thatexecutable as a .dmg file for ease of installation on Macs.

I'll show you how nw-builder works first, and then how to turn the executable app

into a .dmg file with appdmg.

18.3.1 Creating the Mac executable app

nw-builder is a tool for creating different executables of your NW.js app for differentOSs. If you haven't got it installed already, run the following command on your com-mand line:

npm install –g nw-builder

Now, you can use nw-builder to build a Mac executable app. Find an NW.js app thatyou want to build an executable copy of, and you'll create an executable for it. I'llresort to building a copy of the Lorikeet app that you created earlier in the book.

Once you've checked out a copy of the app, you can use nw-builder with it by pass-ing a series of arguments to the command-line command. Let's say you've checkedout a copy of the Lorikeet app's source code on your computer. cd into the app folder,and then run the following commands to generate the app's Mac OS executable:

nwbuild lorikeet-nwjs –p osx64

The first command goes to the directory where Lorikeet's source code is, and the sec-ond handles building the app for the 64-bit version of Mac OS. When the commandhas finished, you should have a new build folder. Inside the build folder is anotherfolder named lorikeet, and inside that folder is the 64-bit build, which contains anexecutable of the app.

Creating an NW.js app executable for Mac OS

307

The next step is to turn these executable builds of the app into .dmg files, whichare visual installers that make installing Apple Mac software easy. This is where theappdmg module comes in handy.

To install appdmg, run the following command in the Terminal:

npm install –g appdmg

Running that command installs the appdmg module as a global npm module. Thismeans you can use it to create .dmg files for all the Mac OS builds across all of yourNW.js and Electron apps.

To use appdmg, pass two arguments to the command line, like so:

appdmg <json-path> <dmg-path>

Here, the first argument passed to the appdmg command is a path to a JSON file con-taining configuration information for appdmg. The second argument passed is thepath where you want the created .dmg to be placed.

The JSON file contains configuration information for appdmg, and you can give itany filename. I've given it the name app.json. An example of the app.json that youmight want to use for the Lorikeet app is shown in the following listing.

Listing 18.1 The app.json file for the appdmg image creator

Size oficons insetupinstallerwindows

Title to display in {window "title": "Lorikeet",   "icon": "icon.icns",    "background": "background.png",      "icon-size": 80,       "contents": [               { "x": 448, "y": 220, "type": "link", "path": "/Applications" }, { "x": 192, "y": 220, "type": "file", "path":"build/lorikeet/osx64/lorikeet.app" } ]

Relative path to icon to display when mounting app

Background to display in setup installer window

Files to be displayed insetup installer window

}

When you have this configuration set up in the app.json file, you can run the appdmgcommand on your Mac OS computer, like so:

appdmg app.json ~/Desktop/lorikeet.dmg

When you run this command, the output .dmg file will be placed in your Desktopfolder and therefore it will be visible on your desktop screen. The Terminal outputshould look something like figure 18.14.

When the process has finished and you have a .dmg file on your desktop, double-

click to open it, and something like figure 18.15 should appear.

308

CHAPTER 18 Packaging the application for the wider world

Figure 18.14 Running appdmg on Mac OS. If all goes well, you can expect to see an itemized breakdown of the tasks being performed to create the .dmg file, and they should all be green.

Figure 18.15 The .dmg file in action, showing the app installer

In figure 18.15, you'll see the .dmg file's app installer window, where the user can dragand drop the Lorikeet app into the Applications folder to install it on their computer. This covers how to create a standalone NW.js app for Mac OS and package it as a.dmg for users to easily install on their computer. The next section shows how to dothe same for Electron apps.

Creating an NW.js app executable for Mac OS

309

18.3.2 Creating an Electron app executable for Mac OS

Electron offers a number of npm modules that can take care of creating the appexecutable on Mac OS, including electron-builder, mentioned earlier. You'll use theelectron-builder module because it provides a good UX for creating packaged appbuilds of Electron apps.

First, grab the Electron Hello World app to create a Mac .dmg for. When you havea copy of the source code for the app checked out, cd into the directory containingthe app and run this command on the Terminal to install electron-builder as a devel-opment dependency:

npm i electron-builder –-save-dev

Once you've installed electron-builder as a development dependency for the app,take a look at the app's package.json file and make sure it has the following requiredfields:

 Name Version Author Description

Once you've got those fields populated in the package.json file, the next thing to do isadd the build configuration to the package.json file, as in the next listing.

Listing 18.2 Adding the build configuration information to the package.json file

{ "name": "hello-world", "version": "0.0.1", "main": "main.js", "description":"A hello world application for Electron", "author": "Paul Jensen <paul@anephenix.com>", "scripts": {          "pack": "node_modules/.bin/build", "dist": "node_modules/.bin/build" }, "build": {        "mac": {  "title": "Hello World",  "icon": "icon.icns",  "background": "background.png",  "icon-size": 80,  "contents": [  {   "x": 448,   "y": 220,   "type": "link",   "path": "/Applications"  },

Include build configuration info here

Adds some scripts for handling creation of .app and .dmg files

310

CHAPTER 18 Packaging the application for the wider world

{   "x": 192,   "y": 220,   "type": "file",   "path": "dist/hello-world-darwin-x64/hello-world.app"  }  ] } }, "devDependencies": { "electron-builder": "^13.5.0", "electron ": "1.4.15" }}

If you take a close look at the package.json file, you'll notice that the build propertylooks remarkably similar to the configuration used for creating the .dmg file for theNW.js app with appdmg. This is because electron-builder uses appdmg under thehood and passes the configuration to that library here, instead of through a separateJSON file.

Once you have the script in place, you want to make sure you have the following

image assets in place for the app:

 An icon.icns file for the app's icon A background.png image to be displayed in the background of the app installer

When you have both of those items in the app's source code, you can run the npmcommands that will generate the .app and .dmg files. In the Terminal, run the follow-ing commands:

npm run pack && npm run dist

This code uses the Unix && operator to run two commands in sequential order. Oncethe first command (npm run pack) has finished, it triggers the second command (npmrun dist). npm run pack will create the .app file that contains all the app's source codeas a standalone executable, and npm run dist does the following:

 Creates the .dmg file for users to install the app on their computer Creates a mac.zip file for supporting automatic updates via Squirrel

The first file is the one you want to offer to new users to install your app. The zip file isthe one for existing users of your app and is the package that's used to provide themwith automatic updates. When you run the .dmg file, you can expect to see a resultlike the one shown in figure 18.16.

This shows how you can create setup installers for Mac OS using a variety of tools.The key thing to take away from this is that appdmg is a great tool for handling thecreation of .dmg files, but when it comes to creating those .dmg files for Electron

Creating executable apps for Linux

311

Figure 18.16 The .dmg installer for the Hello World Electron app

apps, you're better off using the electron-builder npm module, because it takes careof a lot more things.

The next section shows how to create standalone executables for Linux.

18.4 Creating executable apps for Linux

When it comes to creating executable apps for Linux, bear in mind that there aremultiple distributions of Linux, some of which are quite common and popular (LinuxMint, Ubuntu, Fedora, and openSUSE come to mind), and some of which are smaller,more niche distributions. To install software for Linux distributions, there are a num-ber of different software package management tools:

 Yum (used by Red Hat, Fedora, CentOS) YaST (used by OpenSUSE) Synaptic (used by Ubuntu, Linux Mint)

You can always serve your software as a tarball and let Linux users run make and makeinstall on their computer, but not all Linux users will know how to do that, andLinux is making inroads into all kinds of areas, including education and local govern-ment. In order to best support your Linux users, do the following:

 Identify what Linux distributions are supported by your app framework Find out (if you can) what Linux OSs your customers are using If you can't identify that, find out what the most popular Linux OSs are and

support those

312

CHAPTER 18 Packaging the application for the wider world

18.4.1 Creating NW.js standalone apps for Linux

One of the options available to you for NW.js is to use nw-builder, which has been usedearlier in the book. If you haven't already, you can install nw-builder by running thefollowing command:

npm install –g nw-builder

Next, you need an app to convert into a Linux standalone executable and run nw-builder on with configuration details specific to Linux. In the chapter so far, we'veused the Lorikeet app, but to add some variety, you'll use one of the other apps thatyou worked on earlier in the book, a WYSIWYG app called Cirrus.

Grab a copy from GitHub at https://github.com/paulbjensen/cirrus/archive/master.zip. Once you've downloaded the zip file and extracted the contents into a folder, cdinto the folder and run the following command to install software dependencies:

npm install

Now, you can build the Linux standalone executables with nw-builder. Run the follow-ing command in the Terminal to build both 32-bit and 64-bit versions of app for Linux:

nwbuild cirrus –p linux32,linux64

This will create two builds of the app for Linux—one for 32-bit architecture, andanother for 64-bit architecture. When nw-builder finishes building the packages, you'llfind a build folder. The build folder contains another folder with the name of the soft-ware (Cirrus, in this case), and inside that are two folders: linux32 and linux64. Theseare the folders for the different builds of the app that you specified earlier.

As the app stands, you could take the files produced from the build and run them

on Linux, as shown in figure 18.17.

The software at this point is a collection of these files: Cirrus (a binary executable that takes the name of the app) icudtl.dat (a binary data file for NW.js) libffmpegsumo.so (a file used by Chromium for multimedia support) locales folder (a folder containing files for localization info for different

countries)

 nw.pak (a file for NW.js)

When you want to bundle these files into packages for RPM, Yum, Apt, and dpkg,you'll want to include all of them and make the binary executable named after yourapp the main executable.

This covers what to do for an NW.js project. How about for Electron?

Creating executable apps for Linux

313

Figure 18.17 Cirrus running on Ubuntu Linux 14.04 LTS. Cirrus is running in the foreground, and in the background are the files that make up the app. You may also notice the app icon in the bottom-left corner.

18.4.2 Creating Electron standalone apps for Linux

Electron has a number of tools available for building an Electron app as a standaloneLinux executable:

 Grunt-build-atom-shell (grunt plugin: https://github.com/paulcbetts/grunt-

build-atom-shell)

 electron-packager (npm module: www.npmjs.com/package/electron-packager) electron-builder (npm module: https://github.com/electron-userland/electron-

builder)

You used electron-builder for the Mac OS and Windows builds earlier in the chapter,so this time you'll take electron-packager for a spin instead. electron-packager is inthe Electron-userland organization on GitHub, and is maintained by a number ofmajor contributors within Electron's community.

You'll start by installing electron-packager on your computer as a global dependency:

npm install –g electron-packager

314

CHAPTER 18 Packaging the application for the wider world

cd into the directory where the app's source code is (in this case, you'll use the HelloWorld Electron app as an example), and then run the electron-packager command:

cd hello-world-electronelectron-packager FULL_PATH_TO/hello-world-electron --name=hello-world --platform=linux --arch=x64 --version=1.4.15

This will take the source in the hello-world-electron directory, turn it into an Electronapp called hello-world with Electron version 1.4.15, and build that app for Linux onthe 64-bit x86 architecture.

After running that command, you should have a new folder called hello-world-

linux-x64. Inside that folder will be the following set of files:

 content_shell.pak (a file for Electron) hello-world (a binary executable that takes the name of the app) icudtl.dat (a binary data file for Electron) libffmpeg.so (a file used by Chromium for multimedia support) libnode.so (a file for Electron) LICENSE (a text file containing license information for the software) LICENSES.chromium.html (an HTML file containing license informationabout the software used in Chromium, the open source version of Chrome thatElectron uses)

 locales folder (a folder containing files for localization info for different

countries)

 natives_blob.bin (a file for Electron) resources folder (a folder containing the app's source code) snapshot_blob.bin (a file for Electron) version (a text file containing the software version

When you run the app and its files on a Linux machine (say, a machine runningUbuntu 14.04), you'll see something like figure 18.18.

This shows you how you can use electron-packager to package an Electron app as astandalone Linux executable. The ability to do this for both NW.js and Electronmeans you have the flexibility to choose which desktop app framework you want touse for the app. That said, do bear in mind one major caveat when choosing Electronwith regard to Windows support: if you need to support Windows XP (which still has astatistically significant customer base in China), then Electron isn't supported.

Summary

315

Figure 18.18 The Hello World Electron app as a standalone app on Ubuntu

18.5 Summary

In this chapter, we've looked at the different ways in which you can build your NW.jsand Electron apps for the different OSs out there.

Consider which OSs your customers are likely to use so you can spend your timeworking on supporting the platforms that need to be supported. Being able to buildWindows and Mac OS executables for the app with tools like nw-builder, electron-builder, and electron-packager ensures that you can reduce the amount of time spentpackaging the app—and spend more time creating features for your app.

You also explored how to create setup installers for the executables of your app sothat users of your app can install them with ease. You'll find that Inno Setup 5 is agreat tool for creating setup installers and is easy to use, so that will help you with cre-ating setup installers for your Windows apps.

As for Mac OS, appdmg is the tool of choice for creating .dmg files for your Mac


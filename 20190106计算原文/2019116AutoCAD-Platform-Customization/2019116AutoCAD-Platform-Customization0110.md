# 0110. Using, Loading, and Managing Custom Files

Throughout this book, I discuss how to define a set of CAD standards that can be applied to all your drawings so they have a consistent look. I show you how to customize the Autodesk® AutoCAD® program on systems running on Windows and Mac OS. Being able to customize the files for AutoCAD on your local workstation is a great start, but in the end you want to make sure that you can deploy or share any customized files with others in your company.

Customizing AutoCAD, as you have read and seen thus far in this book, is a great way to increase your productivity, but you can also download custom programs from the Internet or the Autodesk Exchange store to introduce new functionality and commands. You can also create your own custom programs that improve your company's workflows, but doing so is beyond the scope of this book.

After you spend the time to customize AutoCAD, you will want to make sure you back up your files. How you back up your custom files will vary based on if you are on Windows or Mac OS. Last but not least, recent releases of AutoCAD provide a few utilities that allow you to migrate your customized files to a newer release.

Deploying Your Custom Files

Now that you have taken the time to learn how to customize AutoCAD, you probably can't wait to share what you have learned with others to increase their productivity. Before you start passing files around to everyone in your company, you might want to take a step back and formulate a long-term plan for maintaining any customized files.

Consider the following:

Where will you store and maintain your customized files? The answer to this question will be based on how your environment is configured. Chances are you have a network available to you that most users in your company can access, but you can also use a local drive or a cloud-based file service to share customized files.

Who needs access to your customized files? Usually, customized files are shared within a company, but you might also want to consider sharing your customized files with your subcontractors. This can make it easier to share project files and even complete projects faster. When sharing customized files, consider marking them read-only to avoid accidental changes to the files. Placing files on a network for those in your company is the ideal solution, because that makes the files more secure and easier to manage. But for those outside your company, a cloud-based file service or an FTP site might be the best choice.

How often do you plan on making changes? The method used to host customized files can impact how many updates you might make on a daily, weekly, or monthly basis. No matter how large or small the changes, you want to create a log of the changes so you can identify any errors that are encountered. This approach also gives your users an idea of what functionality is available to them over time.

Organizing Your Customized Files

As I have mentioned throughout this book, I recommend creating your own or creating a copy of a customizable file over directly modifying the files that come with AutoCAD. Then, once the files are customized, you should place those files in their own location. In the exercises and samples in this book, we used the MyCustomFolders folder under the Documents (or My Documents) folder. This approach has these advantages:

It lowers the risk of losing your customization during a reset or reinstall of AutoCAD.

Sharing of customized files is made easier. You can add the folders in which AutoCAD can locate your files as part of the Support File Search Path node in the Options (Windows) or Application Preferences (Mac OS) dialog box.

Upgrading to a newer release is streamlined, since you know exactly where your customized files reside.

Backing up customized files is simplified, because you know which files have been customized and where those files reside.

Where to Place Customized Files

I recommend placing all the customized and support files you want to share with others in your organization in a common and shared location instead of manually copying files between workstations. Manually copying files takes extra time and planning that might not be necessary when changes are made to the files. If you place the files on the network, you just need to copy any changed files to a single location, and AutoCAD will load them as long as you have identified the location of the customized files using the Options (Windows) or Application Preferences (Mac OS) dialog box.

No matter whether you store your files on a network or local drive, I recommend defining a folder structure that allows you to use or organize your files by type instead of just placing them all in a single folder. The following is a sample folder structure I have used for my customized files and the environments I have configured for other companies:

<company_name> <release> Blocks Plotting PC3 Plot Styles Support Actions Custom Programs Icons Palettes Templates

The value <company_name> in the sample folder structure represents your company's name to help ensure your files are separate from those that come with AutoCAD or even other third-party utilities that might be installed. The value <release> represents the AutoCAD release you have installed. If you have more than one release installed, you will want to have a folder structure for each release to avoid potential conflicts between older and newer releases. Customizable files are commonly designed to be forward compatible, but they are not always backward compatible.

Where you create your folder structure depends on the storage option you choose for your customized files. Here are some suggestions based on various storage options:

Network Drive Map a drive letter to the root of the folder structure. This helps ensure that you don't create long folder paths that will cause problems when AutoCAD tries to access the files.

Cloud-Based File-Sharing Service Use the location in which the cloud-based file-sharing service stores local copies of the files that are synchronized from the remote server. For example, Microsoft SkyDrive synchronizes files locally to the SkyDrive folder and Dropbox uses the Dropbox folder. Both of these folders are located under your user profile.

Removable Drive Create a folder for the customized files on the removable drive at the root level.

Local Drive Create a folder for the customized files on the local drive at the root level, the ProgramData folder on Windows, or the Library folder on Mac OS.

NOTE

Although you could use a folder that is part of a user's Roaming profile for your company's custom files, I recommend not doing that. It requires the user to be logged in to receive any updated files, and it creates duplications of the files under each user's profile. In addition, the files that make up a user's profile should be only the ones that they create or manage themselves.

Maintaining Files Offline

In a perfect world, your customized files would never need to be updated and would only need to be accessible from the company's network. However, Internet connections are not available everywhere and not all connections are fast, stable, or secure. Instead of hoping for an Internet connection, you will want to plan ahead and ensure that remote users have access to the files they need.

For individuals working from home or on a laptop in the field, local access to the most recent files is critical. The same advantages still apply about having your customized files separated from those that come with AutoCAD, but you need to take an extra step to ensure the user has the latest files. You could use any of the following techniques based on your skill level to maintain a local copy of the customized files that might normally be posted on the network:

Copying files manually is a low-cost way of getting your files from a network to a local drive. However, it does require someone to remember to do it before they log out and hit the road.

Using a cloud-based file-sharing service can be a nice and easy-to-set-up solution for taking customized files offline with you. File-sharing platforms like Dropbox, SkyDrive, Google Drive, and others allow you to create a company account and grant read-only access to the files. Since many of the cloud-based services are available on both Windows and Mac OS, they can be useful in mixed environments.

Creating a batch or shell script that is executed at startup or as part of a Group Policy can be ideal and gives you the most control over where the files are placed and when the synchronization takes place.

There are additional options that are specific to a given operating system, so feel free to experiment and use the solutions that might work best for you to keep your users' local files in sync with those on the network. I have used Robocopy, Offline Files, and Task Scheduler on Windows in the past. You can use rsync or FileSync on Mac OS. These days, I tend to lean toward cloud-based approaches, so I have my customized files available on both my Windows and Mac OS workstations with very little effort.

Customizing the Folders Used by AutoCAD

The folders that AutoCAD looks in for its support files and your customized files are defined as part of the current AutoCAD profile. You can modify the current user profile or create a new one by using the options command. AutoCAD doesn't search the subfolders of the folders that are listed as part of the current user profile. Each folder that contains custom program files you want AutoCAD to use must be listed as part of a user profile. I explain managing user profiles in Chapter 4,「Manipulating the Drawing Environment.」

NOTE

New user profiles can be created only in AutoCAD on Windows.

Based on the locations in which your customized files are stored, you might need to add the folders under the following nodes of the Files tab in the Options dialog box (Windows) or the Application tab in the Application Preferences dialog box (Mac OS). For information about other nodes on the Files or Application tab, see the AutoCAD Help system.

NOTE

While you can change the paths listed in the current user profile, be careful. Do not remove the folders that contain the AutoCAD core application and support files. Unexpected results might occur if those folders are removed.

Support File Search Path The Support File Search Path node contains the folders that AutoCAD looks in for its own support files and most of your customized files. Here are some of the file types that should be listed in the folders under this node: AutoLISP® (LSP/FAS/VLX)

Blocks (DWG)

Compiled shapes (SHX)

Hatch patterns (PAT)

Linetype definitions (LIN)

Managed.NET (DLL) (Windows only)

ObjectARX® (ARX/CRX/BUNDLE)

ObjectDBX™ (DBX)

Program parameter (PGP)

Scripts (SCR)












VBA projects (DVB) (Windows only)(Windows only)

Trusted Locations The Trusted Locations node contains the folders of the custom programs that AutoCAD should trust. For files loaded from these locations, AutoCAD does not display a security warning message. I discuss loading custom program files later, in the「Loading a Custom Program」section.

Customization Files The Customization Files node contains the folders where the CUIx or CUI files that define many of the tools in the user interface are stored. You can also define the location that AutoCAD looks in for icons used by your custom tools in the user interface. I discussed customizing the AutoCAD user interface in Chapter 5,「Customizing the AutoCAD User Interface for Windows,」and Chapter 6,「Customizing the AutoCAD User Interface for Mac.」

Printer Support File Path The Printer Support File Path node contains the folders where the printer configuration (PC3/PCM), printer description (PMP), and plot style (CTB/STB) files are stored. I discussed printer configuration and plot styles in Chapter 1,「Establishing the Foundation for Drawing Standards.」

Template Settings The Template Settings node contains the folders where the drawing (DWT) and sheet set/project (DST) template files are stored. I discussed drawing templates in Chapter 1.

Tool Palettes File Locations (Windows Only) The Tool Palettes File Locations node contains the folders where the tool palette (ATC) files are stored for the Tool Palettes window. I discussed tool palettes and the Tool Palettes window in Chapter 7,「Creating Tools and Tool Palettes.」

Action Recorder Settings (Windows Only) The Action Recorder Settings node contains the folders where action macro (ACTM) files that AutoCAD can edit and play back are stored. I discussed action macros and the Action Recorder in Chapter 8,「Automating Repetitive Tasks.」

The following steps explain how to add the MyCustomFiles folder to the Support File Search Path node in the Options dialog box on Windows. This folder is the expected location for the files created as a result of completing the exercises in this book.

Click the Application menu button Options (or at the command prompt, type options and press Enter).

When the Options dialog box opens, click the Files tab.

Select the Support File Search Path node and click Add, and then click Browse.

In the Browse For Folder dialog box, browse to the MyCustomFiles folder that you created for this book in the Documents (or My Documents) folder, or browse to the folder that contains your customized files.

Select the folder that contains your customized files and click OK.

Click OK to save the changes to the Options dialog box.

If you are using AutoCAD on Mac OS, use these steps:

On the menu bar, click AutoCAD <release> Preferences (or at the command prompt, type options and press Enter).

When the Application Preferences dialog box opens, click the Application tab.

Select the Support File Search Path node.

Near the bottom of the dialog box, click the plus sign (+).

In the Open dialog box, browse to the MyCustomFiles folder that you created for this book in the Documents folder, or browse to the folder that contains your customized files.

Select the folder that contains your customized files and click Open.

Click OK to save the changes to the Application Preferences dialog box.

You can change an existing folder in the Options or Application Preferences dialog box by expanding a node and then selecting the node you want to edit. After selecting the folder to edit, click Browse on Windows and select the new folder, or double-click the folder on Mac OS and then select the new folder.

Using and Loading Custom Programs

Everything that I have discussed in this book until now has primarily focused on customizing AutoCAD. While customizing AutoCAD is a great way to increase your productivity, customization does have its limitations when you are trying to automate or simplify complex workflows.

Leveraging one or more of the programming languages that AutoCAD supports with the customization features that you have learned about in this book will help you further increase your productivity. You do not need to learn how to program, but you should be familiar with the programming languages available so you can take advantage of the many custom programs that are available for free (or for a small fee) on the Internet.

What Are Custom Programs?

Custom programs are applications that extend the functionality of AutoCAD through the inclusion of new commands or custom objects, or the extension of a supported programming language. The programming languages that AutoCAD supports allow for a wide range of skills, from basic to advanced. Even if you do not want to learn to be a programmer, having a basic understanding of a language can be beneficial if you download programs from the Internet. If you do decide to learn a programming language, consider AutoLISP and Visual Basic for Applications (VBA), which are fairly easy to learn with no or little previous experience. Here are the programming languages that AutoCAD supports:

AutoLISP AutoLISP is often the first programming language that a drafter or nonprogrammer learns to extend the functionality of AutoCAD. You can write an AutoLISP program using Notepad on Windows or TextEdit on Mac OS, or the Visual LISP® development environment built into the Windows release of AutoCAD. AutoLISP programs have the file extension .lsp. AutoLISP files, which can be compiled, have the file extensions .fas and .vlx. (VLX files are supported on Windows only.) You can load an AutoLISP file by using the appload command or the load AutoLISP function.

VBA (Windows Only) VBA is an extension of the Visual Basic (VB) programming language. VBA is an object-oriented programming language that uses the concept of interactive objects defined with properties, methods, and events. When creating VBA programs, you communicate with AutoCAD using the AutoCAD Object Library to create and modify objects in a drawing or the AutoCAD environment. VBA programs are stored in project files with a .dvb file extension. DVB files can be loaded and executed using the vbaman or vbarun command or with the vl-vbaload or vl-vbarun AutoLISP function.

VB.NET and C# (Windows Only) VB.NET and C# are two of the modern programming languages that AutoCAD supports. Both of these languages require the installation of the.NET Framework, as well as access to specific libraries that are installed with AutoCAD or as part of the ObjectARX software development kit (SDK). Applications created with VB.NET or C# require you to use Microsoft Visual Studio (Express is free, or you can purchase a license for Professional or higher). VB.NET and C# programs must be compiled with the .dll file extension and loaded into AutoCAD using the netload command.

JavaScript (Windows Only) JavaScript (JS), the most recent programming language that AutoCAD supports, was first introduced with AutoCAD 2014. A JS program can be either a standalone file with the .js file extension and loaded with the webload command, or part of an HTML file and displayed with the showhtmlmodalwindow AutoLISP function. You can create a JS or HTML file using Notepad or a specialized editor.

C++ and Objective-C C++ (Windows) and Objective-C (Mac OS) are two programming languages that are based on the C programming language. Both of these languages require you to download and obtain the ObjectARX SDK, which contains the libraries required to communicate with AutoCAD. An ObjectARX application must be compiled before it can be loaded into AutoCAD. If you want to develop applications with C++, you need to install Microsoft Visual Studio. (Again, Express is free, or you can purchase a license for Professional or higher.) If you are developing applications with Objective-C, you will need to install Xcode. Both languages support the development of graphical user interfaces with MFC (Windows) or Cocoa (Mac OS). ObjectARX programs must be compiled with the .arx (Windows) or .bundle (Mac OS) file extension. ARX and BUNDLE files can be loaded into AutoCAD using the appload command or with the arxload AutoLISP function.

NOTE: You can download the ObjectARX SDK (which you can use to develop a program using VB.NET, C#, C++, or Objective-C) from www.objectarx.com.

Loading a Custom Program

As I previously mentioned, AutoCAD supports a variety of programming languages and each has its own method of being loaded into AutoCAD. The most common types of custom files that you will encounter are AutoLISP (LSP) and ObjectARX (ARX/BUNDLE). Understanding how to load an LSP, ARX, or BUNDLE file allows you to take advantage of the many free routines that others have created and made available for download from the Internet over the past two decades.

Starting with AutoCAD 2013 Service Pack 1 and AutoCAD 2014, Autodesk implemented an additional layer of security that you should be aware of that restricts the loading and execution of custom programs without some user interaction. Prior to those two releases, there were no restrictions on loading and executing custom programs. The following list explains the settings and options that affect the loading and execution of custom programs in AutoCAD 2013 and AutoCAD 2014:

AutoCAD 2013 with Service Pack 1 (Windows Only) The system variables and the command-line switch that affect the loading of custom programs in AutoCAD 2013 are as follows: autoload, which specifies whether AutoCAD can automatically load custom files with specific names at startup

autoloadpath, which specifies the folders from which AutoCAD can automatically load custom files with specific names at startup

lispenabled, which indicates whether AutoLISP has been disabled in the current session

/nolisp, which disables the execution of AutoLISP (LSP/FAS/VLX) (Windows only) files in the current session

AutoCAD 2014 The system variables and command-line switches that affect the loading of custom programs in AutoCAD 2014 are as follows: secureload, which specifies whether AutoCAD can load executable files from any folder with or without a warning, or whether it can load files only from the folders specified by the trustedpaths system variable.

trustedpaths, which specifies the folders from which AutoLISP, VBA, Managed.NET, and ObjectARX files can be loaded without user interaction. VBA and Managed.NET are supported on Windows only.

trusteddomains, which specifies the domains and URLs from which JS files can be loaded without user interaction (Windows only).

safemode, which indicates whether executable files can be loaded and executed in the current session.

/safemode, which disables the execution of executable files in the current session (Windows only).

-safemode, which disables the execution of executable files in the current session (Mac OS only).

The following steps explain how to load an AutoLISP or ObjectARX application:

Do one of the following: On the ribbon, click the Manage tab Applications panel Load Application (Windows).

On the menu bar, click Tools Load Application (Mac OS).

At the command prompt, type appload and press Enter (Windows and Mac OS).

When the Load/Unload Application dialog box (see Figure 10.1) opens, browse to and select the AutoLISP or ObjectARX file you want to load. Click Load.

If the File Loading - Security Concerns message box is displayed, click Load. See the topics on the secureload and trustedpaths system variables in the AutoCAD 2014 Help system for information on how to avoid this message each time you load a custom program.

Click Close to return to the drawing area.

Execute any new command that is made available after the custom program file is loaded.

Figure 10.1 Loading a custom program

You can use the Startup Suite section of the Load/Unload Applications dialog box to automatically load custom program files each time AutoCAD starts. For information on using the Startup Suite, see the appload command in the AutoCAD Help system.

Locating Custom Programs on the Internet

Custom programs can be found on the Internet by performing a search using your favorite search engine. You can find some custom program files by doing a search on a combination of the keywords autolisp, objectarx, programs, files, sample, download, and free. An example keyword search might be autolisp files; the results in Bing are shown in Figure 10.2.

WARNING

With any files that you download from the Internet, make sure you scan the files with virus software. Also, download files from a reputable website whenever possible. If you are unsure about a website that contains free custom program files for AutoCAD, check whether someone on the Autodesk (forums.autodesk.com) or AUGI (forums.augi.com) forums has downloaded files from the website.

Figure 10.2 Internet search results on AutoLISP files

The following lists my website (HyperPics) and other reputable sites that offer free custom programs that can be used with AutoCAD:

AfraLISP: www.afralisp.net

DotSoft: www.dotsoft.com

HyperPics: www.hyperpics.com/customization/

JTB World: www.jtbworld.com

ManuSoft: www.manusoft.com

If you are using AutoCAD 2013 or AutoCAD 2014 on Windows, you can also download and install custom programs through the Autodesk Exchange App Store (http://apps.exchange.autodesk.com/). The Autodesk Exchange App Store contains a variety of apps not only for AutoCAD, but also for AutoCAD-based vertical applications and other Autodesk products. You can find both free and paid for apps in the store.

Backing Up and Migrating Customization

Backing up your custom settings and files is often one of the last tasks you perform after customizing AutoCAD, but it is also an important one if something were to go wrong. I recommend backing up frequently—that comes out of habit after forgetting to back up a few times over the years and having to redo several days of customization work. While backing up files is often one of the last tasks you perform, migrating is one of the first tasks you will perform when upgrading to a new release.

The most basic way to back up and migrate your files on either Windows or Mac OS is to manually copy your files between folders. The following lists the folders that AutoCAD uses by default to store the customized files it can make changes to:

%AppData%\Autodesk\<product_name>\<release>\<language> (Windows)

%LOCALAPPDATA%\Autodesk\<product_name>\<release>\<language> (Windows)

˜Library/Application Support/Autodesk/roaming/<product_name>/<release>/<language> (Mac OS)

˜Library/Application Support/Autodesk/local/<product_name>/<release>/<language> (Mac OS)

As I discussed earlier in this chapter, I strongly recommend storing your customization in separate folders and files from those that AutoCAD creates after installation. If you follow my recommendation, be sure to back up the folders and files in those locations in addition to the ones that AutoCAD updates.

If you are using AutoCAD on Windows, there are some additional utilities available for backing up custom settings and files, synchronizing custom settings with your Autodesk 360 account, and helping to migrate custom settings to a new release. These utilities include the following:

Export AutoCAD <release> Settings The Export AutoCAD <release> Settings option on the Windows Start menu or Start screen allows you to export the custom settings and files of AutoCAD to a ZIP file.

Import AutoCAD <release> Settings The Import AutoCAD <release> Settings option on the Windows Start menu or Start screen allows you to import the custom settings and files that were previously exported using Export AutoCAD <release> Settings.

Synchronize Custom Settings The Synchronize Custom Settings feature allows you to back up your custom settings and files to your Autodesk 360 account. These settings can then be restored on another workstation or on the same workstation they were backed up from. You can control whether you want to use this feature, and the types of settings and files that can be backed up, on the Online tab of the Options dialog box (options command).

Migrate From A Previous Release The Migrate From A Previous Release option on the Windows Start menu or Start screen allows you to migrate your custom settings and files from a previous release to a newer release. For example, you can migrate your settings from AutoCAD 2012 to AutoCAD 2014. Both releases need to be installed in order to migrate the custom settings and files.

Customize User Interface, Transfer Tab The Transfer tab of the Customize User Interface (CUI) Editor allows you to transfer user-interface elements between two different CUIx files. This can be helpful if you want to migrate only some of the elements in your user interface to a new release. I discussed the CUI Editor in Chapter 5.

For more information on these utilities, see the AutoCAD Help system.

TIP

For additional information on issues that could affect migrating custom settings and files, or using custom program files from an earlier release, see the CAD Administration Guide in the AutoCAD Help system (docs.autodesk.com/ACD/2014/ENU/).
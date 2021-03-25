Additional Resources

Hopefully by now you have a solid starting point to build and code your Electron application. We have touched on many of the core features that most desktop applications require: native menus and dialogs, platform-specific installers, integration with the local file system, and more. The challenge is taking these features and integrating them in your actual application.

Understanding that Electron is built atop two separate systems, you should be able to isolate much

of the Electron-specific code from the main process, leaving your renderer process free to your core application. As we come to the end of this book, we want to cover some of the various loose ends that we need to touch upon before you begin writing the next awesome Electron app!

Additional Electron APIs

While we introduced you to a lot of the core APIs that Electron offers, we did not cover every one. But, we would be remiss if we did not touch briefly on some of the other APIs that you should be aware of:

desktopCapturerThis API allows you to capture audio and video from the user desktop. This API is built atop the webkitGetUserMedia API. It should be noted that whenever you access media recording functions, you need to be transparent with the user about performing the recording action.

crashReporterElectron has this built-in API that will submit crash reports to a remote server. It does require some additional server configurations in order to accept the crash reports from your application.

ClientRequestThis powerful API is used to make HTTP/HTTPS requests via the main process. The actual method implements Node's Writable Stream interface. Some examples of supported streams are the following:

fs write streams

•	 HTTP request•	 HTTP responses•	•	•	•

zlib streams

crypto streams

TCP sockets

© Chris Griffith, Leif Wells 2017 C. Griffith, L. Wells, Electron: From Beginner to Pro, https://doi.org/10.1007/978-1-4842-2826-5_17

263

Chapter 17 ■ additional resourCes

netAlthough like the HTTP and HTTPs modules in Node.js, this API uses Chromium's native networking library instead. Better support for web proxies is one reason you might consider this solution instead of the Node.js modules.

DownloadItemYou can use this API to control file downloads from remote sources. This works well if you need to interact with remote files.

Electron Forge

Billed as the command-line interface for Electron applications, this project is being developed by Electron Userland. You might recognize that name, as they are the developers of the npm modules electron-packager and electron-builder.

The main idea of this project is to provide a CLI for many of the common Electron tasks, including

scaffolding a new Electron app, installing new Node modules, packaging and publishing. This is certainly an effort that we are closely following for use in our next Electron application. To learn more about this tool, visit https://beta.electronforge.io/.

Community Resources

The success of any open source project is, in part, due to the strength of the community around it. Electron is fortunate to have an active community that new and experienced developers can turn to when dealing with an issue or looking for a solution. Here is a list of some of the more popular channels that you can become a part of:

#atom-shell on Freenode (http://webchat.freenode.net/?channels=atom-shell)

Reddit (https://www.reddit.com/r/electronjs)

Stack Overflow (http://stackoverflow.com/questions/tagged/electron)

•	 Discuss (https://discuss.atom.io/c/electron)•	•	•	 @electronjs on Twitter (https://twitter.com/electronjs)•	•	•	•	•	•	 @electron_ru on Telegram (Russian) (https://telegram.me/electron_ru)•

electron-jp (Japanese) (https://electron-jp-slackin.herokuapp.com/)

#electron on Atom Slack (http://atom-slack.herokuapp.com/)

electron-br (Brazilian Portuguese) (https://electron-br.slack.com/)

electron-kr (Korean) (http://www.meetup.com/electronkr)

electronjs on Facebook (https://www.facebook.com/groups/electronjs/)

We should not forget that Electron is an open source project living and breathing on GitHub. Take the

time to look over the issues for the project, or you can even contribute to the project.

264

Chapter 17 ■ additional resourCes


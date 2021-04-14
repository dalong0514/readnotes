# 0301. Building your first desktop application

This chapter covers

 Opening files from the file explorer  Accessing the filesystem  Refactoring code using Node.js’s module functionality  Implementing search features in the desktop app

Building an app is a journey of creating an initial skeleton of the app and progressively adding to the skeleton until it begins to resemble a complete product. The moment when the product comes alive with features is often, for me, the moment I get excited, and in this chapter those moments shall arrive.

In chapter 2, you began a journey of building a file explorer called Lorikeet and got to a stage where you had the UI for a working desktop application. In this chapter, you’ll continue that journey and add features that will result in a file explorer app you can call a minimally viable product.

The goal is that not only will you have made the app’s features by the end of the chapter, but you’ll understand exactly how Electron and NW.js let you do that. The process will give you enough experience to start using those desktop app frameworks in other places as well. Chances are, your mind will open up with lots of ideas for things you can do that you didn’t know how to do before. Excited? Good! Get comfortable and settle in for round two.

3.1 Exploring the folders

The main ingredients for making this happen are now in place: the files and folders for a given path can now be displayed visually in the window. Next you need to build the functionality so that when the user double-clicks a folder in the main area, the app navigates to that folder and displays its contents in the main area.

3.1.1 Refactoring the code

If you look at the app.js file now, you’ll notice that it’s beginning to look a bit muddled, and at this point it’s worth refactoring the code so that it doesn’t become overwhelming and difficult to manage. Refactoring the file requires organizing the code into logical groups, as shown in figure 3.1.

Before

app.js

After

app.js

fileSystem.js

userInterface.js

Figure 3.1 You'll start breaking out the code into logical groups of functionality so that the code is more readable and easier to work with.

In figure 3.1, the app.js file will be turned into three files. There will still be an app.js file as the main entry point for the front-end code, but there will also be two other files. The fileSystem.js file will contain code that handles interacting with the files and folders on the user’s computer, and the userInterface.js file will hold functions that handle UI interactions. These are two distinct logical groups, and they will allow you to keep the code orderly.

Create two files in the Lorikeet folder at the same level as the app.js file: fileSystem.js and userInterface.js. In the fileSystem.js file, insert the code shown here.

The fileSystem.js file contains the getUsersHomeFolder, getFilesInFolder, inspectAndDescribeFile, and inspectAndDescribeFiles functions from the app.js file. The extra bit of code at the bottom exposes some of the functions that need to be accessed by other files through the use of the module.exports function call, a CommonJS JavaScript convention for exposing public code items in libraries. This is an important factor in the way you organize and make your code usable across multiple projects.

In the userInterface.js file, insert the code shown in the following listing.

Here, you expose the bindDocument and displayFiles functions in the code. The bindDocument function is used to pass the window.document context to the user-Interface.js file—otherwise, the file will not be able to access the DOM in the NW.js variant of the app (Electron is unaffected). The displayFiles function is used to display all the files, and because there’s no need to call the displayFile function separate from the displayFiles function, you don’t expose the displayFile function as a public API.

Now that the code that was in the app.js file has been moved into the fileSystem.js and userInterface.js files, you can replace the app.js file with the code shown here.

The app.js file is now 17 lines of code and is much more readable. Here, you can see that there are two Node.js modules included in the code (fileSystem and userInterface), and that the main function is identical to how it was in the app.js file, with the exception of calling functions from the Node.js modules instead.

The last change left is to alter the index.html file so that the function that calls the user’s personal folder is calling the fileSystem file module. Change the index.html file so that it looks like the following code.

Save the changes to the files. The refactoring is almost complete. The next feature you want to add is the ability to navigate folders by double-clicking them in the file explorer.

3.1.2 Handling double-clicks on folders

One of the common features of using a file explorer is navigating folders by doubleclicking the folder icon. You’ll add this functionality to the Lorikeet app.

When you double-click a folder, the UI of the app updates so that the following things happen:

 The current folder changes to that of the folder that’s clicked.

 The files that were displayed in the file explorer are updated to show the files for the folder path that was clicked.

 When you click another folder, the same behavior occurs again.

You also want to make sure that double-clicking a folder behaves as you expect, and that double-clicking a file opens that file in its default application. To achieve that, you’ll do the following:

 Create a function in the userInterface.js file called displayFolderPath, which will update the current folder path displayed in the UI.

 Add another function in the userInterface.js file called clearView, which will remove the files and folders that are currently displayed in the main area.

 Create a function called loadDirectory, which will handle querying the computer for the files and folders at a given folder path and then display the files and folders in the main area. This code is effectively moved out of the app.js file.

 Alter the displayFile function so that it attaches an event listener to a folder icon to trigger loading that folder.

 Change the app.js file so that it calls the loadDirectory function of the user-Interface.js file.

 Remove the script tag inside the current-folder element in the index.html file, because it’s no longer needed.

In the userInterface.js file, change the code to look like the next listing.

Next, amend the app.js file so that it calls the loadDirectory function from the user-Interface.js file. Change the app.js file to look like the following code.

One more change left to do. You can now remove the script tag from inside the currentfolder div element. Change the current-folder div element in the index.html file so that it looks like this:

```
<div id="current-folder"></div>
```

With those files changed, reload the app. Now, when you double-click an app folder, you’ll see that the folder path changes in the toolbar, and the files and folders on display in the main area change as well. An example of this is shown in Electron in figure 3.2.

Figure 3.2 The Lorikeet app in Electron after navigating to a list of files inside of a folder, three levels away from the starting folder path

And figure 3.3 shows the same result in NW.js with the same file changes.

Figure 3.3 The Lorikeet app in NW.js, navigating to a hidden folder inside of my home folder

You can see here that you’ve been able to use plain vanilla JavaScript, HTML, and CSS to implement what is beginning to feel like a real desktop app. So far so goodbut it’s not mission complete yet. You’re going to add quick search functionality to the app.

3.2 Implementing quick search

Lorikeet

Lorikeet

/Users/paulbjensen

/Users/paulbjensen

Search

Search

Desktop

Public

Desktop

Documents

Work

Documents

Downloads

Diary.doc

Downloads

Movies

elephants.jpg

Movies

Musicic

Mus

Pictures

Pictures

Figure 3.4

The quick search feature that you want to implement in the app

Figure 3.4 shows a preview of what you’ll add next: quick search functionality.

If you have a folder containing lots of files, searching through the entire list of them can be tedious. In the wireframe, the toolbar features a search field in the top right, and to implement an in-directory search feature is relatively easy. You’ll need to do the following:

1

2

3

4

Add a search field to the top right of the toolbar.

Add an in-memory search library.

Add the list of files and folders in the current folder to the search index. When the user begins searching, filter the files displayed in the main area.

3.2.1 Adding the search field in the toolbar

The first thing you need to do is add some HTML for the search field in the top toolbar. Insert the following HTML snippet into the index.html file, after the currentfolder div element:

<input type="search" id="search" results="5" placeholder="Search" />

This adds an input tag with the type search and some extra attributes that give it the visual style of a search field. The next step is to add the following CSS to the app.css stylesheet:

Once this is done, the search field appears as shown in figure 3.5.

Figure 3.5 The search field in the top toolbar, like the wireframe in figure 3.4. Interestingly, the results attribute on an input element with the type search inserts a magnifying glass inside the text field.

3.2.2 Adding an in-memory search library

Now that the search field exists, you need a way to perform searching on the list of files and folders with a searching library. Thankfully, you don’t need to write one, as this is a common need that has already been satisfied.

lunr.js is a client-side search library, written by Oliver Nightingale (a colleague of mine when we both worked at New Bamboo, now part of Thoughtbot). It allows you to create an index for the list of the files and folders and perform searches with that index.

You can install lunr.js with npm from the command line:

npm install lunr --save

This will install lunr.js inside the node_modules folder and save it as a dependency to the package.json file. Now, you need to create a new file at the same level as the app.js file, called search.js. You can create it either on the command line with the command touch search.js or via your text editor. Once it exists, add the code shown in the next listing to the search.js file.

The code implements three functions: addToIndex allows you to add files to the index, find allows you to query the index, and resetIndex resets the index when you need to view a new folder and clear the existing index. You expose these functions through module.exports so that you can load the file in app.js and access those functions.

Once you’ve created and saved the search.js file, you need to attach it to the search field in the UI, as well as get it to change what files are displayed in the main area.

3.2.3 Hooking up the search functionality with the UI To have the search field trigger searching the file names, you need to be able to intercept the event of typing the query in the field. You can do this by adding a function to the userInterface.js file called bindSearchField, which will attach an event listener to the search field. In the userInterface.js file, add the following function to the file:

function bindSearchField(cb) { document.getElementById('search').addEventListener('keyup', cb, false); }

This code will intercept any events where the user has typed in the search field, and the key on the keyboard is back up (hence, the event name keyup). You also add this function to the module.exports object at the bottom of the userInterface.js file so that you can expose it to the app.js file, as shown here:

module.exports = { bindDocument, displayFiles, loadDirectory, bindSearchField };

This function will be used to attach a function to the search field in the UI that triggers each time the user presses a key on the keyboard while typing into the search field.

Here, you’ll inspect the value that exists inside the search field. If it’s blank, then you don’t want to filter any files. But if it has another value, then you want to filter the files that are displayed in the main area. To achieve that, you need to do the following:

 Before you load a folder path in the main area, you reset the search index.

 When a file is added to the main area, you add it to the search index.

 When the search field is empty, you make sure that all files are on show.

 When the search field has a term, you filter the display of the files based on that term.

But first, you should include the search module at the top of the dependencies list of the userInterface.js file. Change the top of the userInterface.js file so that it looks like this:

This provides you with access to the search module. Following the inclusion of the search module, the first change you want to make is to the loadDirectory function. You want it to reset the search index every time it’s called so it only searches for files that are in the current folder path. Change the loadDirectory function’s code to match the next listing.

Listing 3.8

Resetting the search index when calling loadDirectory

Once that’s done, the next thing you want to adjust is the displayFile function below the loadDirectory function. The function will handle adding the file to the search index as well as making sure that the img element contains a reference to the file’s path so that the file can be filtered visually without needing to add/remove elements from the DOM. Change the displayFile function’s code to look like the following.

Listing 3.9

Adding files to the search index in the displayFile function

Next, add a function for filtering the results visually. This function uses a function to look at the file paths for the files and folders on display in the main area and check whether any of them matches with the search results for the term typed into the search field. After the bindSearchField function, add the function shown in the next listing to the userInterface.js file.

You can add a small utility function to handle the case of resetting the filter. This occurs when the search field is blank. Add the following function after the filterResults function that was added to the userInterface.js file:

Here, you use a selector to select all div elements that have a CSS class of item, and make sure they’re visible by removing any custom style attributes that would have marked them as hidden. Also, you want to make sure that the filterResults and resetFilter functions are publically available via the module API. Change the module .exports object at the bottom of the userInterface.js file so that it looks like this:

That’s all the changes to make to the userInterface.js file for now. Next, turn your attention to the app.js file and change it so that

 It binds on the search field in the user interface.

 It passes the search field’s term to the search tool lunr.

 It then passes the results from the search tool back to the UI for rendering.

Change the code in the app.js file so that it looks like the code shown next.

Listing 3.11

Integrating the search feature into the app.js file

After saving this file along with the previous files, reload the app. The app loads like before, but this time you’ll find that when you type a term into the search field, the files and folders in the main area of the app are filtered to show only those that match the search term. If you then type a blank value into the search field, all the files and folders inside the current folder path are shown. Even as you double-click a folder and navigate into it to see its files and folders, the search field will work on that current folder and filter its contents, as shown in figure 3.6.

Figure 3.6

The search field filtering files based on their name inside Atom’s hidden folder

With about six handcrafted files totaling no more than 281 lines of code and some npm modules, you’ve managed to build a file explorer. The file explorer can show the files in a folder, traverse the folders, and filter the files based on the name of the file as indicated in the original wireframe. Not bad, given the relatively small size of the code.

Next, you want to improve navigating through the app as well as getting files to open with their default application.

3.3 Enhancing navigation in the app

You’ve gotten to a stage where you can display the contents of the user’s personal folder and allow them to traverse through those folders to see what other files and folders exist on their computer, as well as filter the files and folders by a search query. Now you’ll help the user navigate backward as well, as there isn’t currently a way to do that in the app.

To do this, you’ll give the user the ability to navigate the folders via the current folder path—you’ll make it a clickable path, with each folder in the path going to that folder’s location on the computer.

3.3.1 Making the current folder path clickable

Figure 3.7 shows what you want to do.

Figure 3.7 When clicking any path in the current folder path in the top toolbar, you want to display the contents of the folder in the main area.

The current folder is currently a line of text that’s displayed in the UI in the toolbar, but it can be used to do so much more. In this case, you’re looking to change it so that it looks the same as it looks now but allows the user to load a different folder path by clicking a folder name in the path, like clicking a link in a web page, as shown in figure 3.8.

Let’s begin by looking at the code that handles the display of the current folder in the toolbar, the displayFolderPath function in the userInterface.js file. You’ll need to modify this function so that instead of returning the current folder path, it passes the folder path to another function, which will convert that folder path into a set of

Figure 3.8 How clicking a path item in the current folder path will end up loading that path in the app

span HTML elements. The span tags will contain not only the name of the folder, but also a data attribute referring to the path of that folder. This is so that when the folder is selected, you can pass that folder to the loadFolder function and load the folder in the app.

Let’s begin by creating a function that will receive a folder name and return the folder as a list of HTML span tags, with the path for that folder added as an attribute on the span tag. Call this function convertFolderPathIntoLinks and place it in the userInterface.js file. First, you need to add a module dependency at the top of the file (after the search module require) to load Node.js’s path module:

const path = require('path');

The path module is used to return the path separator used by the operating system. In Mac OS and Linux, the path separator is a forward slash (/), but on Windows it’s a backward slash (\). This will be used by the function to create the folder path for each folder as well as to display the full path for the current folder. In the convertFolderPathIntoLinks function, the following code is used:

The function takes the path for the folder and turns it into a list of folders by splitting it on the folder path separator. With this list of folders in the current folder path, you can begin to create the span tags for each one. Each span tag will have a class attribute with a value of path, a data-path attribute that contains the path for that folder, and, finally, the name of the folder as the text inside the span tag.

Once the span tags are created, the HTML is joined together and returned as a string. This HTML is then used by the displayFolderPath function. It receives the current folder path and returns the HTML to be inserted into the toolbar. As a result, you’ll need to update the function to insert HTML instead of text. Adjust the displayFolderPath function to this code:

The function now uses innerHTML to insert the HTML into the current-folder element in the screen, and the convertFolderPathIntoLinks function receives the folder path passed to the displayFolderPath function and returns HTML in its place. The nice thing about this change is how you only had to change a small part of the displayFolderPath function, rather than lots of changes in multiple places. This is a desirable goal with coding: construct it so that it can be altered with ease. With this change accomplished, you now need to handle clicking a folder name in the toolbar and having the screen navigate to that folder.

In the userInterface.js file, you’ll add another function that will bind on a user clicking a folder name (in this case, any span element with a class of path) and return the folder path to a callback function. The callback function can then use the folder path to pass that to the code that handles loading a folder. Add the following code to the userInterface.js file, roughly toward the bottom of the file, but before the module .exports object:

You then want to call this function as part of the displayFolderPath function. Change the displayFolderPath function to this:

The userInterface.js file is easily extended to include extra functionality for handling clicks on path items in the current folder path—which is nice, because it allows you to easily alter your code without having to rewire whole swathes of the codebase.

3.3.2 Getting the app to load at the folder path

This simple one-line change enables the functionality to work, and the last code change you want to do before you put it into action is to make the span elements show a pointer when the cursor passes over them. Add the following code to the app.css file:

span.path:hover { opacity: 0.7; cursor: pointer; }

With these changes saved, you can now reload the app, click through folders as normal, and then go back by clicking a folder in the current folder path. This ensures that users can navigate back to other folders, because otherwise they would be stuck. What you’ve done so far is replicate a feature that’s common to all native file explorers across the operating systems (navigating folders via paths), but you added a twist to it so that the paths are clickable—not all file explorers do this. This shows how with Electron or NW.js you have the power to not only re-create desktop experiences using web technologies, but also combine them in ways to do new things that haven’t been done in desktop apps before.

Now that you’ve added that feature, the next step is to handle opening files with their default application.

3.3.3 Opening files with their default application

So far in the app, you’ve focused a lot on interacting with folders, but now you need to look at how you can make the file explorer open files like images, videos, documents, and other items.

In order to implement this feature, you’ll need to do the following:

 Handle clicking on a file as opposed to a folder.

 Pass the file path for that file to NW.js/Electron’s way of opening external files.

We’ll look at handling clicking a file first.

CLICKING A FILE

You’ll probably remember from earlier on in the chapter that you detected whether the file you were rendering to the main area was a folder, and attached an event to it when it was double-clicked. You’ll use the same pattern again to handle doubleclicking files.

In the userInterface.js file is the displayFile function that handles displaying the individual files and folders in the main area, as well as attaching events to them. Change the function so that it looks like the following listing.

Listing 3.12

Adding file double-clicking to the displayFile function

The couple of extra lines of code allow you to listen to the file being double-clicked and attach it to a new function called openFile in the fileSystem.js module, which you’ll now create.

The openFile function in the fileSystem.js module is going to call out to either Electron or NW.js’s shell API. The shell API is able to open URLs, files, and folders in their default applications. To show you how compatible Electron and NW.js are as desktop app frameworks, you’ll write one item of code that can be used across both frameworks without any need for modification.

In the fileSystem.js file, add the following snippet of code toward the top of the file, below the dependency declarations:

This snippet of code can run on either an Electron app or an NW.js app, which means less code for you to have to write/adjust. Notice how Electron and NW.js call out to a shell object (though NW.js calls it via the GUI API, and with a title-cased name). If the app is running as an Electron application, it will load Electron’s shell API, and if running NW.js, it will load NW.js’ shell API.

With the shell API loaded for the given Node.js desktop app framework, you now call out to the shell API’s method for opening files. Add the function shown in the following listing to the fileSystem.js file, right before the module.exports object.

Listing 3.13

Adding the openFile function to the fileSystem.js file

Notice anything funny? The shell API’s function name for opening files is the same across both Electron and NW.js. It’s a pleasant surprise that may seem unexpected unless you know a bit about NW.js and Electron’s shared history.

With this new function, all you need to do now is make sure it’s available as a public API function in the fileSystem.js file. Amend the module.exports object so that it includes the function, as shown in the following code:



I’d almost say you’re done, but there’s one more thing (to borrow a phrase from the late Steve Jobs). You want to give the app a visual indicator that the files and the folders can be clicked when the cursor is hovering over them. You can extend the last CSS rule you added earlier to the app.css file. As a reminder, it looked like this:



Extend it so that it also applies to the file and folder icons in the main area:



With those changes saved, reload the app and have a go at double-clicking files in the Lorikeet app. You’ll see that those files end up opening in their default applications.


Fantastic! You now have a functional file explorer that can open files, as well as explore folders and filter the view by name.

## Summary

In this chapter, you built on the beginnings of a desktop app and created some rich features that make the app a usable, minimally viable product. You also had a chance to explore how you can evolve a desktop app’s codebase to remain readable, and how you can organize the code for a desktop app (because there’s no convention-overconfiguration approach to doing this currently).

Things we’ve covered include the following:

1 Refactoring the code by using Node.js’s module functionality.

2 Using third-party libraries to implement search features.

3 Applying Electron and NW.js’s shell API to handle opening files with their default applications.

4 Improving app navigation to make the desktop app more usable.

The main thing to take away from this chapter is that with a couple-hundred lines of code and some external files, you can build an app that replicates what a native desktop app can do (and one that has relatively complex functionality). Not only that, you’ve been able to use third-party libraries like lunr.js to help provide this functionality, and structured the code in such a way that it can be used in web apps and allow for building apps for both the web and desktop from the same source code.

In chapter 4, you’ll prepare the app for distribution: you’ll hide the app developer toolbar, give the app its own icon, and build it so that it can be run as a native app on each of the operating systems.


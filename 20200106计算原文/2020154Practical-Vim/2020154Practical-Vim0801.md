Vim lets us work on multiple files at the same time. The buffer list lets us keep track of the set of files that we’ve opened in the course of an editing session. In Tip 37, we’ll learn how to interact with this list as well as learn the distinction between a file and a buffer.

The argument list is a great complement to the buffer list. In Tip 38, we’ll see how to use the :args command to group files from the buffer list into a collection. We can then traverse the list or execute an Ex command on each member of the set using the :argdo command.

Vim allows us to divide our workspace into split windows. We’ll learn how in Tip 40. Then in Tip 41, we’ll see how Vim’s tabbed interface can be used to organize split windows into a collection.

Tip 37 Track Open Files with the Buffer List

	 	 	 	 We can load multiple files during an editing session. Vim lets us manage them using the buffer list.

Understand the Distinction Between Files and Buffers

	 	 Just like any other text editor, Vim allows us to read files, edit them, and save our changes. When we discuss our workflow, it’s tempting to say that we’re editing a file, but that’s not what we’re actually doing. Instead, we’re editing an in-memory representation of a file, which is called a buffer in Vim’s terminology.

Files are stored on the disk, whereas buffers exist in memory. When we open a file in Vim, its contents are read into a buffer, which takes the same name as the file. Initially, the contents of the buffer will be identical to those of the file, but the two will diverge as we make changes to the buffer. If we decide that we want to keep our changes, we can write the contents of the buffer back into the file. Most Vim commands operate on buffers, but a few operate on files, including the :write, :update, and :saveas commands.

Meet the Buffer List

Vim allows us to work with multiple buffers simultaneously. Let’s open a few files by running these commands in the shell:

​=> ​$ cd code/files​

​=> ​$ vim *.txt​

​<= 2 files to edit

The *.txt wildcard matches two files in the current directory: a.txt and b.txt. This command tells Vim to open both of those files. When Vim starts up, it shows a single window with a buffer representing the first of the two files. The other file isn’t visible, but it has been loaded into a buffer in the background, as we can see by running the following:

​=> ​:ls​

​<= 1 %a "a.txt" line 1

​ 2 "b.txt" line 0

	 	 	 The :ls command gives us a listing of all the buffers that have been loaded into memory (:lsⓘ). We can switch to the next buffer in the list by running the :bnext command:

​=> ​:bnext​

​=> ​:ls​

​<= 1 # "a.txt" line 1

​ 2 %a "b.txt" line 1

	 	 The % symbol indicates which of the buffers is visible in the current window, while the # symbol represents the alternate file. We can quickly toggle between the current and alternate files by pressing <C-^>. Press it once, and we’ll switch to a.txt; press it a second time, and we’ll get back to b.txt.

Use the Buffer List

	 	 	 	 We can traverse the buffer list using four commands—:bprev and :bnext to move backward and forward one at a time, and :bfirst and :blast to jump to the start or end of the list. It’s a good idea to map them to something easier to reach. I use these mappings from Tim Pope’s unimpaired.vim plugin:[9]

​ nnoremap <​silent​> [​b​ :​bprevious​<CR>

​ nnoremap <​silent​> ]​b​ :​bnext​<CR>

​ nnoremap <​silent​> [B :​bfirst​<CR>

​ nnoremap <​silent​> ]B :​blast​<CR>

(Vim already uses the [ and ] keys as prefixes for a series of related commands (see [ⓘ), so these mappings have a consistent feel to them. The unimpaired.vim plugin provides similar mappings for scrolling through the argument ([a and ]a), quickfix ([q and ]q), location ([l and ]l), and tag lists ([t and ]t). Check it out.)

	 	 	 	 The :ls listing starts with a digit, which is assigned to each buffer automatically on creation. We can jump directly to a buffer by number, using the :buffer N command (see :bⓘ). Alternatively, we can use the more intuitive form, :buffer {bufname}. The {bufname} need only contain enough characters from the filepath to uniquely identify the buffer. If we enter a string that matches more than one of the items in the buffer list, we can use tab-completion to choose between the options (see Tip 32).

	 The :bufdo command allows us to execute an Ex command in all of the buffers listed by :ls (:bufdoⓘ). In practice, I usually find that it’s more practical to use :argdo instead, which we’ll meet in Tip 38.

Deleting Buffers

	 	 	 Vim creates a new buffer any time we open a file, and we’ll learn a few ways of doing that in Chapter 7, ​Open Files and Save Them to Disk​. If we want to delete a buffer, we can do so using the :bdelete command. This can take one of these forms:

​ :bdelete N1 N2 N3

​ :N,M bdelete

Note that deleting a buffer has no effect on its associated file; it simply removes the in-memory representation. If we wanted to delete buffers numbered 5 through 10 inclusive, we could do so by running :5,10bd. But if we wanted to keep buffer number 8, then we’d instead have to run :bd 5 6 7 9 10.

Buffer numbers are automatically assigned by Vim, and we have no means of changing them by hand. So if we want to delete one or more buffers, we first have to look them up to find out their numbers. This procedure is relatively time-consuming. Unless I have a good reason to delete a buffer, I usually don’t bother. As a result, the :ls listing comes to represent all of the files that I have opened in the course of an editing session.

Vim’s built-in controls for managing the buffer list lack flexibility. If we want to arrange buffers in a way that makes sense for our workflow, attempting to organize the buffer list is not the way to go. Instead, we’re better off dividing our workspace using split windows, tab pages, or the argument list. The next few tips will show how.

Tip 38 Group Buffers into a Collection with the Argument List

	 	 	 	 	 	 The argument list is easily managed and can be useful for grouping together a collection of files for easy navigation. We can run an Ex command on each item in the argument list using the :argdo command.

Let’s start by opening a handful of files in Vim:

​=> ​$ cd code/files/letters​

​=> ​$ vim *.txt​

​<= 5 files to edit

In Tip 37, we saw that the :ls command provides a listing of buffers. Now let’s examine the argument list:

​=> ​:args​

​<= [a.txt] b.txt c.txt. d.txt e.txt

	 The argument list represents the list of files that was passed as an argument when we ran the vim command. In our case, we provided a single argument, *.txt, but our shell expanded the * wildcard, matching the five files that we see in our argument list. The [] characters indicate which of the files in the argument list is active.

Compared to the listing provided by the :ls command, the output from running :args looks crude. It should come as no surprise to learn that the argument list was a feature of vi, whereas the buffer list is an enhancement introduced by Vim. But give the argument list a chance, and you’ll see that it makes a fine complement to the buffer list.

Like many features in Vim, the functionality of the argument list has been enhanced, while the original name has stuck. We can change the contents of the argument list at any time, which means that the :args listing doesn’t necessarily reflect the values that were passed to the vim command when we launched the editor. Don’t take the name literally! (Also, see ​‘:compiler’ and ‘:make’ Are Not Just for Compiled Languages​.)

Populate the Argument List

	 	 When the :args Ex command is run without arguments, it prints the contents of the argument list. We can also set the contents of the argument list using this form (:args_fⓘ):

​ :args {arglist}

The {arglist} can include filenames, wildcards, or even the output from a shell command. To demonstrate, we’ll use the files/mvc directory, which you can find in the source files that come distributed with this book. If you want to follow along, switch to that directory and launch Vim:

​=> ​$ cd code/files/mvc​

​=> ​$ vim​

For an overview of the directory tree, refer to the code listing.

Specify Files by Name

		 The simplest way of populating the argument list is by specifying filenames one by one:

​=> ​:args index.html app.js​

​=> ​:args​

​<= [index.html] app.js

This technique works fine if we only want to add a handful of buffers to our set. It has the advantage that we can specify the order, but doing it by hand can be laborious. If we want to add a lot of files to the argument list, we can get the job done faster by using wildcards.

Specify Files by Glob

		 		 Wildcards are placeholders that can stand in for characters in the name of a file or directory. The * symbol will match zero or more characters, but only in the scope of the specified directory (wildcardⓘ). The ** wildcard also matches zero or more characters, but it can recurse downward into directories below the specified directory (starstar-wildcardⓘ).

		 We can combine these wildcards and use partial filenames or directories to form patterns, also known as globs, that match the set of files we’re interested in. This table shows a representative summary of some (but not all) of the files in the files/mvc directory that are matched by the specified globs.

GlobFiles Matching the Expansion

:args *.*

​ index.html

​ app.js

:args **/*.js

​ app.js

​ lib/framework.js

​ app/controllers/Mailer.js

​ ...etc

:args **/*.*

​ app.js

​ index.js

​ lib/framework.js

​ lib/theme.css

​ app/controllers/Mailer.js

​ ...etc

Just as we can use more than one filename in the {arglist}, we can also supply more than one glob. If we wanted to build an argument list containing all js and css files but not other file types, we could use these globs:

​=> ​:args **/*.js **/*.css​

Specify Files by Backtick Expansion

		 As I wrote this book, I sometimes wanted to populate the argument list with the chapters in the same order that they appear in the table of contents. For this purpose, I maintained a plain-text file that contains one filename per line. Here’s an excerpt from it:

files/.chapters

​ the_vim_way.pml

​ normal_mode.pml

​ insert_mode.pml

​ visual_mode.pml

I can populate the argument list from this file by running this:

​=> ​:args `cat .chapters`​

		 		 Vim executes the text inside the backtick characters in the shell, using the output from the cat command as the argument for the :args command. Here, we’ve used the cat command to get the contents of the .chapters file, but we could use any command that’s available in the shell. This feature is not available on all systems. See backtick-expansionⓘ for more details.

Use the Argument List

The argument list is simpler to manage than the buffer list, making it the ideal place to group our buffers into a collection. With the :args {arglist} command, we can clear the argument list and then repopulate it from scratch with a single command. We can traverse the files in the argument list using :next and :prev commands. Or we can use :argdo to execute the same command on each buffer in the set.

The way I see it, the buffer list is like my desktop: it’s always messy. The argument list is like a separate workspace that I always keep tidy, just in case I need space to stretch out. We’ll see a few examples of how the argument list can be used in other tips, such as Tip 36, and Tip 70.

Tip 39 Manage Hidden Files

	 	 	 When a buffer has been modified, Vim gives it special treatment to ensure that we don’t accidentally quit the editor without saving our changes. Find out how to hide a modified buffer and how to handle hidden buffers when quitting Vim.

Run these commands in the shell to launch Vim:

​=> ​$ cd code/files​

​=> ​$ ls​

​<= a.txt b.txt

​=> ​$ vim *.txt​

​<= 2 files to edit

Let’s make a change to a.txt. We’ll just press Go to append a blank line at the end of the buffer. Without saving the changes, let’s examine the buffer list:

​=> ​:ls​

​<= 1 %a + "a.txt" line 1

​ 2 "b.txt" line 0

The buffer representing a.txt is annotated with a + sign, which indicates that it has been modified. If we were to save the file now, the contents of the buffer would be written to disk and the + annotation would go away. But let’s not save the buffer just yet. Instead, we’ll try to switch to the next buffer:

​=> ​:bnext​

​<= E37: No write since last change (add ! to override)

	 	 	Vim raises an error message, reporting that the current buffer contains unsaved changes. Let’s try following the advice in parentheses and add a trailing bang symbol:

​=> ​:bnext!​

​=> ​:ls​

​<= 1 #h + "a.txt" line 1

​ 2 %a "b.txt" line 1

	 	The bang symbol forces Vim to switch buffers, even if our current buffer has unsaved changes. When we run the :ls command now, b.txt is marked with the letter a for active, while a.txt is marked with the letter h for hidden.

Handle Hidden Buffers on Quit

	 	 	 When a buffer is hidden, Vim lets us go about our business as usual. We can open other buffers, change them, save them, and so on, all without consequences—that is, right up until we attempt to close our editing session. That’s when Vim reminds us that we have unsaved changes in one of our buffers:

​=> ​:quit​

​<= E37: No write since last change (add ! to override)

​ E162: No write since last change for buffer "a.txt"

	 	 	 	 Vim loads the first hidden buffer with modifications into the current window so that we can decide what to do with it. If we want to keep the changes, we can run :write to save the buffer to a file. Or if we want to discard the changes, we can instead run :edit!, which rereads the file from disk, overwriting the contents of the buffer. Having reconciled the contents of the buffer with the file on disk, we can try the :quit command again.

If we have more than one hidden buffer with modifications, then Vim activates the next unsaved buffer each time we enter the :quit command. Again, we could :write or :edit! to keep or discard the changes. This cycle continues until we make a decision for each of the hidden buffers with modifications. When there are no more windows and no more hidden modified buffers, the :q command closes Vim.

	 If we want to quit Vim without reviewing our unsaved changes, we can issue the :qall! command. Or, if we want to write all modified buffers without reviewing them one by one, we can use the :wall command. Table 9, ​Options for Hidden Buffers on Quit​ summarizes our options.

* * *

Table 9. Options for Hidden Buffers on Quit

CommandEffect

:w[rite]

Write the contents of the buffer to disk

:e[dit]!

Read the file from disk back into the buffer (that is, revert changes)

:qa[ll]!

Close all windows, discarding changes without warning

:wa[ll]

Write all modified buffers to disk

* * *

Enable the ‘hidden’ Setting Before Running ‘:*do’ Commands

	 	 By default, Vim prevents us from abandoning a modified buffer. Whether we use the :next!, :bnext!, :cnext!, or any similar command, if we omit the trailing bang symbol, Vim will nag us with the「No write since last change」error message. In most cases, this message is a useful reminder. But in one scenario it becomes a nuisance.

Consider the commands :argdo, :bufdo, and :cfdo commands. The :argdo {cmd} command works like this:

​=> ​:first​

​=> ​:{cmd}​

​=> ​:next​

​=> ​:{cmd}​

​<= etc.

If our chosen {cmd} modifies the first buffer, the :next command will fail. Vim won’t permit us to advance to the second item in the argument list until we save the changes to the first item in the list. That’s not much use!

If we enable the ‘hidden’ setting (see 'hidden'ⓘ), then we can use the :next, :bnext, :cnext (and so on) commands without a trailing bang. If the active buffer is modified, Vim will automatically hide it when we navigate away from it. The ‘hidden’ setting makes it possible to use :argdo, :bufdo, and :cfdo to change a collection of buffers with a single command.

After running :argdo {cmd}, we’ll want to save the changes that were made to each item in the argument list. We could do it one at a time by running :first and then :wn, which would give us the opportunity to eyeball each file. Or if we’re confident that everything is in order, we could run :argdo write (or :wall) to save all buffers.

Tip 40 Divide Your Workspace into Split Windows

	 	 	 	 Vim allows us to view multiple buffers side by side by dividing our workspace into split windows.

	 In Vim’s terminology, a window is a viewport onto a buffer (windowⓘ). We can open multiple windows, each containing the same buffer, or we can load different buffers into each window. Vim’s window management system is flexible, allowing us to build a workspace tailored to the demands of our workflow.

Creating Split Windows

When Vim starts up, it contains a single window. We can divide this window horizontally with the <C-w>s command, which creates two windows of equal height. Or we can use the <C-w>v command to split the window vertically, producing two windows of equal width. We can repeat these commands as often as we like, splitting our workspace again and again in a process that resembles cell division.

The following figure illustrates a few of the possible results. In each case, the shaded rectangle represents the active window.

	 	 Each time we use the <C-w>s and <C-w>v commands, the two resulting split windows will contain the same buffer as the original window that was divided. Having the same buffer displayed in separate windows can be useful, especially if we’re working on a long file. For example, we could scroll in one of the windows to show a part of the buffer that we want to refer to while making changes to another part of the buffer in the other window.

	 	 	 	 We can use the :edit command to load another buffer into the active window. If we run <C-w>s followed by :edit {filename}, we can divide our workspace and then open another buffer in one split window while keeping the existing buffer visible in the other split. Alternatively, we could use the command :split {filename}, which combines those two steps into one. This table summarizes the ways of dividing our workspace into split windows:

CommandEffect

		 		 <C-w>s

Split the current window horizontally, reusing the current buffer in the new window

		 		 <C-w>v

Split the current window vertically, reusing the current buffer in the new window

		 		 :sp[lit] {file}

Split the current window horizontally, loading {file} into the new window

		 		 :vsp[lit] {file}

Split the current window vertically, loading {file} into the new window

Changing the Focus Between Windows

	 	 	 	 	 	 Vim provides a handful of commands for switching the focus between split windows. This table summarizes some of the highlights (for the complete list, see window-move-cursorⓘ):

CommandEffect

<C-w>w

Cycle between open windows

<C-w>h

Focus the window to the left

<C-w>j

Focus the window below

<C-w>k

Focus the window above

<C-w>l

Focus the window to the right

In fact, <C-w><C-w> does the same thing as <C-w>w. That means we can press the <Ctrl> key and hold it while typing ww (or wj or any of the others from the table) to change the active window. It’s easier to type <C-w><C-w> than <C-w>w, even though it looks nastier when written down. Still, if you use split windows heavily, you might want to consider mapping these commands to something even more convenient.

If your terminal supports mouse interactions or if you’re using GVim, then you can also activate a window by clicking it with the mouse. If it doesn’t work for you, check that the ‘mouse’ option is set appropriately ('mouse'ⓘ).

Closing Windows

	 	 	 	 	 	 	 If we want to reduce the number of windows in our workspace, we can take one of two strategies. We could use the :close command to close the active window, or if we want to close all windows except the active one, we can instead use the :only command. This table summarizes the options and shows the normal mode equivalents:

Ex CommandNormal CommandEffect

:clo[se]

<C-w>c

Close the active window

:on[ly]

<C-w>o

Keep only the active window, closing all others

Resizing and Rearranging Windows

	 	 	 	 	 	 Vim provides several key mappings for resizing windows. For the full list, look up window-resizeⓘ. This table summarizes a handful of the most useful commands:

KeystrokesBuffer Contents

<C-w>=

Equalize width and height of all windows

<C-w>_

		 		 		 Maximize height of the active window

<C-w>|

		 		 Maximize width of the active window

[N]<C-w>_

Set active window height to [N] rows

[N]<C-w>|

Set active window width to [N] columns

Resizing windows is one of the few tasks I prefer to do with the mouse. It’s simple: click on the line that separates two windows, drag the mouse until each window is the desired size, and then let go of the mouse. This works only if your terminal supports the mouse or if you’re using GVim.

Vim includes commands for rearranging windows, but rather than describing them here, I’d like to point you toward a screencast on Vimcasts.org that demonstrates the possibilities.[10] You can also find more details by looking up window-movingⓘ.

Tip 41 Organize Your Window Layouts with Tab Pages

	 	 	 Vim’s tabbed interface is different from that of many other text editors. We can use tab pages to organize split windows into a collection of workspaces.

In Vim, a tab page is a container that can hold a collection of windows (tabpageⓘ). If you’re accustomed to using another text editor, then Vim’s tabbed interface might seem strange at first. Let’s begin by considering how tabs work in many other text editors and IDEs.

	 	 The classic graphical user interface (GUI) for a text editor features a main workspace for editing files and a sidebar that shows the directory tree of the current project. If we click on a file in the sidebar, it opens a new tab in the main workspace for the specified file. A new tab is created for each file that we open. In this model, we could say that the tabs represent the set of files that are currently open.

	 When we open a file using the :edit command, Vim doesn’t automatically create a new tab. Instead, it creates a new buffer and loads it into the current window. Vim keeps track of the set of files that are open using the buffer list, as we saw in Tip 37.

Vim’s tab pages are not mapped to buffers in a one-to-one relationship. Instead, think of a tab page as a container that can hold a collection of windows. The following figure illustrates a workspace with three tab pages, each containing one or more windows. In each scenario, the shaded rectangles represent the active windows and tabs.

	 	 Tab pages are available to us whether we’re using GVim or running Vim inside a terminal. GVim draws a tab bar as part of the GUI, giving it an appearance much like that of a web browser or any other tabbed interface. When Vim runs inside a terminal, it draws a tab bar as a textual user interface (TUI). Apart from the differences in appearance, tab pages are functionally identical whether rendered as a GUI or a TUI.

How to Use Tabs

	 	 Vim’s tab pages can be used to partition work into different workspaces. They have more in common with the virtual desktops in Linux than they do with the tabbed interface of most other text editors.

Suppose that we’re at work on a project, with our workspace divided into a few split windows. Out of the blue, something urgent comes up and we have to switch contexts. Rather than opening new files in our current tab page, which would mess up our carefully assembled workspace, we can create a new tab page and do the work there. When we’re ready to resume our previous work, we just have to switch back to the original tab page where all of our windows will have been preserved as we left them.

	 The :lcd {path} command lets us set the working directory locally for the current window. If we create a new tab page and then use the :lcd command to switch to another directory, we can then comfortably scope each tab page to a different project. Note that :lcd applies locally to the current window, not to the current tab page. If we have a tab page containing two or more split windows, we could set the local working directory for all of them by running :windo lcd {path}. Check out episode 9 of Vimcasts for more information.[11]

Opening and Closing Tabs

	 	 	 We can open a new tab page with the :tabedit {filename} command. If we omit the {filename} argument, then Vim creates a new tab page containing an empty buffer.

Alternatively, if the current tab page contains more than one window, we can use the <C-w>T command, which moves the current window into a new tab page (see CTRL-W_Tⓘ).

	 	 	 If the active tab page contains only a single window, the :close command will close the window and the tab page with it. Or we can use the :tabclose command, which closes the current tab page no matter how many windows it contains. Finally, if we want to close all tab pages except for the current one, we can use the :tabonly command.

CommandEffect

:tabe[dit] {filename}

Open {filename} in a new tab

<C-w>T

Move the current window into its own tab

:tabc[lose]

Close the current tab page and all of its windows

:tabo[nly]

Keep the active tab page, closing all others

Switching Between Tabs

	 	 	 Tabs are numbered starting from 1. We can switch between tabs with the {N}gt command, which can be remembered as goto tab {N}. When this command is prefixed with a number, Vim jumps to the specified tab, but if the number is omitted, Vim advances to the next tab. The gT command does the same but in reverse.

Ex CommandNormal CommandEffect

		 		 :tabn[ext] {N}

{N}gt

Switch to tab page number {N}

		 		 :tabn[ext]

gt

Switch to the next tab page

		 		 :tabp[revious]

gT

Switch to the previous tab page

Rearranging Tabs

	 	 We can use the :tabmove [N] Ex command to rearrange tab pages. When [N] is 0, the current tab page is moved to the beginning, and if we omit [N], the current tab page is moved to the end. If your terminal supports the mouse or if you’re using GVim, reordering tab pages by drag and drop is also possible.

Footnotes

[9]

https://github.com/tpope/vim-unimpaired

[10]

http://vimcasts.org/e/7

[11]

http://vimcasts.org/e/9

Copyright © 2016, The Pragmatic Bookshelf.

Chapter 7

Open Files and Save Them to Disk


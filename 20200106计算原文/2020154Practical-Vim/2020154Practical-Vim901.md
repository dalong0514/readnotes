Vim has a few ways of opening files. In Tip 42, we’ll look at the :edit command, which can be used to open any file by providing a filepath.

If we’re working on files that are two or more directories beneath our project root, having to specify a complete filepath for every file we want to open can be awkward. In Tip 43, we’ll learn how to configure the ‘path’ option, which makes it possible to use the :find command. This saves us from having to specify fully qualified filepaths and allows us to simply enter the filename.

The netrw plugin, which ships with Vim, makes it possible to explore the contents of a directory tree. We’ll find out how to use it in Tip 44.

The :write command lets us save the contents of a buffer to disk. Its usage is generally straightforward, but it can become complicated if we attempt to save to a nonexistent directory or if we don’t have the permissions required to write a file. We’ll find out how to cope with these scenarios in Tip 45, and Tip 46.

Tip 42 Open a File by Its Filepath Using ‘:edit’

	 	 	 	 The :edit command allows us to open files from within Vim, either by specifying an absolute or a relative filepath. We’ll also learn how to specify a path relative to the active buffer.

As a demonstration, we’ll use the files/mvc directory, which you can find in the source files that come distributed with this book. It contains the following directory tree:

​ app.js

​ index.html

​ app/

​ controllers/

​ Mailer.js

​ Main.js

​ Navigation.js

​ models/

​ User.js

​ views/

​ Home.js

​ Main.js

​ Settings.js

​ lib/

​ framework.js

​ theme.css

In the shell, we’ll start by changing to the files/mvc directory and then launching Vim:

​=> ​$ cd code/files/mvc​

​=> ​$ vim index.html​

Open a File Relative to the Current Working Directory

	 	 	 	 In Vim, just as in bash and other shells, we have the notion of a working directory. When Vim is launched, it adopts the same working directory that was active in the shell. We can confirm this by running the :pwd Ex command, which (just as in bash) stands for「print working directory」:

​=> ​:pwd​

​<= /Users/drew/practical-vim/code/files/mvc

The :edit {file} command can accept a filepath relative to the working directory. If we wanted to open the lib/framework.js file, we could do so by running this command:

​=> ​:edit lib/framework.js​

Or we could open the app/controllers/Navigation.js file by running this:

​=> ​:edit app/controllers/Navigation.js​

	 	 We can use the tab key to autocomplete these filepaths (see Tip 32, for more details). So if we wanted to open the Navigation.js file, we could simply press :edit a<Tab>c<Tab>N<Tab>.

Open a File Relative to the Active File Directory

	 	 	 	 	 Suppose that we’re editing the app/controllers/Navigation.js file, and we decide that we want to edit the Main.js file in the same directory. We could drill down to it from our working directory, but that feels like unnecessary work. The file we want to open is in the same directory as our active buffer. It would be ideal if we could use the context of the active buffer as a reference point. 	 Try this:

​=> ​:edit %<Tab>​

	 The % symbol is a shorthand for the filepath of the active buffer (see cmdline-specialⓘ). Pressing the <Tab> key expands the filepath, revealing the absolute path of the active buffer. That’s not quite what we want, but it’s getting close. Now try this instead:

​=> ​:edit %:h<Tab>​

The :h modifier removes the filename while preserving the rest of the path (see ::hⓘ). In our case, typing %:h<Tab> is expanded to the full path of the current file’s directory:

​=> ​:edit app/controllers/​

From there, we can type Main.js (or have the tab key autocomplete it for us), and Vim will open the file. In total, we have to enter only the following keystrokes:

​=> ​:edit %:h<Tab>M<Tab><Tab>​

	 The %:h expansion is so useful that you might want to consider creating a mapping for it. Check out ​Easy Expansion of the Active File Directory​, for a suggestion.

Easy Expansion of the Active File Directory

	 	 	 Try sourcing this line in your vimrc file:

​ cnoremap <expr> %% getcmdtype() == ':' ? expand('%:h').'/' : '%%'

Now when we type %% on Vim’s : command-line prompt, it automatically expands to the path of the active buffer, just as though we had typed %:h<Tab>. Besides working nicely with :edit, this can come in handy with other Ex commands such as :write, :saveas, and :read.

For more ideas on how to use this mapping, see the Vimcasts episode on the :edit command.[12]

Tip 43 Open a File by Its Filename Using ‘:find’

	 	 	 The :find command allows us to open a file by its name without having to provide a fully qualified path. To exploit this feature, we first have to configure the ‘path’ setting.

We can always use the :edit command to open a file by providing its full path. But what if we’re working on a project where the files are nested a few directories deep? Entering the full path every time we want to open a file can get tiresome. That’s where the :find command comes in.

Preparation

We’ll use the files/mvc directory to demonstrate. The source files are distributed with this book. In the shell, we’ll launch Vim from the files/mvc directory:

​=> ​$ cd code/files/mvc​

​=> ​$ vim index.html​

Let’s see what happens if we attempt to use the :find command right now:

​=> ​:find Main.js​

​<= E345: Can't find file "Main.js" in path

The error message tells us that no Main.js file can be found in the path. So let’s do something about it.

Configure the ‘path’

	 	 	 The ‘path’ option allows us to specify a set of directories inside of which Vim will search when the :find command is invoked (see 'path'ⓘ). In our case, we want to make it easier to look up files in the app/controllers and app/views directories. We can add these to our path simply by running this:

​=> ​:set path+=app/**​

	 The ** wildcard matches all subdirectories beneath the app/ directory. We discussed wildcards in ​Populate the Argument List​, but the treatment of * and ** is slightly different in the context of the ‘path’ setting (see file-searchingⓘ). The wildcards are handled by Vim rather than by the shell.

Smart Path Management with rails.vim

	 	 	 Tim Pope’s rails.vim plugin does some clever things to make navigating around a Rails project easier.[13] The plugin automatically configures the ‘path’ setting to include all the directories found in a conventional Rails project. This means that we can use the :find command without having to worry about setting up the ‘path’.

But rails.vim doesn’t stop there. It also provides convenience commands, such as :Rcontroller, :Rmodel, :Rview, and others. Each of these acts as a specialized version of the :find command, scoping its search to the corresponding directory.

Use ‘:find’ to Look up Files by Name

	 Now that we’ve configured our ‘path’, we can open files in the directories we specified by providing just their filename. For example, if we wanted to open the app/controllers/Navigation.js file, we could enter this command:

​=> ​:find Navigation.js​

We can use the <Tab> key to autocomplete filenames, so in fact we can get what we want by typing as little as :find nav<Tab> followed by the Enter key.

You might be wondering what happens if the specified filename is not unique. Let’s find out. In our demo codebase, we have two files named Main.js: one is in the app/controllers directory and the other is in app/views.

​=> ​:find Main.js<Tab>​

If we type out the Main.js filename and then hit <Tab>, Vim expands the entire path of the first full match: ./app/controllers/Main.js. Press <Tab> a second time, and the next matching filepath takes its place, in this case ./app/views/Main.js. When we press the Enter key, Vim will use the entire filepath if it has been expanded or the first full match if no <Tab> expansion has been performed.

	 You may observe slightly different tab-completion behavior if you have changed the ‘wildmode’ setting from its default value of full. Refer to Tip 32, for more details.

Tip 44 Explore the File System with netrw

	 	 	 In addition to letting us view (and edit) the contents of a file, Vim also lets us view the contents of a directory. The netrw plugin, included in the Vim distribution, allows us to explore the file system.

Preparation

The functionality described in this tip is not implemented in Vim’s core source code but in a plugin called netrw. This plugin comes as standard with the Vim distribution, so we don’t have to install anything, but we do need to make sure that Vim is configured to load plugins. These lines of configuration are the minimum requirement for your vimrc file:

essential.vim

​ ​set​ nocompatible

​ ​filetype​ plugin ​on​

Meet netrw—Vim’s Native File Explorer

If we launch Vim with the path to a directory rather than a file, it will start up with a file explorer window:

​=> ​$ cd code/file/mvc​

​=> ​$ ls​

​<= app app.js index.html lib

​=> ​$ vim .​

The screenshot shows how the file explorer looks. It’s a regular Vim buffer, but instead of showing the contents of a file, it represents the contents of a directory.

We can move the cursor up and down using the k and j keys. When we press the <CR> key, it opens the item under the cursor. If the cursor is positioned on a directory, the explorer window is redrawn to show the contents of that directory. If the cursor is positioned on a filename, the file is loaded into a buffer in the current window, replacing the file explorer. We can open the parent directory by pressing the - key or by positioning the cursor on the .. item and pressing <CR>.

We’re not limited to navigating the directory listing with j and k keys. We can use all of the motions that are available to us in a regular Vim buffer. For example, if we wanted to open the index.html file, we could search for /html<CR>, putting our cursor right where we need it.

Opening the File Explorer

	 	 	 	 	 We can open the file explorer window with the :edit {path} command by supplying a directory name (instead of a filename) as the {path} argument. The dot symbol stands for the current working directory, so if we run the :edit . command, we can bring up a file explorer for the project root.

If we wanted to open a file explorer for the directory of the current file, we could do so by typing :edit %:h (see ​Open a File Relative to the Active File Directory​, for an explanation). But the netrw plugin provides a more convenient way with the :Explore command (see :Exploreⓘ).

	 Both of these commands can be abbreviated. Instead of typing out :edit ., we can get away with just :e.—we don’t even need the space before the dot. And :Explore can be truncated right down to :E. This table summarizes the long- and shorthand forms of these commands:

Ex CommandShorthandEffect

:edit .

:e.

Open file explorer for current working directory

:Explore

:E

Open file explorer for the directory of the active buffer

	 	 In addition to :Explore, netrw also provides :Sexplore and :Vexplore commands, which open the file explorer in a horizontal split window or vertical split window, respectively.

Working with Split Windows

	 	 	 The classic GUI for a text editor presents the file explorer in a sidebar, sometimes known as the project drawer. If you’re used to this kind of interface, then it might seem strange that Vim’s :E and :e. commands behave the way they do by replacing the contents of the current window with a file explorer. There’s a good reason for this: it works well with split windows.

Consider the layout in the first frame of this image:

Here we see three split windows, each displaying a different buffer. Let’s imagine for a moment that a project drawer containing a file explorer was bolted to the side of Vim’s interface. If we want to open a file by clicking its name in the project drawer, where would it open?

The window labeled C is active (as indicated by the shading), so that would seem to be the natural target. But the relationship between the project drawer and the active window is not immediately apparent. It would be easy to lose track of which window was active, leading to a surprise result when, on selecting a file from the project drawer, it didn’t open where you expected it to.

Now let’s remove our imaginary project drawer from this scenario and consider the way it actually works in Vim. If we run the :Explore command, the active window is replaced with a file explorer, as illustrated by frame 2 of the figure. There can be no doubt that when a file is selected it will load in the same window.

Think of each window as a playing card. One side of the card shows the contents of a file, and the other side shows the file explorer. When we run the :Explore command, the card for the active window flips over to show the side with the file explorer (frame 2 of the figure). After choosing the file we want to edit, we press <CR> and the card flips over again, this time showing the contents of the file that we just selected (frame 3 of the figure). After summoning the file explorer view, if we decide that we want to switch back to the buffer we were already editing, we can do so using the <C-^> command.

In a sense, we could say that Vim’s windows have two modes: one for working with files and one for working with directories. This model works together with Vim’s split window interface perfectly, whereas the notion of a project drawer doesn’t really fit.

Doing More with netrw

The netrw plugin doesn’t just let us explore the file system. We can create new files (netrw-%ⓘ) or directories (netrw-dⓘ), rename existing ones (netrw-renameⓘ), or delete them (netrw-delⓘ). For a demonstration, watch episode 15 of Vimcasts.[14]

	 	 We haven’t even touched on the killer feature that gives the plugin its name: netrw makes it possible to read and write files across a network. The plugin can use many protocols, including scp, ftp, curl, and wget, depending on what’s available on your system. To find out more, look up netrw-refⓘ.

Tip 45 Save Files to Nonexistent Directories

	 	 	 	 Vim is happy to let us edit a buffer whose path includes directories that don’t exist. It’s only when we attempt to write the buffer to a file that Vim objects. Here’s a quick tip on how to deal with this situation.

	 	 	 The :edit {file} command is most commonly used to open a file that already exists. But if we specify a filepath that doesn’t correspond to an existing file, then Vim will create a new empty buffer. If we press <C-g>, we’ll see that the buffer is labeled as「new file」(the <C-g> command echoes the name and status of the current file; see ctrl-Gⓘ). When we run the :write command, Vim will attempt to write the contents of that buffer to a new file using the filepath that was specified when the buffer was created.

If we run :edit {file} and specify a filepath that contains nonexistent directories, things can get a little awkward:

​=> ​:edit madeup/dir/doesnotexist.yet​

​=> ​:write​

​<= "madeup/dir/doesnotexist.yet" E212: Can't open file for writing

	 In this case, the madeup/dir directories do not exist. Vim creates a new buffer anyway, but this time it’s labeled as「new DIRECTORY.」It’s only when we attempt to write the buffer to disk that Vim raises an error. We can remedy this situation by calling the external mkdir program:

​=> ​:!mkdir -p %:h​

​=> ​:write​

The -p flag tells mkdir to create intermediate directories. See ​Open a File Relative to the Active File Directory​, for an explanation of what the %:h characters stand for.

Tip 46 Save a File as the Super User

	 	 	 	 	 Running Vim as the super user isn’t normal, but sometimes we have to save changes to a file that requires sudo permission. We can do so without restarting Vim by delegating the task to a shell process and running that with sudo.

This tip may not work in GVim and certainly won’t work on Windows. It does work on Unix systems when you run Vim inside a terminal, which is a common enough scenario to make this tip worthy of inclusion.

	 Let’s use the /etc/hosts file to demonstrate. The file is owned by root, but we’re logged in with username「drew,」so we have permission only to read this file:

​=> ​$ ls -al /etc/ | grep hosts​

​<= -rw-r--r-- 1 root wheel 634 6 Apr 15:59 hosts

​=> ​$ whoami​

​<= drew

We’ll open up the file in Vim as user drew:

​=> ​$ vim /etc/hosts​

The first thing to note is that if we press <C-g> to view the file status, Vim labels it as [readonly].

	 Let’s try to make a change and see what happens. We’ll run the Go commands to add a blank line at the end of the file. Vim echoes a message that reads「W10: Warning: Changing a readonly file.」Consider this a friendly reminder rather than an absolute rule. After showing the message, Vim proceeds by making the change anyway.

Vim won’t prevent us from making changes to a readonly buffer, but it will prevent us from saving the changes to disk in the usual manner:

​=> ​:write​

​<= E45: 'readonly' option is set (add ! to override)

Let’s follow the advice in the message and repeat the command with a trailing bang symbol (which can be read as「This time I mean it!」):

​=> ​:write!​

​<= "/etc/hosts" E212: Can't open file for writing

The problem here is that we don’t have permission to write the /etc/hosts file. Remember: it’s owned by root, and we’re running Vim as user drew. The remedy is this strange-looking command:

​=> ​:w !sudo tee % > /dev/null​

​<= Password:

​ W12: Warning: File "hosts" has changed and the buffer was

​ changed in Vim as well

​ [O]k, (L)oad File, Load (A)ll, (I)gnore All:

Vim requires interaction from us in two ways: first we have to enter the password for user drew (look away while I type it); then Vim warns us that the file has changed and prompts us with a menu of options. I recommend pressing l to load the file back into the buffer.

	 How does it work? The :write !{cmd} command sends the contents of the buffer as standard input to the specified {cmd}, which can be any external program (see :write_cⓘ). Vim is still running as user drew, but we can tell our external process to operate as the superuser. In this case, the tee utility is executed with sudo permissions, which means that it can write to the /etc/hosts file.

	 The % symbol has special meaning on Vim’s command line: it expands to represent the path of the current buffer (see :_%ⓘ), in this case /etc/hosts. So we can expand the final part of this command to read as follows: tee /etc/hosts > /dev/null. This command receives the contents of the buffer as standard input, using it to overwrite the contents of the /etc/hosts file.

Vim detects that the file has been modified by an external program. Usually that would mean that the contents of the buffer and the file were out of sync, which is why Vim prompts us to choose whether we want to keep the version in the buffer or load the version on disk. In this case, the file and buffer happen to have the same contents.

Footnotes

[12]

http://vimcasts.org/episodes/the-edit-command/

[13]

https://github.com/tpope/vim-rails

[14]

http://vimcasts.org/e/15

Copyright © 2016, The Pragmatic Bookshelf.

Part 3

Getting Around Faster

Motions are some of the most important commands for operating Vim. Not only do they let us move our cursor around, but when used in Operator-Pending mode, they also allow us to specify the range of text on which an operation will act. We’ll meet some of the most useful motions in this part of the book. We’ll also learn about Vim’s jump commands, which allow us to quickly navigate between files.

Chapter 8

Navigate Inside Files with Motions


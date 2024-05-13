The focus of this book is on mastering the core functionality of Vim, but some default settings may not be to your taste. Vim is highly configurable; we can make tweaks to suit our preferences.

Change Vim’s Settings on the Fly

Vim has hundreds of options that let us customize its behavior (see option-listⓘ for the full list). We can use the :set command to change them.

	 Let’s take the ‘ignorecase’ setting as an example (as discussed in Tip 73). This is a boolean option: it can either be on or off. We can enable it by running this:

​=> ​:set ignorecase​

To turn this feature off, we prefix the name of the setting with the word「no」:

​=> ​:set noignorecase​

	 	 If we append a trailing bang symbol after a boolean option, we can toggle the setting:

​=> ​:set ignorecase!​

	 If we append a trailing question mark, we can find out what the option is currently set to:

​=> ​:set ignorecase?​

​<= ignorecase

	 We can also append a trailing & symbol to reset any option to its default value:

​=> ​:set ignorecase&​

​=> ​:set ignorecase?​

​<= noignorecase

Some of Vim’s settings expect a value either as a string or as a number. For example, the ‘tabstop’ setting specifies the number of columns that a tab character should represent ('tabstop'ⓘ). We can set the value like this:

​=> ​:set tabstop=2​

	 We can make multiple assignments with a single set statement:

​=> ​:set ts=2 sts=2 sw=2 et​

	 	 	 The ‘softtabstop’, ‘shiftwidth’, and ‘expandtab’ settings also influence Vim’s treatment of indentation. To find out more, watch the Vimcasts episode about tabs and spaces.[35]

	 Most of Vim’s options also have a shorthand version. The ‘ignorecase’ setting can be abbreviated to ic, so we could toggle this feature by running :se ic! or disable it with :se noic. I tend to use shorthand option names for convenience when customizing Vim on the fly, but I prefer to use the longhand names in my vimrc for the sake of readability.

Vim’s settings usually apply globally, but some options are scoped to a window or buffer. For example, when we run :setlocal tabstop=4, it applies to the active buffer only. That means we can open several different files and customize the ‘tabstop’ setting for each one individually. If we wanted to apply the same value to all existing buffers, we could run the following:

​=> ​:bufdo setlocal tabstop=4​

The ‘number’ option can be configured on a per window basis. When we run :setlocal number, it enables line numbering for the active window. If we wanted to enable line numbering for every window, we could run this:

​=> ​:windo setlocal number​

	 The :setlocal command scopes the change to the current window or buffer (unless the option can only be set globally). If we were to run :set number, it would enable line numbering for the current window as well as set a new global default. Existing windows would retain their local settings, but new windows would adopt the new global setting.

Save Your Configuration in a vimrc File

	 	 	 Changing Vim’s settings on the fly is all very well, but if you have customizations that you are particularly fond of, wouldn’t it be handy if they persisted between editing sessions?

	 We can save our customizations by writing them to a file. Then we can use the :source {file} command to apply the settings from the specified {file} to our current editing session (:sourceⓘ). When sourcing a file, Vim executes each line as an Ex command, just as though it had been entered in Command-Line mode.

Suppose that we often work on files indented with two spaces. We could create a file with the appropriate settings and save it to disk:

customizations/two-space-indent.vim

​ ​" Use two spaces for indentation​

​ ​set​ tabstop=2

​ ​set​ softtabstop=2

​ ​set​ shiftwidth=2

​ ​set​ expandtab

Whenever we want to apply those settings to the current buffer, we run this command:

​=> ​:source two-space-indent.vim​

When changing settings on the fly, we start by typing a colon to switch to Command-Line mode. The leading colon isn’t necessary when saving settings to a file because the :source command assumes that each line of the file is to be executed as an Ex command.

When Vim starts up, it checks for the existence of a file called vimrc. If the file is found, then Vim automatically sources the contents of that file on launch. Using this mechanism, we can save our favorite customizations to the vimrc file, and they will be applied every time we start Vim.

	 	 Vim looks for a vimrc in several places (see vimrcⓘ). On Unix systems, Vim expects to find a file called ~/.vimrc. On Windows, the expected filename is $HOME/_vimrc. No matter which system you’re running, you can open the file from inside Vim by running this command:

​=> ​:edit $MYVIMRC​

	 $MYVIMRC is an environment variable in Vim, which expands to the path of the vimrc file. After saving changes to the vimrc file, we can load the new configuration into our Vim session by running this:

​=> ​:source $MYVIMRC​

If the vimrc file is the active buffer, then this can be shortened to :so %.

Apply Customizations to Certain Types of Files

	 	 	 Our preferences may vary from one type of file to another. For example, suppose that we work with a house style that advises two spaces for indentation in Ruby and four-column-wide tabs for JavaScript. We could apply these settings by putting the following lines in our vimrc:

customizations/filetype-indentation.vim

​ ​if​ has(​"autocmd"​)

​ ​filetype​ ​on​

​ autocmd FileType ​ruby​ ​setlocal​ ​ts​=2 ​sts​=2 ​sw​=2 et

​ autocmd FileType javascript ​setlocal​ ​ts​=4 ​sts​=4 ​sw​=4 noet

​ ​endif​

	 The autocmd declaration tells Vim to listen for an event and to execute the specified commands whenever that event fires (:autocmdⓘ). In this case we’re listening for the FileType event, which is triggered when Vim detects the type of the current file.

We can have more than one autocommand listening for the same event. Suppose that we want to use nodelint as the compiler for JavaScript files. We could add this line to the example above:

​ autocmd FileType javascript ​compiler​ nodelint

Both autocommands would be executed each time the FileType event was triggered on a JavaScript file.

	 Putting autocommands in the vimrc file works fine if you only have to make one or two customizations for a file type. But if we wanted to apply lots of settings to a particular kind of file, then it starts to look messy. The ftplugin is an alternative mechanism for applying customizations to file types. Instead of declaring our JavaScript preferences in the vimrc using autocommands, we could place them in a file called ~/.vim/after/ftplugin/javascript.vim:

customizations/ftplugin/javascript.vim

​ ​setlocal​ ​ts​=4 ​sts​=4 ​sw​=4 noet

​ ​compiler​ nodelint

This file is just like a regular vimrc, except that the settings will only be applied to JavaScript files. We could also create a ftplugin/ruby.vim file for Ruby customizations and another for each file type that we work with regularly. For more details, look up ftplugin-nameⓘ.

For the ftplugin mechanism to work, we must ensure that both file-type detection and plugins are enabled. Check that this line is present in your vimrc file:

​ filetype plugin on

Footnotes

[35]

http://vimcasts.org/e/2

Copyright © 2016, The Pragmatic Bookshelf.

You May Be Interested In…

Click a cover for more information

* * *


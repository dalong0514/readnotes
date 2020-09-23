ctags is an external program that scans through a codebase and generates an index of keywords. It was originally built into Vim, but with the release of Vim version 6, ctags became a separate project. That heritage is evident today in Vim’s tight integration with ctags.

Vim’s ctags support allows us to navigate around a codebase by quickly jumping to definitions of functions and classes. We’ll see how in Tip 104. As a secondary benefit, we can also use the output from ctags to generate a word list for autocompletion, as we’ll see in ​Tag Files​.

Tag navigation and tag autocompletion won’t work unless Vim knows where to look for an up-to-date index file. Tip 103, shows how to configure Vim to work with ctags. But first, let’s find out how to install and execute ctags.

Tip 102 Meet ctags

To use Vim’s tag navigation features, we must first install ctags. Then we’ll learn how to execute the program and understand the index that it generates.

Installing Exuberant Ctags

	 	 	 	 Linux users should be able to get ctags with their package manager. For example, on Ubuntu you can install it by running the following:

​=> ​$ sudo apt-get install exuberant-ctags​

OS X ships with a BSD program called ctags. Beware: this is not the same thing as Exuberant Ctags. You’ll have to install Exuberant Ctags yourself. Using homebrew, it’s as easy as this:

​=> ​$ brew install ctags​

Check that ctags is installed and that it’s in your path by running the following:

​=> ​$ ctags --version​

​<= Exuberant Ctags 5.8, Copyright (C) 1996-2009 Darren Hiebert

​ Compiled: Dec 18 2010, 22:44:26

​ ...

If you don’t get this message, you might have to modify your $PATH. Make sure that /usr/local/bin takes precedence over /usr/bin.

Indexing a Codebase with ctags

	 	 	 	 We can invoke ctags from the command line, giving it the path for one or more files that we would like it to index. The source code distributed with this book includes a small demo program consisting of three Ruby files. Let’s run ctags on this codebase:

​=> ​$ cd code/ctags​

​=> ​$ ls​

​<= anglophone.rb francophone.rb speaker.rb

​=> ​$ ctags *.rb​

​=> ​$ ls​

​<= anglophone.rb francophone.rb speaker.rb tags

	 Note that ctags has created a plain-text file called tags. It contains an index of the keywords from the three source files that ctags analyzed.

The Anatomy of a tags File

Let’s look inside the tags file we just generated. Note that some lines have been truncated to fit the page:

ctags/tags-abridged

​ !_TAG_FILE_FORMAT 2 /extended format/

​ !_TAG_FILE_SORTED 1 /0=unsorted, 1=sorted, 2=foldcase/

​ !_TAG_PROGRAM_AUTHOR Darren Hiebert //

​ !_TAG_PROGRAM_NAME Exuberant Ctags //

​ !_TAG_PROGRAM_URL http://ctags.sourceforge.net /official site/

​ !_TAG_PROGRAM_VERSION 5.8 //

​ Anglophone anglophone.rb /^class Anglophone < Speaker$/;" c

​ Francophone francophone.rb /^class Francophone < Speaker$/;" c

​ Speaker speaker.rb /^class Speaker$/;" c

​ initialize speaker.rb /^ def initialize(name)$/;" f

​ speak anglophone.rb /^ def speak$/;" f class:Anglophone

​ speak francophone.rb /^ def speak$/;" f class:Francophone

​ speak speaker.rb /^ def speak$/;" f class:Speaker

The tags file begins with a few lines of metadata. After that it lists one keyword per line, along with the filename and address where that keyword is defined in the source code. The keywords are arranged in alphabetical order, so Vim (or any text editor, for that matter) can rapidly locate them with a binary search.

Keywords Are Addressed by Pattern, Not by Line Number

The specification for the tags file format states that the address could be any Ex command. One option would be to use absolute line numbers. For example, we could make the cursor jump to an address on line 42 with the Ex command :42. But think of how brittle that could be. Adding just one new line at the top of a file would throw every address out of step.

		 Instead, ctags uses the search command to address each keyword (if you’re not convinced that search is an Ex command, try entering :/pattern). This method is more robust than using line numbers, but it’s still not perfect. What if the search command used to address a particular keyword had more than one match for a given file?

That situation shouldn’t arise, because the pattern can match as many lines of code as is necessary to produce a unique address. So long as the line length doesn’t exceed 512 characters, a tags file will remain backward compatible with vi. Of course, as a search pattern becomes longer, it, too, becomes brittle in its own way.

Keywords Are Tagged with Metadata

		 The classic tags file format only required three tab-separated fields: the keyword, the filename, and the address. But the extended format used today allows for additional fields at the end to provide metadata about the keyword. In this example, we can see that the Anglophone, Francophone, and Speaker keywords are labeled c for class, while initialize and speak are labeled f for function.

Extending ctags or Using a Compatible Tag Generator

ctags can be extended to work with languages that are not supported out of the box. By using the --regex, --langdef, and --langmap options, we can define regular expressions to create simple rules for indexing the key constructs of any language. We also have the option of droping down into C to write a parser. Parsers written in C tend to perform better than parsers specified as regular expressions, so if you’re working with a large codebase, this could make a big difference.

Instead of extending ctags, another option is to create a dedicated tool for indexing your chosen language. For example, gotags is a ctags-compatible tag generator for Go, itself implemented in Go.[24] It produces output in the same format as ctags, so it works seamlessly with Vim.

There’s nothing proprietary about the tags file format; it’s plain text. Anybody can write a script to generate tags files that Vim understands.

Tip 103 Configure Vim to Work with ctags

	 	 	 If we want to use Vim’s ctag navigation commands, we must ensure that the tags file is up-to-date and that Vim knows where to look for it.

Tell Vim Where to Find the Tags File

	 The ‘tags’ option specifies where Vim should look to find a tags file ('tags'ⓘ). When ./ is used in the ‘tags’ option, Vim replaces it with the path of the currently active file. We can inspect the defaults:

​=> ​:set tags?​

​<= tags=./tags,tags

With these settings, Vim looks for a tags file in the directory of the current file and in the working directory. Under certain conditions, if a match is found in the first tags file, Vim won’t even look in the second file (see tags-optionⓘ for more details). Using Vim’s default settings, we could keep a tags file in every subdirectory of our project. Or we could keep it simple by creating a global tags file in the project root directory.

If you run ctags often enough to keep the index up-to-date, then your tags file (or files) could show up in every source code check-in. To keep your commit history clean, tell your source control to ignore tags files.

Generate the tags File

	 As we saw in ​Indexing a Codebase with ctags​, ctags can be executed from the command line. But we needn’t leave Vim to regenerate the tags file.

Simple Case: Execute ctags Manually

We can invoke ctags directly from Vim by running the following:

​=> ​:!ctags -R​

		 Starting from Vim’s current working directory, this command would recurse through all subdirectories, indexing every file. The resulting tags file would be written in the current working directory.

If we were to tweak the command by adding such options as --exclude=.git or --languages=-sql, typing it out would become more of a chore. We could save ourselves some time by creating a mapping for it:

​=> ​:nnoremap <f5> :!ctags -R<CR>​

That lets us rebuild the index just by pressing the <F5> key, but we still have to remember periodically to generate the tags file. Now let’s consider a couple of options for automating this process.

Automatically Execute ctags Each Time a File is Saved

		 		 Vim’s autocommand feature allows us to invoke a command on each occurrence of an event, such as a buffer being created, opened, or written to file. We could set up an autocommand that invokes ctags every time we save a file:

​=> ​:autocmd BufWritePost * call system("ctags -R")​

This would re-index our entire codebase each time we saved changes to a single file.

Automatically Execute ctags with Version Control Hooks

		 Most source control systems provide hooks that allow us to execute a script in response to events on the repository. We can use these to instruct our source control to re-index the repository every time we commit our code.

In「Effortless Ctags with Git,」Tim Pope demonstrates how to set up hooks for the post-commit, post-merge, and post-checkout events.[25] The beauty of this solution is that it uses global hooks, so configuring each individual repository on your system is unnecessary.

Discussion

Each strategy for indexing our source code has its pros and cons. The manual solution is simplest, but having to remember to regenerate the index means that it’s more likely to go stale.

Using an autocommand to invoke ctags every time a buffer is saved ensures that our tags file is always up-to-date, but at what cost? For a small codebase, the time taken to run ctags may be imperceptible, but for larger projects, the lag may be long enough to interrupt our workflow. Also, this technique is blind to any changes that happen to a file outside of the editor.

Re-indexing our codebase on each commit strikes a good balance. Sure, the tags file might fall out of step with our working copy, but the errors are tolerable. The code that we’re actively working on is the code we’re least likely to want to navigate using tags. And remember that keywords in the tags file are addressed with a search command (see ​The Anatomy of a tags File​), which makes them reasonably robust in the face of changes.

Tip 104 Navigate Keyword Definitions with Vim’s Tag Navigation Commands

	 	 Vim’s ctags integration turns the keywords in our code into a kind of hyperlink, allowing us to jump rapidly to a definition. We’ll see how to use the Normal mode <C-]> and g<C-]> commands as well as their complementary Ex commands.

Jump to a Keyword Definition

	 	 Pressing <C-]> makes our cursor jump from the keyword under the cursor to the definition. Here it is in action:

KeystrokesBuffer Contents

{start}

​ require './speaker.rb'

​ class Anglophone < Speaker

​ def speak

​ puts "Hello, my name is #{@name}"

​ end

​ end

​ Anglophone.new('Jack').speak

<C-]>

​ require './speaker.rb'

​ class Anglophone < Speaker

​ def speak

​ puts "Hello, my name is #{@name}"

​ end

​ end

​ Anglophone.new('Jack').speak

In this case, the definition of the Anglophone class happens to be in the same buffer, but if we move our cursor onto the Speaker keyword and invoke the same command, we’ll switch to the buffer where that class is defined:

KeystrokesBuffer Contents

fS

​ require './speaker.rb'

​ class Anglophone < Speaker

​ def speak

​ puts "Hello, my name is #{@name}"

​ end

​ end

​ Anglophone.new('Jack').speak

<C-]>

​ class Speaker

​ def initialize(name)

​ @name = name

​ end

​ def speak

​ puts "#{name}"

​ end

​ end

	 	 As we navigate our codebase in this fashion, Vim maintains a history of the tags we’ve visited. The <C-t> command acts as the back button for our tag history. If we pressed it now, we would jump from the Speaker definition back to the Francophone definition, and if we pressed it a second time, it would take us back to where we started. For more information on interacting with the tag jump list, look up tag-stackⓘ.

Specify Where to Jump to When a Keyword Has Multiple Matches

	 Our previous example was straightforward because the demo codebase contains only one definition for the Speaker and Anglophone keywords. But suppose that our cursor was positioned on an invocation of the speak method, like this:

​ Anglophone.new('Jack').speak

The Speaker, Francophone, and Anglophone classes all define a function called speak, so which one will Vim jump to if we invoke the <C-]> command now? Try it yourself.

If a tag in the current buffer matches the keyword, it gets the highest priority. So in this case, we would jump to the definition of the speak function in the Anglophone class. Look up tag-priorityⓘ if you want to know more about how Vim ranks matching tags.

Instead of <C-]>, we could use the g<C-]> command. Both of these commands behave identically in the case when the current keyword has only a single match. But if it has multiple matches, then the g<C-]> command presents us with a list of choices from the tag match list:

​ # pri kind tag file

​ 1 F C f speak anglophone.rb

​ class:Anglophone

​ def speak

​ 2 F f speak francophone.rb

​ class:Francophone

​ def speak

​ 3 F f speak speaker.rb

​ class:Speaker

​ def speak

​ Type number and <Enter> (empty cancels):

As the prompt indicates, we can choose which destination we want to jump to by typing its number and pressing <CR>.

	 Suppose that we invoked <C-]> and found ourselves on the wrong definition. We could use the :tselect command to retrospectively pull up the menu of the tag match list. Or we could use the :tnext command to jump to the next matching tag without showing a prompt. As you might expect, this command is complemented with :tprev, :tfirst, and :tlast. Refer to the discussion of the unimpaired plugin, for a suggested set of mappings for these commands.

Use Ex Commands

	 	 	 	 We don’t have to move the cursor on top of a keyword to jump to its tag. We could just as well call an Ex command. For example, :tag {keyword} and :tjump {keyword} behave like the <C-]> and g<C-]> commands, respectively (see :tagⓘ and :tjumpⓘ).

At times, typing these commands can be quicker than maneuvering the cursor onto a keyword in the document—especially since Vim provides tab-completion for all keywords in the tags file. For example, we could type :tag Fran<Tab>, and Vim would expand our fragment to Francophone.

	 Also, these Ex commands can accept a regular expression when used in the form :tag /{pattern} or :tjump /{pattern} (note the leading / before {pattern}). For example, to navigate between any definitions whose keywords end with phone, we could invoke the following:

​=> ​:tjump /phone$​

​<= # pri kind tag

​ 1 F C c Anglophone anglophone.rb

​ class Anglophone < Speaker

​ 2 F c Francophone francophone.rb

​ class Francophone < Speaker

​ Type number and <Enter> (empty cancels):

Here are the commands that we can use to navigate our codebase using tags:

CommandEffect

<C-]>

Jump to the first tag that matches the word under the cursor

g<C-]>

Prompt user to select from multiple matches for the word under the cursor. If only one match exists, jump to it without prompting.

:tag {keyword}

Jump to the first tag that matches {keyword}

:tjump {keyword}

Prompt user to select from multiple matches for {keyword}. If only one match exists, jump to it without prompting.

:pop or <C-t>

			 Reverse through tag history

:tag

Advance through tag history

:tnext

			 Jump to next matching tag

:tprev

			 Jump to previous matching tag

:tfirst

			 Jump to first matching tag

:tlast

			 Jump to last matching tag

:tselect

			 Prompt user to choose an item from the tag match list

Footnotes

[24]

https://github.com/jstemmer/gotags

[25]

http://tbaggery.com/2011/08/08/effortless-ctags-with-git.html

Copyright © 2016, The Pragmatic Bookshelf.

Chapter 17

Compile Code and Navigate Errors

with the Quickfix List


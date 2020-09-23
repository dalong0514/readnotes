As we learned in the previous chapter, motions allow us to move around within a file. Jumps are similar, except that they can also move us between different files. Vim provides a couple of commands that turn keywords in the document into a wormhole, allowing us to jump quickly from one part of our codebase to another. That might seem disorienting at first, but Vim always traces our path by leaving a trail that we can easily follow to get back to where we came from.

Tip 56 Traverse the Jump List

	 	 Vim records our location before and after making a jump and provides a couple of commands for retracing our steps.

	 In web browsers, we’re used to using the back button to return to pages that we visited earlier. Vim provides a similar feature by way of the jump list: the <C-o> command is like the back button, while the complementary <C-i> command is like the forward button. These commands allow us to traverse Vim’s jump list, but what exactly is a jump?

Let’s start by making this distinction: motions move around within a file, whereas jumps can move between files (although we’ll soon see that some motions are also classified as jumps). We can inspect the contents of the jump list by running this command:

​=> ​:jumps​

​<= jump line col file/text

​ 4 12 2 <recipe id="sec.jump.list">

​ 3 114 2 <recipe id="sec.change.list">

​ 2 169 2 <recipe id="sec.gf">

​ 1 290 2 <recipe id="sec.global.marks">

​ >

​ Press Enter or type command to continue

Any command that changes the active file for the current window can be described as a jump. In the jump list, Vim records the cursor location before and after running such a command. For example, if we run the :edit command to open a new file (see Tip 42), then we can use the <C-o> and <C-i> commands to jump back and forth between the two files.

Moving directly to a line number with [count]G counts as a jump, but moving up or down one line at a time does not. The sentence-wise and paragraph-wise motions are jumps, but the character-wise and word-wise motions are not. As a rule of thumb, we could say that long-range motions may be classified as a jump, but short-range motions are just motions.

This table summarizes a selection of jumps:

CommandEffect

[count]G

Jump to line number

/pattern<CR>/?pattern<CR>/n/N

Jump to next/previous occurrence of pattern

%

Jump to matching parenthesis

(/)

Jump to start of previous/next sentence

{/}

Jump to start of previous/next paragraph

H/M/L

Jump to top/middle/bottom of screen

gf

Jump to file name under the cursor

<C-]>

Jump to definition of keyword under the cursor

’{mark}/`{mark}

Jump to a mark

	 	 The <C-o> and <C-i> commands themselves are never treated as a motion. This means that we can’t use them to extend the reach of a Visual mode selection, nor can we use them in Operator-Pending mode. I tend to think of the jump list as a breadcrumb trail that makes it easy to retrace my steps through the files that I’ve visited during the course of an editing session.

Vim can maintain multiple jump lists at the same time. In fact, each separate window has its own jump list. If we’re using split windows or multiple tab pages, then the <C-o> and <C-i> commands will always be scoped to the jump list of the active window.

Beware of Mapping the Tab Key

Try pressing <C-i> in Insert mode, and you should find that it has the same effect as pressing the <Tab> key. That’s because Vim sees <C-i> and <Tab> as the same thing.

Beware that if you attempt to create a mapping for the <Tab> key, it will also be triggered when you press <C-i> (and vice versa). That may not seem like a problem, but consider this: if you map the <Tab> key to something else, it will overwrite the default behavior of the <C-i> command. Think carefully about whether that’s a worthwhile trade-off. The jump list is much less useful if you can only traverse it in one direction.

Tip 57 Traverse the Change List

	 	 	 Vim records the location of our cursor after each change we make to a document. Traversing this change list is simple and can be the quickest way to get where we want to go.

Have you ever used the undo command followed immediately by redo? The two commands cancel each other out, but they have the side effect of placing the cursor on the most recent change. That could be useful if we wanted to jump back to the part of the document that we edited most recently. It’s a hack, but u<C-r> gets us there.

It turns out that Vim maintains a list of the modifications we make to each buffer during the course of an editing session. It’s called the change list (see changelistⓘ), and we can inspect its contents by running the following:

​=> ​:changes​

​<= change line col text

​ 3 1 8 Line one

​ 2 2 7 Line two

​ 1 3 9 Line three

​ >

​ Press ENTER or type command to continue

	 	 This example output shows that Vim records the line and column number for each change. Using the g; and g, commands, we can traverse backward and forward through the change list. As a memory aid for g; and g,, it may help to remember that the ; and , commands can be used to repeat or reverse the f{char} command (see Tip 50).

	 To jump back to the most recent modification in the document, we press g;. That places the cursor back on the line and column where it ended up after the previous edit. The result is the same as if we had pressed u<C-r>, except that we don’t make any transitory changes to the document.

Marks for the Last Change

	 	 	 Vim automatically creates a couple of marks that complement the change list. The `. mark always references the position of the last change (`.ⓘ), while the `^ mark tracks the position of the cursor the last time that Insert mode was stopped (`^ⓘ).

	 In most scenarios, jumping to the `. mark has the same effect as the g; command. Whereas the mark can only refer to the position of the most recent change, the change list stores multiple locations. We can press g; again and again, and each time it takes us to a location that was recorded earlier in the change list. The `., on the other hand, will always take us to the last item in the change list.

	 	 The `^ mark references the last insertion, which is slightly more specific than the last change. If we leave Insert mode and then scroll around the document, we can quickly carry on where we left off by pressing gi (giⓘ). In a single move, that uses the `^ mark to restore the cursor position and then switches back into Insert mode. It’s a great little time saver!

Vim maintains a change list for each individual buffer in an editing session. By contrast, a separate jump list is created for each window.

Tip 58 Jump to the Filename Under the Cursor

	 	 	 	 	 Vim treats filenames in our document as a kind of hyperlink. When configured properly, we can use the gf command to go to the filename under the cursor.

Let’s demonstrate with the jumps directory, from the source files distributed with this book. It contains the following directory tree:

​ practical_vim.rb

​ practical_vim/

​ core.rb

​ jumps.rb

​ more.rb

​ motions.rb

In the shell, we’ll start by changing to the jumps directory and then launching Vim. For this demonstration, I recommend using the -u NONE -N flags to ensure that Vim starts up without loading any plugins:

​=> ​$ cd code/jumps​

​=> ​$ vim -u NONE -N practical_vim.rb​

The practical_vim.rb file does nothing more than load the contents of the core.rb and more.rb files:

jumps/practical_vim.rb

​ require ​'practical_vim/core'​

​ require ​'practical_vim/more'​

Wouldn’t it be useful if we could quickly inspect the contents of the file specified by the require directive? That’s what Vim’s gf command is for. Think of it as go to file (gfⓘ).

Let’s try it out. We’ll start by placing our cursor somewhere inside the ’practical_vim/core’ string (for example, pressing fp would get us there quickly). If we try using the gf command now, we get this error:「E447: Can’t find file ‘practical_vim/core’ in path.」

	 Vim tries to open a file called practical_vim/core and reports that it doesn’t exist, but there is a file called practical_vim/core.rb (note the file extension). Somehow we need to instruct Vim to modify the filepath under the cursor by appending the rb file extension before attempting to open it. We can do this with the ‘suffixesadd’ option.

Specify a File Extension

	 The ‘suffixesadd’ option allows us to specify one or more file extensions, which Vim will attempt to use when looking up a filename with the gf command ('suffixesadd'ⓘ). We can set it up by running this command:

​=> ​:set suffixesadd+=.rb​

Now when we use the gf command, Vim jumps directly to the filepath under the cursor. Try using it to open more.rb. In that file, you’ll find a couple of other require declarations. Pick one, and open it up using the gf command.

Each time we use the gf command, Vim adds a record to the jump list, so we can always go back to where we came from using the <C-o> command (see Tip 56). In this case, pressing <C-o> the first time would take us back to more.rb, and pressing it a second time would take us back to practical_vim.rb.

Specify the Directories to Look Inside

	 In this example, each of the files referenced with the require statement was located relative to the working directory. But what if we referenced functionality that was provided by a third-party library, such as a rubygem?

	 That’s where the ‘path’ option comes in ('path'ⓘ). We can configure this to reference a comma-separated list of directories. When we use the gf command, Vim checks each of the directories listed in ‘path’ to see if it contains a filename that matches the text under the cursor. The ‘path’ setting is also used by the :find command, which we covered in Tip 43.

We can inspect the value of the path by running this command:

​=> ​:set path?​

​<= path=.,/usr/include,,

	 In this context, the . stands for the directory of the current file, whereas the empty string (delimited by two adjacent commas) stands for the working directory. The default settings work fine for this simple example, but for a larger project we would want to configure the ‘path’ setting to include a few more directories.

	 	 For example, it would be useful if the ‘path’ included the directories for all rubygems used in a Ruby project. Then we could use the gf command to open up the modules referenced by any require statements. For an automated solution, check out Tim Pope’s bundler.vim plugin,[17] which uses the project Gemfile to populate the ‘path’ setting.

Discussion

	 	 	 In the setup for this tip, I recommended launching Vim with plugins disabled. That’s because Vim is usually distributed with a Ruby file-type plugin, which handles the setup of ‘suffixesadd’ and ‘path’ options for us. If you do a lot of work with Ruby, I recommend getting the latest version of the file-type plugin from github because it’s actively maintained.[18]

	 	 The ‘suffixesadd’ and ‘path’ options can be set locally for each buffer, so they can be configured in different ways for different file types. Vim is distributed with file-type plugins for many languages besides Ruby, so in practice you won’t often have to set these options yourself. Even so, it’s worth understanding how the gf command works. It makes each filepath in our document behave like a hyperlink, which makes it easier to navigate through a codebase.

	 The <C-]> command has a similar role. It also requires a bit of setup (as discussed in Tip 103), but when it’s correctly configured, it allows us to jump from any method invocation directly to the place where it was defined. Skip ahead to Tip 104, for a demonstration.

While the jump list and change list are like breadcrumb trails that allow us to retrace our steps, the gf and <C-]> commands provide wormholes that transport us from one part of our codebase to another.

Tip 59 Snap Between Files Using Global Marks

	 	 	 	 	 	 A global mark is a kind of bookmark that allows us to jump between files. Marks can be especially useful for snapping back to a file after exploring a codebase.

	 The m{letter} command allows us to create a mark at the current cursor position (mⓘ). Lowercase letters create marks that are local to a buffer, whereas uppercase letters create global marks. Having set a mark, we can snap our cursor back to it with the `{letter} command (`ⓘ).

	 Try this: open up your vimrc file and press mV to set a global mark (mnemonic: V for vimrc). Switch to another file and then press `V, and you should snap back to the global mark you set in the vimrc file. By default, global marks are persisted between editing sessions (although this behavior can be configured; see 'viminfo'ⓘ). Now you can always open up your vimrc file with two keystrokes—that is, unless you set the global V mark to another location.

Set a Global Mark Before Going Code Diving

	 Global marks can be especially useful when we need to browse through a set of files and then quickly snap back to where we started. Suppose that we’re working on some code, and we want to find all occurrences of a method called fooBar in our codebase. We could use the :vimgrep command (covered in Tip 111):

​=> ​:vimgrep /fooBar/ **​

By default, :vimgrep jumps directly to the first match that it finds, which could mean switching to another file. At this point, we can use the <C-o> command to get back to where we were prior to running :vimgrep.

Let’s say that our codebase contains dozens of matches for the pattern fooBar. For each match :vimgrep finds, it creates a record in the quickfix list. Now suppose that we spend a minute or two traversing that list until eventually we find what we are looking for. Now we want to get back to where we were before we ran the :vimgrep command. How do we do it?

We could get there using the <C-o> command to reverse through the jump list, but it might take a while. This is a scenario where a global mark would come in handy. If we had run the mM command before invoking :vimgrep, then we could snap back in one move with the `M command.

Advice is rarely welcome when it goes「You should have started by doing X.」Global marks are only useful if we have the forethought to set them up correctly in advance. With practice, you’ll learn to recognize the scenarios where it would be useful to set a global mark.

Try to get into a habit of setting a global mark before using any commands that interact with the quickfix list, such as :grep, :vimgrep, and :make. The same goes for the commands that interact with the buffer and argument lists, such as :args {arglist} and :argdo (see Tip 38).

Remember, you can set up to twenty-six global marks, which is more than you’ll ever need. Use them liberally; set a global mark any time you see something that you might want to snap back to later.

Footnotes

[17]

https://github.com/tpope/vim-bundler

[18]

https://github.com/vim-ruby/vim-ruby

Copyright © 2016, The Pragmatic Bookshelf.

Part 4

Registers

	 Vim’s registers are simply containers that hold text. They can be used in the manner of a clipboard for cutting, copying, and pasting text, or they can be used to record a macro by saving a sequence of keystrokes. In this part of the book, we’ll master this core feature.

Chapter 10

Copy and Paste


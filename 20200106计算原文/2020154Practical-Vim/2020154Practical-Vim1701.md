The :global command combines the power of Ex commands with Vim’s pattern matching abilities—it runs an Ex command on each line that matches a specified pattern. Alongside the Dot Formula and macros, the :global command is one of Vim’s power tools for performing repetitive work efficiently.

Tip 98 Meet the Global Command

	 	 The :global command allows us to run an Ex command on each line that matches a particular pattern. Let’s start by studying its syntax.

The :global command takes the following form (see :gⓘ):

​ :[range] global[!] /{pattern}/ [cmd]

The default range for the :global command is the entire file (%). That sets it apart from most other Ex commands, including :delete, :substitute, and :normal, whose range is the current line (.) by default.

The {pattern} field integrates with search history. That means we can leave it blank and Vim will automatically use the current search pattern.

The [cmd] could be any Ex command except for another :global command. In practice, Ex commands that interact with the text in the document prove most useful, such as those in Table 7, ​Ex Commands That Operate on the Text in a Buffer​. If we don’t specify a [cmd], then Vim will use :print by default.

	 	 We can invert the behavior of the :global command either by running :global! or :vglobal (mnemonic: invert). Each of these tells Vim to execute [cmd] on each line that doesn’t match the specified pattern. In the next tip, we’ll see examples of both :global and :vglobal in action.

The :global command works by making two passes through the lines specified by [range]. In the first pass, Vim marks each line that matches the specified {pattern}. Then on the second pass, the [cmd] is executed for each marked line. The [cmd] can accept a range of its own, which allows us to operate on multiline regions. This powerful technique is demonstrated by Tip 101.

On the Etymology of Grep

Consider this abbreviated form of the :global command:

​=> ​:g/re/p​

re stands for regular expression, and p is short for :print, which is the default [cmd]. If we ignore the / symbols, we find the word「grep.」

Tip 99 Delete Lines Containing a Pattern

	 	 	 Combining the :global and :delete commands allows us to cut down the size of a file rapidly. We can either keep or discard all lines that match a {pattern}.

This file contains links to the first few episodes from the Vimcasts.org archive:

global/episodes.html

​ <ol>

​ <li>

​ <a href=​"/episodes/show-invisibles/"​>

​ Show invisibles

​ </a>

​ </li>

​ <li>

​ <a href=​"/episodes/tabs-and-spaces/"​>

​ Tabs and Spaces

​ </a>

​ </li>

​ <li>

​ <a href=​"/episodes/whitespace-preferences-and-filetypes/"​>

​ Whitespace preferences and filetypes

​ </a>

​ </li>

​ </ol>

Each list item contains two pieces of data: the title of an episode and its URL. We’ll use a :global command to expose each of these.

Delete Matching Lines with ‘:g/re/d’

What if we wanted to throw away everything except for the contents of each <a> tag? In this file, the contents of each link appear on a line of their own, while every other line of the file contains either an opening or a closing tag. So if we can devise a pattern that matches HTML tags, we could use it with the :global command to reject any lines that match the pattern.

These commands would do the trick:

​=> ​/\v\<\/?\w+>​

​=> ​:g//d​

If we run these two commands on the Vimcasts.org archive file, we’re left with this:

​ Show invisibles

​ Tabs and Spaces

​ Whitespace preferences and filetypes

Just like with the :substitute command, we can leave the search field of the :global command blank, and Vim will reuse the last search pattern (see Tip 91). That means that we can build our regular expression by starting with a broad match and then narrowing it, as demonstrated in Tip 85.

The regular expression uses very magic mode (covered in Tip 74). It matches an opening angle bracket (\<), followed by an optional forward slash (\/?), and then one or more word characters (\w+) followed by an end-of-word delimiter (>). This is not an all-purpose tag-matching regex, but it’s good enough for this particular case.

Keep Only Matching Lines with ‘:v/re/d’

	 This time we’ll switch things around. The :vglobal command, or :v for short, does the opposite of the :g command. That is, it executes a command on each line that does not match the specified pattern.

The lines containing the URLs are easy to identify: they all contain the href attribute. We can select only those lines by running this command:

​=> ​:v/href/d​

This can be read as「Delete each line that doesn’t contain href.」The result looks like this:

​ <a href="/episodes/show-invisibles/">

​ <a href="/episodes/tabs-and-spaces/">

​ <a href="/episodes/whitespace-preferences-and-filetypes/">

With a single command, we’ve condensed the file to the lines that interest us.

Tip 100 Collect TODO Items in a Register

	 	 	 	 	 Combining the :global and :yank commands allows us to collect all lines that match a {pattern} in a register.

This excerpt of code contains a couple of comments that lead with「TODO」:

global/markdown.js

​ Markdown.dialects.Gruber = {

​ lists: ​function​() {

​ ​// TODO: Cache this regexp for certain depths.​

​ ​function​ regex_for_depth(depth) { ​/* implementation */​ }

​ },

​ ​"`"​: ​function​ inlineCode( text ) {

​ ​var​ m = text.match( ​/​​(​​`+​​)(([\s\S]​​*​​?)\1)​​/​ );

​ ​if​ ( m && m[2] )

​ ​return​ [ m[1].length + m[2].length ];

​ ​else​ {

​ ​// TODO: No matching end code found - warn!​

​ ​return​ [ 1, ​"`"​ ];

​ }

​ }

​ }

Suppose that we wanted to collect all of the TODO items in one place. We could view them all at a glance by running this command:

​=> ​:g/TODO​

​<= // TODO: Cache this regexp for certain depths.

​ // TODO: No matching end code found - warn!

	 Remember, :print is the default [cmd] for the :global command. This simply echoes each line containing the word「TODO.」It’s not a great deal of use though, because the messages disappear as soon as we execute another command.

Here’s an alternative strategy: let’s yank each line containing the word「TODO」into a register. Then we can paste the contents of that register into another file and keep them around for later.

	 	 We’ll use the a register. First we’ll need to clear it by running qaq. Let’s break that down: qa tells Vim to start recording a macro into the a register, and then q stops the recording. We didn’t type anything while the macro was recording, so the register ends up empty. We can check that by running the following:

​=> ​:reg a​

​<= --- Registers ---

​ "a

Now we can go ahead and yank the TODO comments into the register:

​=> ​:g/TODO/yank A​

​=> ​:reg a​

​<= "a // TODO: Cache this regexp for certain depths.

​ // TODO: No matching end code found - warn!

	 	 The trick here is that we’ve addressed our register with an uppercase A. That tells Vim to append to the specified register, whereas a lowercase a would overwrite the register’s contents. We can read the global command as「For each line that matches the pattern /TODO/, append the entire line into register a.」

This time, when we run :reg a, we can see that the register contains the two TODO items from the document. (For the sake of legibility, I’ve formatted these items on two separate lines, but in Vim it actually shows a ^J symbol for newlines.) We could then open up a new buffer in a split window and run "ap to paste the a register into the new document.

Discussion

In this example, we’ve just collected two TODO items, which we could have done by hand quite rapidly. But this technique scales well. If the document contained a dozen TODO items, it would require the same effort on our part.

	 	 We could even combine the :global command with either :bufdo or :argdo to collect all TODO items from a set of files. I’ll leave that as an exercise for you, but look to Tip 36, for a hint at the workflow.

Here’s an alternative solution:

​=> ​:g/TODO/t$​

It uses the :t command, which we met in Tip 29. Rather than appending each TODO item to a register, we simply copy it to the end of the file. After running this command, we could jump to the end of the file to review the TODO items. This technique is more straightforward because it avoids messing around with registers. But it won’t work as neatly with the :argdo and :bufdo commands.

Tip 101 Alphabetize the Properties of Each Rule in a CSS File

	 	 	 	 	 	 When combining an Ex command with :global, we can also specify a range for our chosen [cmd]. Vim allows us to set the range dynamically using the :g/{pattern} as a reference point. Here we’ll see how we can exploit this fact to alphabetize the properties within each block of a CSS file.

We’ll use this CSS file for demonstration purposes:

global/unsorted.css

​1: html {

​- margin: 0;

​- padding: 0;

​- border: 0;

​5: font-size: 100%;

​- font: inherit;

​- vertical-align: baseline;

​- }

​- body {

​10: line-height: 1.5;

​- color: black;

​- background: white;

​- }

	 Suppose that we want to sort the properties of each rule into alphabetical order. We could do so using Vim’s built-in :sort command (:sortⓘ).

Sort Properties for a Single Block of Rules

Let’s start by trying out the :sort command on a subset of the file. (See Table 16, ​Sort a Subset of a File​.)

* * *

Table 16. Sort a Subset of a File

KeystrokesBuffer Contents

{start}

​ html {

​ margin: 0;

​ padding: 0;

​ border: 0;

​ font-size: 100%;

​ font: inherit;

​ vertical-align: baseline;

​ }

vi{

​ html {

​ margin: 0;

​ padding: 0;

​ border: 0;

​ font-size: 100%;

​ font: inherit;

​ vertical-align: baseline;

​ }

:’<,’>sort

​ html {

​ border: 0;

​ font-size: 100%;

​ font: inherit;

​ margin: 0;

​ padding: 0;

​ vertical-align: baseline;

​ }

* * *

	 We can easily select the lines inside a {} block using the vi{ text object. Running :’<,’>sort then rearranges the lines into alphabetical order. This technique works great if we just have to sort one block of rules at a time, but suppose that we had a style sheet containing hundreds of rules. Wouldn’t it be better if we could automate the process somehow?

Sort Properties for Every Block of Rules

We can sort the properties for every block of rules in the file with a single :global command. Say we run this command on our style sheet:

​=> ​:g/{/ .+1,/}/-1 sort​

We should end up with this result:

​ html {

​ border: 0;

​ font-size: 100%;

​ font: inherit;

​ margin: 0;

​ padding: 0;

​ vertical-align: baseline;

​ }

​

​

​ body {

​ background: white;

​ color: black;

​ line-height: 1.5;

​ }

The sort command has been executed inside the {} block for each rule. Our sample style sheet only contains a dozen lines, but this technique would work just as well for a longer CSS file.

This command is complex, but understanding how it works will help us to appreciate just how powerful the :global command can be. The standard form looks like this:

​ :g/{pattern}/[cmd]

Remember: Ex commands can usually accept a range themselves (as discussed in Tip 28). This is still true for the [cmd] in the context of a :global command. So we could expand the template as follows:

​ :g/{pattern}/[range][cmd]

The [range] for our [cmd] can be set dynamically using the match from :g/{pattern} as a reference point. Normally the . address stands for the line that the cursor is positioned on. But in the context of a :global command, it stands for each line in turn that matches the specified {pattern}.

We can break our command into two separate Ex commands. Let’s work our way backward from the end. This is a valid Ex command:

​=> ​:.+1,/}/-1 sort​

If we strip out the offsets from our range, it becomes simply .,/}/. We can interpret this as「from the current line up until the next line that matches the /}/ pattern.」The +1 and -1 offsets simply narrow the range to focus on the contents of the {} block. If we place our cursor on either line 1 or line 9 of our original unsorted CSS file, then this Ex command would alphabetize the rules inside the corresponding {} block.

We just need to position our cursor at the start of each {} block and then run the :.,/}/sort command to alphabetize the rules inside that block. Got that? Now try executing a search using the {pattern} from our :global command:

​=> ​/{/​

That places our cursor at the top of a {} block, right where we need it. Now let’s put our :global and [cmd] Ex commands back together:

​=> ​:g/{/ .+1,/}/-1 sort​

The { pattern matches the first line of each {} block. For every line that matches, the :sort command is executed on a [range] that terminates at the end of the {} block. The end result is that all CSS properties are alphabetized within each block of rules.

Discussion

A generalized form of this :global command goes like this:

​ :g/{start}/ .,{finish} [cmd]

We can read this as「For each range of lines beginning with {start} and ending with {finish}, run the specified [cmd].」

	 We could use the same formula for a :global command in combination with any Ex command. For example, suppose that we wanted to indent the specified ranges. We could do so with the :> Ex command (see :>ⓘ):

​=> ​:g/{/ .+1,/}/-1 >​

​<= 6 lines >ed 1 time

​ 3 lines >ed 1 time

	 	 Note that the :> command echoes a message each time it is invoked, whereas :sort doesn’t. We can mute these messages by prefixing our [cmd] with :silent (see :silⓘ):

​=> ​:g/{/sil .+1,/}/-1 >​

This technique is especially useful in cases where the :g/{pattern} matches a large number of lines.

Copyright © 2016, The Pragmatic Bookshelf.

Part 6

Tools

	 	「Do one thing, and do it well」is a principle of Unix philosophy. Vim provides wrapper commands that make it easy to call external programs such as make or grep. Some tasks require deeper integration with the text editor, so Vim provides native tools for spell checking and autocompletion and also provides a built-in :vimgrep command. In this part of the book we’ll study Vim’s toolbox and its interface for working with external tools.

Chapter 16

Index and Navigate

Source Code with ctags


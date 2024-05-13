Vim traces its ancestry back to vi, which is where the modal editing paradigm was conceived. In turn, vi traces its ancestry back to a line editor called ex, which is why we have Ex commands. The DNA of these early Unix text editors is preserved in modern Vim. For some line-oriented tasks, Ex commands are still the best tool for the job. In this chapter, we’ll learn how to use Command-Line mode, which exposes us to the vestiges of ex.

Tip 27 Meet Vim’s Command Line

Command-Line mode prompts us to enter an Ex command, a search pattern, or an expression. In this tip, we’ll meet a selection of Ex commands that operate on the text in a buffer, and we’ll learn about some of the special key mappings that can be used in this mode.

* * *

Table 7. Ex Commands That Operate on the Text in a Buffer

Command

Effect

		 		 		:[range]delete [x]

Delete specified lines [into register x]

:[range]yank [x]

Yank specified lines [into register x]

:[line]put [x]

Put the text from register x after the specified line

:[range]copy {address}

Copy the specified lines to below the line specified by {address}

:[range]move {address}

Move the specified lines to below the line specified by {address}

:[range]join

Join the specified lines

:[range]normal {commands}

Execute Normal mode {commands} on each specified line

:[range]substitute/{pattern}/{string}/[flags]

Replace occurrences of {pattern} with {string} on each specified line

:[range]global/{pattern}/[cmd]

Execute the Ex command [cmd] on all specified lines where the {pattern} matches

* * *

	 	 	 When we press the : key, Vim switches into Command-Line mode. This mode has some resemblance to the command line that we use in the shell. We can type the name of a command and then execute it by pressing <CR>. At any time, we can switch from Command-Line mode back to Normal mode by pressing <Esc>.

	 For historical reasons, the commands that we execute from Command-Line mode are called Ex commands (see ​On the Etymology of Vim (and Family)​). Command-Line mode is also enabled when we press / to bring up a search prompt or <C-r>= to access the expression register (see Tip 16). Some of the tricks in this chapter are applicable with each of these different prompts, but for the most part we’ll focus on Ex commands.

	 	 	 	 	 	 	 	 	 	 	 We can use Ex commands to read and write files (:edit and :write), to create tabs (:tabnew) or split windows (:split), or to interact with the argument list (:prev/:next) or the buffer list (:bprev/:bnext). In fact, Vim has an Ex command for just about everything (see ex-cmd-indexⓘ for the full list).

In this chapter, we’ll focus mainly on the handful of Ex commands we can use to edit text. Table 7, ​Ex Commands That Operate on the Text in a Buffer​, shows a selection of some of the most useful ones.

Most of these commands can accept a range. We’ll find out what this means in Tip 28. The :copy command is great for quickly duplicating a line, as we’ll see in ​Duplicate Lines with the ‘:t’ Command​. The :normal command provides a convenient way to make the same change on a range of lines, as we’ll see in Tip 30.

We’ll learn more about :delete, :yank, and :put commands in Chapter 10, ​Copy and Paste​. The :substitute and :global commands are very powerful, so they each get a chapter of their own. See Chapter 14, ​Substitution​, and Chapter 15, ​Global Commands​.

On the Etymology of Vim (and Family)

	 	 	 	 ed was the original Unix text editor. It was written at a time when video displays were uncommon. Source code was usually printed onto a roll of paper and edited on a teletype terminal.[7] Commands entered at the terminal would be sent to a mainframe computer for processing, and the output from each command would be printed. In those days, the connection between a terminal and a mainframe was slow, so much so that a quick typist could outpace the network, entering commands faster than they could be sent for processing. In this context, it was vital that ed provide a terse syntax. Consider how p prints the current line, while %p prints the entire file.

	 	 	 	 	 ed went through several generations of improvements, including em (dubbed the「editor for mortals」), en, and eventually ex.[8] By this time, video displays were more common. ex added a feature that turned the terminal screen into an interactive window that showed the contents of a file. Now it was possible to see changes as they were made in real time. The screen-editing mode was activated by entering the :visual command, or just :vi for short. And that is where the name vi comes from.

Vim stands for vi improved. That’s an understatement—I can’t stand to use regular vi! Look up vi-differencesⓘ for a list of Vim features that are unavailable in vi. Vim’s enhancements are essential, but it still owes much to its heritage. The constraints that guided the design of Vim’s ancestors have endowed us with a highly efficient command set that’s still valuable today.

Special Keys in Vim’s Command-Line Mode

	 	 Command-Line mode is similar to Insert mode in that most of the buttons on the keyboard simply enter a character. In Insert mode, the text goes into a buffer, whereas in Command-Line mode the text appears at the prompt. In both of these modes, we can use control key chords to trigger commands.

	 	 	 	 	 	 	 	 Some of these commands are shared between Insert mode and Command-Line mode. For example, <C-w> and <C-u> delete backward to the start of the previous word or to the start of the line, respectively. We can use <C-v> or <C-k> to insert characters that are not found on the keyboard. And we can insert the contents of any register at the command line using the <C-r>{register} command, just as we saw in Tip 15. Some Command-Line mode mappings are not found in Insert mode. We’ll meet a few of these in Tip 33.

	 At the command-line prompt, we are limited in the range of motions that we can use. The <left> and <right> arrow keys move our cursor one character at a time in either direction. Compared to the rich set of motions that we’re used to using in Normal mode, this can feel quite limiting. But as we’ll see in Tip 34, Vim’s command-line window provides all of the editing power that we could want for composing complex commands at the prompt.

Ex Commands Strike Far and Wide

	 	 It can sometimes be quicker to use an Ex command than to get the same job done with Vim’s Normal commands. For example, Normal commands tend to act on the current character or the current line, whereas an Ex command can be executed anywhere. This means that we can use Ex commands to make changes without having to move our cursor. But the greatest feature that distinguishes Ex commands is their ability to be executed across many lines at the same time.

As a general rule, we could say that Ex commands are long range and have the capacity to modify many lines in a single move. Or to condense that even further: Ex commands strike far and wide.

Tip 28 Execute a Command on One or More Consecutive Lines

Many Ex commands can be given a [range] of lines to act upon. We can specify the start and end of a range with either a line number, a mark, or a pattern.

	 	 	 One of the strengths of Ex commands is that they can be executed across a range of lines. We’ll use this short excerpt of HTML as an example:

cmdline_mode/practical-vim.html

​1: ​<!DOCTYPE html>​​<!-- -->​

​2: <html>​<!-- -->​

​3: <head><title>Practical Vim</title></head>​<!-- -->​

​4: <body><h1>Practical Vim</h1></body>​<!-- -->​

​5: </html>​<!-- -->​

	 To demonstrate, we’ll use the :print command, which simply echoes the specified lines below Vim’s command line. This command doesn’t perform any useful work, but it helps to illustrate which lines make up a range. Try replacing :print in each of the following examples with a command such as :delete, :join, :substitute, or :normal, and you should get a feel for how useful Ex commands can be.

Use Line Numbers as an Address

	 If we enter an Ex command consisting only of a number, then Vim will interpret that as an address and move our cursor to the specified line. We can jump to the top of the file by running the following:

​=> ​:1​

​=> ​:print​

​<= 1 <!DOCTYPE html>

This file contains only five lines. If we wanted to jump to the end of the file, we could enter :5 or we could use the special $ symbol:

​=> ​:$​

​=> ​:p​

​<= 5 </html>

Here we’ve used :p, which is the abbreviated form of :print. Instead of splitting up the two commands, we could roll them into a single incantation:

​=> ​:3p​

​<= 3 <head><title>Practical Vim</title></head>

That moves the cursor to line 3 and then echoes the contents of that line. Remember, we’re just using the :p command for illustrative purposes here. If we had issued the command :3d, then we would have jumped to line 3 and deleted it in a single move. The equivalent Normal mode commands would be 3G followed by dd. So this is one example where an Ex command can be quicker than a Normal mode command.

Specify a Range of Lines by Address

So far, we’ve specified addresses as a single line number. But we can also specify a range of lines. Here’s an example:

​=> ​:2,5p​

​<= 2 <html>

​ 3 <head><title>Practical Vim</title></head>

​ 4 <body><h1>Practical Vim</h1></body>

​ 5 </html>

That prints each line from 2 to 5, inclusive. Note that after running this command, the cursor would be left positioned on line 5. In general, we could say that a range takes this form:

​ :{start},{end}

Note that both the {start} and {end} are addresses. So far, we’ve looked at using line numbers for addresses, but we’ll soon see that using a pattern or a mark is also possible.

	 We can use the . symbol as an address to represent the current line. So, we can easily compose a range representing everything from here to the end of the file:

​=> ​:2​

​=> ​:.,$p​

​<= 2 <html>

​ 3 <head><title>Practical Vim</title></head>

​ 4 <body><h1>Practical Vim</h1></body>

​ 5 </html>

	 	 The % symbol also has a special meaning—it stands for all the lines in the current file:

​=> ​:%p​

​<= 1 <!DOCTYPE html>

​ 2 <html>

​ 3 <head><title>Practical Vim</title></head>

​ 4 <body><h1>Practical Vim</h1></body>

​ 5 </html>

	 This is equivalent to running :1,$p. Using this shorthand in combination with the :substitute command is very common:

​=> ​:%s/Practical/Pragmatic/​

This command tells Vim to replace the first occurrence of「Practical」with「Pragmatic」on each line. We’ll learn more about this command in Chapter 14, ​Substitution​.

Specify a Range of Lines by Visual Selection

	 	 Instead of addressing a range of lines by number, we could just make a visual selection. If we ran the command 2G followed by VG, we would make a visual selection that looks like this:

​ <!DOCTYPE html>

​ <html>

​ <head><title>Practical Vim</title></head>

​ <body><h1>Practical Vim</h1></body>

​ </html>

If we press the : key now, the command-line prompt will be prepopulated with the range :’<,’>. It looks cryptic, but you can think of it simply as a range standing for the visual selection. Then we can specify our Ex command, and it will execute on every selected line:

​=> ​:'<,'>p​

​<= 2 <html>

​ 3 <head><title>Practical Vim</title></head>

​ 4 <body><h1>Practical Vim</h1></body>

​ 5 </html>

This range can be really handy if we want to run a :substitute command on a subset of the file.

	 	 	 	 ’< is a mark standing for the first line of the visual selection, while ’> is the last line of the visual selection (see Tip 54, for more about marks). These marks persist even when we leave Visual mode. If you try running :’<,’>p straight from Normal mode, it will always act on the lines that most recently formed a Visual mode selection.

Specify a Range of Lines by Patterns

	 Vim also accepts a pattern as an address for an Ex command, such as the one shown here:

​=> ​:/<html>/,/<\/html>/p​

​<= 2 <html>

​ 3 <head><title>Practical Vim</title></head>

​ 4 <body><h1>Practical Vim</h1></body>

​ 5 </html>

This looks quite complex, but it follows the usual form for a range: :{start},{end}. The {start} address in this case is the pattern /<html>/, while the {end} address is /<\/html>/. In other words, the range begins on the line containing an opening <html> tag and ends on the line containing the corresponding closing tag.

In this particular case, we could achieve the same result using the address :2,5, which is shorter but more brittle. If we use patterns to specify the range, then our command will always operate on the entire <html></html> element, no matter how many lines it comprises.

Modify an Address Using an Offset

	 	 Suppose that we wanted to run an Ex command on every line inside the <html></html> block but not on the lines that contain the <html> and </html> tags themselves. We could do so using an offset:

​=> ​:/<html>/+1,/<\/html>/-1p​

​<= 3 <head><title>Practical Vim</title></head>

​ 4 <body><h1>Practical Vim</h1></body>

The general form for an offset goes like this:

​ :{address}+n

If n is omitted, it defaults to 1. The {address} could be a line number, a mark, or a pattern.

Suppose that we wanted to execute a command on a particular number of lines, starting with the current line. We could use an offset relative to the current line:

​=> ​:2​

​=> ​:.,.+3p​

The . symbol stands for the current line, so :.,.+3 is equivalent to :2,5 in this case.

Discussion

	 	 The syntax for defining a range is very flexible. We can mix and match line numbers, marks, and patterns, and we can apply an offset to any of them. This table summarizes a few of the symbols that can be used to create addresses and ranges for Ex commands:

SymbolAddress

1

First line of the file

$

Last line of the file

0

Virtual line above first line of the file

.

Line where the cursor is placed

’m

Line containing mark m

’<

Start of visual selection

’>

End of visual selection

%

The entire file (shorthand for :1,$)

Line 0 doesn’t really exist, but it can be useful as an address in certain contexts. In particular, it can be used as the final argument in the :copy {address} and :move {address} commands when we want to copy or move a range of lines to the top of a file. We’ll see examples of these commands in the next two tips.

When we specify a [range], it always represents a set of contiguous lines. It’s also possible to execute an Ex command on a set of noncontiguous lines using the :global command. We’ll learn more about that in Chapter 15, ​Global Commands​.

Tip 29 Duplicate or Move Lines Using ‘:t’ and ‘:m’ Commands

	 	 	 	 	 The :copy command (and its shorthand :t) lets us duplicate one or more lines from one part of the document to another, while the :move command lets us place them somewhere else in the document.

For demonstration purposes, we’ll use this shopping list:

cmdline_mode/shopping-list.todo

​ Shopping list

​ Hardware Store

​ Buy new hammer

​ Beauty Parlor

​ Buy nail polish remover

​ Buy nails

Duplicate Lines with the ‘:t’ Command

	 Our shopping list is incomplete: we also need to buy nails at the hardware store. To fix the list, we’ll reuse the last line of the file, creating a copy of it below「Hardware Store.」We can easily do so using the :copy Ex command:

KeystrokesBuffer Contents

{start}

​ Shopping list

​ Hardware Store

​ Buy new hammer

​ Beauty Parlor

​ Buy nail polish remover

​ Buy nails

:6copy.

​ Shopping list

​ Hardware Store

​ Buy nails

​ Buy new hammer

​ Beauty Parlor

​ Buy nail polish remover

​ Buy nails

The format of the copy command goes like this (see :copyⓘ):

​ :[range]copy {address}

In our example, the [range] was line 6. For our {address}, we used the . symbol, which stands for the current line. So we can read the :6copy. command as「Make a copy of line 6 and put it below the current line.」

We could shorten the :copy command to only two letters, as :co. Or we can be even more succinct by using the :t command, which is a synonym for :copy. As a mnemonic, you can think of it as copy TO. This table shows a few examples of the :t command in action:

CommandEffect

:6t.

Copy line 6 to just below the current line

:t6

Copy the current line to just below line 6

:t.

Duplicate the current line (similar to Normal mode yyp)

:t$

Copy the current line to the end of the file

:’<,’>t0

Copy the visually selected lines to the start of the file

	 	 	 Note that :t. duplicates the current line. Alternatively, we could achieve the same effect using Normal mode yank and put commands (yyp). The one notable difference between these two techniques for duplicating the current line is that yyp uses a register, whereas :t. doesn’t. I’ll sometimes use :t. to duplicate a line when I don’t want to overwrite the current value in the default register.

In this example, we could have used a variant of yyp to duplicate the line we wanted, but it would require some extra moving around. We would have to jump to the line we wanted to copy (6G), yank it (yy), snap back to where we started (<C-o>), and use the put command (p) to duplicate the line. When duplicating a distant line, the :t command is usually more efficient.

In ​Ex Commands Strike Far and Wide​, we observed the general rule that Normal commands act locally, whereas Ex commands are long range. This example demonstrates this principle in action.

Move Lines with the ‘:m’ Command

	 	 	 	 The :move command looks similar to the :copy command (see :moveⓘ):

​ :[range]move {address}

We can shorten it to a single letter: :m. Suppose that we want to move the Hardware Store section after the Beauty Parlor section. We could do so using the :move command as shown in Table 8, ​Moving a Set of Lines with the ‘:m’ Command​.

* * *

Table 8. Moving a Set of Lines with the ‘:m’ Command

KeystrokesBuffer Contents

{start}

​ Shopping list

​ Hardware Store

​ Buy nails

​ Buy new hammer

​ Beauty Parlor

​ Buy nail polish remover

​ Buy nails

Vjj

​ Shopping list

​ Hardware Store

​ Buy nails

​   Buy new hammer

​ Beauty Parlor

​ Buy nail polish remover

​ Buy nails

:’<,’>m$

​ Shopping list

​ Beauty Parlor

​ Buy nail polish remover

​ Buy nails

​ Hardware Store

​ Buy nails

​ Buy new hammer

* * *

Having made our visual selection, we simply have to run the command :’<,’>m$. Alternatively, we could run dGp. This breaks down like this: d to delete the visual selection, G to jump to the end of the file, and p to paste the text that was deleted.

	 	 Remember that the ’<,’> range stands for the visual selection. We could easily make another visual selection and then repeat the :’<,’>m$ command to move the selected text to the end of the file. Repeating the last Ex command is as easy as pressing @: (see Tip 31, for another example), so this method is more easily reproducible than using Normal mode commands.

Tip 30 Run Normal Mode Commands Across a Range

	 	 	 	 If we want to run a Normal mode command on a series of consecutive lines, we can do so using the :normal command. When used in combination with the dot command or a macro, we can perform repetitive tasks with very little effort.

	 Consider the example we met in Tip 2. We wanted to append a semicolon at the end of a series of lines. Using the Dot Formula allowed us to complete the task rapidly, but in that example we needed to make the change only on three consecutive lines. What if we had to make the same change fifty times? Using the Dot Formula, we would have to press j. fifty times. That makes a total of one hundred keystrokes!

There is a better way. To demonstrate, we’ll append a semicolon at the end of each line in this file. To save space, I’ve only included five lines, but if you can imagine instead that there are fifty lines, then this technique will seem more potent:

cmdline_mode/foobar.js

​ ​var​ foo = 1

​ ​var​ bar = ​'a'​

​ ​var​ baz = ​'z'​

​ ​var​ foobar = foo + bar

​ ​var​ foobarbaz = foo + bar + baz

We’ll start off as we did before, by changing the first line:

KeystrokesBuffer Contents

{start}

​ var foo = 1

​ var bar = 'a'

​ var baz = 'z'

​ var foobar = foo + bar

​ var foobarbaz = foo + bar + baz

A;<Esc>

​ var foo = 1;

​ var bar = 'a'

​ var baz = 'z'

​ var foobar = foo + bar

​ var foobarbaz = foo + bar + baz

We want to avoid executing the . command on each line one by one. Instead, we can use the :normal Ex command to execute the dot command across a range of lines:

KeystrokesBuffer Contents

jVG

​ var foo = 1;

​ var bar = ’a’

​ var baz = ’z’

​ var foobar = foo + bar

​ var foobarbaz = foo + bar + baz

:’<,’>normal .

​ var foo = 1;

​ var bar = 'a';

​ var baz = 'z';

​ var foobar = foo + bar;

​ var foobarbaz = foo + bar + baz;

The :’<,’>normal . command can be read as follows:「For each line in the visual selection, execute the Normal mode . command.」This technique works just as well whether we’re operating on five lines or fifty lines. The real beauty of it is that we don’t even have to count the lines—we can get away with selecting them in Visual mode.

In this case, we’ve used :normal to execute the dot command, but we can execute any Normal mode commands in the same way. For example, we could have solved the problem above with this single command:

​=> ​:%normal A;​

	 	 The % symbol is used as a range representing the entire file. So :%normal A; instructs Vim to append a semicolon at the end of every line of the file. Making this change involves switching into Insert mode, but Vim automatically reverts to Normal mode afterward.

Before executing the specified Normal mode command on each line, Vim moves the cursor to the beginning of the line. So we don’t have to worry about where the cursor is positioned when we execute the command. This single command could be used to comment out an entire JavaScript file:

​=> ​:%normal i//​

While it’s possible to use :normal with any normal command, I find it most powerful when used in combination with one of Vim’s repeat commands: either :normal . for simple repeats or :normal @q for more complex tasks. Skip ahead to Tip 68, and Tip 70, for a couple of examples.

In ​Ex Commands Strike Far and Wide​, we noted that Ex commands can change multiple lines at once. The :normal command allows us to combine the expressive nature of Vim’s Normal mode commands with the range of Ex commands. It’s a powerful combination!

For yet another alternative solution to the problem covered in this tip, refer to Tip 26.

Tip 31 Repeat the Last Ex Command

	 	 	 	 	 While the . command can be used to repeat our most recent Normal mode command, we have to use @: instead if we want to repeat the last Ex command. Knowing how to reverse the last command is always useful, so we’ll consider that, too, in our discussion.

In Chapter 1, ​The Vim Way​, we saw how the . command can be used to repeat the last change. But the dot command won’t replay changes made from Vim’s command line. Instead, we can repeat the last Ex command by pressing @: (see @:ⓘ).

	 	 For example, this command can be useful when iterating through items in the buffer list. We can step forward through the list with the :bn[ext] command and backward with the :bp[revious] command (Tip 37, discusses the buffer list in more detail). Suppose that we had a dozen or so items in the buffer list, and we wanted to take a look at each one of them. We could type this command once:

​=> ​:bnext​

Then we use @: to repeat the command. Note the similarity between this and the method for executing a macro (​Play Back a Sequence of Commands by Executing a Macro​). Also note that the : register always holds the most recently executed command line (see quote_:ⓘ). After running @: for the first time, we can subsequently repeat it with the @@ command.

	 Suppose that we got trigger-happy and fired the @: command too many times, overshooting our mark. How would we change direction then? We could execute the :bprevious command. But think about what would happen if we were to use the @: command again. It would go backward through the buffer list, which is the exact opposite of what it did before. That could be confusing.

	 	 In this case, a better option would be to use the <C-o> command (see Tip 56). Each time we run :bnext (or repeat it with the @: command), it adds a record to the jump list. The <C-o> command goes back to the previous record in the jump list.

We could run :bnext once and then repeat it as often as we like using the @: command. If we needed to back up, we could do so using the <C-o> command. Then, if we wanted to continue going forward through the buffer list, we could go back to using the @: command. Remember our mantra from Tip 4: act, repeat, reverse.

	 	 Vim provides an Ex command for just about everything. While it’s always possible to repeat the last Ex command by pressing @:, it’s not always straightforward to reverse the effects. The <C-o> trick covered in this tip also works for reversing the effects of :next, :cnext, and :tnext commands (and so on). Whereas, for each of the items in Table 7, ​Ex Commands That Operate on the Text in a Buffer​, we could undo their effects by pressing u.

Tip 32 Tab-Complete Your Ex Commands

	 	 	 	 Just like in the shell, we can use the <Tab> key to autocomplete commands at the prompt.

Vim is smart about picking suggestions for tab-completion. It looks at the context of what has already been typed at the command line and builds a list of suitable suggestions. For example, we could type this:

​=> ​:col<C-d>​

​<= colder colorscheme

The <C-d> command asks Vim to reveal a list of possible completions (see c_CTRL-Dⓘ). If we hit the <Tab> key, the prompt will cycle through colder, colorscheme, and then the original col again. We can scroll backward through the suggestions by pressing <S-Tab>.

	 Suppose we want to change the color scheme, but we can’t remember the name of the theme we want. We could use the <C-d> command to show all the options:

​=> ​:colorscheme <C-d>​

​<= blackboard desert morning shine

​ blue elflord murphy slate

​ darkblue evening pablo solarized

​ default koehler peachpuff torte

​ delek mac_classic ron zellner

This time, <C-d> shows a list of suggestions based on the color schemes that are available. If we wanted to enable the solarized theme, we could just type the letters「so」and then hit the Tab key to complete our command.

	 	 	 	 In many scenarios, Vim’s tab-completion does the right thing. If we type a command that expects a filepath as an argument (such as :edit or :write), then <Tab> will complete directories and filenames relative to the current working directory. With the :tag command we can autocomplete tag names. The :set and :help commands know about every configuration option in Vim.

We can even define the tab-completion behavior when creating our own custom Ex commands. To see what’s possible, check out :command-completeⓘ.

Choosing from Multiple Matches

	 When Vim finds only a single suggestion for tab-completion, it uses the entire match. But if Vim finds multiple suggestions, then one of several things could happen. By default, Vim expands the first suggestion when the Tab key is pressed for the first time. With each subsequent press of the Tab key, we can scroll through the remaining suggestions.

	 We can customize this behavior by tweaking the ‘wildmode’ option (see 'wildmode'ⓘ). If you’re used to working with the bash shell, then this setting will match your expectations:

​ ​set​ wildmode=longest,list

	 If you’re used to the autocomplete menu provided by zsh, you might want to try this instead:

​ ​set​ wildmenu

​ ​set​ wildmode=full

With the ‘wildmenu’ option enabled, Vim provides a navigable list of suggestions. We can scroll forward through the items by pressing <Tab>, <C-n>, or <Right>, and we can scroll backward through them with <S-Tab>, <C-p>, or <Left>.

Tip 33 Insert the Current Word at the Command Prompt

	 	 	 	 Even in Command-Line mode, Vim always knows where the cursor is positioned and which split window is active. To save time, we can insert the current word (or WORD) from the active document onto our command prompt.

At Vim’s command line, the <C-r><C-w> mapping copies the word under the cursor and inserts it at the command-line prompt. We can use this to save ourselves a bit of typing.

Suppose that we want to rename the tally variable in this excerpt to counter:

cmdline_mode/loop.js

​ ​var​ tally;

​ ​for​ (tally=1; tally <= 10; tally++) {

​ ​// do something with tally​

​ };

	 With our cursor positioned on the word tally, we could use the * command to search for each occurrence. (The * command is equivalent to typing the sequence /\<<C-r><C-w>\><CR>. See Tip 77, for a discussion of how \< and \> items work in a pattern.)

KeystrokesBuffer Contents

{start}

​ var tally;

​ for (tally=1; tally <= 10; tally++) {

​ // do something with tally

​ };

*

​ var tally;

​ for (tally=1; tally <= 10; tally++) {

​ // do something with tally

​ };

cwcounter<Esc>

​ var tally;

​ for (counter=1; tally <= 10; tally++) {

​ // do something with tally

​ };

When we press the * key, our cursor jumps forward to the next match, but the cursor ends up on the same word anyway. Typing cwcounter<Esc> makes the change.

	 We’ll carry out the remaining changes using a :substitute command. Since our cursor is on the word「counter,」we don’t need to type it out again. We can just use the <C-r><C-w> mapping to populate the replacement field:

​=> ​:%s//<C-r><C-w>/g​

That command doesn’t look very succinct when written down, but two keystrokes to insert a word ain’t bad. We didn’t have to type the search pattern either, thanks to the * command. Refer to Tip 91, to see why we can leave the search field blank like that.

While <C-r><C-w> gets the word under the cursor, we can instead use <C-r><C-a> if we want to get the WORD (for an explanation, see Tip 49). See c_CTRL-R_CTRL-Wⓘ for more details. We’ve used the :substitute command in this example, but these mappings can be used with any Ex command.

For another application, try opening your vimrc file, place your cursor on a setting, and then type :help <C-r><C-w> to look up the documentation for that setting.

Tip 34 Recall Commands from History

	 	 	 	 	 Vim records the commands that we enter in Command-Line mode and provides two ways of recalling them: scrolling through past command-lines with the cursor keys or dialing up the command-line window.

Vim keeps a history of our activity in Command-Line mode. We can easily recall previous commands, so there’s no need to type out a long Ex command at the prompt more than once.

	 To begin with, let’s switch to Command-Line mode by pressing the : key. Leave the prompt empty; then press the <Up> arrow key. The command line should be populated with the most recent Ex command that we executed. We can use the <Up> key again to go further back through our Ex command history or use the <Down> key to go in the opposite direction.

	 Now try typing :help, followed by the <Up> key. Again, this should scroll through previous Ex commands, but instead of showing everything, the list will be filtered to only include Ex commands that started with the word「help.」

	 By default, Vim records the last twenty commands. With memory becoming ever cheaper in today’s computers, we can probably afford to up this limit by changing the ‘history’ option. Try adding this line to your vimrc:

​ set history=200

Note that history is not recorded just for the current editing session. It persists even when we quit and relaunch Vim (see viminfoⓘ). Increasing the number of items recorded in history can be really useful.

	 	 	 As well as recording a history of Ex commands, Vim keeps a separate record of our search history. If we press / to bring up the search prompt, we can also scroll backward and forward through previous searches with the <Up> and <Down> keys. The search prompt is, after all, just another form of Command-Line mode.

Meet the Command-Line Window

	 Like Insert mode, Command-Line mode is fine for composing something from scratch, but it’s not a comfortable place to edit text.

Suppose we’re working on a simple Ruby script. Each time we make a change, we find ourselves running the following two commands:

​=> ​:write​

​=> ​:!ruby %​

After running these two commands in quick succession a couple of times, we realize that we could streamline our workflow by folding them into a single command line. This way we can dial up one complete command from our history and replay it:

​=> ​:write | !ruby %​

	 Each of these commands is already in our history, so we shouldn’t have to type the entire command line from scratch. But how can we merge two records from our history into one? Press q: and meet the command-line window (see cmdwinⓘ).

The command-line window is like a regular Vim buffer, where each line contains an item from our history. With the k and j keys, we can move backward and forward through our history. Or we can use Vim’s search feature to find the line that we’re looking for. When we press the <CR> key, the contents of the current line are executed as an Ex command.

The beauty of the command-line window is that it allows us to change historical commands using the full modal editing power of Vim. We can navigate with any of the motions we’re accustomed to using in Normal mode. We can operate on visual selections or switch to Insert mode. We can even run Ex commands on the contents of the command-line window!

Having summoned the command-line window by pressing q:, we could solve our problem as follows:

KeystrokesBuffer Contents

{start}

​ write

​ !ruby %

A|<Esc>

​ write |

​ !ruby %

J

​ write | !ruby %

:s/write/update

​ update | !ruby %

Pressing <CR> would then execute the :update | !ruby % command as though we had typed it into the command line.

	 When the command-line window is open, it always gets the focus. That means we can’t switch to other windows except by dismissing the command-line window. We can close the command-line window by running the :q command (just like any ordinary Vim window) or by pressing <CR>.

Note that when we press <CR> in the command-line window, the command is executed in the context of the active window: that is, the window that was active before the command-line window was summoned. Vim doesn’t indicate which is the active window when the command-line window is open, so pay attention if you’re using split windows!

What if halfway through composing an Ex command at the prompt, we realize that we need more editing power? In Command-Line mode, we can use the <C-f> mapping to switch to the command-line window, preserving a copy of the command that was typed at the prompt. This table summarizes a few of the methods for summoning the command-line window:

CommandAction

q/

Open the command-line window with history of searches

q:

Open the command-line window with history of Ex commands

ctrl-f

		 		 Switch from Command-Line mode to the command-line window

It’s easy to mix up the q: and :q commands. I’m sure that we’ve all opened the command-line window by accident when we actually meant to quit Vim! It’s a shame, because this feature is really useful, but many people are frustrated by their first (accidental) encounter with it. Skip ahead to Tip 85, for another example of the command-line window in action.

Tip 35 Run Commands in the Shell

	 	 	 We can easily invoke external programs without leaving Vim. Best of all, we can send the contents of a buffer as standard input to a command or use the standard output from an external command to populate our buffer.

The commands discussed in this tip work best when used from Vim inside a terminal. If you’re using GVim (or MacVim), then things may not work quite as smoothly. That shouldn’t come as a great surprise. It’s much easier for Vim to delegate work to the shell if Vim itself is already running inside a shell. GVim does some things better, but this is one area where terminal Vim has the edge.

Executing Programs in the Shell

	 	 From Vim’s Command-Line mode, we can invoke external programs in the shell by prefixing them with a bang symbol (see :!ⓘ). For example, if we want to examine the contents of the current directory, we could run the following:

​=> ​:!ls​

​<= duplicate.todo loop.js

​ emails.csv practical-vim.html

​ foobar.js shopping-list.todo

​ history-scrollers.vim

​

​ Press ENTER or type command to continue

Note the difference between :!ls and :ls—the former calls the ls command in the shell, whereas :ls calls Vim’s built-in command, which shows the contents of the buffer list.

	 On Vim’s command line, the % symbol is shorthand for the current file name (see cmdline-specialⓘ). We can exploit this to run external commands that do something with the current file. For example, if we’re working on a Ruby file, we could execute it by running this:

​=> ​:!ruby %​

Vim also provides a set of filename modifiers, which allow us to extract information from the current filename, such as its path or extension (see filename-modifiersⓘ). Skip ahead to Tip 45, for an example of how these can be used.

	 The :!{cmd} syntax is great for firing one-off commands, but what if we want to run several commands in the shell? In that case, we can use Vim’s :shell command to start an interactive shell session (see :shellⓘ):

​=> ​:shell​

​=> ​$ pwd​

​<= /Users/drew/books/PracticalVim/code/cmdline_mode

​=> ​$ ls​

​<= duplicate.todo loop.js

​ emails.csv practical-vim.html

​ foobar.js shopping-list.todo

​ history-scrollers.vim

​=> ​$ exit​

	 The exit command kills the shell and returns us to Vim.

Putting Vim in the Background

	 	 The :shell command is a feature provided by Vim, which lets us switch to an interactive shell. But if we’re already running Vim in a terminal, then we also have access to built-in shell commands. For example, the bash shell supports job control, which allows us to suspend a job by putting it into the background and then lets us resume it later by bringing it back into the foreground.

Suppose that we’re running Vim inside a bash shell and we want to execute a series of shell commands. Pressing Ctrl-z suspends the process that’s running Vim and returns control to bash. The Vim process sits idle in the background, allowing us to interact with our bash session as normal. We can inspect the list of jobs by running this command:

​=> ​$ jobs​

​<= [1]+ Stopped vim

	 	 	 In bash, we can use the fg command to resume a suspended job, bringing it back into the foreground. That brings Vim back to life exactly as we left it. The Ctrl-z and fg commands are quicker and easier to use than Vim’s equivalent :shell and exit commands. For more information, run man bash and read the section on job control.

Using the Contents of a Buffer for Standard Input or Output

When we use the :!{cmd} syntax, Vim echoes output from the {cmd}. This works fine if the command produces little or no output, but it’s not very helpful if the command produces many lines of output. As an alternative, we can use the :read !{cmd} command, which puts the output from the {cmd} into our current buffer (see :read!ⓘ).

	 	 The :read !{cmd} command lets us direct standard output into a buffer. As you might expect, the :write !{cmd} does the inverse: it uses the contents of the buffer as standard input for the specified {cmd} (see :write_cⓘ). Skip ahead to Tip 46, to see an example of this feature in use.

The bang symbol can take on different meanings depending on where it is placed within the command line. Compare these commands:

​=> ​:write !sh​

​=> ​:write ! sh​

​=> ​:write! sh​

The first two commands pass the contents of the buffer as standard input to the external sh command. The last command writes the contents of the buffer to a file called sh by calling the :write! command. In this case, the bang tells Vim to overwrite any existing sh file. As you can see, the placement of the bang symbol can drastically alter the outcome. Take care when composing this sort of command!

The effect of the :write !sh command is that each line of the current buffer is executed in the shell. Refer to rename-filesⓘ for a nice example of this command in use.

Filtering the Contents of a Buffer Through an External Command

	 	 	 The :!{cmd} command takes on a different meaning when it’s given a range. The lines specified by [range] are passed as standard input for the {cmd}, and then the output from {cmd} overwrites the original contents of [range]. Or to put it another way, the [range] is filtered through the specified {cmd} (see :range!ⓘ). Vim defines a filter as「a program that accepts text as standard input, changes it some way, and sends it to standard output.」

As a demonstration, let’s use the external sort command to rearrange the records in this CSV file:

cmdline_mode/emails.csv

​ first name,last name,email

​ john,smith,john@example.com

​ drew,neil,drew@vimcasts.org

​ jane,doe,jane@example.com

We’ll sort the records by the second field: last name. We can use the -t’,’ option to tell the sort command that fields are separated with commas, and we can use the -k2 flag to indicate that the second field is to be used for the sort.

The first line of the file contains header information. We want to leave it at the top of the file, so we’ll exclude it from the sort operation by using a range of :2,$. This command line does what we want:

​=> ​:2,$!sort -t',' -k2​

	 	 The records in our CSV file should now be sorted by last name:

​ first name,last name,email

​ jane,doe,jane@example.com

​ drew,neil,drew@vimcasts.org

​ john,smith,john@example.com

	 Vim provides a convenient shortcut for setting the range of a :[range]!{filter} command such as this. The !{motion} operator command drops us into Command-Line mode and prepopulates the [range] with the lines covered by the specified {motion} (see !ⓘ). For example, if we place our cursor on line 2 and then invoke !G, Vim opens a prompt with the :.,$! range set up for us. We still have to type out the rest of the {filter} command, but it saves a little work.

Discussion

	 When operating Vim, we’re never more than a couple of keystrokes away from the shell. This table summarizes a selection of the most useful methods for calling external commands:

CommandEffect

:shell

		 		 Start a shell (return to Vim by typing exit)

		 		 :!{cmd}

Execute {cmd} with the shell

		 		 :read !{cmd}

Execute {cmd} in the shell and insert its standard output below the cursor

		 		 		 :[range]write !{cmd}

Execute {cmd} in the shell with [range] lines as standard input

		 		 		 :[range]!{filter}

Filter the specified [range] through external program {filter}

Vim gives special treatment to some commands. For example, both make and grep have wrapper commands. Not only are they easy to execute from inside Vim, but their output is parsed and used to populate the quickfix list. These commands are covered in greater depth in both Chapter 17, ​Compile Code and Navigate Errors

with the Quickfix List​, and Chapter 18, ​Search Project-Wide

with grep, vimgrep, and Others​.

Tip 36 Run Multiple Ex Commands as a Batch

If we need to execute a sequence of Ex commands, we can save ourselves work by putting those commands in a script. Next time we want to run those commands, we can source the script rather than typing the commands one by one.

This file contains links to the first couple of episodes from the Vimcasts archive:

cmdline_mode/vimcasts/episodes-1.html

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

​ </ol>

We need to modify this into a plain-text format showing the title followed by the URL:

cmdline_mode/vimcasts-episodes-1.txt

​ Show invisibles: http://vimcasts.org/episodes/show-invisibles/

​ Tabs and Spaces: http://vimcasts.org/episodes/tabs-and-spaces/

Let’s suppose we anticipate having to make these same transformations across a series of files that follow a similar format. We’ll look at a couple of different ways we could approach this.

Run Ex Commands One by One

It might be possible to make this transformation using a single :substitute command, but my preference would be to break this up into several small tasks. This sequence of Ex commands is one possible solution:

​=> ​:g/href/j​

​=> ​:v/href/d​

​<= 8 fewer lines

​=> ​:%norm A: http://vimcasts.org​

​=> ​:%norm yi"$p​

​=> ​:%s/\v^[^\>]+\>\s//g​

You don’t have to understand what each of these commands does to follow the rest of this tip, but if you’re curious, here’s a brief outline. The :global and :vglobal commands work together to collapse the file down into two lines that contain the information we need, albeit in the wrong order (Tip 99). The :normal commands append the URL at the end of the line (Tip 30). And the :substitute command removes the opening <a href=""> tag. As always, the best way to understand these commands is to try them out for yourself.

Write Ex Commands to a Script and Source It

Instead of executing these commands one by one, we could put them all into a file and save it to disk. Let’s call it batch.vim. (Using the .vim extension will make Vim use the correct syntax highlighting.) Each line of this file corresponds to a command line from the workflow outlined earlier. In this context we don’t need to prefix each line with a : character. Personally, I prefer to use the longhand names for Ex commands when putting them in a script. Saving keystrokes is less of a concern than making the script easy to read.

cmdline_mode/batch.vim

​ global​/href/​​join​

​ vglobal​/href/​delete

​ %normal A: http:​//​vimcasts.org

​ %normal yi"$​p​

​ %substitute​/\v^[^\>]+\>\s/​/​g​

We can use the :source command to execute the batch.vim script (see sourceⓘ). Each line of the script is executed as an Ex command, just as though we had typed it at Vim’s command line. You’ve probably come across the :source command before in another context: it’s commonly used to load configuration settings from a vimrc file at runtime. (See ​Save Your Configuration in a vimrc File​, for more details.)

I suggest you try this out for yourself. You can download the source code from Practical Vim’s book page on the Pragmatic Bookshelf site. Before opening Vim, change to the cmdline_mode directory, where you’ll find both the batch.vim and episodes-1.html files.

​=> ​$ pwd​

​<= ~/dnvim2/code/cmdline_mode

​=> ​$ ls *.vim​

​<= batch.vim history-scrollers.vim

​=> ​$ vim vimcasts/episodes-1.html​

Now we can execute our script:

​=> ​:source batch.vim​

With that single command line, we’ve executed each of the Ex commands from batch.vim. If you change your mind, you can undo those changes by pressing the u key once.

Source the Script to Change Multiple Files

There’s little point in saving our Ex commands to a file if we’re only going to execute the script one time. This trick comes into its own if we want to run that same sequence of Ex commands several times.

The code samples provided with this book include a few files with the same format as the episodes-1.html file. Make sure that you’re in the cmdline_mode directory and launch Vim:

​=> ​$ pwd​

​<= ~/dnvim2/code/cmdline_mode

​=> ​$ ls vimcasts​

​<= episodes-1.html episodes-2.html episodes-3.html

​=> ​$ vim vimcasts/*.html​

Launching Vim with a wildcard will populate the argument list with all of the files that match that pattern. We could step through those files one by one, sourcing our batch.vim for each one:

​=> ​:args​

​<= [vimcasts/episodes-1.html] vimcasts/episodes-2.html vimcasts/episodes-3.html

​=> ​:first​

​=> ​:source batch.vim​

​=> ​:next​

​=> ​:source batch.vim​

​<= etc.

Or better still, we could use the :argdo command (:argdoⓘ):

​=> ​:argdo source batch.vim​

Boom! With a single command we’ve executed each of the Ex commands in batch.vim across each of the files in the argument list.

I’ve chosen to illustrate this technique using a varied selection of Ex commands to demonstrate what’s possible. In practice, I most commonly use this technique to execute one or more :substitute commands if I find myself using them again and again. I’ll often discard the batch.vim file after use, but I might put it under source control if I think it could be useful in the future.

Footnotes

[7]

http://en.wikipedia.org/wiki/Teleprinter

[8]

http://www.theregister.co.uk/2003/09/11/bill_joys_greatest_gift/

Copyright © 2016, The Pragmatic Bookshelf.

Part 2

Files

In this part of the book, we’ll learn how to work with files and buffers. Vim lets us work on multiple files in a single editing session. We can view them one at a time or divide our workspace into split windows or tabs, each containing a separate buffer. We’ll look at several different ways of opening files from inside Vim. We’ll also learn a couple of workarounds for common gotchas that may prevent us from saving our buffers to a file.

Chapter 6

Manage Multiple Files


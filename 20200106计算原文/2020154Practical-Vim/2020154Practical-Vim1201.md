Vim’s cut, copy, and paste functionality differs from what you may be used to. For a start, the terminology is different, as we’ll see in ​Vim’s Terminology Versus the World​. In Tip 60, we’ll learn how to use Vim’s delete, yank, and put commands for a handful of common cases.

Instead of dealing with a single system-wide clipboard, Vim provides a couple of dozen registers where we can store regions of text. We’ll learn more about Vim’s registers in Tip 61. Vim’s put command is smart about how it treats line-wise and character-wise text, as we’ll see in Tip 63. The put command has some interesting quirks when used from Visual mode, as we’ll discover in Tip 62.

Finally, in Tip 64, we’ll learn about how to use the system paste command inside Vim without producing strange effects.

Tip 60 Delete, Yank, and Put with Vim’s Unnamed Register

	 	 	 	 Vim’s delete, yank, and put commands are designed to make common tasks easy by default. We’ll study a few problems that can easily be solved using Vim’s unnamed register, and then we’ll finish by looking at a task that requires a better understanding of how Vim’s registers work.

	 	 Normally when we discuss cut, copy, and paste, we talk about putting text on a clipboard. In Vim’s terminology, we don’t deal with a clipboard but instead with registers. In Tip 61, we’ll see that Vim has multiple registers, and we can specify which ones we want to use. But let’s start off by looking at what can be done using the unnamed register.

Transposing Characters

	 	 I consistently misspell some words. Over time, I may notice that I habitually mistype a certain word, and then I can train myself out of it. But some spelling mistakes are more haphazard. The most common typing error that I make is to get two characters in the wrong order. Vim makes it easy to fix such mistakes.

Suppose that we’re typing out the title of this book when we make such a transposition error:

KeystrokesBuffer Contents

{start}

​ Practica lvim

F

​ Practica lvim

x

​ Practicalvim

p

​ Practical vim

	 	 Here we’ve typed the space too soon, but it’s easily mended. The F command places our cursor on the first of the two characters that we want to swap (see Tip 50). The x command cuts the character under the cursor, placing a copy of it in the unnamed register. Then the p command pastes the contents of the unnamed register after the cursor position. Taken together, the xp commands can be considered as「Transpose the next two characters.」

Transposing Lines

	 	 	 We can just as easily transpose the order of two lines of text. Instead of using the x command to cut the current character, we can use the dd command, which cuts the current line, placing it into the unnamed register:

KeystrokesBuffer Contents

{start}

​ 2) line two

​ 1) line one

​ 3) line three

dd

​ 1) line one

​ 3) line three

p

​ 1) line one

​ 2) line two

​ 3) line three

The p command knows that this time we’re dealing with a line-wise chunk of text, so it does the thing we would expect: it pastes the contents of the unnamed register after the current line. Remember, when we pressed xp in the previous example, the p command pasted after the current character.

The ddp sequence could be considered to stand for「Transpose the order of this line and its successor.」

Duplicating Lines

	 	 	 	 	 If we want to create a new line of text that’s broadly similar to another line but with one or two small differences, we can give ourselves a head start by duplicating a line and using it as a template. In Vim, a line-wise yank followed by a put operation does the trick:

KeystrokesBuffer Contents

{start}

​ 1) line one

​ 2) line two

yyp

​ 1) line one

​ 2) line two

​ 2) line two

Note the similarities between these two sequences, ddp and yyp. The first does a line-wise cut and paste, which effectively transposes the order of two lines. The second sequence does a line-wise copy and paste, which effectively duplicates a line.

Oops! I Clobbered My Yank

So far, Vim’s delete, yank, and put operations are looking quite intuitive. They make common tasks trivially easy to perform. Now let’s look at a scenario where things don’t work out quite so smoothly. Start off with this sample:

copy_and_paste/collection.js

​ collection = getCollection();

​ process(somethingInTheWay, target);

We’re going to copy collection into the unnamed register and then replace somethingInTheWay with the word that we’ve just copied. Table 11, ​Copy and Paste—First Attempt​ shows a first attempt.

* * *

Table 11. Copy and Paste—First Attempt

KeystrokesBuffer Contents

yiw

​ collection = getCollection();

​ process(somethingInTheWay, target);

jww

​ collection = getCollection();

​ process(somethingInTheWay, target);

diw

​ collection = getCollection();

​ process(, target);

P

​ collection = getCollection();

​ process(somethingInTheWay, target);

* * *

	 	 	 To begin with, our cursor is already on the word we want to copy, so we can get it into the unnamed register by typing yiw.

Next we move our cursor to the place where we want to paste our collection, but before we can put it there we’ll have to clear a space for it. So we run diw to delete the word somethingInTheWay.

Now we can hit the P key to paste the contents of our unnamed register in front of the cursor. But instead of pasting the word collection, which we yanked earlier, we get the word somethingInTheWay. What’s going on?

	 The diw command doesn’t just delete the word: it also copies it into the unnamed register. Or to rephrase that using more familiar terminology—diw cuts the word. (See ​Vim’s Terminology Versus the World​, for a discussion).

It’s obvious now what we did wrong. When we ran the diw command, it overwrote the contents of the unnamed register. That’s why when we pressed P, we got back the word we just deleted rather than the word we yanked earlier.

To solve this problem, we’ll have to get a deeper understanding of how Vim’s registers work.

Vim's Terminology Versus the World

	 The cut, copy, and paste terminology is universally understood, and these operations are available across most desktop software programs and operating systems. Vim provides these features too, but it uses different terminology: delete, yank, and put.

	 	 Vim’s put command is effectively identical to the paste operation. Fortunately, both words begin with the letter p, so the mnemonic for the key command works whichever terminology we use.

	 	 Vim’s yank command is equivalent to the copy operation. Historically, the c command was already assigned to the change operation, so vi’s authors were pushed to come up with an alternative name. The y key was available, so the copy operation became the yank command.

	 	 Vim’s delete command is equivalent to the standard cut operation. That is, it copies the specified text into a register and then removes it from the document. Understanding this is key to avoiding the common pitfall outlined in ​Oops! I Clobbered My Yank​.

	 	 You might be wondering what Vim’s equivalent is for really deleting text—that is, how can you remove text from the document and not copy it into any registers? Vim’s answer is a special register called the black hole, from which nothing returns. The black hole register is addressed by the _ symbol (see quote_ⓘ), so "_d{motion} performs a true deletion.

Tip 61 Grok Vim’s Registers

	 	 	 Rather than using a single clipboard for all cut, copy, and paste operations, Vim provides multiple registers. When we use the delete, yank, and put commands, we can specify which register we want to interact with.

Addressing a Register

	 The delete, yank, and put commands all interact with one of Vim’s registers. We can specify which register we want to use by prefixing the command with "{register}. If we don’t specify a register, then Vim will use the unnamed register.

For example, if we wanted to yank the current word into register a, we could run "ayiw. Or if we wanted to cut the current line into register b, we could run "bdd. Then we could paste the word from register a by typing "ap, or we could paste the line from register b by typing "bp.

	 In addition to the Normal mode commands, Vim also provides Ex commands for delete, yank, and put operations. We could cut the current line into register c by running :delete c, and then we could paste it below the current line with the :put c command. These may seem verbose in comparison with the Normal mode commands, but they’re useful in combination with other Ex commands and in Vim scripts. For example, Tip 100, shows how :yank can be used with the :global command.

The Unnamed Register ("")

	 	 If we don’t specify which register we want to interact with, then Vim will use the unnamed register, which is addressed by the " symbol (see quote_quoteⓘ). To address this register explicitly, we have to use two double quote marks: for example, ""p, which is effectively equivalent to p by itself.

	 	 	 	 	 The x, s, d{motion}, c{motion}, and y{motion} commands (and their uppercase equivalents) all set the contents of the unnamed register. In each case, we can prefix "{register} to specify another register, but the unnamed register is the default. The fact that it’s so easy to overwrite the contents of the unnamed register can cause problems if we’re not careful.

Consider again the example in ​Oops! I Clobbered My Yank​. We start off by yanking some text (the word「collection」) with the intention of pasting it elsewhere. Before we can paste it, we have to clear a space by deleting some text that is in our way, which overwrites the contents of the unnamed register. When we use the p command, we get back the text that we just deleted, rather than getting the text that we yanked previously.

Vim’s choice of terminology is unfortunate. The x and d{motion} commands are usually referred to as「delete」commands. This is a misnomer. It’s better to think of them as「cut」commands. The unnamed register often doesn’t contain the text that I expected to find there, but luckily, the yank register (which we’ll meet next) is more dependable.

The Yank Register ("0)

	 	 When we use the y{motion} command, the specified text is copied not only into the unnamed register but also into the yank register, which is addressed by the 0 symbol (see quote0ⓘ).

As the name suggests, the yank register is set only when we use the y{motion} command. To put it another way: it’s not set by the x, s, c{motion}, and d{motion} commands. If we yank some text, we can be sure that it will stick around in register 0 until we explicitly overwrite it by yanking something else. The yank register is reliable, whereas the unnamed register is volatile.

We can use the yank register to solve our problem from ​Oops! I Clobbered My Yank​:

KeystrokesBuffer Contents

yiw

​ collection = getCollection();

​ process(somethingInTheWay, target);

jww

​ collection = getCollection();

​ process(somethingInTheWay, target);

diw

​ collection = getCollection();

​ process(, target);

"0P

​ collection = getCollection();

​ process(collection, target);

	 The diw command still overwrites the unnamed register, but it leaves the yank register untouched. We can safely paste from the yank register by pressing "0P, and Vim gives us the text that we want.

If we inspect the contents of the unnamed and yank registers, we’ll see that they contain the text that we deleted and yanked, respectively:

​=> ​:reg "0​

​<= --- Registers ---

​ "" somethingInTheWay

​ "0 collection

The Named Registers ("a--"z)

	 	 Vim has one named register for each letter of the alphabet (see quote_alphaⓘ). That means that we can cut ("ad{motion}), copy ("ay{motion}), or paste ("ap) up to twenty-six pieces of text.

We could use a named register to solve our problem from ​Oops! I Clobbered My Yank​:

KeystrokesBuffer Contents

"ayiw

​ collection = getCollection();

​ process(somethingInTheWay, target);

jww

​ collection = getCollection();

​ process(somethingInTheWay, target);

diw

​ collection = getCollection();

​ process(, target);

"aP

​ collection = getCollection();

​ process(collection, target);

Using a named register requires extra keystrokes, so for a simple example like this we’re better off using the yank register ("0). Named registers can become really useful when we’ve got one or more pieces of text that we want to paste in several places.

	 	 	 	 When we address a named register with a lowercase letter, it overwrites the specified register, whereas when we use an uppercase letter, it appends to the specified register. Skip ahead to Tip 100, to see a demonstration of appending to a register.

The Black Hole Register ("_)

	 	 	 The black hole register is a place from which nothing returns. It’s addressed by the underscore symbol (see quote_ⓘ). If we run the command "_d{motion}, then Vim deletes the specified text without saving a copy of it. This can be useful if we want to delete text without overwriting the contents of the unnamed register.

We could use the black hole register to solve our problem from ​Oops! I Clobbered My Yank​:

KeystrokesBuffer Contents

yiw

​ collection = getCollection();

​ process(somethingInTheWay, target);

jww

​ collection = getCollection();

​ process(somethingInTheWay, target);

"_diw

​ collection = getCollection();

​ process(, target);

P

​ collection = getCollection();

​ process(collection, target);

The System Clipboard ("+) and Selection ("*) Registers

	 	 	 	 	 All of the registers that we’ve discussed so far are internal to Vim. If we want to copy some text from inside of Vim and paste it into an external program (or vice versa), then we have to use one of the system clipboards.

Vim’s plus register references the system clipboard and is addressed by the + symbol (see quote+ⓘ).

If we use the cut or copy command to capture text in an external application, then we can paste it inside Vim using "+p command (or <C-r>+ from the Insert mode). Conversely, if we prefix Vim’s yank or delete commands with "+, the specified text will be captured in the system clipboard. That means we can easily paste it inside other applications.

	 	 	 The X11 windowing system has a second kind of clipboard called the primary. This represents the most recently selected text, and we can use the middle mouse button (if we have one) to paste from it. Vim’s quotestar register maps to the primary clipboard and is addressed by the * symbol (quotestarⓘ).

KeystrokesBuffer Contents

"+

The X11 clipboard, used with cut, copy, and paste

"*

The X11 primary, used with middle mouse button

	 	 In Windows and Mac OS X, there is no primary clipboard, so we can use the "+ and "* registers interchangeably: they both represent the system clipboard.

Vim can be compiled with or without support for X11 clipboard integration. To find out whether your version of Vim has the feature enabled, run the :version command and look for xterm_clipboard. If it’s prefixed with a minus sign, then your version of Vim does not support this feature. A plus sign means that the feature is available.

The Expression Register ("=)

	 	 	 Vim’s registers can be thought of simply as containers that hold a block of text. The expression register, referenced by the = symbol (quote=ⓘ), is an exception. When we fetch the contents of the expression register, Vim drops into Command-Line mode, showing an = prompt. We can enter a Vim script expression and then press <CR> to execute it. If the expression returns a string (or a value that can be easily coerced into a string), then Vim uses it.

For examples of the expression register in action, check out Tip 16, Tip 96, Tip 95, and Tip 71.

More Registers

	 	 We can set the contents of the named, unnamed, and yank registers explicitly using the delete and yank commands. In addition, Vim provides a handful of registers whose values are set implicitly. These are known collectively as the read-only registers (quote.ⓘ). The following table summarizes them:

RegisterContents

"%

		 		 Name of the current file

"#

Name of the alternate file

".

		 		 Last inserted text

":

		 		 Last Ex command

"/

		 		 Last search pattern

Technically, the "/ register is not read-only—it can be set explicitly using the :let command (see quote/ⓘ)—but it’s included in this table for convenience.

Tip 62 Replace a Visual Selection with a Register

	 	 	 	 	 When used from Visual mode, Vim’s put command has some unusual qualities. We’ll find out how these can be exploited in this tip.

When we use the p command in Visual mode, Vim replaces the selection with the contents of the specified register (see v_pⓘ). We can exploit this feature to solve our problem from ​Oops! I Clobbered My Yank​:

KeystrokesBuffer Contents

yiw

​ collection = getCollection();

​ process(somethingInTheWay, target);

jww

​ collection = getCollection();

​ process(somethingInTheWay, target);

ve

​ collection = getCollection();

​ process(somethingInTheWay, target);

p

​ collection = getCollection();

​ process(collection, target);

	 	 For this particular problem, this is my favorite solution. We can get away with using the unnamed register for both the yank and put operations because there’s no delete step. Instead, we combine the delete and put operations into a single step that replaces the selection.

It’s important to understand that this technique has a side effect. Try pressing u to undo the last change. Now press gv to reselect the last visual selection and then press the p key again. What happens? Apparently nothing!

	 	 To make it work this time, we’d have to press "0p to replace the visual selection with the contents of the yank register. We got away with using p the first time because the unnamed register happened to contain the text that we wanted to use. The second time around, the unnamed register contains the text that was overwritten.

To illustrate how strange this is, let’s consider an imaginary API for the standard cut, copy, and paste model. This API has methods called setClipboard() and getClipboard(). The cut and copy operations both call setClipboard(), while the paste operation calls getClipboard(). When we use Vim’s p command in Visual mode, it does both: it gets the contents of the unnamed register, and it sets the contents of the unnamed register.

Think of it this way: the visual selection in the document swaps places with the text in the register. Is it a feature? Is it a bug? You decide!

Swap Two Words

	 	 We can exploit this quirk in Vim’s visual put behavior. Let’s say that we want to swap the order of two words in this sentence to make it read「fish and chips」:

KeystrokesBuffer Contents

{start}

​ I like chips and fish.

fc

​ I like chips and fish.

de

​ I like  and fish.

mm

​ I like  and fish.

ww

​ I like and fish.

ve

​ I like and fish.

p

​ I like and chips.

`m

​ I like  and chips.

P

​ I like fish and chips.

We use de to cut the word「chips,」copying it into the unnamed register. Then we visually select the word「fish,」which we want to replace. When we use the p command, the word「chips」goes into the document, and the word「fish」is copied into the unnamed register. Then we can snap back to the gap and paste the word「fish」from the unnamed register back into the document.

In this case, it would be quicker to delete「chips and fish」and then type out「fish and chips」instead, using the c3w command for example. But this same technique can also be used to swap the order of longer phrases.

The m{char} command sets a mark, and the `{char} command jumps to the mark. Refer to Tip 54, for more information.

Tip 63 Paste from a Register

	 	 	 	 	 The Normal mode put command can behave differently, depending on the nature of the text that is being inserted. It can be helpful to adopt different strategies, depending on whether we’re pasting a line-wise or a character-wise region of text.

In Tip 60, we saw that we could transpose the order of two characters by pressing xp, while ddp would transpose the order of two lines. We use the p command in both cases, but the outcome is subtly different.

	 	 The p command puts the text from a register after the cursor position (pⓘ). As a complement, Vim also provides the (uppercase) P command, which inserts text before the cursor position. What is meant by before or after the cursor position can differ, depending on the contents of the register that is being inserted.

In the case of xp, the register contains a single character. The p command puts the contents of the register directly after the character that the cursor is positioned on.

In the case of ddp, the register contains one complete line. The p command puts the contents of the register on the line below the one that the cursor is positioned on.

Whether the p command puts the text from the register after the current character or after the current line depends on how the specified register was set. A line-wise yank or delete operation (such as dd, yy, or dap) creates a line-wise register, whereas a character-wise yank or delete (such as x, diw, or das) creates a character-wise register. In general, the outcome of using the p command is fairly intuitive (see linewise-registerⓘ for more details).

Pasting Character-wise Regions

	 	 Suppose that our default register contains the text collection, and that we want to paste as the first argument to a method call. Whether we use the p or P command depends on where the cursor is positioned. Take this buffer:

​ collection = getCollection();

​ process(, target);

Compare it with this:

​ collection = getCollection();

​ process(, target);

In the first case we would use p, whereas in the second case we would use P. I don’t find this to be very intuitive. In fact, I get it wrong often enough that puP and Pup are practically muscle memory for me!

	 I don’t like having to think about whether a character-wise region of text needs to go in front of the cursor or after it. For that reason, I sometimes prefer to paste character-wise regions of text from Insert mode using the <C-r>{register} mapping rather than using the Normal mode p and P commands. Using this technique, the text from the register is always inserted in front of the cursor position, just as though we were typing it in Insert mode.

From Insert mode, we can insert the contents of the unnamed register by pressing <C-r>", or we can insert the contents of the yank register by pressing <C-r>0 (see Tip 15, for more details). We can use this technique to solve our problem from ​Oops! I Clobbered My Yank​:

KeystrokesBuffer Contents

yiw

​ collection = getCollection();

​ process(somethingInTheWay, target);

jww

​ collection = getCollection();

​ process(somethingInTheWay, target);

ciw<C-r>0<Esc>

​ collection = getCollection();

​ process(collection, target);

	 Using the ciw command gives us an added bonus: the dot command now replaces the current word with「collection.」

Pasting Line-Wise Regions

	 	 When pasting from a line-wise register, the p and P commands put the text below or above the current line. This is more intuitive than the character-wise behavior.

It’s worth noting that Vim also provides gp and gP commands. These also put the text before or after the current line, but they leave the cursor positioned at the end of the pasted text instead of at the beginning. The gP command is especially useful when duplicating a range of lines, as demonstrated here:

KeystrokesBuffer Contents

yap

​ <table>

​

​ <tr>

​ <td>Symbol</td>

​ <td>Name</td>

​ </tr>

​

​ </table>

gP

​ <table>

​

​ <tr>

​ <td>Symbol</td>

​ <td>Name</td>

​ </tr>

​

​   <tr>

​ <td>Symbol</td>

​ <td>Name</td>

​ </tr>

​

​ </table>

We can use the duplicated text as a template, changing the contents of the table cells to make it look how we want. Both the P and gP commands would have worked fine, except that the first one would leave our cursor positioned above the inserted text. The gP command leaves our cursor positioned on the second duplicate, which sets us up conveniently so that we can change it to suit our needs.

Discussion

The p and P commands are great for pasting multiline regions of text. But for short sections of character-wise text, the <C-r>{register} mapping can be more intuitive.

Tip 64 Interact with the System Clipboard

	 	 	 Besides Vim’s built-in put commands, we can sometimes use the system paste command. However, using this can occasionally produce unexpected results when running Vim inside a terminal. We can avoid these issues by enabling the ‘paste’ option before using the system paste command.

Preparation

	 	 This tip is only applicable when running Vim inside the terminal, so you can safely skip it if you always use GVim. We’ll start by launching Vim in the terminal:

​=> ​$ vim -u NONE -N​

Enabling the ‘autoindent’ setting is a sure way to induce strange effects when pasting from the system clipboard:

​=> ​:set autoindent​

Finally, we’ll need to copy the following code into the system clipboard. Copying code listings from a PDF can produce strange results, so I recommend downloading the sample code and then opening it in another text editor (or a web browser) and using the system copy command:

copy_and_paste/fizz.rb

​ [1,2,3,4,5,6,7,8,9,10].each ​do​ |n|

​ ​if​ n%5==0

​ puts ​"fizz"​

​ ​else​

​ puts n

​ ​end​

​ ​end​

Locating the System Paste Command

	 	 	 Throughout this tip, we’ll refer to the system paste command, and you can substitute the appropriate mapping for your system. On OS X, the system paste command is triggered by the Cmd-v mapping. We can use this inside the Terminal or in MacVim, and it inserts the contents of the system clipboard.

	 	 Things aren’t quite so tidy on Linux and Windows. The standard mapping for the system paste command is normally Ctrl-v. In Normal mode, this mapping enables Visual-Block mode (Tip 21), and in Insert mode it enables us to insert characters literally or by a numeric code (Tip 17​Insert Unusual Characters by Character Code​).

Some terminal emulators on Linux provide a modified version of Ctrl-v for pasting from the system clipboard. It might be Ctrl-Shift-v or perhaps Ctrl-Alt-v, depending on the system. Don’t worry if you can’t figure out what the system paste command is for your setup. An alternative using the "* register is presented at the end of this tip.

Using the System Paste Command in Insert Mode

	 If we switch to Insert mode and then use the system paste command, we get this strange result:

​ [1,2,3,4,5,6,7,8,9,10].each ​do​ |n|

​ ​if​ n%5==0

​ puts ​"fizz"​

​ ​else​

​ puts n

​ ​end​

​ ​end​

	 	 Something is wrong with the indentation. When we use the system paste command in Insert mode, Vim acts as though each character has been typed by hand. When the ‘autoindent’ option is enabled, Vim preserves the same level of indentation each time we create a new line. The leading whitespace at the start of each line in the clipboard is added on top of the automatic indent, and the result is that each line wanders further and further to the right.

	 GVim is able to discern when text is pasted from the clipboard and adjust its behavior accordingly, but when Vim runs inside a terminal this information is not available. The ‘paste’ option allows us to manually warn Vim that we’re about to use the system paste command. When the ‘paste’ option is enabled, Vim turns off all Insert mode mappings and abbreviations and resets a host of options, including ‘autoindent’ (look up 'paste'ⓘ for the full list). That allows us to safely paste from the system clipboard with no surprises.

	 When we’re finished using the system paste command, we should disable the ‘paste’ option again. That means switching back to Normal mode and then running the Ex command :set paste!. Don’t you think it would be handy if there were a way of toggling this option without leaving Insert mode?

	 	 The way that Vim behaves when ‘paste’ is enabled means that the usual methods for creating custom mappings won’t work in Insert mode. Instead, we can assign a key to the ‘pastetoggle’ option ('pastetoggle'ⓘ):

​=> ​:set pastetoggle=<f5>​

	 Try executing that command line: it sets up the <f5> to toggle the paste option on and off. It should work both in Insert and Normal modes. If you find the mapping useful, add that line (or a variation of it) to your vimrc.

Avoid Toggling ‘paste’ by Putting from the Plus Register

	 	 	 If you’re running a version of Vim with system clipboard integration, then you can avoid fiddling with the ‘paste’ option entirely. The Normal mode "+p command pastes the contents of the plus register, which mirrors the system clipboard (see ​The System Clipboard ("+) and Selection ("*) Registers​, for more details). This command preserves the indentation of the text in the clipboard so you can expect no surprises, regardless of how the ‘paste’ and ‘autoindent’ options are set.

Copyright © 2016, The Pragmatic Bookshelf.

Chapter 11

Macros


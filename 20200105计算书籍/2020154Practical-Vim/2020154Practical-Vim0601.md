Vim’s Visual mode allows us to define a selection of text and then operate upon it. This should feel pretty intuitive, since it is the model that most editing software follows. But Vim’s take is characteristically different, so we’ll start by making sure we grok Visual mode (Tip 20).

Vim has three variants of Visual mode involving working with characters, lines, or rectangular blocks of text. We’ll explore ways of switching between these modes as well as some useful tricks for modifying the bounds of a selection (Tip 21).

We’ll see that the dot command can be used to repeat Visual mode commands, but that it’s especially effective when operating on line-wise regions. When working with character-wise selections, the dot command can sometimes fall short of our expectations. We’ll see that in these scenarios, operator commands may be preferable.

Visual-Block mode is rather special in that it allows us to operate on rectangular columns of text. You’ll find many uses for this feature, but we’ll focus on three tips that demonstrate some of its capabilities.

Tip 20 Grok Visual Mode

Visual mode allows us to select a range of text and then operate upon it. However intuitive this might seem, Vim’s perspective on selecting text is different from other text editors.

Suppose for a minute that we’re not working with Vim but instead filling out a text area on a web page. We’ve written the word「March,」but it should read「April,」so using the mouse, we double-click the word to select it. Having highlighted the word, we could hit the backspace key to delete it and then type out the correct month as a replacement.

You probably already know that there’s no need to hit the backspace key in this example. With the word「March」selected, we would only have to type the letter「A」and it would replace the selection, preparing the way so that we could type out the rest of the word「April.」It’s not much, but a keystroke saved is a keystroke earned.

If you expect this behavior to carry over to Vim’s Visual mode, you’re in for a surprise. The clue is right there in the name: Visual mode is just another mode, which means that each key performs a different function.

	 	 Many of the commands that you are familiar with from Normal mode work just the same in Visual mode. We can still use h, j, k, and l as cursor keys. We can use f{char} to jump to a character on the current line and then repeat or reverse the jump with the ; and , commands, respectively. We can even use the search command (and n/N) to jump to pattern matches. Each time we move our cursor in Visual mode, we change the bounds of the selection.

Some Visual mode commands perform the same basic function as in Normal mode but with a slight twist. For example, the c command is consistent in both modes in that it deletes the specified text and then switches to Insert mode. The difference is in how we specify the range on which to act. From Normal mode, we trigger the change command first and then specify the range as a motion. This, if you’ll remember from Tip 12, is called an operator command. Whereas in Visual mode, we start off by making the selection and then trigger the change command. This inversion of control can be generalized for all operator commands (see Table 2, ​Vim’s Operator Commands​). For most people, the Visual mode approach feels more intuitive.

Let’s revisit the simple example where we wanted to change the word「March」to「April.」This time, suppose that we have left the confines of the text area on a web page and we’re comfortably back inside Vim. We place our cursor somewhere on the word「March」and run viw to visually select the word. Now, we can’t just type the word「April」because that would trigger the A command and append the text「pril」! Instead, we’ll use the c command to change the selection, deleting the word and dropping us into Insert mode, where we can type out the word「April」in full. This pattern of usage is similar to our original example, except that we use the c key instead of backspace.

Meet Select Mode

	 In a typical text editing environment, selected text is deleted when we type any printable character. Vim’s Visual mode doesn’t follow this convention—but Select mode does. According to Vim’s built-in documentation, it「resembles the selection mode in Microsoft Windows」(see Select-modeⓘ). Printable characters cause the selection to be deleted, Vim enters Insert mode, and the typed character is inserted.

We can toggle between Visual and Select modes by pressing <C-g>. The only visible difference is the message at the bottom of screen, which switches between -- VISUAL -- and -- SELECT --. But if we type any printable character in Select mode, it will replace the selection and switch to Insert mode. Of course, from Visual mode you could just as well use the c key to change the selection.

If you are happy to embrace the modal nature of Vim, then you should find little use for Select mode, which holds the hand of users who want to make Vim behave more like other text editors. I can think of only one place where I consistently use Select mode: when using a plugin that emulates TextMate’s snippet functionality, Select mode highlights the active placeholder.

Tip 21 Define a Visual Selection

	 	 Visual mode’s three submodes deal with different kinds of text. In this tip, we’ll look at the ways of enabling each visual submode, as well as how to switch between them.

	 	 	 	 Vim has three kinds of Visual mode. In character-wise Visual mode, we can select anything from a single character up to a range of characters within a line or spanning multiple lines. This is suitable for working at the level of individual words or phrases. If we want to operate on entire lines, we can use line-wise Visual mode instead. Finally, block-wise Visual mode allows us to work with columnar regions of the document. Block-wise Visual mode is quite special, so we’ll discuss it at greater length in Tip 24, Tip 25, and Tip 26.

Enabling Visual Modes

	 	 The v key is our gateway into Visual mode. From Normal mode, we can press v by itself to enable character-wise Visual mode. Line-wise Visual mode is enabled by pressing V (with the Shift key), and block-wise Visual mode by pressing <C-v> (with the Control key). These commands are summarized in the following table:

CommandEffect

v

Enable character-wise Visual mode

V

Enable line-wise Visual mode

<C-v>

Enable block-wise Visual mode

gv

Reselect the last visual selection

	 The gv command is a useful little shortcut. It reselects the range of text that was last selected in Visual mode. No matter whether the previous selection was character-wise, line-wise, or block-wise, the gv command should do the right thing. The only case where it might get confused is if the last selection has since been deleted.

Switching Between Visual Modes

	 We can switch between the different flavors of Visual mode in the same way that we enable them from Normal mode. If we’re in character-wise Visual mode, we can switch to the line-wise variant by pressing V, or to block-wise Visual mode with <C-v>. But if we were to press v from character-wise Visual mode, it would switch us back into Normal mode. So you can think of the v key as a toggle between Normal mode and character-wise Visual mode. The V and <C-v> keys also toggle between Normal mode and their respective flavors of Visual mode. Of course, you can always switch back to Normal mode by pressing <Esc> or <C-[> (just like getting out of Insert mode). This table summarizes the commands for switching between Visual modes:

CommandEffect

<Esc> / <C-[>

		 		 Switch to Normal mode

v / V / <C-v>

Switch to Normal mode (when used from character-, line- or block-wise Visual mode, respectively)

v

		 		 Switch to character-wise Visual mode

V

		 		 Switch to line-wise Visual mode

<C-v>

		 		 Switch to block-wise Visual mode

o

Go to other end of highlighted text

Toggling the Free End of a Selection

	 The range of a Visual mode selection is marked by two ends: one end is fixed and the other moves freely with our cursor. We can use the o key to toggle the free end. This is really handy if halfway through defining a selection we realize that we started in the wrong place. Rather than leaving Visual mode and starting afresh, we can just hit o and redefine the bounds of the selection. The following demonstrates how we can use this technique:

KeystrokesBuffer Contents

{start}

​ Select from here to here.

vbb

​ Select from here to here.

o

​ Select from here to here.

e

​ Select from here to here.

Tip 22 Repeat Line-Wise Visual Commands

	 	 	 	 When we use the dot command to repeat a change made to a visual selection, it repeats the change on the same range of text. In this tip, we’ll make a change to a line-wise selection and then repeat it with the dot command.

When we execute a command from Visual mode, we are dropped back into Normal mode and the range of text that was marked out in Visual mode is unselected. So what should we do if we want to perform another Visual mode command on the same range of text?

Suppose that we had the following excerpt of malformatted Python:

visual_mode/fibonacci-malformed.py

​ ​def​ fib(n):

​ a, b = 0, 1

​ ​while​ a < n:

​ ​print​ a,

​ a, b = b, a+b

​ fib(42)

This code sample uses four spaces per indentation. First, we’ll have to configure Vim to match this style.

Preparation

	 	 	 	 	 To make the < and > commands work properly, we should set the ‘shiftwidth’ and ‘softtabstop’ settings to 4 and enable ‘expandtab’. If you want to understand how these settings work together, check out the「Tabs and Spaces」episode on Vimcasts.org.[6] This one-liner does the trick:

​=> ​:set shiftwidth=4 softtabstop=4 expandtab​

Indent Once, Then Repeat

	 	 In our malformed Python excerpt, the two lines below the while keyword should be indented further by two levels. We could fix it by visually selecting the text and triggering the > command to indent it. But that would only increase the indentation by one level before dropping us back into Normal mode.

One solution would be to reselect the same text using the gv command and then invoke the indentation command again. But if you’re getting a feel for the Vim way, then this should raise alarm bells for you.

When we need to repeat ourselves, the dot command is our friend. Rather than reselecting the same range of text and repeating the same command manually, we can just hit the . key from Normal mode. Here it is in action:

KeystrokesBuffer Contents

{start}

​ def fib(n):

​ a, b = 0, 1

​ while a < n:

​ print a,

​ a, b = b, a+b

​ fib(42)

Vj

​ def fib(n):

​ a, b = 0, 1

​ while a < n:

​ print a,

​ a, b = b, a+b

​ fib(42)

>.

​ def fib(n):

​ a, b = 0, 1

​ while a < n:

​ print a,

​ a, b = b, a+b

​ fib(42)

If you’re good at counting, you might prefer to hit the target in a single blow by running 2> from Visual mode. I prefer using the dot command because it gives me instant visual feedback. If I need to trigger the indentation command again, I just hit . another time. Or if I get trigger-happy and overshoot my mark, I press the u key to bring it back in line. Tip 11, discusses the differences in a little more detail.

When we use the dot command to repeat a Visual mode command, it acts on the same amount of text as was marked by the most recent visual selection. This behavior tends to work in our favor when we make line-wise visual selections, but it can have surprising results with character-wise selections. Next, we’ll look at an example that illustrates this.

Tip 23 Prefer Operators to Visual Commands Where Possible

	 	 	 Visual mode may be more intuitive than Vim’s Normal mode of operation, but it has a weakness: it doesn’t always play well with the dot command. We can route around this weakness by using Normal mode operators when appropriate.

Suppose that we want to transform the following list of links to make them shout:

visual_mode/list-of-links.html

​ <a href=​"#"​>one</a>

​ <a href=​"#"​>two</a>

​ <a href=​"#"​>three</a>

We can select the inner contents of a tag by running vit, which can be read as: visually select inside the tag. The it command is a special kind of motion called a text object, which we’ll cover in detail in Tip 52.

Using a Visual Operator

	 	 	 In Visual mode, we make a selection and then act on it. In this case, we could use the U command, which converts the selected characters to uppercase (v_Uⓘ). See Table 4, ​Uppercasing in Visual Mode​.

* * *

Table 4. Uppercasing in Visual Mode

KeystrokesBuffer Contents

{start}

​ <a href="#">one</a>

​ <a href="#">two</a>

​ <a href="#">three</a>

vit

​ <a href="#">one</a>

​ <a href="#">two</a>

​ <a href="#">three</a>

U

​ <a href="#">ONE</a>

​ <a href="#">two</a>

​ <a href="#">three</a>

* * *

Having transformed the first line, we now want to perform the same change on the next two lines. How about we try using the Dot Formula?

Running j. advances our cursor to the next line and then repeats the last change. It works fine on line two, but if we try it again we end up with this strange-looking result:

​ <a href=​"#"​>ONE</a>

​ <a href=​"#"​>TWO</a>

​ <a href=​"#"​>THRee</a>

Do you see what’s happened? When a Visual mode command is repeated, it affects the same range of text (see visual-repeatⓘ). In this case, the original command affected a word consisting of three letters. This works fine for line two, which happens to also contain a three-letter word, but it falls short when we try to repeat the command on a word containing five letters.

Using a Normal Operator

	 The Visual mode U command has a Normal mode equivalent: gU{motion} (gUⓘ). If we use this to make the first change, we can complete the subsequent edits using the Dot Formula:

KeystrokesBuffer Contents

{start}

​ <a href="#">one</a>

​ <a href="#">two</a>

​ <a href="#">three</a>

gUit

​ <a href="#">ONE</a>

​ <a href="#">two</a>

​ <a href="#">three</a>

j.

​ <a href="#">ONE</a>

​ <a href="#">TWO</a>

​ <a href="#">three</a>

j.

​ <a href="#">ONE</a>

​ <a href="#">TWO</a>

​ <a href="#">THREE</a>

Discussion

Both of these techniques require only four keystrokes: vitU versus gUit, but the underlying semantics are quite different. In the Visual mode approach, the four keystrokes can be considered as two separate commands: vit to make a selection and U to transform the selection. In contrast, gUit can be considered as a single command comprised of an operator (gU) and a motion (it).

If we want to set up the dot command so that it repeats something useful, then we’re better off staying out of Visual mode. As a general rule, we should prefer operator commands over their Visual mode equivalents when working through a repetitive set of changes.

That’s not to say that Visual mode is out of bounds. It still has a place. Not every editing task needs to be repeated, so Visual mode is perfectly adequate for one-off changes. And even though Vim’s motions allow for surgical precision, sometimes we need to modify a range of text whose structure is difficult to trace. In these cases, Visual mode is the right tool for the job.

Tip 24 Edit Tabular Data with Visual-Block Mode

	 	 	 	 	 We can work with rows of text in any editor, but manipulating columns of text requires a more specialized tool. Vim provides this capability in the form of its Visual-Block mode, which we’ll use to transform a plain-text table.

Suppose that we have a plain-text table such as this one:

visual_mode/chapter-table.txt

​ Chapter Page

​ Normal mode 15

​ Insert mode 31

​ Visual mode 44

We want to draw a vertical line out of pipe characters to separate the two columns of text and make it look more like a table. But first, we’ll reduce the spacing between the two columns, which are farther apart than they need be. We can make both of these changes using Visual-Block mode. See how in Table 5, ​Adding vertical pipes between columns​.

* * *

Table 5. Adding vertical pipes between columns

KeystrokesBuffer Contents

{start}

​ Chapter   Page

​ Normal mode 15

​ Insert mode 31

​ Visual mode 44

<C-v>3j

​ Chapter   Page

​ Normal mode   15

​ Insert mode   31

​ Visual mode   44

x...

​ Chapter   Page

​ Normal mode 15

​ Insert mode 31

​ Visual mode 44

gv

​ Chapter   Page

​ Normal mode   15

​ Insert mode   31

​ Visual mode   44

r|

​ Chapter | Page

​ Normal mode | 15

​ Insert mode | 31

​ Visual mode | 44

yyp

​ Chapter | Page

​ Chapter | Page

​ Normal mode | 15

​ Insert mode | 31

​ Visual mode | 44

Vr-

​ Chapter | Page

​ --------------------

​ Normal mode | 15

​ Insert mode | 31

​ Visual mode | 44

* * *

To begin, we use <C-v> to engage Visual-Block mode; then we define the column selection by moving our cursor down several lines. Pressing the x key deletes that column, and the dot command repeats the deletion for the same range of text. We repeat until the two columns are about the right distance apart.

Instead of using the dot command, we could have expanded our column selection into a box by moving the cursor two or three steps to the right. Then we would have to make only a single deletion. I prefer the instant visual feedback that we get when we delete a single column and repeat it.

Now that we’ve lined up the two columns of text where we want them, we’re ready to draw a line between them. We can reselect our last visual selection using the gv command and then press r| to replace each character in the selection with a pipe character.

While we’re at it, we may as well draw a horizontal line to separate the table headers from the rows beneath. We do a quick line-wise yank-and-put to duplicate the top line (yyp) and then replace every character in that line with a dash character (Vr-).

Tip 25 Change Columns of Text

	 	 	 	 	 We can use Visual-Block mode to insert text into several lines of text simultaneously.

Visual-Block mode is not just useful to us when working with tabular data. Oftentimes, we can benefit from this feature when working with code. For example, take this snippet of (suboptimal) CSS:

visual_mode/sprite.css

​ li.one a{ background-image: ​url('/images/sprite.png')​; }

​ li.two a{ background-image: ​url('/images/sprite.png')​; }

​ li.three a{ background-image: ​url('/images/sprite.png')​; }

Suppose that the sprite.png file has been moved from images/ into a components/ directory. We’ll need to change each of these lines to reference the file’s new location. We could do this using Visual-Block mode as shown in Table 6, ​Inserting into Multiple Lines​.

* * *

Table 6. Inserting into Multiple Lines

KeystrokesBuffer Contents

{start}

Normal mode

​ li.one a{ background-image: url('/images/sprite.png'); }

​ li.two a{ background-image: url('/images/sprite.png'); }

​ li.three a{ background-image: url('/images/sprite.png'); }

<C-v>jje

Visual mode

​ li.one a{ background-image: url('/images/sprite.png'); }

​ li.two a{ background-image: url('/images/sprite.png'); }

​ li.three a{ background-image: url('/images/sprite.png'); }

c

Insert mode

​ li.one a{ background-image: url('//sprite.png'); }

​ li.two a{ background-image: url('//sprite.png'); }

​ li.three a{ background-image: url('//sprite.png'); }

components

Insert mode

​ li.one a{ background-image: url('/components/sprite.png'); }

​ li.two a{ background-image: url('//sprite.png'); }

​ li.three a{ background-image: url('//sprite.png'); }

<Esc>

Normal mode

​ li.one a{ background-image: url('/components/sprite.png'); }

​ li.two a{ background-image: url('/components/sprite.png'); }

​ li.three a{ background-image: url('/components/sprite.png'); }

* * *

The procedure should look pretty familiar. We begin by defining the selection that we want to operate on, which happens to be a rectangular Visual-Block. When we hit the c key, all of the selected text disappears and we are dropped into Insert mode.

As we type the word「components」in Insert mode, it appears on the topmost line only. Nothing happens to the two lines below. We see the text that we typed in those lines only when we press <Esc> to return to Normal mode.

The behavior of Vim’s Visual-Block change command may be a little surprising. It seems inconsistent that the deletion should affect all marked lines simultaneously, but the insertion affects only the topmost line (at least for the duration of Insert mode). Some text editors provide similar functionality, but they update all selected lines at the same time. If you’re used to that kind of behavior (as I was), then you might find Vim’s implementation less polished. But in practice, it makes no difference in the final outcome. So long as you dip into Insert mode only for short bursts, you shouldn’t have any surprises.

Tip 26 Append After a Ragged Visual Block

	 	 	 	 	 Visual-Block mode is great for operating on rectangular chunks of code such as lines and columns, but it’s not confined to rectangular regions of text.

We’ve already met this snippet of JavaScript:

the_vim_way/2_foo_bar.js

​ ​var​ foo = 1

​ ​var​ bar = ​'a'​

​ ​var​ foobar = foo + bar

Three consecutive lines, each of different length. We want to append a semicolon at the end of each. In Tip 2, we solved this problem using the dot command, but we could just as well use Visual-Block mode:

KeystrokesBuffer Contents

{start}

Normal mode

​ var foo = 1

​ var bar = 'a'

​ var foobar = foo + bar

<C-v>jj$

Visual-Block

​ var foo = 1

​ var bar = ’a’

​ var foobar = foo + bar

A;

Insert mode

​ var foo = 1;

​ var bar = 'a'

​ var foobar = foo + bar

<Esc>

Normal mode

​ var foo = 1;

​ var bar = 'a';

​ var foobar = foo + bar;

After engaging Visual-Block mode, we extend our selection to the end of each line by pressing $. At first glance, one might expect this to cause difficulty because each line is a different length. But in this context, Vim understands that we want to extend our selection to the end of all selected lines. This lets us break free from our rectangular constraints, creating a selection that traces the ragged right edge of our text.

Having defined our selection, we can append at the end of each line using the A command (see ​Vim’s Conventions for「i」and「a」Keys​). This drops us into Insert mode on the topmost line of our selection. Anything that we type will appear on this line only for the duration of Insert mode, but as soon as we revert to Normal mode, our changes are propagated across the rest of the lines that we selected.

Vim's Conventions for「i」and「a」Keys

	 	 	 		 		 Vim has a couple of conventions for switching from Normal to Insert mode. The i and a commands both do it, positioning the cursor in front of or after the current character, respectively. The I and A commands behave similarly, except that they position the cursor at the start or end of the current line.

	 	 Vim follows similar conventions for switching from Visual-Block to Insert mode. The I and A commands both do it, placing the cursor at the start or end of the selection, respectively. So what about the i and a commands; what do they do in Visual mode?

	 In Visual and Operator-Pending modes the i and a keys follow a different convention: they form the first half of a text object. These are covered in greater depth in Tip 52. If you’ve made a selection with Visual-Block mode and you wonder why you’re not in Insert mode after pressing i, try using I instead.

Footnotes

[6]

http://vimcasts.org/e/2

Copyright © 2016, The Pragmatic Bookshelf.

In the beginning, there was ed. ed begat ex, and ex begat vi, and vi begat Vim.

The Old Testament of Unix

Chapter 5

Command-Line Mode


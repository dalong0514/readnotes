# Part 1Modes

Vim provides a modal user interface. This means that the result of pressing any key on the keyboard may differ depending on which mode is active at the time. It’s vital to know which mode is active and how to switch between Vim’s modes. In this part of the book, we’ll learn how each mode works and what it can be used for.

# 0101. Normal Mode

Normal mode is Vim’s natural resting state. If this chapter seems surprisingly short, then that’s because most of this book is about how to use Normal mode! Here, however, is where we cover some core concepts and general tips.

Other text editors spend most of their time in something that resembles Insert mode. So to the Vim newcomer, it can seem strange that Normal mode is the default. In Tip 7, we’ll begin explaining why this is by drawing an analogy with the workspace of a painter.

Many Normal mode commands can be executed with a count, which causes them to be run multiple times. In Tip 10, we’ll meet a pair of commands that increment and decrement numerical values and see how these commands can be combined with a count to do simple arithmetic.

Just because you can save keystrokes by using a count doesn’t mean that you should. We’ll look at some examples where it’s better simply to repeat a command than take the time to count how many times you want to run it.

Much of the power of Normal mode stems from the way that operator commands can be combined with motions. We’ll finish by looking at the consequences of this.

Tip 7 Pause with Your Brush Off the Page

For those unused to Vim, Normal mode can seem like an odd default. But experienced Vim users have difficulty imagining it any other way. This tip uses an analogy to illustrate the Vim way.

	 How much time do you reckon artists spend with their paint brushes in contact with the canvas? No doubt it would vary from artist to artist, but I’d be surprised if it counted for as much as half of the time painters spend at work.

Think of all of the things that painters do besides paint. They study their subject, adjust the lighting, and mix paints into new hues. And when it comes to applying paint to the canvas, who says they have to use brushes? A painter might switch to a palette knife to achieve a different texture or use a cotton swab to touch up the paint that’s already been applied.

The painter does not rest with a brush on the canvas. And so it is with Vim. Normal mode is the natural resting state. The clue is in the name, really.

Just as painters spend a fraction of their time applying paint, programmers spend a fraction of their time composing code. More time is spent thinking, reading, and navigating from one part of a codebase to another. And when we do want to make a change, who says we have to switch to Insert mode? We can reformat existing code, duplicate it, move it around, or delete it. From Normal mode, we have many tools at our disposal.

Tip 8 Chunk Your Undos

	 	 In other text editors, invoking the undo command after typing a few words might revert the last typed word or character. However, in Vim we can control the granularity of the undo command.

	 The u key triggers the undo command, which reverts the most recent change. A change could be anything that modifies the text in the document. That includes commands triggered from Normal, Visual, and Command-Line modes, but a change could also encompass any text entered (or deleted) in Insert mode. So we could also say that i{insert some text}<Esc> constitutes a change.

In nonmodal text editors, triggering the undo command after typing a few words could do one of two things. It could undo the last character that was typed. Or, more helpfully, it could chunk a set of characters together so that each undo operation removed a word instead of a character.

	 	 In Vim, we can control the granularity of the undo command. From the moment we enter Insert mode until we return to Normal mode, everything we type (or delete) counts as a single change. So we can make the undo command operate on words, sentences, or paragraphs just by moderating our use of the <Esc> key.

So how often should you leave Insert mode? It’s a matter of preference, but I like to make each「undoable chunk」correspond to a thought. As I write this text (in Vim, of course!), I often pause at the end of a sentence to consider what I’ll write next. No matter how brief its duration, each pause forms a natural break point, giving me a cue to leave Insert mode. When I’m ready to continue writing, I press A and carry on where I left off.

If I decide that I’ve taken a wrong turn, I’ll switch to Normal mode and press u. Each time I undo, my text decomposes in coherent chunks that correspond to my thought process as I was writing the original text. It means that I can easily try out a sentence or two and then throw them away with a couple of keystrokes.

If I’m in Insert mode with my cursor at the end of a line, the quickest way to open a new line is to press <CR>. And yet I sometimes prefer to press <Esc>o just because I anticipate that I might want that extra granularity from the undo command. If this sounds hard core, don’t worry. As you become adept with Vim, switching modes feels more and more lightweight.

As a general rule, if you’ve paused for long enough to ask the question,「Should I leave Insert mode?」then do it.

Moving Around in Insert Mode Resets the Change

	 	 	 	 When I said that the undo command would revert all characters entered (or deleted) during a trip into Insert mode and back, I was glossing over a small detail. If we use the <Up>, <Down>, <Left>, or <Right> cursor keys while in Insert mode, a new undo chunk is created. It’s just as though we had switched back to Normal mode to move around with the h, j, k, or l commands, except that we don’t have to leave Insert mode. This also has implications on the operation of the dot command.

Tip 9 Compose Repeatable Changes

Vim is optimized for repetition. In order to exploit this, we have to be mindful of how we compose our changes.

	 	 	 In Vim, we always have more than one way of doing something. In evaluating which way is best, the most obvious metric is efficiency: which technique requires the fewest keystrokes (a.k.a. VimGolf[3]). But how should we pick a winner in the event of a tie?

Suppose that our cursor is positioned on the「h」at the end of this line of text, and we want to delete the word「nigh.」

normal_mode/the_end.txt

​ The end is nigh

Delete Backward

		Since our cursor is already at the end of the word, we might begin by deleting backward.

KeystrokesBuffer Contents

{start}

​ The end is nigh

db

​ The end is h

x

​ The end is

		Pressing db deletes from the cursor’s starting position to the beginning of the word, but it leaves the final「h」intact. We can delete this rogue character by pressing x. That gives us a Vim golf score of 3.

Delete Forward

		This time, let’s try deleting forward instead.

KeystrokesBuffer Contents

{start}

​ The end is nigh

b

​ The end is nigh

dw

​ The end is

	 We have to start by maneuvering our cursor into position with the b motion. Once it’s in place, we can excise the word with a single dw command. Once again, our Vim golf score is 3.

Delete an Entire Word

		 		 		Both of our solutions so far have involved some kind of preparation or clean-up. We can be more surgical by using the aw text object instead of a motion (see awⓘ):

KeystrokesBuffer Contents

{start}

​ The end is nigh

daw

​ The end is

	 The daw command is easily remembered by the mnemonic delete a word. We’ll go into more detail on text objects in Tip 52, and Tip 53.

Tie-Breaker: Which Is Most Repeatable?

	 We’ve tried three techniques for deleting a word: dbx, bdw, and daw. In each case, our Vim golf score is 3. So how can we settle the question of which is best?

	 Remember, Vim is optimized for repetition. Let’s go through these techniques again. This time, we’ll finish by invoking the dot command and see what happens. I urge you to try these out for yourself.

The backward deletion technique involves two operations: db deletes to the start of the word and then x deletes a single character. If we invoke the dot command, it repeats the single character deletion (. == x). That’s not what I would call a big win.

The forward deletion technique also involves two steps. This time, b is just a plain motion, while dw makes a change. The dot command repeats dw, deleting from the cursor position to the beginning of the next word. It so happens that we’re already at the end of the line. There is no「next word,」so in this context the dot command isn’t useful. But at least it’s shorthand for something longer (. == dw).

The final solution only invokes a single operation: daw. This technique doesn’t just remove the word, it also deletes a whitespace character. As a result, our cursor ends up on the last character of the word「is.」If we invoke the dot command, it will repeat the instruction to delete a word. This time, the dot command does something truly useful (. == daw).

Discussion

The daw technique invests the most power into the dot command, so I declare it the winner of this round.

Making effective use of the dot command often requires some forethought. If you notice that you have to make the same small change in a handful of places, you can attempt to compose your changes in such a way that they can be repeated with the dot command. Recognizing those opportunities takes practice. But if you develop a habit of making your changes repeatable wherever possible, then Vim will reward you for it.

Sometimes, I won’t see an opportunity to use the dot command. After making a change—and finding that I need to perform an identical edit—I realize that the dot command is primed and ready to do the work for me. It makes me grin every time.

Tip 10 Use Counts to Do Simple Arithmetic

		 		Most Normal mode commands can be executed with a count. We can exploit this feature to do simple arithmetic.

Many of the commands that are available in Normal mode can be prefixed with a count. Instead of executing the command just once, Vim will attempt to execute the command the specified number of times (see countⓘ).

	 	 	 	 	 The <C-a> and <C-x> commands perform addition and subtraction on numbers. When run without a count they increment by one, but if we prefix a number, then we can add or subtract by any whole number. For example, if we positioned our cursor on a 5 character, running 10<C-a> would modify it to read 15.

But what happens if the cursor is not positioned on a numeric digit? The documentation says that the <C-a> command will「add [count] to the number at or after the cursor」(see ctrl-aⓘ). So if the cursor is not already positioned on a number, then the <C-a> command will look ahead for a digit on the current line. If it finds one, it jumps straight to it. We can use this to our advantage.

Here’s a snippet of CSS:

normal_mode/sprite.css

​ .blog, .news { background-image: ​url(/sprite.png)​; }

​ .blog { background-position: 0px 0px }

	 	 We’re going to duplicate the last line and make two small modifications to it: replace the word「blog」with「news,」and change「0px」to「-180px.」We can duplicate the line by running yyp and then using cW to change the first word. But how should we deal with that number?

One approach would be to jump to the digit with f0 and then dip into Insert mode to change the value by hand: i-18<Esc>. But it’s quicker just to run 180<C-x>. Since our cursor isn’t on a digit to begin with, it jumps forward to the first one that it finds. That saves us the step of moving the cursor by hand. Let’s see this work flow in action:

KeystrokesBuffer Contents

{start}

​ .blog, .news { background-image: url(/sprite.png); }

​ .blog { background-position: 0px 0px }

yyp

​ .blog, .news { background-image: url(/sprite.png); }

​ .blog { background-position: 0px 0px }

​ .blog { background-position: 0px 0px }

cW.news<Esc>

​ .blog, .news { background-image: url(/sprite.png); }

​ .blog { background-position: 0px 0px }

​ .news { background-position: 0px 0px }

180<C-x>

​ .blog, .news { background-image: url(/sprite.png); }

​ .blog { background-position: 0px 0px }

​ .news { background-position: -180px 0px }

In this example, we’ve only duplicated the line once and made changes. But suppose we had to make ten copies, subtracting 180 from the number in each successive copy. If we were to switch to Insert mode to amend each number, we’d have to type something different each time (-180, then -360, and so on). But by using the 180<C-x> command, our work flow is identical for each successive line. We could even record our keystrokes as a macro (see Chapter 11, ​Macros​) and then play it back as many times as needed.

Number Formats

What follows 007? No, this isn’t a James Bond gag; I’m asking what result would you expect if you added one to 007.

	 	 	 If you answered 008, then you might be in for a surprise when you try using Vim’s <C-a> command on any number with a leading zero. As is the convention in some programming languages, Vim interprets numerals with a leading zero to be in octal notation rather than in decimal. In the octal numeric system, 007 + 001 = 010, which looks like the decimal ten but is actually an octal eight. Confused?

	 If you work with octal numbers frequently, Vim’s default behavior might suit you. If you don’t, you probably want to add the following line to your vimrc:

​ ​set​ nrformats=

	 This will cause Vim to treat all numerals as decimal, regardless of whether they are padded with zeros.

Tip 11 Don’t Count If You Can Repeat

	 	 	 	 We can minimize the keystrokes required to perform certain tasks by providing a count, but that doesn’t mean that we should. Consider the pros and cons of counting versus repeating.

Suppose that we had the following text in our buffer:

​ Delete more than one word

We want to do as the text says, changing it to read「Delete one word」instead. That is to say, we’re going to delete two words.

We can approach this in a handful of ways. Both d2w and 2dw will work. With d2w, we invoke the delete command and then give 2w as the motion. We could read that as「delete two words.」However, 2dw turns things around. This time the count applies to the delete command, but the motion acts over a single word. We could read this as「delete a word two times.」Putting semantics aside, we get the same result either way.

Now let’s consider an alternative: dw.. This we can read as「Delete a word and then repeat.」

To recap, our options are as follows: d2w, 2dw, or dw.—three keystrokes each. But which is best?

For our discussion, d2w and 2dw are identical. After running either of these, we can press the u key to undo, and the two words that were deleted will appear again. Or, instead of undoing our change, we could repeat it with the dot command, which would delete the next two words.

In the case of dw., the result of pressing u or . is subtly different. Here, the change was dw—「delete word.」So if we wanted to restore the two words that were deleted, we’d have to undo twice: pressing uu (or 2u if you prefer). Pressing the dot command would just delete the next word rather than the next two.

Now suppose that instead of deleting two words, our original intent was to delete three words. By a small error in judgment, we run d2w instead of d3w. What next? We can’t use the dot command, because that would cause a total of four words to be deleted. So we could either back up and revise our count (ud3w) or continue by deleting the next word (dw).

If, on the other hand, we had used the command dw. in the first place, we would have to repeat the dot command only one more time. Because our original change was simply dw, the u and . commands have more granularity. Each acts upon one word at a time.

Now suppose that we want to delete seven words. We could either run d7w, or dw...... (that is, dw followed by the dot command six times). Counting keystrokes, we have a clear winner. But would you trust yourself to make the right count?

Counting is tedious. I’d rather hit the dot command six times than spend the same time looking ahead in order to reduce the number of keys that I have to press. What if I hit the dot command one too many times? No matter, I just back up by hitting the u key once.

Remember our mantra (from Tip 4): act, repeat, reverse. Here it is in action.

Use a Count When It Matters

Suppose that we wanted to change the text「I have a couple of questions」to instead read「I have some more questions.」We could do so as follows:

KeystrokesBuffer Contents

{start}

​ I have a couple of questions.

c3wsome more<Esc>

​ I have some more questions.

In this scenario, it doesn’t make much sense to use the dot command. We could delete one word and then another (with the dot command), but then we’d have to switch gears and change to Insert mode (using i or cw, for example). To me, that feels awkward enough that I’d rather go ahead and use a count.

	 There’s another advantage to using a count: it gives us a clean and coherent undo history. Having made this change, we could undo it with a single press of the u key, which ties in with the discussion in Tip 8.

That same argument also goes in favor of counting (d5w) over repeating (dw....), so my preferences may seem inconsistent here. You’ll develop your own opinion on this, depending on how much you value keeping your undo history clean and whether or not you find it tiresome to use counts.

Tip 12 Combine and Conquer

	 	 	 	 Much of Vim’s power stems from the way that operators and motions can be combined. In this tip, we’ll look at how this works and consider the implications.

Operator + Motion = Action

		 		 		 		The d{motion} command can operate on a single character (dl), a complete word (daw), or an entire paragraph (dap). Its reach is defined by the motion. The same goes for c{motion}, y{motion}, and a handful of others. Collectively, these commands are called operators. You can find the complete list by looking up operatorⓘ, while Table 2, ​Vim’s Operator Commands​, summarizes some of the more common ones.

* * *

Table 2. Vim’s Operator Commands

TriggerEffect

		 		 		 c

Change

d

Delete

y

Yank into register

g~

Swap case

gu

Make lowercase

gU

Make uppercase

>

Shift right

<

Shift left

=

Autoindent

!

Filter {motion} lines through an external program

* * *

The g~, gu, and gU commands are invoked by two keystrokes. In each case, we can consider the g to be a prefix that modifies the behavior of the subsequent keystroke. See ​Meet Operator-Pending Mode​, for further discussion.

The combination of operators with motions forms a kind of grammar. The first rule is simple: an action is composed from an operator followed by a motion. Learning new motions and operators is like learning the vocabulary of Vim. If we follow the simple grammar rules, we can express more ideas as our vocabulary grows.

		 		Suppose that we already know how to delete a word using daw, and then we learn about the gU command (see gUⓘ). It’s an operator too, so we can invoke gUaw to convert the current word to SHOUTY case. If we then expand our vocabulary to include the ap motion, which acts upon a paragraph, then we find two new operations at our disposal: dap to delete, or gUap to make the whole paragraph shout.

Vim’s grammar has just one more rule: when an operator command is invoked in duplicate, it acts upon the current line. So dd deletes the current line, while >> indents it. The gU command is a special case. We can make it act upon the current line by running either gUgU or the shorthand gUU.

Extending Vim’s Combinatorial Powers

The number of actions that we can perform using Vim’s default set of operators and motions is vast. But we can expand these even further by rolling our own custom motions and operators. Let’s consider the implications.

Custom Operators Work with Existing Motions

		 		 		 The standard set of operators that ships with Vim is relatively small, but it is possible to define new ones. Tim Pope’s commentary.vim plugin provides a good example.[4] This adds a command for commenting and uncommenting lines of code in all languages supported by Vim.

		 		 The commentary command is triggered by gc{motion}, which toggles commenting for the specified lines. It’s an operator command, so we can combine it with all of the usual motions. gcap will toggle commenting for the current paragraph. gcG comments from the current line to the end of the file. gcc comments the current line.

If you’re curious about how to create your own custom operators, start by reading :map-operatorⓘ.

Custom Motions Work with Existing Operators

		 		 		 		 Vim’s standard set of motions is fairly comprehensive, but we can augment it further by defining new motions and text objects.

Kana Natsuno’s textobj-entire plugin is a good example.[5] It adds two new text objects to Vim: ie and ae, which act upon the entire file.

If we wanted to autoindent the entire file using the = command, we could run gg=G (that is, gg to jump to the top of the file and then =G to autoindent everything from the cursor position to the end of the file). But if we had the textobj-entire plugin installed, we could simply run =ae. It wouldn’t matter where our cursor was when we ran this command; it would always act upon the entire file.

Note that if we had both the commentary and textobj-entire plugins installed, we could use them together. Running gcae would toggle commenting throughout the current file.

If you’re curious about how to create your own custom motions, start by reading omap-infoⓘ.

Meet Operator-Pending Mode

	 Normal, Insert, and Visual modes are readily identified, but Vim has other modes that are easy to overlook. Operator-Pending mode is a case in point. We use it dozens of times daily, but it usually lasts for just a fraction of a second. For example, we invoke it when we run the command dw. It lasts during the brief interval between pressing d and w keys. Blink and you’ll miss it!

If we think of Vim as a finite-state machine, then Operator-Pending mode is a state that accepts only motion commands. It is activated when we invoke an operator command, and then nothing happens until we provide a motion, which completes the operation. While Operator-Pending mode is active, we can return to Normal mode in the usual manner by pressing escape, which aborts the operation.

Many commands are invoked by two or more keystrokes (for examples, look up gⓘ, zⓘ, ctrl-wⓘ, or [ⓘ), but in most cases, the first keystroke merely acts as a prefix for the second. These commands don’t initiate Operator-Pending mode. Instead, we can think of them as namespaces that expand the number of available command mappings. Only the operator commands initiate Operator-Pending mode.

Why, you might be wondering, is an entire mode dedicated to those brief moments between invoking operator and motion commands, whereas the namespaced commands are merely an extension of Normal mode? Good question! Because we can create custom mappings that initiate or target Operator-Pending mode. In other words, it allows us to create custom operators and motions, which in turn allows us to expand Vim’s vocabulary.

Footnotes

[3]

http://vimgolf.com/

[4]

https://github.com/tpope/vim-commentary

[5]

https://github.com/kana/vim-textobj-entire

Copyright © 2016, The Pragmatic Bookshelf.

Chapter 3

Insert Mode

	Most of Vim’s commands are triggered from other modes, but some functionality is within easy reach from Insert mode. In this chapter, we’ll explore these commands. Although delete, yank, and put commands are all triggered from Normal mode, we’ll see that there is a convenient shortcut for pasting text from a register without leaving Insert mode. We’ll learn that Vim provides two easy ways for inserting unusual characters that are not represented on the keyboard.

Replace mode is a special case of Insert mode, which overwrites existing characters in the document. We’ll learn how to invoke this and consider some scenarios where it proves useful. We’ll also meet Insert Normal mode, a submode that lets us fire a single Normal mode command before dropping us back into Insert mode.

Autocompletion is the most advanced functionality available to us from Insert mode. We’ll cover it in depth in Chapter 19, ​Dial X for Autocompletion​.

Tip 13 Make Corrections Instantly from Insert Mode

	 	 	 If we make a mistake while composing text in Insert mode, we can fix it immediately. There’s no need to change modes. Besides the backspace key, we can use a couple of other Insert mode commands to make quick corrections.

	 Touch typing is more than just not looking at the keyboard; it means doing it by feel. When touch typists make an error, they know it even before their eyes process the information on the screen in front of them. They feel it in their fingers, like a misplaced step.

	 When we make a typing error, we can use the backspace key to erase the mistake and then make a correction. As long as the error appears near the end of the word, this may be the quickest strategy for making amends. But what if the mistake was at the start of the word?

Expert typists recommend drastic measures: delete the entire word; then type it out again. If you can type at a rate above sixty words per minute, retyping a word from scratch will only take a second. If you can’t type that fast, consider this to be good practice! There are particular words that I consistently mistype. Since I started following this advice, I’ve become more aware of which words trip me up. As a result, I now make fewer mistakes.

Alternatively, you could switch to Normal mode, navigate to the start of the word, fix the error, then hit A to return to where you left off in Insert mode. That little dance could take longer than a second, and it would do nothing to improve your touch-typing skills. Just because we can switch modes doesn’t mean that we should.

In Insert mode, the backspace key works just as you would expect: it deletes the character in front of the cursor. The following chords are also available to us:

KeystrokesEffect

		 		 		<C-h>

Delete back one character (backspace)

		 		 		<C-w>

Delete back one word

		 		 		<C-u>

Delete back to start of line

These commands are not unique to Insert mode or even to Vim. We can also use them in Vim’s command line as well as in the bash shell.

Tip 14 Get Back to Normal Mode

	 	 Insert mode is specialized for one task—entering text—whereas Normal mode is where we spend most of our time (as the name suggests). So it’s important to be able to switch quickly between them. This tip demonstrates a couple of tricks that reduce the friction of mode switching.

	 	 The classic way of getting back to Normal mode is with the <Esc> key, but on many keyboards that can seem like a long reach. Alternatively, we can press <C-[>, which has exactly the same effect (see i_CTRL-[ⓘ).

KeystrokesEffect

<Esc>

Switch to Normal mode

<C-[>

Switch to Normal mode

		 		<C-o>

Switch to Insert Normal mode

Vim novices frequently become fatigued by the constant need to switch modes, but with practice it starts to feel more natural. Vim’s modal nature can feel awkward in one particular scenario: when we’re in Insert mode and we want to run only one Normal command and then continue where we left off in Insert mode. Vim has a neat solution to ease the friction caused by switching modes: Insert Normal mode.

Meet Insert Normal Mode

Insert Normal mode is a special version of Normal mode, which gives us one bullet. We can fire off a single command, after which we’ll be returned to Insert mode immediately. From Insert mode, we can switch to Insert Normal mode by pressing <C-o> (i_CTRL-Oⓘ).

	 	 	 	 When the current line is right at the top or bottom of the window, I sometimes want to scroll the screen to see a bit more context. The zz command redraws the screen with the current line in the middle of the window, which allows us to read half a screen above and below the line we’re working on. I’ll often trigger this from Insert Normal mode by tapping out <C-o>zz. That puts me straight back into Insert mode so that I can continue typing uninterrupted.

Remap the Caps Lock Key

		 		 		For Vim users, the Caps Lock key is a menace. If Caps Lock is engaged and you try using the k and j keys to move the cursor around, you’ll instead trigger the K and J commands. Briefly: K looks up the man page for the word under the cursor (Kⓘ), and J joins the current and next lines together (Jⓘ). It’s surprising how quickly you can mangle the text in your buffer by accidentally enabling the Caps Lock key!

		Many Vim users remap the Caps Lock button to make it act like another key, such as <Esc> or <Ctrl>. On modern keyboards, the <Esc> key is difficult to reach, whereas the Caps Lock key is handy. Mapping Caps Lock to behave as an <Esc> key can save a lot of effort, especially since the <Esc> key is so heavily used in Vim. I prefer to map the Caps Lock button to behave instead as a <Ctrl> key. The <C-[> mapping is synonymous with <Esc>, and it’s easier to type when the <Ctrl> key is within easy reach. Additionally, the <Ctrl> key can be used for many other mappings, both in Vim and in other programs too.

The simplest way to remap the Caps Lock key is to do it at the system level. The methods differ on OS X, Linux, and Windows, so rather than reproducing instructions here for each system, I suggest that you consult Google. Note that this customization won’t just affect Vim: it applies system-wide. If you take my advice, you’ll throw away the Caps Lock key forever. You won’t miss it, I promise.

Tip 15 Paste from a Register Without Leaving Insert Mode

	 	 	 	 Vim’s yank and put operations are usually executed from Normal mode, but sometimes we might want to paste text into the document without leaving Insert mode.

Here’s an unfinished excerpt of text:

insert_mode/practical-vim.txt

​ Practical Vim, by Drew Neil

​ Read Drew Neil's

We want to complete the last line by inserting the title of this book. Since that text is already present at the start of the first line, we’ll yank it into a register and then append the text at the end of the next line in Insert mode:

KeystrokesBuffer Contents

yt,

​ Practical Vim, by Drew Neil

​ Read Drew Neil's

jA

​ Practical Vim, by Drew Neil

​ Read Drew Neil's

<C-r>0

​ Practical Vim, by Drew Neil

​ Read Drew Neil's Practical Vim

.<Esc>

​ Practical Vim, by Drew Neil

​ Read Drew Neil's Practical Vim.

	 	 	 The command yt, yanks the words Practical Vim into the yank register (we’ll meet the t{char} motion in Tip 50). In Insert mode, we can press <C-r>0 to paste the text that we just yanked at the current cursor position. We’ll discuss registers and the yank operation at greater length in Chapter 10, ​Copy and Paste​.

The general format of the command is <C-r>{register}, where {register} is the address of the register we want to insert (see i_CTRL-Rⓘ).

Use <C-r>{register} for Character-wise Registers

	 	 The <C-r>{register} command is convenient for pasting a few words from Insert mode. If the register contains a lot of text, you might notice a slight delay before the screen updates. That’s because Vim inserts the text from the register as if it were being typed one character at a time. If the ‘textwidth’ or ‘autoindent’ options are enabled, you might end up with unwanted line breaks or extra indentation.

	 The <C-r><C-p>{register} command is smarter. It inserts text literally and fixes any unintended indentation (see i_CTRL-R_CTRL-Pⓘ). But it’s a bit of a handful! If I want to paste a register containing multiple lines of text, I prefer to switch to Normal mode and use one of the put commands (see Tip 63).

Tip 16 Do Back-of-the-Envelope Calculations in Place

	 	 	 	 	 The expression register allows us to perform calculations and then insert the result directly into our document. In this tip, we’ll see one application for this powerful feature.

	 	 	 Most of Vim’s registers contain text either as a string of characters or as entire lines of text. The delete and yank commands allow us to set the contents of a register, while the put command allows us to get the contents of a register by inserting it into the document.

The expression register is different. It can evaluate a piece of Vim script code and return the result. Here, we can use it like a calculator. Passing it a simple arithmetic expression, such as 1+1, gives a result of 2. We can use the return value from the expression register just as though it were a piece of text saved in a plain old register.

The expression register is addressed by the = symbol. From Insert mode we can access it by typing <C-r>=. This opens a prompt at the bottom of the screen where we can type the expression that we want to evaluate. When done, we hit <CR>, and Vim inserts the result at our current position in the document.

Suppose that we’ve just typed the following:

insert_mode/back-of-envelope.txt

​ 6 chairs, each costing $35, totals $

There’s no need to scribble on the back side of an envelope. Vim can do the math for us, and we don’t even have to leave Insert mode. Here’s how:

KeystrokesBuffer Contents

A

​ 6 chairs, each costing $35, totals $

<C-r>=6*35<CR>

​ 6 chairs, each costing $35, totals $210

The expression register is capable of much more than simple arithmetic. We’ll meet a slightly more advanced example in Tip 71.

Tip 17 Insert Unusual Characters by Character Code

	 	 	 	 	 	 Vim can insert any character by its numeric code. This can be handy for entering symbols that are not found on the keyboard.

We can tell Vim to insert any arbitrary character if we know its numeric code. From Insert mode, we just have to type <C-v>{code}, where {code} is the address of the character that we want to insert.

Vim expects the numeric code to consist of three digits. Suppose, for example, that we wanted to insert an uppercase「A」character. The character code is 65, so we would have to enter it as <C-v>065.

	 But what if we wanted to insert a character whose numeric code is longer than three digits? For example, the Unicode Basic Multilingual Plane has an address space for up to 65,535 characters. It turns out that we can enter all of these using a four-digit hexadecimal code if we type <C-v>u{1234} (note the u preceding the digit this time). Let’s say we wanted to insert an inverted question mark symbol (「¿」), which is represented by the character code 00bf. From Insert mode, we would just have to type <C-v>u00bf. See i_CTRL-V_digitⓘ for more details.

	 	 	 	If you want to find out the numeric code for any character in your document, just place the cursor on it and trigger the ga command. This outputs a message at the bottom of the screen, revealing the character code in decimal and hexadecimal notations (see gaⓘ). Of course, this is of little help if you want to know the code for a character that is not already present in your document. In that case, you might want to look up the unicode tables.

In another scenario, if the <C-v> command is followed by any nondigit key, it will insert the character represented by that key literally. For example, if the ‘expandtab’ option is enabled, then pressing the <Tab> key will insert space characters instead of a tab character. However, pressing <C-v><Tab> will always insert a tab character literally, regardless of whether ‘expandtab’ is enabled or not.

Table 3, ​Inserting Unusual Characters​, summarizes the commands for entering unusual characters.

* * *

Table 3. Inserting Unusual Characters

KeystrokesEffect

<C-v>{123}

Insert character by decimal code

<C-v>u{1234}

Insert character by hexadecimal code

<C-v>{nondigit}

Insert nondigit literally

<C-k>{char1}{char2}

Insert character represented by {char1}{char2} digraph

* * *

Tip 18 Insert Unusual Characters by Digraph

	 	 	 	 	 	 While Vim allows us to insert any character by its numeric code, these can be hard to remember and awkward to type. We can also insert unusual characters as digraphs: pairs of characters that are easy to remember.

Digraphs are easy to use. From Insert mode, we just type <C-k>{char1}{char2}. So if we wanted to insert the「¿」character, which is represented by the digraph ?I, we would simply type <C-k>?I.

The character pairs that make up a digraph are chosen to be descriptive, making them easier to remember or even guess. For example, the double-angle quotation marks « and » are represented by the digraphs << and >>; the vulgar (or common) fractions ½, ¼, and ¾ are represented by the digraphs 12, 14, and 34, respectively. The default set of digraphs that ship with Vim follows certain conventions, which are summarized under digraphs-defaultⓘ.

We can view a list of the available digraphs by running :digraphs, but the output of this command is difficult to digest. A more usable list can be found by looking up digraph-tableⓘ.

Tip 19 Overwrite Existing Text with Replace Mode

	 	 	 	 Replace mode is identical to Insert mode, except that it overwrites existing text in the document.

Suppose that we had an excerpt of text such as this:

insert_mode/replace.txt

​ Typing in Insert mode extends the line. But in Replace mode

​ the line length doesn't change.

Instead of using two separate sentences, we’re going to run this together into a single sentence by changing the period to a comma. We also have to downcase the「B」in the word「But.」This example shows how we could do this using Replace mode.

KeystrokesBuffer Contents

{start}

​ Typing in Insert mode extends the line. But in Replace mode

​ the line length doesn't change.

f.

​ Typing in Insert mode extends the line. But in Replace mode

​ the line length doesn't change.

R,b<Esc>

​ Typing in Insert mode extends the line, but in Replace mode

​ the line length doesn't change.

	 	 From Normal mode, we can engage Replace mode with the R command. As the example demonstrates, typing「, b」overwrites the existing「. B」characters. And when we’re finished with Replace mode, we can hit the <Esc> key to return to Normal mode. Not all keyboards have an <Insert> key, but if yours does, then you can use it to toggle between Insert and Replace modes.

Overwrite Tab Characters with Virtual Replace Mode

	 	 	 	 Some characters can complicate matters for Replace mode. Consider the tab character. This is represented by a single character in the file, but onscreen it expands to fill several columns, as defined by the ‘tabstop’ setting (see 'tabstop'ⓘ). If we placed our cursor on a tab stop and initiated Replace mode, then the next character we typed would overwrite the tab character. Supposing that the ‘tabstop’ option was set to 8 (the default), this would appear to replace eight characters with one, causing a drastic reduction in the length of the current line.

Vim has a second variant of Replace mode. Virtual Replace mode is triggered with gR and treats the tab character as though it consisted of spaces. Suppose that we position the cursor on a tab stop spanning eight columns of screen real estate. If we switch to Virtual Replace mode, we could type up to seven characters, each of which would be inserted in front of the tab character. Finally, if we typed an eighth character, it would replace the tab stop.

	 In Virtual Replace mode, we overwrite characters of screen real estate rather than dealing with the actual characters that would eventually be saved in a file. This tends to produce fewer surprises, so I would recommend using Virtual Replace mode whenever possible.

	 	 Vim also provides a single-shot version of Replace mode and Virtual Replace mode. The r{char} and gr{char} commands allow us to overwrite a single character before switching straight back to Normal mode (rⓘ).

Copyright © 2016, The Pragmatic Bookshelf.

Chapter 4

Visual Mode


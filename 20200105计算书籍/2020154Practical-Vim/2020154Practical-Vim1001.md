Vim provides many ways of moving around within a document as well as commands for jumping between buffers. In this chapter we’ll focus on motions, which allow us to move around within a document.

Perhaps the simplest way of moving around is using the cursor keys. Vim allows us to navigate up, down, left, and right without moving our hands from the home row, as we’ll see in Tip 47. That’s a start, but there are quicker ways of moving around: Tip 49, shows how to move a word at a time; Tip 50, shows how to move with precision to any character within the current line; and Tip 51, shows how to use the search command for getting around.

Motions are not just for navigating around a document. They can also be used in Operator-Pending mode to perform real work, as discussed in Tip 12. Throughout this chapter, we’ll study examples of how motions can be used in combination with operator commands. The stars of Operator-Pending mode are text objects, which we’ll cover in Tip 52, and Tip 53.

Vim has a vast number of motions. We can’t cover them all in this chapter, so I recommend that you look up the motion.txtⓘ section of Vim’s documentation for a complete reference. Set yourself the goal of adding a couple of motions to your repertoire each week.

Tip 47 Keep Your Fingers on the Home Row

	 	 	 Vim is optimized for the touch typist. Learn to move around without removing your hands from the home row, and you’ll be able to operate Vim quicker.

The first thing you learn as a touch typist is that your fingers should rest on the home row. On a Qwerty keyboard, that means the left-hand fingers rest on a, s, d, and f, while the right-hand fingers rest on j, k, l, and ; keys. When poised in this position, we can reach for any other key on the keyboard without having to move our hands or look at our fingers. It’s the ideal posture for touch typing.

Just as with any other text editor, Vim lets us use the arrow keys to move the cursor around, but it also provides an alternative by way of the h, j, k, and l keys. They work as follows:

CommandMove cursor

h

One column left

l

One column right

j

One line down

k

One line up

	 	Admittedly, these cursor motions are not as intuitive to use as the arrow keys. The j and k keys are side by side, making it difficult to remember which goes up and which goes down. And the l key doesn’t move left, it moves right! The keys are assigned this way for historical reasons, so don’t go looking hard for a logical pattern.[15]

Here are a few pointers that might help if you’re struggling to remember which key does what. The letter j sort of looks like an arrow pointing downward. On a Qwerty keyboard, the h and l keys are positioned to the left and right of each other, mirroring the direction in which they move the cursor.

Although h, j, k, and l may seem unintuitive at first, learning to use them is worth your while. To reach for the arrow keys, you have to move your hand away from its resting place on the home row. Because the h, j, k, and l keys are all within easy reach, you can move Vim’s cursor without having to move your hand.

That might sound like a trivial saving, but it adds up. Once you’ve acquired the habit of using h, j, k, and l to move around, using any other editor that depends on the arrow keys will feel strange. You’ll wonder how you put up with it for so long!

Leave Your Right Hand Where It Belongs

On a Qwerty keyboard, the j, k, and l keys fall directly beneath the index, middle, and ring fingers of the right hand. We use the index finger to press the h key, but we have to reach for it. Some people see this as a problem, and as a solution they recommend shifting your entire right hand one step to the left so that h, j, k, and l are each covered by a finger. Please don’t do that.

As we’ll see throughout the rest of this chapter, Vim provides much quicker ways of moving around. You’re wasting keystrokes if you press the h key more than two times in a row. When it comes to moving horizontally, you can get around quicker using word-wise or character search motions (see Tip 49, and Tip 50).

I use the h and l keys for off-by-one errors, when I narrowly miss my target. Apart from that, I hardly touch them. Given how little I use the h key, I’m happy to have to stretch for it on a Qwerty keyboard. On the flip side, I use the character search commands often (see Tip 50), so I’m pleased that the ; key rests comfortably beneath my little finger.

Break the Habit of Reaching for the Arrow Keys

	 	 If you’re finding it difficult to break the habit of using the arrow keys, try putting this in your vimrc file:

motions/disable-arrowkeys.vim

​ noremap <Up> <Nop>

​ noremap <Down> <Nop>

​ noremap <Left> <Nop>

​ noremap <Right> <Nop>

	 This maps each of the arrow keys to do nothing. Each time you reach for the arrow keys, you’ll be reminded that you should have left your hand on the home row. It won’t take long to get the hang of using h, j, k, and l instead.

I don’t recommend keeping those mappings in your vimrc forever, just long enough to get into the habit of using h, j, k, and l. After that, you could always consider mapping the arrow keys to something more useful.

Tip 48 Distinguish Between Real Lines and Display Lines

	 	 Avoid frustration by learning the difference between real lines and display lines. Vim lets us operate on both.

	 Unlike many text editors, Vim makes a distinction between real lines and display lines. When the ‘wrap’ setting is enabled (and it’s on by default), each line of text that exceeds the width of the window will display as wrapped, ensuring that no text is truncated from view. As a result, a single line in the file may be represented by multiple lines on the display.

	 	 The easiest way to tell the difference between real lines and display lines is by enabling the ‘number’ setting. Lines that begin with a number correspond to the real lines, which may span one or more display lines. Each time a line is wrapped to fit inside the window, it begins without a line number. This screenshot shows a Vim buffer containing three real lines (numbered) and nine display lines:

	 	 Understanding the difference between real and display lines is important because Vim provides motions for interacting with both kinds. The j and k commands move down and up by real lines, whereas the gj and gk commands move down and up by display lines.

Consider our screenshot. Suppose that we wanted to move the cursor upward to position it on the word「vehicula.」Our target is one display line above the cursor, so we could get where we want to go by pressing gk. The k key would move up by a real line, placing our cursor on the word「ac,」which is not what we want in this case.

	 	 	 	 	 Vim also provides commands for jumping directly to the first or last character of a line. This table summarizes the commands for interacting with real and display lines:

CommandMove Cursor

j

Down one real line

gj

Down one display line

k

Up one real line

gk

Up one display line

0

To first character of real line

g0

To first character of display line

^

To first nonblank character of real line

g^

To first nonblank character of display line

$

To end of real line

g$

To end of display line

Note the pattern: j, k, 0, and $ all interact with real lines, while prefixing any of these with g tells Vim to act on display lines instead.

Most other text editors have no notion of the concept of real lines, and they provide the means to interact with display lines only. When you start out, it can be frustrating to discover that Vim seems to treat lines differently. When you learn to use the gj and gk commands, you’ll appreciate that j and k may let you cover more distance with fewer keystrokes.

Remap Line Motion Commands

If you would prefer to have the j and k keys operate on display lines rather than on real lines, you can always remap them. Try putting these lines into your vimrc file:

motions/cursor-maps.vim

​ nnoremap ​k​ gk

​ nnoremap gk ​k​

​ nnoremap ​j​ gj

​ nnoremap gj ​j​

These mappings make j and k move down and up by display lines, while gj and gk would move down and up by real lines (the opposite of Vim’s default behavior). I wouldn’t recommend using these mappings if you have to work with Vim on many different machines. In that case, getting used to Vim’s default behavior would be better.

Tip 49 Move Word-Wise

	 	 	 Vim has two speeds for moving backward and forward word-wise. Both allow for a more rapid traversal than moving by one column at a time.

Vim provides a handful of motions that let us move the cursor forward and backward by one word at a time (see word-motionsⓘ). They’re summarized in this table:

CommandMove Cursor

w

		 		Forward to start of next word

		 		b

Backward to start of current/previous word

e

		 		Forward to end of current/next word

ge

		Backward to end of previous word

We can think of these motions as coming in pairs: the w and b commands both target the start of a word, while the e and ge commands target the end of a word. w and e both advance the cursor forward, while b and ge move the cursor backward. This matrix of word-wise motions is illustrated here:

Trying to memorize all four of these commands isn’t easy, and I wouldn’t recommend it. Start off by using the w and b commands (think of them as (for-)word and back-word if you need a mnemonic). You should find that moving back and forward a word at a time is considerably faster than using h and l to move a column at a time.

The e and ge commands complete the set, but you can get by without them at first. Eventually you’ll notice that sometimes it would be useful to go directly to the end of the current word in a single move. For example, suppose that we want to turn the word「fast」into「faster」in this excerpt:

KeystrokesBuffer Contents

{start}

​ Go fast.

eaer<Esc>

​ Go faster.

Taken together, the ea commands can be read as「Append at the end of the current word.」I use ea often enough that it feels to me like a single command. Occasionally useful, the gea command can be read as「append at the end of the previous word.」

Know Your Words from Your WORDS

	 	 We’ve been talking a lot about words, but so far we haven’t pinned down what a word actually is. Vim provides two definitions and distinguishes between them by calling one a「word」and the other a「WORD.」Each word-wise motion we met earlier has a WORD-wise equivalent, including W, B, E, and gE.

A word consists of a sequence of letters, digits, and underscores, or as a sequence of other nonblank characters separated with whitespace (see wordⓘ). The definition of a WORD is simpler: it consists of a sequence of nonblank characters separated with whitespace (see WORDⓘ).

Ok, but what does that actually mean? The details we can leave to Vim’s implementors. As users, we can think of them in simpler terms: WORDS are bigger than words! Look at this text and quickly count the number of words:

​ e.g. we're going too slow

Did you count five or ten (or something in between)? That example contains five WORDS and ten words. The periods and apostrophes count as words, so if we try to advance through this text with the w command, it’ll be slow going:

KeystrokesBuffer Contents

{start}

​ e.g. we're going too slow

wwww

​ e.g. we're going too slow

www

​ e.g. we're going too slow

If we move WORD-wise instead, we make progress with fewer keystrokes:

KeystrokesBuffer Contents

{start}

​ e.g. we're going too slow

W

​ e.g. we're going too slow

W

​ e.g. we're going too slow

In this example, the WORD-wise motions appear to be the better choice, but that won’t be true every time. Sometimes we’ll want to act on「we」as a word. For example, if we wanted it to read「you」instead, we would do this:

KeystrokesBuffer Contents

{start}

​ e.g. we're going too slow

cwyou<Esc>

​ e.g. you're going too slow

Other times, we might prefer to treat「we’re」as a WORD. For example, if we wanted to change it to read「it’s」instead, we would do this:

KeystrokesBuffer Contents

{start}

​ e.g. we're going too slow

cWit’s<Esc>

​ e.g. it's going too slow

Use WORD-wise motions if you want to move faster, and use word-wise motions if you want a more fine-grained traversal. Play around with them, and you’ll get a feel for when to use words and when to use WORDS. You can develop an intuition for these things without fully understanding the implementation details.

Tip 50 Find by Character

	 	 	 	 Vim’s character search commands allow us to move quickly within a line, and they work beautifully in Operator-Pending mode.

	 The f{char} command is one of the quickest methods of moving around in Vim. It searches for the specified character, starting with the cursor position and continuing to the end of the current line. If a match is found, then the cursor advances to the specified character. If no match is found, then the cursor stays put (see fⓘ).

That may sound complex, but it’s quite simple in practice. Observe:

KeystrokesBuffer Contents

{start}

​ Find the first occurrence of {char} and move to it.

fx

​ Find the first occurrence of {char} and move to it.

fo

​ Find the first occurrence of {char} and move to it.

In this case, the fx command does nothing. Vim searches forward for an occurrence of the「x」character, but no matches are found, so the cursor doesn’t move. The fo command finds an occurrence of the「o」character, so the cursor is positioned on top of the first match.

If we need to position our cursor at the start of the word「occurrence,」there’s no way we can do it with fewer than two keystrokes. The f{char} command is efficient, and when it works as well as it does in this example, it feels as though Vim is reading our minds.

But the f{char} command doesn’t always work out so well. Suppose that we wanted to position our cursor on the「c」at the start of the word {char}. Watch what happens when we use the fc command:

KeystrokesBuffer Contents

{start}

​ Find the first occurrence of {char} and move to it.

fc

​ Find the first occurrence of {char} and move to it.

;

​ Find the first occurrence of {char} and move to it.

;

​ Find the first occurrence of {char} and move to it.

;

​ Find the first occurrence of {char} and move to it.

	 The「c」character occurs several times on this line, so this time we don’t make a direct hit on our target. It takes a few attempts to move the cursor to the position where we want it. Luckily we don’t have to explicitly repeat the fc command. Vim keeps track of the most recent f{char} search, and we can repeat it using the ; command (see ;ⓘ). In this example, we have to press ; three times to maneuver the cursor into position.

The f{char} and ; commands make a powerful combination, and we can cover a lot of distance with very few keystrokes. But where the cursor will end up isn’t always obvious. As a result, it’s easy to get trigger-happy with the ; key, and occasionally we’ll miss our target. For example, suppose that we want to place the cursor at the start of the word「of」:

KeystrokesBuffer Contents

{start}

​ Find the first occurrence of {char} and move to it.

fo

​ Find the first occurrence of {char} and move to it.

;;

​ Find the first occurrence of {char} and move to it.

,

​ Find the first occurrence of {char} and move to it.

	 	 Having accidentally overshot our mark, we can back up using the , command. This repeats the last f{char} search but in the opposite direction (see ,ⓘ). Remember our mantra from Tip 4: act, repeat, reverse. I think of , as a safety net for those times when I get overzealous with the ; key.

Don't Throw Away the Reverse Character Search Command

	 	 	 Vim assigns a function to almost every key on the keyboard. If we want to create our own custom mappings, which keys should we bind them to? Vim provides the <Leader> key as a namespace for our own user-defined commands. Here is how we can create our own custom mappings using <Leader>:

​ noremap <Leader>​n​ nzz

​ noremap <Leader>N Nzz

The default leader key is \, so we could trigger these custom mappings by pressing \n and \N. If you want to know what these mappings do, look up zzⓘ.

On some keyboards, the \ command is inconvenient to reach, so Vim makes it easy to set the leader key to something else (see mapleaderⓘ). A common choice is to set the comma key as leader. If you take this route, I strongly recommend mapping the reverse character search command to another key. Here’s an example:

​ ​let​ mapleader=​","​

​ noremap \ ,

The ; and , commands complement each other. If you take one of them away, then the whole family of character search commands becomes much less useful.

Character Searches Can Include or Exclude the Target

The f{char}, ;, and , commands are part of a set of character-search commands. This table lists them all:

CommandEffect

f{char}

Forward to the next occurrence of {char}

F{char}

		 		 Backward to the previous occurrence of {char}

t{char}

		 		 Forward to the character before the next occurrence of {char}

T{char}

		 		 Backward to the character after the previous occurrence of {char}

;

Repeat the last character-search command

,

Reverse the last character-search command

Think of the t{char} and T{char} commands as searching till the specified character. The cursor stops one character before {char}, whereas the f{char} and F{char} commands position the cursor on top of the specified character.

It’s not immediately obvious why you would want both kinds of character search. This example demonstrates them in action:

KeystrokesBuffer Contents

{start}

​ I've been expecting you, Mister Bond.

f,

​ I've been expecting you, Mister Bond.

dt.

​ I've been expecting you.

To begin with, we want to position our cursor directly on top of the comma symbol. For this we can use the f, command. Next we want to delete all of the text until the end of the sentence, but not including the period symbol itself. This time, the dt. command does the job.

Alternatively, we could have used dfd, which would delete everything from the cursor position to the last letter of the word「Bond.」The end result is the same either way, but I find that dt. requires less concentration. Deleting through the letter「d」is not a common pattern, whereas deleting the last clause of a sentence is something we do often enough that we can treat f,dt. as a finger macro.

In general, I tend to use f{char} and F{char} in Normal mode when I want to move the cursor quickly within the current line, whereas I tend to use the t{char} and T{char} character search commands in combination with d{motion} or c{motion}. To put it another way, I use f and F in Normal mode, and t and T in Operator-Pending mode. Refer to Tip 12 (and ​Meet Operator-Pending Mode​), for more details.

Think Like a Scrabble® Player

The character search commands can be highly economical with keystrokes, but their efficiency varies depending on our choice of target. As any Scrabble player can tell you, some letters appear more frequently than others. If we can make a habit of choosing less common characters for use with the f{char} command, then we’ll be more likely to strike our target with a single move.

Suppose that we wanted to delete the only adjective from this sentence:

​ Improve your writing by deleting excellent adjectives.

	 What motion should we use to position our cursor on the word「excellent」? If we target the first letter by pressing fe, then we have to follow up by pressing ;;; to skip all of the obstacles in between. A better choice would be fx, which gets us where we want to go with a single move. From there, we can delete the word with the daw command (for more details about aw, see Tip 53).

Take a look at the text that you’re reading. It’s composed almost entirely of lowercase letters. Capital letters are much rarer, and so too are punctuation marks. When using the character search commands, it’s better to choose target characters with a low frequency of occurrences. With practice you’ll learn to spot them.

Tip 51 Search to Navigate

	 	 	 The search command allows us to rapidly cover distances both large and small with very few keystrokes.

The character search commands (f{char}, t{char}, and so on) are fast and lightweight, but they have limitations. They can only search for a single character at a time, and they can only operate within the current line. If we need to search for more than one character or move beyond the current line, then we can use the search command instead.

Suppose that we want to position our cursor on the word「takes」in this sample:

motions/search-haiku.txt

​ search for your target

​ it only takes a moment

​ to get where you want

We could do so by searching for the word: /takes<CR>. It only occurs once in this short sample, so that would be sure to get us where we want to go in a single move. But let’s see if we can we do it with even fewer keystrokes:

KeystrokesBuffer Contents

{start}

​ search for your target

​ it only takes a moment

​ to get where you want

/ta<CR>

​ search for your target

​ it only takes a moment

​ to get where you want

/tak<CR>

​ search for your target

​ it only takes a moment

​ to get where you want

Searching for the two-letter string「ta」gets two hits, but the three-letter string「tak」has one unique hit. In this example, the search motion makes a short hop, but in a large document we can use this technique to cover great distances with few keystrokes. The search command is a very economical way to move around.

Even if we had searched for the two-letter「ta」fragment and ended up in the wrong place, we could jump to the next occurrence by repeating the previous search with the n command. Also, if we pressed the n key too many times, we could back up again with the N command. The mantra from Tip 4, should be becoming familiar by now: act, repeat, reverse.

In the previous tip, we saw that the fe command was rarely useful because the letter e is so common. We can get around this shortcoming by searching for a string of two or more letters in sequence. Although e may appear many times in the English language, only a fraction of those occurrences are succeeded immediately by the letter r. It’s surprising how often we can jump to any word of our choice just by searching for the first few characters.

In our「takes」example, I enabled the ‘hlsearch’ feature to highlight the search matches. When searching for a short string, we’ll often find multiple matches scattered across the document. Results can get unsightly when the ‘hlsearch’ option is enabled, so you might want to disable this feature if you make a habit of using the search command to navigate (it’s off by default). However, the ‘incsearch’ option is very useful in this use case. Refer to Tip 82, for more details.

Operate with a Search Motion

	 	 	 We’re not limited to using the search command in Normal mode. We can use it from Visual and Operator-Pending modes just as well to do real work. For example, suppose that we wanted to delete the text「takes time but eventually」from this phrase:

KeystrokesBuffer Contents

v

​ This phrase takes time but

​ eventually gets to the point.

/ge<CR>

​ This phrase takes time but

​ eventually gets to the point.

h

​ This phrase takes time but

​ eventually gets to the point.

d

​ This phrase gets to the point.

To begin with, we press v to switch to Visual mode. Then we can extend the selection by searching for the short「ge」string, which puts the cursor where we want it in a single bound. Well, almost—we have an off-by-one error. The selection includes the「g」at the start of the word, but we don’t want to delete that. We’ll use h to back up one character. Then, having defined our selection, we’ll delete it with the d command.

Here’s an even quicker way of doing the same thing:

KeystrokesBuffer Contents

{start}

​ This phrase takes time but

​ eventually gets to the point.

d/ge<CR>

​ This phrase gets to the point.

	 Here, we use the /ge<CR> search motion to tell the d{motion} command what to delete. The search command is an exclusive motion. That means that even though our cursor ends up on the「g」at the start of the word「gets,」that character is excluded from the delete operation (see exclusiveⓘ).

By staying out of Visual mode, we’ve cut out two unnecessary keystrokes (see also Tip 23). It takes a bit of getting used to, but combining the d{motion} operator with the search motion is a power move. Use it to amaze your friends and coworkers.

Tip 52 Trace Your Selection with Precision Text Objects

	 	 	 Text objects allow us to interact with parentheses, quotes, XML tags, and other common patterns that appear in text.

Take a look at this code sample:

motions/template.js

​ ​var​ tpl = [

​ ​'<a href="{url}">{title}</a>'​

​ ]

Each opening { character is balanced by a closing } character. The same is true of [ and ], < and >, and the opening and closing HTML tags, <a> and </a>. This sample also contains single and double quotation marks, which come in pairs.

Vim understands the structure of these well-formed patterns, and it allows us to operate on the regions of text that they delimit. Text objects define regions of text by structure (see text-objectsⓘ). With only a couple of keystrokes, we can use these to select or operate on a chunk of text.

	 Suppose that our cursor was positioned inside a set of curly braces and we wanted to visually select the text inside the {}. Press vi}:

KeystrokesBuffer Contents

{start}

​ var tpl = [

​ '<a href="{url}">{title}</a>'

​ ]

vi}

​ var tpl = [

​ '<a href="{url}">{title}</a>'

​ ]

a"

​ var tpl = [

​ '<a href="{url}">{title}</a>'

​ ]

i>

​ var tpl = [

​ '<a href="{url}">{title}</a>'

​ ]

it

​ var tpl = [

​ '<a href="{url}">{title}</a>'

​ ]

at

​ var tpl = [

​ '<a href="{url}">{title}</a>'

​ ]

a]

​ var tpl = [

​ ’<a href="{url}">{title}</a>’

​ ]

Normally when we use Visual mode, one end of the selection is anchored to a particular character, while the other end of the selection is free to move. When we use motions such as l, w, and f{char}, we can expand or contract the selection by moving the free end of the visual range.

What’s happening here is different. When we press vi}, Vim initiates Visual mode and then selects all of the characters contained by the {} braces. Where the cursor is positioned to begin with doesn’t matter so long as it’s located somewhere inside a block of curly braces when the i} text object is invoked.

	 	 	 	 	 	 We can expand the selection again using another text object. For example, a" selects a range of characters delimited by double quotes. i> selects everything inside a pair of angle brackets.

Vim’s text objects consist of two characters, the first of which is always either i or a. In general, we can say that the text objects prefixed with i select inside the delimiters, whereas those that are prefixed with a select everything including the delimiters. As a mnemonic, think of i as inside and a as around (or all).

In the previous example, check whether the text object leads with i or a. In particular, note the difference between it and at. Note, too, that in this example a] expands the selection to span multiple lines.

A partial list of Vim’s built-in text objects is summarized in the following table. In the interests of neatness, some duplicates have been omitted. For example, i( and i) are equivalent to each other, and so too are a[ and a]. Use whichever style you find most comfortable.

Text ObjectSelectionText ObjectSelection

a) or ab

A pair of (parentheses)

i) or ib

Inside of (parentheses)

a} or aB

A pair of {braces}

i} or iB

Inside of {braces}

a]

A pair of [brackets]

i]

Inside of [brackets]

a>

A pair of <angle brackets>

i>

Inside of <angle brackets>

a’

A pair of ’single quotes’

i’

Inside of ’single quotes’

a"

A pair of "double quotes"

i"

Inside of "double quotes"

a`

A pair of `backticks`

i`

Inside of `backticks`

at

A pair of <xml>tags</xml>

it

Inside of <xml>tags</xml>

Performing Operations with Text Objects

Visual mode makes for a nice introduction to text objects because it’s easy to see what’s happening. But text objects reveal their true power when we use them in Operator-Pending mode.

Text objects are not motions themselves: we can’t use them to navigate around the document. But we can use text objects in Visual mode and in Operator-Pending mode. Remember this: whenever you see {motion} as part of the syntax for a command, you can also use a text object. Common examples include d{motion}, c{motion}, and y{motion} (see Table 2, ​Vim’s Operator Commands​, for more).

	 Let’s demonstrate using the c{motion} command, which deletes the specified text and then switches to Insert mode (cⓘ). We’ll use it to replace {url} with a # symbol, and then again to replace {title} with a placeholder:

KeystrokesBuffer Contents

{start}

​ '<a href="{url}">{title}</a>'

ci"#<Esc>

​ '<a href="#">{title}</a>'

citclick here<Esc>

​ '<a href="#">click here</a>'

We can read the ci" command as「change inside the double quotes.」The cit command can be read as「change inside the tag.」We could just as easily use the yit command to yank the text from inside the tag, or dit to delete it.

Discussion

Each of these commands requires only three keystrokes, and yet they’re elegant in spite of this terseness. I would almost go so far as to say that they are self-documenting. That’s because these commands follow the rules of Vim’s simple grammar, which is covered in Tip 12.

In Tip 50, and Tip 51, we learned a couple of tricks that allow us to move the cursor with precision. Whether we’re using f{char} to search for a single character or /target<CR> to search for several characters, the pattern of usage is the same: we look for a suitable target, take aim, and then fire. If we’re good, we’ll hit our target with a single move. These power moves allow us to cover a lot of ground with little effort.

Text objects are the next level up. If the f{char} and /pattern<CR> commands are like a flying kick to the head, then text objects are like a scissors kick that strikes two targets with a single move:

Tip 53 Delete Around, or Change Inside

	 	 	 Text objects usually come in pairs: one that acts inside the object and another that acts around the object. In this tip, we’ll examine a typical use case for each kind of text object.

Vim’s text objects fall into two categories: those that interact with pairs of delimiters, such as i), i", and it, and those that interact with chunks of text, such as words, sentences, and paragraphs. Here’s a summary of the latter.

KeystrokesCurrent…KeystrokesCurrent…

iw

word

aw

word plus space(s)

iW

WORD

aW

WORD plus space(s)

is

sentence

as

sentence plus space(s)

ip

paragraph

ap

paragraph plus blank line(s)

	 	 	 	 	 	 I’ve labeled the first category as delimited text objects because they begin and end with matching symbols. Words, sentences, and paragraphs are defined by boundaries, so I’ve labeled this category as bounded text objects (Vim’s documentation calls them「block」and「non-block」objects, but I find that to be an unhelpful distinction).

	 	 Let’s compare the iw and aw text objects. Using our mnemonic, we can think of these as acting inside the word or around the word, respectively. But what does that mean?

The iw text object interacts with everything from the first to the last character of the current word. The aw text object does the same, but it extends the range to include any whitespace characters after or before the word, if whitespace is present. To see how Vim defines the boundaries of a word, refer to Tip 49.

The distinction between iw and aw is subtle, and it’s not immediately obvious why we need them both, so let’s look at a typical use case for each of them.

	 Suppose that we want to delete the word「excellent」from the following sentence. We can do it using the daw command:

KeystrokesBuffer Contents

{start}

​ Improve your writing by deleting excellent adjectives.

daw

​ Improve your writing by deleting adjectives.

	 This deletes the word plus one space, giving a clean result. If we used diw instead, then we’d end up with two adjacent spaces, which is probably not what we want.

	 Now let’s suppose that we want to change the word to something else. This time we’ll use the ciw command:

KeystrokesBuffer Contents

{start}

​ Improve your writing by deleting excellent adjectives.

ciwmost<Esc>

​ Improve your writing by deleting most adjectives.

	 The ciw command deletes the word without trimming any whitespace and then puts us into Insert mode. That’s just what we want. If we had used caw instead, then we’d end up running words together to read「mostadjectives.」That would be easy enough to mend, but it’s better still if we can avoid the problem altogether.

As a general rule, we could say that the d{motion} command tends to work well with aw, as, and ap, whereas the c{motion} command works better with iw and similar.

Tip 54 Mark Your Place and Snap Back to It

	 	 	 	 Vim’s marks allow us to jump quickly to locations of interest within a document. We can set marks manually, but Vim also keeps track of certain points of interest for us automatically.

	 	 The m{a-zA-Z} command marks the current cursor location with the designated letter (mⓘ). Lowercase marks are local to each individual buffer, whereas uppercase marks are globally accessible. We’ll learn more about them in Tip 59. Vim does nothing to indicate that a mark has been set, but if you’ve done it right, then you should be able to jump directly to your mark with only two keystrokes from anywhere in the file.

	 	 	 Vim provides two Normal mode commands for jumping to a mark. (Pay attention—they look similar!) ’{mark} moves to the line where a mark was set, positioning the cursor on the first non-whitespace character. The `{mark} command moves the cursor to the exact position where a mark was set, restoring the line and the column at once (see mark-motionsⓘ).

If you commit only one of these commands to memory, go with `{mark}. Whether you care about restoring the exact position or just getting to the right line, this command will get you there. The only time you have to use the ’{mark} form is in the context of an Ex command (see Tip 28).

	 	 The mm and `m commands make a handy pair. Respectively, they set the mark m and jump to it. ​Swap Two Words​, shows one example of how they can be used for a quick mark-then-snap-back maneuver.

Automatic Marks

	 	 We can set up to twenty-six lowercase marks per buffer. That’s one mark for each letter of the alphabet, and it’s way more than you’re ever likely to need! In Vim’s predecessor, vi, there was no such thing as Visual mode. Back then, marks would have been a much more important feature than they are now. Many of the tasks that would have required a mark in vi can be done in Vim using Visual mode.

But marks have not become obsolete in Vim; they still have their uses. In particular, the marks that Vim sets for us automatically can be really handy. They include the marks shown in Table 10, ​Vim’s Automatic Marks​.

* * *

Table 10. Vim’s Automatic Marks

KeystrokesBuffer Contents

「

Position before the last jump within current file

‘.

Location of last change

‘^

Location of last insertion

‘[

Start of last change or yank

‘]

End of last change or yank

‘<

Start of last visual selection

‘>

End of last visual selection

* * *

	 The `` mark complements the jump list (Tip 56), and we’ll see a use for it in the next tip. The `. complements the change list, which is covered by Tip 57.

The start and end of the last visual selection are both recorded automatically as marks, so we might even consider Visual mode to be a fancy interface to the underlying marks feature.

Tip 55 Jump Between Matching Parentheses

	 	 	 	 Vim provides a motion that lets us move between opening and closing pairs of parentheses. By enabling the matchit.vim plugin, we can extend this behavior to work on pairs of XML tags as well as on keywords in some programming languages.

	 The % command lets us jump between opening and closing sets of parentheses (see %ⓘ). It works with (), {}, and [], as this example demonstrates:

KeystrokesBuffer Contents

{start}

​ console.log([{'a':1},{'b':2}])

%

​ console.log([{'a':1},{'b':2}])

h

​ console.log([{'a':1},{'b':2}])

%

​ console.log([{'a':1},{'b':2}])

l

​ console.log([{'a':1},{'b':2}])

%

​ console.log([{'a':1},{'b':2}])

To see how we might use % in practice, let’s use this short extract of Ruby:

motions/parentheses.rb

​ cities = ​%w{London Berlin New\ York}​

Suppose that we want to switch from the %w{London Berlin New\ York} syntax to a regular list definition: ["London", "Berlin", "New York"]. We’ll have to switch opening and closing curly braces to square brackets. You might think that this would be a perfect occasion to use the % motion. You’d be right, but there’s a gotcha!

Let’s say that we start off by positioning our cursor on the opening curly brace and then we press r[ to change it to an opening square bracket. Now we’ve got this strange-looking construct: [London Berlin New\ York}. The % command only works on well-formed matching parentheses, so we can’t use it to jump to the closing } character.

	 The trick here is to use the % command before making any changes. When we use the % command, Vim automatically sets a mark for the location from which we jumped. We can snap back to it by pressing ``. Here’s a partial solution for our example refactoring:

KeystrokesBuffer Contents

{start}

​ cities = %w{London Berlin New\ York}

dt{

​ cities = {London Berlin New\ York}

%

​ cities = {London Berlin New\ York}

r]

​ cities = {London Berlin New\ York]

``

​ cities = {London Berlin New\ York]

r[

​ cities = [London Berlin New\ York]

	 Note that in this case, the <C-o> command would work just as well as the `` motion (see Tip 56). The surround.vim plugin provides commands that would make this task even easier. Find out more in ​Surround.vim​.

Jump Between Matching Keywords

	 	 Vim ships with a plugin called matchit, which enhances the functionality of the % command. When this plugin is enabled, the % command can jump between matching pairs of keywords. For example, in an HTML file, the % command would jump between opening and closing tags. In a Ruby file, it would jump between class/end, def/end, and if/end pairs.

	 Even though matchit ships with the Vim distribution, it’s not enabled by default. This minimal vimrc would make Vim autoload the matchit plugin on startup:

​ ​set​ nocompatible

​ ​filetype​ plugin ​on​

​ runtime macros/matchit.​vim​

The enhancements provided by this plugin are very useful, so I’d recommend enabling it. Consult matchit-installⓘ for more details.

Surround.vim

	 	 One of my favorite plugins is surround.vim by Tim Pope,[16] which makes wrapping a selection with a pair of delimiters easy. For example, we could put the words New York in quote marks:

KeystrokesBuffer Contents

{start}

​ cities = ["London", "Berlin", New York]

vee

​ cities = ["London", "Berlin", New York]

S"

​ cities = ["London", "Berlin", "New York"]

	 The S" command is provided by surround.vim, and it can be read as「Surround the selection with a pair of double quote marks.」We could just as easily use S) or S} if we wanted to wrap the selection with opening and closing parentheses or braces.

We can also use surround.vim to change existing delimiters. For example, we could change {London} to [London] with the cs}] command, which can be read as「Change surrounding {} braces to [] brackets.」Or we could go the other way with the cs]} command. It’s a powerful plugin—check it out.

Footnotes

[15]

http://www.catonmat.net/blog/why-vim-uses-hjkl-as-arrow-keys/

[16]

http://github.com/tpope/vim-surround

Copyright © 2016, The Pragmatic Bookshelf.

Chapter 9

Navigate Between Files with Jumps


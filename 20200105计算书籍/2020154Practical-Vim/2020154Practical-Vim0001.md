# 0001. The Vim Way

Our work is repetitive by nature. Whether we’re making the same small change in several places or moving around between similar regions of a document, we repeat many actions. Anything that can streamline a repetitive workflow will save our time multifold.

Vim is optimized for repetition. Its efficiency stems from the way it tracks our most recent actions. We can always replay the last change with a single keystroke. Powerful as this sounds, it’s useless unless we learn to craft our actions so that they perform a useful unit of work when replayed. Mastering this concept is the key to becoming effective with Vim.

The dot command is our starting point. This seemingly simple command is the most versatile tool in the box, and understanding it is the first step toward Vim mastery. We’ll work through a handful of simple editing tasks that can be rapidly completed with the dot command. Although each task looks quite different from the next, their solutions almost converge. We’ll identify an ideal editing formula, which requires only one keystroke to move and another to execute.

### Tip 1 Meet the Dot Command

The dot command lets us repeat the last change. It is the most powerful and versatile command in Vim.

Vim’s documentation simply states that the dot command「repeats the last change」(see .ⓘ). It doesn’t sound like much, but in that simple definition we’ll find the kernel of what makes Vim’s modal editing model so effective. First we have to ask,「What is a change?」

	 To understand the power of the dot command, we have to realize that the「last change」could be one of many things. A change could act at the level of individual characters, entire lines, or even the whole file.

To demonstrate, we’ll use this snippet of text:

the_vim_way/0_mechanics.txt

​ Line one

​ Line two

​ Line three

​ Line four

The x command deletes the character under the cursor. When we use the dot command in this context,「repeat last change」tells Vim to delete the character under the cursor:

KeystrokesBuffer Contents

{start}

​ Line one

​ Line two

​ Line three

​ Line four

x

​ ine one

​ Line two

​ Line three

​ Line four

.

​ ne one

​ Line two

​ Line three

​ Line four

..

​  one

​ Line two

​ Line three

​ Line four

We can restore the file to its original state by pressing the u key a few times to undo the changes.

	 	 	 The dd command also performs a deletion, but this one acts on the current line as a whole. If we use the dot command after dd, then「repeat last change」instructs Vim to delete the current line:

KeystrokesBuffer Contents

{start}

​ Line one

​ Line two

​ Line three

​ Line four

dd

​ Line two

​ Line three

​ Line four

.

​ Line three

​ Line four

		 		 		Finally, the >G command increases the indentation from the current line until the end of the file. If we follow this command with the dot command, then「repeat last change」tells Vim to increase the indentation level from the current position to the end of the file. In this example, we’ll start with the cursor on the second line to highlight the difference

KeystrokesBuffer Contents

{start}

​ Line one

​ Line two

​ Line three

​ Line four

>G

​ Line one

​ Line two

​ Line three

​ Line four

j

​ Line one

​ Line two

​ Line three

​ Line four

.

​ Line one

​ Line two

​ Line three

​ Line four

j.

​ Line one

​ Line two

​ Line three

​ Line four

	 	 	 	 	 The x, dd, and > commands are all executed from Normal mode, but we also create a change each time we dip into Insert mode. From the moment we enter Insert mode (by pressing i, for example) until we return to Normal mode (by pressing <Esc>), Vim records every keystroke. After making a change such as this, the dot command will replay our keystrokes (see ​Moving Around in Insert Mode Resets the Change​, for a caveat).

The Dot Command Is a Micro Macro

	 	 Later, in Chapter 11, ​Macros​, we’ll see that Vim can record any arbitrary number of keystrokes to be played back later. This allows us to capture our most repetitive workflows and replay them at a keystroke. We can think of the dot command as being a miniature macro, or a「micro」if you prefer.

	 	 	 	 We’ll see a few applications of the dot command throughout this chapter. We’ll also learn a couple of best practices for working with the dot command in Tip 9, and Tip 23.

Tip 2 Don’t Repeat Yourself

For such a common use case as appending a semicolon at the end of a series of lines, Vim provides a dedicated command that combines two steps into one.

	 Suppose that we have a snippet of JavaScript code like this:

the_vim_way/2_foo_bar.js

​ ​var​ foo = 1

​ ​var​ bar = ​'a'​

​ ​var​ foobar = foo + bar

	 	 	 	 We need to append a semicolon at the end of each line. Doing so involves moving our cursor to the end of the line and then switching to Insert mode to make the change. The $ command will handle the motion for us, and then we can run a;<Esc> to make the change.

To finish the job, we could run the exact same sequence of keystrokes on the next two lines, but that would be missing a trick. The dot command will repeat that last change, so instead of duplicating our efforts, we could just run j$. twice. One keystroke (.) buys us three (a;<Esc>). It’s a small saving, but these efficiencies accumulate when repeated.

	 	 		 But let’s take a closer look at this pattern: j$.. The j command moves the cursor down one line, and then the $ command moves it to the end of the line. We’ve used two keystrokes just to maneuver our cursor into position so that we can use the dot command. Do you sense that there’s room for improvement here?

Reduce Extraneous Movement

		 		 		While the a command appends after the current cursor position, the A command appends at the end of the current line. It doesn’t matter where our cursor is at the time, pressing A will switch to Insert mode and move the cursor to the end of the line. In other words, it squashes $a into a single keystroke. In ​Two for the Price of One​, we see that Vim has a handful of compound commands.

Two for the Price of One

We could say that the A command compounds two actions ($a) into a single keystroke. It’s not alone in doing this. Many of Vim’s single-key commands can be seen as a condensed version of two or more other commands. The table below shows an approximation of some examples. Can you identify anything else that they all have in common?

Compound Command

Equivalent in Longhand

C

c$

s

cl

S

^C

I

^i

A

$a

o

A<CR>

O

ko

If you catch yourself running ko (or worse, k$a<CR>), stop! Think about what you’re doing. Then recognize that you could have used the O command instead.

Did you identify the other property that these commands share? They all switch from Normal to Insert mode. Think about that and how it might affect the dot command.

Here is a refinement of our previous example:

KeystrokesBuffer Contents

{start}

​ var foo = 1

​ var bar = 'a'

​ var foobar = foo + bar

A;<Esc>

​ var foo = 1;

​ var bar = 'a'

​ var foobar = foo + bar

j

​ var foo = 1;

​ var bar = 'a'

​ var foobar = foo + bar

.

​ var foo = 1;

​ var bar = 'a';

​ var foobar = foo + bar

j.

​ var foo = 1;

​ var bar = 'a';

​ var foobar = foo + bar;

		 		 		By using A instead of $a, we give the dot command a boost. Instead of having to position the cursor at the end of the line we want to change, we just have to make sure it is somewhere (anywhere!) on that line. Now we can repeat the change on consecutive lines just by typing j. as many times as it takes.

One keystroke to move, another to execute. That’s about as good as it gets! Watch for this pattern of usage, because we’ll see it popping up in a couple more examples.

	 Although this formula looks terrific for our short example, it’s not a universal solution. Imagine if we had to append a semicolon to fifty consecutive lines. Pressing j. for each change starts to look like a lot of work. For an alternative approach, skip ahead to Tip 30.

Tip 3 Take One Step Back, Then Three Forward

We can pad a single character with two spaces (one in front, the other behind) by using an idiomatic Vim solution. At first it might look slightly odd, but the solution has the benefit of being repeatable, which allows us to complete the task effortlessly.

	 	 	 Suppose that we have a line of code that looks like this:

the_vim_way/3_concat.js

​ ​var​ foo = ​"method("​+argument1+​","​+argument2+​")"​;

	 	 Concatenating strings in JavaScript never looks pretty, but we could make this a little easier on the eye by padding each + sign with spaces to make it look like this:

​ ​var​ foo = ​"method("​ + argument1 + ​","​ + argument2 + ​")"​;

Make the Change Repeatable

This idiomatic approach solves the problem:

Keystrokes

Buffer Contents

{start}

​ var foo = "method("+argument1+","+argument2+")";

f+

​ var foo = "method("+argument1+","+argument2+")";

s+<Esc>

​ var foo = "method(" + argument1+","+argument2+")";

;

​ var foo = "method(" + argument1+","+argument2+")";

.

​ var foo = "method(" + argument1 + ","+argument2+")";

;.

​ var foo = "method(" + argument1 + "," + argument2+")";

;.

​ var foo = "method(" + argument1 + "," + argument2 + ")";

	 	 	 The s command compounds two steps into one: it deletes the character under the cursor and then enters Insert mode. Having deleted the + sign, we then type + and leave Insert mode.

One step back and then three steps forward. It’s a strange little dance that might seem unintuitive, but we get a big win by doing it this way: we can repeat the change with the dot command; all we need to do is position our cursor on the next + symbol, and the dot command will repeat that little dance.

Make the Motion Repeatable

	 	 	 There’s another trick in this example. The f{char} command tells Vim to look ahead for the next occurrence of the specified character and then move the cursor directly to it if a match is found (see fⓘ). So when we type f+, our cursor goes straight to the next + symbol. We’ll learn more about the f{char} command in Tip 50.

		 		 		Having made our first change, we could jump to the next occurrence by repeating the f+ command, but there’s a better way. The ; command will repeat the last search that the f command performed. So instead of typing f+ four times, we can use that command once and then follow up by using the ; command three times.

All Together Now

The ; command takes us to our next target, and the . command repeats the last change, so we can complete the changes by typing ;. three times. Does that look familiar?

Instead of fighting Vim’s modal input model, we’re working with it, and look how much easier it makes this particular task.

Tip 4 Act, Repeat, Reverse

	 	 	 When facing a repetitive task, we can achieve an optimal editing strategy by making both the motion and the change repeatable. Vim has a knack for this. It remembers our actions and keeps the most common ones within close reach so that we can easily replay them. In this tip, we’ll introduce each of the actions that Vim can repeat and learn how to reverse them.

* * *

Table 1. Repeatable Actions and How to Reverse Them

IntentActRepeatReverse

Make a change

{edit}

.

u

Scan line for next character

f{char}/t{char}

;

,

Scan line for previous character

F{char}/T{char}

;

,

Scan document for next match

/pattern<CR>

n

N

Scan document for previous match

?pattern<CR>

n

N

Perform substitution

:s/target/replacement

&

u

Execute a sequence of changes

qx{changes}q

@x

u

* * *

	 	 	 	 We’ve seen that the dot command repeats the last change. Since lots of operations count as a change, the dot command proves to be versatile. But some commands can be repeated by other means. For example, @: can be used to repeat any Ex command (as discussed in Tip 31). Or we can repeat the last :substitute command (which itself happens to be an Ex command as well) by pressing & (see Tip 93).

If we know how to repeat our actions without having to spell them out every single time, then we can be more efficient. First we act; then we repeat.

But when so much can be achieved with so few keystrokes, we have to watch our step. It’s easy to get trigger-happy. Rapping out j.j.j. again and again feels a bit like doing a drum roll. What happens if we accidentally hit the j key twice in a row? Or worse, the . key?

	 	 Whenever Vim makes it easy to repeat an action or a motion, it always provides some way of backing out in case we accidentally go too far. In the case of the dot command, we can always hit the u key to undo the last change. If we hit the ; key too many times after using the f{char} command, we’ll miss our mark. But we can back up again by pressing the , key, which repeats the last f{char} search in the reverse direction (see Tip 50).

	 	 It always helps to know where the reverse gear is in case you accidentally go a step too far. Table 1, ​Repeatable Actions and How to Reverse Them​, summarizes Vim’s repeatable commands along with their corresponding reverse action. In most cases, the undo command is the one that we reach for. No wonder the u key on my keyboard is so worn out!

Tip 5 Find and Replace by Hand

	 	 	 Vim has a :substitute command for find-and-replace tasks, but with this alternative technique, we’ll change the first occurrence by hand and then find and replace every other match one by one. The dot command will save us from labor, but we’ll meet another nifty one-key command that makes jumping between matches a snap.

In this excerpt, the word「content」appears on every line:

the_vim_way/1_copy_content.txt

​ ...We're waiting for content before the site can go live...

​ ...If you are content with this, let's go ahead with it...

​ ...We'll launch as soon as we have the content...

Suppose that we want to use the word「copy」(as in「copywriting」) instead of「content.」Easy enough, you might think; we can just use the substitute command, like this:

​=> ​:%s/content/copy/g​

But wait a minute! If we run this command, then we’re going to create the phrase「If you are ‘copy’ with this,」which is nonsense!

We’ve run into this problem because the word「content」has two meanings. One is synonymous with「copy」(and pronounced content), the other with「happy」(pronounced content). Technically, we’re dealing with heteronyms (words that are spelled the same but differ in both meaning and pronunciation), but that doesn’t really matter. The point is, we have to watch our step.

We can’t just blindly replace every occurrence of「content」with「copy.」We have to eyeball each one and answer「yay」or「nay」to the question, should this occurrence be changed? The substitute command is up to the task, and we’ll find out how in Tip 90. But right now, we’ll explore an alternative solution that fits with the theme of this chapter.

Be Lazy: Search Without Typing

		You might have guessed by now that the dot command is my favorite single-key Vim trigger. In second place is the * command. This executes a search for the word under the cursor at that moment (see *ⓘ).

We could search for the word「content」by pulling up the search prompt and spelling out the word in full:

​=> ​/content​

Or we could simply place our cursor on the word and hit the * key. Consider the following workflow:

KeystrokesBuffer Contents

{start}

​ ...We're waiting for content before the site can go live...

​ ...If you are content with this, let's go ahead with it...

​ ...We'll launch as soon as we have the content...

*

​ ...We're waiting for content before the site can go live...

​ ...If you are content with this, let's go ahead with it...

​ ...We'll launch as soon as we have the content...

cwcopy<Esc>

​ ...We're waiting for content before the site can go live...

​ ...If you are content with this, let's go ahead with it...

​ ...We'll launch as soon as we have the copy...

n

​ ...We're waiting for content before the site can go live...

​ ...If you are content with this, let's go ahead with it...

​ ...We'll launch as soon as we have the copy...

.

​ ...We're waiting for copy before the site can go live...

​ ...If you are content with this, let's go ahead with it...

​ ...We'll launch as soon as we have the copy...

We begin with our cursor positioned on the word「content」and then use the * command to search for it. Try it for yourself. Two things should happen: the cursor will jump forward to the next match, and all occurrences will be highlighted. If you don’t see any highlighting, try running :set hls and then refer to Tip 81, for more details.

Having executed a search for the word「content,」we can now advance to the next occurrence just by hitting the n key. In this case, pressing *nn would cycle through all matches, taking us back to where we started.

Make the Change Repeatable

		 		 		 		 		 		With our cursor positioned at the start of the word「content,」we are poised to change it. This involves two steps: deleting the word「content」and then typing its replacement. The cw command deletes to the end of the word and then drops us into Insert mode, where we can spell out the word「copy.」Vim records our keystrokes until we leave Insert mode, so the full sequence cwcopy<Esc> is considered to be a single change. Pressing the . command deletes to the end of the current word and changes it to「copy.」

All Together Now

We’re all set! Each time we press the n key, our cursor advances to the next occurrence of the word「content.」And when we press the . key, it changes the word under the cursor to「copy.」

If we wanted to replace all occurrences, we could blindly hammer out n.n.n. as many times as it took to complete all the changes (although in that case, we might as well have used the :%s/content/copy/g command). But we need to watch out for false matches. So after pressing n, we can examine the current match and decide if it should be changed to「copy.」If so, we trigger the . command. If not, we don’t. Whatever our decision, we can then move on to the next occurrence by pressing n again. Rinse and repeat until done.

Tip 6 Meet the Dot Formula

	 	 We’ve considered three simple editing tasks so far. Even though each problem was different, we found a solution using the dot command for each one. In this tip, we’ll compare each solution and identify a common pattern—an optimal editing strategy that I call the Dot Formula.

Reviewing Three Dot-Command Editing Tasks

In Tip 2, we wanted to append a semicolon at the end of a sequence of lines. We changed the first line by invoking A;<Esc>, which set us up so that we could use the dot command to repeat the change on each subsequent line. We could move between lines using the j command, and the remaining changes could be completed simply by pressing j. as many times as necessary.

In Tip 3, we wanted to pad each occurrence of the + symbol with a space both in front and behind. We used the f+ command to jump to our target and then the s command to substitute one character with three. That set us up so that we could complete the task by pressing ;. a few times.

In Tip 5, we wanted to substitute every occurrence of the word「content」with the word「copy.」We used the * command to initiate a search for the target word and then ran the cw command to change the first occurrence. This set us up so that the n key would take us to the next match and the . key would apply the same change. We could complete the task simply by pressing n. as many times as it took.

The Ideal: One Keystroke to Move, One Keystroke to Execute

In all of these examples, using the dot command repeats the last change. But that’s not the only thing they share. A single keystroke is all that’s required to move the cursor to its next target.

We’re using one keystroke to move and one keystroke to execute. It can’t really get any better than that, can it? It’s an ideal solution. We’ll see this editing strategy coming up again and again, so for the sake of convenience, we’ll refer to this pattern as the Dot Formula.

Copyright © 2016, The Pragmatic Bookshelf.
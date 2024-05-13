Vim offers more than one way to repeat changes. We’ve already learned about the dot command, which is useful for repeating small changes. But when we want to repeat anything more substantial, we should reach for Vim’s macros. Using these, we can record any number of keystrokes into a register and then play them back.

Macros are ideal for repeating changes over a set of similar lines, paragraphs, or even files. We’ll discover that there are two ways of executing a macro across a set of targets—playing it back in series or running it multiple times in parallel—and we’ll learn when to use each one.

When recording a sequence of commands, there’s always the chance that we’ll make a mistake. But we needn’t discard a bad take. We can easily append commands to the end of an existing macro. For more extensive amendments, we can even paste the macro into a document, edit the sequence of commands in place, and then yank it back into a register.

Sometimes we need to insert consecutive numbers into our text. In Tip 67, we’ll learn how to do that with a method that uses rudimentary Vim script in combination with the expression register.

Like the game of Othello, Vim’s macros take a minute to learn and a lifetime to master. But everyone—from beginners to experts—can get a lot of value from this feature that makes it easy to automate tasks. Let’s see how.

Tip 65 Record and Execute a Macro

	 	 	 Macros allow us to record a sequence of changes and then play them back. This tip shows how.

Many repetitive tasks involve making multiple changes. If we want to automate these, we can record a macro and then execute it.

Capture a Sequence of Commands by Recording a Macro

	 The q key functions both as the「record」button and the「stop」button. To begin recording our keystrokes, we type q{register}, giving the address of the register where we want to save the macro. We can tell that we’ve done it right if the word「recording」appears in the status line. Every command that we execute will be captured, right up until we press q again to stop recording.

Let’s see this in action:

KeystrokesBuffer Contents

qa

​ foo = 1

​ bar = 'a'

​ foobar = foo + bar

A;<Esc>

​ foo = 1;

​ bar = 'a'

​ foobar = foo + bar

Ivar<Esc>

​ var foo = 1;

​ bar = 'a'

​ foobar = foo + bar

q

​ var foo = 1;

​ bar = 'a'

​ foobar = foo + bar

Pressing qa begins recording and saves our macro into register a. We then perform two changes on the first line: appending a semicolon and prepending the word var. Having completed both of those changes, we press q to stop recording our macro (qⓘ).

	 We can inspect the contents of register a by typing the following:

​=> ​:reg a​

​<= --- Registers ---

​ "a A;^[Ivar ^[

It doesn’t make for easy reading, but the same sequence of commands that we recorded moments ago should be recognizable. The only surprise might be that the symbol ^[ is used to stand for the Escape key. See ​Keyboard Codes in Macros​, for an explanation.

Play Back a Sequence of Commands by Executing a Macro

	 The @{register} command executes the contents of the specified register (see @ⓘ). We can also use @@, which repeats the macro that was invoked most recently.

Here’s an example:

KeystrokesBuffer Contents

{start}

​ var foo = 1;

​ bar = 'a'

​ foobar = foo + bar

j

​ var foo = 1;

​ bar = 'a'

​ foobar = foo + bar

@a

​ var foo = 1;

​ var bar = 'a';

​ foobar = foo + bar

j@@

​ var foo = 1;

​ var bar = 'a';

​ var foobar = foo + bar;

We’ve executed the macro that we just recorded, repeating the same two changes for each of the subsequent lines. Note that we use @a on the first line and then @@ to replay the same macro on the next line.

In this example, we played the macro back by running j@a (and subsequently j@@). Superficially, this has some resemblance to the Dot Formula. It involves one keystroke to move (j) and two to act (@a). Not bad, but there’s room for improvement.

We have a couple of techniques at our disposal for executing a macro multiple times. The setup differs slightly for each technique, but more importantly, they react differently on encountering an error. I’ll explain the differences by way of a comparison with Christmas tree lights.

If you buy a cheap set of party lights, the chances are that they will be wired in series. If one bulb blows, they all go out. If you buy a premium set, they’re more likely to be wired in parallel. That means any bulb can go out, and the rest will be unaffected.

I’ve borrowed the expressions in series and in parallel from the field of electronics to differentiate between two techniques for executing a macro multiple times. The technique for executing a macro in series is brittle. Like cheap Christmas tree lights, it breaks easily. The technique for executing a macro in parallel is more fault tolerant.

Execute the Macro in Series

	 Picture a robotic arm and a conveyor belt containing a series of items for the robot to manipulate.

Recording a macro is like programming the robot to do a single unit of work. As a final step, we instruct the robot to move the conveyor belt and bring the next item within reach. In this manner, we can have a single robot carry out a series of repetitive tasks on similar items.

One consequence of this approach is that if the robot encounters any surprises, it sounds an alarm and aborts the operation. Even if items on the conveyor belt still need to be manipulated, the work stops.

Execute the Macro in Parallel

		 When we execute the macro in parallel, it’s as though we’ve dispensed with the conveyor belt entirely. Instead, we deploy an assemblage of robots,[19] all programmed to do the same simple task. Each is given a single job to do. If it succeeds, very well. If it fails, no matter.

Under the hood, Vim always executes macros sequentially, no matter which of these two techniques we use. The term in parallel is intended to draw an analogy with the robustness of parallel circuits. It is not meant to suggest that Vim executes multiple changes concurrently.

In Tip 68, as well as Tip 70, we’ll see examples of a macro being executed both in series and in parallel.

Tip 66 Normalize, Strike, Abort

	 	 Executing a macro can sometimes produce unexpected results, but we can achieve better consistency if we follow a handful of best practices.

When we execute a macro, Vim blindly repeats the sequence of canned keystrokes. If we aren’t careful, the outcome when we replay a macro might diverge from our expectations. But it’s possible to compose macros that are more flexible, adapting to do the right thing in each context.

The golden rule is this: when recording a macro, ensure that every command is repeatable.

Normalize the Cursor Position

	 As soon as you start recording a macro, ask yourself these questions: where am I, where have I come from, and where am I going? Before you do anything, make sure your cursor is positioned so that the next command does what you expect, where you expect it.

That might mean moving the cursor to the next search match (n) or the start of the current line (0) or perhaps the first line of the current file (gg). Always starting on square one makes it easier to strike the right target every time.

Strike Your Target with a Repeatable Motion

	 Vim has many motion commands for getting around a text file. Use them well.

Don’t just hammer the l key until your cursor reaches its target. Remember, Vim executes your keystrokes blindly. Moving your cursor ten characters to the right might get you where you need to go as you record the macro, but what about when you play it back later? In another context, moving the cursor ten places to the right might overshoot the mark or stop short of it.

Word-wise motions, such as w, b, e, and ge tend to be more flexible than character-wise h and l motions. If we recorded the motion 0 followed by e, we could expect consistent results each time we executed the macro. The cursor would end up on the last character of the first word of the current line. It wouldn’t matter how many characters that word contained, so long as the line contained at least one word.

	 Navigate by search. Use text objects. Exploit the full arsenal of Vim’s motions to make your macros as flexible and repeatable as you can. Don’t forget: when recording a macro, using the mouse is verboten!

Abort When a Motion Fails

	 	 	 	 	 	 Vim’s motions can fail. For example, if our cursor is positioned on the first line of a file, the k command does nothing. The same goes for j when our cursor is on the last line of a file. By default, Vim beeps at us when a motion fails, although we can mute it with the ‘visualbell’ setting (see 'visualbell'ⓘ).

If a motion fails while a macro is executing, then Vim aborts the rest of the macro. Consider this a feature, not a bug. We can use motions as a simple test of whether or not the macro should be executed in the current context.

Consider this example: We start by searching for a pattern. Let’s say that the document has ten matches. We start recording a macro using the n command to repeat the last search. With our cursor positioned on a match, we make some small change to the text and stop recording the macro. The result of our edit is that this particular region of text no longer matches our search pattern. Now the document has only nine matches.

When we execute this macro, it jumps to the next match and makes the same change. Now the document has only eight matches. We execute the macro again and again, until eventually no matches remain. If we attempt to execute the macro now, the n command will fail because there are no more matches. The macro aborts.

Suppose that the macro was stored in the a register. Rather than executing @a ten times, we could prefix it with a count: 10@a. The beauty of this technique is that we can be unscrupulous about how many times we execute this macro. Don’t care for counting? It doesn’t matter! We could execute 100@a or even 1000@a, and it would produce the same result.

Tip 67 Play Back with a Count

	 	 	 	 The Dot Formula can be an efficient editing strategy for a small number of repeats, but it can’t be executed with a count. Overcome this limitation by recording a cheap one-off macro and playing it back with a count.

In Tip 3, we used the Dot Formula to transform this:

the_vim_way/3_concat.js

​ ​var​ foo = ​"method("​+argument1+​","​+argument2+​")"​;

What we want is for it to look like this:

​ ​var​ foo = ​"method("​ + argument1 + ​","​ + argument2 + ​")"​;

The Dot Formula meant that we could complete the task simply by repeating ;. a few times. What if we faced the same problem but on a larger scale?

​ x = ​"("​+a+​","​+b+​","​+c+​","​+d+​","​+e+​")"​;

We can approach this in exactly the same way. But when we have to invoke the two commands ;. so many times to complete the job, it starts to feel like a lot of work. Isn’t there some way that we could apply a count?

It’s tempting to think that running 11;. would do the trick, but it’s no use. This instructs Vim to run the ; command eleven times, and then the . command once. The equivalent mistake is more obvious if we run ;11., which tells Vim to invoke ; once and then . eleven times. We really want to run ;. eleven times.

We can simulate this by recording one of the simplest possible macros: qq;.q. Here, qq tells Vim to record the following keystrokes and save them to the q register. Then we type our commands ;. and finish recording the macro by pressing q one final time. Now we can execute the macro with a count: 11@q. This executes ;. eleven times.

Let’s put all of that together.

Keystrokes

Buffer Contents

{start}

​ x = "("+a+","+b+","+c+","+d+","+e+")";

f+

​ x = "("+a+","+b+","+c+","+d+","+e+")";

s + <Esc>

​ x = "(" + a+","+b+","+c+","+d+","+e+")";

qq;.q

​ x = "(" + a + ","+b+","+c+","+d+","+e+")";

22@q

​ x = "(" + a + "," + b + "," + c + "," + d + "," + e + ")";

The ; command repeats the f+ search. When our cursor is positioned after the last + character on the line, the ; motion fails and the macro aborts.

In our case, we want to execute the macro ten times. But if we were to play it back eleven times, the final execution would abort. In other words, we can complete the task so long as we invoke the macro with a count of ten or more.

Who wants to sit there and count the exact number of times that a macro should be executed? Not me. I’d rather give a count that I think is high enough to get the job done. I often use 22, because I’m lazy and it’s easy to type. On my keyboard, the @ and 2 characters are entered with the same button.

Note that it won’t always be possible to make approximations when providing a count to a macro. It works in this case because the macro has a built-in safety catch: the ; motion will fail if no more + symbols are left on the current line. See ​Abort When a Motion Fails​, for more details.

Tip 68 Repeat a Change on Contiguous Lines

	 	 We can make light work out of repeating the same set of changes on a range of lines by recording a macro and then playing it back on each line. There are two ways to do this: executing the macro in series or in parallel.

As a demonstration, we’ll transform this snippet of text:

macros/consecutive-lines.txt

​ 1. one

​ 2. two

​ 3. three

​ 4. four

We’ll make it look like this:

​ 1) One

​ 2) Two

​ 3) Three

​ 4) Four

The task may look trivial, but it presents a couple of interesting challenges.

Record One Unit of Work

To begin, we record all changes made to the first line:

KeystrokesBuffer Contents

qa

​ 1. one

​ 2. two

0f.

​ 1. one

​ 2. two

r)

​ 1) one

​ 2. two

w~

​ 1) One

​ 2. two

j

​ 1) One

​ 2. two

q

​ 1) One

​ 2. two

Note the use of motions in this macro. We begin with the 0 command, which normalizes our cursor position by placing it at the start of the line. This means that our next motion always starts from the same place, making it more repeatable.

Some might look at the next motion, f., and consider it wasteful. It moves the cursor only one step to the right, same as the l command. Why use two keystrokes when one would do?

Once again, it’s a matter of repeatability. In our sample set, we have lines numbered only one to four, but suppose the numbers ran into double digits?

​ 1. one

​ 2. two

​ ...

​ 10. ten

​ 11. eleven

On the first nine lines, 0l takes us to the second character of the line, which happens to be a period. But from line ten onward, that motion stops short of the target, whereas f. works on all of these lines and would continue to work into triple digits and beyond.

Using the f. motion also adds a safety catch. If no . characters are found on the current line, the f. command raises an error and macro execution aborts. We’ll exploit this later, so keep that thought at the back of your mind.

Execute Macro in Series

	 We can execute the macro we just recorded by pressing @a. This carries out the following steps: jump to the first . character on the line, change it to ), uppercase the first letter of the next word, and finish by advancing to the next line.

We could invoke the @a command three times to complete the task, but running 3@a is quicker:

KeystrokesBuffer Contents

{start}

​ 1) One

​ 2. two

​ 3. three

​ 4. four

3@a

​ 1) One

​ 2) Two

​ 3) Three

​ 4) Four

Let’s introduce a new obstacle. Suppose our file contains comments.

macros/broken-lines.txt

​ 1. one

​ 2. two

​ // break up the monotony

​ 3. three

​ 4. four

Now watch what happens if we attempt to replay the same macro on this file.

KeystrokesBuffer Contents

{start}

​ 1. one

​ 2. two

​ // break up the monotony

​ 3. three

​ 4. four

5@a

​ 1) One

​ 2) Two

​ // break up the monotony

​ 3. three

​ 4. four

The macro stalls on line three—the one containing the comment. When the f. command is executed, it finds no . characters and the macro aborts. We’ve tripped the safety catch, and it’s a good thing too. If the macro had successfully executed on this line, then it would have made changes that were probably unwanted.

But we are left with a problem. We asked Vim to execute the macro five times, and it bailed out on the third repetition. So we have to invoke it again on the next lines to complete the job. Let’s look at an alternative technique.

Execute Macro in Parallel

	 	 Tip 30, demonstrated a method for running the dot command on a series of consecutive lines. We can apply the same technique here:

KeystrokesBuffer Contents

qa

​ 1. one

0f.r)w~

​ 1) One

q

​ 1) One

jVG

​ 1) One

​ 2. two

​ // break up the monotony

​ 3. three

​ 4. four

:’<,’>normal @a

​ 1) One

​ 2) Two

​ // break up the monotony

​ 3) Three

​ 4) Four

We’ve re-recorded the macro from scratch. This one is almost identical, except that we’ve omitted the final j command to advance to the next line. We won’t be needing it this time.

The :normal @a command tells Vim to execute the macro once for each line in the selection. Just as before, the macro succeeds on the first two lines and then aborts on line three, but it doesn’t stall there this time—it completes the job. Why?

Previously, we queued up five repetitions in series by running 5@a. When the third iteration aborted, it killed the remaining items in the queue. This time, we’ve lined up five iterations in parallel. Each invocation of the macro is independent from the others. So when the third iteration fails, it does so in isolation.

Deciding: Series or Parallel

			 Which is better, series or parallel? The answer (as always): it depends.

Executing a macro on multiple items in parallel is more robust. In this scenario, it’s the better solution. But if we raise an error when we execute a macro, maybe we want those alarms to go off. Executing a macro on multiple items in series makes it clear when and where any errors occur.

Learn both techniques, and you’ll develop a knack for knowing which one is right for the occasion.

Tip 69 Append Commands to a Macro

	 	 	 	 Sometimes we miss a vital step when we record a macro. There’s no need to re-record the whole thing from scratch. Instead, we can tack extra commands onto the end of an existing macro.

Suppose that we record this macro (borrowed from Tip 68):

KeystrokesBuffer contents

qa

​ 1. one

​ 2. two

0f.r)w~

​ 1) One

​ 2. two

q

​ 1) One

​ 2. two

Immediately after pressing q to stop recording, we realize that we should have finished by pressing j to advance to the next line.

Before we fix it, let’s inspect the contents of register a:

​=> ​:reg a​

​<= "a 0f.r)w~

	 	 	 	If we type qa, then Vim will record our keystrokes, saving them into register a by overwriting the existing contents of that register. If we type qA, then Vim will append our keystrokes to the existing contents of register a.

KeystrokesBuffer Contents

qA

​ 1) One

​ 2. two

j

​ 1) One

​ 2. two

q

​ 1) One

​ 2. two

Let’s see what’s in the a register now:

​=> ​:reg a​

​<= "a 0f.r)w~j

All of the commands that we recorded the first time around are still there, but now it ends with j.

Discussion

This little trick saves us from having to re-record the entire macro from scratch. But we can use it only to tack commands on at the end of a macro. If we wanted to add something at the beginning or somewhere in the middle of a macro, this technique would be of no use to us. In Tip 72, we’ll learn about a more powerful method for amending a macro after it has been recorded.

Tip 70 Act Upon a Collection of Files

	 	 	 So far, we’ve stuck to tasks that were repeated in the same file, but we can play back a macro across a collection of files. Once again, we’ll consider how to execute the macro in parallel and in series.

Let’s start with a set of files that look something like this:

macros/ruby_module/animal.rb

​ ​# ...[end of copyright notice]​

​ ​class​ Animal

​ ​# implementation​

​ ​end​

We’ll wrap the class in a module to end up with this:

​ ​# ...[end of copyright notice]​

​ ​module​ Rank

​ ​class​ Animal

​ ​# implementation...​

​ ​end​

​ ​end​

Preparation

Source these lines of configuration to reproduce the examples in this tip:

macros/rc.vim

​ ​set​ nocompatible

​ ​filetype​ plugin indent ​on​

​ ​set​ hidden

​ ​if​ has(​"autocmd"​)

​ autocmd FileType ​ruby​ ​setlocal​ ​ts​=2 ​sts​=2 ​sw​=2 expandtab

​ ​endif​

The ‘hidden’ option is discussed in more depth in ​Enable the ‘hidden’ Setting Before Running ‘:*do’ Commands​.

If you’d like to follow along, consult ​Downloading the Examples​. The folder code/macros/ruby_module contains the files we’ll be working with.

Build a List of Target Files

	 Let’s stake out the terrain by building a list of the files that we want to act upon. We’ll keep track of them using the argument list (for more details, see Tip 38):

​=> ​:cd code/macros/ruby_module​

​=> ​:args *.rb​

Running :args without arguments reveals the contents of the list:

​=> ​:args​

​<= [animal.rb] banker.rb frog.rb person.rb

We can navigate through this list of files using :first, :last, :prev, and :next.

Record a Unit of Work

Before we begin, let’s make sure we’re at the start of the arguments list:

​=> ​:first​

Now let’s record a macro that performs the necessary work:

KeystrokesBuffer Contents

qa

​ # ...[end of copyright notice]

​ class Animal

​ # implementation...

​ end

gg/class<CR>

​ # ...[end of copyright notice]

​ class Animal

​ # implementation...

​ end

Omodule Rank<Esc>

​ # ...[end of copyright notice]

​ module Rank

​ class Animal

​ # implementation...

​ end

j>G

​ # ...[end of copyright notice]

​ module Rank

​ class Animal

​ # implementation...

​ end

Goend<Esc>

​ # ...[end of copyright notice]

​ module Rank

​ class Animal

​ # implementation...

​ end

​ end

q

​ # ...[end of copyright notice]

​ module Rank

​ class Animal

​ # implementation...

​ end

​ end

	 Each of these files begins with a copyright notice, so we have to take care to properly normalize the cursor position. Pressing gg places the cursor at the start of the file, and /class<CR> jumps forwards to the first occurrence of the word「class.」Having made these preparatory steps, we can now proceed to make the changes.

We use the O command to open a new line above the cursor, inserting the new text. Then we advance our cursor to the next line, where we use the >G command to indent each line up to the end of the file. Finally, we jump to the end of the file by pressing G and then using the o command to create a new line below the cursor, inserting the end keyword there.

If you’re following along with your editor, try to resist the urge to save your changes to the file by running :w. We’ll see why in a moment.

Execute the Macro in Parallel

	 	 The :argdo command allows us to execute an Ex command once for each buffer in the argument list (see :argdoⓘ). But if we were to run :argdo normal @a right now, there would be side effects.

Think about it. Running :argdo normal @a executes the macro that we just recorded in all of the buffers in the argument list, including the first one: the one that we changed as we recorded the macro. As a result, the first buffer gets wrapped in a module twice over.

To prevent this, we’ll revert all of the changes we just made to the first buffer in the argument list by running :edit! (see :edit!ⓘ):

​=> ​:edit!​

If you had already written the changes to a file, then :edit! won’t work. In this case, you could just use the u command repeatedly until the file looked as it did when you opened it.

Now we can go ahead and execute the macro in all of the buffers in the argument list:

​=> ​:argdo normal @a​

This technique takes a bit of setup, but that one command does a lot of work for us. Now let’s see how we could adapt this macro to run in series.

Execute the Macro in Series

	 Our macro performs a single unit of work on a single buffer. If we want to make it act upon multiple buffers, we could append a final step that advances to the next buffer in the list. (See Table 12, ​Executing the Macro in Series​.)

* * *

Table 12. Executing the Macro in Series

KeystrokesBuffer Contents

qA

​ module Rank

​ class Animal

​ # implementation...

​ end

​ end

:next

​ class Banker

​ # implementation...

​ end

q

​ class Banker

​ # implementation...

​ end

22@a

​ module Rank

​ class Person

​ # implementation...

​ end

​ end

* * *

While we could run 3@a to execute the macro on each of the remaining files in the buffer list, there’s no need to be so precise about it. When we reach the last buffer in the argument list, the :next command fails and the macro aborts. So, rather than specifying an exact count, we only have to ensure that we provide a number that’s large enough: 22 will do, and it’s easy to type.

Save Changes to All Files

	 	 	 We’ve changed four files, but we haven’t saved any of them yet. We could run :argdo write to save all files in the argument list, but it would be quicker simply to run this:

​=> ​:wall​

Note that this saves all files in the buffer list, so it’s not exactly equivalent to :argdo write (see :waⓘ).

	 Another useful command is :wnext (see :wnⓘ), which is equivalent to running :write followed by :next. If you are executing a macro in series across several files in the argument list, you may prefer to use this.

Discussion

Suppose that something caused the macro to fail while executing on the third buffer in the argument list. If we were using the :argdo normal @a command, then the macro would fail only in that one buffer, whereas if we executed the macro in series by using a count, then it would abort, and any items that follow in the argument list would be left unchanged.

We’ve already seen this effect in Tip 68. But the consequences are slightly different this time. When we performed the same task on a block of adjacent lines, we could see everything at a glance. If anything went wrong, it was there right in front of our eyes.

This time we’re working on a set of files, so we can’t see everything in a single glance. If we execute the macro in series and it fails, then it will halt at the place where the error occurs, whereas if we execute the macro in parallel and it fails, we’ll have to browse through the argument list until we find the buffer where the error was raised.

In the case where an error is raised, running the macro in parallel may complete the job faster, but it conceals useful information.

Tip 71 Evaluate an Iterator to Number Items in a List

	 	 	 	 	 Being able to insert a value that changes for each execution of a macro can be useful. In this tip, we’ll learn a technique for incrementing a number as we record a macro so that we can insert the numbers 1 to 5 on consecutive lines.

Suppose that we want to create a numbered list from a series of items on adjacent lines. To demonstrate, we’ll start with this text:

macros/incremental.txt

​ partridge in a pear tree

​ turtle doves

​ French hens

​ calling birds

​ golden rings

We’ll transform it to look like this:

​ 1) partridge in a pear tree

​ 2) turtle doves

​ 3) French hens

​ 4) calling birds

​ 5) golden rings

We’ve already learned a couple of ways to make Vim perform simple arithmetic. We can either use the <C-a> and <C-x> commands with a count (see Tip 10), or we can use the expression register (see Tip 16). For this solution, we’ll use the expression register with a touch of Vim script.

Rudimentary Vim Script

	 	 	 Let’s begin by stepping through a few simple command-line invocations. Using the let keyword, we can create a variable called i and assign it a value of 0. The :echo command allows us to inspect the current value assigned to a variable.

​=> ​:let i=0​

​=> ​:echo i​

​<= 0

We can increment the value of i:

​=> ​:let i += 1​

​=> ​:echo i​

​<= 1

The :echo command is fine for revealing the value that is assigned to a variable, but ideally we want to insert that value into the document. We can do that using the expression register. In Tip 16, we saw that the expression register can be used to do simple sums and to insert the result into the document. We can insert the value stored in variable i just by running <C-r>=i<CR> in Insert mode.

Record the Macro

	 Now let’s put all of this together:

KeystrokesBuffer Contents

:let i=1

​ partridge in a pear tree

qa

​ partridge in a pear tree

I<C-r>=i<CR>) <Esc>

​ 1) partridge in a pear tree

:let i += 1

​ 1) partridge in a pear tree

q

​ 1) partridge in a pear tree

	 	 Before we begin recording the macro, we set the variable i to 1. Inside the macro, we use the expression register to insert the value stored in i. Then, before we finish recording the macro, we increment the value stored in the variable, which should now contain the value 2.

Execute the Macro

We can then play it back for the remaining lines.

KeystrokesBuffer Contents

{start}

​ 1) partridge in a pear tree

​ turtle doves

​ French hens

​ calling birds

​ golden rings

jVG

​ 1) partridge in a pear tree

​ turtle doves

​ French hens

​ calling birds

​ golden rings

:’<,’>normal @a

​ 1) partridge in a pear tree

​ 2) turtle doves

​ 3) French hens

​ 4) calling birds

​ 5) golden rings

The :normal @a command tells Vim to execute the macro on each of the selected lines (see ​Execute Macro in Parallel​). The value of i is 2 to begin with, but it gets incremented each time the macro executes. The end result is that each line is prefixed with consecutive digits.

We could also use the yank, put, and <C-a> commands to accomplish this same task. Try it yourself for exercise!

Tip 72 Edit the Contents of a Macro

	 	 	 In Tip 69, we saw that adding commands at the end of a macro is straightforward. But what if we want to remove the last command? Or change something at the beginning of the macro? In this tip, we’ll learn how to edit the content of a macro as if it were plain text.

The Problem: Nonstandard Formatting

Suppose that we’ve just followed the steps in ​Record One Unit of Work​, saving our keystrokes into register a. Now we’re faced with this file, which is formatted slightly differently:

macros/mixed-lines.txt

​ 1. One

​ 2. Two

​ 3. three

​ 4. four

	 	 	 	 	 Some of the lines already use a capital letter. In our macro, we used the ~ command, which toggles the case of the letter under the cursor (see ~ⓘ). Instead of using ~, let’s update the macro to use the command vU, which uppercases the letter under the cursor (see v_Uⓘ).

Keyboard Codes in Macros

	 	 	 In this example, we are working with a relatively simple register. But things can get messy quickly if we attempt to edit a larger macro. For example, let’s inspect the macro that was recorded in Tip 70:

​=> ​:reg a​

​<= --- Registers ---

​ "a Omoul<80>kb<80>kbdule Rank^[j>GGoend^[

	 Notice anything strange? First of all, the ^[ symbol appears a couple of times. No matter whether you press <Esc> or <C-[>, that’s how Vim represents the Escape key.

	 Stranger still is the <80>kb symbol, which represents the backspace key. Study the keystrokes. When I recorded this macro, I started off by typing「moul.」Upon seeing my mistake, I hit the backspace key a couple of times and then typed out「dule,」the rest of the word.

This action is of no practical consequence. If I replay those keystrokes, Vim will reproduce my mistake followed by my correction. The net result will be correct. But it does make the register harder to read and more fiddly to edit.

Paste the Macro into a Document

	 	 	 The registers that we use for recording macros are the very same with which the yank and put operations interact. So if we want to make changes to the macro saved in register a, we simply have to paste it into the document, where we can edit it as plain text.

	 Let’s press G and jump to the end of the current document. We want to paste the contents of register a into a new line. The simplest way of doing that is with the :put command:

​=> ​:put a​

Why didn’t we just use the "ap command? In this context, the p command would paste the contents of the a register after the cursor position on the current line. The :put command, on the other hand, always pastes below the current line, whether the specified register contains a line-wise or a character-wise set of text.

Edit the Text

	 Now we can edit the macro as plain text. The sequence of commands shown in Table 13, ​Editing the Macro as Plain Text​ replaces the ~ character with vU.

* * *

Table 13. Editing the Macro as Plain Text

KeystrokesBuffer Contents

{start}

​ 0f.r)w~j

f~

​ 0f.r)w~j

svU<Esc>

​ 0f.r)wvUj

* * *

Yank the Macro from the Document Back into a Register

	 We’ve got the sequence of commands looking just the way we want it to, so we can yank it from the document back into a register. The simplest way is to run "add (or :d a), but this could cause us problems later. The dd command performs a line-wise deletion. The register contains a trailing ^J character:

​=> ​:reg a​

​<= 0f.r)wvUj^J

This character represents a newline, which in most circumstances won’t matter. But sometimes this trailing newline could change the meaning of the macro. As a precaution, using a character-wise yank to get the characters from the document back into the register is a safer bet:

KeystrokesBuffer Contents

{start}

​ // last line of the file proper

​ 0f.r)wvUj

0

​ // last line of the file proper

​ 0f.r)wvUj

"ay$

​ // last line of the file proper

​ 0f.r)wvUj

dd

​ // last line of the file proper

When we run the command 0 followed by "ay$, we yank every character on that line except for the carriage return. Having captured everything that we want to keep into register a, we can then run dd to delete the line. This will end up in the default register, but we won’t use it.

Having followed these steps, register a now contains a new and improved macro. We can use it on the example text that we met at the start of this tip.

Discussion

Being able to paste a macro into the document, edit it right there, and then yank it back into a register and execute it is very handy. But the register can be fussy to work with for the reasons noted in ​Keyboard Codes in Macros​. If you only have to append a command at the end of your macro, following the procedure outlined in Tip 69, is simpler.

	 Since Vim’s registers are no more than containers for strings of text, we can also manipulate them programmatically using Vim script. For example, we could use the substitute() function (which is not the same as the :substitute command! See substitute()ⓘ) to perform the same edit as before:

​=> ​:let @a=substitute(@a, '\~', 'vU', 'g')​

If you’re curious about this approach, look up function-listⓘ for more ideas.

Footnotes

[19]

http://all-sorts.org/of/robots

Copyright © 2016, The Pragmatic Bookshelf.

Part 5

Patterns

	 This part of the book is devoted to patterns, which are integral to some of Vim’s most powerful commands. We’ll look at some tricks that make it easier to compose regular expressions and to search for text verbatim. We’ll study the mechanics of the search command itself and then explore two powerful Ex commands: :substitute, which allows us to find occurrences of one pattern and replace them with something else, and :global, which lets us run any Ex command on each line that matches a particular pattern.

Chapter 12

Matching Patterns and Literals


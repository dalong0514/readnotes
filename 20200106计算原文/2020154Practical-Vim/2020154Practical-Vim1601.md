You might think that the substitute command is just for simple find and replace operations, but in fact, it’s one of the most powerful Ex commands available. By the time we’ve reached the end of this chapter, we’ll have learned all the many roles that the substitute command can play, from simple to very complex.

We’ll look at a few tips and tricks that allow us to compose substitution commands more quickly by reusing the last search pattern. We’ll also look at a special case, where Vim allows us to eyeball every occurrence before confirming the substitution. We’ll learn how we can fill out the replacement field without typing, and we’ll examine some of the special behaviors that are available through the replacement field. We’ll also learn how to repeat the last substitute command over a different range without having to retype the whole command.

We can execute Vim script expressions in the replacement field. We’ll study an advanced example that exploits this to perform arithmetic on a series of numerical matches. Then we’ll learn how to swap two (or more) words with a single substitute command.

We’ll finish by looking at a couple of strategies for performing search and replace across multiple files.

Tip 88 Meet the Substitute Command

	 	 The :substitute command is complex: in addition to providing a search pattern and replacement string, we have to specify the range over which it will execute. Optionally, we can also provide flags to tweak its behavior.

The substitute command allows us to find and replace one chunk of text with another. The command’s syntax looks like this:

​ :[range]s[ubstitute]/{pattern}/{string}/[flags]

The substitute command has many parts to it. The rules for the [range] are just the same as for every other Ex command, which we covered in-depth in Tip 28. As for the {pattern}, that was covered in Chapter 12, ​Matching Patterns and Literals​.

Tweak the Substitute Command Using Flags

	 We can tweak the behavior of the substitute command using flags. The best way to understand what a flag does is to see it in action, so let’s briefly define a handful of flags that are used in other tips. (For a complete reference, look up :s_flagsⓘ.)

	 	 The g flag makes the substitute command act globally, causing it to change all matches within a line rather than just changing the first one. We’ll meet it in Tip 89.

	 	 The c flag gives us the opportunity to confirm or reject each change. We’ll see it in action in Tip 90.

	 The n flag suppresses the usual substitute behavior, causing the command to report the number of occurrences that would be affected if we ran the substitute command. Tip 86, gives an example of usage.

	 If we run the substitute command using a pattern that has no matches in the current file, Vim will report an error saying「E486: Pattern not found.」We can silence these errors by including the e flag.

	 The & flag simply tells Vim to reuse the same flags from the previous substitute command. Tip 93, shows a scenario where it comes in handy.

Special Characters for the Replacement String

	 	 In Chapter 12, ​Matching Patterns and Literals​, we saw that some characters take on special meaning when used in search patterns. The replacement field also has a handful of special characters. You can find the complete list by looking up sub-replace-specialⓘ, but some of the highlights are summarized in this table:

SymbolRepresents

\r

		 		 Insert a carriage return

\t

		 		 Insert a tab character

\\

		 		 		 Insert a single backslash

\1

Insert the first submatch

\2

Insert the second submatch (and so on, up to \9)

\0

Insert the entire matched pattern

&

Insert the entire matched pattern

~

Use {string} from the previous invocation of :substitute

\={Vim script}

Evaluate {Vim script} expression; use result as replacement {string}

The \r, \t and \\ tokens should be fairly self-explanatory. In Tip 93, we’ll see how the ~ token works, but we’ll also learn about a couple of shortcuts that make it even faster to repeat a substitute command. We’ll see \1 and \2 in use in Tip 94.

The \={Vim script} token is very powerful. It allows us to execute code and use the result as our replacement {string}. In Tip 95, and Tip 96, we’ll see a couple of examples of usage.

Tip 89 Find and Replace Every Match in a File

	 	 	 By default, the substitute command acts on the current line, changing the first occurrence only. To change every match throughout a file, we have to specify a range and use the g flag.

For demonstration purposes, we’ll use this text:

substitution/get-rolling.txt

​ When the going gets tough, the tough get going.

​ If you are going through hell, keep going.

Let’s try and replace every occurrence of the word going with rolling. First, we’ll enable the ‘hlsearch’ option so that we can see what we’re doing (see Tip 81, for more details):

​=> ​:set hlsearch​

The simplest thing that we could do with the substitute command is to provide a target {pattern} and replacement {string}:

KeystrokesBuffer Contents

:s/going/rolling

​ When the rolling gets tough, the tough get going.

​ If you are going through hell, keep going.

See what’s happened? Vim has replaced the first occurrence of「going」with「rolling,」but it’s left every other match untouched.

To understand why, it helps to think of a file as a two-dimensional board made up of characters along the x-axis and lines down the y-axis. By default, the substitute command only acts upon the first match on the current line. Let’s see what’s required to expand its scope to cover the x- and y-axes in their entirety.

To keep going on the horizontal axis we need to include the g flag. This stands for global, which is a rather misleading name. One might expect that this flag would cause the substitution to be carried out across the entire file, but in fact, it just means「globally within the current line.」This makes more sense if you remember that Vim is a direct descendent of the line editor ed, as discussed in ​On the Etymology of Vim (and Family)​.

We’ll press u to undo the last change and then try running a variation of the substitute command. This time, we’ll tack the /g flag on at the end:

KeystrokesBuffer Contents

:s/going/rolling/g

​ When the rolling gets tough, the tough get rolling.

​ If you are going through hell, keep going.

	 This time, all occurrences of going on the current line have been changed to rolling, but that still leaves a couple of instances unchanged elsewhere in the file. So how do we tell the substitute command to act on the entire vertical axis of our file?

The answer is to provide a range. If we prefix a % at the start of the substitute command, it will be executed on every line of the file:

KeystrokesBuffer Contents

:%s/going/rolling/g

​ When the rolling gets tough, the tough get rolling.

​ If you are rolling through hell, keep rolling.

The substitute command is just one of many Ex commands, all of which can accept a range in the same manner. Tip 28, goes into greater depth.

To recap, if we want to find and replace all occurrences in the current file, we have to explicitly tell the substitute command to operate on the entire x- and y-axes. The g flag deals with the horizontal axis, while the % address deals with the vertical axis.

It’s easy enough to forget one or the other of these details. In Tip 93, we’ll look at a couple of techniques for repeating a substitute command.

Tip 90 Eyeball Each Substitution

	 	 	 Finding all occurrences of a pattern and blindly replacing them with something else won’t always work. Sometimes we need to look at each match and decide if it should be substituted. The c flag modifies the :substitute command to make this possible.

Remember this example from Tip 5?

the_vim_way/1_copy_content.txt

​ ...We're waiting for content before the site can go live...

​ ...If you are content with this, let's go ahead with it...

​ ...We'll launch as soon as we have the content...

We couldn’t use find and replace to change「content」to「copy.」Instead, we used the Dot Formula to solve our problem. However, we could also have used the c flag on the substitute command:

​=> ​:%s/content/copy/gc​

	 The c flag causes Vim to show us each match and ask「Replace with copy?」We can then say y to perform the change or n to skip it. Vim does what we ask and then moves to the next match and asks us again.

In our example, we would respond yny, changing the first and last occurrences while leaving the middle one untouched.

We aren’t limited to just two answers. In fact, Vim helpfully reminds us of our options with the prompt「y/n/a/q/l/^E/^Y.」This table shows what each answer means:

TriggerEffect

y

Substitute this match

n

Skip this match

q

Quit substituting

l

「last」—Substitute this match, then quit

a

「all」—Substitute this and any remaining matches

<C-e>

Scroll the screen up

<C-y>

Scroll the screen down

You can also find this information in Vim’s help by looking up :s_cⓘ.

Discussion

	 Unusually, most buttons on the keyboard do nothing in Vim’s Substitute-Confirmation mode. As always, the <Esc> key allows us to return to Normal mode, but apart from that, the landscape feels unfamiliar.

On the up side, this allows us to complete the task with a minimum of keystrokes. On the down side, all of the functionality that we’re used to is unavailable to us. By contrast, if we use the Dot Formula (as in Tip 5), then we’re in plain old Normal mode throughout. Everything works just as we expect it to.

Try both methods, and use whichever one you feel more comfortable with.

Tip 91 Reuse the Last Search Pattern

	 	 	 Leaving the search field of the substitute command blank instructs Vim to reuse the most recent search pattern. We can exploit this fact to streamline our workflow.

Let’s face it: to execute a substitute command, we have to do a lot of typing. First we specify the range, then we fill out the pattern and replacement fields, and finally we append any necessary flags. That’s a lot to think about, and making a mistake in any of these fields could change the outcome.

Here’s the good news: leaving the search field blank tells Vim to use the current pattern.

Take this monolithic substitute command (from Tip 85):

​=> ​:%s/\v'(([^']|'\w)+)'/「\1」/g​

It’s equivalent to these two separate commands:

​=> ​/\v'(([^']|'\w)+)'​

​=> ​:%s//「\1」/g​

So what? One way or another, we’ll still have to type out the full pattern, right? That’s not the point. The substitute command involves two steps: composing a pattern and devising a suitable replacement string. This technique allows us to decouple those two tasks.

	 When composing a nontrivial regular expression, it usually takes a few attempts to get it right. If we were to test our pattern by executing a substitute command, we would change the document each time we tried it out. That’s messy. When we execute a search command, the document is not changed, so we can make as many mistakes as we like. In Tip 85, we see an effective workflow for building regular expressions. Separating the two tasks allows for a cleaner workflow. We can measure twice and cut once.

Besides, who says we have to type out the pattern? In Tip 87, we used a smidgen of Vim script to add a Visual mode equivalent of the * command. This mapping allows us to select any text in our document and then hit the * key to search for the selection. We could then run the substitute command with an empty search field to replace our selection (and any similar matches) with something else. Talk about being lazy!

It’s Not Always Appropriate

I’m not saying that you should never fill out the search field of the substitute command. Here, for example, we have a substitute command that joins every line of a file by replacing newlines with commas:

​=> ​:%s/\n/,​

It’s such a simple command that you won’t gain anything by splitting it in two. In fact, doing so would probably add work.

Implications for Command History

	 Another point to consider is that leaving the search field blank creates an incomplete record in our command history. Patterns are saved in Vim’s search history, while substitute commands are saved in the history of Ex commands (cmdline-historyⓘ). Decoupling the search and replacement tasks causes the two pieces of information to be placed in separate silos, which could cause difficulty if you want to reuse an old substitute command later.

If you think that you’ll want to recall a substitute command in its complete form from history, you can always fill out the search field explicitly. Pressing <C-r>/ at the command line pastes the contents of the last search register in place. Typing out the following would create a complete entry in our command history:

​=> ​:%s/<C-r>//「\1」/g​

Sometimes leaving the search field of the substitute command blank is convenient. Other times it’s not. Try both ways, and you’ll develop an intuition for whether or not to use it. As always, use your judgment.

Tip 92 Replace with the Contents of a Register

	 	 	 	 We don’t have to type out the replacement string by hand. If the text already exists in the document, we can yank it into a register and use it in the replacement field. Then we can pass the contents of a register either by value or by reference.

In Tip 91, we saw that Vim makes an intelligent assumption when we leave the search field of the substitute command blank. It’s tempting to think that leaving the replacement field blank would also reuse the string from the previous substitute command, but this isn’t the case. Instead, a blank replacement field instructs the substitute command to replace each match with an empty string. In other words, it deletes each match.

Pass by Value

	 We can insert the contents of a register by typing <C-r>{register}. Suppose that we have yanked some text and want to paste it into the replacement field of the substitute command. We could do so by typing this:

​=> ​:%s//<C-r>0/g​

When we type <C-r>0, Vim pastes the contents of register 0 in place, which means we can examine it before we execute the substitute command. In many cases, this works just fine, but complications could ensue.

If the text in register 0 contains any characters that have special meaning within the replacement field (such as & or ~, for example), we would have to edit the string by hand to escape those characters. Also, if register 0 contained a multiline excerpt of text, it might not fit on the command line.

To avoid these problems, we could simply pass a reference to the register containing the text we want to use in the substitution field.

Pass by Reference

	 Suppose that we’ve yanked a multiline selection of text, and it’s stored in register 0. Now we want to use that text as the replacement field of the substitute command. We could do so by running this:

​=> ​:%s//\=@0/g​

In the replacement field, the \= item tells Vim to evaluate a Vim script expression. In Vim script, we can reference the contents of a register as @{register}. @0 returns the contents of the yank register, while @" returns the contents of the default register. So the expression :%s//\=@0/g tells Vim to substitute the last pattern with the contents of the yank register.

Comparison

Look at this command:

​=> ​:%s/Pragmatic Vim/Practical Vim/g​

Compare it with this sequence of commands:

​=> ​:let @/='Pragmatic Vim'​

​=> ​:let @a='Practical Vim'​

​=> ​:%s//\=@a/g​

:let @/=’Pragmatic Vim’ is a programmatic way of setting the search pattern. It has the same effect as executing the search /Pragmatic Vim<CR> (except that running :let @/=’Pragmatic Vim’ does not create a record in the search history).

	 	 Likewise, :let @a=’Practical Vim’ sets the contents of the a register. The end result is the same as if we had visually selected the text「Practical Vim」and then typed "ay to yank the selection into register a.

Both substitute commands do the same thing—they replace all occurrences of「Pragmatic Vim」with「Practical Vim.」But think about the consequences of each approach.

In the first case, we create a record in our command history that reads :%s/Pragmatic Vim/Practical Vim/g. That’s unambiguous. Later in our editing session, if we realize that we need to repeat this substitute command, we can dial it up from the command history and play it back as is. No surprises.

In the second case, we create a record in our command history that reads :%s//\=@a/g. That looks pretty cryptic, don’t you think?

When we ran this substitute command for the first time, the search pattern was「Pragmatic Vim,」while the a register contained the text「Practical Vim.」But half an hour later, our current search pattern could have changed dozens of times, and we might have overwritten the a register to contain something else. So if we repeated the :%s//\=@a/g command, it could have a completely different effect!

We could exploit this. We could search for the text we want to act upon and yank its replacement into register a. Then we could replay the :%s//\=@a/g command, and it would use the values of @/ and @a that we had just prepared. Next we could search for something else and yank another replacement string into register a, and when we replayed the :%s//\=@a/g command, it would do something else entirely.

Try it out. You might love it or you might hate it. But either way, it’s a pretty neat trick!

Tip 93 Repeat the Previous Substitute Command

	 	 At times, we might have to amend the range of a substitute command. We might have made a mistake on our first try, or maybe we just want to rerun the command exactly but on a different buffer. A couple of shortcuts make it easy to repeat the substitute command.

Repeat a Line-Wise Substitution Across the Entire File

Suppose that we’ve just executed this command, which acts upon the current line:

​=> ​:s/target/replacement/g​

	 We realize our mistake at once: we should have prepended %. No harm done. We can repeat the command across the entire file just by pressing g& (see g&ⓘ), which is equivalent to running the following:

​=> ​:%s//~/&​

This longhand command spells out the following instruction: repeat the last substitute command using the same flags, the same replacement string, and the current search pattern, but use the % range. In other words, repeat the last substitution across the entire file.

The next time you catch yourself tweaking the search history to prepend a % to a substitute command that is otherwise all right, try hitting g& instead.

Amend the Range of a Substitute Command

	 Start with this code:

substitution/mixin.js

​ mixin = {

​ applyName: ​function​(config) {

​ ​return​ Factory(config, ​this​.getName());

​ },

​ }

Suppose that we want to extend it to look like this:

​ mixin = {

​ applyName: ​function​(config) {

​ ​return​ Factory(config, ​this​.getName());

​ },

​ applyNumber: ​function​(config) {

​ ​return​ Factory(config, ​this​.getNumber());

​ },

​ }

The new applyNumber function is almost identical to the existing one. So let’s start off by duplicating the applyName function. Then we can use the substitute command to change some occurrences of「Name」to「Number.」But there’s a mistake in the following workflow:

KeystrokesBuffer Contents

{start}

​ mixin = {

​ applyName: function(config) {

​ return Factory(config, this.getName());

​ },

​ }

Vjj

​ mixin = {

​ applyName: function(config) {

​ return Factory(config, this.getName());

​ },

​ }

yP

​ mixin = {

​ applyName: function(config) {

​ return Factory(config, this.getName());

​ },

​ applyName: function(config) {

​ return Factory(config, this.getName());

​ },

​ }

:%s/Name/Number/g

​ mixin = {

​ applyNumber: function(config) {

​ return Factory(config, this.getNumber());

​ },

​ applyNumber: function(config) {

​ return Factory(config, this.getNumber());

​ },

​ }

	 	 Can you see what went wrong? We used the % symbol as a range, so it changed every occurrence of「Name」to「Number.」Instead, we should have specified a range to focus the substitute command on the lines of the second function (the duplicate).

Not to worry. We can easily undo the mistake and fix it. Have a look at the following:

KeystrokesBuffer Contents

u

​ mixin = {

​ applyName: function(config) {

​ return Factory(config, this.getName());

​ },

​ applyName: function(config) {

​ return Factory(config, this.getName());

​ },

​ }

gv

​ mixin = {

​ applyName: function(config) {

​ return Factory(config, this.getName());

​ },

​ applyName: function(config) {

​ return Factory(config, this.getName());

​ },

​ }

:’<,’>&&

​ mixin = {

​ applyName: function(config) {

​ return Factory(config, this.getName());

​ },

​ applyNumber: function(config) {

​ return Factory(config, this.getNumber());

​ },

​ }

	 The gv command enables Visual mode and rehighlights the last selection (we discussed it in Tip 21). When we press : in Visual mode, the command line is prepopulated with the range :’<,’>, which focuses the next Ex command on the selected lines.

The :&& command requires some explanation, since the first and second & symbols have different meanings. The first one forms the :& Ex command, which repeats the last :substitute command (see :&ⓘ), while the second one indicates that the flags from the previous :s command should be reused.

Discussion

We can always specify a new range and replay the substitution using the :&& command. It doesn’t matter what range was used the last time. :&& by itself acts on the current line, :’<,’>&& acts on the visual selection, and :%&& acts on the entire file. As we saw already, the g& command is a handy shortcut for :%&&.

Fixing the & Command

	 The & command is a synonym for :s, which repeats the last substitution. Unfortunately, if any flags were used, the & command disregards them, meaning that the outcome could be quite different from the previous substitution.

	 Making & trigger the :&& command is more useful. It preserves flags and therefore produces more consistent results. These mappings fix the & command in Normal mode and create a Visual mode equivalent:

​ nnoremap & :&&<CR>

​ xnoremap & :&&<CR>

Tip 94 Rearrange CSV Fields Using Submatches

	 	 	 	 In this tip, we’ll see how submatches captured from the search pattern can be referenced in the replacement field.

Let’s say that we have a CSV file containing a list of email addresses along with first and last names:

substitution/subscribers.csv

​ last name,first name,email

​ neil,drew,drew@vimcasts.org

​ doe,john,john@example.com

Now suppose that we want to swap the order of the fields so that the email comes first, then the first name, and finally the last name. We could use this substitute command to do it:

​=> ​/\v^([^,]*),([^,]*),([^,]*)$​

​=> ​:%s//\3,\2,\1​

In the pattern, [^,] matches anything that isn’t a comma. So ([^,]*) matches zero or more consecutive non-commas and captures the result as a submatch (refer to Tip 76). We repeat this three times to capture each of the three fields in the CSV file.

We can reference these submatches using the \n notation. So, in the replacement field, \1 will refer to the last name field, \2 refers to the first name field, and \3 refers to the email field. Having sliced each line into the individual fields, we can rearrange them into the order we want, namely \3,\2\,1—email, first name, last name.

The result of running this command looks like this:

​ email,first name,last name

​ drew@vimcasts.org,drew,neil

​ john@example.com,john,doe

Tip 95 Perform Arithmetic on the Replacement

	 	 	 The replacement field needn’t be a simple string. We can evaluate a Vim script expression and then use the result as the replacement string. Thus with a single command, we can promote every HTML header tag in a document.

Suppose that we have an HTML document like this:

substitution/headings.html

​ <h2>Heading number 1</h2>

​ <h3>Number 2 heading</h3>

​ <h4>Another heading</h4>

We want to promote each heading, turning <h2> into <h1>, <h3> into <h2>, and so on. To put it another way, we want to subtract one from the numeral part of all HTML header tags.

We’ll harness the substitute command to do it. Here’s the general idea: we write a pattern that matches the numeral portion of HTML header tags. Then we write a substitute command that uses a Vim script expression to subtract one from the number that was captured. When we run the substitute command globally across the entire file, all HTML header tags will be changed with that single command.

The Search Pattern

The only thing that we want to change is the numeral part of the header tags, so ideally we want to create a pattern that matches that and nothing else. We don’t want to match all digits. We only want to match the ones that immediately follow <h or </h. This pattern should do the trick:

​=> ​/\v\<\/?h\zs\d​

The \zs item allows us to zoom in on part of the match. To simplify our example, we could say that a pattern of h\zs\d would match the letter h followed by any digit (h1, h2, and so on). The placement of \zs indicates that the h itself would be excluded from the match, even though it is an integral part of the broader pattern (we met the \zs item in Tip 78, where we compared it to Perl’s positive lookbehind assertion). Our pattern looks slightly more complex, because we don’t just match h1 and h2, but <h1, </h1, <h2, </h2, and so on.

Try executing this search for yourself. You should see that the numeral part of each header tag is highlighted, while the freestanding digits are not.

The Substitute Command

	 	 	 	 We want to perform arithmetic inside the replacement field of our substitute command. To do this, we’ll have to evaluate a Vim script expression. We can fetch the current match by calling the submatch(0) function. Since our search pattern matched a digit and nothing else, we can expect that submatch(0) will return a number. From this, we subtract one and return the result to be substituted in place of the match.

This substitute command should work:

​=> ​:%s//\=submatch(0)-1/g​

When we execute the search followed by this substitute command on our fragment of HTML, it produces this result:

​ <h1>Heading number 1</h1>

​ <h2>Number 2 heading</h2>

​ <h3>Another heading</h3>

All HTML header tags have been changed, but the freestanding numerals have been left untouched.

Tip 96 Swap Two or More Words

	 	 	 	 We can devise a substitute command that swaps all occurrences of one word with another and vice versa by using the expression register and a Vim script dictionary.

Take this excerpt:

substitution/who-bites.txt

​ The dog bit the man.

Suppose that we want to swap the order of the words「dog」and「man.」We could, of course, use a succession of yank and put operations, as demonstrated in ​Swap Two Words​. But let’s consider how we would go about doing this with the substitute command.

Here’s a naïve attempt at a solution:

​=> ​:%s/dog/man/g​

​=> ​:%s/man/dog/g​

The first command replaces the word「dog」with「man,」leaving us with the phrase「the man bit the man.」Then the second command replaces both occurrences of「man」with「dog,」giving us「the dog bit the dog.」Clearly, we have to try harder.

A two-pass solution is no good, so we need a substitute command that works in a single pass. The easy part is writing a pattern that matches both「dog」and「man」(think about it). The tricky part is writing an expression that accepts either of these words and returns the other one. Let’s solve this part of the puzzle first.

Return the Other Word

We don’t even have to create a function to get the job done. We can do it with a simple dictionary data structure by creating two key-value pairs. In Vim, try typing the following:

​=> ​:let swapper={"dog":"man","man":"dog"}​

​=> ​:echo swapper["dog"]​

​<= man

​=> ​:echo swapper["man"]​

​<= dog

When we pass "dog" as a key to our swapper dictionary, it returns "man", and vice versa.

Match Both Words

Did you figure out the pattern? Here it is:

​=> ​/\v(<man>|<dog>)​

This pattern simply matches the whole word「man」or the whole word「dog.」The parentheses serve to capture the matched text so that we can reference it in the replacement field.

All Together Now

Let’s put everything together. We’ll start by running the search command. This should cause all occurrences of「dog」and「man」to be highlighted. Then when we run the substitute command, we can leave the search field blank and it will simply reuse the last search pattern (as discussed in Tip 91).

For the replacement, we’ll have to evaluate a little bit of Vim script. That means using the \= item in the replacement field. This time, we won’t bother assigning the dictionary to a variable, we’ll just create it inline for a single use.

Normally we could refer to captured text using Vim’s \1, \2 (and so on) notation. But in Vim script, we have to fetch the captured text by calling the submatch() function (see submatch()ⓘ).

When we put everything together, this is what we get:

​=> ​/\v(<man>|<dog>)​

​=> ​:%s//\={"dog":"man","man":"dog"}[submatch(1)]/g​

Discussion

This is a daft example! We have to type out the words「man」and「dog」three times each. Obviously, it would be quicker to change the two words in the document, one time each. But if we were working with a large body of text with multiple occurrences of each word, then this extra effort could quickly pay for itself. Note that this technique could easily be adapted to swap three or more words in a single pass.

There still remains the issue of all that typing. With a little bit more Vim script, we could write a custom command that exposed a more user-friendly interface that would do all of the repetitive work for us under the hood. That’s beyond the scope of this book, but check out ​Abolish.vim: A Supercharged Substitute Command​, for inspiration.

Abolish.vim: A Supercharged Substitute Command

	 	 	 One of my favorite plugins from Tim Pope is called Abolish.[23] It adds a custom command called :Subvert (or :S for short), which acts like a supercharged version of Vim’s :substitute command. Using this plugin, we could swap the words「man」and「dog」by issuing the following command:

​=> ​:%S/{man,dog}/{dog,man}/g​

Not only is this easier to type, but it’s much more flexible too. As well as replacing「man」with「dog」(and vice versa), it would also replace「MAN」with「DOG」and「Man」with「Dog.」This example merely scratches the surface of this terrific plugin. I encourage you to explore its other capabilities.

Tip 97 Find and Replace Across Multiple Files

	 	 	 The substitute command operates on the current file. So what do we do if we want to make the same substitution throughout an entire project? Although this scenario is common, Vim doesn’t include a dedicated command for project-wide find and replace. We can get this functionality by combining a few of Vim’s primitive commands that operate with the quickfix list.

As a demonstration, we’ll use the refactor-project directory, which you can find in the source files that come distributed with this book. It contains the following files, reproduced here with their contents:

​ refactor-project/

​ about.txt

​ Pragmatic Vim is a hands-on guide to working with Vim.

​

​ credits.txt

​ Pragmatic Vim is written by Drew Neil.

​

​ license.txt

​ The Pragmatic Bookshelf holds the copyright for this book.

​

​ extra/

​ praise.txt

​ What people are saying about Pragmatic Vim...

​

​ titles.txt

​ Other titles from the Pragmatic Bookshelf...

Each of these files contains the word「Pragmatic,」either as part of the phrase「Pragmatic Bookshelf」or「Pragmatic Vim.」We’ll do a find and replace to change each occurrence of「Pragmatic Vim」to「Practical Vim」while leaving each occurrence of「Pragmatic Bookshelf」unchanged.

If you’d like to follow along, download the source code from Practical Vim’s book page on the Pragmatic Bookshelf site. Before opening Vim, change to the refactor-project directory.

The workflow described here depends on the :cfdo command, which first became available in Vim version 7.4.858. If you are using an older version of Vim you should upgrade to get access to this command.

The Substitute Command

Let’s start by devising the substitute command. We want to compose a pattern that matches the word「Pragmatic」when it appears in the phrase「Pragmatic Vim,」but not when it appears in the phrase「Pragmatic Bookshelf.」This pattern will do the trick:

​=> ​/Pragmatic\ze Vim​

This uses the \ze item to exclude the word「Vim」from the match (see Tip 78). Then we can run this substitute command:

​=> ​:%s//Practical/g​

	 	 Next we just need to figure out how to execute that command across the entire project. We’ll do this in two steps. First we’ll perform a project-wide search for our target pattern. Then we’ll run the substitute command on the files that returned a positive match.

Execute a Project-Wide Search Using ‘:vimgrep’

To perform a project-wide search, we’ll reach for the :vimgrep command (see Tip 111​Grep with Vim’s Internal Search Engine​). Since this uses Vim’s built-in search engine, we can reuse the exact same pattern. Try running this:

​=> ​/Pragmatic\ze Vim​

​=> ​:vimgrep // **/*.txt​

The search field for this command is delimited by the two adjacent / characters. We’ve left the search field blank, which tells Vim to run :vimgrep using the last search pattern. We use the **/*.txt wildcard to tell vimgrep to look inside all files contained in the current directory that use the .txt extension.

Execute a Project-Wide Substitute Command Using ‘:cfdo’

Each match returned by vimgrep is recorded in the quickfix list (see Chapter 17, ​Compile Code and Navigate Errors

with the Quickfix List​). We can browse the results by running :copen, which opens the quickfix window. But instead of stepping through the results one at a time, we want to run the substitute command on every file that appears in the quickfix list. We can do so using the :cfdo command (see :cfdoⓘ).

Before using the :cfdo command, make sure the hidden setting is enabled:

​=> ​:set hidden​

	 This setting enables us to navigate away from a modified file without first saving it. Refer to Tip 38, for a more detailed discussion.

Now we can execute our substitution command across all the files in the quickfix list by running this:

​=> ​:cfdo %s//Practical/gc​

The c flag is optional here. It lets us view each match and decide whether we want to perform the substitution (see Tip 90). We’ll finish by writing the changes to disk:

​=> ​:cfdo update​

The :update command saves the file, but only if it has been changed (see updateⓘ).

Note that the last two commands could be combined into one, like this:

​=> ​:cfdo %s//Practical/g | update​

	 The | character has a different meaning on Vim’s command line than shell users might expect. In Unix, the pipe character passes standard output from one command into the standard input of the next command (creating a「pipeline」). In Vim, | is simply a command separator, making it equivalent to the semicolon in the Unix shell. Look up :barⓘ for more details.

Summary

Here’s the complete sequence of commands:

​=> ​/Pragmatic\ze Vim​

​=> ​:vimgrep // **/*.txt​

​=> ​:cfdo %s//Practical/gc​

​=> ​:cfdo update​

We start by composing a search pattern and checking that it works in the current buffer. Then we use :vimgrep to search the whole project for the same pattern, populating the quickfix list with the results. We can then iterate through the files in the quickfix list using :cfdo to run the :substitute and :update commands.

Footnotes

[23]

https://github.com/tpope/vim-abolish

Copyright © 2016, The Pragmatic Bookshelf.

Chapter 15

Global Commands


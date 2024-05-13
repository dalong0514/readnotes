Having studied Vim’s regular expression engines in the previous chapter, let’s see how we can put them to use with the search command. We’ll start with the basics: how to execute a search, highlight matches, and jump between them. Then we’ll learn a couple of tricks that exploit Vim’s incremental search feature, which not only gives us instant feedback but can also save us typing by autocompleting our match. We’ll also learn how to count the number of matches that occur in a document.

The search offsets feature allows us to position our cursor relative to a match. We’ll look at one scenario where search offsets can streamline our workflow. Then we’ll see how search offsets can be exploited to operate on a complete search match.

Composing a regular expression—and getting it right—often takes a few attempts, so developing a workflow that allows us to iterate on a pattern is important. We’ll learn about two methods for doing this: calling up our search history and working in the command-line window.

Have you ever wished for a simple way of searching for text that’s already present in your document? We’ll finish by devising a simple customization that overrides the * command to search for the current visual selection.

Tip 80 Meet the Search Command

	 	 In this tip, we’ll cover the basics of using the search command, including how to specify the direction of a search, repeat (or reverse) the last search, and work with the search history.

Execute a Search

	 	 	 	 From Normal mode, the / key brings up Vim’s search prompt. Here we can enter the pattern, or literal text, that we want to search for. Vim does nothing until we press the <CR> key to execute the search. If we press the <Esc> key instead, the search prompt will be dismissed and we’ll return to Normal mode.

When we execute a search, Vim scans forward from the current cursor position, stopping on the first match that it finds. If nothing is found before the end of the document, Vim informs us「search hit BOTTOM, continuing at TOP.」This means that in some circumstances, a forward search can take us backward. That’s not as disorienting as it might sound. Just remember that the search command wraps around the document, and it’ll make sense.

	 If you ever need to search from the current cursor position to the end of the document without wrapping around, you can disable the ‘wrapscan’ option (see 'wrapscan'ⓘ).

Specify the Search Direction

	 	 	 	 When a search is initiated with the / key, Vim scans the document forward. If we use the ? key to bring up the search prompt, Vim searches backward instead. The search prompt always begins with either the / or ? character, which indicates in what direction the search will scan.

Repeat the Last Search

	 	 The n command jumps to the next match, and the N command jumps to the previous match. We can easily navigate between matches in the current document with the n and N commands. But the definition of「next match」depends on context.

The n command preserves the direction as well as any offsets that were applied to the previous search. (We’ll meet offsets in Tip 83.) So if we execute a forward search using /, then n will continue searching forward. Whereas if we used ? for the original search, then n will continue backward. Meanwhile, the N command always goes in the opposite direction to n.

Sometimes we might want to repeat a search using the same pattern but changing the direction or offset. In this case, it’s useful to know that if we execute a search without providing a pattern, Vim will just reuse the pattern from the previous search. The following table summarizes the matrix of options for repeating a search:

CommandEffect

n

Jump to next match, preserving direction and offset

N

Jump to previous match, preserving direction and offset

/<CR>

Jump forward to next match of same pattern

?<CR>

Jump backward to previous match of same pattern

gn

Enable character-wise Visual mode and select next search match

gN

Enable character-wise Visual mode and select previous search match

Suppose we use ? to initiate a search. Having jumped backward to the previous match, we then decide that we want to skip forward through the remainder of the matches. We could do it with the N key, but somehow that makes everything feel upside down. Instead, we could execute /<CR>. This executes a forward search, reusing the same pattern. Now, we can use the n key to skip forward through the rest of the matches in the document.

The n and N commands move the cursor, placing it on a match for the current pattern. But what if we want to select the matching text using Visual mode so that we can make some modifications to it? That’s where the gn command comes in. When used from Normal mode, gn moves the cursor to the next match, then enables Visual mode and selects the matching text. If your cursor is already on a match, then gn will select the current match without you having to move the cursor. We’ll look at this command in in more detail in Tip 84.

Recall Historical Searches

	 	 Vim records our search patterns so we can easily recall them. When the search prompt is visible, we can scroll through the previous searches by pressing the <Up> key. In fact, the interface for browsing the search history is just the same as for browsing the command-line history. We covered this in more depth in Tip 34. We’ll put these techniques into action in Tip 85.

Tip 81 Highlight Search Matches

	 	 	 Vim can highlight search matches, but this feature is not enabled by default. Learn how to enable it, and (just as importantly) how to mute it for those times when the highlighting takes over.

	 The search command allows us to jump quickly between matches, but by default, Vim does nothing to make them stand out visually. We can fix this by enabling the ‘hlsearch’ option, (see 'hlsearch'ⓘ), which causes all matches to be highlighted throughout the active document as well as in any other open split windows.

Mute Search Highlighting

Search highlighting is a useful feature, but sometimes it can make itself unwelcome. If we search for a common string, for example, or a pattern with hundreds of matches, we’ll soon find that our workspace is riddled with yellow (or whatever hue the active color scheme uses).

	 In this scenario, we could run :set nohlsearch to disable the feature entirely (:se nohls and :se hls! also work). But when we come to execute another search, we might wish to reenable the feature again.

Vim has a more elegant solution. The :nohlsearch command can be used to mute the search highlighting temporarily (see :nohⓘ). It will stay muted until the next time you execute a new or repeat search command. See ​Create a Shortcut to Mute Highlighting​, for a suggested mapping.

Create a Shortcut to Mute Highlighting

Typing :noh<CR> to mute search highlighting is laborious. We can speed things up by creating a mapping such as this:

​ nnoremap <​silent​> <C-​l​> :<C-​u​>​nohlsearch​<CR><C-​l​>

Normally, <C-l> clears and redraws the screen (see CTRL-Lⓘ). This mapping builds on top of the usual behavior by muting search highlighting.

Tip 82 Preview the First Match Before Execution

	 	 	 Vim’s search command is much more useful when the incremental search feature is enabled. Here are a couple of ways that this option can improve your workflow.

	 By default, Vim sits idle as we prepare our search pattern, only springing into action when we press <CR>. My favorite enhancement is enabled with the ‘incsearch’ setting (see 'incsearch'ⓘ). This tells Vim to show a preview of the first match based on what has been entered so far into the search field. Each time we enter another character, Vim instantly updates the preview. This table illustrates how it works:

KeystrokesBuffer Contents

{start} ​ The car was the color of a carrot.

/car

​ The car was the color of a carrot.

/carr

​ The car was the color of a carrot.

/carr<CR>

​ The car was the color of a carrot.

After typing「car」into the search field, Vim highlights the first match, which in this case is the word「car」itself. As soon as we enter the next「r」character, our preview ceases to match, and Vim skips forward to the next matching word. This time, it’s「carrot.」If we were to press the <Esc> key at this point, the search prompt would be dismissed and our cursor restored to its original position at the start of the line. But instead, we press <CR> to execute the command, causing our cursor to jump to the start of the word「carrot.」

This instant feedback lets us know when we’ve hit our target. If our intention was simply to move the cursor to the start of the word「carrot,」then there’s no need to type the full word into the search field. In this case, /carr<CR> is enough. Without the ‘incsearch’ feature enabled, we wouldn’t know whether or not our pattern would hit the target until we executed the search.

Check for the Existence of a Match

In our example, we have two partial matches for「car」on the same line. But imagine if the words「car」and「carrot」were separated by several hundred words. When we updated our search field from「car」to「carr,」Vim would have to scroll the document to bring the word「carrot」into view. And that is exactly what happens.

	 Suppose that we just want to check if the word「carrot」is present in the current document without moving our cursor. With the ‘incsearch’ option enabled, we would simply have to dial up the search prompt and then type as many characters of the word「carrot」as it takes to bring the first occurrence of the word into view. If the word is found, we can just press <Esc>, and we’ll end up right back where we started. No need to interrupt our train of thought.

Autocomplete the Search Field Based on Preview Match

	 	 In that last example, we executed the search command before completing the word「carrot.」That’s good enough if our intention was simply to move our cursor to the first match. But suppose that we needed our pattern to match the entire word「carrot」: for example, if we were planning to follow the search command with a substitute command.

Of course, we could simply type out the「carrot」in full. But here’s a handy shortcut: <C-r><C-w>. This autocompletes the search field using the remainder of the current preview match. If we used this command after entering「carr」into the search field, it would append「ot,」causing the match to encompass the entire word「carrot.」

Note that the <C-r><C-w> autocompletion is slightly brittle in this context. If you prefix your search with the \v item, then <C-r><C-w> will complete the entire word under the cursor (creating /\vcarrcarrot<CR>, for example) instead of the remainder of the word. As long as you are searching for words and not patterns, the autocomplete feature of incremental search can be a nice little time-saver.

Tip 83 Offset the Cursor to the End of a Search Match

	 	 	 A search offset can be used to position the cursor a fixed number of characters away from the start or end of a match. In this tip, we’ll study an example where, by placing the cursor at the end of a match, we’re able to complete a series of changes using the Dot Formula.

Each time we execute a search command, our cursor is positioned on the first character of the match. This default seems reasonable, but sometimes we might rather have the cursor positioned at the end of a search match. Vim makes this possible using its search offset feature (see search-offsetⓘ).

Let’s study an example. In this excerpt, the author has consistently abbreviated the word「language」:

search/langs.txt

​ Aim to learn a new programming lang each year.

​ Which lang did you pick up last year?

​ Which langs would you like to learn?

How would you go about expanding all three occurrences of「lang」to the full word? One solution would be to use the substitute command: :%s/lang/language/g. But let’s see if we can find an alternative that uses the Dot Formula. We might learn something along the way.

First let’s tackle this without using a search offset. We’ll start by searching for the string that we want to modify: /lang<CR>. That places our cursor at the start of the first match. From there, we can append at the end of the word by typing eauage<Esc>. Appending at the end of a word is such a common task that ea should flow from your fingers as though it were a single command.

Now we just need to maneuver our cursor into the right position, and the dot command should take care of the rest. We can amend the next occurrence of「lang」by typing ne. - n jumps to the start of the next match; then e moves us to the end of the word, and . appends the letters required to complete the word. That’s three keystrokes. We haven’t achieved the ideal Dot Formula, but at least it gets the job done.

Or does it? If we bash out the same command sequence a second time, ne., we’ll end up mangling the final word. Can you see why? The final occurrence of「lang」is actually an abbreviation of「languages」(note the plural). So if we blindly repeat our suboptimal Dot Formula, we’ll create the frankenword「langsuage.」Clearly, this is one scenario where placing the cursor at the end of the match, rather than at the end of the word, would be preferable.

Table 14, ​Improved Workflow Using Search Offset​ shows an improved workflow.

* * *

Table 14. Improved Workflow Using Search Offset

KeystrokesBuffer Contents

{start}

​ Aim to learn a new programming lang each year.

​ Which lang did you pick up last year?

​ Which langs would you like to learn?

/lang/e<CR>

​ Aim to learn a new programming lang each year.

​ Which lang did you pick up last year?

​ Which langs would you like to learn?

auage<Esc>

​ Aim to learn a new programming language each year.

​ Which lang did you pick up last year?

​ Which langs would you like to learn?

n

​ Aim to learn a new programming language each year.

​ Which lang did you pick up last year?

​ Which langs would you like to learn?

.

​ Aim to learn a new programming language each year.

​ Which language did you pick up last year?

​ Which langs would you like to learn?

n.

​ Aim to learn a new programming language each year.

​ Which language did you pick up last year?

​ Which languages would you like to learn?

* * *

Here, we search for /lang/e<CR>, which places the cursor at the end of the search match, exactly where we need it. Each time we use the n command, our cursor is positioned at the end of the next search match, setting us up perfectly to use the dot command. The search offset has enabled us to achieve an ideal Dot Formula.

In the real world, it won’t always be obvious when a search offset will come in handy. Suppose that we started off by executing the search command without the offset. Then, after pressing n a couple of times, we realize that we’d prefer to place the cursor at the end of the match. That’s no problem: we could simply run //e<CR>. When we leave the search field blank like this, Vim reuses the pattern from the previous search. So this repeats the last search but with an offset.

Tip 84 Operate on a Complete Search Match

	 	 	 	 	Vim’s search command allows us to highlight matches and jump between them quickly. We can also operate on regions of text that match our current pattern using the gn command.

Vim’s search command is convenient for jumping between occurrences of a pattern, but what if we want to make a change to each match? This used to be awkward, but the gn command (available since Vim 7.4.110) offers a very efficient workflow for operating on search matches.

Let’s look at an example. In this excerpt, we’re dealing with classes called XmlDocument, XhtmlDocument, XmlTag, and XhtmlTag:

search/tag-heirarchy.rb

​ ​class​ XhtmlDocument < XmlDocument; ​end​

​ ​class​ XhtmlTag < XmlTag; ​end​

Suppose we want to rename each class to look like this instead:

​ ​class​ XHTMLDocument < XMLDocument; ​end​

​ ​class​ XHTMLTag < XMLTag; ​end​

To do this we can use the gU{motion} operator to convert a range of text to uppercase (see gUⓘ). For the motion, we’ll use the gn command, which operates on the next match (see gnⓘ). If the cursor is positioned on a match, then gn will act upon the current match. But if the cursor is not currently on a match, then gn will jump forward to the next match and apply the operation there. Table 15, ​Operating on a Complete Search Match​, demonstrates how we can use this.

* * *

Table 15. Operating on a Complete Search Match

KeystrokesBuffer Contents

{start}

​ class XhtmlDocument < XmlDocument; end

​ class XhtmlTag < XmlTag; end

/\vX(ht)?ml\C<CR>

​ class XhtmlDocument < XmlDocument; end

​ class XhtmlTag < XmlTag; end

gUgn

​ class XHTMLDocument < XmlDocument; end

​ class XhtmlTag < XmlTag; end

n

​ class XHTMLDocument < XmlDocument; end

​ class XhtmlTag < XmlTag; end

.

​ class XHTMLDocument < XMLDocument; end

​ class XhtmlTag < XmlTag; end

n.

​ class XHTMLDocument < XMLDocument; end

​ class XHTMLTag < XmlTag; end

.

​ class XHTMLDocument < XMLDocument; end

​ class XHTMLTag < XMLTag; end

* * *

To begin with, we write a regular expression to match either Xml or Xhtml. That’s easy enough: /\vX(ht)?ml\C<CR> does the job. The \C item enforces case sensitivity, so the pattern won’t match XML or XHTML. After searching for this pattern, the four ranges of text that we want to operate on light up with search highlighting, and our cursor is positioned at the start of the first match.

The gUgn command transforms the matching text to uppercase. The beauty of this command is that it’s easily repeated. We can jump to the next match by pressing n and repeat the change with .. That’s two keystrokes per change: our classic Dot Formula. But this is a rare case where we can be even more economical with our keystrokes.

Improving Upon the Dot Formula

We could describe the gUgn operation as: convert the next match to uppercase. If the cursor is already positioned on a match, then pressing . will affect the match under the cursor. But if the cursor is not positioned on a match, then . will jump forward to the next match and apply the operation there. We don’t even have to press the n key. We only have to press ., which means we can repeat the change for each match with only one keystroke per change.

The classic Dot Formula has two parts: one keystroke to move, another to make the change. The gn command lets us condense these two steps into one, because gn operates on the next match, rather than at the current cursor location. If we can arrange things such that pressing the . command jumps to the next match and applies the last operation, then we can use one keystroke to repeat each change. I call this the Improved Dot Formula.

Try working through the same example with a case-insensitive pattern, by changing the \C item to \c. You’ll find that you can still repeat each change by pressing n. (the classic Dot Formula), but pressing . by itself won’t advance through the matches in the document. That’s because the case-insensitive pattern matches the text before and after running the gUgn command: for example, it matches both Xml and XML. In this context, the . command will repeat the change for the match under the cursor, rather than jumping to the next match. You won’t see anything happen, because converting XML to uppercase makes no change.

For the Improved Dot Formula to work, our search pattern should match the target text before making a change, but not after making the change. In this particular example, our gU operation changes the case of the target text, so it’s vital that our search pattern is case-sensitive. But we don’t always have to use a case-sensitive pattern to make the Improved Dot Formula work.

Try working through the same example, but this time use the dgn operation to delete the matching text. Or use cgnJson<Esc> to replace each match with Json. In both cases, you should be able to repeat the change for each match just by pressing .. As long as the target text is modified so as to no longer match the search pattern, we can make use of the Improved Dot Formula.

Be careful when using the Improved Dot Formula on a large file, where the matches may be spaced far apart. If you use n., then you can pause between the two keystrokes and decide whether or not you want to repeat the change by pressing the . key. Whereas if you use . without first jumping to the next match, you won’t get to look at all the matches before changing them.

Since the release of Vim version 7.4.110, the gn command has become a staple of my workflow. If you’re using an older version of Vim, this command is a good reason to upgrade!

Tip 85 Create Complex Patterns by Iterating upon Search History

	 	 	 	 	 Writing regular expressions is hard. We won’t get it right the first time, so the next best thing is to develop a frictionless workflow that allows us to develop a pattern by iteration. Being able to recall and edit previous items from our search history is the trick.

In this example text, the prime symbol has been used as a quote mark:

search/quoted-strings.txt

​ This string contains a 'quoted' word.

​ This string contains 'two' quoted 'words.'

​ This 'string doesn't make things easy.'

	 	 	We want to compose a regular expression to match each quoted string. This will take a few tries, but when we get it right, we’ll run a substitute command to transform the text to use real double-quote symbols, like this:

​ This string contains a「quoted」word.

​ This string contains「two」quoted「words.」

​ This「string doesn't make things easy.」

Draft 1: A Broad Match

Let’s begin with a crude search:

​=> ​/\v'.+'​

This matches a single ’ character, followed by any character one or more times, and terminates with a final ’ character. After executing this search command, our document looks like this:

​ This string contains a ’quoted’ word.

​ This string contains ’two’ quoted ’words.’

​ This ’string doesn’t make things easy.’

	 The first line looks fine, but there’s a problem with line two. The .+ item in the pattern performs a greedy match, meaning that it matches as many characters as possible. But we want to generate two separate matches on this line: one for each quoted word. Let’s go back to the drawing board.

Draft 2: Refinement

	 Instead of using the . symbol to match any character, let’s be a bit more specific. We actually want to match any character except ’, which can be done using [^’]+. We’ll refine our pattern to look like this instead:

​=> ​/\v'[^']+'​

We don’t have to type this out from scratch. Instead, we can press /<Up>, which prepopulates the search field with the most recent pattern. We only have to make a small change, so we’ll use the <Left> and backspace keys to delete the . character from the pattern and then type in the replacement. When we execute the search, we’ll get the following matches:

​ This string contains a ’quoted’ word.

​ This string contains ’two’ quoted ’words.’

​ This ’string doesn’t make things easy.'

That’s an improvement. The first two lines match up just as we want them to, but line three raises a new issue. The ’ character is used here as an apostrophe, which shouldn’t terminate the match. We’ll have to refine our pattern some more.

Draft 3: Another Iteration

Now we need to consider what differentiates an apostrophe from a closing quote mark. Here are a few examples:「won’t,」「don’t,」and「we’re.」In each case, the ’ character is followed immediately by a letter—not by a space or punctuation mark. We could update our pattern to allow ’ characters as long as they are followed by a word character. Here’s our next refinement:

​=> ​/\v'([^']|'\w)+'​

This involves some fairly substantial changes. Not only do we have to type in the extra ’\w item, we also have to wrap the two alternatives in parentheses and separate them with a pipe. It’s time to bring out the big guns.

Instead of pressing /<Up> to prefill the search field with our last pattern, let’s press q/ to summon the command-line window. This acts more or less like a regular Vim buffer, but it’s prepopulated with our search history, one item per line (see ​Meet the Command-Line Window​). We can use the full power of Vim’s modal editing to amend the last pattern.

The following sequence of edits demonstrates how we might make this particular change. If you’re struggling to understand c%(<C-r>")<Esc>, refer to Tip 55, and Tip 15.

KeystrokesBuffer Contents

{start}

​ \v'[^']+'

f[

​ \v'[^']+'

c%(<C-r>")<Esc>

​ \v'([^'])+'

i|’\w<Esc>

​ \v'([^']|'\w)+'

When we’ve got the pattern looking how we want it, we just press the <CR> key to execute the search. The document should light up as follows:

​ This string contains a ’quoted’ word.

​ This string contains ’two’ quoted ’words.’

​ This ’string doesn’t make things easy.’

Score!

Draft 4: One Final Tweak

Our pattern matches in all the right places, but we need to make one final change before we can execute our substitute command. We want to capture everything inside the quotes by wrapping it in parentheses. This is our final pattern:

​=> ​/\v'(([^']|'\w)+)'​

We could either run /<Up> and edit the search field, or we could run q/ and make the change in the command-line window. Use whichever you feel is more appropriate. The search highlighting won’t look any different from the last time, but for each match, the text inside quotes will be assigned to the \1 capture register. That means we can run the following substitute command:

​=> ​:%s//「\1」/g​

We can leave the search field blank, and Vim will reuse the last search command (for more details, skip ahead to Tip 91). Here’s the outcome from running this command:

​ This string contains a「quoted」word.

​ This string contains「two」quoted「words.」

​ This「string doesn't make things easy.」

Discussion

What we’ve done here is effectively identical to this:

​=> ​:%s/\v'(([^']|'\w)+)'/「\1」/g​

Would you trust yourself to type that out correctly in one go?

Don’t worry about getting a search pattern right the first time. Vim keeps our most recent search pattern two keystrokes away, so it’s easy to refine a pattern. Start with a broad match; then take as many steps as you need to focus on your target.

	 Being able to edit the command line directly is great for simple edits. If we have the ‘incsearch’ setting enabled, then we get the added bonus of live feedback as we edit the command line. We lose this perk as soon as we call up the command-line window. But with the full power of Vim’s modal editing at our fingertips, this is a fair trade-off.

Tip 86 Count the Matches for the Current Pattern

	 	 	 	 This tip shows a couple of ways that you can count the number of matches for a pattern.

Suppose we want to find out how many times the word「buttons」appears in this excerpt:

search/buttons.js

​ ​var​ buttons = viewport.buttons;

​ viewport.buttons.previous.show();

​ viewport.buttons.next.show();

​ viewport.buttons.index.hide();

We’ll start by searching for that word:

​=> ​/\<buttons\>​

Now we can move from one match to another by pressing the n and N keys, but Vim’s search command doesn’t give us any indication of how many matches are in the current document. We can get a match count by using either the :substitute or :vimgrep command.

Count Matches with the ‘:substitute’ Command

We can get a match count by running this command:

​=> ​/\<buttons\>​

​=> ​:%s///gn​

​<= 5 matches on 4 lines

We’re calling the :substitute command, but the n flag suppresses the usual behavior. Instead of replacing each match with the target, it simply counts the number of matches and then echoes the result below the command line. By leaving the search field blank, we instruct Vim to use the current search pattern. The replacement field is ignored anyway (because of the n flag), so we can leave it blank too.

Note that the command contains three consecutive / characters. The first and second delimit the pattern field, and the second and third delimit the replacement field. Be careful not to omit any of the / characters. Running :%s//gn would replace every match with gn!

Count Matches with the ‘:vimgrep’ Command

The n flag of the :substitute command lets us know the total number of matches for a pattern. But sometimes it would be useful to know that a particular match is, say, number 3 out of a total of 5. We can get that information with the :vimgrep command:

​=> ​/\<buttons\>​

​=> ​:vimgrep //g %​

​<= (1 of 5) var buttons = viewport.buttons;

This command populates the quickfix list with each match found in the current buffer. The :vimgrep command is capable of finding matches across multiple files, but here we’re asking it to look inside a single file. The % symbol expands to the filepath of the current buffer (see cmdline-specialⓘ). Leaving the pattern field blank tells :vimgrep to reuse the current search pattern.

As well as being able to move between matches with the n and N keys, we can now go back and forward using the :cnext and :cprev commands:

​=> ​:cnext​

​<= (2 of 5) var buttons = viewport.buttons;

​=> ​:cnext​

​<= (3 of 5) viewport.buttons.previous.show();

​=> ​:cprev​

​<= (2 of 5) var buttons = viewport.buttons;

I prefer using this technique over the substitute command when I want to look at each match, perhaps making some changes. It’s helpful seeing (1 of 5), then (2 of 5), and so on, which gives me an idea of how much work I’ve still got to do.

The quickfix list is an important feature that’s central to many Vim workflows. You can read more about the quickfix list in Chapter 17, ​Compile Code and Navigate Errors

with the Quickfix List​.

Tip 87 Search for the Current Visual Selection

	 	 	 	 In Normal mode, the * command lets us search for the word under the cursor. Using a small amount of Vim script, we can redefine the * command in Visual mode so that, instead of searching for the current word, it searches for the current selection.

Search for the Current Word in Visual Mode

	 	 	 In Visual mode, the * command searches for the word under the cursor:

KeystrokesBuffer Contents

{start}

​ She sells sea shells by the sea shore.

*

​ She sells sea shells by the sea shore.

We start off in Visual mode with the first three words selected and our cursor placed on the word「sea.」When we invoke the * command, it searches forward for the next occurrence of the word「sea,」extending the range of the visual selection. Although this behavior is consistent with the Normal mode * command, I rarely find it useful.

Before I became hooked on Vim, I used another text editor, which included a「Use selection for find」command. I had the keyboard shortcut for this burned into my fingers and used it all the time. When I switched to Vim, I was surprised to find that it didn’t have such a feature. It always felt to me that triggering the * command from Visual mode should search for the current selection, not the current word. With a small amount of Vim script, we can add this feature to Vim.

Search for the Current Selection (Prior Art)

	 	 If you look up visual-searchⓘ, you’ll find this suggestion:

Here is an idea for a mapping that makes it possible to do a search for the selected text:

​ :vmap X y/<C-R>"<CR>

Note that special characters (like「.」and「*」) will cause problems.

The y command yanks the current visual selection, and /<C-r>"<CR> brings up the search prompt, pastes the contents of the default register, and then executes the search. That solution is simple, but as the cautionary note in Vim’s documentation says, it has limitations.

In Tip 79, we learned how to overcome these limitations. Now let’s put that theory into practice and create a mapping that searches for the current selection without being derailed by special characters.

Search for the Current Selection (Redux)

This snippet of Vim script does the trick:

patterns/visual-star.vim

​ xnoremap * :<C-​u​>​call​ <SID>VSetSearch(​'/'​)<CR>​/<C-R>=@/​<CR><CR>

​ xnoremap # :<C-​u​>​call​ <SID>VSetSearch(​'?'​)<CR>?<C-R>=@/<CR><CR>

​

​ ​function​! s:VSetSearch(cmdtype)

​ ​let​ temp = @s

​ norm! gv"​sy​

​ ​let​ @/ = ​'\V'​ . substitute(escape(@s, a:cmdtype.​'\'), '​\​n​​', '​\\​n​​', '​​g​')

​ ​let​ @s = temp

​ ​endfunction​

You can either paste this into your vimrc file directly or install the visual star search plugin.[22]

	 As well as overriding the * command, we’ve customized the # command, which searches backward for selected text. The xnoremap keyword specifies that the mappings should apply to Visual mode but not to Select mode (see mapmode-xⓘ).

Footnotes

[22]

https://github.com/nelstrom/vim-visual-star-search

Copyright © 2016, The Pragmatic Bookshelf.

Chapter 14

Substitution


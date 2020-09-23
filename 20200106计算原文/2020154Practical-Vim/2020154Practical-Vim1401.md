In this part of the book, we’ll talk about search, substitute, and global commands. But first, we’ll focus on the core that drives each of them: Vim’s search engine. Have you ever wondered how Vim’s regular expressions work or how to turn them off?

Vim’s regular expression engine may be somewhat different from the one you’re accustomed to using. We’ll see that the most confusing discrepancies can be smoothed out with the very magic pattern switch. Certain characters have a special meaning by default in Vim’s search field, which can complicate matters when we just want to match something verbatim. We’ll learn how to disable all of these special meanings at a stroke, with the very nomagic literal switch.

We’ll focus on a couple of special items that can be used in Vim’s patterns: zero-width delimiters that can mark the boundaries of a word or a search match. We’ll finish with an in-depth discussion of how to deal with the handful of characters that retain special meaning, even when we use the \V literal switch.

Tip 73 Tune the Case Sensitivity of Search Patterns

	 	 	 We can tune the case sensitivity of Vim’s search globally or on a per-search basis.

Setting Case Sensitivity Globally

We can make Vim’s search patterns case insensitive by enabling the ‘ignorecase’ setting:

​=> ​:set ignorecase​

Be aware that this setting has a side effect that influences the behavior of Vim’s keyword autocompletion, as discussed in ​Autocompletion and Case Sensitivity​.

Setting Case Sensitivity per Search

We can override Vim’s default case sensitivity using the \c and \C items. Lowercase \c causes the search pattern to ignore case, while the uppercase \C item forces case sensitivity. If either of these items is used in a search pattern, the value of ‘ignorecase’ is overridden for that search.

Note that these items can be used anywhere in a pattern. If you realize that you need a case sensitive search after you typed out the full pattern, just tack \C on at the end and it will apply to the entire pattern.

Enabling Smarter Default Case Sensitivity

	 	 Vim provides an extra setting that makes an effort to predict our case sensitivity intentions. This is the ‘smartcase’ option. When enabled, ‘smartcase’ has the effect of canceling out the ‘ignorecase’ setting any time that we include an uppercase character in our search pattern. In other words, if our pattern is all lowercase, then the search will be case insensitive. But as soon as we include an uppercase letter, the search becomes case sensitive.

Does that sound complicated? Try it out and you’ll find that it feels quite intuitive. And remember that we can always force case sensitivity or insensitivity for an individual search by including the \C or \c items. The following table illustrates a matrix of case sensitivity options. A similar table can be found in Vim’s built-in documentation by looking up /ignorecaseⓘ.

Pattern

‘ignorecase’

‘smartcase’

Matches

foo

off

-

foo

foo

on

-

foo Foo FOO

foo

on

on

foo Foo FOO

Foo

on

on

Foo

Foo

on

off

foo Foo FOO

\cfoo

-

-

foo Foo FOO

foo\C

-

-

foo

Two Regular Expression Engines

Version 7.4 of Vim introduced a new regular expression engine (see new-regexp-engineⓘ). Whereas the old engine uses a backtracking algorithm, the new engine uses a state machine, which performs better for complex patterns and long text. In turn, this enhancement has improved the performance of all features that use regular expressions, such as syntax highlighting, the search command, and vimgrep.

The new regex engine is enabled by default in Vim 7.4, but the old engine is still available. Some features of Vim’s regular expressions are not supported by the new engine. Vim will automatically use the old engine for a pattern that uses those features. See two-enginesⓘ for more information.

Tip 74 Use the \v Pattern Switch for Regex Searches

	 	 	 	 Vim’s regular expression syntax is closer in style to POSIX than to Perl. For programmers who already know Perl’s regexes, this can be a source of frustration. Using the very magic pattern switch, we can make Vim adopt a more familiar syntax for regular expressions.

Let’s say that we want to compose a regular expression that matches each of the color codes in this snippet of CSS:

patterns/color.css

​ body { color: #3c3c3c; }

​ a { color: #0000EE; }

​ strong { color: #000; }

We need to match a # character followed by either three or six hexadecimal characters. That includes all numeric digits, plus the letters A through F in upper- or lowercase.

Find Hex Colors with Magic Search

	 	 The following regular expression meets these requirements:

​=> ​/#\([0-9a-fA-F]\{6}\|[0-9a-fA-F]\{3}\)​

Try it out if you like. It works ok, but look at all of those backslashes—five in total!

	 	 	 We’re using three types of brackets here. Square brackets have a special meaning by default, so we don’t need to escape them. Parentheses match the ( and ) characters literally, so we have to escape them to make them take on a special meaning. The same goes for curly braces, but get this: we have to escape only the opening member of the pair. We can leave the closing brace unescaped, and Vim will figure out our intentions. This is not the case for parentheses, where both the opening and closing member of the pair must be escaped.

Each of the three bracket types is governed by a different set of rules. Read the previous paragraph again, and commit them to memory. I’ll wait. Tell you what: don’t bother!

Find Hex Colors with Very Magic Search

	 	 We can normalize the rules for all special symbols with the \v pattern switch. This enables very magic search, where all characters assume a special meaning, with the exception of「_」, uppercase and lowercase letters, and the digits 0 through 9 (see \vⓘ).

	 The \v pattern switch makes Vim’s regular expression engine behave much more like that of Perl, Python, or Ruby. There are still differences, which we’ll draw attention to throughout this chapter, but they’re easier to remember than arbitrary rules about what must and must not be escaped.

Let’s rewrite that regular expression for matching hex colors, this time using the \v pattern switch:

​=> ​/\v#([0-9a-fA-F]{6}|[0-9a-fA-F]{3})​

The \v switch at the start causes all subsequent characters to take on a special meaning. It looks much more readable without all of those backslash characters, don’t you think?

Use the Hex Character Class to Further Refine the Pattern

	 	 We can make one further refinement to this pattern: instead of spelling out the character collection [0-9a-fA-F] in full, we can replace it with the character class \x (see /character-classesⓘ). This pattern has exactly the same meaning as the previous one:

​=> ​/\v#(\x{6}|\x{3})​

Discussion

This table presents each of the regular expressions for easy comparison:

PatternRemarks

​ #\([0-9a-fA-F]\{6}\|[0-9a-fA-F]\{3}\)

Using magic search, we have to escape (, ), |, and { characters to confer special meaning upon them.

​ \v#([0-9a-fA-F]{6}|[0-9a-fA-F]{3})

Using the \v pattern switch, the (, ), |, and { characters assume special meaning.

​ \v#(\x{6}|\x{3})

			 We can compact the expression further by using the \x character class, which stands for [0-9A-Fa-f].

	 One final note: # has no special meaning and is matched literally. Remember how very magic search treats all characters as special, except for「_」, letters, and numbers? It looks like we’ve found an exception to this rule!

Vim’s answer is that any characters that do not yet have a special meaning are「reserved for future expansions」(see /\\ⓘ). In other words, just because # has no special meaning today does not mean that will be true for future versions. If # were to take on a special meaning, then we would have to escape it to match the「#」character literally. But don’t let that thought keep you awake at night.

History Lesson: On the Heritage of Vim's Pattern Syntax

	 	 	 	 Vim has two older syntaxes for patterns besides the ones enabled by \v and \V switches. Vim’s default is magic search, while nomagic search emulates the behavior of vi. They can be enabled with the \m and \M switches, respectively.

	 The \M nomagic switch has a similar effect to the \V literal switch, except that a couple of characters automatically take on a special meaning: namely, the ^ and $ symbols.

Magic search automatically assigns a special meaning to a handful of extra symbols, such as the ., *, and square brackets. Magic search was created to make it easier to build simple regexes, but it stopped short of adding special meaning to symbols such as +, ?, parentheses, and braces, each of which must be escaped to assign them with their special meaning.

Magic search goes halfway toward making regular expressions easier to compose. As a result, the rules over what to escape seem haphazard, making them difficult to memorize. The \v pattern search switch fixes this by assigning a special meaning to every symbol except _, numbers, and letters. That’s easily remembered and happens to be consistent with the rules for Perl’s regular expressions.

Tip 75 Use the \V Literal Switch for Verbatim Searches

	 	 	 	 	 	 The special characters used for defining regular expressions are handy when searching for patterns, but they can get in the way if we want to search for text verbatim. Using the verynomagic literal switch, we can cancel out most of the special meanings attached to characters such as ., *, and ?.

Take this excerpt of text:

patterns/excerpt-also-known-as.txt

​ The N key searches backward...

​ ...the \v pattern switch (a.k.a. very magic search)...

Now suppose that we want to jump to the occurrence of「a.k.a.」(which stands for also known as) by searching for it. The most natural thing to do would be to run this search:

​=> ​/a.k.a.​

But when we press Enter, we’ll find that this pattern matches more than we bargained for. The「.」symbol has a special meaning: it matches any character. As chance would have it, the word「backward」contains a fragment that matches our pattern. This table illustrates the outcome.

KeystrokesBuffer Contents

{start}

​ The N key searches backward...

​ ...the \v pattern switch (a.k.a. very magic search)...

/a.k.a.<CR>

​ The N key searches backward...

​ ...the \v pattern switch (a.k.a. very magic search)...

/a\.k\.a\.<CR>

​ The N key searches backward...

​ ...the \v pattern switch (a.k.a. very magic search)...

/\Va.k.a.<CR>

​ The N key searches backward...

​ ...the \v pattern switch (a.k.a. very magic search)...

In this example, the result is merely an irritation. We can jump to the next match—the one we’re aiming for, let’s hope—just by pressing the n key. But in some circumstances, a false positive match could be more insidious. Imagine if we were to go ahead and run a substitute command, such as :%s//also known as/g, without realizing that our search pattern was too broad (leaving the search field of the :substitute command blank tells Vim to use the last search pattern, as discussed in Tip 91). That could lead to some surprising typos!

We can cancel out the special meaning of the . character by escaping it. The following pattern would not match the fragment inside the word backward, but it would still match「a.k.a.」:

​=> ​/a\.k\.a\.​

Alternatively, we could use the \V literal switch to enable very nomagic search:

​=> ​/\Va.k.a.​

As Vim’s documentation says,「use of \V means that in the pattern after it, only the backslash has a special meaning」(see /\Vⓘ). As we’ll see in Tip 79, this is a slight oversimplification, but it will do for the purposes of this discussion.

Creating regular expressions in a very nomagic search is still possible, but it’s awkward because we have to escape every symbol. As a general rule, if you want to search for a regular expression, use the \v pattern switch, and if you want to search for verbatim text, use the \V literal switch.

Tip 76 Use Parentheses to Capture Submatches

	 	 	 	 When specifying a pattern, we can capture submatches and then reference them elsewhere. This feature is especially useful in combination with the substitute command, but it can also be used to define patterns where a word is repeated.

Take this excerpt of text:

patterns/springtime.txt

​ I love Paris in the

​ the springtime.

Can you spot the grammatical error? It’s surprisingly hard to see because of a trick that our mind plays on us, but it should pop out with emphasis:「Paris in the the springtime.」When a line break separates two occurrences of the same word, our brain tends to ignore the duplicate. The effect is called a lexical illusion.[20]

Here’s a regular expression that matches duplicate words:

​=> ​/\v<(\w+)\_s+\1>​

Now try searching for this pattern on the springtime excerpt, and you should see「the the」light up as a search match. Now try joining the two lines together (vipJ will do it), and you should find that it still matches. Best of all, this pattern doesn’t just match「the the,」it works for any pair of duplicate words. Let’s pick the regular expression apart and see how it works.

The trick to matching the same word twice lies in the combination of () and \1. Anything that matches inside of parentheses is automatically assigned to a temporary silo. We can reference the captured text as \1. If our pattern contained more than one set of parentheses, then we could reference the submatch for each pair of () by using \1, \2, and so on, up to \9. The \0 item always refers to the entire match, whether or not parentheses were used in the pattern.

	 	 	 The regular expression for matching lexical illusions contains several other tricks. We’ve already seen in Tip 74, that the \v pattern switch enables very magic search. The < and > symbols match word boundaries, as discussed in Tip 77. Finally, the \_s item matches whitespace or a line break (see /\_ⓘ and 27.8ⓘ, respectively).

There aren’t many scenarios where submatches are useful in a search pattern. One more example springs to mind: matching opening and closing pairs of XML or HTML tags. But as we’ll see in Tip 94, we can also use submatches in the replacement {string} of the :substitute command.

Use Parentheses Without Capturing Their Contents

Sometimes we may want to use parentheses for grouping, while we may have no interest in capturing the submatch. For example, take this pattern, which matches both forms of my name:

​=> ​/\v(And|D)rew Neil​

Here we’re using parentheses to match either「Andrew」or「Drew,」but we’re probably not interested in capturing the「And or D」fragment that is wrapped in parentheses. We can tell Vim not to bother assigning it to the \1 register by prepending a % in front of the parentheses, like this:

​=> ​/\v%(And|D)rew Neil​

What difference does this make? Well, it’s a smidge faster, not that you’re likely to notice. But it can be useful if you find yourself using several sets of parentheses. Suppose we wanted to replace all occurrences of FIRSTNAME LASTNAME with LASTNAME, FIRSTNAME for both forms of my name. We could do so like this:

​=> ​/\v(%(And|D)rew) (Neil)​

​=> ​:%s//\2, \1/g​

The search pattern assigns either「Andrew」or「Drew」to capture register \1 and assigns「Neil」to register \2. If we hadn’t used %() for the second set of parentheses, then it would have captured a fragment of text unnecessarily, cluttering up our replacement field.

Tip 77 Stake the Boundaries of a Word

	 	 	 When defining a pattern, specifying where a word begins and ends can be useful. Vim’s word-delimiter items let us do that.

Some words, especially short ones, have a habit of showing up inside other words. For example,「the」appears inside「these,」「they,」「their,」and many other words besides. So if we search the following excerpt by running /the<CR>, we’ll find more matches than we may have bargained for:

​ the problem with these new recruits is that

​ they don't keep their boots clean.

	 If we specifically want to match「the」as a word rather than a fragment, we can use word boundary delimiters. In very magic searches, these are represented by the < and > symbols. So if we amended our search to /\v<the><CR>, it would find only one match in the excerpt.

	 These are zero-width items, meaning that they don’t match any characters themselves. They represent the boundary between a word and the whitespace or punctuation that surrounds it.

We can approximate the meaning of < and > by combining the \w and \W character classes with the \zs and \ze match delimiters (which we’ll meet in Tip 78). \w matches word characters, including letters, numbers, and the「_」symbol, while \W matches everything except for word characters. Combining these, we could approximate the < item as \W\zs\w, and the > item as \w\ze\W.

	 	In a very magic search, the naked < and > characters are interpreted as word delimiters, but in magic, nomagic, and very nomagic searches we have to escape them. Hence, to look up these items in Vim’s documentation, we must prepend a backslash: /\<ⓘ. Note that if we wanted to match the angle bracket characters literally in a very magic search, we would have to escape them.

Even if we don’t make a habit of using the word boundary items when composing our own search patterns, we use them indirectly each time we trigger the * or # commands (see *ⓘ). These search forward and backward, respectively, for the word under the cursor. If we examine the search history after using either of these commands (by pressing /<Up>), we’ll see that the last search pattern is wrapped with word delimiters. Incidentally, the g* and g# variants perform the same searches without word delimiters.

Tip 78 Stake the Boundaries of a Match

	 	 	 	 Sometimes we might want to specify a broad pattern and then focus on a subset of the match. Vim’s \zs and \ze items allow us to do just that.

Up until now, we’ve assumed a complete overlap between search patterns and the matches they generate. It’s time to pry these apart into two separate concepts. Let’s start by defining them. When we talk of a pattern, we refer to the regular expression (or literal text) that we type into the search field. When we talk of a match, we refer to any text in the document that appears highlighted (assuming the ‘hlsearch’ option is enabled).

The boundaries of a match normally correspond to the start and end of a pattern. But we can use the \zs and \ze items to crop the match, making it a subset of the entire pattern (see /\zsⓘ). The \zs item marks the start of a match, while the \ze item matches the end of a match. Together, they allow us to specify a pattern that entirely matches a range of characters and then zoom in on a subset of the match. Just like the word delimiters (from the previous tip), \zs and \ze are zero-width items.

An example would help at this point. If we searched for /Practical Vim<CR> then any occurrences of「Practical Vim」in our document would light up. If we were to modify the search pattern to /Practical \zsVim<CR>, then only the word「Vim」would be highlighted. The word「Practical」would be excluded from the match, even though it is still part of the pattern. As a result, occurrences of the word「Vim」that directly follow the word「Practical」will be highlighted, but any occurrences of the word「Vim」that do not follow the word「Practical」will not match. The outcome is quite different from simply searching for /Vim<CR>.

Lookaround Expressions

	 	 	 	 Vim’s \zs and \ze are conceptually similar to Perl’s lookaround assertions.[21] Although the syntax differs between the regex engines in Perl and Vim, the \zs item is roughly equivalent to positive lookbehind, while \ze is equivalent to positive lookahead.

As you might expect, Perl also supports negative variants of the lookaround assertions. These are zero-width items that match only if the specified pattern is not present. Vim also supports the full matrix of negative/positive lookahead/lookbehind assertions, but again, the syntax differs from Perl. For a side-by-side comparison, look up perl-patternsⓘ.

Instead of using \zs and \ze, we could rewrite the /\v"\zs[^"]+\ze"<CR> pattern from Tip 78, using Vim’s positive lookaround items, like so:

​=> ​/\v"@<=[^"]+"@=​

I don’t know about you, but I find the version using \zs and \ze easier to parse. Negative lookaround expressions are used heavily in some of Vim’s syntax highlighting definitions, but I’ve found little need for them in everyday usage. However, I’ve found many uses for positive lookaround expressions, so it seems fitting that they should have their own shorthand tokens, namely \zs and \ze.

Here’s another example, this time using both \zs and \ze to tweak the start and end of the match:

KeystrokesBuffer Contents

{start} ​ Match "quoted words"---not quote marks.

/\v"[^"]+"<CR>

​ Match "quoted words"---not quote marks.

/\v"\zs[^"]+\ze"<CR>

​ Match "quoted words"---not quote marks.

The basic pattern uses a common regex idiom: "[^"]+". The pattern begins and ends with a quote mark and then matches one or more characters in between that are anything but a quote. In the final rendition of the pattern, we add the \zs item after the opening quote mark and the \ze item before the closing quote mark. This excludes the quote marks from the match, leaving only the contents of the quotes highlighted. Note that the quote marks are still a critical element in the pattern, even though they are excluded from the match.

Tip 79 Escape Problem Characters

	 	 	 	 The \V literal switch makes it easier to search for text verbatim because it disables the special meanings for the ., +, and * symbols, but there are a few characters whose special meaning can’t be turned off. In this advanced tip, we’ll look at how to handle these.

Escape / Characters When Searching Forward

	 Take this excerpt from a Markdown document:

patterns/search-url.markdown

​ Search items: [http://vimdoc.net/search?q=/\\][s]

​ ...

​ [s]: http://vimdoc.net/search?q=/\\

Suppose that we want to search for all instances of the URL http://vimdoc.net/search?q=/\\. Rather than typing it out in full, we’ll just yank it into a register so that we can paste it into our search field. We want to match this text exactly as is, so we’ll use the \V literal switch.

	 	 	 With our cursor placed anywhere inside the brackets, we can yank the URL into register u with the command "uyi[ (mnemonic: u stands for URL). We then type /\V<C-r>u<CR> to populate the search field with the contents of that same register. Our search prompt looks like this:

​=> ​/\Vhttp://vimdoc.net/search?q=/\\​

When we execute the search, we get this result:

​ Search items: [http://vimdoc.net/search?q=/\\][s]

​ ...

​ [s]: http://vimdoc.net/search?q=/\\

What’s going on here? When we pasted the full URL into the search field, Vim interpreted the first / character as a search field terminator (see ​Search Field Terminators​). Everything after that first forward slash was ignored, so our search string became merely http:.

When searching forward, we have to escape / characters. This is required whether we are doing a very magic search (with the \v pattern switch) or a very nomagic search (with the \V literal switch). Let’s amend the previous search, prefixing each / character with a backslash:

​=> ​/\Vhttp:\/\/vimdoc.net\/search?q=\/\\​

This time, the result is closer to what we would expect:

​ Search items: [http://vimdoc.net/search?q=/\\][s]

​ ...

​ [s]: http://vimdoc.net/search?q=/\\

It’s still not perfect. The match stops short of the final backslash. We’ll find out why soon, but first, let’s consider searching backward.

Escape ? Characters When Searching Backward

	 When searching backward, the ? symbol acts as the search field terminator. That means we don’t have to escape / characters, but instead we have to escape the ? symbol. Watch what happens if we search backward for the URL that we yanked into register u:

​=> ​?http://vimdoc.net/search?q=/\\​

Without escaping anything, Vim matches the string「http://vimdoc.net/search」:

​ Search items: [http://vimdoc.net/search?q=/\\][s]

​ ...

​ [s]: http://vimdoc.net/search?q=/\\

That’s a better result than when we searched forward without escaping anything, but it still doesn’t match the full URL. We can do better if we prepend the ? character with a backslash:

​=> ​?http://vimdoc.net/search\?q=/\\​

That matches the following:

​ Search items: [http://vimdoc.net/search?q=/\\][s]

​ ...

​ [s]: http://vimdoc.net/search?q=/\\

Escape \ Characters Every Time

	 	 There’s one more character that we have to escape in the search field: the backslash. Normally, a \ indicates that the next character is to be given some special treatment. If we double it up as \\, the first backslash cancels out the special meaning of the second one. In effect, we’re telling Vim to search for a single backslash character.

In our example text, we’re searching for a URL that includes two consecutive backslashes. We have to include two backslashes in the search field for each of them. Searching forward, we end up with this:

​=> ​/\Vhttp:\/\/vimdoc.net\/search?q=\/\\\\​

At last! Our search query matches the entire URL:

​ Search items: [http://vimdoc.net/search?q=/\\][s]

​ ...

​ [s]: http://vimdoc.net/search?q=/\\

The backslash character always needs to be escaped, whether we’re searching forward or backward.

Escape Characters Programmatically

	 	 Escaping characters by hand is laborious, error-prone work. Fortunately, Vim script includes a library function that can do the hard work for us: escape({string}, {chars}) (see escape()ⓘ).

The {chars} argument specifies which characters must be escaped with a backslash. If we’re searching forward, we could call escape(@u, ’/\’), which would prefix each / and \ character with a backslash. If we were searching backward, we could instead call escape(@u, ’?\’).

First, make sure that the URL we want to search for is still stored in the u register. Then we’ll bring up the search prompt by pressing / or ?; either one will work just fine. Enter the \V literal switch and then type <C-r>=. That switches from the search prompt to the expression register prompt. Now we type this:

​=> ​=escape(@u, getcmdtype().'\')​

When we press <CR>, the escape() function is evaluated, and the returned value gets inserted into the search field. The getcmdtype() function simply returns a / symbol if we’re searching forward or a ? symbol if we’re searching backward (see getcmdtype()ⓘ). In Vim script, the . operator performs string concatenation, so getcmdtype().’\’ produces ’/\’ if we’re searching forward and ’?\’ if we’re searching backward. The end result is that no matter which way we’re searching, this expression escapes the contents of the u register so that we can find it.

Switching to the expression register and calling the escape() function by hand still involves a lot of typing. With just a little bit more Vim script, we could automate this, making it more convenient to use. Skip ahead to Tip 87, for an example.

Search Field Terminators

You might be wondering why the search field has to treat any character as a terminator. Why not just accept that everything following the search prompt is to be included in the search match? The behavior of Vim’s search command can be tuned by appending certain flags after the search field terminator. For example, if we run the command /vim/e<CR>, then our cursor will be placed at the end of any matches rather than at the start. In Tip 83, we’ll learn how to exploit this feature rather than let it exploit us.

There is one way of entering a pattern without having to worry about search field terminators, but it works only in GVim: use the :promptfind command (see :promptfindⓘ). This brings up a graphical dialog window with a field labeled「Find.」You can enter the / and ? characters here without having to escape them. However, the \ and newline characters still cause problems.

Footnotes

[20]

http://matt.might.net/articles/shell-scripts-for-passive-voice-weasel-words-duplicates/

[21]

http://www.regular-expressions.info/lookaround.html

Copyright © 2016, The Pragmatic Bookshelf.

Chapter 13

Search


Autocompletion saves us from typing out entire words. Given the first letters of a word, Vim builds a list of suggested endings and lets us choose our favorite. Whether or not this is of any use to us depends on how adept we are at interacting with that list of suggestions. We’ll learn a few tricks for working with the autocomplete menu in Tip 113.

Tip 112, introduces the basics of keyword autocompletion. The list of suggested completions is created by scanning all files that have been opened in the current editing session, as well as any included files and tag files. We’ll find out what this means in Tip 114, and see how we can narrow down the list of suggestions.

Besides keywords, Vim has other ways of building a list of suggestions. ​​, lists some of the highlights, each of which is covered by a tip in this chapter.

To make the most of Vim’s autocomplete functionality, we need to understand two things: how to dial up the most relevant suggestions and how to choose the right word from the list. We’ll address each of these topics in the following tips.

Autocompletion and Case Sensitivity

Vim’s search command treats uppercase and lowercase letters as equivalent when the ‘ignorecase’ option is enabled (as discussed in Tip 73), but there’s a side effect: autocompletion also becomes case insensitive.

In the「She sells sea shells」example above, the word「She」is not included in the word list because it starts with an uppercase「S.」However, if the ‘ignorecase’ option were enabled, then「She」would appear in the word list with an uppercase「S.」Seeing as we’ve already typed a lowercase「s,」this might be considered unhelpful.

We can fix this behavior by enabling the ‘infercase’ option (see 'infercase'ⓘ). This would add「she」to the word list but with a lowercase「s.」

Tip 112 Meet Vim’s Keyword Autocompletion

	 	 With keyword autocompletion, Vim attempts to guess the word that we’re typing, which can save us from completing it by hand.

	 Vim’s autocomplete functionality is triggered from Insert mode. When invoked, Vim builds a word list from the contents of each buffer in the current editing session and then examines the characters to the left of the cursor, looking for a partial word. If one is found, the word list is filtered to exclude anything that doesn’t begin with that partial word. The resulting word list is presented in a menu from which we can select our match.

This figure shows two screenshots, one taken before and one after triggering Vim’s keyword autocompletion:

In this case, the letter「s」is used to filter the word list, giving us three choices:「sells,」「sea,」and「shells.」If you’re wondering why「She」isn’t in the list, see ​Autocompletion and Case Sensitivity​.

Trigger Autocompletion

	 	 	 	 Vim’s autocompletion can be triggered from Insert mode with the <C-p> and <C-n> chords, which select the previous and next items in the word list, respectively.

The <C-p> and <C-n> commands both invoke generic keyword autocompletion. There are several variant forms of autocompletion, all of which are prefixed with the <C-x> chord. In this chapter, we’ll discuss the methods listed in the following table (you can view the complete list at ins-completionⓘ).

CommandType of Completion

<C-n>

Generic keywords

<C-x><C-n>

Current buffer keywords

<C-x><C-i>

Included file keywords

<C-x><C-]>

tags file keywords

<C-x><C-k>

Dictionary lookup

<C-x><C-l>

Whole line completion

<C-x><C-f>

Filename completion

<C-x><C-o>

Omni-completion

If you use <C-x><C-n> on the「She sells sea shells」example, then you should get the same word list as is shown in the illustration. But <C-n> may produce more suggestions, because the word list is populated from sources beyond the current buffer. We’ll take an in-depth look at how the word list for generic keywords is populated in Tip 114.

No matter which form of autocompletion is triggered, the commands for interacting with the suggestions menu are the same. We’ll explore these in the next tip.

Tip 113 Work with the Autocomplete Pop-Up Menu

	 	 	 	 To get the most from the autocomplete command, learn how to interact with the pop-up menu. Either refine the choices and then pick an item, or dismiss the list if it doesn’t contain what you want.

When autocomplete is triggered, Vim draws a pop-up menu containing the items in the word list. We can interact with this menu using the commands shown in Table 18, ​Commands for the Pop-Up Menu​.

* * *

Table 18. Commands for the Pop-Up Menu

KeystrokesEffect

<C-n>

Use the next match from the word list (next match)

<C-p>

Use the previous match from the word list (previous match)

<Down>

Select the next match from the word list

<Up>

Select the previous match from the word list

<C-y>

Accept the currently selected match (yes)

<C-e>

Revert to the originally typed text (exit from autocompletion)

<C-h> (and <BS>)

Delete one character from current match

<C-l>

Add one character from current match

{char}

Stop completion and insert {char}

* * *

More details can be found in Vim’s documentation: popupmenu-completionⓘ.

No matter which variant of autocompletion is used, when the autocomplete pop-up menu is visible, <C-n> and <C-p> always move to the previous or next item in the menu. In contrast, when used from Insert mode, <C-n> and <C-p> trigger generic keyword autocompletion.

The <C-n> and <Down> keys both select the next item from the pop-up menu, while the <C-p> and <Up> keys select the previous item. The mechanics are slightly different, whether we use <C-p>/<C-n> or <Up>/<Down>.

Browse the Word List Without Changing the Document

	 When we press <Down>, the pop-up menu is updated to select the next item in the list but the text in the document is left unchanged. We can scroll through the list of words in the pop-up menu using the <Up> and <Down> keys until we find the word we want to use. Then we can insert it into the document either by hitting the <CR> key or by pressing <C-y>.

Update the Document As You Scroll Through the Word List

	 	 By contrast, the <C-n> key not only selects the next item from the list, it also updates the document to use the selected word. This means that we don’t have to press <CR> to confirm our selection, because the text in the document is always synchronized with the selected item in the pop-up menu. Once we’ve chosen our word from the list, we simply continue typing and the pop-up menu disappears.

I prefer the <C-p> and <C-n> chords over <Up> and <Down> for a couple of reasons. I don’t have to move my hand from the home row when using <C-p> and <C-n>. Also, I don’t have to confirm my choice by pressing <CR> or <C-y> because the text is inserted into the document automatically. Once again, we meet our mantra from Tip 47: keep your fingers on the home row.

Dismiss All Selections

Once we’ve summoned the autocomplete menu, we might want to dismiss it again. For instance, if the list has too many suggestions, typing out the word by hand may prove quicker. We can end autocompletion by pressing <C-e>, which dismisses the pop-up menu and restores the text in front of the cursor to the partial word that was typed before autocomplete was invoked.

Refine the Word List as You Type

Here’s one of my favorite tricks when working with the autocomplete pop-up menu. Try pressing <C-n><C-p>. That’s two separate commands: <C-n> followed immediately by <C-p> (although <C-p><C-n> would work just as well). The first command invokes autocomplete, summons the pop-up menu, and selects the first item in the word list. The second command selects the previous item in the word list, taking us back to where we started but without dismissing the pop-up menu. Now we can continue to type, and Vim will filter the word list in real time.

This can be especially handy if the word list contains too many suggestions to read in one visual gulp. Suppose that the word list contains twenty suggestions and we typed only a partial word consisting of two characters. If we type a third character, the word list will be immediately refined. We can continue typing characters in this manner until the word list is short enough to be useful and we can make our selection.

This trick works just as well with the other variants of autocompletion. For example, we could type <C-x><C-o><C-p> to perform live filtering on omni autocompletion, or <C-x><C-f><C-p> to do the same with filename completion.

Tip 114 Understand the Source of Keywords

	 	 	 Generic keyword autocompletion compiles its word list from a handful of sources. We can be more specific about which sources we want to use.

Several forms of autocompletion use a specific file or set of files to generate their word list. Generic keyword autocompletion uses an amalgamation of these word lists. To understand where generic keywords come from, we should first look at each of the more targeted forms of autocompletion.

The Buffer List

	 The simplest mechanism for populating the autocomplete word list would be to use words only from the current buffer. Current file keyword completion does just that and is triggered with <C-x><C-n> (see compl-currentⓘ). This can be useful when generic keyword completion generates too many suggestions and you know that the word you want is somewhere in the current buffer.

But current buffer keyword completion has little to offer when the current buffer has a low word count. To augment the word list, we can have Vim source keywords from each item in the buffer list. We can inspect these by running this command:

​=> ​:ls!​

Generic keywords are sourced from the contents of each file in this list, which represents all of the files that have been opened in the current Vim session. As we’ll see next, we needn’t even open a file for its contents to be pulled into the autocomplete word list.

Included Files

	 Most programming languages provide some way of loading code from an external file or library. In C, this can be done using the #include directive, whereas Python uses import and Ruby uses require. If we are working on a file that includes code from another library, then it would be useful if Vim could read the contents of those referenced files when building a word list for autocompletion. And that is exactly what happens when we trigger keyword completion with the <C-x><C-i> command (see compl-keywordⓘ).

	 Vim understands the C way of including files, but it can be taught to follow the corresponding directives in other languages by tweaking the ‘include’ setting (see 'include'ⓘ). This is usually handled by a file-type plugin. And the good news is that Vim is distributed with support for many languages, so you shouldn’t have to tinker with this setting unless you are working with an unsupported language. Try opening a Ruby or Python file and running :set include?, and you should find that Vim already knows how to look up included files for those languages.

Tag Files

	 In Chapter 16, ​Index and Navigate

Source Code with ctags​, we met Exuberant Ctags, which is an external program that scans source code for keywords such as function names, class names, and any other constructs that are significant in the given language. When ctags is run on a codebase, it generates an index of keywords, which are addressed and sorted alphabetically. By convention, the index is saved in a file called tags.

The main reason for indexing a codebase with ctags is to make it easier to navigate, but a tags file creates a useful by-product: a list of keywords that can be used for autocompletion. We can dial up this list using the <C-x><C-]> command (see compl-tagⓘ).

If the word you are trying to complete is a language object (such as a function name or class name), then tag autocompletion will give a good signal-to-noise ratio.

Put It All Together

Generic keyword autocompletion generates suggestions by combining the word list generated from the buffer list, included files, and tag files into one. If you want to tweak this behavior, see ​Customizing the Generic Autocompletion​. Remember, generic keyword autocompletion is triggered simply with the <C-n> chord, whereas the more focused variants are all invoked with <C-x> followed by another chord.

Customizing the Generic Autocompletion

We can customize the list of places that are scanned by generic keyword completion using the ‘complete’ option. This option holds a comma-separated list of one-letter flags, whose presence enables scanning of a particular place. The default setting is complete=.,w,b,u,t,i. We could disable scanning of included files by running the following:

​=> ​:set complete-=i​

Or we could enable completion of words in the spelling dictionary by running this:

​=> ​:set complete+=k​

Look up 'complete'ⓘ to find out what each of the flags does.

Tip 115 Autocomplete Words from the Dictionary

	 	 	 	 Vim’s dictionary autocompletion builds a list of suggestions from a word list. We can configure Vim so that dictionary autocompletion uses the same word list as the built-in spell checker.

Sometimes we might want to use autocompletion on a word that isn’t present in any of our open buffers, included files, or tags. In that case, we can always resort to looking it up in the dictionary. This can be triggered by running the <C-x><C-k> command (see compl-dictionaryⓘ).

	 To enable this feature, we need to supply Vim with a suitable word list. The easiest way to do this is by running :set spell to enable Vim’s spell checker (see Chapter 20, ​Find and Fix Typos with Vim’s Spell Checker​, for more details). All of the words in the spelling dictionary become available through the <C-x><C-k> command.

If you don’t want to enable Vim’s spell checker, you can also use the ‘dictionary’ option to specify one or more files containing word lists (see 'dictionary'ⓘ).

Dictionary autocompletion is perhaps most useful when you want to complete a word that is long or difficult to spell. Here’s an example:

There’s one other form of autocompletion that uses the spelling dictionary. We’ll find out how to use it in Tip 123.

Tip 116 Autocomplete Entire Lines

	 	 	 	 In all of the examples so far, we’ve looked at completing words, but Vim can also autocomplete entire lines.

Line-wise autocompletion is triggered by running <C-x><C-l> (see compl-whole-lineⓘ). Suppose that we started off with this snippet:

auto_complete/bg-colors.css

​ .top {

​ background-color: #ef66ef; }

​ .bottom {

We want to duplicate the second line and place it at the end of the file. Here’s how this can be done using whole-line autocompletion:

KeystrokesBuffer Contents

{start}

​ .top {

​ background-color: #ef66ef; }

​ .bottom {

oba

​ .top {

​ background-color: #ef66ef; }

​ .bottom {

​ ba

<C-x><C-l><Esc>

​ .top {

​ background-color: #ef66ef; }

​ .bottom {

​ background-color: #ef66ef; }

The same files that provide the source for generic keyword autocompletion (see Tip 114) are also used to generate a list of suggestions for line-wise autocompletion. Also, note that Vim ignores any indentation at the start of the line.

The beauty of line-wise autocompletion is that we don’t have to know the location of the line we’re duplicating. We need to know only that it exists. After typing out the first few characters, we hit <C-x><C-l>, and bang! Vim fills out the rest for us.

We’ve seen two other methods for duplicating a line by means of a register (​Duplicating Lines​) or an Ex command (​Duplicate Lines with the ‘:t’ Command​). Each has its strengths and its weaknesses. Try to identify the scenarios where each of these techniques shines, and use them accordingly.

Tip 117 Autocomplete Sequences of Words

When we use autocomplete to expand a word, Vim remembers the context from which that word was taken. If we invoke autocomplete a second time, Vim will insert the word that followed the original completion. We can repeat this again and again to fill in entire sequences of words. This can often produce results faster than using copy and paste to duplicate phrases.

Suppose that we’re working on this document:

auto_complete/help-refs.xml

​ Here's the "hyperlink" for the Vim tutor:

​ <vimref href=​"http://vimhelp.appspot.com/usr_01.txt.html#tutor"​>tutor</vimref>.

​

​ For more information on autocompletion see:

​ <vimr

The <vimref> tag is a custom element that I use throughout the XML manuscript for this book to mark up links to Vim’s :help pages. We want to insert a <vimref> tag on the last line of this document for the ins-completionⓘ entry in Vim’s documentation. The tag will look just like the existing <vimref> entry, except that instead of usr_01 we want insert, and instead of tutor we want ins-completion.

We can get the result we want quickly by duplicating the existing <vimref> tag and altering the parts that need to change. We could move our cursor to the existing <vimref> tag, yank it, then move back to where we want to insert a new tag and paste the text that we yanked. That wouldn’t be too much hassle in this case, because the document we are working on is so short. But if we were working on a document containing thousands of words, finding an instance of <vimref> to yank could mean moving the cursor a long way from where we want it.

Alternatively, we could use Vim’s autocompletion to insert a copy of the <vimref> tag right where we want it:

KeystrokesBuffer Contents

{start}

​ <vimr

a<C-x><C-p>

​ <vimref

<C-x><C-p>

​ <vimref>.

<C-p>

​ <vimref href

<C-x><C-p>

​ <vimref href="http

<C-x><C-p>

​ <vimref href="http://vimhelp

We start by pressing a to switch into Insert mode. Now we can use <C-x><C-p> to autocomplete the partial word vimr to vimref. (We could just as well use <C-x><C-n> throughout this example.)

It gets interesting when we use <C-x><C-p> a second time. Vim remembers the context from where in the document it found the completion for vimref. When we invoke the autocomplete command again, Vim completes the next word that followed vimref. In this case there are two possible options, because the word vimref appears as an opening tag and a closing tag. Vim pops up the completion menu, prompting us to choose which context we want to use for our completion. Pressing <C-p> a second time gets us the result we want.

Now we can continue pressing <C-x><C-p> again and again. Each time we invoke this command, Vim inserts the next word that it finds in the context where the original autocomplete match came from. It doesn’t take long to fill out the rest of the XML tag. After we’ve done this, we can edit the tag by hand, changing usr_01 to insert, and tutor to ins-completion.

	 Vim’s autocompletion doesn’t only let us insert sequences of words. It also works for sequences of lines. If we repeatedly use the <C-x><C-l> command (which we met in Tip 116​Autocomplete Entire Lines​), it lets us insert a sequence of consecutive lines from elsewhere in our document.

Being able to autocomplete sequences of words and lines can often let us duplicate text more quickly than using copy and paste. When your coworkers see you using this technique, they’ll stop you to ask how you did it!

Tip 118 Autocomplete Filenames

	 	 	 When we work at the command line, we can hit the <Tab> key to autocomplete paths for directories and files. With filename autocompletion, we can do the same from within Vim.

Filename autocompletion is triggered by the <C-x><C-f> command (see compl-filenameⓘ).

	 	 	 	 Vim always maintains a reference to the current working directory, just like the shell. We can find out what this is at any given time by running the :pwd command (print working directory), and we can change our working directory at any time using the :cd {path} command (change directory). It’s important to understand that Vim’s filename autocompletion always expands paths relative to the working directory, not relative to the file that is currently being edited.

Suppose that we were working on a small web application comprised of the following files:

​ webapp/

​ public/

​ index.html

​ js/

​ application.js

Now let’s say that we were editing the index.html file:

auto_complete/webapp/public/index.html

​ ​<!DOCTYPE html>​

​ <html>

​ <head>

​ <title>Practical Vim - the app</title>

​ <script src=​""​ type=​"text/javascript"​></script>

​ </head>

​ <body></body>

​ </html>

We want to fill out the src="" attribute to refer to the application.js file. But there’s a complication if we want to use filename autocompletion:

​=> ​:pwd​

​<= webapp

If we were to invoke filename autocompletion now, it would complete the path relative to the webapp directory, giving us src="public/js/application.js". But we actually want it to reference src="js/application.js". If we want to use filename autocompletion, we’ll first have to change to the public directory:

​=> ​:cd public​

Now we can invoke filename autocompletion, and it will work relative to the webapp/public directory:

KeystrokesBuffer Contents

i

​ <script src=""/>

js/ap

​ <script src="js/ap"/>

<C-x><C-f>

​ <script src="js/application.js"/>

Having inserted the filepath, we can revert back to our original working directory:

​=> ​:cd -​

Just like in the shell, cd - switches to the previous working directory (see :cd-ⓘ).

In the documentation for filename autocompletion, it states that「the ‘path’ option is not used (yet).」Perhaps in future versions of Vim it won’t be necessary to change directories to use this feature for our hypothetical web app scenario.

Tip 119 Autocomplete with Context Awareness

	 	 	 	 Omni-completion is Vim’s answer to intellisense. It provides a list of suggestions that’s tailored for the context of the cursor position. In this tip, we’ll look at how it works in the context of a CSS file.

Omni-completion is triggered with the <C-x><C-o> command (see compl-omniⓘ). The functionality is implemented as a file-type plugin, so to activate it we have to source these lines of configuration:

essential.vim

​ ​set​ nocompatible

​ ​filetype​ plugin ​on​

We also have to install a plugin that implements omni-completion for the language that we’re working with. Vim ships with support for about a dozen languages, including HTML, CSS, JavaScript, PHP, and SQL. You can find the full list by looking up compl-omni-filetypesⓘ.

	 Here’s the results of triggering omni-completion in a CSS file in two slightly different contexts.

Given「ba」as a fragment of a CSS property, it shows a list of completions, including background, background-attachment, and a few others. In this example, background-color is selected. The second time that omni-completion is triggered, no fragment of text is provided, but Vim can tell from the context that a color is expected, so it offers three suggestions: #, rgb(, and transparent.

The relatively static nature of CSS makes it well suited to omni-completion, but if you try out the feature with a programming language, your mileage may vary. If you’re unsatisfied with the support for a particular language, shop around for an alternative plugin or write your own. To figure out how to write omni-completion plugins, start with complete-functionsⓘ.

Copyright © 2016, The Pragmatic Bookshelf.

Chapter 20

Find and Fix Typos with Vim’s Spell Checker


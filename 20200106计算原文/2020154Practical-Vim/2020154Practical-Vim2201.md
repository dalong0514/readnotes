Vim’s spell checker makes it easy to find and correct spelling mistakes. In Tip 120, we’ll find out how to operate the spell checker from Normal mode, and in Tip 123, we’ll learn that it can also be operated from Insert mode.

Vim usually ships with a spell file for the English language only, but it’s easy to install others. Also, as we’ll see in Tip 121, we can switch between American and British English (beside others). And if a word is incorrectly marked as misspelled, adding it to a spell file is a simple matter, as we’ll see in Tip 122.

Tip 120 Spell Check Your Work

With the spell checker enabled, Vim flags words that are not in its spell file. We can quickly jump between spelling mistakes and have Vim suggest corrections.

Take this excerpt of text:

spell_check/yoru-moustache.txt

​ Yoru mum has a moustache.

The first word has clearly been misspelled. We can make Vim highlight it as such by enabling the built-in spell checker:

​=> ​:set spell​

	 	 The word「Yoru」should now be flagged with the SpellBad syntax highlighting. Typically, that means the word will be underlined with a red dashed line, but how it looks will depend on which color scheme you use.

By default, Vim checks spellings against a dictionary of English words. We’ll see how to customize this in Tip 121, but for now we’ll make do with the defaults.

Operate Vim’s Spell Checker

	 	 	 	 We can jump backward and forward between flagged words with the [s and ]s commands, respectively (see ]sⓘ). With our cursor positioned on a misspelled word, we can ask Vim for a list of suggested corrections by invoking the z= command (see z=ⓘ). This figure shows two screenshots taken before and after triggering the z= command:

We can replace the misspelled word with「Your」by pressing 1<CR>. If the list doesn’t contain what we’re looking for, we can dismiss it by pressing <Esc>.

We can skip the prompt altogether by prefixing the z= command with a count, which instructs Vim to use the numbered suggestion. If we’re confident that the first suggestion will be correct, we can run 1z= to fix it in one go.

When writing, I prefer to separate the composition and spell-checking processes into separate tasks. I’ll often disable the spell checker while I write to avoid being nagged each time I make a mistake. Then I’ll make a final pass through the document with the spell checker enabled, fixing the typos it flags.

	 Here are the essential Normal mode spell checker commands.

CommandEffect

]s

Jump to next spelling error

[s

Jump to previous spelling error

z=

Suggest corrections for current word

zg

Add current word to spell file

zw

Remove current word from spell file

zug

Revert zg or zw command for current word

We’ll meet the zg, zw, and zug commands in Tip 122.

Tip 121 Use Alternate Spelling Dictionaries

	 	 	 Out of the box, Vim’s spell checker supports regional variations of English. Find out how to specify the region and how to obtain spelling dictionaries for other languages.

	 When we enable Vim’s spell checker, it compares words against an English dictionary by default. We can change this by tweaking the ‘spelllang’ option (see 'spelllang'ⓘ). This isn’t a global setting; ‘spelllang’ is always local to the buffer. That means it’s possible to work simultaneously on two or more documents and use a different spell file for each—handy if you’re bilingual.

Specify a Regional Variant of a Language

	 Vim’s spell file supports several regional variations of English. The default spelllang=en setting will permit a word whose spelling is acceptable in any English-speaking region. No matter whether we write「moustache」(using the British spelling) or「mustache」(the American way), Vim’s spell checker will let it pass.

We can tell Vim to permit only American spellings:

​=> ​:set spell​

​=> ​:set spelllang=en_us​

With this setting,「moustache」would be flagged as a misspelling, but「mustache」would be permitted. Other supported regions include en_au, en_ca, en_gb, and en_nz. See spell-remarksⓘ for more details.

Obtain Spell Files for Other Languages

Vim ships with a spell file for the English language, but spell files are available for dozens of other languages at this URL: http://ftp.vim.org/vim/runtime/spell/.

If we try to enable a spell file that isn’t available on our system, Vim offers to fetch and install it for us:

​=> ​:set spell​

​=> ​:set spelllang=fr​

​<= Cannot find spell file for "fr" in utf-8

​ Do you want me to try downloading it?

​ (Y)es, [N]o:

​=> ​Y​

​<= Downloading fr.utf-8.spl

​ In which directory do you want to write the file:

​ 1. /Users/drew/.vim/spell

​ 2. /Applications/MacVim.app/Contents/Resources/vim/runtime/spell

​ [C]ancel, (1), (2):

	 This functionality is provided by a plugin called spellfile.vim, which ships with Vim (see spellfile.vimⓘ). To make it work, you need to have these two lines in your vimrc (at the very least):

​ ​set​ nocompatible

​ plugin ​on​

Tip 122 Add Words to the Spell File

	 	 	 Vim’s spelling dictionaries are not comprehensive, but we can augment them by adding words to a spell file.

	 Sometimes Vim will incorrectly mark something as misspelled because the word doesn’t appear in the dictionary. We can teach Vim to recognize words with the zg command (zgⓘ), which adds the word under the cursor to a spell file.

	 Vim also provides a complementary zw command, which marks the word under the cursor as a misspelled word. In effect, this command allows us to remove words from the spell file. If we were to trigger the zg or zw command unintentionally, we could end up adding or removing words from our spell file by accident. Vim provides a dedicated undo command for just such an occasion, zug, which reverts the zg or zw command for the word under the cursor.

	 	Vim records words added to the dictionary in a spell file so that they persist from one session to another. The name of the spell file is derived from the language and file encoding.

For example, if we were working with a UTF-8 encoded file and the spell checker was using an English dictionary, any words added with the zg command would be recorded in a file called ~/.vim/spell/en.utf-8.add.

Create a Spell File for Specialist Jargon

	 	 With the ‘spellfile’ option, we can specify the path of the file where Vim tracks words added or removed using the zg and zw commands (see 'spellfile'ⓘ). Vim allows us to specify more than one spell file simultaneously, which means we can maintain multiple word lists.

This book contains many strings of text that don’t count as words in English, including Vim commands (such as ciw) and settings (such as ‘spelllang’). I don’t want Vim to keep flagging these as misspelled, but neither do I want to tell Vim to consider them as valid English words. As a compromise, I maintain a separate word list of Vim terminology. I can load this as a spell file any time that I’m writing about Vim.

When I’m ready to check the spelling in a chapter of this book, I source a file containing these lines of configuration:

spell_check/spellfile.vim

​ ​setlocal​ spelllang=en_us

​ ​setlocal​ spellfile=~​/.vim/​​spell​/​en​.utf-8.add

​ ​setlocal​ spellfile+=~​/books/​practical_vim/jargon.utf-8.add

~/.vim/spell/en.utf-8.add is the default path, where Vim saves words added with the zg command. The ~/books/practical_vim/jargon.utf-8.add path points to a file within the repository for my book, where I keep a list of Vim terminology.

For each word that the spell checker flags incorrectly, I now have a choice. I could press 2zg to add it to my list of Vim terminology, or 1zg to add it to the default word list.

Tip 123 Fix Spelling Errors from Insert Mode

	 	 	 	 	 Vim’s spelling autocompletion allows us to fix typos without even having to leave Insert mode.

Picture this: we’ve just typed a line of text, and then we realize that there’s a spelling mistake a few words back. What can we do?

Preparation

This technique depends on having the spell checker enabled:

​=> ​:set spell​

The Usual Way: Switch to Normal Mode

To fix the mistake, we could switch to Normal mode, use the [s command to jump back to the spelling mistake, and then use 1z= to fix it. Having made the correction, we could then switch back to Insert mode with the A command, continuing where we left off.

The Fast Way: Use Spelling Autocompletion

Alternatively, we could fix the error from Insert mode using the <C-x>s command, which triggers a special form of autocompletion (see compl-spellingⓘ). We could just as well use <C-x><C-s>, which is slightly easier to type. In this figure, we see screenshots taken before and after triggering the <C-x>s command. Note that we’re in Insert mode throughout:

The autocomplete word list contains the same suggestions as we saw in Tip 120, when we used the z= command.

When we trigger an autocomplete command, Vim usually offers suggestions on how to complete the word at the current cursor position. But in the case of <C-x>s, Vim scans backward from the cursor position, stopping when it finds a misspelled word. It then builds a word list from suggested corrections and presents them in an autocomplete pop-up menu. We can choose a result using any of the techniques described in Tip 113.

	 The <C-x>s command really comes into its own when a line contains more than one misspelled word. Using the same example as in the previous figure, if we were to run :set spelllang=en_us, then the word「moustache」would also be marked as misspelled. Starting off in Insert mode with our cursor at the end of the line, we could fix both mistakes just by typing <C-x>s twice. Try it yourself. It’s neat!

Copyright © 2016, The Pragmatic Bookshelf.

Chapter 21

Now What?

Congratulations—you’ve reached the end of Practical Vim! Now what?

Keep Practicing!


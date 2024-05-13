Vim’s search command is great for finding all occurrences of a pattern within a file. But what if we want to find matches across an entire project? Then we have to scan many files. Traditionally, this has been the domain of grep, a dedicated Unix tool.

In this chapter, we’ll discover Vim’s :grep command, which allows us to call an external program without leaving our editor. While this command calls grep by default (when available), we’ll see that it can easily be customized to outsource the task to other dedicated programs, such as ack.

One down side to using external programs is that their regex syntax may be incompatible with the one we use for most Vim searches. We’ll see that the :vimgrep command allows us to use Vim’s native search engine to find patterns in multiple files. This convenience comes at a cost: vimgrep isn’t nearly as fast as dedicated programs.

Tip 109 Call grep Without Leaving Vim

	 	 	 Vim’s :grep command acts as a wrapper to an external grep (or grep-like) program. Using this wrapper, we can have grep search for a pattern across multiple files without leaving Vim, and then we can navigate the results using the quickfix list.

First we’ll step through a workflow where grep and Vim run independently without talking to each other. We’ll examine the weaknesses with this approach before considering an integrated solution that solves these problems.

Using grep from the Command Line

	 	 Suppose that we’re working on something in Vim and we need to find every occurrence of the word「Waldo」in all files in the current directory. Leaving Vim, we run the following in the shell:

​=> ​$ grep -n Waldo *​

​<= department-store.txt:1:Waldo is beside the boot counter.

​ goldrush.txt:6:Waldo is studying his clipboard.

​ goldrush.txt:9:The penny farthing is 10 paces ahead of Waldo.

By default, grep prints one line of output for each match, displaying the contents of the matching line and the name of the file. The -n flag tells grep to include the line number in the printed output.

So what can we do with this output? Well, we could just treat it as a table of contents. For each line in the result list, we could open the file and specify the line number. For example, to open goldrush.txt at line 9, we could run this from the shell:

​=> ​$ vim goldrush.txt +9​

Surely our tools can integrate better than this.

Calling grep from Inside Vim

Vim’s :grep command is a wrapper for the external grep program (see :grepⓘ). Instead of running grep in the shell, we could execute this directly from Vim:

​=> ​:grep Waldo *​

Behind the scenes, Vim executes grep -n Waldo * in the shell for us. Rather than printing grep’s output, Vim does something much more useful. It parses the results and builds a quickfix list from them. We can navigate through the results using the :cnext/:cprev commands and all of the other techniques that we explored in Chapter 17, ​Compile Code and Navigate Errors

with the Quickfix List​.

Even though we simply called :grep Waldo *, Vim automatically included the -n flag, telling grep to include line numbers in the output. That’s why when we navigate through the quickfix list, it takes us directly to each matching line.

	 	 Suppose we want to run a case-insensitive grep. We supply grep with the -i flag:

​=> ​:grep -i Waldo *​

Behind the scenes, Vim executes grep -n -i Waldo *. Note that the default -n flag is still present. We can pass along any other flags to grep in the same manner if we want to tweak its behavior.

Tip 110 Customize the grep Program

	 	 Vim’s :grep command is a wrapper for the external grep program. We can customize the way that Vim delegates this task by manipulating two settings: ‘grepprg’ and ‘grepformat’. First we’ll examine the defaults, and then we’ll see how tweaking them allows us to outsource the search task to any other suitable program.

Vim’s Default grep Settings

	 	 	 The ‘grepprg’ setting specifies what to run in the shell when Vim’s :grep command is executed ('grepprg'ⓘ). The ‘grepformat’ setting tells Vim how to parse the output returned by the :grep command (see 'grepformat'ⓘ). On Unix systems, the defaults are these:

​ grepprg=​"grep -n $* /dev/null"​

​ grepformat=​"%f:%l:%m,%f:%l%m,%f %l%m"​

The $* symbol used in the ‘grepprg’ setting is a placeholder, which is replaced with any arguments supplied to the :grep command.

The ‘grepformat’ setting is a string containing tokens that describe the output returned by :grep. The special tokens used in the ‘grepformat’ string are the same as those used by ‘errorformat’, which we met in ​Populate the Quickfix List Using Nodelint’s Output​. For the complete list, look up errorformatⓘ.

Let’s see how the default %f:%l %m format stacks up against this output from grep:

​ department-store.txt:1:Waldo is beside the boot counter.

​ goldrush.txt:6:Waldo is studying his clipboard.

​ goldrush.txt:9:The penny farthing is 10 paces ahead of Waldo.

For each record, %f matches the filename (department-store.txt or goldrush.txt), %l matches the line number, and %m matches the text on that line.

The ‘grepformat’ string can contain multiple formats separated by commas. The default matches either %f:%l %m or %f %l%m. Vim will use the first format that matches the output from :grep.

Make ‘:grep’ Call ack

	 	 ack is a grep alternative that is targeted specifically at programmers. If you’re wondering how it compares to grep, visit the home page (and be sure to read the URL, http://betterthangrep.com).

First, we need to install ack. On Ubuntu, we can do so as follows:

​=> ​$ sudo apt-get install ack-grep​

​=> ​$ sudo ln -s /usr/bin/ack-grep /usr/local/bin/ack​

The first of these commands installs the program, allowing us to call it as ack-grep. The second command creates a symlink so that we can call it simply as ack.

	 	 On OS X, we can install ack using Homebrew:

​=> ​$ brew install ack​

Let’s see how we could customize the ‘grepprg’ and ‘grepformat’ settings so that :grep calls ack instead. By default, ack lists the filename on a line of its own, followed by the line number and contents of each matched line, like this:

​=> ​$ ack Waldo *​

​<= department-store.txt

​ 1:Waldo is beside the boot counter.

​

​ goldrush.txt

​ 6:Waldo is studying his clipboard.

​ 9:The penny farthing is 10 paces ahead of Waldo.

We can easily massage this output so that it resembles that of grep -n by running ack with the --nogroup switch:

​=> ​$ ack --nogroup Waldo *​

​<= department-store.txt:1:Waldo is beside the boot counter.

​ goldrush.txt:6:Waldo is studying his clipboard.

​ goldrush.txt:9:The penny farthing is 10 paces ahead of Waldo.

This output matches the format of grep -n, and since Vim’s default ‘grepformat’ string knows how to parse this, we don’t need to change it. So the simplest thing we could do to use ack instead of grep would be to set ‘grepprg’ as follows:

​=> ​:set grepprg=ack\ --nogroup\ $*​

Alternative grep Plugins

Outsourcing a multiple-file search to an external program is easy with Vim. We have only to change the ‘grepprg’ and ‘grepformat’ settings and then execute :grep. And just like that, our results are in the quickfix list. No matter which program is actually called, the interface is nearly identical.

But there are some important differences. grep uses POSIX regular expressions, whereas ack uses Perl regular expressions. If the :grep command calls ack in the background, a layer of misdirection is added. Wouldn’t you rather create a custom command called :Ack that does what it says on the label?

The Ack.vim plugin follows this strategy and so does fugitive.vim,[30] which adds a custom :Ggrep command that executes git-grep. We can install several plugins like this, and since each one creates a custom command rather than overriding the :grep command, they can all coexist without conflict. We needn’t stick to one grep-like program. We can use whichever is best for the task at hand.

Make ack Jump to Line and Column

But ack has another trick up its sleeve. When run with the --column option, ack will output the line and column number of each match. Observe:

​=> ​$ ack --nogroup --column Waldo *​

​<= department-store.txt:1:1:Waldo is beside the boot counter.

​ goldrush.txt:6:1:Waldo is studying his clipboard.

​ goldrush.txt:9:41:The penny farthing is 10 paces ahead of Waldo.

If we could tweak the ‘grepformat’ to extract this extra information, then we could navigate search results by jumping to the precise position of each match rather than just to the right line. It’s easily done using these settings:

​=> ​:set grepprg=ack\ --nogroup\ --column\ $*​

​=> ​:set grepformat=%f:%l:%c:%m​

The %c item matches the column number.

Tip 111 Grep with Vim’s Internal Search Engine

	 	 	 The :vimgrep command allows us to search through multiple files using Vim’s native regular expression engine.

As a demonstration, we’ll use the files in the grep/quotes directory, which you can find in the source files that come distributed with this book. The directory contains the following files, reproduced here with their contents:

​ quotes/

​ about.txt

​ Don't watch the clock; do what it does. Keep going.

​

​ tough.txt

​ When the going gets tough, the tough get going.

​

​ where.txt

​ If you don't know where you are going,

​ you might wind up someplace else.

Each of these files contains at least one occurrence of the word「going.」We can ask Vim to search for that word in each of those files using the :vimgrep command, like this:

​=> ​:vimgrep /going/ clock.txt tough.txt where.txt​

​<= (1 of 3): Don't watch the clock; do what it does. Keep going.

​=> ​:cnext​

​<= (2 of 3): When the going gets tough, the tough get going.

​=> ​:cnext​

​<= (3 of 3): If you don't know where you are going,

The :vimgrep command populates the quickfix list with one entry for each line that contains a match. Navigate through the results using commands such as :cnext and :cprev (see Tip 106​Browse the Quickfix List​).

The file tough.txt contains two occurrences of the word「going,」but our :vimgrep command only counted the first match. If we supply the g flag after the pattern, then :vimgrep will match all occurrences of the specified pattern, not just the first match on each line:

​=> ​:vim /going/g clock.txt tough.txt where.txt​

​<= (1 of 4): Don't watch the clock; do what it does. Keep going.

This time the quickfix list contains an entry for all four occurrences of the word「going.」This might remind you of the way that the :substitute command works: by default it only affects the first match on the line, but when supplied with the g flag it will affect all matches on a given line. When I’m using the :substitute or :vimgrep command, I almost always want the behavior that the g flag specifies.

Specifying Which Files to Look Inside

This is the format of the :vimgrep command (:vimgrepⓘ):

​ :​vim​[​grep​][!] ​/{pattern}/​[​g​][​j​] {​file​} ...

The {file} argument must not be blank. It can include filenames, wildcards, backtick expressions, and combinations of all of the above. Each of the techniques that we can use to populate the argument list can also be used here. (See ​Populate the Argument List​ for a detailed discussion.)

	 	 In the previous examples, we spelled out the names of each file individually. We could get the same result by using a wildcard:

​=> ​:vim /going/g *.txt​

​<= (1 of 4): Don't watch the clock; do what it does. Keep going.

As well as being able to use * and ** wildcards, we can use the ## symbol, which is expanded to represent the names of each file in the argument list (cmdline-specialⓘ). This allows for an alternative workflow. First, we populate the argument list with the files we want to inspect. Then we run :vimgrep across each of the files in the argument list:

​=> ​:args *.txt​

​=> ​:vim /going/g ##​

​<= (1 of 4): Don't watch the clock; do what it does. Keep going.

This may look like more work because we have to run two seperate Ex commands. But I often prefer to use :vimgrep this way because it lets me address two questions separately: what files do I want to search inside, and what pattern am I looking for? Once the argument list has been populated, we can reuse that set of files with the :vimgrep command as often as we like.

Search in File, Then Search in Project

We can leave the pattern field empty, which tells :vimgrep to use the current search pattern. The same trick works for the :substitute command (as discussed in Tip 91), and also for the :global command. This is handy if we want to search for a regular expression across multiple files. We can begin by composing a regular expression and testing it in the current file. When we’re satisfied that the pattern matches where it should, we execute :vimgrep using the exact same pattern. For example, here we use the search command to look inside the current file for a regex that will match both「don’t」and「Don’t.」

​=> ​/[Dd]on't​

​=> ​:vim //g *.txt​

​<= (1 of 2): Don't watch the clock; do what it does. Keep going.

The main advantage to using :vimgrep is that it understands the same patterns as Vim’s search command. If we wanted to use :grep to do a project-wide search for the same pattern, we would first have to translate it into a POSIX regular expression. That won’t take long for a simple pattern such as this, but you wouldn’t want to do that for a complex regular expression, such as the one we constructed in Tip 85.

Search History and :vimgrep

I often use this command, which looks inside each of the files in the argument list for the current search pattern:

​=> ​:vim //g ##​

​<= (1 of 2): Don't watch the clock; do what it does. Keep going.

One thing to watch out for with this command is that it will always use the current values from the argument list and search history. If we repeat this command later, it may behave differently depending on what’s in our argument list and search history.

Alternatively, we could fill the search field with the value of the current pattern by pressing <C-r>/. The search results would be the same either way, but our command history would be different.

​=> ​:vim /<C-r>//g ##​

If you think that you might want to rerun the same :vimgrep command later, then it would be useful to have that pattern preserved in your command history.

Footnotes

[30]

https://github.com/mileszs/ack.vim and https://github.com/tpope/vim-fugitive, respectively.

Copyright © 2016, The Pragmatic Bookshelf.

Chapter 19

Dial X for Autocompletion


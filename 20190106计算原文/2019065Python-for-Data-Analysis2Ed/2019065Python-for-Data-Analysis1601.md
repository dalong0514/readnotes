In Chapter 2 we looked at the basics of using the IPython shell and Jupyter notebook. In this chapter, we explore some deeper functionality in the IPython system that can either be used from the console or within Jupyter.

B.1 Using the Command History

IPython maintains a small on-disk database containing the text of each command that you execute. This serves various purposes:

Searching, completing, and executing previously executed commands with minimal typing

Persisting the command history between sessions

Logging the input/output history to a file

These features are more useful in the shell than in the notebook, since the notebook by design keeps a log of the input and output in each code cell.

Searching and Reusing the Command History

The IPython shell lets you search and execute previous code or other commands. This is useful, as you may often find yourself repeating the same commands, such as a %run command or some other code snippet. Suppose you had run:

In[7]: %run first/second/third/data_script.py

and then explored the results of the script (assuming it ran successfully) only to find that you made an incorrect calculation. After figuring out the problem and modifying data_script.py, you can start typing a few letters of the %run command and then press either the Ctrl-P key combination or the up arrow key. This will search the command history for the first prior command matching the letters you typed. Pressing either Ctrl-P or the up arrow key multiple times will continue to search through the history. If you pass over the command you wish to execute, fear not. You can move forward through the command history by pressing either Ctrl-N or the down arrow key. After doing this a few times, you may start pressing these keys without thinking!

Using Ctrl-R gives you the same partial incremental searching capability provided by the readline used in Unix-style shells, such as the bash shell. On Windows, readline functionality is emulated by IPython. To use this, press Ctrl-R and then type a few characters contained in the input line you want to search for:

In [1]: a_command = foo(x, y, z) (reverse-i-search)`com': a_command = foo(x, y, z)

Pressing Ctrl-R will cycle through the history for each line matching the characters you’ve typed.

Input and Output Variables

Forgetting to assign the result of a function call to a variable can be very annoying. An IPython session stores references to both the input commands and output Python objects in special variables. The previous two outputs are stored in the _ (one underscore) and __ (two underscores) variables, respectively:

In [24]: 2 ** 27 Out[24]: 134217728 In [25]: _ Out[25]: 134217728

Input variables are stored in variables named like _iX, where X is the input line number. For each input variable there is a corresponding output variable _X. So after input line 27, say, there will be two new variables _27 (for the output) and _i27 for the input:

In [26]: foo = 'bar' In [27]: foo Out[27]: 'bar' In [28]: _i27 Out[28]: u'foo' In [29]: _27 Out[29]: 'bar'

Since the input variables are strings they can be executed again with the Python exec keyword:

In [30]: exec(_i27)

Here _i27 refers to the code input in In [27].

Several magic functions allow you to work with the input and output history. %hist is capable of printing all or part of the input history, with or without line numbers. %reset is for clearing the interactive namespace and optionally the input and output caches. The %xdel magic function is intended for removing all references to a particular object from the IPython machinery. See the documentation for both of these magics for more details.

Warning

When working with very large datasets, keep in mind that IPython’s input and output history causes any object referenced there to not be garbage-collected (freeing up the memory), even if you delete the variables from the interactive namespace using the del keyword. In such cases, careful usage of %xdel and %reset can help you avoid running into memory problems.

B.2 Interacting with the Operating System

Another feature of IPython is that it allows you to seamlessly access the filesystem and operating system shell. This means, among other things, that you can perform most standard command-line actions as you would in the Windows or Unix (Linux, macOS) shell without having to exit IPython. This includes shell commands, changing directories, and storing the results of a command in a Python object (list or string). There are also simple command aliasing and directory bookmarking features.

See Table B-1 for a summary of magic functions and syntax for calling shell commands. I’ll briefly visit these features in the next few sections.

Table B-1. IPython system-related commandsCommandDescription

!cmd Execute cmd in the system shell

output = !cmd args Run cmd and store the stdout in output

%alias alias_name cmd Define an alias for a system (shell) command

%bookmark Utilize IPython’s directory bookmarking system

%cd directory Change system working directory to passed directory

%pwd Return the current system working directory

%pushd directory Place current directory on stack and change to target directory

%popd Change to directory popped off the top of the stack

%dirs Return a list containing the current directory stack

%dhist Print the history of visited directories

%env Return the system environment variables as a dict

%matplotlib Configure matplotlib integration options

Shell Commands and Aliases

Starting a line in IPython with an exclamation point !, or bang, tells IPython to execute everything after the bang in the system shell. This means that you can delete files (using rm or del, depending on your OS), change directories, or execute any other process.

You can store the console output of a shell command in a variable by assigning the expression escaped with ! to a variable. For example, on my Linux-based machine connected to the internet via ethernet, I can get my IP address as a Python variable:

In [1]: ip_info = !ifconfig wlan0 | grep "inet " In [2]: ip_info[0].strip() Out[2]: 'inet addr:10.0.0.11 Bcast:10.0.0.255 Mask:255.255.255.0'

The returned Python object ip_info is actually a custom list type containing various versions of the console output.

IPython can also substitute in Python values defined in the current environment when using !. To do this, preface the variable name by the dollar sign $:

In [3]: foo = 'test*' In [4]: !ls $foo test4.py test.py test.xml

The %alias magic function can define custom shortcuts for shell commands. As a simple example:

In [1]: %alias ll ls -l In [2]: ll /usr total 332 drwxr-xr-x 2 root root 69632 2012-01-29 20:36 bin/ drwxr-xr-x 2 root root 4096 2010-08-23 12:05 games/ drwxr-xr-x 123 root root 20480 2011-12-26 18:08 include/ drwxr-xr-x 265 root root 126976 2012-01-29 20:36 lib/ drwxr-xr-x 44 root root 69632 2011-12-26 18:08 lib32/ lrwxrwxrwx 1 root root 3 2010-08-23 16:02 lib64 -> lib/ drwxr-xr-x 15 root root 4096 2011-10-13 19:03 local/ drwxr-xr-x 2 root root 12288 2012-01-12 09:32 sbin/ drwxr-xr-x 387 root root 12288 2011-11-04 22:53 share/ drwxrwsr-x 24 root src 4096 2011-07-17 18:38 src/

You can execute multiple commands just as on the command line by separating them with semicolons:

In [558]: %alias test_alias (cd examples; ls; cd ..) In [559]: test_alias macrodata.csv spx.csv	tips.csv

You’ll notice that IPython「forgets」any aliases you define interactively as soon as the session is closed. To create permanent aliases, you will need to use the configuration system.

Directory Bookmark System

IPython has a simple directory bookmarking system to enable you to save aliases for common directories so that you can jump around very easily. For example, suppose you wanted to create a bookmark that points to the supplementary materials for this book:

In [6]: %bookmark py4da /home/wesm/code/pydata-book

Once you’ve done this, when we use the %cd magic, we can use any bookmarks we’ve defined:

In [7]: cd py4da (bookmark:py4da) -> /home/wesm/code/pydata-book /home/wesm/code/pydata-book

If a bookmark name conflicts with a directory name in your current working directory, you can use the -b flag to override and use the bookmark location. Using the -l option with %bookmark lists all of your bookmarks:

In [8]: %bookmark -l Current bookmarks: py4da -> /home/wesm/code/pydata-book-source

Bookmarks, unlike aliases, are automatically persisted between IPython sessions.

B.3 Software Development Tools

In addition to being a comfortable environment for interactive computing and data exploration, IPython can also be a useful companion for general Python software development. In data analysis applications, it’s important first to have correct code. Fortunately, IPython has closely integrated and enhanced the built-in Python pdb debugger. Secondly you want your code to be fast. For this IPython has easy-to-use code timing and profiling tools. I will give an overview of these tools in detail here.

Interactive Debugger

IPython’s debugger enhances pdb with tab completion, syntax highlighting, and context for each line in exception tracebacks. One of the best times to debug code is right after an error has occurred. The %debug command, when entered immediately after an exception, invokes the「post-mortem」debugger and drops you into the stack frame where the exception was raised:

In [2]: run examples/ipython_bug.py --------------------------------------------------------------------------- AssertionError Traceback (most recent call last) /home/wesm/code/pydata-book/examples/ipython_bug.py in <module>() 13 throws_an_exception() 14 ---> 15 calling_things() /home/wesm/code/pydata-book/examples/ipython_bug.py in calling_things() 11 def calling_things(): 12 works_fine() ---> 13 throws_an_exception() 14 15 calling_things() /home/wesm/code/pydata-book/examples/ipython_bug.py in throws_an_exception() 7 a = 5 8 b = 6 ----> 9 assert(a + b == 10) 10 11 def calling_things(): AssertionError: In [3]: %debug > /home/wesm/code/pydata-book/examples/ipython_bug.py(9)throws_an_exception() 8 b = 6 ----> 9 assert(a + b == 10) 10 ipdb>

Once inside the debugger, you can execute arbitrary Python code and explore all of the objects and data (which have been「kept alive」by the interpreter) inside each stack frame. By default you start in the lowest level, where the error occurred. By pressing u (up) and d (down), you can switch between the levels of the stack trace:

ipdb> u > /home/wesm/code/pydata-book/examples/ipython_bug.py(13)calling_things() 12 works_fine() ---> 13 throws_an_exception() 14

Executing the %pdb command makes it so that IPython automatically invokes the debugger after any exception, a mode that many users will find especially useful.

It’s also easy to use the debugger to help develop code, especially when you wish to set breakpoints or step through the execution of a function or script to examine the state at each stage. There are several ways to accomplish this. The first is by using %run with the -d flag, which invokes the debugger before executing any code in the passed script. You must immediately press s (step) to enter the script:

In [5]: run -d examples/ipython_bug.py Breakpoint 1 at /home/wesm/code/pydata-book/examples/ipython_bug.py:1 NOTE: Enter 'c' at the ipdb> prompt to start your script. > <string>(1)<module>() ipdb> s --Call-- > /home/wesm/code/pydata-book/examples/ipython_bug.py(1)<module>() 1---> 1 def works_fine(): 2 a = 5 3 b = 6

After this point, it’s up to you how you want to work your way through the file. For example, in the preceding exception, we could set a breakpoint right before calling the works_fine method and run the script until we reach the breakpoint by pressing c (continue):

ipdb> b 12 ipdb> c > /home/wesm/code/pydata-book/examples/ipython_bug.py(12)calling_things() 11 def calling_things(): 2--> 12 works_fine() 13 throws_an_exception()

At this point, you can step into works_fine() or execute works_fine() by pressing n (next) to advance to the next line:

ipdb> n > /home/wesm/code/pydata-book/examples/ipython_bug.py(13)calling_things() 2 12 works_fine() ---> 13 throws_an_exception() 14

Then, we could step into throws_an_exception and advance to the line where the error occurs and look at the variables in the scope. Note that debugger commands take precedence over variable names; in such cases, preface the variables with ! to examine their contents:

ipdb> s --Call-- > /home/wesm/code/pydata-book/examples/ipython_bug.py(6)throws_an_exception() 5 ----> 6 def throws_an_exception(): 7 a = 5 ipdb> n > /home/wesm/code/pydata-book/examples/ipython_bug.py(7)throws_an_exception() 6 def throws_an_exception(): ----> 7 a = 5 8 b = 6 ipdb> n > /home/wesm/code/pydata-book/examples/ipython_bug.py(8)throws_an_exception() 7 a = 5 ----> 8 b = 6 9 assert(a + b == 10) ipdb> n > /home/wesm/code/pydata-book/examples/ipython_bug.py(9)throws_an_exception() 8 b = 6 ----> 9 assert(a + b == 10) 10 ipdb> !a 5 ipdb> !b 6

Developing proficiency with the interactive debugger is largely a matter of practice and experience. See Table B-2 for a full catalog of the debugger commands. If you are accustomed to using an IDE, you might find the terminal-driven debugger to be a bit unforgiving at first, but that will improve in time. Some of the Python IDEs have excellent GUI debuggers, so most users can find something that works for them.

Table B-2. (I)Python debugger commandsCommandAction

h(elp) Display command list

help command Show documentation for command

c(ontinue) Resume program execution

q(uit) Exit debugger without executing any more code

b(reak) number Set breakpoint at number in current file

b path/to/file.py:number Set breakpoint at line number in specified file

s(tep) Step into function call

n(ext) Execute current line and advance to next line at current level

u(p)/d(own) Move up/down in function call stack

a(rgs) Show arguments for current function

debug statement Invoke statement statement in new (recursive) debugger

l(ist) statement Show current position and context at current level of stack

w(here) Print full stack trace with context at current position

Other ways to make use of the debugger

There are a couple of other useful ways to invoke the debugger. The first is by using a special set_trace function (named after pdb.set_trace), which is basically a「poor man’s breakpoint.」Here are two small recipes you might want to put somewhere for your general use (potentially adding them to your IPython profile as I do):

from IPython.core.debugger import Pdb def set_trace(): Pdb(color_scheme='Linux').set_trace(sys._getframe().f_back) def debug(f, *args, **kwargs): pdb = Pdb(color_scheme='Linux') return pdb.runcall(f, *args, **kwargs)

The first function, set_trace, is very simple. You can use a set_trace in any part of your code that you want to temporarily stop in order to more closely examine it (e.g., right before an exception occurs):

In [7]: run examples/ipython_bug.py > /home/wesm/code/pydata-book/examples/ipython_bug.py(16)calling_things() 15 set_trace() ---> 16 throws_an_exception() 17

Pressing c (continue) will cause the code to resume normally with no harm done.

The debug function we just looked at enables you to invoke the interactive debugger easily on an arbitrary function call. Suppose we had written a function like the following and we wished to step through its logic:

def f(x, y, z=1): tmp = x + y return tmp / z

Ordinarily using f would look like f(1, 2, z=3). To instead step into f, pass f as the first argument to debug followed by the positional and keyword arguments to be passed to f:

In [6]: debug(f, 1, 2, z=3) > <ipython-input>(2)f() 1 def f(x, y, z): ----> 2 tmp = x + y 3 return tmp / z ipdb>

I find that these two simple recipes save me a lot of time on a day-to-day basis.

Lastly, the debugger can be used in conjunction with %run. By running a script with %run -d, you will be dropped directly into the debugger, ready to set any breakpoints and start the script:

In [1]: %run -d examples/ipython_bug.py Breakpoint 1 at /home/wesm/code/pydata-book/examples/ipython_bug.py:1 NOTE: Enter 'c' at the ipdb> prompt to start your script. > <string>(1)<module>() ipdb>

Adding -b with a line number starts the debugger with a breakpoint set already:

In [2]: %run -d -b2 examples/ipython_bug.py Breakpoint 1 at /home/wesm/code/pydata-book/examples/ipython_bug.py:2 NOTE: Enter 'c' at the ipdb> prompt to start your script. > <string>(1)<module>() ipdb> c > /home/wesm/code/pydata-book/examples/ipython_bug.py(2)works_fine() 1 def works_fine(): 1---> 2 a = 5 3 b = 6 ipdb>

Timing Code: %time and %timeit

For larger-scale or longer-running data analysis applications, you may wish to measure the execution time of various components or of individual statements or function calls. You may want a report of which functions are taking up the most time in a complex process. Fortunately, IPython enables you to get this information very easily while you are developing and testing your code.

Timing code by hand using the built-in time module and its functions time.clock and time.time is often tedious and repetitive, as you must write the same uninteresting boilerplate code:

import time start = time.time() for i in range(iterations): # some code to run here elapsed_per = (time.time() - start) / iterations

Since this is such a common operation, IPython has two magic functions, %time and %timeit, to automate this process for you.

%time runs a statement once, reporting the total execution time. Suppose we had a large list of strings and we wanted to compare different methods of selecting all strings starting with a particular prefix. Here is a simple list of 600,000 strings and two identical methods of selecting only the ones that start with 'foo':

# a very large list of strings strings = ['foo', 'foobar', 'baz', 'qux', 'python', 'Guido Van Rossum'] * 100000 method1 = [x for x in strings if x.startswith('foo')] method2 = [x for x in strings if x[:3] == 'foo']

It looks like they should be about the same performance-wise, right? We can check for sure using %time:

In [561]: %time method1 = [x for x in strings if x.startswith('foo')] CPU times: user 0.19 s, sys: 0.00 s, total: 0.19 s Wall time: 0.19 s In [562]: %time method2 = [x for x in strings if x[:3] == 'foo'] CPU times: user 0.09 s, sys: 0.00 s, total: 0.09 s Wall time: 0.09 s

The Wall time (short for「wall-clock time」) is the main number of interest. So, it looks like the first method takes more than twice as long, but it’s not a very precise measurement. If you try %time-ing those statements multiple times yourself, you’ll find that the results are somewhat variable. To get a more precise measurement, use the %timeit magic function. Given an arbitrary statement, it has a heuristic to run a statement multiple times to produce a more accurate average runtime:

In [563]: %timeit [x for x in strings if x.startswith('foo')] 10 loops, best of 3: 159 ms per loop In [564]: %timeit [x for x in strings if x[:3] == 'foo'] 10 loops, best of 3: 59.3 ms per loop

This seemingly innocuous example illustrates that it is worth understanding the performance characteristics of the Python standard library, NumPy, pandas, and other libraries used in this book. In larger-scale data analysis applications, those milliseconds will start to add up!

%timeit is especially useful for analyzing statements and functions with very short execution times, even at the level of microseconds (millionths of a second) or nanoseconds (billionths of a second). These may seem like insignificant amounts of time, but of course a 20 microsecond function invoked 1 million times takes 15 seconds longer than a 5 microsecond function. In the preceding example, we could very directly compare the two string operations to understand their performance characteristics:

In [565]: x = 'foobar' In [566]: y = 'foo' In [567]: %timeit x.startswith(y) 1000000 loops, best of 3: 267 ns per loop In [568]: %timeit x[:3] == y 10000000 loops, best of 3: 147 ns per loop

Basic Profiling: %prun and %run -p

Profiling code is closely related to timing code, except it is concerned with determining where time is spent. The main Python profiling tool is the cProfile module, which is not specific to IPython at all. cProfile executes a program or any arbitrary block of code while keeping track of how much time is spent in each function.

A common way to use cProfile is on the command line, running an entire program and outputting the aggregated time per function. Suppose we had a simple script that does some linear algebra in a loop (computing the maximum absolute eigenvalues of a series of 100 × 100 matrices):

import numpy as np from numpy.linalg import eigvals def run_experiment(niter=100): K = 100 results = [] for _ in xrange(niter): mat = np.random.randn(K, K) max_eigenvalue = np.abs(eigvals(mat)).max() results.append(max_eigenvalue) return results some_results = run_experiment() print 'Largest one we saw: %s' % np.max(some_results)

You can run this script through cProfile using the following in the command line:

python -m cProfile cprof_example.py

If you try that, you’ll find that the output is sorted by function name. This makes it a bit hard to get an idea of where the most time is spent, so it’s very common to specify a sort order using the -s flag:

$ python -m cProfile -s cumulative cprof_example.py Largest one we saw: 11.923204422 15116 function calls (14927 primitive calls) in 0.720 seconds Ordered by: cumulative time ncalls tottime percall cumtime percall filename:lineno(function) 1 0.001 0.001 0.721 0.721 cprof_example.py:1(<module>) 100 0.003 0.000 0.586 0.006 linalg.py:702(eigvals) 200 0.572 0.003 0.572 0.003 {numpy.linalg.lapack_lite.dgeev} 1 0.002 0.002 0.075 0.075 __init__.py:106(<module>) 100 0.059 0.001 0.059 0.001 {method 'randn') 1 0.000 0.000 0.044 0.044 add_newdocs.py:9(<module>) 2 0.001 0.001 0.037 0.019 __init__.py:1(<module>) 2 0.003 0.002 0.030 0.015 __init__.py:2(<module>) 1 0.000 0.000 0.030 0.030 type_check.py:3(<module>) 1 0.001 0.001 0.021 0.021 __init__.py:15(<module>) 1 0.013 0.013 0.013 0.013 numeric.py:1(<module>) 1 0.000 0.000 0.009 0.009 __init__.py:6(<module>) 1 0.001 0.001 0.008 0.008 __init__.py:45(<module>) 262 0.005 0.000 0.007 0.000 function_base.py:3178(add_newdoc) 100 0.003 0.000 0.005 0.000 linalg.py:162(_assertFinite) ...

Only the first 15 rows of the output are shown. It’s easiest to read by scanning down the cumtime column to see how much total time was spent inside each function. Note that if a function calls some other function, the clock does not stop running. cProfile records the start and end time of each function call and uses that to produce the timing.

In addition to the command-line usage, cProfile can also be used programmatically to profile arbitrary blocks of code without having to run a new process. IPython has a convenient interface to this capability using the %prun command and the -p option to %run. %prun takes the same「command-line options」as cProfile but will profile an arbitrary Python statement instead of a whole .py file:

In [4]: %prun -l 7 -s cumulative run_experiment() 4203 function calls in 0.643 seconds Ordered by: cumulative time List reduced from 32 to 7 due to restriction <7> ncalls tottime percall cumtime percall filename:lineno(function) 1 0.000 0.000 0.643 0.643 <string>:1(<module>) 1 0.001 0.001 0.643 0.643 cprof_example.py:4(run_experiment) 100 0.003 0.000 0.583 0.006 linalg.py:702(eigvals) 200 0.569 0.003 0.569 0.003 {numpy.linalg.lapack_lite.dgeev} 100 0.058 0.001 0.058 0.001 {method 'randn'} 100 0.003 0.000 0.005 0.000 linalg.py:162(_assertFinite) 200 0.002 0.000 0.002 0.000 {method 'all' of 'numpy.ndarray'}

Similarly, calling %run -p -s cumulative cprof_example.py has the same effect as the command-line approach, except you never have to leave IPython.

In the Jupyter notebook, you can use the %%prun magic (two % signs) to profile an entire code block. This pops up a separate window with the profile output. This can be useful in getting possibly quick answers to questions like,「Why did that code block take so long to run?」

There are other tools available that help make profiles easier to understand when you are using IPython or Jupyter. One of these is SnakeViz, which produces an interactive visualization of the profile results using d3.js.

Profiling a Function Line by Line

In some cases the information you obtain from %prun (or another cProfile-based profile method) may not tell the whole story about a function’s execution time, or it may be so complex that the results, aggregated by function name, are hard to interpret. For this case, there is a small library called line_profiler (obtainable via PyPI or one of the package management tools). It contains an IPython extension enabling a new magic function %lprun that computes a line-by-line-profiling of one or more functions. You can enable this extension by modifying your IPython configuration (see the IPython documentation or the section on configuration later in this chapter) to include the following line:

# A list of dotted module names of IPython extensions to load. c.TerminalIPythonApp.extensions = ['line_profiler']

You can also run the command:

%load_ext line_profiler

line_profiler can be used programmatically (see the full documentation), but it is perhaps most powerful when used interactively in IPython. Suppose you had a module prof_mod with the following code doing some NumPy array operations:

from numpy.random import randn def add_and_sum(x, y): added = x + y summed = added.sum(axis=1) return summed def call_function(): x = randn(1000, 1000) y = randn(1000, 1000) return add_and_sum(x, y)

If we wanted to understand the performance of the add_and_sum function, %prun gives us the following:

In [569]: %run prof_mod In [570]: x = randn(3000, 3000) In [571]: y = randn(3000, 3000) In [572]: %prun add_and_sum(x, y) 4 function calls in 0.049 seconds Ordered by: internal time ncalls tottime percall cumtime percall filename:lineno(function) 1 0.036 0.036 0.046 0.046 prof_mod.py:3(add_and_sum) 1 0.009 0.009 0.009 0.009 {method 'sum' of 'numpy.ndarray'} 1 0.003 0.003 0.049 0.049 <string>:1(<module>)

This is not especially enlightening. With the line_profiler IPython extension activated, a new command %lprun is available. The only difference in usage is that we must instruct %lprun which function or functions we wish to profile. The general syntax is:

%lprun -f func1 -f func2 statement_to_profile

In this case, we want to profile add_and_sum, so we run:

In [573]: %lprun -f add_and_sum add_and_sum(x, y) Timer unit: 1e-06 s File: prof_mod.py Function: add_and_sum at line 3 Total time: 0.045936 s Line # Hits Time Per Hit % Time Line Contents ============================================================== 3 def add_and_sum(x, y): 4 1 36510 36510.0 79.5 added = x + y 5 1 9425 9425.0 20.5 summed = added.sum(axis=1) 6 1 1 1.0 0.0 return summed

This can be much easier to interpret. In this case we profiled the same function we used in the statement. Looking at the preceding module code, we could call call_function and profile that as well as add_and_sum, thus getting a full picture of the performance of the code:

In [574]: %lprun -f add_and_sum -f call_function call_function() Timer unit: 1e-06 s File: prof_mod.py Function: add_and_sum at line 3 Total time: 0.005526 s Line # Hits Time Per Hit % Time Line Contents ============================================================== 3 def add_and_sum(x, y): 4 1 4375 4375.0 79.2 added = x + y 5 1 1149 1149.0 20.8 summed = added.sum(axis=1) 6 1 2 2.0 0.0 return summed File: prof_mod.py Function: call_function at line 8 Total time: 0.121016 s Line # Hits Time Per Hit % Time Line Contents ============================================================== 8 def call_function(): 9 1 57169 57169.0 47.2 x = randn(1000, 1000) 10 1 58304 58304.0 48.2 y = randn(1000, 1000) 11 1 5543 5543.0 4.6 return add_and_sum(x, y)

As a general rule of thumb, I tend to prefer %prun (cProfile) for「macro」profiling and %lprun (line_profiler) for「micro」profiling. It’s worthwhile to have a good understanding of both tools.

Note

The reason that you must explicitly specify the names of the functions you want to profile with %lprun is that the overhead of「tracing」the execution time of each line is substantial. Tracing functions that are not of interest has the potential to significantly alter the profile results.

B.4 Tips for Productive Code Development Using IPython

Writing code in a way that makes it easy to develop, debug, and ultimately use interactively may be a paradigm shift for many users. There are procedural details like code reloading that may require some adjustment as well as coding style concerns.

Therefore, implementing most of the strategies described in this section is more of an art than a science and will require some experimentation on your part to determine a way to write your Python code that is effective for you. Ultimately you want to structure your code in a way that makes it easy to use iteratively and to be able to explore the results of running a program or function as effortlessly as possible. I have found software designed with IPython in mind to be easier to work with than code intended only to be run as as standalone command-line application. This becomes especially important when something goes wrong and you have to diagnose an error in code that you or someone else might have written months or years beforehand.

Reloading Module Dependencies

In Python, when you type import some_lib, the code in some_lib is executed and all the variables, functions, and imports defined within are stored in the newly created some_lib module namespace. The next time you type import some_lib, you will get a reference to the existing module namespace. The potential difficulty in interactive IPython code development comes when you, say, %run a script that depends on some other module where you may have made changes. Suppose I had the following code in test_script.py:

import some_lib x = 5 y = [1, 2, 3, 4] result = some_lib.get_answer(x, y)

If you were to execute %run test_script.py then modify some_lib.py, the next time you execute %run test_script.py you will still get the old version of some_lib.py because of Python’s「load-once」module system. This behavior differs from some other data analysis environments, like MATLAB, which automatically propagate code changes.1 To cope with this, you have a couple of options. The first way is to use the reload function in the importlib module in the standard library:

import some_lib import importlib importlib.reload(some_lib)

This guarantees that you will get a fresh copy of some_lib.py every time you run test_script.py. Obviously, if the dependencies go deeper, it might be a bit tricky to be inserting usages of reload all over the place. For this problem, IPython has a special dreload function (not a magic function) for「deep」(recursive) reloading of modules. If I were to run some_lib.py then type dreload(some_lib), it will attempt to reload some_lib as well as all of its dependencies. This will not work in all cases, unfortunately, but when it does it beats having to restart IPython.

Code Design Tips

There’s no simple recipe for this, but here are some high-level principles I have found effective in my own work.

Keep relevant objects and data alive

It’s not unusual to see a program written for the command line with a structure somewhat like the following trivial example:

from my_functions import g def f(x, y): return g(x + y) def main(): x = 6 y = 7.5 result = x + y if __name__ == '__main__': main()

Do you see what might go wrong if we were to run this program in IPython? After it’s done, none of the results or objects defined in the main function will be accessible in the IPython shell. A better way is to have whatever code is in main execute directly in the module’s global namespace (or in the if __name__ == '__main__': block, if you want the module to also be importable). That way, when you %run the code, you’ll be able to look at all of the variables defined in main. This is equivalent to defining top-level variables in cells in the Jupyter notebook.

Flat is better than nested

Deeply nested code makes me think about the many layers of an onion. When testing or debugging a function, how many layers of the onion must you peel back in order to reach the code of interest? The idea that「flat is better than nested」is a part of the Zen of Python, and it applies generally to developing code for interactive use as well. Making functions and classes as decoupled and modular as possible makes them easier to test (if you are writing unit tests), debug, and use interactively.

Overcome a fear of longer files

If you come from a Java (or another such language) background, you may have been told to keep files short. In many languages, this is sound advice; long length is usually a bad「code smell,」indicating refactoring or reorganization may be necessary. However, while developing code using IPython, working with 10 small but interconnected files (under, say, 100 lines each) is likely to cause you more headaches in general than two or three longer files. Fewer files means fewer modules to reload and less jumping between files while editing, too. I have found maintaining larger modules, each with high internal cohesion, to be much more useful and Pythonic. After iterating toward a solution, it sometimes will make sense to refactor larger files into smaller ones.

Obviously, I don’t support taking this argument to the extreme, which would to be to put all of your code in a single monstrous file. Finding a sensible and intuitive module and package structure for a large codebase often takes a bit of work, but it is especially important to get right in teams. Each module should be internally cohesive, and it should be as obvious as possible where to find functions and classes responsible for each area of functionality.

B.5 Advanced IPython Features

Making full use of the IPython system may lead you to write your code in a slightly different way, or to dig into the configuration.

Making Your Own Classes IPython-Friendly

IPython makes every effort to display a console-friendly string representation of any object that you inspect. For many objects, like dicts, lists, and tuples, the built-in pprint module is used to do the nice formatting. In user-defined classes, however, you have to generate the desired string output yourself. Suppose we had the following simple class:

class Message: def __init__(self, msg): self.msg = msg

If you wrote this, you would be disappointed to discover that the default output for your class isn’t very nice:

In [576]: x = Message('I have a secret') In [577]: x Out[577]: <__main__.Message instance at 0x60ebbd8>

IPython takes the string returned by the __repr__ magic method (by doing output = repr(obj)) and prints that to the console. Thus, we can add a simple __repr__ method to the preceding class to get a more helpful output:

class Message: def __init__(self, msg): self.msg = msg def __repr__(self): return 'Message: %s' % self.msg

In [579]: x = Message('I have a secret') In [580]: x Out[580]: Message: I have a secret

Profiles and Configuration

Most aspects of the appearance (colors, prompt, spacing between lines, etc.) and behavior of the IPython and Jupyter environments are configurable through an extensive configuration system. Here are some things you can do via configuration:

Change the color scheme

Change how the input and output prompts look, or remove the blank line after Out and before the next In prompt

Execute an arbitrary list of Python statements (e.g., imports that you use all the time or anything else you want to happen each time you launch IPython)

Enable always-on IPython extensions, like the %lprun magic in line_profiler

Enabling Jupyter extensions

Define your own magics or system aliases

Configurations for the IPython shell are specified in special ipython_config.py files, which are usually found in the .ipython/ directory in your user home directory. Configuration is performed based on a particular profile. When you start IPython normally, you load up, by default, the default profile, stored in the profile_default directory. Thus, on my Linux OS the full path to my default IPython configuration file is:

/home/wesm/.ipython/profile_default/ipython_config.py

To initialize this file on your system, run in the terminal:

ipython profile create

I’ll spare you the gory details of what’s in this file. Fortunately it has comments describing what each configuration option is for, so I will leave it to the reader to tinker and customize. One additional useful feature is that it’s possible to have multiple profiles. Suppose you wanted to have an alternative IPython configuration tailored for a particular application or project. Creating a new profile is as simple as typing something like the following:

ipython profile create secret_project

Once you’ve done this, edit the config files in the newly created profile_secret_project directory and then launch IPython like so:

$ ipython --profile=secret_project Python 3.5.1 | packaged by conda-forge | (default, May 20 2016, 05:22:56) Type "copyright", "credits" or "license" for more information. IPython 5.1.0 -- An enhanced Interactive Python. ? -> Introduction and overview of IPython's features. %quickref -> Quick reference. help -> Python's own help system. object? -> Details about 'object', use 'object??' for extra details. IPython profile: secret_project

As always, the online IPython documentation is an excellent resource for more on profiles and configuration.

Configuration for Jupyter works a little differently because you can use its notebooks with languages other than Python. To create an analogous Jupyter config file, run:

jupyter notebook --generate-config

This writes a default config file to the .jupyter/jupyter_notebook_config.py directory in your home directory. After editing this to suit your needs, you may rename it to a different file, like:

$ mv ~/.jupyter/jupyter_notebook_config.py ~/.jupyter/my_custom_config.py

When launching Jupyter, you can then add the --config argument:

jupyter notebook --config=~/.jupyter/my_custom_config.py

B.6 Conclusion

As you work through the code examples in this book and grow your skills as a Python programmer, I encourage you to keep learning about the IPython and Jupyter ecosystems. Since these projects have been designed to assist user productivity, you may discover tools that enable you to do your work more easily than using the Python language and its computational libraries by themselves.

You can also find a wealth of interesting Jupyter notebooks on the nbviewer website.

1

Since a module or package may be imported in many different places in a particular program, Python caches a module’s code the first time it is imported rather than executing the code in the module every time. Otherwise, modularity and good code organization could potentially cause inefficiency in an application.

Index

Symbols

! (exclamation point), Shell Commands and Aliases

!= operator, Binary operators and comparisons, Boolean Indexing, Universal Functions: Fast Element-Wise Array Functions

# (hash mark), Comments

% (percent sign), About Magic Commands, Basic Profiling: %prun and %run -p

%matplotlib magic function, A Brief matplotlib API Primer

& operator, Binary operators and comparisons, set, set, Boolean Indexing

&= operator, set

() (parentheses), Function and object method calls, Tuple

* (asterisk), Introspection

* operator, Binary operators and comparisons

** operator, Binary operators and comparisons

+ operator, Binary operators and comparisons, Tuple, Concatenating and combining lists

- operator, Binary operators and comparisons, set

-= operator, set

. (period), Tab Completion

/ operator, Binary operators and comparisons

// operator, Binary operators and comparisons, Numeric types

: (colon), Indentation, not braces

; (semicolon), Indentation, not braces

< operator, Binary operators and comparisons, Universal Functions: Fast Element-Wise Array Functions

<= operator, Binary operators and comparisons, Universal Functions: Fast Element-Wise Array Functions

== operator, Binary operators and comparisons, Universal Functions: Fast Element-Wise Array Functions

> operator, Binary operators and comparisons, Universal Functions: Fast Element-Wise Array Functions

>= operator, Binary operators and comparisons, Universal Functions: Fast Element-Wise Array Functions

>>> prompt, The Python Interpreter

? (question mark), Introspection-Introspection

@ symbol, Linear Algebra

[] (square brackets), Tuple, List

\ (backslash), Strings, Regular Expressions

^ operator, Binary operators and comparisons, set

^= operator, set

_ (underscore), Tab Completion, Unpacking tuples, NumPy dtype Hierarchy, Input and Output Variables

{} (curly braces), dict, set

| operator, Binary operators and comparisons, set-set, Boolean Indexing

|= operator, set

~ operator, Boolean Indexing

A

%a datetime format, Converting Between String and Datetime

%A datetime format, Converting Between String and Datetime

a(rgs) debugger command, Interactive Debugger

abs function, Universal Functions: Fast Element-Wise Array Functions, Example: Random Walks

accumulate method, ufunc Instance Methods

accumulations, Summarizing and Computing Descriptive Statistics

add binary function, Universal Functions: Fast Element-Wise Array Functions

add method, set, Arithmetic methods with fill values

add_categories method, Categorical Methods

add_constant function, Estimating Linear Models

add_patch method, Annotations and Drawing on a Subplot

add_subplot method, Figures and Subplots

aggfunc method, Pivot Tables and Cross-Tabulation

aggregate (agg) method, Data Aggregation, Group Transforms and「Unwrapped」GroupBys

aggregations (reductions), Mathematical and Statistical Methods

%alias magic function, Interacting with the Operating System-Shell Commands and Aliases

all method, Methods for Boolean Arrays, ufunc Instance Methods

and keyword, Tab Completion, Booleans, Boolean Indexing

annotate function, Annotations and Drawing on a Subplot

annotating in matplotlib, Annotations and Drawing on a Subplot-Annotations and Drawing on a Subplot

anonymous (lambda) functions, Anonymous (Lambda) Functions

any built-in function, Tab Completion

any method, Methods for Boolean Arrays, Simulating Many Random Walks at Once, Detecting and Filtering Outliers

Apache Parquet format, Using HDF5 Format

APIs, pandas interacting with, Interacting with Web APIs

append method, Adding and removing elements, Index Objects

append mode for files, Files and the Operating System

apply method, Function Application and Mapping, Unique Values, Value Counts, and Membership, Apply: General split-apply-combine-Example: Group-Wise Linear Regression, Group Transforms and「Unwrapped」GroupBys-Group Transforms and「Unwrapped」GroupBys

applymap method, Function Application and Mapping

arange function, Import Conventions, Creating ndarrays

arccos function, Universal Functions: Fast Element-Wise Array Functions

arccosh function, Universal Functions: Fast Element-Wise Array Functions

arcsin function, Universal Functions: Fast Element-Wise Array Functions

arcsinh function, Universal Functions: Fast Element-Wise Array Functions

arctan function, Universal Functions: Fast Element-Wise Array Functions

arctanh function, Universal Functions: Fast Element-Wise Array Functions

argmax method, Mathematical and Statistical Methods, Example: Random Walks, Summarizing and Computing Descriptive Statistics

argmin method, Mathematical and Statistical Methods, Summarizing and Computing Descriptive Statistics

argpartition method, Partially Sorting Arrays

argsort method, Indirect Sorts: argsort and lexsort, Partially Sorting Arrays

arithmetic operationsbetween DataFrame and Series, Operations between DataFrame and Series

between objects with different indexes, Arithmetic and Data Alignment

on date and time periods, Periods and Period Arithmetic-Creating a PeriodIndex from Arrays

with fill values, Arithmetic methods with fill values

with NumPy arrays, Arithmetic with NumPy Arrays

array function, Creating ndarrays, Creating ndarrays

arrays (see ndarray object)

arrow function, Annotations and Drawing on a Subplot

as keyword, Imports

asarray function, Creating ndarrays

asfreq method, Period Frequency Conversion, Upsampling and Interpolation

assign method, Techniques for Method Chaining

associative arrays (see dicts)

asterisk (*), Introspection

astype method, Data Types for ndarrays

as_ordered methdo, Categorical Methods

as_ordered method, Categorical Type in pandas

as_unordered method, Categorical Methods

attributesfor data types, Structured and Record Arrays

for ndarrays, Creating ndarrays, Reshaping Arrays, Broadcasting Over Other Axes, The Importance of Contiguous Memory

hidden, Tab Completion

in DataFrame data structure, DataFrame

in Python, Attributes and methods, Correlation and Covariance

in Series data structure, Series

automagic feature, About Magic Commands

%automagic magic function, About Magic Commands

average method, Sorting and Ranking

axesbroadcasting over, Broadcasting Over Other Axes

concatenating along, Combining and Merging Datasets, Concatenating Along an Axis-Concatenating Along an Axis

renaming indexes for, Renaming Axis Indexes

selecting indexes with duplicate labels, Axis Indexes with Duplicate Labels

swapping in arrays, Transposing Arrays and Swapping Axes

AxesSubplot object, Figures and Subplots, Ticks, Labels, and Legends

axis method, Summarizing and Computing Descriptive Statistics

B

%b datetime format, Converting Between String and Datetime

%B datetime format, Converting Between String and Datetime

b(reak) debugger command, Interactive Debugger

backslash (\), Strings, Regular Expressions

bang (!), Shell Commands and Aliases

bar method, Bar Plots

bar plots, Bar Plots-Bar Plots

barh method, Bar Plots

barplot function, Bar Plots

base frequency, Frequencies and Date Offsets

bcolz binary format, Binary Data Formats

beta function, Pseudorandom Number Generation

binary data formatsabout, Binary Data Formats

binary mode for files, Files and the Operating System-Bytes and Unicode with Files

HDF5 format, Using HDF5 Format-Using HDF5 Format

Microsoft Excel files, Reading Microsoft Excel Files-Reading Microsoft Excel Files

binary moving window functions, Binary Moving Window Functions

binary operators and comparisons in Python, Binary operators and comparisons, set

binary searches of lists, Binary search and maintaining a sorted list

binary universal functions, Universal Functions: Fast Element-Wise Array Functions, Universal Functions: Fast Element-Wise Array Functions

binding, defined, Variables and argument passing, Concatenating Along an Axis

binning continuous data, Discretization and Binning

binomial function, Pseudorandom Number Generation

bisect module, Binary search and maintaining a sorted list

Bitly dataset example, 1.USA.gov Data from Bitly-Counting Time Zones with pandas

Blosc compression library, Binary Data Formats

Bokeh tool, Other Python Visualization Tools

%bookmark magic function, Interacting with the Operating System, Directory Bookmark System

bookmarking directories in IPython, Directory Bookmark System

bool data type, Scalar Types, Booleans, Data Types for ndarrays

bool function, Type casting

boolean arrays, Methods for Boolean Arrays

boolean indexing, Boolean Indexing-Boolean Indexing

braces {}, dict, set

break keyword, for loops

broadcasting, ndarrays and, Arithmetic with NumPy Arrays, Repeating Elements: tile and repeat, Broadcasting-Setting Array Values by Broadcasting

bucket analysis, Quantile and Bucket Analysis

build_design_matrices function, Data Transformations in Patsy Formulas

builtins module, Data Transformations in Patsy Formulas

bytes data type, Scalar Types, Bytes and Unicode

C

%C datetime format, Converting Between String and Datetime

C order (row major order), C Versus Fortran Order, The Importance of Contiguous Memory

c(ontinue) debugger command, Interactive Debugger

calendar module, Date and Time Data Types and Tools

Cartesian product, itertools module, Database-Style DataFrame Joins

casefold method, String Object Methods

cat method, Vectorized String Functions in pandas

categorical databasic overview, Categorical Data-Creating dummy variables for modeling

facet grids and, Facet Grids and Categorical Data

Patsy library and, Categorical Data and Patsy-Categorical Data and Patsy

Categorical object, Discretization and Binning, Quantile and Bucket Analysis, Categorical Data-Creating dummy variables for modeling

%cd magic function, Interacting with the Operating System, Directory Bookmark System

ceil function, Universal Functions: Fast Element-Wise Array Functions

center method, Vectorized String Functions in pandas

chaining methods, Techniques for Method Chaining-The pipe Method

chisquare function, Pseudorandom Number Generation

clear method, set

clipboard, executing code from, Executing Code from the Clipboard

close method, Files and the Operating System, Files and the Operating System

closed attribute, Files and the Operating System

!cmd command, Interacting with the Operating System

collections module, Default values

colon (:), Indentation, not braces

color selection in matplotlib, Colors, Markers, and Line Styles

column major order (Fortran order), C Versus Fortran Order, The Importance of Contiguous Memory

columns method, Pivot Tables and Cross-Tabulation

column_stack function, Concatenating and Splitting Arrays

combinations function, itertools module

combine_first method, Combining and Merging Datasets, Combining Data with Overlap

combining data (see merging data)

command historyinput and output variables, Input and Output Variables

reusing, Searching and Reusing the Command History

searching, Searching and Reusing the Command History

using in IPython, Using the Command History-Input and Output Variables

commandsdebugger, Interactive Debugger

magic functions, About Magic Commands-About Magic Commands

updating packages, Installing or Updating Python Packages

comments in Python, Comments

compile method, Regular Expressions

complex128 data type, Data Types for ndarrays

complex256 data type, Data Types for ndarrays

complex64 data type, Data Types for ndarrays

concat function, Combining and Merging Datasets, Merging on Index, Concatenating Along an Axis-Concatenating Along an Axis, Column-Wise and Multiple Function Application

concatenate function, Concatenating Along an Axis, Concatenating and Splitting Arrays

concatenatingalong an axis, Combining and Merging Datasets, Concatenating Along an Axis-Concatenating Along an Axis

lists, Concatenating and combining lists

strings, Strings

conda update command, Installing or Updating Python Packages

conditional logic as array operations, Expressing Conditional Logic as Array Operations

configuration for IPython, Profiles and Configuration-Profiles and Configuration

configuring matplotlib, matplotlib Configuration

contains method, Vectorized String Functions in pandas

contiguous memory, The Importance of Contiguous Memory-The Importance of Contiguous Memory

continue keyword, for loops

continuing education, Continuing Your Education

control flow in Python, Control Flow-Ternary expressions

coordinated universal time (UTC), Time Zone Handling

copy method, Basic Indexing and Slicing, DataFrame

copysign function, Universal Functions: Fast Element-Wise Array Functions

corr aggregation function, Binary Moving Window Functions

corr method, Correlation and Covariance

correlation, Correlation and Covariance-Correlation and Covariance, Example: Group Weighted Average and Correlation

corrwith method, Correlation and Covariance

cos function, Universal Functions: Fast Element-Wise Array Functions

cosh function, Universal Functions: Fast Element-Wise Array Functions

count method, Strings, Tuple methods, Summarizing and Computing Descriptive Statistics, String Object Methods-String Object Methods, Vectorized String Functions in pandas, Data Aggregation

cov method, Correlation and Covariance

covariance, Correlation and Covariance-Correlation and Covariance

%cpaste magic function, Executing Code from the Clipboard, About Magic Commands

cProfile module, Basic Profiling: %prun and %run -p-Basic Profiling: %prun and %run -p

cross-tabulation, Cross-Tabulations: Crosstab

crosstab function, Cross-Tabulations: Crosstab

cross_val_score function, Introduction to scikit-learn

CSV files, Reading and Writing Data in Text Format, Writing Data to Text Format-Working with Delimited Formats

csv module, Working with Delimited Formats

Ctrl-A keyboard shortcut, Terminal Keyboard Shortcuts

Ctrl-B keyboard shortcut, Terminal Keyboard Shortcuts

Ctrl-C keyboard shortcut, Interrupting running code, Terminal Keyboard Shortcuts

Ctrl-D keyboard shortcut, The Python Interpreter

Ctrl-E keyboard shortcut, Terminal Keyboard Shortcuts

Ctrl-F keyboard shortcut, Terminal Keyboard Shortcuts

Ctrl-K keyboard shortcut, Terminal Keyboard Shortcuts

Ctrl-L keyboard shortcut, Terminal Keyboard Shortcuts

Ctrl-N keyboard shortcut, Terminal Keyboard Shortcuts, Searching and Reusing the Command History

Ctrl-P keyboard shortcut, Terminal Keyboard Shortcuts, Searching and Reusing the Command History

Ctrl-R keyboard shortcut, Terminal Keyboard Shortcuts, Searching and Reusing the Command History

Ctrl-Shift-V keyboard shortcut, Terminal Keyboard Shortcuts

Ctrl-U keyboard shortcut, Terminal Keyboard Shortcuts

cummax method, Summarizing and Computing Descriptive Statistics

cummin method, Summarizing and Computing Descriptive Statistics

cumprod method, Mathematical and Statistical Methods, Summarizing and Computing Descriptive Statistics

cumsum method, Mathematical and Statistical Methods, Summarizing and Computing Descriptive Statistics, ufunc Instance Methods

curly braces {}, dict, set

currying, Currying: Partial Argument Application

cut function, Discretization and Binning, Quantile and Bucket Analysis

c_ object, Stacking helpers: r_ and c_

D

%d datetime format, Dates and times, Converting Between String and Datetime

%D datetime format, Dates and times, Converting Between String and Datetime

d(own) debugger command, Interactive Debugger

data aggregationabout, Data Aggregation

column-wise, Column-Wise and Multiple Function Application-Column-Wise and Multiple Function Application

multiple function application, Column-Wise and Multiple Function Application-Column-Wise and Multiple Function Application

returning data without row indexes, Returning Aggregated Data Without Row Indexes

data alignment, pandas library and, Arithmetic and Data Alignment-Operations between DataFrame and Series

data analysis with Pythonabout, Why Python for Data Analysis?, Python Language Basics, IPython, and Jupyter Notebooks-Python Language Basics, IPython, and Jupyter Notebooks

glue code, Python as Glue

MovieLens 1M dataset example, MovieLens 1M Dataset-Measuring Rating Disagreement

restrictions to consider, Why Not Python?

US baby names dataset example, US Baby Names 1880–2010-Boy names that became girl names (and vice versa)

US Federal Election Commission database example, 2012 Federal Election Commission Database-Donation Statistics by State

USA.gov data from Bitly example, 1.USA.gov Data from Bitly-Counting Time Zones with pandas

USDA food database example, USDA Food Database-USDA Food Database

「two-language」problem, Solving the「Two-Language」Problem

data cleaning and preparation (see data wrangling)

data loading (see reading data)

data manipulation (see data wrangling)

data munging (see data wrangling)

data selectionfor axis indexes with duplicate labels, Axis Indexes with Duplicate Labels

in pandas library, Indexing, Selection, and Filtering-Selection with loc and iloc

time series data, Indexing, Selection, Subsetting

data structuresabout, Data Structures and Sequences

dict comprehensions, List, Set, and Dict Comprehensions

dicts, dict-Valid dict key types

for pandas library, Introduction to pandas Data Structures-Index Objects

list comprehensions, List, Set, and Dict Comprehensions-Nested list comprehensions

lists, List-Slicing

set comprehensions, List, Set, and Dict Comprehensions

sets, set-set

tuples, Tuple-Tuple methods

data transformation (see transforming data)

data typesattributes for, Structured and Record Arrays

defined, Data Types for ndarrays, ndarray Object Internals

for date and time data, Date and Time Data Types and Tools

for ndarrays, Data Types for ndarrays-Data Types for ndarrays

in Python, Scalar Types-Dates and times

nested, Nested dtypes and Multidimensional Fields

NumPy hierarchy, NumPy dtype Hierarchy

parent classes of, NumPy dtype Hierarchy

data wranglingcombining and merging datasets, Combining and Merging Datasets-Combining Data with Overlap

defined, Jargon

handling missing data, Handling Missing Data-Filling In Missing Data

hierarchical indexing, Hierarchical Indexing-Indexing with a DataFrame’s columns, Reshaping with Hierarchical Indexing

pivoting data, Pivoting「Long」to「Wide」Format-Pivoting「Wide」to「Long」Format

reshaping data, Reshaping with Hierarchical Indexing

string manipulation, String Manipulation-Vectorized String Functions in pandas

transforming data, Data Transformation-Computing Indicator/Dummy Variables

working with delimited formats, Working with Delimited Formats-Working with Delimited Formats

databasesDataFrame joins, Database-Style DataFrame Joins-Database-Style DataFrame Joins

pandas interacting with, Interacting with Databases

storing data in, Pivoting「Long」to「Wide」Format

DataFrame data structureabout, pandas, DataFrame-DataFrame, Nested dtypes and Multidimensional Fields

database-stye joins, Database-Style DataFrame Joins-Database-Style DataFrame Joins

indexing with columns, Indexing with a DataFrame’s columns

JSON data and, JSON Data

operations between Series and, Operations between DataFrame and Series

optional function arguments, Reading and Writing Data in Text Format

plot method arguments, Line Plots

possible data inputs to, DataFrame

ranking data in, Sorting and Ranking

sorting considerations, Sorting and Ranking, Indirect Sorts: argsort and lexsort

summary statistics methods for, Correlation and Covariance

DataOffset object, Operations with Time Zone−Aware Timestamp Objects

datasetscombining and merging, Combining and Merging Datasets-Combining Data with Overlap

MovieLens 1M example, MovieLens 1M Dataset-Measuring Rating Disagreement

US baby names example, US Baby Names 1880–2010-Boy names that became girl names (and vice versa)

US Federal Election Commission database example, 2012 Federal Election Commission Database-Donation Statistics by State

USA.gov data from Bitly example, 1.USA.gov Data from Bitly-Counting Time Zones with pandas

USDA food database example, USDA Food Database-USDA Food Database

date data type, Dates and times, Date and Time Data Types and Tools

date offsets, Frequencies and Date Offsets, Shifting dates with offsets-Shifting dates with offsets

date ranges, generating, Generating Date Ranges-Generating Date Ranges

dates and timesabout, Dates and times

converting between strings and datetime, Converting Between String and Datetime-Converting Between String and Datetime

data types and tools, Date and Time Data Types and Tools

formatting specifications, Converting Between String and Datetime, Converting Between String and Datetime

generating date ranges, Generating Date Ranges-Generating Date Ranges

period arithmetic and, Periods and Period Arithmetic-Creating a PeriodIndex from Arrays

datetime data typeabout, Dates and times, Date and Time Data Types and Tools-Date and Time Data Types and Tools

converting between strings and, Converting Between String and Datetime-Converting Between String and Datetime

format specification for, Converting Between String and Datetime

datetime module, Dates and times, Date and Time Data Types and Tools

datetime64 data type, Time Series Basics

DatetimeIndex class, Time Series Basics, Generating Date Ranges, Time Zone Localization and Conversion

dateutil package, Converting Between String and Datetime

date_range function, Generating Date Ranges-Generating Date Ranges

daylight saving time (DST), Time Zone Handling

debug function, Other ways to make use of the debugger

%debug magic function, Exceptions in IPython, Interactive Debugger

debugger, IPython, Interactive Debugger-Other ways to make use of the debugger

decode method, Bytes and Unicode

def keyword, Functions, Anonymous (Lambda) Functions

default values for dicts, Default values

defaultdict class, Default values

del keyword, dict, DataFrame

del method, DataFrame

delete method, Index Objects

delimited formats, working with, Working with Delimited Formats-Working with Delimited Formats

dense method, Sorting and Ranking

density plots, Histograms and Density Plots-Histograms and Density Plots

deque (double-ended queue), Adding and removing elements

describe method, Summarizing and Computing Descriptive Statistics, Data Aggregation

design matrix, Creating Model Descriptions with Patsy

det function, Linear Algebra

development tools for IPython (see software development tools for IPython)

%dhist magic function, Interacting with the Operating System

diag function, Linear Algebra

Dialect class, Working with Delimited Formats

dict comprehensions, List, Set, and Dict Comprehensions

dict function, Creating dicts from sequences

dictionary-encoded representation, Background and Motivation

dicts (data structures)about, dict

creating from sequences, Creating dicts from sequences

DataFrame data structure as, DataFrame

default values, Default values

grouping with, Grouping with Dicts and Series

Series data structure as, Series

valid key types, Valid dict key types

diff method, Summarizing and Computing Descriptive Statistics

difference method, set, Index Objects

difference_update method, set

dimension tables, Background and Motivation

directories, bookmarking in IPython, Directory Bookmark System

%dirs magic function, Interacting with the Operating System

discretization, Discretization and Binning

distplot method, Histograms and Density Plots

div method, Arithmetic methods with fill values

divide function, Universal Functions: Fast Element-Wise Array Functions

divmod function, Universal Functions: Fast Element-Wise Array Functions

dmatrices function, Creating Model Descriptions with Patsy

dnorm function, Estimating Linear Models

dot function, Transposing Arrays and Swapping Axes, Linear Algebra-Linear Algebra

downsampling, Resampling and Frequency Conversion, Downsampling-Open-High-Low-Close (OHLC) resampling

dreload function, Reloading Module Dependencies

drop method, Index Objects, Dropping Entries from an Axis

dropna method, Handling Missing Data-Filtering Out Missing Data, Example: Filling Missing Values with Group-Specific Values, Pivot Tables and Cross-Tabulation

drop_duplicates method, Removing Duplicates

DST (daylight saving time), Time Zone Handling

dstack function, Concatenating and Splitting Arrays

dtype (see data types)

dtype attribute, The NumPy ndarray: A Multidimensional Array Object, Data Types for ndarrays

duck typing, Duck typing

dummy variables, Computing Indicator/Dummy Variables-Computing Indicator/Dummy Variables, Creating dummy variables for modeling, Interfacing Between pandas and Model Code, Categorical Data and Patsy

dumps function, JSON Data

duplicate dataaxis indexes with duplicate labels, Axis Indexes with Duplicate Labels

removing, Removing Duplicates

time series with duplicate indexes, Time Series with Duplicate Indices

duplicated method, Removing Duplicates

dynamic references in Python, Dynamic references, strong types

E

edit-compile-run workflow, IPython and Jupyter

education, continuing, Continuing Your Education

eig function, Linear Algebra

elif statement, if, elif, and else

else statement, if, elif, and else

empty function, Creating ndarrays-Creating ndarrays

empty namespace, The %run Command

empty_like function, Creating ndarrays

encode method, Bytes and Unicode

end-of-line (EOL) markers, Files and the Operating System

endswith method, String Object Methods, Vectorized String Functions in pandas

enumerate function, enumerate

%env magic function, Interacting with the Operating System

EOL (end-of-line) markers, Files and the Operating System

equal function, Universal Functions: Fast Element-Wise Array Functions

error handling in Python, Errors and Exception Handling-Exceptions in IPython

escape characters, Strings

ewm function, Exponentially Weighted Functions

Excel files (Microsoft), Reading Microsoft Excel Files-Reading Microsoft Excel Files

ExcelFile class, Reading Microsoft Excel Files

exception handling in Python, Errors and Exception Handling-Exceptions in IPython

exclamation point (!), Shell Commands and Aliases

execute-explore workflow, IPython and Jupyter

exit command, The Python Interpreter

exp function, Universal Functions: Fast Element-Wise Array Functions

expanding function, Moving Window Functions

exponentially-weighted functions, Exponentially Weighted Functions

extend method, Concatenating and combining lists

extract method, Vectorized String Functions in pandas

eye function, Creating ndarrays

F

%F datetime format, Dates and times, Converting Between String and Datetime

fabs function, Universal Functions: Fast Element-Wise Array Functions

facet grids, Facet Grids and Categorical Data

FacetGrid class, Facet Grids and Categorical Data

factorplot built-in function, Facet Grids and Categorical Data

fancy indexing, Fancy Indexing, Fancy Indexing Equivalents: take and put

FDIC bank failures list, XML and HTML: Web Scraping

Feather binary file format, Reading and Writing Data in Text Format, Binary Data Formats

feature engineering, Interfacing Between pandas and Model Code

Federal Election Commission database example, 2012 Federal Election Commission Database-Donation Statistics by State

Figure object, Figures and Subplots

file managementbinary data formats, Binary Data Formats-Reading Microsoft Excel Files

commonly used file methods, Files and the Operating System

design tips, Overcome a fear of longer files

file input and output with arrays, File Input and Output with Arrays

JSON data, JSON Data-JSON Data

memory-mapped files, Memory-Mapped Files

opening files, Files and the Operating System

Python file modes, Files and the Operating System

reading and writing data in text format, Reading and Writing Data in Text Format-Writing Data to Text Format

saving plots to files, Saving Plots to File

Web scraping, XML and HTML: Web Scraping-Parsing XML with lxml.objectify

working with delimited formats, Working with Delimited Formats-Working with Delimited Formats

filling in dataarithmetic methods with fill values, Arithmetic methods with fill values

filling in missing data, Filling In Missing Data-Filling In Missing Data, Replacing Values

with group-specific values, Example: Filling Missing Values with Group-Specific Values

fillna method, Handling Missing Data, Filling In Missing Data-Filling In Missing Data, Replacing Values, Example: Filling Missing Values with Group-Specific Values, Upsampling and Interpolation

fill_value method, Pivot Tables and Cross-Tabulation

filteringin pandas library, Indexing, Selection, and Filtering-Selection with loc and iloc

missing data, Filtering Out Missing Data

outliers, Detecting and Filtering Outliers

find method, String Object Methods-String Object Methods

findall method, Regular Expressions, Regular Expressions, Vectorized String Functions in pandas

finditer method, Regular Expressions

first method, Sorting and Ranking, Data Aggregation

fit method, Estimating Linear Models, Introduction to scikit-learn

fixed frequency, Time Series

flags attribute, The Importance of Contiguous Memory

flatten method, Reshaping Arrays

float data type, Scalar Types, Type casting

float function, Type casting

float128 data type, Data Types for ndarrays

float16 data type, Data Types for ndarrays

float32 data type, Data Types for ndarrays

float64 data type, Data Types for ndarrays

floor function, Universal Functions: Fast Element-Wise Array Functions

floordiv method, Arithmetic methods with fill values

floor_divide function, Universal Functions: Fast Element-Wise Array Functions

flow control in Python, Control Flow-Ternary expressions

flush method, Files and the Operating System, Memory-Mapped Files

fmax function, Universal Functions: Fast Element-Wise Array Functions

fmin function, Universal Functions: Fast Element-Wise Array Functions

for loops, for loops, Nested list comprehensions

format method, Strings

formattingdates and times, Converting Between String and Datetime, Converting Between String and Datetime

strings, Strings

Fortran order (column major order), C Versus Fortran Order, The Importance of Contiguous Memory

frequenciesbase, Frequencies and Date Offsets

basic for time series, Generating Date Ranges

converting between, Date Ranges, Frequencies, and Shifting, Resampling and Frequency Conversion-Resampling with Periods

date offsets and, Frequencies and Date Offsets

fixed, Time Series

period conversion, Period Frequency Conversion

quarterly period frequencies, Quarterly Period Frequencies

fromfile function, Why Use Structured Arrays?

frompyfunc function, Writing New ufuncs in Python

from_codes method, Categorical Type in pandas

full function, Creating ndarrays

full_like function, Creating ndarrays

functions, Functions(see also universal functions)

about, Functions

accessing variables, Namespaces, Scope, and Local Functions

anonymous, Anonymous (Lambda) Functions

as objects, Functions Are Objects-Functions Are Objects

currying, Currying: Partial Argument Application

errors and exception handling, Errors and Exception Handling

exponentially-weighted, Exponentially Weighted Functions

generators and, Generators-Exceptions in IPython

grouping with, Grouping with Functions

in Python, Function and object method calls

lambda, Anonymous (Lambda) Functions

magic, About Magic Commands-About Magic Commands

namespaces and, Namespaces, Scope, and Local Functions

object introspection, Introspection

partial argument application, Currying: Partial Argument Application

profiling line by line, Profiling a Function Line by Line-Profiling a Function Line by Line

returning multiple values, Returning Multiple Values

sequence, Built-in Sequence Functions-reversed

transforming data using, Transforming Data Using a Function or Mapping

type inference in, Reading and Writing Data in Text Format

writing fast NumPy functions with Numba, Writing Fast NumPy Functions with Numba-Creating Custom numpy.ufunc Objects with Numba

functools module, Currying: Partial Argument Application

G

gamma function, Pseudorandom Number Generation

generatorsabout, Generators

generator expressions for, Generator expresssions

itertools module and, itertools module

get method, Default values, Vectorized String Functions in pandas

GET request (HTTP), Interacting with Web APIs

getattr function, Attributes and methods

getroot method, Parsing XML with lxml.objectify

get_chunk method, Reading Text Files in Pieces

get_dummies function, Computing Indicator/Dummy Variables, Creating dummy variables for modeling, Interfacing Between pandas and Model Code

get_indexer method, Unique Values, Value Counts, and Membership

get_value method, Selection with loc and iloc

GIL (global interpreter lock), Why Not Python?

global keyword, Namespaces, Scope, and Local Functions

glue for code, Python as, Python as Glue

greater function, Universal Functions: Fast Element-Wise Array Functions

greater_equal function, Universal Functions: Fast Element-Wise Array Functions

Greenwich Mean Time, Time Zone Handling

group keys, suppressing, Suppressing the Group Keys

group operationsabout, Data Aggregation and Group Operations, Advanced GroupBy Use

cross-tabulation, Cross-Tabulations: Crosstab

data aggregation, Data Aggregation-Returning Aggregated Data Without Row Indexes

GroupBy mechanics, GroupBy Mechanics-Grouping by Index Levels

pivot tables, Data Aggregation and Group Operations, Pivot Tables and Cross-Tabulation-Cross-Tabulations: Crosstab

split-apply-combine, GroupBy Mechanics, Apply: General split-apply-combine-Example: Group-Wise Linear Regression

unwrapped, Group Transforms and「Unwrapped」GroupBys

group weighted average, Example: Group Weighted Average and Correlation

groupby function, itertools module

groupby method, Computations with Categoricals, numpy.searchsorted: Finding Elements in a Sorted Array

GroupBy objectabout, GroupBy Mechanics-GroupBy Mechanics

grouping by index level, Grouping by Index Levels

grouping with dicts, Grouping with Dicts and Series

grouping with functions, Grouping with Functions

grouping with Series, Grouping with Dicts and Series

iterating over groups, Iterating Over Groups

optimized methods, Data Aggregation

selecting columns, Selecting a Column or Subset of Columns

selecting subset of columns, Selecting a Column or Subset of Columns

groups method, Regular Expressions

H

%H datetime format, Dates and times, Converting Between String and Datetime

h(elp) debugger command, Interactive Debugger

hasattr function, Attributes and methods

hash function, Valid dict key types

hash maps (see dicts)

hash mark (#), Comments

hashability, Valid dict key types

HDF5 (hierarchical data format 5), Using HDF5 Format-Using HDF5 Format, HDF5 and Other Array Storage Options

HDFStore class, Using HDF5 Format

head method, DataFrame

heapsort method, Alternative Sort Algorithms

hierarchical data format (HDF5), HDF5 and Other Array Storage Options

hierarchical indexingabout, Hierarchical Indexing-Hierarchical Indexing

in pandas, Reading and Writing Data in Text Format

reordering and sorting levels, Reordering and Sorting Levels

reshaping data with, Reshaping with Hierarchical Indexing

summary statistics by level, Summary Statistics by Level

with DataFrame columns, Indexing with a DataFrame’s columns

%hist magic function, About Magic Commands

hist method, Histograms and Density Plots

histograms, Histograms and Density Plots-Histograms and Density Plots

hsplit function, Concatenating and Splitting Arrays

hstack function, Concatenating and Splitting Arrays

HTML files, XML and HTML: Web Scraping-Parsing XML with lxml.objectify

HTTP requests, Interacting with Web APIs

Hugunin, Jim, NumPy Basics: Arrays and Vectorized Computation

Hunter, John D., matplotlib, Plotting and Visualization

I

%I datetime format, Dates and times, Converting Between String and Datetime

identity function, Creating ndarrays

IDEs (Integrated Development Environments), Integrated Development Environments (IDEs) and Text Editors

idxmax method, Summarizing and Computing Descriptive Statistics

idxmin method, Summarizing and Computing Descriptive Statistics

if statement, if, elif, and else

iloc operator, Selection with loc and iloc, Permutation and Random Sampling

immutable objects, Mutable and immutable objects, Categorical Type in pandas

import conventionsfor matplotlib, A Brief matplotlib API Primer

for modules, Import Conventions, Imports

for Python, Import Conventions, Imports, The NumPy ndarray: A Multidimensional Array Object

importlib module, Reloading Module Dependencies

imshow function, Array-Oriented Programming with Arrays

in keyword, Adding and removing elements, String Object Methods

in-place sorts, Sorting, More About Sorting

in1d method, Unique and Other Set Logic, Unique and Other Set Logic

indentation in Python, Indentation, not braces

index method, String Object Methods-String Object Methods, Pivot Tables and Cross-Tabulation

Index objects, Index Objects-Index Objects

indexes and indexingaxis indexes with duplicate labels, Axis Indexes with Duplicate Labels

boolean indexing, Boolean Indexing-Boolean Indexing

fancy indexing, Fancy Indexing, Fancy Indexing Equivalents: take and put

for ndarrays, Basic Indexing and Slicing-Indexing with slices

for pandas library, Indexing, Selection, and Filtering-Selection with loc and iloc, Axis Indexes with Duplicate Labels

grouping by index level, Grouping by Index Levels

hierarchical indexing, Reading and Writing Data in Text Format, Hierarchical Indexing-Indexing with a DataFrame’s columns, Reshaping with Hierarchical Indexing

Index objects, Index Objects-Index Objects

integer indexing, Integer Indexes

merging on index, Merging on Index-Merging on Index

renaming axis indexes, Renaming Axis Indexes

time series data, Indexing, Selection, Subsetting

time series with duplicate indexes, Time Series with Duplicate Indices

timedeltas and, Time Series

indexing operator, Slicing

indicator variables, Computing Indicator/Dummy Variables-Computing Indicator/Dummy Variables

indirect sorts, Indirect Sorts: argsort and lexsort

inner join type, Database-Style DataFrame Joins

input variables, Input and Output Variables

insert method, Adding and removing elements, Index Objects

insort function, Binary search and maintaining a sorted list

int data type, Scalar Types, Type casting

int function, Type casting

int16 data type, Data Types for ndarrays

int32 data type, Data Types for ndarrays

int64 data type, Data Types for ndarrays

int8 data type, Data Types for ndarrays

integer arrays, indexing, Fancy Indexing, Fancy Indexing Equivalents: take and put

integer indexing, Integer Indexes

Integrated Development Environments (IDEs), Integrated Development Environments (IDEs) and Text Editors

interactive debugger, Interactive Debugger-Other ways to make use of the debugger

interpreted languages, Why Python for Data Analysis?, The Python Interpreter

interrupting running code, Interrupting running code

intersect1d method, Unique and Other Set Logic

intersection method, set-set, Index Objects

intersection_update method, set

intervals of time, Time Series

inv function, Linear Algebra

.ipynb file extension, Running the Jupyter Notebook

IPython%run command and, The Python Interpreter

%run command in, The %run Command-Interrupting running code

about, IPython and Jupyter

advanced features, Advanced IPython Features-Profiles and Configuration

bookmarking directories, Directory Bookmark System

code development tips, Tips for Productive Code Development Using IPython-Overcome a fear of longer files

command history in, Using the Command History-Input and Output Variables

exception handling in, Exceptions in IPython

executing code from clipboard, Executing Code from the Clipboard

figures and subplots, Figures and Subplots

interacting with operating system, Interacting with the Operating System-Directory Bookmark System

keyboard shortcuts for, Terminal Keyboard Shortcuts

magic commands in, About Magic Commands-About Magic Commands

matplotlib integration, Matplotlib Integration

object introspection, Introspection-Introspection

running Jupyter notebook, Running the Jupyter Notebook-Running the Jupyter Notebook

running shell, Running the IPython Shell-Running the IPython Shell

shell commands in, Shell Commands and Aliases

software development tools, Software Development Tools-Profiling a Function Line by Line

tab completion in, Tab Completion-Tab Completion

ipython command, Running the IPython Shell-Running the IPython Shell

is keyword, Binary operators and comparisons

is not keyword, Binary operators and comparisons

isalnum method, Vectorized String Functions in pandas

isalpha method, Vectorized String Functions in pandas

isdecimal method, Vectorized String Functions in pandas

isdigit method, Vectorized String Functions in pandas

isdisjoint method, set

isfinite function, Universal Functions: Fast Element-Wise Array Functions

isin method, Index Objects, Unique Values, Value Counts, and Membership

isinf function, Universal Functions: Fast Element-Wise Array Functions

isinstance function, Dynamic references, strong types

islower method, Vectorized String Functions in pandas

isnan function, Universal Functions: Fast Element-Wise Array Functions

isnull method, Series, Handling Missing Data

isnumeric method, Vectorized String Functions in pandas

issubdtype function, NumPy dtype Hierarchy

issubset method, set

issuperset method, set

isupper method, Vectorized String Functions in pandas

is_monotonic property, Index Objects

is_unique property, Index Objects, Axis Indexes with Duplicate Labels, Time Series with Duplicate Indices

iter function, Duck typing

__iter__ magic method, Duck typing

iterator protocol, Duck typing, Generators-itertools module

itertools module, itertools module

J

jit function, Writing Fast NumPy Functions with Numba

join method, String Object Methods-String Object Methods, Vectorized String Functions in pandas, Merging on Index

join operations, Database-Style DataFrame Joins-Database-Style DataFrame Joins

JSON (JavaScript Object Notation), JSON Data-JSON Data, 1.USA.gov Data from Bitly

json method, Interacting with Web APIs

Jupyter notebook%load magic function, The %run Command

about, IPython and Jupyter

plotting nuances, Figures and Subplots

running, Running the Jupyter Notebook-Running the Jupyter Notebook

jupyter notebook command, Running the Jupyter Notebook

K

KDE (kernel density estimate) plots, Histograms and Density Plots

kernels, defined, IPython and Jupyter, Running the Jupyter Notebook

key-value pairs, dict

keyboard shortcuts for IPython, Terminal Keyboard Shortcuts

KeyboardInterrupt exception, Interrupting running code

KeyError exception, set

keys method, dict

keyword arguments, Function and object method calls, Functions

kurt method, Summarizing and Computing Descriptive Statistics

L

l(ist) debugger command, Interactive Debugger

labelsaxis indexes with duplicate labels, Axis Indexes with Duplicate Labels

selecting in matplotlib, Ticks, Labels, and Legends-Setting the title, axis labels, ticks, and ticklabels

lagging data, Shifting (Leading and Lagging) Data

lambda (anonymous) functions, Anonymous (Lambda) Functions

language semantics for Pythonabout, Language Semantics

attributes, Attributes and methods

binary operators and comparisons, Binary operators and comparisons, set

comments, Comments

duck typing, Duck typing

function and object method calls, Function and object method calls

import conventions, Imports

indentation not braces, Indentation, not braces

methods, Attributes and methods

mutable and immutable objects, Mutable and immutable objects

object model, Everything is an object

references, Variables and argument passing-Dynamic references, strong types

strongly typed language, Dynamic references, strong types

variables and argument passing, Variables and argument passing

last method, Data Aggregation

leading data, Shifting (Leading and Lagging) Data

left join type, Database-Style DataFrame Joins

legend method, Adding legends

legend selection in matplotlib, Colors, Markers, and Line Styles-Adding legends

len function, Grouping with Functions

len method, Vectorized String Functions in pandas

less function, Universal Functions: Fast Element-Wise Array Functions

less_equal function, Universal Functions: Fast Element-Wise Array Functions

level keyword, Grouping by Index Levels

level method, Summarizing and Computing Descriptive Statistics

levelsgrouping by index levels, Grouping by Index Levels

sorting, Reordering and Sorting Levels

summary statistics by, Summary Statistics by Level

lexsort method, Indirect Sorts: argsort and lexsort

libraries (see specific libraries)

line plots, Line Plots-Line Plots

line style selection in matplotlib, Colors, Markers, and Line Styles

linear algebra, Linear Algebra-Linear Algebra

linear regression, Example: Group-Wise Linear Regression, Estimating Linear Models-Estimating Linear Models

Linux, setting up Python on, GNU/Linux

list comprehensions, List, Set, and Dict Comprehensions-Nested list comprehensions

list function, Binary operators and comparisons, List

lists (data structures)about, List

adding and removing elements, Adding and removing elements

combining, Concatenating and combining lists

concatenating, Concatenating and combining lists

maintaining sorted lists, Binary search and maintaining a sorted list

slicing, Slicing

sorting, Sorting

lists (data structures)binary searches, Binary search and maintaining a sorted list

ljust method, String Object Methods

load function, File Input and Output with Arrays, Advanced Array Input and Output

%load magic function, The %run Command

loads function, JSON Data

loc operator, DataFrame, Selection with loc and iloc, Adding legends, Interfacing Between pandas and Model Code

local namespace, Namespaces, Scope, and Local Functions, Getting Started with pandas

localizing data to time zones, Time Zone Localization and Conversion

log function, Universal Functions: Fast Element-Wise Array Functions

log10 function, Universal Functions: Fast Element-Wise Array Functions

log1p function, Universal Functions: Fast Element-Wise Array Functions

log2 function, Universal Functions: Fast Element-Wise Array Functions

logical_and function, Universal Functions: Fast Element-Wise Array Functions, ufunc Instance Methods

logical_not function, Universal Functions: Fast Element-Wise Array Functions

logical_or function, Universal Functions: Fast Element-Wise Array Functions

logical_xor function, Universal Functions: Fast Element-Wise Array Functions

LogisticRegression class, Introduction to scikit-learn

LogisticRegressionCV class, Introduction to scikit-learn

long format, Pivoting「Long」to「Wide」Format

lower method, Transforming Data Using a Function or Mapping, String Object Methods, Vectorized String Functions in pandas

%lprun magic function, Profiling a Function Line by Line

lstrip method, String Object Methods, Vectorized String Functions in pandas

lstsq function, Linear Algebra

lxml library, XML and HTML: Web Scraping-Parsing XML with lxml.objectify

M

%m datetime format, Dates and times, Converting Between String and Datetime

%M datetime format, Dates and times, Converting Between String and Datetime

mad method, Summarizing and Computing Descriptive Statistics

magic functions, About Magic Commands-About Magic Commands(see also specific magic functions)

%debug magic function, About Magic Commands

%magic magic function, About Magic Commands

many-to-many merge, Database-Style DataFrame Joins

many-to-one join, Database-Style DataFrame Joins

map built-in function, List, Set, and Dict Comprehensions, Functions Are Objects

map method, Function Application and Mapping, Transforming Data Using a Function or Mapping, Renaming Axis Indexes

mappingtransforming data using, Transforming Data Using a Function or Mapping

universal functions, Function Application and Mapping-Sorting and Ranking

margins method, Pivot Tables and Cross-Tabulation

margins, defined, Pivot Tables and Cross-Tabulation

marker selection in matplotlib, Colors, Markers, and Line Styles

match method, Unique Values, Value Counts, and Membership, Regular Expressions, Regular Expressions, Vectorized String Functions in pandas

Math Kernel Library (MKL), Linear Algebra

matplotlib libraryabout, matplotlib, Plotting and Visualization

annotations in, Annotations and Drawing on a Subplot-Annotations and Drawing on a Subplot

color selection in, Colors, Markers, and Line Styles

configuring, matplotlib Configuration

creating image plots, Array-Oriented Programming with Arrays

figures in, Figures and Subplots-Adjusting the spacing around subplots

import convention, A Brief matplotlib API Primer

integration with IPython, Matplotlib Integration

label selection in, Ticks, Labels, and Legends-Setting the title, axis labels, ticks, and ticklabels

legend selection in, Colors, Markers, and Line Styles-Adding legends

line style selection in, Colors, Markers, and Line Styles

marker selection in, Colors, Markers, and Line Styles

saving plots to files, Saving Plots to File

subplots in, Figures and Subplots-Adjusting the spacing around subplots, Annotations and Drawing on a Subplot-Annotations and Drawing on a Subplot

tick mark selection in, Ticks, Labels, and Legends-Setting the title, axis labels, ticks, and ticklabels

%matplotlib magic function, Matplotlib Integration, Interacting with the Operating System

matrix operations in NumPy, Transposing Arrays and Swapping Axes, Linear Algebra

max method, Mathematical and Statistical Methods, Sorting and Ranking, Summarizing and Computing Descriptive Statistics, Data Aggregation

maximum function, Universal Functions: Fast Element-Wise Array Functions

mean method, Mathematical and Statistical Methods, Summarizing and Computing Descriptive Statistics, GroupBy Mechanics, Data Aggregation

median method, Summarizing and Computing Descriptive Statistics, Data Aggregation

melt method, Pivoting「Wide」to「Long」Format

memmap object, Memory-Mapped Files

memory managementC versus Fortran order, C Versus Fortran Order

continguous memory, The Importance of Contiguous Memory-The Importance of Contiguous Memory

NumPy-based algorithms and, NumPy Basics: Arrays and Vectorized Computation

memory-mapped files, Memory-Mapped Files

merge function, Database-Style DataFrame Joins-Database-Style DataFrame Joins

mergesort method, Alternative Sort Algorithms

merging datacombining data with overlap, Combining Data with Overlap

concatenating along an axis, Concatenating Along an Axis-Concatenating Along an Axis

database-stye DataFrame joins, Database-Style DataFrame Joins-Database-Style DataFrame Joins

merging on index, Merging on Index-Merging on Index

meshgrid function, Array-Oriented Programming with Arrays

methodscategorical, Categorical Methods-Categorical Methods

chaining, Techniques for Method Chaining-The pipe Method

defined, Function and object method calls

for boolean arrays, Methods for Boolean Arrays

for strings, String Object Methods-String Object Methods

for summary statistics, Unique Values, Value Counts, and Membership-Unique Values, Value Counts, and Membership

for tuples, Tuple methods

hidden, Tab Completion

in Python, Function and object method calls, Attributes and methods

object introspection, Introspection

optimized for GroupBy, Data Aggregation

statistical, Mathematical and Statistical Methods-Mathematical and Statistical Methods

ufunc instance methods, ufunc Instance Methods-ufunc Instance Methods

vectorized string methods in pandas, Vectorized String Functions in pandas-Vectorized String Functions in pandas

Microsoft Excel files, Reading Microsoft Excel Files-Reading Microsoft Excel Files

min method, Mathematical and Statistical Methods, Sorting and Ranking, Summarizing and Computing Descriptive Statistics, Data Aggregation

minimum function, Universal Functions: Fast Element-Wise Array Functions

missing dataabout, Handling Missing Data

filling in, Filling In Missing Data-Filling In Missing Data, Replacing Values

filling with group-specific values, Example: Filling Missing Values with Group-Specific Values

filtering out, Filtering Out Missing Data

marked by sentinel values, Reading and Writing Data in Text Format, Handling Missing Data

sorting considerations, Sorting and Ranking

mixture-of-normals estimate, Histograms and Density Plots

MKL (Math Kernel Library), Linear Algebra

mod function, Universal Functions: Fast Element-Wise Array Functions

modf function, Universal Functions: Fast Element-Wise Array Functions-Universal Functions: Fast Element-Wise Array Functions

modulesimport conventions for, Import Conventions, Imports

reloading dependencies, Reloading Module Dependencies

MovieLens 1M dataset example, MovieLens 1M Dataset-Measuring Rating Disagreement

moving window functionsabout, Moving Window Functions-Moving Window Functions

binary, Binary Moving Window Functions

exponentially-weighted functions, Exponentially Weighted Functions

user-defined, User-Defined Moving Window Functions

mro method, NumPy dtype Hierarchy

MSFT attribute, Correlation and Covariance

mul method, Arithmetic methods with fill values

multiply function, Universal Functions: Fast Element-Wise Array Functions

munging (see data wrangling)

mutable objects, Mutable and immutable objects

N

n(ext) debugger command, Interactive Debugger

NA data type, Handling Missing Data

name attribute, Series, DataFrame

names attribute, Boolean Indexing, Structured and Record Arrays

namespacesempty, The %run Command

functions and, Namespaces, Scope, and Local Functions

in Python, Dynamic references, strong types

NumPy, The NumPy ndarray: A Multidimensional Array Object

NaN (Not a Number), Universal Functions: Fast Element-Wise Array Functions, Series, Handling Missing Data

NaT (Not a Time), Converting Between String and Datetime

ndarray objectabout, NumPy Basics: Arrays and Vectorized Computation, The NumPy ndarray: A Multidimensional Array Object-The NumPy ndarray: A Multidimensional Array Object

advanced input and output, Advanced Array Input and Output-HDF5 and Other Array Storage Options

arithmetic with, Arithmetic with NumPy Arrays

array-oriented programming, Array-Oriented Programming with Arrays-Unique and Other Set Logic

as structured arrays, Structured and Record Arrays-Why Use Structured Arrays?

attributes for, Creating ndarrays, Reshaping Arrays, Broadcasting Over Other Axes, The Importance of Contiguous Memory

boolean indexing, Boolean Indexing-Boolean Indexing

broadcasting and, Arithmetic with NumPy Arrays, Repeating Elements: tile and repeat, Broadcasting-Setting Array Values by Broadcasting

C versus Fortan order, C Versus Fortran Order

C versus Fortran order, The Importance of Contiguous Memory

concatenating arrays, Concatenating and Splitting Arrays

creating, Creating ndarrays-Creating ndarrays

creating PeriodIndex from arrays, Creating a PeriodIndex from Arrays

data types for, Data Types for ndarrays-Data Types for ndarrays

fancy indexing, Fancy Indexing, Fancy Indexing Equivalents: take and put

file input and output, File Input and Output with Arrays

finding elements in sorted arrays, numpy.searchsorted: Finding Elements in a Sorted Array

indexes for, Basic Indexing and Slicing-Indexing with slices

internals overview, ndarray Object Internals-NumPy dtype Hierarchy

linear algebra and, Linear Algebra-Linear Algebra

partially sorting arrays, Partially Sorting Arrays

pseudorandom number generation, Pseudorandom Number Generation-Pseudorandom Number Generation

random walks example, Example: Random Walks-Simulating Many Random Walks at Once

repeating elements in, Repeating Elements: tile and repeat

reshaping arrays, Transposing Arrays and Swapping Axes, Reshaping Arrays

slicing arrays, Basic Indexing and Slicing-Indexing with slices

sorting considerations, Sorting, More About Sorting

splitting arrays, Concatenating and Splitting Arrays

storage options, HDF5 and Other Array Storage Options

swapping axes in, Transposing Arrays and Swapping Axes

transposing arrays, Transposing Arrays and Swapping Axes

ndim attribute, Creating ndarrays

nested code, Flat is better than nested

nested data types, Nested dtypes and Multidimensional Fields

nested list comprehensions, Nested list comprehensions-Nested list comprehensions

nested tuples, Unpacking tuples

New York MTA (Metropolitan Transportation Authority), Parsing XML with lxml.objectify

newaxis attribute, Broadcasting Over Other Axes

「no-op」statement, pass

None data type, Scalar Types, None, Handling Missing Data

normal function, Pseudorandom Number Generation

not keyword, Adding and removing elements

notfull method, Handling Missing Data

notnull method, Series

not_equal function, Universal Functions: Fast Element-Wise Array Functions

.npy file extension, File Input and Output with Arrays

.npz file extension, File Input and Output with Arrays

null value, Scalar Types, None, JSON Data

Numbacreating custom ufunc objects with, Creating Custom numpy.ufunc Objects with Numba

writing fast NumPy functions with, Writing Fast NumPy Functions with Numba-Creating Custom numpy.ufunc Objects with Numba

numeric data types, Numeric types

NumPy libraryabout, NumPy, NumPy Basics: Arrays and Vectorized Computation-NumPy Basics: Arrays and Vectorized Computation

advanced array input and output, Advanced Array Input and Output-HDF5 and Other Array Storage Options

advanced array manipulation, Advanced Array Manipulation-Fancy Indexing Equivalents: take and put

advanced ufunc usage, Advanced ufunc Usage-Writing New ufuncs in Python

array-oriented programming, Array-Oriented Programming with Arrays-Unique and Other Set Logic

arrays and broadcasting, Broadcasting-Setting Array Values by Broadcasting

file input and output with arrays, File Input and Output with Arrays

linear algebra and, Linear Algebra-Linear Algebra

ndarray object internals, ndarray Object Internals-NumPy dtype Hierarchy

ndarray object overview, The NumPy ndarray: A Multidimensional Array Object-Transposing Arrays and Swapping Axes

performance tips, Performance Tips-The Importance of Contiguous Memory

pseudorandom number generation, Pseudorandom Number Generation-Pseudorandom Number Generation

random walks example, Example: Random Walks-Simulating Many Random Walks at Once

sorting considerations, Sorting, More About Sorting-numpy.searchsorted: Finding Elements in a Sorted Array

structured and record arrays, Structured and Record Arrays-Why Use Structured Arrays?

ufunc overview, Universal Functions: Fast Element-Wise Array Functions-Universal Functions: Fast Element-Wise Array Functions

writing fast functions with Numba, Writing Fast NumPy Functions with Numba-Creating Custom numpy.ufunc Objects with Numba

O

object data type, Data Types for ndarrays

object introspection, Introspection-Introspection

object model, Everything is an object

objectify function, Parsing XML with lxml.objectify-Parsing XML with lxml.objectify

objects (see Python objects)

OHLC (Open-High-Low-Close) resampling, Open-High-Low-Close (OHLC) resampling

ohlc aggregate function, Open-High-Low-Close (OHLC) resampling

Oliphant, Travis, NumPy Basics: Arrays and Vectorized Computation

OLS (ordinary least squares) regression, Example: Group-Wise Linear Regression, Creating Model Descriptions with Patsy

OLS class, Estimating Linear Models

Olson database, Time Zone Handling

ones function, Creating ndarrays-Creating ndarrays

ones_like function, Creating ndarrays

open built-in function, Files and the Operating System, Bytes and Unicode with Files

openpyxl package, Reading Microsoft Excel Files

operating system, IPython interacting with, Interacting with the Operating System-Directory Bookmark System

or keyword, Booleans, Boolean Indexing

OS X, setting up Python on, Apple (OS X, macOS)

outer method, ufunc Instance Methods

outliers, detecting and filtering, Detecting and Filtering Outliers

output join type, Database-Style DataFrame Joins

output variables, Input and Output Variables

P

%p datetime format, Converting Between String and Datetime

packages, installing or updating, Installing or Updating Python Packages

pad method, Vectorized String Functions in pandas

%page magic function, About Magic Commands

pairplot function, Scatter or Point Plots

pairs plot, Scatter or Point Plots

pandas library, pandas(see also data wrangling)

about, pandas, Getting Started with pandas

arithmetic and data alignment, Arithmetic and Data Alignment-Operations between DataFrame and Series

as time zone naive, Time Zone Localization and Conversion

binary data formats, Binary Data Formats-Reading Microsoft Excel Files

categorical data and, Categorical Data-Creating dummy variables for modeling

data structures for, Introduction to pandas Data Structures-Index Objects

drop method, Dropping Entries from an Axis

filtering in, Indexing, Selection, and Filtering-Selection with loc and iloc

function application and mapping, Function Application and Mapping

group operations and, Advanced GroupBy Use-Grouped Time Resampling

indexes in, Indexing, Selection, and Filtering-Selection with loc and iloc, Axis Indexes with Duplicate Labels

integer indexing, Integer Indexes

interacting with databases, Interacting with Databases

interacting with Web APIs, Interacting with Web APIs

interfacing with model code, Interfacing Between pandas and Model Code

JSON data, JSON Data-JSON Data

method chaining, Techniques for Method Chaining-The pipe Method

nested data types and, Nested dtypes and Multidimensional Fields

plotting with, Plotting with pandas and seaborn-Facet Grids and Categorical Data

ranking data in, Sorting and Ranking-Sorting and Ranking

reading and writing data in text format, Reading and Writing Data in Text Format-Writing Data to Text Format

reductions in, Summarizing and Computing Descriptive Statistics-Unique Values, Value Counts, and Membership

reindex method, Reindexing-Reindexing

selecting data in, Indexing, Selection, and Filtering-Selection with loc and iloc

sorting considerations, Sorting and Ranking-Sorting and Ranking, Indirect Sorts: argsort and lexsort, numpy.searchsorted: Finding Elements in a Sorted Array

summary statistics in, Summarizing and Computing Descriptive Statistics-Unique Values, Value Counts, and Membership

vectorized string methods in, Vectorized String Functions in pandas-Vectorized String Functions in pandas

Web scraping, XML and HTML: Web Scraping-Parsing XML with lxml.objectify

working with delimited formats, Working with Delimited Formats-Working with Delimited Formats

pandas-datareader package, Correlation and Covariance

parentheses (), Function and object method calls, Tuple

parse method, Reading Microsoft Excel Files, Converting Between String and Datetime

partial argument application, Currying: Partial Argument Application

partial function, Currying: Partial Argument Application

partition method, Partially Sorting Arrays

pass statement, pass

%paste magic function, Executing Code from the Clipboard, About Magic Commands

patches, defined, Annotations and Drawing on a Subplot

Patsy libraryabout, Creating Model Descriptions with Patsy

categorical data and, Categorical Data and Patsy-Categorical Data and Patsy

creating model descriptions with, Creating Model Descriptions with Patsy-Creating Model Descriptions with Patsy

data transformations in Patsy formulas, Data Transformations in Patsy Formulas

pct_change method, Summarizing and Computing Descriptive Statistics, Example: Group Weighted Average and Correlation

%pdb magic function, About Magic Commands, Exceptions in IPython, Interactive Debugger

percent sign (%), About Magic Commands, Basic Profiling: %prun and %run -p

percentileofscore function, User-Defined Moving Window Functions

Pérez, Fernando, IPython and Jupyter

period (.), Tab Completion

Period class, Periods and Period Arithmetic

PeriodIndex class, Periods and Period Arithmetic, Creating a PeriodIndex from Arrays

periods of dates and timesabout, Periods and Period Arithmetic

converting frequencies, Period Frequency Conversion

converting timestamps to/from, Converting Timestamps to Periods (and Back)

creating PeriodIndex from arrays, Creating a PeriodIndex from Arrays

fixed periods, Time Series

quarterly period frequencies, Quarterly Period Frequencies

resampling with, Resampling with Periods

period_range function, Periods and Period Arithmetic, Quarterly Period Frequencies

Perktold, Josef, statsmodels

permutation function, Pseudorandom Number Generation, Permutation and Random Sampling

permutations function, itertools module

pickle module, Binary Data Formats

pinv function, Linear Algebra

pip tool, Installing or Updating Python Packages, XML and HTML: Web Scraping

pipe method, The pipe Method

pivot method, Pivoting「Long」to「Wide」Format

pivot tables, Data Aggregation and Group Operations, Pivot Tables and Cross-Tabulation-Cross-Tabulations: Crosstab

pivoting data, Pivoting「Long」to「Wide」Format-Pivoting「Wide」to「Long」Format

pivot_table method, Pivot Tables and Cross-Tabulation

plot function, Colors, Markers, and Line Styles

plot method, Line Plots-Line Plots

Plotly tool, Other Python Visualization Tools

plottingwith matplotlib, A Brief matplotlib API Primer-matplotlib Configuration

with pandas and seaborn, Plotting with pandas and seaborn-Facet Grids and Categorical Data

point plots, Scatter or Point Plots

pop method, Adding and removing elements, dict-Default values, set

%popd magic function, Interacting with the Operating System

positional arguments, Function and object method calls, Functions

pound sign (#), Comments

pow method, Arithmetic methods with fill values

power function, Universal Functions: Fast Element-Wise Array Functions

pprint module, Making Your Own Classes IPython-Friendly

predict method, Introduction to scikit-learn

preparation, data (see data wrangling)

private attributes, Tab Completion

private methods, Tab Completion

prod method, Summarizing and Computing Descriptive Statistics, Data Aggregation

product function, itertools module

profiles for IPython, Profiles and Configuration-Profiles and Configuration

profiling code in IPython, Basic Profiling: %prun and %run -p-Basic Profiling: %prun and %run -p

profiling functions line by line, Profiling a Function Line by Line-Profiling a Function Line by Line

%prun magic function, About Magic Commands, Basic Profiling: %prun and %run -p-Profiling a Function Line by Line

pseudocode, Jargon, Language Semantics

pseudorandom number generation, Pseudorandom Number Generation-Pseudorandom Number Generation

%pushd magic function, Interacting with the Operating System

put method, Fancy Indexing Equivalents: take and put

%pwd magic function, Interacting with the Operating System

.py file extension, The Python Interpreter, Imports

pyplot module, Ticks, Labels, and Legends

Pythoncommunity and conferences, Community and Conferences

control flow, Control Flow-Ternary expressions

data analysis with, Why Python for Data Analysis?-Why Not Python?, Python Language Basics, IPython, and Jupyter Notebooks-Python Language Basics, IPython, and Jupyter Notebooks

essential libraries, Essential Python Libraries-statsmodels

historical background, Python 2 and Python 3

import conventions, Import Conventions, Imports, The NumPy ndarray: A Multidimensional Array Object

installation and setup, Installation and Setup-Integrated Development Environments (IDEs) and Text Editors

interpreter for, The Python Interpreter

language semantics, Language Semantics-Mutable and immutable objects

scalar types, Scalar Types-Dates and times

python command, The Python Interpreter

Python objectsattributes and methods, Attributes and methods

converting to strings, Strings

defined, Everything is an object

formatting, Running the IPython Shell

functions as, Functions Are Objects-Functions Are Objects

key-value pairs, dict

pytz library, Time Zone Handling

Q

q(uit) debugger command, Interactive Debugger

qcut function, Discretization and Binning, Quantile and Bucket Analysis, Computations with Categoricals

qr function, Linear Algebra

quantile analysis, Quantile and Bucket Analysis

quantile method, Summarizing and Computing Descriptive Statistics, Data Aggregation

quarterly period frequencies, Quarterly Period Frequencies

question mark (?), Introspection-Introspection

%quickref magic function, About Magic Commands

quicksort method, Alternative Sort Algorithms

quotation marks in strings, Strings

R

r character prefacing quotes, Strings

R language, pandas, statsmodels, Handling Missing Data

radd method, Arithmetic methods with fill values

rand function, Pseudorandom Number Generation

randint function, Pseudorandom Number Generation

randn function, Boolean Indexing, Pseudorandom Number Generation

random module, Pseudorandom Number Generation-Simulating Many Random Walks at Once

random number generation, Pseudorandom Number Generation-Pseudorandom Number Generation

random sampling and permutation, Example: Random Sampling and Permutation

random walks example, Example: Random Walks-Simulating Many Random Walks at Once

RandomState class, Pseudorandom Number Generation

range function, range, Creating ndarrays

rank method, Sorting and Ranking

ranking data in pandas library, Sorting and Ranking-Sorting and Ranking

ravel method, Reshaping Arrays

rc method, matplotlib Configuration

rdiv method, Arithmetic methods with fill values

re module, Functions Are Objects, Regular Expressions

read method, Files and the Operating System-Files and the Operating System

read-and-write mode for files, Files and the Operating System

read-only mode for files, Files and the Operating System

reading datain Microsoft Excel files, Reading Microsoft Excel Files-Reading Microsoft Excel Files

in text format, Reading and Writing Data in Text Format-Reading Text Files in Pieces

readline functionality, Searching and Reusing the Command History

readlines method, Files and the Operating System

read_clipboard function, Reading and Writing Data in Text Format

read_csv function, Files and the Operating System, Reading and Writing Data in Text Format, Reading and Writing Data in Text Format, Bar Plots, Column-Wise and Multiple Function Application

read_excel function, Reading and Writing Data in Text Format, Reading Microsoft Excel Files

read_feather function, Reading and Writing Data in Text Format

read_fwf function, Reading and Writing Data in Text Format

read_hdf function, Reading and Writing Data in Text Format, Using HDF5 Format

read_html function, Reading and Writing Data in Text Format, XML and HTML: Web Scraping-Parsing XML with lxml.objectify

read_json function, Reading and Writing Data in Text Format, JSON Data

read_msgpack function, Reading and Writing Data in Text Format

read_pickle function, Reading and Writing Data in Text Format, Binary Data Formats

read_sas function, Reading and Writing Data in Text Format

read_sql function, Reading and Writing Data in Text Format, Interacting with Databases

read_stata function, Reading and Writing Data in Text Format

read_table function, Reading and Writing Data in Text Format, Reading and Writing Data in Text Format, Working with Delimited Formats

reduce method, ufunc Instance Methods

reduceat method, ufunc Instance Methods

reductions (aggregations), Mathematical and Statistical Methods

references in Python, Variables and argument passing-Dynamic references, strong types

regplot method, Scatter or Point Plots

regress function, Example: Group-Wise Linear Regression

regular expressionspasses as delimiters, Reading and Writing Data in Text Format

string manipulation and, Regular Expressions-Regular Expressions

reindex method, Reindexing-Reindexing, Selection with loc and iloc, Axis Indexes with Duplicate Labels, Upsampling and Interpolation

reload function, Reloading Module Dependencies

remove method, Adding and removing elements, set

remove_categories method, Categorical Methods

remove_unused_categories method, Categorical Methods

rename method, Renaming Axis Indexes

rename_categories method, Categorical Methods

reorder_categories method, Categorical Methods

repeat function, Repeating Elements: tile and repeat

repeat method, Vectorized String Functions in pandas

replace method, Replacing Values, String Object Methods-String Object Methods, Vectorized String Functions in pandas

requests package, Interacting with Web APIs

resample method, Date Ranges, Frequencies, and Shifting, Resampling and Frequency Conversion-Open-High-Low-Close (OHLC) resampling, Grouped Time Resampling

resamplingdefined, Resampling and Frequency Conversion

downsampling and, Resampling and Frequency Conversion-Open-High-Low-Close (OHLC) resampling

OHLC, Open-High-Low-Close (OHLC) resampling

upsampling and, Resampling and Frequency Conversion, Upsampling and Interpolation

with periods, Resampling with Periods

%reset magic function, About Magic Commands, Input and Output Variables

reset_index method, Pivoting「Wide」to「Long」Format, Returning Aggregated Data Without Row Indexes

reshape method, Fancy Indexing, Reshaping Arrays

*rest syntax, Unpacking tuples

return statement, Functions

reusing command history, Searching and Reusing the Command History

reversed function, reversed

rfind method, String Object Methods

rfloordiv method, Arithmetic methods with fill values

right join type, Database-Style DataFrame Joins

rint function, Universal Functions: Fast Element-Wise Array Functions

rjust method, String Object Methods

rmul method, Arithmetic methods with fill values

rollback method, Shifting dates with offsets

rollforward method, Shifting dates with offsets

rolling function, Moving Window Functions, Moving Window Functions

rolling_corr function, Binary Moving Window Functions

row major order (C order), C Versus Fortran Order, The Importance of Contiguous Memory

row_stack function, Concatenating and Splitting Arrays

rpow method, Arithmetic methods with fill values

rstrip method, String Object Methods, Vectorized String Functions in pandas

rsub method, Arithmetic methods with fill values

%run magic functionabout, About Magic Commands

exceptions and, Exceptions in IPython

interactive debugger and, Interactive Debugger, Other ways to make use of the debugger

IPython and, The Python Interpreter, The %run Command-Interrupting running code

reusing command history with, Searching and Reusing the Command History

r_ object, Stacking helpers: r_ and c_

S

%S datetime format, Dates and times, Converting Between String and Datetime

s(tep) debugger command, Interactive Debugger

sample method, Permutation and Random Sampling, Example: Random Sampling and Permutation

save function, File Input and Output with Arrays, Advanced Array Input and Output

savefig method, Saving Plots to File

savez function, File Input and Output with Arrays

savez_compressed function, File Input and Output with Arrays

scalar types in Python, Scalar Types-Dates and times, Arithmetic with NumPy Arrays

scatter plot matrix, Scatter or Point Plots

scatter plots, Scatter or Point Plots

scikit-learn library, scikit-learn, Introduction to scikit-learn-Introduction to scikit-learn

SciPy library, SciPy

scope of functions, Namespaces, Scope, and Local Functions

scripting languages, Why Python for Data Analysis?

Seabold, Skipper, statsmodels

seaborn library, Plotting with pandas and seaborn

search method, Regular Expressions, Regular Expressions

searchingbinary searches of lists, Binary search and maintaining a sorted list

command history, Searching and Reusing the Command History

searchsorted method, numpy.searchsorted: Finding Elements in a Sorted Array

seed function, Pseudorandom Number Generation

seek method, Files and the Operating System, Files and the Operating System-Bytes and Unicode with Files

semantics, language (see language semantics for Python)

semicolon (;), Indentation, not braces

sentinel value, Reading and Writing Data in Text Format, Handling Missing Data

sequence functions, Built-in Sequence Functions-reversed

serialization (see storing data)

Series data structureabout, pandas, Series-Series

duplicate indexes example, Axis Indexes with Duplicate Labels

grouping with, Grouping with Dicts and Series

JSON data and, JSON Data

operations between DataFrame and, Operations between DataFrame and Series

plot method arguments, Line Plots

ranking data in, Sorting and Ranking

sorting considerations, Sorting and Ranking, Indirect Sorts: argsort and lexsort

summary statistics methods for, Correlation and Covariance

set comprehensions, List, Set, and Dict Comprehensions

set function, set, Bar Plots

set literals, set

set operations, set-set, Unique and Other Set Logic

setattr function, Attributes and methods

setdefault method, Default values

setdiff1d method, Unique and Other Set Logic

sets (data structures), set-set

setxor1d method, Unique and Other Set Logic

set_categories method, Categorical Methods

set_index method, Pivoting「Long」to「Wide」Format

set_title method, Setting the title, axis labels, ticks, and ticklabels, Annotations and Drawing on a Subplot

set_trace function, Other ways to make use of the debugger

set_value method, Selection with loc and iloc

set_xlabel method, Setting the title, axis labels, ticks, and ticklabels

set_xlim method, Annotations and Drawing on a Subplot

set_xticklabels method, Setting the title, axis labels, ticks, and ticklabels

set_xticks method, Setting the title, axis labels, ticks, and ticklabels

set_ylim method, Annotations and Drawing on a Subplot

shape attribute, The NumPy ndarray: A Multidimensional Array Object-Creating ndarrays, Reshaping Arrays

shell commands in IPython, Shell Commands and Aliases

shift method, Shifting (Leading and Lagging) Data, Downsampling

shifting time series data, Shifting (Leading and Lagging) Data-Shifting dates with offsets

shuffle function, Pseudorandom Number Generation

side effects, Mutable and immutable objects

sign function, Universal Functions: Fast Element-Wise Array Functions, Detecting and Filtering Outliers

sin function, Universal Functions: Fast Element-Wise Array Functions

sinh function, Universal Functions: Fast Element-Wise Array Functions

size method, GroupBy Mechanics

skew method, Summarizing and Computing Descriptive Statistics

skipna method, Summarizing and Computing Descriptive Statistics

slice method, Vectorized String Functions in pandas

slice notation, Slicing

slicinglists, Slicing

ndarrays, Basic Indexing and Slicing-Indexing with slices

strings, Strings

Smith, Nathaniel, statsmodels

Social Security Administration (SSA), US Baby Names 1880–2010

software development tools for IPythonabout, Software Development Tools

basic profiling, Basic Profiling: %prun and %run -p-Basic Profiling: %prun and %run -p

interactive debugger, Interactive Debugger-Other ways to make use of the debugger

profiling functions line by line, Profiling a Function Line by Line-Profiling a Function Line by Line

timing code, Timing Code: %time and %timeit-Timing Code: %time and %timeit

solve function, Linear Algebra

sort method, Sorting, sorted, Anonymous (Lambda) Functions, Sorting

sorted function, Sorting, sorted

sorting considerationsfinding elements in sorted arrays, numpy.searchsorted: Finding Elements in a Sorted Array

hierarchical indexing, Reordering and Sorting Levels

in-place sorts, Sorting, More About Sorting

indirect sorts, Indirect Sorts: argsort and lexsort

missing data, Sorting and Ranking

NumPy library, Sorting, More About Sorting-numpy.searchsorted: Finding Elements in a Sorted Array

pandas library, Sorting and Ranking-Sorting and Ranking, Indirect Sorts: argsort and lexsort, numpy.searchsorted: Finding Elements in a Sorted Array

partially sorting arrays, Partially Sorting Arrays

stable sorting, Alternative Sort Algorithms

sort_index method, Sorting and Ranking

sort_values method, Sorting and Ranking, Indirect Sorts: argsort and lexsort

spaces, structuring code with, Indentation, not braces

split concatenation function, Concatenating and Splitting Arrays

split function, Concatenating and Splitting Arrays

split method, Working with Delimited Formats, String Object Methods, String Object Methods-Regular Expressions, Regular Expressions, Vectorized String Functions in pandas

split-apply-combineabout, GroupBy Mechanics

applying, Apply: General split-apply-combine-Example: Group-Wise Linear Regression

filling missing values with group-specific values, Example: Filling Missing Values with Group-Specific Values

group weighted average and correlation, Example: Group Weighted Average and Correlation

group-wise linear regression, Example: Group-Wise Linear Regression

quantile and bucket analysis, Quantile and Bucket Analysis

random sampling and permutation, Example: Random Sampling and Permutation

suppressing group keys, Suppressing the Group Keys

SQL (structured query language), Data Aggregation and Group Operations

SQLAlchemy project, Interacting with Databases

sqlite3 module, Interacting with Databases

sqrt function, Universal Functions: Fast Element-Wise Array Functions

square brackets [], Tuple, List

square function, Universal Functions: Fast Element-Wise Array Functions

SSA (Social Security Administration), US Baby Names 1880–2010

stable sorting, Alternative Sort Algorithms

stack method, Reshaping with Hierarchical Indexing

stacked format, Pivoting「Long」to「Wide」Format

stacking operation, Combining and Merging Datasets, Concatenating Along an Axis

start index, Slicing

startswith method, String Object Methods, Vectorized String Functions in pandas

Stata file format, Reading and Writing Data in Text Format

statistical methods, Mathematical and Statistical Methods-Mathematical and Statistical Methods

statsmodels libraryabout, statsmodels, Introduction to statsmodels

estimating linear models, Estimating Linear Models-Estimating Linear Models

estimating time series processes, Estimating Time Series Processes

OLS regression and, Example: Group-Wise Linear Regression

std method, Mathematical and Statistical Methods, Summarizing and Computing Descriptive Statistics, Data Aggregation

step index, Slicing

stop index, Slicing

storing datain binary format, Binary Data Formats-Reading Microsoft Excel Files

in databases, Pivoting「Long」to「Wide」Format

ndarray object, HDF5 and Other Array Storage Options

str data type, Scalar Types, Type casting

str function, Strings, Type casting, Converting Between String and Datetime

strftime method, Dates and times, Converting Between String and Datetime

strides/strided view, ndarray Object Internals

stringsconcatenating, Strings

converting between datetime and, Converting Between String and Datetime-Converting Between String and Datetime

converting Python objects to, Strings

data types for, Strings-Strings

formatting, Strings

manipulating, String Manipulation-Vectorized String Functions in pandas

methods for, String Object Methods-String Object Methods

regular expressions and, Regular Expressions-Regular Expressions

slicing, Strings

vectorized methods in pandas, Vectorized String Functions in pandas-Vectorized String Functions in pandas

string_ data type, Data Types for ndarrays

strip method, String Object Methods, String Object Methods, Vectorized String Functions in pandas

strongly typed language, Dynamic references, strong types

strptime function, Dates and times, Converting Between String and Datetime

structured arrays, Structured and Record Arrays-Why Use Structured Arrays?

structured data, What Kinds of Data?

sub method, Arithmetic methods with fill values, Regular Expressions, Regular Expressions

subn method, Regular Expressions

subplotsabout, Figures and Subplots-Adjusting the spacing around subplots

drawing on, Annotations and Drawing on a Subplot-Annotations and Drawing on a Subplot

subplots method, Figures and Subplots

subplots_adjust method, Adjusting the spacing around subplots

subsetting time series data, Indexing, Selection, Subsetting

subtract function, Universal Functions: Fast Element-Wise Array Functions

sum method, Mathematical and Statistical Methods, Summarizing and Computing Descriptive Statistics, Summarizing and Computing Descriptive Statistics, Data Aggregation, ufunc Instance Methods

summary method, Estimating Linear Models

summary statisticsabout, Summarizing and Computing Descriptive Statistics-Summarizing and Computing Descriptive Statistics

by level, Summary Statistics by Level

correlation and covariance, Correlation and Covariance-Correlation and Covariance

methods for, Unique Values, Value Counts, and Membership-Unique Values, Value Counts, and Membership

svd function, Linear Algebra

swapaxes method, Transposing Arrays and Swapping Axes

swapping axes in arrays, Transposing Arrays and Swapping Axes

symmetric_difference method, set

symmetric_difference_update method, set

syntactic sugar, Jargon

sys module, Files and the Operating System, Writing Data to Text Format

T

T attribute, Transposing Arrays and Swapping Axes

tab completion in IPython, Tab Completion-Tab Completion

tabs, structuring code with, Indentation, not braces

take method, Permutation and Random Sampling, Background and Motivation, Fancy Indexing Equivalents: take and put

tan function, Universal Functions: Fast Element-Wise Array Functions

tanh function, Universal Functions: Fast Element-Wise Array Functions

Taylor, Jonathan, statsmodels

tell method, Files and the Operating System, Files and the Operating System

ternary expressions, Ternary expressions

text editors, Integrated Development Environments (IDEs) and Text Editors

text filesreading, Reading and Writing Data in Text Format-Reading Text Files in Pieces

text mode for files, Files and the Operating System-Bytes and Unicode with Files

writing to, Reading and Writing Data in Text Format-Writing Data to Text Format

text function, Annotations and Drawing on a Subplot

TextParser class, Reading Text Files in Pieces

tick mark selection in matplotlib, Ticks, Labels, and Legends-Setting the title, axis labels, ticks, and ticklabels

tile function, Repeating Elements: tile and repeat

time data type, Dates and times, Date and Time Data Types and Tools

%time magic function, About Magic Commands, Timing Code: %time and %timeit

time module, Date and Time Data Types and Tools

time series dataabout, Time Series

basics overview, Time Series Basics-Time Series Basics

date offsets and, Frequencies and Date Offsets, Shifting dates with offsets-Shifting dates with offsets

estimating time series processes, Estimating Time Series Processes

frequences and, Generating Date Ranges

frequencies and, Frequencies and Date Offsets, Resampling and Frequency Conversion-Resampling with Periods

indexing and, Indexing, Selection, Subsetting

moving window functions, Moving Window Functions-User-Defined Moving Window Functions

periods in, Periods and Period Arithmetic-Creating a PeriodIndex from Arrays

resampling, Resampling and Frequency Conversion-Resampling with Periods

selecting, Indexing, Selection, Subsetting

shifting, Shifting (Leading and Lagging) Data-Shifting dates with offsets

subsetting, Indexing, Selection, Subsetting

time zone handling, Time Zone Handling-Operations Between Different Time Zones

with duplicate indexes, Time Series with Duplicate Indices

time zonesabout, Time Zone Handling

converting data to, Time Zone Localization and Conversion

localizing data to, Time Zone Localization and Conversion

operations between different, Operations Between Different Time Zones

operations with timestamp objects, Operations with Time Zone−Aware Timestamp Objects

USA.gov dataset example, Counting Time Zones in Pure Python-Counting Time Zones with pandas

time, programmer versus CPU, Why Not Python?

timedelta data type, Time Series-Date and Time Data Types and Tools

TimeGrouper object, Grouped Time Resampling

%timeit magic function, About Magic Commands, The Importance of Contiguous Memory, Timing Code: %time and %timeit

Timestamp object, Time Series Basics, Shifting dates with offsets, Operations with Time Zone−Aware Timestamp Objects

timestampsconverting periods to/from, Converting Timestamps to Periods (and Back)

defined, Time Series

operations with time-zone–aware objects, Operations with Time Zone−Aware Timestamp Objects

timezone method, Time Zone Handling

timing code, Timing Code: %time and %timeit-Timing Code: %time and %timeit

top function, Apply: General split-apply-combine

to_csv method, Writing Data to Text Format

to_datetime method, Converting Between String and Datetime

to_excel method, Reading Microsoft Excel Files

to_json method, JSON Data

to_period method, Converting Timestamps to Periods (and Back)

to_pickle method, Binary Data Formats

to_timestamp method, Converting Timestamps to Periods (and Back)

trace function, Linear Algebra

transform method, Group Transforms and「Unwrapped」GroupBys-Group Transforms and「Unwrapped」GroupBys

transforming dataabout, Data Transformation

computing indicator/dummy variables, Computing Indicator/Dummy Variables-Computing Indicator/Dummy Variables

detecting and filtering outliers, Detecting and Filtering Outliers

discretization and binning, Discretization and Binning

in Patsy formulas, Data Transformations in Patsy Formulas

permutation and random sampling, Permutation and Random Sampling

removing duplicates, Removing Duplicates

renaming axis indexes, Renaming Axis Indexes

replacing values, Replacing Values

using functions or mapping, Transforming Data Using a Function or Mapping

transpose method, Transposing Arrays and Swapping Axes

transposing arrays, Transposing Arrays and Swapping Axes

truncate method, Indexing, Selection, Subsetting

try/except blocks, Errors and Exception Handling-Errors and Exception Handling

tuples (data structures)about, Tuple

methods for, Tuple methods

nested, Unpacking tuples

unpacking, Unpacking tuples

「two-language」problem, Solving the「Two-Language」Problem

type casting, Type casting

type inference in functions, Reading and Writing Data in Text Format

TypeError exception, Errors and Exception Handling

tzinfo data type, Date and Time Data Types and Tools

tz_convert method, Time Zone Localization and Conversion

U

%U datetime format, Dates and times, Converting Between String and Datetime

u(p) debugger command, Interactive Debugger

ufuncs (see universal functions)

uint16 data type, Data Types for ndarrays

uint32 data type, Data Types for ndarrays

uint64 data type, Data Types for ndarrays

uint8 data type, Data Types for ndarrays

unary universal functions, Universal Functions: Fast Element-Wise Array Functions, Universal Functions: Fast Element-Wise Array Functions

underscore (_), Tab Completion, Unpacking tuples, NumPy dtype Hierarchy

undescore (_), Input and Output Variables

Unicode standard, Strings, Bytes and Unicode, Bytes and Unicode with Files

unicode_ data type, Data Types for ndarrays

uniform function, Pseudorandom Number Generation

union method, set-set, Index Objects

union1d method, Unique and Other Set Logic

unique method, Unique and Other Set Logic-Unique and Other Set Logic, Index Objects, Unique Values, Value Counts, and Membership, Unique Values, Value Counts, and Membership, Background and Motivation

universal functionsapplying and mapping, Function Application and Mapping

comprehensive overview, Universal Functions: Fast Element-Wise Array Functions-Universal Functions: Fast Element-Wise Array Functions

creating custom objects with Numba, Creating Custom numpy.ufunc Objects with Numba

instance methods, ufunc Instance Methods-ufunc Instance Methods

writing in Python, Writing New ufuncs in Python

unpacking tuples, Unpacking tuples

unstack method, Reshaping with Hierarchical Indexing

unwrapped group operation, Group Transforms and「Unwrapped」GroupBys

update method, dict, set

updating packages, Installing or Updating Python Packages

upper method, String Object Methods, Vectorized String Functions in pandas

upsampling, Resampling and Frequency Conversion, Upsampling and Interpolation

US baby names dataset example, US Baby Names 1880–2010-Boy names that became girl names (and vice versa)

US Federal Election Commission database example, 2012 Federal Election Commission Database-Donation Statistics by State

USA.gov dataset example, 1.USA.gov Data from Bitly-Counting Time Zones with pandas

USDA food database example, USDA Food Database-USDA Food Database

UTC (coordinated universal time), Time Zone Handling

UTF-8 encoding, Bytes and Unicode with Files

V

ValueError exception, Errors and Exception Handling, Data Types for ndarrays

values attribute, DataFrame

values method, dict, Pivot Tables and Cross-Tabulation

values property, Interfacing Between pandas and Model Code

value_count method, Discretization and Binning

value_counts method, Unique Values, Value Counts, and Membership, Bar Plots, Background and Motivation

var method, Mathematical and Statistical Methods, Summarizing and Computing Descriptive Statistics, Data Aggregation

variablesdummy, Computing Indicator/Dummy Variables-Computing Indicator/Dummy Variables, Creating dummy variables for modeling, Interfacing Between pandas and Model Code, Categorical Data and Patsy

function scope and, Namespaces, Scope, and Local Functions

in Python, Variables and argument passing-Dynamic references, strong types

indicator, Computing Indicator/Dummy Variables-Computing Indicator/Dummy Variables

input, Input and Output Variables

output, Input and Output Variables

shell commands and, Shell Commands and Aliases

vectorization, Arithmetic with NumPy Arrays

vectorize function, Writing New ufuncs in Python, Creating Custom numpy.ufunc Objects with Numba

vectorized string methods in pandas, Vectorized String Functions in pandas-Vectorized String Functions in pandas

visualization tools, Other Python Visualization Tools

vsplit function, Concatenating and Splitting Arrays

vstack function, Concatenating and Splitting Arrays

W

%w datetime format, Dates and times, Converting Between String and Datetime

%W datetime format, Dates and times, Converting Between String and Datetime

w(here) debugger command, Interactive Debugger

Waskom, Michael, Plotting with pandas and seaborn

Wattenberg, Laura, The「last letter」revolution

Web APIs, pandas interacting with, Interacting with Web APIs

Web scraping, XML and HTML: Web Scraping-Parsing XML with lxml.objectify

where function, Expressing Conditional Logic as Array Operations, Combining Data with Overlap

while loops, while loops

whitespaceregular expression describing, Regular Expressions

structuring code with, Indentation, not braces

trimming around figures, Saving Plots to File

%who magic function, About Magic Commands

%whos magic function, About Magic Commands

%who_ls magic function, About Magic Commands

Wickham, Hadley, Binary Data Formats, GroupBy Mechanics, US Baby Names 1880–2010

wildcard expressions, Introspection

Williams, Ashley, USDA Food Database

Windows, setting up Python on, Windows

with statement, Files and the Operating System

wrangling (see data wrangling)

write method, Files and the Operating System

write-only mode for files, Files and the Operating System

writelines method, Files and the Operating System-Files and the Operating System

writing data in text format, Reading and Writing Data in Text Format-Writing Data to Text Format

X

%x datetime format, Converting Between String and Datetime

%X datetime format, Converting Between String and Datetime

%xdel magic function, About Magic Commands, Input and Output Variables

xlim method, Ticks, Labels, and Legends

xlrd package, Reading Microsoft Excel Files

XLS files, Reading Microsoft Excel Files

XLSX files, Reading Microsoft Excel Files

XML files, XML and HTML: Web Scraping-Parsing XML with lxml.objectify

%xmode magic function, Exceptions in IPython

Y

%Y datetime format, Dates and times, Converting Between String and Datetime

%y datetime format, Dates and times, Converting Between String and Datetime

yield keyword, Generators

Z

%z datetime format, Dates and times, Converting Between String and Datetime

"zero-copy" array views, ndarray Object Internals

zeros function, Creating ndarrays-Creating ndarrays

zeros_like function, Creating ndarrays

zip function, zip

About the Author

Wes McKinney is a New York-based software developer and entrepreneur. After finishing his undergraduate degree in mathematics at MIT in 2007, he went on to do quantitative finance work at AQR Capital Management in Greenwich, CT. Frustrated by cumbersome data analysis tools, he learned Python and started building what would later become the pandas project. He’s now an active member of the Python data community and is an advocate for the use of Python in data analysis, finance, and statistical computing applications.

Wes was later the cofounder and CEO of DataPad, whose technology assets and team were acquired by Cloudera in 2014. He has since become involved in big data technology, joining the Project Management Committees for the Apache Arrow and Apache Parquet projects in the Apache Software Foundation. In 2016, he joined Two Sigma Investments in New York City, where he continues working to make data analysis faster and easier through open source software.

Colophon

The animal on the cover of Python for Data Analysis is a golden-tailed, or pen-tailed, tree shrew (Ptilocercus lowii). The golden-tailed tree shrew is the only one of its species in the genus Ptilocercus and family Ptilocercidae; all the other tree shrews are of the family Tupaiidae. Tree shrews are identified by their long tails and soft red-brown fur. As nicknamed, the golden-tailed tree shrew has a tail that resembles the feather on a quill pen. Tree shrews are omnivores, feeding primarily on insects, fruit, seeds, and small vertebrates.

Found predominantly in Indonesia, Malaysia, and Thailand, these wild mammals are known for their chronic consumption of alcohol. Malaysian tree shrews were found to spend several hours consuming the naturally fermented nectar of the bertam palm, equalling about 10 to 12 glasses of wine with 3.8% alcohol content. Despite this, no golden-tailed tree shrew has ever been intoxicated, thanks largely to their impressive ability to break down ethanol, which includes metabolizing the alcohol in a way not used by humans. Also more impressive than any of their mammal counterparts, including humans? Brain-to-body mass ratio.

Despite these mammals’ name, the golden-tailed shrew is not a true shrew, instead more closely related to primates. Because of their close relation, tree shrews have become an alternative to primates in medical experimentation for myopia, psychosocial stress, and hepatitis.

The cover image is from Cassell’s Natural History. The cover fonts are URW Typewriter and Guardian Sans. The text font is Adobe Minion Pro; the heading font is Adobe Myriad Condensed; and the code font is Dalton Maag’s Ubuntu Mono.

PrefaceNew for the Second Edition

Conventions Used in This Book

Using Code Examples

O’Reilly Safari

How to Contact Us

AcknowledgmentsIn Memoriam: John D. Hunter (1968–2012)

Acknowledgments for the Second Edition (2017)

Acknowledgments for the First Edition (2012)

Preliminaries1.1 What Is This Book About?What Kinds of Data?

1.2 Why Python for Data Analysis?Python as Glue

Solving the「Two-Language」Problem

Why Not Python?

1.3 Essential Python LibrariesNumPy

pandas

matplotlib

IPython and Jupyter

SciPy

scikit-learn

statsmodels

1.4 Installation and SetupWindows

Apple (OS X, macOS)

GNU/Linux

Installing or Updating Python Packages

Python 2 and Python 3

Integrated Development Environments (IDEs) and Text Editors

1.5 Community and Conferences

1.6 Navigating This BookCode Examples

Data for Examples

Import Conventions

Jargon

Python Language Basics, IPython, and Jupyter Notebooks2.1 The Python Interpreter

2.2 IPython BasicsRunning the IPython Shell

Running the Jupyter Notebook

Tab Completion

Introspection

The %run Command

Executing Code from the Clipboard

Terminal Keyboard Shortcuts

About Magic Commands

Matplotlib Integration

2.3 Python Language BasicsLanguage Semantics

Scalar Types

Control Flow

Built-in Data Structures, Functions, and Files3.1 Data Structures and SequencesTuple

List

Built-in Sequence Functions

dict

set

List, Set, and Dict Comprehensions

3.2 FunctionsNamespaces, Scope, and Local Functions

Returning Multiple Values

Functions Are Objects

Anonymous (Lambda) Functions

Currying: Partial Argument Application

Generators

Errors and Exception Handling

3.3 Files and the Operating SystemBytes and Unicode with Files

3.4 Conclusion

NumPy Basics: Arrays and Vectorized Computation4.1 The NumPy ndarray: A Multidimensional Array ObjectCreating ndarrays

Data Types for ndarrays

Arithmetic with NumPy Arrays

Basic Indexing and Slicing

Boolean Indexing

Fancy Indexing

Transposing Arrays and Swapping Axes

4.2 Universal Functions: Fast Element-Wise Array Functions

4.3 Array-Oriented Programming with ArraysExpressing Conditional Logic as Array Operations

Mathematical and Statistical Methods

Methods for Boolean Arrays

Sorting

Unique and Other Set Logic

4.4 File Input and Output with Arrays

4.5 Linear Algebra

4.6 Pseudorandom Number Generation

4.7 Example: Random WalksSimulating Many Random Walks at Once

4.8 Conclusion

Getting Started with pandas5.1 Introduction to pandas Data StructuresSeries

DataFrame

Index Objects

5.2 Essential FunctionalityReindexing

Dropping Entries from an Axis

Indexing, Selection, and Filtering

Integer Indexes

Arithmetic and Data Alignment

Function Application and Mapping

Sorting and Ranking

Axis Indexes with Duplicate Labels

5.3 Summarizing and Computing Descriptive StatisticsCorrelation and Covariance

Unique Values, Value Counts, and Membership

5.4 Conclusion

Data Loading, Storage, and File Formats6.1 Reading and Writing Data in Text FormatReading Text Files in Pieces

Writing Data to Text Format

Working with Delimited Formats

JSON Data

XML and HTML: Web Scraping

6.2 Binary Data FormatsUsing HDF5 Format

Reading Microsoft Excel Files

6.3 Interacting with Web APIs

6.4 Interacting with Databases

6.5 Conclusion

Data Cleaning and Preparation7.1 Handling Missing DataFiltering Out Missing Data

Filling In Missing Data

7.2 Data TransformationRemoving Duplicates

Transforming Data Using a Function or Mapping

Replacing Values

Renaming Axis Indexes

Discretization and Binning

Detecting and Filtering Outliers

Permutation and Random Sampling

Computing Indicator/Dummy Variables

7.3 String ManipulationString Object Methods

Regular Expressions

Vectorized String Functions in pandas

7.4 Conclusion

Data Wrangling: Join, Combine, and Reshape8.1 Hierarchical IndexingReordering and Sorting Levels

Summary Statistics by Level

Indexing with a DataFrame’s columns

8.2 Combining and Merging DatasetsDatabase-Style DataFrame Joins

Merging on Index

Concatenating Along an Axis

Combining Data with Overlap

8.3 Reshaping and PivotingReshaping with Hierarchical Indexing

Pivoting「Long」to「Wide」Format

Pivoting「Wide」to「Long」Format

8.4 Conclusion

Plotting and Visualization9.1 A Brief matplotlib API PrimerFigures and Subplots

Colors, Markers, and Line Styles

Ticks, Labels, and Legends

Annotations and Drawing on a Subplot

Saving Plots to File

matplotlib Configuration

9.2 Plotting with pandas and seabornLine Plots

Bar Plots

Histograms and Density Plots

Scatter or Point Plots

Facet Grids and Categorical Data

9.3 Other Python Visualization Tools

9.4 Conclusion

Data Aggregation and Group Operations10.1 GroupBy MechanicsIterating Over Groups

Selecting a Column or Subset of Columns

Grouping with Dicts and Series

Grouping with Functions

Grouping by Index Levels

10.2 Data AggregationColumn-Wise and Multiple Function Application

Returning Aggregated Data Without Row Indexes

10.3 Apply: General split-apply-combineSuppressing the Group Keys

Quantile and Bucket Analysis

Example: Filling Missing Values with Group-Specific Values

Example: Random Sampling and Permutation

Example: Group Weighted Average and Correlation

Example: Group-Wise Linear Regression

10.4 Pivot Tables and Cross-TabulationCross-Tabulations: Crosstab

10.5 Conclusion

Time Series11.1 Date and Time Data Types and ToolsConverting Between String and Datetime

11.2 Time Series BasicsIndexing, Selection, Subsetting

Time Series with Duplicate Indices

11.3 Date Ranges, Frequencies, and ShiftingGenerating Date Ranges

Frequencies and Date Offsets

Shifting (Leading and Lagging) Data

11.4 Time Zone HandlingTime Zone Localization and Conversion

Operations with Time Zone−Aware Timestamp Objects

Operations Between Different Time Zones

11.5 Periods and Period ArithmeticPeriod Frequency Conversion

Quarterly Period Frequencies

Converting Timestamps to Periods (and Back)

Creating a PeriodIndex from Arrays

11.6 Resampling and Frequency ConversionDownsampling

Upsampling and Interpolation

Resampling with Periods

11.7 Moving Window FunctionsExponentially Weighted Functions

Binary Moving Window Functions

User-Defined Moving Window Functions

11.8 Conclusion

Advanced pandas12.1 Categorical DataBackground and Motivation

Categorical Type in pandas

Computations with Categoricals

Categorical Methods

12.2 Advanced GroupBy UseGroup Transforms and「Unwrapped」GroupBys

Grouped Time Resampling

12.3 Techniques for Method ChainingThe pipe Method

12.4 Conclusion

Introduction to Modeling Libraries in Python13.1 Interfacing Between pandas and Model Code

13.2 Creating Model Descriptions with PatsyData Transformations in Patsy Formulas

Categorical Data and Patsy

13.3 Introduction to statsmodelsEstimating Linear Models

Estimating Time Series Processes

13.4 Introduction to scikit-learn

13.5 Continuing Your Education

Data Analysis Examples14.1 1.USA.gov Data from BitlyCounting Time Zones in Pure Python

Counting Time Zones with pandas

14.2 MovieLens 1M DatasetMeasuring Rating Disagreement

14.3 US Baby Names 1880–2010Analyzing Naming Trends

14.4 USDA Food Database

14.5 2012 Federal Election Commission DatabaseDonation Statistics by Occupation and Employer

Bucketing Donation Amounts

Donation Statistics by State

14.6 Conclusion

Advanced NumPyA.1 ndarray Object InternalsNumPy dtype Hierarchy

A.2 Advanced Array ManipulationReshaping Arrays

C Versus Fortran Order

Concatenating and Splitting Arrays

Repeating Elements: tile and repeat

Fancy Indexing Equivalents: take and put

A.3 BroadcastingBroadcasting Over Other Axes

Setting Array Values by Broadcasting

A.4 Advanced ufunc Usageufunc Instance Methods

Writing New ufuncs in Python

A.5 Structured and Record ArraysNested dtypes and Multidimensional Fields

Why Use Structured Arrays?

A.6 More About SortingIndirect Sorts: argsort and lexsort

Alternative Sort Algorithms

Partially Sorting Arrays

numpy.searchsorted: Finding Elements in a Sorted Array

A.7 Writing Fast NumPy Functions with NumbaCreating Custom numpy.ufunc Objects with Numba

A.8 Advanced Array Input and OutputMemory-Mapped Files

HDF5 and Other Array Storage Options

A.9 Performance TipsThe Importance of Contiguous Memory

More on the IPython SystemB.1 Using the Command HistorySearching and Reusing the Command History

Input and Output Variables

B.2 Interacting with the Operating SystemShell Commands and Aliases

Directory Bookmark System

B.3 Software Development ToolsInteractive Debugger

Timing Code: %time and %timeit

Basic Profiling: %prun and %run -p

Profiling a Function Line by Line

B.4 Tips for Productive Code Development Using IPythonReloading Module Dependencies

Code Design Tips

B.5 Advanced IPython FeaturesMaking Your Own Classes IPython-Friendly

Profiles and Configuration

B.6 Conclusion

Index


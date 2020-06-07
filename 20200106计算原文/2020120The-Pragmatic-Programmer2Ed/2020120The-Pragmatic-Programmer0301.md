# 03. The Basic Tools

Every maker starts their journey with a basic set of good-quality tools. A woodworker might need rules, gauges, a couple of saws, some good planes, fine chisels, drills and braces, mallets, and clamps. These tools will be lovingly chosen, will be built to last, will perform specific jobs with little overlap with other tools, and, perhaps most importantly, will feel right in the budding woodworker’s hands.

Then begins a process of learning and adaptation. Each tool will have its own personality and quirks, and will need its own

special handling. Each must be sharpened in a unique way, or held just so. Over time, each will wear according to use, until the grip looks like a mold of the woodworker’s hands and the

cutting surface aligns perfectly with the angle at which the tool is held. At this point, the tools become conduits from the

maker’s brain to the finished product—they have become

extensions of their hands. Over time, the woodworker will add new tools, such as biscuit cutters, laser-guided miter saws, dovetail jigs—all wonderful pieces of technology. But you can bet that they’ll be happiest with one of those original tools in hand, feeling the plane sing as it slides through the wood.

Tools amplify your talent. The better your tools, and the better

you know how to use them, the more productive you can be.

Start with a basic set of generally applicable tools. As you gain experience, and as you come across special requirements, you’ll add to this basic set. Like the maker, expect to add to your toolbox regularly. Always be on the lookout for better ways of doing things. If you come across a situation where you feel your current tools can’t cut it, make a note to look for something different or more powerful that would have helped. Let need

drive your acquisitions.

Many new programmers make the mistake of adopting a single

power tool, such as a particular integrated development

environment (IDE), and never leave its cozy interface. This

really is a mistake. You need to be comfortable beyond the

limits imposed by an IDE. The only way to do this is to keep the basic tool set sharp and ready to use.

In this chapter we’ll talk about investing in your own basic toolbox. As with any good discussion on tools, we’ll start (in Topic 16, The Power of Plain Text) by looking at your raw materials, the stuff you’ll be shaping. From there we’ll move to the workbench, or in our case the computer. How can you use

your computer to get the most out of the tools you use? We’ll discuss this in Topic 17, Shell Games. Now that we have material and a bench to work on, we’ll turn to the tool you’ll probably use more than any other, your editor. In Topic 18,

Power Editing, we’ll suggest ways of making you more efficient.

To ensure that we never lose any of our precious work, we

should always use a Topic 19, Version Control system—even for personal things such as recipes or notes. And, since Murphy was really an optimist after all, you can’t be a great programmer until you become highly skilled at Topic 20, Debugging.

You’ll need some glue to bind much of the magic together. We discuss some possibilities in Topic 21, Text Manipulation.

Finally, the palest ink is still better than the best memory. Keep track of your thoughts and your history, as we describe in Topic 22, Engineering Daybooks.

Spend time learning to use these tools, and at some point you’ll be surprised to discover your fingers moving over the keyboard, manipulating text without conscious thought. The tools will

have become extensions of your hands.

## Topic 16 The Power of Plain Text

As Pragmatic Programmers, our base material isn’t wood or

iron, it’s knowledge. We gather requirements as knowledge, and then express that knowledge in our designs, implementations, tests, and documents. And we believe that the best format for storing knowledge persistently is plain text. With plain text, we give ourselves the ability to manipulate knowledge, both

manually and programmatically, using virtually every tool at our disposal.

The problem with most binary formats is that the context

necessary to understand the data is separate from the data

itself. You are artificially divorcing the data from its meaning.

The data may as well be encrypted; it is absolutely meaningless without the application logic to parse it. With plain text,

however, you can achieve a self-describing data stream that is independent of the application that created it.

WHAT IS PLAIN TEXT?

Plain text is made up of printable characters in a form that conveys information. It can be as simple as a shopping list:

* milk

* lettuce

* coffee

or as complex as the source of this book (yes, it’s in plain text, much to the chagrin of the publisher, who wanted us to use a word processor).

The information part is important. The following is not useful plain text:

hlj;uijn bfjxrrctvh jkni'pio6p7gu;vh bjxrdi5rgvhj

Neither is this:

Field19=467abe

The reader has no idea what the significance of 467abe may be.

We like our plain text to be understandable to humans.

Tip 25

Keep Knowledge in Plain Text

THE POWER OF TEXT

Plain text doesn’t mean that the text is unstructured; HTML, JSON, YAML, and so on are all plain text. So are the majority of the fundamental protocols on the net, such as HTTP, SMTP,

IMAP, and so on. And that’s for some good reasons:

Insurance against obsolescence

Leverage existing tools

Easier testing

Insurance Against Obsolescence

Human-readable forms of data, and self-describing data, will outlive all other forms of data and the applications that created them. Period. As long as the data survives, you will have a

chance to be able to use it—potentially long after the original application that wrote it is defunct.

You can parse such a file with only partial knowledge of its

format; with most binary files, you must know all the details of the entire format in order to parse it successfully.

Consider a data file from some legacy system that you are given.

[24] You know little about the original application; all that’s important to you is that it maintained a list of clients’ Social Security numbers, which you need to find and extract. Among

the data, you see

<FIELD10>123-45-6789</FIELD10>

...

<FIELD10>567-89-0123</FIELD10>

...

<FIELD10>901-23-4567</FIELD10>

Recognizing the format of a Social Security number, you can

quickly write a small program to extract that data—even if you have no information on anything else in the file.

But imagine if the file had been formatted this way instead:

AC27123456789B11P

...

XY43567890123QTYL

...

6T2190123456788AM

You may not have recognized the significance of the numbers

quite as easily. This is the difference between human readable and human understandable.

While we’re at it, FIELD10 doesn’t help much either. Something like

<SOCIAL-SECURITY-NO>123-45-6789</SOCIAL-SECURITY-NO> makes the exercise a no-brainer—and ensures that the data will

outlive any project that created it.

Leverage

Virtually every tool in the computing universe, from version control systems to editors to command-line tools, can operate on plain text.

The Unix Philosophy

Unix is famous for being designed around the philosophy of small, sharp tools, each intended to do one thing well. This philosophy is enabled by using a common underlying format—the line-oriented, plain-text file. Databases used for system administration (users and passwords, networking configuration, and so on) are all kept as plain-text files. (Some systems also maintain a binary form of certain databases as a performance optimization. The plain-text version is kept as an interface to the binary version.)

When a system crashes, you may be faced with only a minimal environment to restore it (you may not be able to access graphics drivers, for instance). Situations such as this can really make you appreciate the simplicity of plain text.

Plain text is also easier to search. If you can’t remember which configuration file manages your system backups, a quick grep -r backup /etc should tell you.

For instance, suppose you have a production deployment of a

large application with a complex site-specific configuration file.

If this file is in plain text, you could place it under a version control system (see Topic 19, Version Control), so that you automatically keep a history of all changes. File comparison tools such as diff and fc allow you to see at a glance what changes have been made, while sum allows you to generate a checksum to monitor the file for accidental (or malicious) modification.

Easier Testing

If you use plain text to create synthetic data to drive system tests, then it is a simple matter to add, update, or modify the test data without having to create any special tools to do so.

Similarly, plain-text output from regression tests can be trivially analyzed with shell commands or a simple script.

LOWEST COMMON DENOMINATOR

Even in the future of blockchain-based intelligent agents that travel the wild and dangerous internet autonomously,

negotiating data interchange among themselves, the ubiquitous text file will still be there. In fact, in heterogeneous

environments the advantages of plain text can outweigh all of the drawbacks. You need to ensure that all parties can

communicate using a common standard. Plain text is that

standard.

RELATED SECTIONS INCLUDE

Topic 17, Shell Games

Topic 21, Text Manipulation

Topic 32, Configuration

CHALLENGES

Design a small address book database (name, phone number, and so on) using a straightforward binary representation in your language of choice. Do this before reading the rest of this challenge.

Translate that format into a plain-text format using XML or

JSON.

For each version, add a new, variable-length field called

directions in which you might enter directions to each person’s house.

What issues come up regarding versioning and extensibility? Which

form was easier to modify? What about converting existing data?

Topic 17

Shell Games

Every woodworker needs a good, solid, reliable workbench,

somewhere to hold work pieces at a convenient height while

they’re being shaped. The workbench becomes the center of the woodshop, the maker returning to it time and time again as a piece takes shape.

For a programmer manipulating files of text, that workbench is the command shell. From the shell prompt, you can invoke your full repertoire of tools, using pipes to combine them in ways never dreamt of by their original developers. From the shell, you can launch applications, debuggers, browsers, editors, and

utilities. You can search for files, query the status of the system, and filter output. And by programming the shell, you can build complex macro commands for activities you perform often.

For programmers raised on GUI interfaces and integrated

development environments (IDEs), this might seem an extreme

position. After all, can’t you do everything equally well by pointing and clicking?

The simple answer is「no.’’ GUI interfaces are wonderful, and they can be faster and more convenient for some simple

operations. Moving files, reading and writing email, and

building and deploying your project are all things that you

might want to do in a graphical environment. But if you do all your work using GUIs, you are missing out on the full

capabilities of your environment. You won’t be able to automate

common tasks, or use the full power of the tools available to you. And you won’t be able to combine your tools to create

customized macro tools. A benefit of GUIs is WYSIWYG—

what you see is what you get. The disadvantage is WYSIAYG—

what you see is all you get.

GUI environments are normally limited to the capabilities that their designers intended. If you need to go beyond the model the designer provided, you are usually out of luck—and more

often than not, you do need to go beyond the model. Pragmatic Programmers don’t just cut code, or develop object models, or write documentation, or automate the build process—we do all of these things. The scope of any one tool is usually limited to the tasks that the tool is expected to perform. For instance, suppose you need to integrate a code preprocessor (to

implement design-by-contract, or multi-processing pragmas, or some such) into your IDE. Unless the designer of the IDE

explicitly provided hooks for this capability, you can’t do it.

Tip 26

Use the Power of Command Shells

Gain familiarity with the shell, and you’ll find your productivity soaring. Need to create a list of all the unique package names explicitly imported by your Java code? The following stores it in a file called「list’’:

sh/packages.sh

grep '^import ' *.java |

sed -e 's/.*import *//' -e 's/;.*$//' |

sort -u >list

If you haven’t spent much time exploring the capabilities of the command shell on the systems you use, this might appear

daunting. However, invest some energy in becoming familiar with your shell and things will soon start falling into place. Play around with your command shell, and you’ll be surprised at how much more productive it makes you.

A SHELL OF YOUR OWN

In the same way that a woodworker will customize their

workspace, a developer should customize their shell. This

typically also involves changing the configuration of the

terminal program you use.

Common changes include:

Setting color themes. Many, many hours can be spent trying out every single theme that’s available online for your particular shell.

Configuring a prompt. The prompt that tells you the shell is ready for you to type a command can be configured to display just about any information you might want (and a bunch of stuff you’d never want). Personal preferences are everything here: we tend to like simple prompts, with a shortened current directory name and

version control status along with the time.

Aliases and shell functions. Simplify your workflow by turning commands you use a lot into simple aliases. Maybe you regularly update your Linux box, but can never remember whether you

update and upgrade, or upgrade and update. Create an alias:

alias apt-up= 'sudo apt-get update && sudo apt-get upgrade'

Maybe you’ve accidentally deleted files with the rm command just one time too often. Write an alias so that it will always prompt in future:

alias rm = 'rm -iv'

Command completion. Most shells will complete the names of commands and files: type the first few characters, hit tab, and it’ll fill in what it can. But you can take this a lot further, configuring the

shell to recognize the command you’re entering and offer context-specific completions. Some even customize the completion

depending on the current directory.

You’ll spend a lot of time living in one of these shells. Be like a hermit crab and make it your own home.

RELATED SECTIONS INCLUDE

Topic 13, Prototypes and Post-it Notes

Topic 16, The Power of Plain Text

Topic 21, Text Manipulation

Topic 30, Transforming Programming

Topic 51, Pragmatic Starter Kit

CHALLENGES

Are there things that you’re currently doing manually in a GUI? Do you ever pass instructions to colleagues that involve a number of individual「click this button,」「select this item」steps? Could these be automated?

Whenever you move to a new environment, make a point of finding out what shells are available. See if you can bring your current shell with you.

Investigate alternatives to your current shell. If you come across a problem your shell can’t address, see if an alternative shell would cope better.

Topic 18

Power Editing

We’ve talked before about tools being an extension of your

hand. Well, this applies to editors more than to any other

software tool. You need to be able to manipulate text as

effortlessly as possible, because text is the basic raw material of programming.

In the first edition of this book we recommended using a single editor for everything: code, documentation, memos, system

administration, and so on. We’ve softened that position a little.

We’re happy for you to use as many editors as you want. We’d just like you to be working toward fluency in each.

Tip 27

Achieve Editor Fluency

Why is this a big deal? Are we saying you’ll save lots of time?

Actually yes: over the course of a year, you might actually gain an additional week if you make your editing just 4% more

efficient and you edit for 20 hours a week.

But that’s not the real benefit. No, the major gain is that by becoming fluent, you no longer have to think about the

mechanics of editing. The distance between thinking something and having it appear in an editor buffer drop way down. Your thoughts will flow, and your programming will benefit. (If

you’ve ever taught someone to drive, then you’ll understand the difference between someone who has to think about every

action they take and a more experienced driver who controls the

car instinctively.)

WHAT DOES「FLUENT」MEAN?

What counts as being fluent? Here’s the challenge list:

When editing text, move and make selections by character, word, line, and paragraph.

When editing code, move by various syntactic units (matching delimiters, functions, modules, …).

Reindent code following changes.

Comment and uncomment blocks of code with a single command.

Undo and redo changes.

Split the editor window into multiple panels, and navigate between them.

Navigate to a particular line number.

Sort selected lines.

Search for both strings and regular expressions, and repeat

previous searches.

Temporarily create multiple cursors based on a selection or on a pattern match, and edit the text at each in parallel.

Display compilation errors in the current project.

Run the current project’s tests.

Can you do all this without using a mouse/trackpad?

You might say that your current editor can’t do some of these things. Maybe it’s time to switch?

MOVING TOWARD FLUENCY

We doubt there are more than a handful of people who know all the commands in any particular powerful editor. We don’t

expect you to, either. Instead, we suggest a more pragmatic

approach: learn the commands that make your life easier.

The recipe for this is fairly simple.

First, look at yourself while you’re editing. Every time you find yourself doing something repetitive, get into the habit of

thinking「there must be a better way.」Then find it.

Once you’ve discovered a new, useful feature, you now need to get it installed into your muscle memory, so you can use it

without thinking. The only way we know to do that is through repetition. Consciously look for opportunities to use your new superpower, ideally many times a day. After a week or so, you’ll find you use it without thinking.

Growing Your Editor

Most of the powerful code editors are built around a basic core that is then augmented through extensions. Many are supplied with the editor, and others can be added later.

When you bump into some apparent limitation of the editor

you’re using, search around for an extension that will do the job.

The chances are that you are not alone in needing that

capability, and if you’re lucky someone else will have published their solution.

Take this a step further. Dig into your editor’s extension

language. Work out how to use it to automate some of the

repetitive things you do. Often you’ll just need a line or two of code.

Sometimes you might take it further still, and you’ll find yourself writing a full-blown extension. If so, publish it: if you had a need for it, other people will, too.

RELATED SECTIONS INCLUDE

Topic 7, Communicate!

CHALLENGES

No more autorepeat.

Everyone does it: you need to delete the last word you typed, so you press down on backspace and wait for autorepeat to kick in. In fact, we bet that your brain has done this so much that you can judge pretty much exactly when to release the key.

So turn off autorepeat, and instead learn the key sequences to move, select, and delete by characters, words, lines, and blocks.

This one is going to hurt.

Lose the mouse/trackpad. For one whole week, edit using just the keyboard. You’ll discover a bunch of stuff that you can’t do without pointing and clicking, so now’s the time to learn. Keep notes (we recommend going old-school and using pencil and paper) of the key sequences you learn.

You’ll take a productivity hit for a few days. But, as you learn to do stuff without moving your hands away from the home position, you’ll find that your editing becomes faster and more fluent than it ever was in the past.

Look for integrations. While writing this chapter, Dave wondered if he could preview the final layout (a PDF file) in an editor buffer.

One download later, the layout is sitting alongside the original text, all in the editor. Keep a list of things you’d like to bring into your editor, then look for them.

Somewhat more ambitiously, if you can’t find a plugin or extension that does what you want, write one. Andy is fond of making custom, local file-based Wiki plugins for his favorite editors. If you can’t

find it, build it!

Topic 19

Version Control

One of the important things we

look for in a user interface is the

Progress, far from

undo key—a single button that

consisting in change,

forgives us our mistakes. It’s even

depends on

better if the environment supports

retentiveness. Those

multiple levels of undo and redo,

who cannot remember

so you can go back and recover

the past are

from something that happened a

condemned to repeat

couple of minutes ago.

it.

But what if the mistake happened

last week, and you’ve turned your

George Santayana, Life of

Reason

computer on and off ten times

since then? Well, that’s one of the

many benefits of using a version

control system (VCS): it’s a giant undo key—a project-wide time machine that can return you to those halcyon days of last week, when the code actually compiled and ran.

For many folks, that’s the limit of their VCS usage. Those folks are missing out on a whole bigger world of collaboration,

deployment pipelines, issue tracking, and general team

interaction.

So let’s take a look at VCS, first as a repository of changes, and then as a central meeting place for your team and their code.

Shared Directories Are NOT Version Control

We still come across the occasional team who share their project source files across a network: either internally or using some kind of cloud storage.

This is not viable.

Teams that do this are constantly messing up each other’s work, losing changes, breaking builds, and getting into fist fights in the car park. It’s like writing concurrent code with shared data and no synchronization mechanism. Use version control.

But there’s more! Some folks do use version control, and keep their main repository on a network or cloud drive. They reason that this is the best of both worlds: their files are accessible anywhere and (in the case of cloud storage) it’s backed up off-site.

Turns out that this is even worse, and you risk losing everything. The version control software uses a set of interacting files and directories. If two instances simultaneously make changes, the overall state can become corrupted, and there’s no telling how much damage will be done. And no one likes seeing developers cry.

IT STARTS AT THE SOURCE

Version control systems keep track of every change you make in your source code and documentation. With a properly

configured source code control system, you can always go back to a previous version of your software.

But a version control system does far more than undo mistakes.

A good VCS will let you track changes, answering questions

such as: Who made changes in this line of code? What’s the

difference between the current version and last week’s? How

many lines of code did we change in this release? Which files get changed most often? This kind of information is invaluable for bug-tracking, audit, performance, and quality purposes.

A VCS will also let you identify releases of your software. Once identified, you will always be able to go back and regenerate the release, independent of changes that may have occurred later.

Version control systems may keep the files they maintain in a central repository—a great candidate for archiving.

Finally, version control systems allow two or more users to be working concurrently on the same set of files, even making

concurrent changes in the same file. The system then manages the merging of these changes when the files are sent back to the repository. Although seemingly risky, such systems work well in practice on projects of all sizes.

Tip 28

Always Use Version Control

Always. Even if you are a single-person team on a one-week

project. Even if it’s a「throw-away’’ prototype. Even if the stuff you’re working on isn’t source code. Make sure that everything is under version control: documentation, phone number lists, memos to vendors, makefiles, build and release procedures, that little shell script that tidies up log files—everything. We

routinely use version control on just about everything we type (including the text of this book). Even if we’re not working on a project, our day-to-day work is secured in a repository.

BRANCHING OUT

Version control systems don’t just keep a single history of your project. One of their most powerful and useful features is the way they let you isolate islands of development into things

called branches. You can create a branch at any point in your project’s history, and any work you do in that branch will be isolated from all other branches. At some time in the future you can merge the branch you’re working on back into another branch, so the target branch now contains the changes you

made in your branch. Multiple people can even be working on a

branch: in a way, branches are like little clone projects.

One benefit of branches is the isolation they give you. If you develop feature A in one branch, and a teammate works on

feature B in another, you’re not going to interfere with each other.

A second benefit, which may be surprising, is that branches are often at the heart of a team’s project workflow.

And this is where things get a little confusing. Version control branches and test organization have something in common:

they both have thousands of people out there telling you how you should do it. And that advice is largely meaningless,

because what they’re really saying is「this is what worked for me.」

So use version control in your project, and if you bump into workflow issues, search for possible solutions. And remember to review and adjust what you’re doing as you gain experience.

A Thought Experiment

Spill an entire cup of tea (English breakfast, with a little milk) onto your laptop keyboard.

Take the machine to the smart-person bar, and have them tut and frown. Buy a new computer. Take it home.

How long would it take to get that machine back to the same state it was in (with all the SSH keys, editor configuration, shell setup, installed applications, and so on) at the point where you first lifted that fateful cup? This was an issue one of us faced recently.

Just about everything that defined the configuration and usage of the original machine was stored in version control, including:

All the user preferences and dotfiles

The editor configuration

The list of software installed using Homebrew

The Ansible script used to configure apps

All current projects

The machine was restored by the end of the afternoon.

VERSION CONTROL AS A PROJECT HUB

Although version control is incredibly useful on personal

projects, it really comes into its own when working with a team.

And much of this value comes from how you host your

repository.

Now, many version control systems don’t need any hosting.

They are completely decentralized, with each developer

cooperating on a peer-to-peer basis. But even with these

systems, it’s worth looking into having a central repository, because once you do, you can take advantage of a ton of

integrations to make the project flow easier.

Many of the repository systems are open source, so you can

install and run them in your company. But that’s not really your line of business, so we’d recommend most people host with a

third party. Look for features such as:

Good security and access control

Intuitive UI

The ability to do everything from the command line, too (because you may need to automate it)

Automated builds and tests

Good support for branch merging (sometimes called pull requests) Issue management (ideally integrated into commits and merges, so

you can keep metrics)

Good reporting (a Kanban board-like display of pending issues and tasks can be very useful)

Good team communications: emails or other notifications on

changes, a wiki, and so on

Many teams have their VCS configured so that a push to a

particular branch will automatically build the system, run the tests, and if successful deploy the new code into production.

Sound scary? Not when you realize you’re using version control.

You can always roll it back.

RELATED SECTIONS INCLUDE

Topic 11, Reversibility

Topic 49, Pragmatic Teams

Topic 51, Pragmatic Starter Kit

CHALLENGES

Knowing you can roll back to any previous state using the VCS is one thing, but can you actually do it? Do you know the commands to do it properly? Learn them now, not when disaster strikes and you’re under pressure.

Spend some time thinking about recovering your own laptop

environment in case of a disaster. What would you need to recover?

Many of the things you need are just text files. If they’re not in a VCS (hosted off your laptop), find a way to add them. Then think about the other stuff: installed applications, system configuration, and so on. How can you express all that stuff in text files so it, too, can be saved?

An interesting experiment, once you’ve made some progress, is to find an old computer you no longer use and see if your new system can be used to set it up.

Consciously explore the features of your current VCS and hosting provider that you’re not using. If your team isn’t using feature branches, experiment with introducing them. The same with

pull/merge requests. Continuous integration. Build pipelines. Even continuous deployment. Look into the team communication tools, too: wikis, Kanban boards, and the like.

You don’t have to use any of it. But you do need to know what it does so you can make that decision.

Use version control for nonproject things, too.

Topic 20

Debugging

The word bug has been used to

describe an「object of terror’’ ever

It is a painful thing

since the fourteenth century. Rear

To look at your own

Admiral Dr. Grace Hopper, the

trouble and know

inventor of COBOL, is credited

That you yourself and

with observing the first computer

no one else has made it

bug—literally, a moth caught in a

relay in an early computer system.

Sophocles, Ajax

When asked to explain why the

machine wasn’t behaving as

intended, a technician reported

that there was「a bug in the system,」and dutifully taped it—

wings and all—into the log book.

Regrettably, we still have bugs in the system, albeit not the flying kind. But the fourteenth century meaning—a bogeyman—

is perhaps even more applicable now than it was then. Software defects manifest themselves in a variety of ways, from

misunderstood requirements to coding errors. Unfortunately,

modern computer systems are still limited to doing what you

tell them to do, not necessarily what you want them to do.

No one writes perfect software, so it’s a given that debugging will take up a major portion of your day. Let’s look at some of the issues involved in debugging and some general strategies for finding elusive bugs.

PSYCHOLOGY OF DEBUGGING

Debugging is a sensitive, emotional subject for many developers. Instead of attacking it as a puzzle to be solved, you may encounter denial, finger pointing, lame excuses, or just plain apathy.

Embrace the fact that debugging is just problem solving, and attack it as such.

Having found someone else’s bug, you can spend time and

energy laying blame on the filthy culprit who created it. In some workplaces this is part of the culture, and may be cathartic.

However, in the technical arena, you want to concentrate on

fixing the problem, not the blame.

Tip 29

Fix the Problem, Not the Blame

It doesn’t really matter whether the bug is your fault or

someone else’s. It is still your problem.

A DEBUGGING MINDSET

Before you start debugging, it’s important to adopt the right mindset. You need to turn off many of the defenses you use each day to protect your ego, tune out any project pressures you may be under, and get yourself comfortable. Above all, remember

the first rule of debugging:

Tip 30

Don’t Panic

It’s easy to get into a panic, especially if you are facing a deadline, or have a nervous boss or client breathing down your neck while you are trying to find the cause of the bug. But it is very important to step back a pace, and actually think about

what could be causing the symptoms that you believe indicate a bug.

If your first reaction on witnessing a bug or seeing a bug report is「that’s impossible,」you are plainly wrong. Don’t waste a single neuron on the train of thought that begins「but that can’t happen」because quite clearly it can, and has.

Beware of myopia when debugging. Resist the urge to fix just the symptoms you see: it is more likely that the actual fault may be several steps removed from what you are observing, and may involve a number of other related things. Always try to discover the root cause of a problem, not just this particular appearance of it.

WHERE TO START

Before you start to look at the bug, make sure that you are working on code that built cleanly—without warnings. We

routinely set compiler warning levels as high as possible. It doesn’t make sense to waste time trying to find a problem that the computer could find for you! We need to concentrate on the harder problems at hand.

When trying to solve any problem, you need to gather all the relevant data. Unfortunately, bug reporting isn’t an exact

science. It’s easy to be misled by coincidences, and you can’t afford to waste time debugging coincidences. You first need to be accurate in your observations.

Accuracy in bug reports is further diminished when they come through a third party—you may actually need to watch the user who reported the bug in action to get a sufficient level of detail.

Andy once worked on a large graphics application. Nearing release, the testers reported that the application crashed every time they painted a stroke with a particular brush. The

programmer responsible argued that there was nothing wrong

with it; he had tried painting with it, and it worked just fine.

This dialog went back and forth for several days, with tempers rapidly rising.

Finally, we got them together in the same room. The tester

selected the brush tool and painted a stroke from the upper

right corner to the lower left corner. The application exploded.

「Oh,」said the programmer, in a small voice, who then

sheepishly admitted that he had made test strokes only from the lower left to the upper right, which did not expose the bug.

There are two points to this story:

You may need to interview the user who reported the bug in order to gather more data than you were initially given.

Artificial tests (such as the programmer’s single brush stroke from bottom to top) don’t exercise enough of an application. You must brutally test both boundary conditions and realistic end-user usage

patterns. You need to do this systematically (see Ruthless and

Continuous Testing).

DEBUGGING STRATEGIES

Once you think you know what is going on, it’s time to find out what the program thinks is going on.

Reproducing Bugs

No, our bugs aren’t really multiplying (although some of them are probably old enough to do it legally). We’re talking about a different kind of reproduction.

The best way to start fixing a bug is to make it reproducible.

After all, if you can’t reproduce it, how will you know if it is ever fixed?

But we want more than a bug that can be reproduced by

following some long series of steps; we want a bug that can be reproduced with a single command. It’s a lot harder to fix a bug if you have to go through 15 steps to get to the point where the bug shows up.

So here’s the most important rule of debugging:

Tip 31

Failing Test Before Fixing Code

Sometimes by forcing yourself to isolate the circumstances that display the bug, you’ll even gain an insight on how to fix it. The act of writing the test informs the solution.

CODER IN A STRANGE LAND

All this talk about isolating the bug is fine, when faced with 50,000 lines of code and a ticking clock, what’s a poor coder to do?

First, look at the problem. Is it a crash? It’s always surprising when we teach courses that involve programming how many

developers see an exception pop up in red and immediately tab across to the code.

Tip 32

Read the Damn Error Message

’nuf said.

Bad Results

What if it’s not a crash? What if it’s just a bad result?

Get in there with a debugger and use your failing test to trigger the problem.

Before anything else, make sure that you’re also seeing the

incorrect value in the debugger. We’ve both wasted hours trying to track down a bug only to discover that this particular run of the code worked fine.

Sometimes the problem is obvious: interest_rate is 4.5 and should be 0.045. More often you have to look deeper to find out why the value is wrong in the first place. Make sure you know how to move up and down the call stack and examine the local stack

environment.

We find it often helps to keep pen and paper nearby so we can jot down notes. In particular we often come across a clue and chase it down, only to find it didn’t pan out. If we didn’t jot down where we were when we started the chase, we could lose a lot of time getting back there.

Sometimes you’re looking at a stack trace that seems to scroll on forever. In this case, there’s often a quicker way to find the problem than examining each and every stack frame: use a

binary chop. But before we discuss that, let’s look at two other common bug scenarios.

Sensitivity to Input Values

You’ve been there. Your program works fine with all the test data, and survives its first week in production with honor. Then it suddenly crashes when fed a particular dataset.

You can try looking at the place it crashes and work backwards.

But sometimes it’s easier to start with the data. Get a copy of the dataset and feed it through a locally running copy of the app, making sure it still crashes. Then binary chop the data until you isolate exactly which input values are leading to the crash.

Regressions Across Releases

You’re on a good team, and you release your software into

production. At some point a bug pops up in code that worked

OK a week ago. Wouldn’t it be nice if you could identify the specific change that introduced it? Guess what? Binary chop

time.

THE BINARY CHOP

Every CS undergraduate has been forced to code a binary chop (sometimes called a binary search). The idea is simple. You’re looking for a particular value in a sorted array. You could just look at each value in turn, but you’d end up looking at roughly half the entries on average until you either found the value you wanted, or you found a value greater than it, which would mean the value’s not in the array.

But it’s faster to use a divide and conquer approach. Choose a value in the middle of the array. If it’s the one you’re looking for, stop. Otherwise you can chop the array in two. If the value you find is greater than the target then you know it must be in the first half of the array, otherwise it’s in the second half. Repeat the procedure in the appropriate subarray, and in no time you’ll have a result. (As we’ll see when we talk about Big-O Notation, a linear search is

, and a binary chop is

).

So, the binary chop is way, way faster on any decent sized

problem. Let’s see how to apply it to debugging.

When you’re facing a massive stacktrace and you’re trying to find out exactly which function mangled the value in error, you do a chop by choosing a stack frame somewhere in the middle

and seeing if the error is manifest there. If it is, then you know to focus on the frames before, otherwise the problem is in the frames after. Chop again. Even if you have 64 frames in the

stacktrace, this approach will give you an answer after at most six attempts.

If you find bugs that appear on certain datasets, you might be able to do the same thing. Split the dataset into two, and see if the problem occurs if you feed one or the other through the app.

Keep dividing the data until you get a minimum set of values that exhibit the problem.

If your team has introduced a bug during a set of releases, you can use the same type of technique. Create a test that causes the current release to fail. Then choose a half-way release between now and the last known working version. Run the test again,

and decide how to narrow your search. Being able to do this is just one of the many benefits of having good version control in your projects. Indeed, many version control systems will take this further and will automate the process, picking releases for you depending on the result of the test.

Logging and/or Tracing

Debuggers generally focus on the state of the program now.

Sometimes you need more—you need to watch the state of a

program or a data structure over time. Seeing a stack trace can only tell you how you got here directly. It typically can’t tell you what you were doing prior to this call chain, especially in event-based systems. [25]

Tracing statements are those little diagnostic messages you print to the screen or to a file that say things such as「got here」

and「value of x = 2.」It’s a primitive technique compared with IDE-style debuggers, but it is peculiarly effective at diagnosing several classes of errors that debuggers can’t. Tracing is

invaluable in any system where time itself is a factor:

concurrent processes, real-time systems, and event-based

applications.

You can use tracing statements to drill down into the code. That is, you can add tracing statements as you descend the call tree.

Trace messages should be in a regular, consistent format as you may want to parse them automatically. For instance, if you

needed to track down a resource leak (such as unbalanced file opens/closes), you could trace each open and each close in a log file. By processing the log file with text processing tools or shell commands, you can easily identify where the offending open was occurring.

Rubber Ducking

A very simple but particularly useful technique for finding the cause of a problem is simply to explain it to someone else. The other person should look over your shoulder at the screen, and nod his or her head constantly (like a rubber duck bobbing up and down in a bathtub). They do not need to say a word; the

simple act of explaining, step by step, what the code is supposed to do often causes the problem to leap off the screen and

announce itself. [26]

It sounds simple, but in explaining the problem to another

person you must explicitly state things that you may take for granted when going through the code yourself. By having to

verbalize some of these assumptions, you may suddenly gain new insight into the problem. And if you don’t have a person, a rubber duck, or teddy bear, or potted plant will do. [27]

Process of Elimination

In most projects, the code you are debugging may be a mixture of application code written by you and others on your project team, third-party products (database, connectivity, web

framework, specialized communications or algorithms, and so

on) and the platform environment (operating system, system

libraries, and compilers).

It is possible that a bug exists in the OS, the compiler, or a third-party product—but this should not be your first thought. It is much more likely that the bug exists in the application code under development. It is generally more profitable to assume that the application code is incorrectly calling into a library than to assume that the library itself is broken. Even if the problem does lie with a third party, you’ll still have to eliminate your code before submitting the bug report.

We worked on a project where a senior engineer was convinced that the select system call was broken on a Unix system. No

amount of persuasion or logic could change his mind (the fact that every other networking application on the box worked fine was irrelevant). He spent weeks writing workarounds, which,

for some odd reason, didn’t seem to fix the problem. When

finally forced to sit down and read the documentation on select, he discovered the problem and corrected it in a matter of

minutes. We now use the phrase「select is broken’’ as a gentle reminder whenever one of us starts blaming the system for a

fault that is likely to be our own.

Tip 33

「select」Isn’t Broken

Remember, if you see hoof prints, think horses—not zebras. The OS is probably not broken. And select is probably just fine.

If you「changed only one thing’’ and the system stopped

working, that one thing was likely to be responsible, directly or indirectly, no matter how farfetched it seems. Sometimes the thing that changed is outside of your control: new versions of the OS, compiler, database, or other third-party software can wreak havoc with previously correct code. New bugs might show up. Bugs for which you had a workaround get fixed, breaking

the workaround. APIs change, functionality changes; in short, it’s a whole new ball game, and you must retest the system

under these new conditions. So keep a close eye on the schedule when considering an upgrade; you may want to wait until after the next release.

THE ELEMENT OF SURPRISE

When you find yourself surprised by a bug (perhaps even

muttering「that’s impossible」under your breath where we can’t hear you), you must reevaluate truths you hold dear. In that discount calculation algorithm—the one you knew was

bulletproof and couldn’t possibly be the cause of this bug—did you test all the boundary conditions? That other piece of code you’ve been using for years—it couldn’t possibly still have a bug in it. Could it?

Of course it can. The amount of surprise you feel when

something goes wrong is proportional to the amount of trust

and faith you have in the code being run. That’s why, when

faced with a「surprising’’ failure, you must accept that one or

more of your assumptions is wrong. Don’t gloss over a routine or piece of code involved in the bug because you「know」it

works. Prove it. Prove it in this context, with this data, with these boundary conditions.

Tip 34

Don’t Assume It—Prove It

When you come across a surprise bug, beyond merely fixing it, you need to determine why this failure wasn’t caught earlier.

Consider whether you need to amend the unit or other tests so that they would have caught it.

Also, if the bug is the result of bad data that was propagated through a couple of levels before causing the explosion, see if better parameter checking in those routines would have isolated it earlier (see the discussions on crashing early and assertions

here and here, respectively).

While you’re at it, are there any other places in the code that may be susceptible to this same bug? Now is the time to find and fix them. Make sure that whatever happened, you’ll know if it happens again.

If it took a long time to fix this bug, ask yourself why. Is there anything you can do to make fixing this bug easier the next time around? Perhaps you could build in better testing hooks, or

write a log file analyzer.

Finally, if the bug is the result of someone’s wrong assumption, discuss the problem with the whole team: if one person

misunderstands, then it’s possible many people do.

Do all this, and hopefully you won’t be surprised next time.

DEBUGGING CHECKLIST

Is the problem being reported a direct result of the underlying bug, or merely a symptom?

Is the bug really in the framework you’re using? Is it in the OS? Or is it in your code?

If you explained this problem in detail to a coworker, what would you say?

If the suspect code passes its unit tests, are the tests complete enough? What happens if you run the tests with this data?

Do the conditions that caused this bug exist anywhere else in the system? Are there other bugs still in the larval stage, just waiting to hatch?

RELATED SECTIONS INCLUDE

Topic 24, Dead Programs Tell No Lies

CHALLENGES

Debugging is challenge enough.

Topic 21

Text Manipulation

Pragmatic Programmers manipulate text the same way

woodworkers shape wood. In previous sections we discussed

some specific tools—shells, editors, debuggers—that we use.

These are similar to a woodworker’s chisels, saws, and planes—

tools specialized to do one or two jobs well. However, every now and then we need to perform some transformation not readily

handled by the basic tool set. We need a general-purpose text manipulation tool.

Text manipulation languages are to programming what

routers[28 ]are to woodworking. They are noisy, messy, and somewhat brute force. Make mistakes with them, and entire

pieces can be ruined. Some people swear they have no place in the toolbox. But in the right hands, both routers and text

manipulation languages can be incredibly powerful and

versatile. You can quickly trim something into shape, make

joints, and carve. Used properly, these tools have surprising finesse and subtlety. But they take time to master.

Fortunately, there are a number of great text manipulation

languages. Unix developers (and we include macOS users here) often like to use the power of their command shells, augmented with tools such as awk and sed. People who prefer a more

structured tool may prefer languages such as Python or Ruby.

These languages are important enabling technologies. Using

them, you can quickly hack up utilities and prototype ideas—

jobs that might take five or ten times as long using conventional languages. And that multiplying factor is crucially important to the kind of experimenting that we do. Spending 30 minutes

trying out a crazy idea is a whole lot better than spending five hours. Spending a day automating important components of a

project is acceptable; spending a week might not be. In their book The Practice of Programming [KP99], Kernighan and Pike built the same program in five different languages. The Perl version was the shortest (17 lines, compared with C’s 150).

With Perl you can manipulate text, interact with programs, talk over networks, drive web pages, perform arbitrary precision

arithmetic, and write programs that look like Snoopy swearing.

Tip 35

Learn a Text Manipulation Language

To show the wide-ranging applicability of text manipulation

languages, here’s a sample of some stuff we’ve done with Ruby and Python just related to the creation of this book:

Building the Book

The build system for the Pragmatic Bookshelf is written

in Ruby. Authors, editors, layout people, and support

folks use Rake tasks to coordinate the building of PDFs

and ebooks.

Code inclusion and highlighting

We think it is important that any code presented in a

book should have been tested first. Most of the code in

this book has been. However, using the DRY principle

(see Topic 9, DRY—The Evils of Duplication) we didn’t want to copy and paste lines of code from the tested

programs into the book. That would mean we’d be

duplicating code, virtually guaranteeing that we’d forget to update an example when the corresponding program

was changed. For some examples, we also didn’t want to

bore you with all the framework code needed to make our

example compile and run. We turned to Ruby. A

relatively simple script is invoked when we format the

book—it extracts a named segment of a source file, does

syntax highlighting, and converts the result into the

typesetting language we use.

Website update

We have a simple script that does a partial book build,

extracts the table of contents, then uploads it to the

book’s page on our website. We also have a script that

extracts sections of a book and uploads them as samples.

Including equations

There’s a Python script that converts LaTeX math

markup into nicely formatted text.

Index generation

Most indexes are created as separate documents (which

makes maintaining them difficult if a document

changes). Ours are marked up in the text itself, and a

Ruby script collates and formats the entries.

And so on. In a very real way, the Pragmatic Bookshelf is built around text manipulation. And if you follow our advice to keep things in plain text, then using these languages to manipulate that text will bring a whole host of benefits.

RELATED SECTIONS INCLUDE

Topic 16, The Power of Plain Text

Topic 17, Shell Games

EXERCISES

Exercise 11

You’re rewriting an application that used to use YAML as a

configuration language. Your company has now standardized on JSON, so you have a bunch of .yaml files that need to be turned into .json. Write a script that takes a directory and converts each

.yaml file into a corresponding .json file (so database.yaml becomes database.json, and the contents are valid JSON).

Exercise 12

Your team initially chose to use camelCase names for variables, but then changed their collective mind and switched to

snake_case. Write a script that scans all the source files for camelCase names and reports on them.

Exercise 13

Following on from the previous exercise, add the ability to

change those variable names automatically in one or more files.

Remember to keep a backup of the originals in case something goes horribly, horribly wrong.

## Topic 22 Engineering Daybooks

Dave once worked for a small computer manufacturer, which

meant working alongside electronic and sometimes mechanical

engineers.

Many of them walked around with a paper notebook, normally

with a pen stuffed down the spine. Every now and then when we were talking, they’d pop the notebook open and scribble

something.

Eventually Dave asked the obvious question. It turned out that they’d been trained to keep an engineering daybook, a kind of journal in which they recorded what they did, things they’d

learned, sketches of ideas, readings from meters: basically

anything to do with their work. When the notebook became full, they’d write the date range on the spine, then stick it on the shelf next to previous daybooks. There may have been a gentle competition going on for whose set of books took the most shelf space.

We use daybooks to take notes in meetings, to jot down what

we’re working on, to note variable values when debugging, to leave reminders where we put things, to record wild ideas, and sometimes just to doodle. [29]

The daybook has three main benefits:

It is more reliable than memory. People might ask「What was the name of that company you called last week about the power supply

problem?」and you can flip back a page or so and give them the name and number.

It gives you a place to store ideas that aren’t immediately relevant to the task at hand. That way you can continue to concentrate on what you are doing, knowing that the great idea won’t be forgotten.

It acts as a kind of rubber duck (described here). When you stop to write something down, your brain may switch gears, almost as if talking to someone—a great chance to reflect. You may start to make a note and then suddenly realize that what you’d just done, the topic of the note, is just plain wrong.

There’s an added benefit, too. Every now and then you can look back at what you were doing oh-so-many-years-ago and think

about the people, the projects, and the awful clothes and

hairstyles.

So, try keeping an engineering daybook. Use paper, not a file or a wiki: there’s something special about the act of writing

compared to typing. Give it a month, and see if you’re getting any benefits.

If nothing else, it’ll make writing your memoir easier when

you’re rich and famous.

## RELATED SECTIONS INCLUDE

Topic 6, Your Knowledge Portfolio

Topic 37, Listen to Your Lizard Brain

## Footnotes

[24] All software becomes legacy software as soon as it’s written.

[25] Although the Elm language does have a time-traveling debugger. Why「rubber ducking’’? While an undergraduate at Imperial College in London, Dave

[26] did a lot of work with a research assistant named Greg Pugh, one of the best developers Dave has known. For several months Greg carried around a small yellow rubber duck, which he’d place on his terminal while coding. It was a while before Dave had the courage to ask….

[27] Earlier versions of the book talked about talking to your pot plant. It was a typo. Honest.

[28] Here router means the tool that spins cutting blades very, very fast, not a device for interconnecting networks.

[29] There is some evidence that doodling helps focus and improves cognitive skills, for example, see What does doodling do? [And10].
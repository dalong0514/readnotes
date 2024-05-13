because you wanted to see whether the butler actually did it.

This chapter gives you some advice you should take into account when you start

developing your own VBA solutions. Following these guidelines is no panacea to

keep you out of (programming) trouble, but following them can help you avoid

pitfalls that others have stumbled over.

Do Declare All Variables

How convenient it is: Simply start typing your VBA code without having to go through the tedious chore of declaring each and every variable you want to use.

Although Excel allows you to use undeclared variables, doing so is simply asking

for trouble.

The first commandment of VBA programming should be this:

Thou shalt declare every variable.

CHAPTER 24  Ten VBA Do's and Don'ts    383

If you lack self-discipline, add an「Option Explicit」statement at the top of your modules. That way, your code won't even run if it includes one or more undeclared

variables. Not declaring all variables has only one advantage: You save a few sec-

onds. But using undeclared variables will eventually come back to haunt you. And

it will take you more than a few seconds to figure out the problem.

Don't Confuse Passwords with Security

You spent months creating a killer Excel app, with some amazing macros. You're

ready to release it to the world, but you don't want others to see your incredible

macro programming. Just password-protect the VBA project, and you're safe,

right? Wrong.

Using a VBA password can keep most casual users from viewing your code. But if

someone  really wants to check it, he'll figure out how to crack the password.

Bottom line? If you absolutely, positively need to keep your code a secret, Excel

isn't the best choice for a development platform.

Do Clean Up Your Code

After your app is working to your satisfaction, you should clean it up. Code house-

keeping tasks include the following:

» Make sure every variable is declared.

» Make sure all the lines are indented properly so the code structure is apparent.

» Remove any debugging aids, such as MsgBox statements of Debug.Print

statements.

» Rename any poorly named variables. For example, if you use the variable

MyVariable, there's a pretty good chance that you can make the variable name

more descriptive. You'll thank yourself later.

» Your modules probably have a few「test」procedures that you wrote while

trying to figure something out. They've served their purpose, so delete them.

» Add comments so you'll understand how the code works when you revisit it

six months from now.

384    PART 6  The Part of Tens

» Make sure everything is spelled correctly — especially text in UserForms and message boxes.

» Check for redundant code. If you have two or more procedures that have

identical blocks of code, consider creating a new procedure that other

procedures can call.

Don't Put Everything in One Procedure

Want to make an unintelligible program? An efficient way to accomplish that is to

put all your code inside one nice big procedure. If you ever revisit this program

again to make changes, you're bound to make mistakes and introduce some fine-

looking bugs.

Do you see the problem? The solution is modular code. Split your program into

smaller chunks, with each chunk designed to perform a specific task. After you

pick up this habit, you'll find that writing bug-free code is easier than ever.

Do Consider Other Software

Excel is an amazingly versatile program, but it's not suitable for everything. When

you're ready to undertake a new project, take some time to consider all your options. To paraphrase an old saying,「When all you know is Excel VBA, everything looks like a VBA macro.」

Don't Assume That Everyone

Enables Macros

As you know, Excel allows you to open a workbook with its macros disabled. In

fact, it's almost as though the designers of recent versions of Excel  want users to disable macros.

Enabling macros when you open a workbook from an unknown source is not a

good idea, of course. So you need to know your users. In some corporate environ-

ments, all Microsoft Office macros are disabled, and the user has no choice in the

matter.

CHAPTER 24  Ten VBA Do's and Don'ts    385

One thing to consider is adding a digital signature to the workbooks that you distribute to others. That way, the user can be assured that the workbooks actually

come from you and that they haven't been altered. Consult the Help system for

more information about digital signatures.

Do Get in the Habit of Experimenting

When working on a large-scale Excel project, spend time writing small VBA

「experiments.」 For example, if you're trying to find out about a new object, method, or property, write a simple Sub procedure and play around with it until

you're satisfied that you have a thorough understanding of how it works — and

the potential problems.

Setting up simple experiments is almost always much more efficient than incor-

porating a new idea into your existing code without understanding what those experiments bring.

Don't Assume That Your Code Will Work

with Other Excel Versions

When you create an Excel app, you have absolutely no guarantee that it will work

flawlessly in older versions of Excel (or in future versions for that matter). In some cases, the incompatibilities will be obvious. For example, if your code refers

to a new feature introduced in Excel 2019, you know that it won't work in prior

versions. But you'll also find that things that should work with an earlier version

don't work.

Excel includes a handy compatibility checker (choose File ➪  Info ➪  Check For Issues ➪  Check Compatibility), but it only checks the workbook and ignores the

VBA code. The only way to be sure that your application works with versions other

than the one you created it with is to test it in those versions.

Do Keep Your Users in Mind

Excel apps fall into two main categories: those that you develop for yourself and

those that you develop for others to use. If you develop apps for others, your job

is much more difficult because you can't make the same types of assumptions.

386    PART 6  The Part of Tens

For example, you can be more lax with error handling if you're the only user. If an error crops up, you'll have a pretty good idea where to look so you can fix it. If

someone else is using your app and the same error appears, he or she will be out

of luck. And when you're working with your own application, you can usually get

by without instructions.

You need to understand the skill level of those who will be using your workbooks

and try to anticipate problems that they might have. Try to picture yourself as a

new user of your application, and identify all areas that may cause confusion or

problems.

Don't Forget About Backups

Nothing is more discouraging than a hard drive crash without a backup. If you're

working on an important project, ask yourself a simple question:「If my computer


I f you’re going to be spending time working the Visual Basic Editor, then why not take advantage of a few of the built-in tools that can make your job easier?

Whether you’re a fresh-faced analyst new to programming, or a jaded veteran

living on Mountain Dew and sunflower seeds, these tips can greatly improve your

macro programming experience.

CHAPTER 22  Ten Handy Visual Basic Editor Tips    369

Applying Block Comments

Placing a single apostrophe in front of any statement effectively tells Excel to skip that statement. This is called commenting out code. You can use the single apostrophe to also create comments or notes in your code (see Figure 22-1).

It’s sometimes beneficial to comment out multiple lines of code. This way, you

can test certain lines of code while telling Excel to ignore the commented lines.

FIGURE 22-1:

A single

apostrophe

in front of any

line turns that

line into a

comment.

Instead of spending time commenting out one line at a time, you can use the Edit

toolbar to comment out whole blocks of code.

You can activate the Edit toolbar by choosing View ➪  Toolbars ➪  Edit.

Select the lines of code you want commented out and then click the Comment

Block icon on the Edit toolbar (see Figure 22-2).

FIGURE 22-2:

The Edit toolbar

allows you to

select entire

blocks of code,

then apply

comments to all

the lines at once.

You can ensure the Edit toolbar is always visible by dragging it up to the VBE

menu bar. It anchors itself to the location you choose.

370    PART 6  The Part of Tens

Copying Multiple Lines of Code at Once

You can copy entire blocks of code by highlighting the lines you need, and then

holding down the Ctrl key on your keyboard while dragging the block where you

need it. This is an old Windows trick that works even when you drag across modules.

You know you’re dragging a copy when your mouse pointer shows a plus symbol

next to it, as shown in Figure 22-3.

FIGURE 22-3:

Holding down

the Ctrl key while

dragging code

creates a copy of

that code.

Jumping between Modules and Procedures

After your cache of macro code starts to grow, it can be a pain to quickly move

between modules and procedures. You can ease the pain by using a few shortcuts:

» Press Ctrl+Tab to quickly move between modules.

» Press Ctrl+Page Up and Ctrl+Page Down to move between procedures within

a module.

Teleporting to Your Functions

When reviewing a macro, you may sometimes encounter a variable or function

name that’s obviously pointing to some other piece of code. Instead of scouring

through all the modules to find where that function or variable name comes from,

you can simply place your cursor on that function/variable name and press Shift+F2.

As Figure 22-4 shows, you’re instantly teleported to the origin of that function or

variable name.

Pressing Ctrl+Shift+F2 takes you back to where you started.

CHAPTER 22  Ten Handy Visual Basic Editor Tips    371

FIGURE 22-4:

Pressing Shift+F2

with your cursor

on a function or

variable name

takes you to it.

Staying in the Right Procedure

When your modules contain multiple procedures, it can get difficult to scroll through a particular procedure without inadvertently scrolling into another procedure. You often find yourself scrolling up, then down, trying to get back to the

correct piece of code.

To avoid this nonsense, you can click the Procedure View button in the lower-left

hand corner of the VBE. (See Figure 22-5.) Clicking this button limits scrolling to

only the procedure you’re in.

FIGURE 22-5:

Click the

Procedure View

button to limit

scrolling to just

the active

procedure.

Stepping Through Your Code

VBA offers several tools to help you「debug」your code. In programming,  debug-

ging means finding and correcting possible errors in code.

372    PART 6  The Part of Tens

One of the more useful debugging tools is the ability to step through your code one

line at a time. When you step through code, you’re literally watching as each line

executes.

To step through your code, place your cursor anywhere within your macro and

press F8. Your macro goes into debug mode.

The first line of code is highlighted and a small arrow appears in the Code window’s left margin (see Figure 22-6). Press F8 again to execute the highlighted

line of code and move to the next line. You can keep pressing F8 to watch each line

be executed until the end of the macro.

As a bonus, while stepping through the code, you can hover over any string or

integer variable to see the current value of that variable.

To get out of debug mode, choose Debug ➪  Step Out.

FIGURE 22-6:

Press F8 key to

step through

each line of your

macro at your

own pace.

Turn to Chapter 13 for a detailed look at the ins and outs of debugging your VBA code.

Stepping to a Specific Line in Your Code

The last section showed how you can step through your code by placing your cur-

sor anywhere within your macro and pressing F8.

This is great, but what if you want to start stepping through your code at a specific line? Well, you can do just that by simply moving the arrow!

CHAPTER 22  Ten Handy Visual Basic Editor Tips    373

When a line of code is highlighted in debug mode, you can click and drag the arrow

in the left margin of the Code window upward or downward, dropping it at which-

ever line of code you want to execute next. (See Figure 22-7.)

FIGURE 22-7:

You can click and

drag the yellow

arrow while

stepping through

your code.

Stopping Your Code at a Predefined Point

Another useful debugging tool is the ability to set a breakpoint in your code. When

you set a breakpoint, your code runs as normal and then halts at the line of code

where you defined the breakpoint.

This debugging technique comes in handy when you want to run tests on small

blocks of code at a time. For example, if you suspect there is an error in your

macro but you know that the majority of the macro runs without any problems,

you can set a breakpoint starting at the suspect line of code, and then run the

macro. When the macros reaches your breakpoint, execution halts. At this point,

you can then press F8 to watch as the macro runs one line at a time.

To set a breakpoint in your code, place your cursor where you want the breakpoint

to start, and press F9. As Figure 22-8 shows, VBA clearly marks the breakpoint

with a dot in the Code window’s left margin, and the code line itself is shaded

maroon.

FIGURE 22-8:

A breakpoint is

marked by a dot

in the left margin

along with

shaded text.

374    PART 6  The Part of Tens

When your macro hits a breakpoint, it’s effectively in debug mode. To get out of

debug mode, choose Debug ➪  Step Out.

Seeing the Beginning and

End of Variable Values

If you hover over a string or integer variable in VBA while in debug mode you can

see the value of that variable in a tooltip. You can then see the values that are

being passed in and out of variables — very useful.

However, these tooltips can only hold 77 characters (including the variable name).

This basically means if the value in your variable is too long, it gets cut off.

To see the last 77 characters, hold down the Ctrl key while you hover.

Figure 22-9 shows what the tooltip looks like when hovering over a variable in

debug mode.

FIGURE 22-9:

Showing the

beginning and

ending characters

in a variable

tooltip.

Turning Off Auto Syntax Check

Oftentimes, while working on some code, you find that you need to go to another

line to copy something. You’re not done with the line — you just need to leave it

for a second. But the VBE immediately stops you in your tracks with an error mes-

sage, similar to the one shown in Figure 22-10, warning you about something you

already know.

CHAPTER 22  Ten Handy Visual Basic Editor Tips    375

These message boxes force you to stop what you’re doing to acknowledge the

error by clicking OK. After a half day of these abrupt message boxes, you’ll be ready to throw your computer against the wall.

FIGURE 22-10:

Leaving an

unfinished line of

code, even for a

second, results in

a jarring error

message.

Well, you can save your computer and your sanity by turning off Auto Syntax Checkby choosing Tools ➪  Options.

On the Editor tab of the Options dialog box, uncheck the Auto Syntax Check option

to stop these annoying error messages. See Figure 22-11.

FIGURE 22-11:

Uncheck the

Auto Syntax

Check option to

prevent warning

messages

while coding.

Don’t worry about missing a legitimate mistake. Your code still turns red if you

make a mistake, providing a visual indication that something is wrong.

376    PART 6  The Part of Tens

IN THIS CHAPTER

» Letting Excel write code for you

» Using the VBA help files

» Pilfering code from the Internet

» Leverageing user forums

» Visiting expert blogs

» Mining YouTube for video training

» Attending live and online training

classes

» Learning from the Microsoft Office

Dev Center

» Dissecting the other Excel files in

your organization

» Asking your local Excel Guru

Chapter 23

Resources for VBA Help

N o one is going to become a VBA expert in one day. VBA is a journey of time

and practice. The good news is that plenty of resources are out there that


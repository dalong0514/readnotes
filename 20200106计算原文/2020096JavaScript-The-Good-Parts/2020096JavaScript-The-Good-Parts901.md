Here is a silly stately style indeed!

—William Shakespeare, The First Part of Henry the Sixth Computer programs are the most complex things that humans make. Programs are made up of a huge number of parts, expressed as functions, statements, and expressions that are arranged in sequences that must be virtually free of error. The runtime behavior has little resemblance to the program that implements it. Software is usually expected to be modified over the course of its productive life. The process of converting one correct program into a different correct program is extremely challenging.

Good programs have a structure that anticipates—but is not overly burdened by—

the possible modifications that will be required in the future. Good programs also have a clear presentation. If a program is expressed well, then we have the best chance of being able to understand it so that it can be successfully modified or repaired.

These concerns are true for all programming languages, and are especially true for JavaScript. JavaScript’s loose typing and excessive error tolerance provide little compile-time assurance of our programs’ quality, so to compensate, we should code with strict discipline.

JavaScript contains a large set of weak or problematic features that can undermine our attempts to write good programs. We should obviously avoid JavaScript’s worst features. Surprisingly, perhaps, we should also avoid the features that are often useful but occasionally hazardous. Such features are attractive nuisances, and by avoiding them, a large class of potential errors is avoided.

The long-term value of software to an organization is in direct proportion to the quality of the codebase. Over its lifetime, a program will be handled by many pairs of hands and eyes. If a program is able to clearly communicate its structure and characteristics, it is less likely to break when it is modified in the never-too-distant future.

94

JavaScript code is often sent directly to the public. It should always be of publication quality. Neatness counts. By writing in a clear and consistent style, your programs become easier to read.

Programmers can debate endlessly on what constitutes good style. Most programmers are firmly rooted in what they’re used to, such as the prevailing style where they went to school, or at their first job. Some have had profitable careers with no sense of style at all. Isn’t that proof that style doesn’t matter? And even if style doesn’t matter, isn’t one style as good as any other?

It turns out that style matters in programming for the same reason that it matters in writing. It makes for better reading.

Computer programs are sometimes thought of as a write-only medium, so it matters little how it is written as long as it works. But it turns out that the likelihood a program will work is significantly enhanced by our ability to read it, which also increases the likelihood that it actually works as intended. It is also the nature of software to be extensively modified over its productive life. If we can read and understand it, then we can hope to modify and improve it.

Throughout this book I have used a consistent style. My intention was to make the code examples as easy to read as possible. I used whitespace consistently to give you more cues about the meaning of my programs.

I indented the contents of blocks and object literals four spaces. I placed a space between if and ( so that the if didn’t look like a function invocation. Only in invocations do I make ( adjacent with the preceding symbol. I put spaces around all infix operators except for . and [, which do not get spaces because they have higher precedence. I use a space after every comma and colon.

I put at most one statement on a line. Multiple statements on a line can be misread.

If a statement doesn’t fit on a line, I will break it after a comma or a binary operator.

That gives more protection against copy/paste errors that are masked by semicolon insertion. (The tragedy of semicolon insertion will be revealed in Appendix A.) I indent the remainder of the statement an extra four spaces, or eight spaces if four would be ambiguous (such as a line break in the condition part of an if statement).

I always use blocks with structured statements such as if and while because it is less error prone. I have seen:

if (a)

b( );

become:

if (a)

b( );

c( );

Style

|

95

which is an error that is very difficult to spot. It looks like: if (a) {

b( );

c( );

}

but it means:

if (a) {

b( );

}

c( );

Code that appears to mean one thing but actually means another is likely to cause bugs. A pair of braces is really cheap protection against bugs that can be expensive to find.

I always use the K&R style, putting the { at the end of a line instead of the front, because it avoids a horrible design blunder in JavaScript’s return statement.

I included some comments. I like to put comments in my programs to leave information that will be read at a later time by people (possibly myself) who will need to understand what I was thinking. Sometimes I think about comments as a time machine that I use to send important messages to future me.

I struggle to keep comments up-to-date. Erroneous comments can make programs even harder to read and understand. I can’t afford that.

I tried to not waste your time with useless comments like this: i = 0; // Set i to zero.

In JavaScript, I prefer to use line comments. I reserve block comments for formal documentation and for commenting out.

I prefer to make the structure of my programs self-illuminating, eliminating the need for comments. I am not always successful, so while my programs are awaiting perfection, I am writing comments.

JavaScript has C syntax, but its blocks don’t have scope. So, the convention that variables should be declared at their first use is really bad advice in JavaScript. JavaScript has function scope, but not block scope, so I declare all of my variables at the beginning of each function. JavaScript allows variables to be declared after they are used.

That feels like a mistake to me, and I don’t want to write programs that look like mistakes. I want my mistakes to stand out. Similarly, I never use an assignment expression in the condition part of an if because:

if (a = b) { ... }

is probably intended to be:

if (a === b) { ... }

96

|

Chapter 9: Style

I want to avoid idioms that look like mistakes.

I never allow switch cases to fall through to the next case. I once found a bug in my code caused by an unintended fall through immediately after having made a vigor-ous speech about why fall through was sometimes useful. I was fortunate in that I was able to learn from the experience. When reviewing the features of a language, I now pay special attention to features that are sometimes useful but occasionally dangerous. Those are the worst parts because it is difficult to tell whether they are being used correctly. That is a place where bugs hide.

Quality was not a motivating concern in the design, implementation, or standardiza-tion of JavaScript. That puts a greater burden on the users of the language to resist the language’s weaknesses.

JavaScript provides support for large programs, but it also provides forms and idioms that work against large programs. For example, JavaScript provides conveniences for the use of global variables, but global variables become increasingly problematic as programs scale in complexity.

I use a single global variable to contain an application or library. Every object has its own namespace, so it is easy to use objects to organize my code. Use of closure provides further information hiding, increasing the strength of my modules.

Style

|

97

Chapter 10

CHAPTER 10

Beautiful Features

10

Thus, expecting thy reply, I profane my lips on thy foot, my eyes on thy picture, and my heart on thy

every part. Thine, in the dearest design of industry...


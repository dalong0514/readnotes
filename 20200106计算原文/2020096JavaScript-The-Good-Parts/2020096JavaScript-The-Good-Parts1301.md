—William Shakespeare, The Comedy of Errors

When C was a young programming language, there were several common programming errors that were not caught by the primitive compilers, so an accessory program called lint was developed that would scan a source file, looking for problems.

As C matured, the definition of the language was strengthened to eliminate some insecurities, and compilers got better at issuing warnings. lint is no longer needed.

JavaScript is a young-for-its-age language. It was originally intended to do small tasks in web pages, tasks for which Java was too heavy and clumsy. But JavaScript is a very capable language, and it is now being used in larger projects. Many of the features that were intended to make the language easy to use are troublesome for larger projects. A lint for JavaScript is needed: JSLint, a JavaScript syntax checker and verifier.

JSLint is a code quality tool for JavaScript. It takes a source text and scans it. If it finds a problem, it returns a message describing the problem and an approximate location within the source. The problem is not necessarily a syntax error, although it often is. JSLint looks at some style conventions as well as structural problems. It does not prove that your program is correct. It just provides another set of eyes to help spot problems.

JSLint defines a professional subset of JavaScript, a stricter language than that defined by the third edition of the ECMAScript Language Specification. The subset is

closely related to the style recommendations from Chapter 9.

JavaScript is a sloppy language, but inside it there is an elegant, better language.

JSLint helps you to program in that better language and to avoid most of the slop.

JSLint can be found at http://www.JSLint.com/.

115

Undefined Variables and Functions

JavaScript’s biggest problem is its dependence on global variables, particularly implied global variables. If a variable is not explicitly declared (usually with the var statement), then JavaScript assumes that the variable was global. This can mask misspelled names and other problems.

JSLint expects that all variables and functions will be declared before they are used or invoked. This allows it to detect implied global variables. It is also good practice because it makes programs easier to read.

Sometimes a file is dependent on global variables and functions that are defined else-where. You can identify these to JSLint by including a comment in your file that lists the global functions and objects that your program depends on, but that are not defined in your program or script file.

A global declaration comment can be used to list all of the names that you are intentionally using as global variables. JSLint can use this information to identify misspellings and forgotten var declarations. A global declaration can look like this:

/*global getElementByAttribute, breakCycles, hanoi */

A global declaration starts with /*global. Notice that there is no space before the g.

Youcan have as many /*global comments as youlike. They must appear before the use of the variables they specify.

Some globals can be predefined for you(see the later section「Options」). Select the

「Assume a browser」(browser) option to predefine the standard global properties that are supplied by web browsers, such as window and document and alert. Select the

「Assume Rhino」(rhino) option to predefine the global properties provided by the Rhino environment. Select the「Assume a Yahoo Widget」(widget) option to predefine the global properties provided by the Yahoo! Widgets environment.

Members

Since JavaScript is a loosely typed dynamic-object language, it is not possible to determine at compile time if property names are spelled correctly. JSLint provides some assistance with this.

At the bottom of its report, JSLint displays a /*members*/ comment. It contains all of the names and string literals that were used with dot notation, subscript notation, and object literals to name the members of objects. Youcan look through the list for misspellings. Member names that were used only once are shown in italics. This is to make misspellings easier to spot.

Youcan copy the /*members*/ comment into your script file. JSLint will check the spelling of all property names against the list. That way, youcan have JSLint look for misspellings for you:

116

|

Appendix C: JSLint

/*members doTell, iDoDeclare, mercySakes, myGoodness, ohGoOn, wellShutMyMouth */

Options

The implementation of JSLint accepts an option object that allows youto determine the subset of JavaScript that is acceptable to you. It is also possible to set those options within the source of a script.

An option specification can look like this:

/*jslint nomen: true, evil: false */

An option specification starts with /*jslint. Notice that there is no space before the j. The specification contains a sequence of name/value pairs, where the names are JSLint options and the values are true or false. An option specification takes precedence over the option object. All of the options default to false. Table C-1 lists the options available in using JSLint.

Table C-1. JSLint options

Option

Meaning

adsafe

true if ADsafe.org rules should be enforced

bitwise

true if bitwise operators should not be allowed

browser

true if the standard browser globals should be predefined cap

true if uppercase HTML should be allowed

debug

true if debugger statements should be allowed

eqeqeq

true if === should be required

evil

true if eval should be allowed

forin

true if unfiltered for in statements should be allowed fragment

true if HTML fragments should be allowed

glovar

true if var should not be allowed to declare global variables laxbreak

true if statement breaks should not be checked

nomen

true if names should be checked

on

true if HTML event handlers should be allowed

passfail

true if the scan should stop on first error

plusplus

true if ++ and -- should not be allowed

rhino

true if the Rhino environment globals should be predefined undef

true if undefined global variables are errors

white

true if strict whitespace rules apply

widget

true if the Yahoo! Widgets globals should be predefined Options

|

117

JSLint comment

name

:

JSLint

true

*/

option

string

false

,

option

/*global

/*jslint

/*members

Semicolon

JavaScript uses a C-like syntax, which requires the use of semicolons to delimit statements. JavaScript attempts to make semicolons optional with a semicolon insertion mechanism. This is dangerous.

Like C, JavaScript has ++ and -- and ( operators, which can be prefixes or suffixes.

The disambiguation is done by the semicolon.

In JavaScript, a linefeed can be whitespace, or it can act as a semicolon. This replaces one ambiguity with another.

JSLint expects that every statement be followed by ; except for for, function, if, switch, try, and while. JSLint does not expect to see unnecessary semicolons or the empty statement.

Line Breaking

As a further defense against the masking of errors by the semicolon insertion mechanism, JSLint expects long statements to be broken only after one of these punctuation characters or operators:

, . ; : { } ( [ = < > ? ! + - * / % ~ ^ | &

== != <= >= += -= *= /= %= ^= |= &= << >> || &&

=== !== <<= >>= >>> >>>=

JSLint does not expect to see a long statement broken after an identifier, a string, a number, a closer, or a suffix operator:

) ] ++ --

118

|

Appendix C: JSLint

JSLint allows you to turn on the「Tolerate sloppy line breaking」(laxbreak) option.

Semicolon insertion can mask copy/paste errors. If youalways break lines after operators, then JSLint can do a better job of finding those errors.

Comma

The comma operator can lead to excessively tricky expressions. It can also mask some programming errors.

JSLint expects to see the comma used as a separator, but not as an operator (except in the initialization and incrementation parts of the for statement). It does not expect to see elided elements in array literals. Extra commas should not be used. A comma should not appear after the last element of an array literal or object literal because it can be misinterpreted by some browsers.

Required Blocks

JSLint expects that if and for statements will be made with blocks—that is, with statements enclosed in braces ({}).

JavaScript allows an if to be written like this:

if (condition)

statement;

That form is known to contribute to mistakes in projects where many programmers are working on the same code. That is why JSLint expects the use of a block: if (condition) {

statements;

}

Experience shows that this form is more resilient.

Forbidden Blocks

In many languages, a block introduces a scope. Variables introduced in a block are not visible outside of the block.

In JavaScript, blocks do not introduce a scope. There is only function-scope. A variable introduced anywhere in a function is visible everywhere in the function. JavaScript’s blocks confuse experienced programmers and lead to errors because the familiar syntax makes a false promise.

JSLint expects blocks with function, if, switch, while, for, do, and try statements and nowhere else. An exception is made for an unblocked if statement on an else or for in.

Forbidden Blocks

|

119

Expression Statements

An expression statement is expected to be an assignment, a function/method call, or delete. All other expression statements are considered errors.

for in Statement

The for in statement allows for looping through the names of all of the properties of an object. Unfortunately, it also loops through all of the members that were inherited through the prototype chain. This has the bad side effect of serving up method functions when the interest is in the data members.

The body of every for in statement should be wrapped in an if statement that does filtering. if can select for a particular type or range of values, it can exclude functions, or it can exclude properties from the prototype. For example: for (name in object) {

if (object.hasOwnProperty(name)) {

....

}

}

switch Statement

A common error in switch statements is to forget to place a break statement after each case, resulting in unintended fall-through. JSLint expects that the statement before the next case or default is one of these: break, return, or throw.

var Statement

JavaScript allows var definitions to occur anywhere within a function. JSLint is stricter.

JSLint expects that:

• A var will be declared only once, and that it will be declared before it is used.

• A function will be declared before it is used.

• Parameters will not also be declared as vars.

JSLint does not expect:

• The arguments array to be declared as a var.

• That a variable will be declared in a block. This is because JavaScript blocks do not have block scope. This can have unexpected consequences, so define all variables at the top of the function body.

120

|

Appendix C: JSLint

with Statement

The with statement was intended to provide a shorthand in accessing members in deeply nested objects. Unfortunately, it behaves very badly when setting new members. Never use the with statement. Use a var instead.

JSLint does not expect to see a with statement.

=

JSLint does not expect to see an assignment statement in the condition part of an if or while statement. This is because it is more likely that: if (a = b) {

...

}

was intended to be:

if (a == b) {

...

}

If you really intend an assignment, wrap it in another set of parentheses: if ((a = b)) {

...

}

== and !=

The == and != operators do type coercion before comparing. This is bad because it causes ' \f\r \n\t ' == 0 to be true. This can mask type errors.

When comparing to any of the following values, always use the === or !== operators, which do not do type coercion:

0 '' undefined null false true

If you want the type coercion, then use the short form. Instead of: (foo != 0)

just say:

(foo)

And instead of:

(foo == 0)

say:

(!foo)

== and !=

|

121

Use of the === and !== operators is always preferred. There is a「Disallow == and !=」

(eqeqeq) option, which requires the use of === and !== in all cases.

Labels

JavaScript allows any statement to have a label, and labels have a separate namespace.

JSLint is stricter.

JSLint expects labels only on statements that interact with break: switch, while, do, and for. JSLint expects that labels will be distinct from variables and parameters.

Unreachable Code

JSLint expects that a return, break, continue, or throw statement will be followed by a } or case or default.

Confusing Pluses and Minuses

JSLint expects that + will not be followed by + or ++, and that - will not be followed by - or --. A misplaced space can turn + + into ++, an error that is difficult to see. Use parentheses to avoid confusion.

++ and --

The ++ (increment) and -- (decrement) operators have been known to contribute to bad code by encouraging excessive trickiness. They are second only to faulty archi-tecture in enabling viruses and other security menaces. The JSLint option plusplus prohibits the use of these operators.

Bitwise Operators

JavaScript does not have an integer type, but it does have bitwise operators. The bitwise operators convert their operands from floating-point to integers and back, so they are not nearly as efficient as they are in C or other languages. They are rarely useful in browser applications. The similarity to the logical operators can mask some programming errors. The bitwise option prohibits the use of these operators.

eval Is Evil

The eval function and its relatives (Function, setTimeout, and setInterval) provide access to the JavaScript compiler. This is sometimes useful, but in most cases it indicates the presence of extremely bad coding. The eval function is the most misused feature of JavaScript.

122

|

Appendix C: JSLint

void

In most C-like languages, void is a type. In JavaScript, void is a prefix operator that always returns undefined. JSLint does not expect to see void because it is confusing and not very useful.

Regular Expressions

Regular expressions are written in a terse and cryptic notation. JSLint looks for problems that may cause portability problems. It also attempts to resolve visual ambigu-ities by recommending explicit escapement.

JavaScript’s syntax for regular expression literals overloads the / character. To avoid ambiguity, JSLint expects that the character preceding a regular expression literal is a ( or = or : or , character.

Constructors and new

Constructors are functions that are designed to be used with the new prefix. The new prefix creates a new object based on the function’s prototype, and binds that object to the function’s implied this parameter. If youneglect to use the new prefix, no new object will be made, and this will be bound to the global object. This is a serious mistake.

JSLint enforces the convention that constructor functions be given names with initial uppercase letters. JSLint does not expect to see a function invocation with an initial uppercase name unless it has the new prefix. JSLint does not expect to see the new prefix used with functions whose names do not start with initial uppercase.

JSLint does not expect to see the wrapper forms new Number, new String, or new Boolean.

JSLint does not expect to see new Object (use {} instead).

JSLint does not expect to see new Array (use [] instead).

Not Looked For

JSLint does not do flow analysis to determine that variables are assigned values before they are used. This is because variables are given a value (undefined) that is a reasonable default for many applications.

JSLint does not do any kind of global analysis. It does not attempt to determine that functions used with new are really constructors (except by enforcing capitalization conventions), or that method names are spelled correctly.

Not Looked For

|

123

HTML

JSLint is able to handle HTML text. It can inspect the JavaScript content contained within <script>...</script> tags and event handlers. It also inspects the HTML

content, looking for problems that are known to interfere with JavaScript:

• All tag names must be in lowercase.

• All tags that can take a close tag (such as </p>) must have a close tag.

• All tags are correctly nested.

• The entity &lt; must be used for literal <.

JSLint is less anal than the sycophantic conformity demanded by XHTML, but more strict than the popular browsers.

JSLint also checks for the occurrence of </ in string literals. Youshould always write

<\/ instead. The extra backslash is ignored by the JavaScript compiler, but not by the HTML parser. Tricks like this should not be necessary, and yet they are.

There is an option that allows use of uppercase tag names. There is also an option that allows the use of inline HTML event handlers.

JSON

JSLint can also check that JSON data structures are well formed. If the first character JSLint sees is { or [, then it strictly enforces the JSON rules. See Appendix E.

Report

If JSLint is able to complete its scan, it generates a function report. It lists the following for each function:

• The line number on which it starts.

• Its name. In the case of anonymous functions, JSLint will「guess」the name.

• The parameters.

• Closure: the variables and parameters that are declared in the function that are used by its inner functions.

• Variables: the variables declared in the function that are used only by the function.

• Unused: the variables that are declared in the function that are not used. This may be an indication of an error.

• Outer: variables used by this function that are declared in another function.

• Global: global variables that are used by this function.

• Label: statement labels that are used by this function.

The report will also include a list of all of the member names that were used.

124

|

Appendix C: JSLint

Appendix D

APPENDIX D

Syntax Diagrams4

Thou map of woe, that thus dost talk in signs!

—William Shakespeare, The Tragedy of Titus Andronicus

array literal

[

expression

]

,

block

{

statements

}

break statement

label

break

name

;

case clause

case

expression

:

statements

125

disruptive statement

break statement

return statement

throw statement

do statement

do

block

while

(

expression

)

;

escaped character

\

double quote

"

single quote

'

\

backslash

/

slash

backspace

b

formfeed

f

n

new line

r

carriage return

t

tab

u

4 hexadecimal digits

exponent

e

+

digit

E

-

126

|

Appendix D: Syntax Diagrams

expression

literal

name

(

expression

)

prefix operator

expression

expression

infix operator

expression

expression

expression

?

:

invocation

refinement

new

expression

invocation

delete

expression

refinement

expression statement

name

=

expression

+=

-=

invocation

refinement

delete

expression

refinement

Syntax Diagrams

|

127

for statement

initialization

for

(

expression statement

;

condition

expression

;

increment

expression statement

)

block

variable

object

name

in

expression

)

fraction

.

digit

function body

{

var statements

statements

}

function literal

function

name

parameters

function body

if statement

then

if

(

expression

)

block

else

block

128

|

Appendix D: Syntax Diagrams

infix operator

logical or

||

multiply

add

greater or equal

equal

logical and

*

+

>=

===

&&

divide

subtract

less or equal

not equal

/

-

<=

!==

modulo

greater

%

>

less

<

0

integer

any digit

except 0

digit

invocation

(

expression

)

,

literal

number literal

string literal

object literal

array literal

function

regexp literal

Syntax Diagrams

|

129

name

letter

digit

_

number literal

integer

fraction

exponent

object literal

{

name

:

expression

}

string

,

parameters

(

name

)

,

prefix operator

type of

typeof

to number

+

negate

-

logical not

!

130

|

Appendix D: Syntax Diagrams

refinement

.

name

[

expression

]

regexp choice

regexp sequence

|

regexp class

[

^

any Unicode character except / and \

]

and [ and ] and ^ and - and

control character

-

regexp class escape

regexp class escape

backspace

\

b

not

formfeed

f

newline

digit

n

D

d

carriage

whitespace

r

return

S

s

tab

word character

t

W

w

literal

u

4

hexadecimal

any special character

digits

Syntax Diagrams

|

131

regexp escape

\

not

formfeed

word boundary

f

B

b

newline

digit

n

D

d

carriage

whitespace

r

return

S

s

tab

word character

t

W

w

literal

u

4

hexadecimal

any special character

digits

back reference

integer

regexp factor

any Unicode character except / and \ and

[ and ] and ( and ) and { and } and ? and

+ and * and | and control character

regexp escape

regexp class

regexp group

regexp group

capturing

(

regexp choice

)

non-capturing

?

:

positive lookahead

=

negative lookahead

!

132

|

Appendix D: Syntax Diagrams

regexp literal

regexp choice

/

/

g

i

m

regexp quantifier

?

?

*

+

{

integer

,

integer

}

regexp sequence

regexp factor

regexp quantifier

return statement

return

expression

;

statements

expression statement

;

disruptive statement

try statement

label

name

:

if statement

switch statement

while statement

for statement

do statement

Syntax Diagrams

|

133

string literal

any Unicode character except

"

"

" and \ and control character

escaped character

any Unicode character except

'

'

' and \ and control character

escaped character

switch statement

switch

(

expression

)

{

case clause

}

disruptive

statement

default

:

statements

throw statement

throw

expression

;

var statements

var

name

=

expression

;

,

while statement

while

(

expression

)

block

134

|

Appendix D: Syntax Diagrams

whitespace

space

tab

line

end

/

/

any character

except line end

any character

*

except * and /

/

*

/

Syntax Diagrams

|

135

Appendix E

APPENDIX E

JSON

5

Farewell: the leisure and the fearful time

Cuts off the ceremonious vows of love

And ample interchange of sweet discourse,

Which so long sunder’d friends shoulddwell upon:

God give us leisure for these rites of love!


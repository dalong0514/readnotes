—William Shakespeare, Much Ado About Nothing

In this appendix, I present some of the problematic features of JavaScript that are easily avoided. By simply avoiding these features, you make JavaScript a better language, and yourself a better programmer.

==

JavaScript has two sets of equality operators: === and !==, and their evil twins == and

!=. The good ones work the way youwould expect. If the two operands are of the same type and have the same value, then === produces true and !== produces false.

The evil twins do the right thing when the operands are of the same type, but if they are of different types, they attempt to coerce the values. The rules by which they do that are complicated and unmemorable. These are some of the interesting cases:

'' == '0' // false

0 == '' // true

0 == '0' // true

false == 'false' // false

false == '0' // true

false == undefined // false

false == null // false

null == undefined // true

' \t\r\n ' == 0 // true

The lack of transitivity is alarming. My advice is to never use the evil twins. Instead, always use === and !==. All of the comparisons just shown produce false with the

=== operator.

109

with Statement

JavaScript has a with statement that was intended to provide a shorthand when accessing the properties of an object. Unfortunately, its results can sometimes be unpredictable, so it should be avoided.

The statement:

with (obj) {

a = b;

}

does the same thing as:

if (obj.a === undefined) {

a = obj.b === undefined ? b : obj.b;

} else {

obj.a = obj.b === undefined ? b : obj.b;

}

So, it is the same as one of these statements:

a = b;

a = obj.b;

obj.a = b;

obj.a = obj.b;

It is not possible to tell from reading the program which of those statements youwill get. It can vary from one running of the program to the next. It can even vary while the program is running. If you can’t read a program and understand what it is going to do, it is impossible to have confidence that it will correctly do what you want.

Simply by being in the language, the with statement significantly slows down JavaScript processors because it frustrates the lexical binding of variable names. It was well intentioned, but the language would be better if it didn’t have it.

eval

The eval function passes a string to the JavaScript compiler and executes the result.

It is the single most misused feature of JavaScript. It is most commonly used by people who have an incomplete understanding of the language. For example, if you know about the dot notation, but are ignorant of the subscript notation, you might write:

eval("myValue = myObject." + myKey + ";"); instead of:

myvalue = myObject[myKey];

The eval form is much harder to read. This form will be significantly slower because it needs to run the compiler just to execute a trivial assignment statement. It also 110

|

Appendix B: Bad Parts

frustrates JSLint (see Appendix C), so the tool’s ability to detect problems is significantly reduced.

The eval function also compromises the security of your application because it grants too much authority to the eval’d text. And it compromises the performance of the language as a whole in the same way that the with statement does.

The Function constructor is another form of eval, and should similarly be avoided.

The browser provides setTimeout and setInterval functions that can take string arguments or function arguments. When given string arguments, setTimeout and setInterval act as eval. The string argument form also should be avoided.

continue Statement

The continue statement jumps to the top of the loop. I have never seen a piece of code that was not improved by refactoring it to remove the continue statement.

switch Fall Through

The switch statement was modeled after the FORTRAN IV computed go to statement.

Each case falls through into the next case unless you explicitly disrupt the flow.

Someone wrote to me once suggesting that JSLint should give a warning when a case falls through into another case. He pointed out that this is a very common source of errors, and it is a difficult error to see in the code. I answered that that was all true, but that the benefit of compactness obtained by falling through more than compensated for the chance of error.

The next day, he reported that there was an error in JSLint. It was misidentifying an error. I investigated, and it turned out that I had a case that was falling through. In that moment, I achieved enlightenment. I no longer use intentional fall throughs.

That discipline makes it much easier to find the unintentional fall throughs.

The worst features of a language aren’t the features that are obviously dangerous or useless. Those are easily avoided. The worst features are the attractive nuisances, the features that are both useful and dangerous.

Block-less Statements

An if or while or do or for statement can take a block or a single statement. The single statement form is another attractive nuisance. It offers the advantage of saving two characters, a dubious advantage. It obscures the program’s structure so that sub-sequent manipulators of the code can easily insert bugs. For example: Block-less Statements

|

111

if (ok)

t = true;

can become:

if (ok)

t = true;

advance( );

which looks like:

if (ok) {

t = true;

advance( );

}

but which actually means:

if (ok) {

t = true;

}

advance( );

Programs that appear to do one thing but actually do another are much harder to get right. A disciplined and consistent use of blocks makes it easier to get it right.

++ --

The increment and decrement operators make it possible to write in an extremely terse style. In languages such as C, they made it possible to write one-liners that could do string copies:

for (p = src, q = dest; !*p; p++, q++) *q = *p;

They also encourage a programming style that, as it turns out, is reckless. Most of the buffer overrun bugs that created terrible security vulnerabilities were due to code like this.

In my own practice, I observed that when I used ++ and --, my code tended to be too tight, too tricky, too cryptic. So, as a matter of discipline, I don’t use them any more.

I think that as a result, my coding style has become cleaner.

Bitwise Operators

JavaScript has the same set of bitwise operators as Java:

& and

| or

^ xor

~ not

>> signed right shift

>>> unsigned right shift

<< left shift

112

|

Appendix B: Bad Parts

In Java, the bitwise operators work with integers. JavaScript doesn’t have integers. It only has double precision floating-point numbers. So, the bitwise operators convert their number operands into integers, do their business, and then convert them back.

In most languages, these operators are very close to the hardware and very fast. In JavaScript, they are very far from the hardware and very slow. JavaScript is rarely used for doing bit manipulation.

As a result, in JavaScript programs, it is more likely that & is a mistyped && operator.

The presence of the bitwise operators reduces some of the language’s redundancy, making it easier for bugs to hide.

The function Statement Versus the function Expression JavaScript has a function statement as well as a function expression. This is confusing because they can look exactly the same. A function statement is shorthand for a var statement with a function value.

The statement:

function foo( ) {}

means about the same thing as:

var foo = function foo( ) {};

Throughout this book, I have been using the second form because it makes it clear that foo is a variable containing a function value. To use the language well, it is important to understand that functions are values.

function statements are subject to hoisting. This means that regardless of where a function is placed, it is moved to the top of the scope in which it is defined. This relaxes the requirement that functions should be declared before used, which I think leads to sloppiness. It also prohibits the use of function statements in if statements.

It turns out that most browsers allow function statements in if statements, but they vary in how that should be interpreted. That creates portability problems.

The first thing in a statement cannot be a function expression because the official grammar assumes that a statement that starts with the word function is a function statement. The workaround is to wrap the function expression in parentheses: (function ( ) {

var hidden_variable;

// This function can have some impact on

// the environment, but introduces no new

// global variables.

})( );

The function Statement Versus the function Expression

|

113

Typed Wrappers

JavaScript has a set of typed wrappers. For example:

new Boolean(false)

produces an object that has a valueOf method that returns the wrapped value. This turns out to be completely unnecessary and occasionally confusing. Don’t use new Boolean or new Number or new String.

Also avoid new Object and new Array. Use {} and [] instead.

new

JavaScript’s new operator creates a new object that inherits from the operand’s prototype member, and then calls the operand, binding the new object to this. This gives the operand (which had better be a constructor function) a chance to customize the new object before it is returned to the requestor.

If youforget to use the new operator, youinstead get an ordinary function call, and this is bound to the global object instead of to a new object. That means that your function will be clobbering global variables when it attempts to initialize the new members. That is a very bad thing. There is no compile-time warning. There is no runtime warning.

By convention, functions that are intended to be used with new should be given names with initial capital letters, and names with initial capital letters should be used only with constructor functions that take the new prefix. This convention gives us a visual cue that can help spot expensive mistakes that the language itself is keen to overlook.

An even better coping strategy is to not use new at all.

void

In many languages, void is a type that has no values. In JavaScript, void is an operator that takes an operand and returns undefined. This is not useful, and it is very confusing. Avoid void.

114

|

Appendix B: Bad Parts

Appendix C

APPENDIX C

JSLint3

What error drives our eyes and ears amiss?


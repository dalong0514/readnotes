Appendix A

APPENDIX A

Awful Parts1

That will prove awful both in deed and word.

—William Shakespeare, Pericles, Prince of Tyre

In this chapter, I present the problematic features of JavaScript that are not easily avoided. You must be aware of these things and be prepared to cope.

Global Variables

The worst of all of JavaScript’s bad features is its dependence on global variables. A global variable is a variable that is visible in every scope. Global variables can be a convenience in very small programs, but they quickly become unwieldy as programs get larger. Because a global variable can be changed by any part of the program at any time, they can significantly complicate the behavior of the program. Use of global variables degrades the reliability of the programs that use them.

Global variables make it harder to run independent subprograms in the same program. If the subprograms happen to have global variables that share the same names, then they will interfere with each other and likely fail, usually in difficult to diagnose ways.

Lots of languages have global variables. For example, Java’s public static members are global variables. The problem with JavaScript isn’t just that it allows them, it requires them. JavaScript does not have a linker. All compilation units are loaded into a common global object.

There are three ways to define global variables. The first is to place a var statement outside of any function:

var foo = value;

The second is to add a property directly to the global object. The global object is the container of all global variables. In web browsers, the global object goes by the name window:

window.foo = value;

101

The third is to use a variable without declaring it. This is called implied global: foo = value;

This was intended as a convenience to beginners by making it unnecessary to declare variables before using them. Unfortunately, forgetting to declare a variable is a very common mistake. JavaScript’s policy of making forgotten variables global creates bugs that can be very difficult to find.

Scope

JavaScript’s syntax comes from C. In all other C-like languages, a block (a set of statements wrapped in curly braces) creates a scope. Variables declared in a block are not visible outside of the block. JavaScript uses the block syntax, but does not provide block scope: a variable declared in a block is visible everywhere in the function containing the block. This can be surprising to programmers with experience in other languages.

In most languages, it is generally best to declare variables at the site of first use. That turns out to be a bad practice in JavaScript because it does not have block scope. It is better to declare all variables at the top of each function.

Semicolon Insertion

JavaScript has a mechanism that tries to correct faulty programs by automatically inserting semicolons. Do not depend on this. It can mask more serious errors.

It sometimes inserts semicolons in places where they are not welcome. Consider the consequences of semicolon insertion on the return statement. If a return statement returns a value, that value expression must begin on the same line as the return: return

{

status: true

};

This appears to return an object containing a status member. Unfortunately, semicolon insertion turns it into a statement that returns undefined. There is no warning that semicolon insertion caused the misinterpretation of the program. The problem can be avoided if the { is placed at the end of the previous line and not at the beginning of the next line:

return {

status: true

};

102

|

Appendix A: Awful Parts

Reserved Words

The following words are reserved in JavaScript:

abstract boolean break byte case catch char class const continue debugger default delete do double else enum export extends false final finally float for function goto if implements import in instanceof int interface long native new null package private protected public return short static super switch synchronized this throw throws transient true try typeof var volatile void while with Most of these words are not used in the language.

They cannot be used to name variables or parameters. When reserved words are used as keys in object literals, they must be quoted. They cannot be used with the dot notation, so it is sometimes necessary to use the bracket notation instead: var method; // ok

var class; // illegal

object = {box: value}; // ok

object = {case: value}; // illegal

object = {'case': value}; // ok

object.box = value; // ok

object.case = value; // illegal

object['case'] = value; // ok

Unicode

JavaScript was designed at a time when Unicode was expected to have at most 65,536

characters. It has since grown to have a capacity of more than 1 million characters.

JavaScript’s characters are 16 bits. That is enough to cover the original 65,536

(which is now known as the Basic Multilingual Plane). Each of the remaining million characters can be represented as a pair of characters. Unicode considers the pair to be a single character. JavaScript thinks the pair is two distinct characters.

typeof

The typeof operator returns a string that identifies the type of its operand. So: typeof 98.6

produces 'number'. Unfortunately:

typeof null

returns 'object' instead of 'null'. Oops. A better test for null is simply: my_value === null

typeof

|

103

A bigger problem is testing a value for objectness. typeof cannot distinguish between null and objects, but you can because null is falsy and all objects are truthy: if (my_value && typeof my_value === 'object') {

// my_value is an object or an array!

}

Also see the later sections「NaN」and「Phony Arrays.」

Implementations disagree on the type of regular expression objects. Some implementations report that:

typeof /a/

is 'object', and others say that it is 'function'. It might have been more useful to report 'regexp', but the standard does not allow that.

parseInt

parseInt is a function that converts a string into an integer. It stops when it sees a nondigit, so parseInt("16") and parseInt("16 tons") produce the same result. It would be nice if the function somehow informed us about the extra text, but it doesn’t.

If the first character of the string is 0, then the string is evaluated in base 8 instead of base 10. In base 8, 8 and 9 are not digits, so parseInt("08") and parseInt("09") produce 0 as their result. This error causes problems in programs that parse dates and times. Fortunately, parseInt can take a radix parameter, so that parseInt("08",10) produces 8. I recommend that you always provide the radix parameter.

+

The + operator can add or concatenate. Which one it does depends on the types of the parameters. If either operand is an empty string, it produces the other operand converted to a string. If both operands are numbers, it produces the sum. Otherwise, it converts both operands to strings and concatenates them. This complicated behavior is a common source of bugs. If you intend + to add, make sure that both operands are numbers.

Floating Point

Binary floating-point numbers are inept at handling decimal fractions, so 0.1 + 0.2 is not equal to 0.3. This is the most frequently reported bug in JavaScript, and it is an intentional consequence of having adopted the IEEE Standard for Binary Floating-Point Arithmetic (IEEE 754). This standard is well-suited for many applications, but it violates most of the things you learned about numbers in middle school.

104

|

Appendix A: Awful Parts

Fortunately, integer arithmetic in floating point is exact, so decimal representation errors can be avoided by scaling.

For example, dollar values can be converted to whole cents values by multiplying them by 100. The cents then can be accurately added. The sum can be divided by 100 to convert back into dollars. People have a reasonable expectation when they count money that the results will be exact.

NaN

The value NaN is a special quantity defined by IEEE 754. It stands for not a number, even though:

typeof NaN === 'number' // true

The value can be produced by attempting to convert a string to a number when the string is not in the form of a number. For example:

+ '0' // 0

+ 'oops' // NaN

If NaN is an operand in an arithmetic operation, then NaN will be the result. So, if you have a chain of formulas that produce NaN as a result, at least one of the inputs was NaN, or NaN was generated somewhere.

Youcan test for NaN. As we have seen, typeof does not distinguish between numbers and NaN, and it turns out that NaN is not equal to itself. So, surprisingly: NaN === NaN // false

NaN !== NaN // true

JavaScript provides an isNaN function that can distinguish between numbers and NaN: isNaN(NaN) // true

isNaN(0) // false

isNaN('oops') // true

isNaN('0') // false

The isFinite function is the best way of determining whether a value can be used as a number because it rejects NaN and Infinity. Unfortunately, isFinite will attempt to convert its operand to a number, so it is not a good test if a value is not actually a number. You may want to define your own isNumber function: var isNumber = function isNumber(value) { return typeof value === 'number' && isFinite(value);

}

Phony Arrays

JavaScript does not have real arrays. That isn’t all bad. JavaScript’s arrays are really easy to use. There is no need to give them a dimension, and they never generate out-of-bounds errors. But their performance can be considerably worse than real arrays.

Phony Arrays

|

105

The typeof operator does not distinguish between arrays and objects. To determine that a value is an array, you also need to consult its constructor property: if (my_value && typeof my_value === 'object' && my_value.constructor === Array) {

// my_value is an array!

}

That test will give a false negative if an array was created in a different frame or window. This test is more reliable when the value might have been created in another frame:

if (my_value && typeof my_value === 'object' && typeof my_value.length === 'number' &&

!(my_value.propertyIsEnumerable('length')) {

// my_value is truly an array!

}

The arguments array is not an array; it is an object with a length member. That test will identify the arguments array as an array, which is sometimes what youwant, even though arguments does not have any of the array methods. In any case, the test can still fail if the propertyIsEnumerable method is overridden.

Falsy Values

JavaScript has a surprisingly large set of falsy values, shown in Table A-1.

Table A-1. The many falsy values of JavaScript

Value

Type

0

Number

NaN (not a number)

Number

'' (empty string)

String

false

Boolean

null

Object

undefined

Undefined

These values are all falsy, but they are not interchangeable. For example, this is the wrong way to determine if an object is missing a member: value = myObject[name];

if (value == null) {

alert(name + ' not found.');

}

undefined is the value of missing members, but the snippet is testing for null. It is using the == operator (see Appendix B), which does type coercion, instead of the more reliable === operator. Sometimes those two errors cancel each other out. Sometimes they don’t.

106

|

Appendix A: Awful Parts

undefined and NaN are not constants. They are global variables, and youcan change their values. That should not be possible, and yet it is. Don’t do it.

hasOwnProperty

In Chapter 3, the hasOwnProperty method was offered as a filter to work around a problem with the for in statement. Unfortunately, hasOwnProperty is a method, not an operator, so in any object it could be replaced with a different function or even a value that is not a function:

var name;

another_stooge.hasOwnProperty = null; // trouble for (name in another_stooge) {

if (another_stooge.hasOwnProperty(name)) { // boom

document.writeln(name + ': ' + another_stooge[name]);

}

}

Object

JavaScript’s objects are never truly empty because they can pick up members from the prototype chain. Sometimes that matters. For example, suppose you are writing a program that counts the number of occurrences of each word in a text. We can use the toLowerCase method to normalize the text to lowercase, and then use the split method with a regular expression to produce an array of words. We can then loop through the words and count the number of times we see each one: var i;

var word;

var text =

"This oracle of comfort has so pleased me, " +

"That when I am in heaven I shall desire " +

"To see what this child does, " +

"and praise my Constructor.";

var words = text.toLowerCase( ).split(/[\s,.]+/);

var count = {};

for (i = 0; i < words.length; i += 1) {

word = words[i];

if (count[word]) {

count[word] += 1;

} else {

count[word] = 1;

}

}

If we look at the results, count['this'] is 2 and count.heaven is 1, but count.

constructor contains a crazy looking string. The reason is that the count object inherits from Object.prototype, and Object.prototype contains a member named Object

|

107

constructor whose value is Object. The += operator, like the + operator, does concatenation rather than addition when its operands are not numbers. Object is a function, so += converts it to a string somehow and concatenates a 1 to its butt.

We can avoid problems like this the same way we avoid problems with for in: by testing for membership with the hasOwnProperty method or by looking for specific types. In this case, our test for the truthiness of count[word] was not specific enough.

We could have written instead:

if (typeof count[word] === 'number') {

108

|

Appendix A: Awful Parts

Appendix B

APPENDIX B

Bad Parts2

And, I pray thee now, tell me for

which of my bad parts didst thou first fall in love with me?


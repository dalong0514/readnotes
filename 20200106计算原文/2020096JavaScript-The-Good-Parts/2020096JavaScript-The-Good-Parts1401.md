Once more, adieu: be valiant, and speed well!

—William Shakespeare, The Tragedy of Richard the Third JavaScript Object Notation (JSON) is a lightweight data interchange format. It is based on JavaScript’s object literal notation, one of JavaScript’s best parts. Even though it is a subset of JavaScript, it is language independent. It can be used to exchange data between programs written in all modern programming languages. It is a text format, so it is readable by humans and machines. It is easy to implement and easy to use. There is a lot of material about JSON at http://www.JSON.org/.

JSON Syntax

JSON has six kinds of values: objects, arrays, strings, numbers, booleans (true and false), and the special value null. Whitespace (spaces, tabs, carriage returns, and newline characters) may be inserted before or after any value. This can make JSON

texts easier for humans to read. Whitespace may be omitted to reduce transmission or storage costs.

A JSON object is an unordered container of name/value pairs. A name can be any string. A value can be any JSON value, including arrays and objects. JSON objects can be nested to any depth, but generally it is most effective to keep them relatively flat. Most languages have a feature that maps easily to JSON objects, such as an object, struct, record, dictionary, hash table, property list, or associative array.

The JSON array is an ordered sequence of values. A value can be any JSON value, including arrays and objects. Most languages have a feature that maps easily onto JSON arrays, such as an array, vector, list, or sequence.

136

JSON value

JSON object

JSON array

JSON string

JSON number

true

false

null

JSON object

JSON string

JSON value

{

:

}

,

JSON array

JSON value

[

]

,

A JSON string is wrapped in double quotes. The \ character is used for escapement.

JSON allows the / character to be escaped so that JSON can be embedded in HTML

<script> tags. HTML does not allow the sequence </ except to start the </script> tag. JSON allows <\/, which produces the same result but does not confuse HTML.

JSON numbers are like JavaScript numbers. A leading zero is not allowed on integers because some languages use that to indicate the octal. That kind of radix confusion is not desirable in a data interchange format. A number can be an integer, real, or scientific.

That’s it. That is all of JSON. JSON’s design goals were to be minimal, portable, tex-tual, and a subset of JavaScript. The less we need to agree on in order to interoperate, the more easily we can interoperate.

JSON Syntax

|

137

JSON string

any Unicode character except

"

"

" or \ or control character

\

quotation mark

"

reverse solidus

\

solidus

/

backspace

b

formfeed

f

newline

n

carriage return

r

horizontal tab

t

u

4 hexadecimal digits

JSON number

integer

fraction

exponent

0

-

.

E

e

digit 1-9

+

-

digit

digit

digit

[

{

"first": "Jerome",

"middle": "Lester",

"last": "Howard",

"nick-name": "Curly",

"born": 1903,

"died": 1952,

"quote": "nyuk-nyuk-nyuk!"

138

|

Appendix E: JSON

},

{

"first": "Harry",

"middle": "Moses",

"last": "Howard",

"nick-name": "Moe",

"born": 1897,

"died": 1975,

"quote": "Why, you!"

},

{

"first": "Louis",

"last": "Feinberg",

"nick-name": "Larry",

"born": 1902,

"died": 1975,

"quote": "I'm sorry. Moe, it was an accident!"

}

]

Using JSON Securely

JSON is particularly easy to use in web applications because JSON is JavaScript. A JSON text can be turned into a useful data structure with the eval function: var myData = eval('(' + myJSONText + ')');

(The concatenation of the parentheses around the JSON text is a workaround for an ambiguity in JavaScript’s grammar.)

The eval function has horrendous security problems, however. Is it safe to use eval to parse a JSON text? Currently, the best technique for obtaining data from a server in a web browser is through XMLHttpRequest. XMLHttpRequest can obtain data only from the same server that produced the HTML. evaling text from that server is no less secure than the original HTML. But, that assumes the server is malicious. What if the server is simply incompetent?

An incompetent server might not do the JSON encoding correctly. If it builds JSON

texts by slapping together some strings rather than using a proper JSON encoder, then it could unintentionally send dangerous material. If it acts as a proxy and simply passes JSON text through without determining whether it is well formed, then it could send dangerous material again.

The danger can be avoided by using the JSON.parse method instead of eval (see http://

www.JSON.org/json2.js). JSON.parse will throw an exception if the text contains anything dangerous. It is recommended that you always use JSON.parse instead of eval to defend against server incompetence. It is also good practice for the day when the browser provides safe data access to other servers.

Using JSON Securely

|

139

There is another danger in the interaction between external data and innerHTML. A common Ajax pattern is for the server to send an HTML text fragment that gets assigned to the innerHTML property of an HTML element. This is a very bad practice.

If the HTML text contains a <script> tag or its equivalent, then an evil script will run. This again could be due to server incompetence.

What specifically is the danger? If an evil script gets to run on your page, it gets access to all of the state and capabilities of the page. It can interact with your server, and your server will not be able to distinguish the evil requests from legitimate requests. The evil script has access to the global object, which gives it access to all of the data in the application except for variables hidden in closures. It has access to the document object, which gives it access to everything that the user sees. It also gives the evil script the capability to dialog with the user. The browser’s location bar and all of the anti-phishing chrome will tell the user that the dialog should be trusted.

The document object also gives the evil script access to the network, allowing it to load more evil scripts, or to probe for sites within your firewall, or to send the secrets it has learned to any server in the world.

This danger is a direct consequence of JavaScript’s global object, which is far and away the worst part of JavaScript’s many bad parts. These dangers are not caused by Ajax or JSON or XMLHttpRequest or Web 2.0 (whatever that is). These dangers have been in the browser since the introduction of JavaScript, and will remain until JavaScript is replaced. Be careful.

A JSON Parser

This is an implementation of a JSON parser in JavaScript: var json_parse = function () {

// This is a function that can parse a JSON text, producing a JavaScript

// data structure. It is a simple, recursive descent parser.

// We are defining the function inside of another function to avoid creating

// global variables.

var at, // The index of the current character

ch, // The current character

escapee = {

'"': '"'

'\\': '\\',

'/': '/',

b: 'b',

f: '\f',

n: '\n',

r: '\r'

t: '\t'

},

140

|

Appendix E: JSON

text,

error = function (m) {

// Call error when something is wrong.

throw {

name: 'SyntaxError',

message: m,

at: at,

text: text

};

},

next = function (c) {

// If a c parameter is provided, verify that it matches the current character.

if (c && c !== ch) {

error("Expected '" + c + "’ instead of '" + ch + "'");

}

// Get the next character. When there are no more characters,

// return the empty string.

ch = text.charAt(at);

at += 1;

return ch;

},

number = function () {

// Parse a number value.

var number,

string = '';

if (ch === '-') {

string = '-';

next('-');

}

while (ch >= '0' && ch <= '9') {

string += ch;

next();

}

if (ch === '.') {

string += '.';

while (next() && ch >= '0' && ch <= '9') {

string += ch;

}

}

if (ch === 'e' || ch === 'E') {

string += ch;

next();

A JSON Parser

|

141

if (ch === '-' || ch === '+') {

string += ch;

next();

}

while (ch >= '0' && ch <= '9') {

string += ch;

next();

}

}

number = +string;

if (isNaN(number)) {

error("Bad number");

} else {

return number;

}

},

string = function () {

// Parse a string value.

var hex,

i,

string = '',

uffff;

// When parsing for string values, we must look for " and \ characters.

if (ch === '"') {

while (next()) {

if (ch === '"') {

next();

return string;

} else if (ch === '\\') {

next();

if (ch === 'u') {

uffff = 0;

for (i = 0; i < 4; i += 1) {

hex = parseInt(next(), 16);

if (!isFinite(hex)) {

break;

}

uffff = uffff * 16 + hex;

}

string += String.fromCharCode(uffff);

} else if (typeof escapee[ch] === ’string’) {

string += escapee[ch];

} else {

break;

}

} else {

string += ch;

}

}

142

|

Appendix E: JSON

}

error("Bad string");

},

white = function () {

// Skip whitespace.

while (ch && ch <= ' ') {

next();

}

},

word = function () {

// true, false, or null.

switch (ch) {

case ’t’:

next('t');

next('r');

next('u');

next('e');

return true;

case 'f':

next('f');

next('a');

next('l');

next('s');

next('e');

return false;

case 'n':

next('n');

next('u');

next('l');

next('l');

return null;

}

error("Unexpected '" + ch + "'");

},

value, // Place holder for the value function.

array = function () {

// Parse an array value.

var array = [];

if (ch === '[') {

next('[');

white();

if (ch === ']') {

next(']');

return array; // empty array

A JSON Parser

|

143

}

while (ch) {

array.push(value());

white();

if (ch === ']') {

next(']');

return array;

}

next(',');

white();

}

}

error("Bad array");

},

object = function () {

// Parse an object value.

var key,

object = {};

if (ch === '{') {

next('{');

white();

if (ch === '}') {

next('}');

return object; // empty object

}

while (ch) {

key = string();

white();

next(':');

object[key] = value();

white();

if (ch === '}') {

next('}');

return object;

}

next(',');

white();

}

}

error("Bad object");

};

value = function () {

// Parse a JSON value. It could be an object, an array, a string, a number,

// or a word.

white();

switch (ch) {

case '{':

return object();

144

|

Appendix E: JSON

case '[':

return array();

case '"':

return string();

case '-':

return number();

default:

return ch >= '0' && ch <= '9' ? number() : word();

}

};

// Return the json_parse function. It will have access to all of the above

// functions and variables.

return function (source, reviver) {

var result;

text = source;

at = 0;

ch = ' ';

result = value();

white();

if (ch) {

error("Syntax error");

}

// If there is a reviver function, we recursively walk the new structure,

// passing each name/value pair to the reviver function for possible

// transformation, starting with a temporary boot object that holds the result

// in an empty key. If there is not a reviver function, we simply return the

// result.

return typeof reviver === 'function' ?

function walk(holder, key) {

var k, v, value = holder[key];

if (value && typeof value === 'object') {

for (k in value) {

if (Object.hasOwnProperty.call(value, k)) {

v = walk(value, k);

if (v !== undefined) {

value[k] = v;

} else {

delete value[k];

}

}

}

}

return reviver.call(holder, key, value);

}({'': result}, '') : result;

};

}();

A JSON Parser

|

145

Index

Symbols

A

-- decrement operator, 112, 118, 122

adsafe option (JSLint), 117

- negation operator, 122

Apply Invocation Pattern, 30

-- operator, confusing pluses and

arguments, 31

minuses, 122

arguments array, 106

- subtraction operator, 122

array literals, 18

!= operator, 109, 121

array.concat( ) method, 78

!== operator, 109

array.join( ) method, 78

& and, 112

array.pop( ) method, 79

&& operator, 16

Array.prototype, 62

+ operator, 16, 104

array.push( ) method, 79

confusing pluses and minuses, 122

array.reverse( ) method, 79

++ increment operator, 112, 118, 122

array.shift( ) method, 79

confusing pluses and minuses, 122

array.slice( ) method, 80

+= operator, 15

array.sort( ) method, 80–82

<< left shift, 112

array.splice( ) method, 82–83

= operator, 15, 121

array.unshift( ) method, 83

== operator, 106, 109, 121

arrays, 58–64, 105

=== operator, 15, 106, 109

appending new elements, 60

>> signed right shift, 112

arrays of arrays, 63

>>> unsigned right shift, 112

cells of an empty matrix, 64

? ternary operator, 15

confusion, 61

[ ] postfix subscript operator, 59

delete operator, 60

\ escape character, 8

dimensions, 63

^ xor, 112

elements of, 59

| or, 112

enumeration, 60

|| operator, 17, 21

length property, 59

~ not, 112

literals, 58

⁄ operator, 16

methods, 62

⁄* *⁄ form of block comments, 6

Object.create method, 63

⁄⁄ comments, 6

splice method, 60

typeof operator, 61

undefined value, 63

assignment, 121

We’d like to hear your suggestions for improving our indexes. Send email to index@oreilly.com.

147

assignment statement, 121

E

augmenting types, 32

ECMAScript Language Specification, 115

empty string, 12

B

enumeration, 24

beautiful features, 98–100

eqeqeq option (JSLint), 117

bitwise operators, 112, 122

equality operators, 109

bitwise option (JSLint), 117

escape character, 8

block comments, 6, 96

escape sequences, 9

block scope, 36, 99

eval function, 110, 122

blockless statements, 111

security problems, 139

blocks, 10, 119

evil option (JSLint), 117

booleans, 20

exceptions, 32

braces, 96

executable statements, 10

break statement, 12, 14, 122

expression statements, 120

browser option (JSLint), 117

expressions, 15–17

built-in value, 15

? ternary operator, 15

built-in value, 15

C

infix operator, 15

invocation, 15

callbacks, 40

literal value, 15

cap option (JSLint), 117

operator precedence, 16

cascades, 42

preceded by prefix operator, 15

case clause, 12

refinement, 15

casting, 46

refinement expression preceded by

catch clause, 13

delete, 15

character type, 8

variables, 15

closure, 37–39

wrapped in parentheses, 15

code quality tool (see JSLint)

comma operator, 119

F

comments, 6, 96

concatenation, 104

factorial, 35, 45

constructor functions, 123

Fibonacci numbers, 44

hazards, 49

floating-point numbers, 104

new prefix, forgetting to include, 49

for in statement, 13, 120

Constructor Invocation Pattern, 29

objects, 24

constructor property, 47

for statements, 10, 12, 119

constructors, 30

forin option (JSLint), 117

defining, 47

fragment option (JSLint), 117

continue statement, 111, 122

Function constructor, 47, 111

curly braces, 10

function invocation, 95

curry method, 43

Function Invocation Pattern, 28

function object, when object is created, 47

D

function statement versus function

expression, 113

debug option (JSLint), 117

function.apply( ) method, 84

deentityify method, 40

functional pattern (inheritance), 52–55

delegation, 23

functions, 19, 26–45, 116

delete operator, 24, 60

arguments, 31

differential inheritance, 51

augmenting types, 32

do statement, 10, 13

callbacks, 40

Document Object Model (DOM), 34

durable object, 55

148

|

Index

cascades, 42

H

closure, 37–39

hasOwnProperty method, 23, 107, 108

curry method, 43

HTML

exceptions, 32

<script> tags (JSON), 137

general pattern of a module, 41

innerHTML property, 140

invocation, 27–30

JSLint, 124

Apply Invocation Pattern, 30

Constructor Invocation Pattern, 29

Function Invocation Pattern, 28

I

Method Invocation Pattern, 28

if statements, 10, 119

new prefix, 29

implied global, 102

invocation operator, 28

Infinity, 7, 8, 15

invoked with constructor invocation, 47

inheritance, 3, 46–57

literals, 27

differential, 51

memoization, 44

functional pattern, 52–55

modules, 40–42

object specifiers, 50

objects, 26

parts, 55–57

recursive, 34–36

prototypal pattern (inheritance), 50

Document Object Model (DOM), 34

pseudoclassical pattern, 47–49, 54

Fibonacci numbers, 44

inherits method, 49

tail recursion optimization, 35

innerHTML property, 140

Towers of Hanoi puzzle, 34

instances, creating, 48

return statement, 31

invocation operator, 17, 28

scope, 36

invocations, 95

that produce objects, 52

var statements, 10

J

JavaScript

G

analyzing, 3–4

global declarations, 116

standard, 4

global object, 140

why use, 2

global variables, 25, 97, 101, 116

JavaScript Object Notation (see JSON)

glovar option (JSLint), 117

JSLint, 4, 115–124

good style, 95

-- decrement operator, 122

grammar, 5–19

confusing pluses and minuses, 122

expressions (see expressions)

- operator, confusing pluses and

functions, 19

minuses, 122

literals, 17

!= operator, 121

names, 6

+ operator, confusing pluses and

numbers, 7

minuses, 122

methods, 8

++ increment operator, 122

negative, 8

confusing pluses and minuses, 122

object literals, 17

= operator, 121

rules for interpreting diagrams, 5

== operator, 121

statements (see statements)

assignment statement, 121

strings, 8

bitwise operators, 122

immutability, 9

blocks, 119

length property, 9

break statement, 122

whitespace, 5

comma operator, 119

constructor functions, 123

Index

|

149

JSLint (continued)

L

continue statement, 122

labeled statement, 14

eval function, 122

labels, 122

expression statements, 120

language, structure (see grammar)

for in statement, 120

laxbreak option (JSLint), 117

for statements, 119

length property (arrays), 59

function report, 124

line breaking, 118

functions, 116

line comments, 96

global declarations, 116

line-ending comments, 6

global variables, 116

looping statement, 12, 14

HTML, 124

loosely typed language, 46

if statements, 119

JSON, 124

labels, 122

M

line breaking, 118

Math object, 8

members, 116

memoization, 44

new prefix, 123

message property, 14

options, 117

Method Invocation Pattern, 28

regular expressions, 123

method method, 49

return statement, 122

methods, 78–93

semicolons, 118

array.concat( ), 78

switch statements, 120

array.join( ), 78

throw statement, 122

array.pop( ), 79

var statements, 120

array.push( ), 79

variables, 116

array.reverse( ), 79

void, 123

array.shift( ), 79

where to find, 115

array.slice( ), 80

with statement, 121

array.sort( ), 80–82

JSON, 124

array.splice( ), 82–83

JSON (JavaScript Object Notation), 3,

array.unshift ( ), 83

136–140

arrays, 62

⁄ character, 137

function.apply( ), 84

array, 136

number.toExponential( ), 84

eval function, 139

number.toFixed( ), 85

HTML <script> tags, 137

number.toPrecision( ), 85

innerHTML property, 140

number.toString( ), 85

JSLint, 124

object.hasOwnProperty( ), 86

numbers, 137

regexp.exec( ), 65, 86

object, 136

regexp.test( ), 65, 88

string, 137

string.charAt( ), 88

syntax, 136–139

string.charCodeAt( ), 88

text example, 138

string.concat( ), 88

using securely, 139

String.fromCharCode( ), 93

JSON.parse method, 139

string.indexOf( ), 88

string.lastIndexOf( ), 89

K

string.localeCompare( ), 89

string.match( ), 65, 89

K&R style, 96

string.replace( ), 65, 90

Kleene, Stephen, 65

string.search( ), 65, 91

string.slice( ), 91

string.split( ), 65, 91

150

|

Index

string.substring( ), 92

literals, 20

string.toLocaleLowerCase( ), 92

properties, 21

string.toLocaleUpperCase( ), 92

property on prototype chain, 23

string.toLowerCase( ), 92

prototype, 22

string.toUpperCase( ), 93

link, 23

that work with regular expressions, 65

reference, 22

modules, 40–42

reflection, 23

general pattern, 41

retrieving values, 21

multiple statements, 95

undefined, 21, 23

my object, 53

updating values, 22

on option (JSLint), 117

N

operator precedence, 16

name property, 14

names, 6

P

NaN (not a number), 7, 8, 12, 15, 105

parseInt function, 104

negative numbers, 8

passfail option (JSLint), 117

new operator, 15, 47, 114, 123

pi as simple constant, 99

forgetting to include, 49

plusplus option (JSLint), 117

functions, 29

Pratt, Vaughn, 98

newline, 73

private methods, 53

nomen option (JSLint), 117

privileged methods, 53

null, 11, 15, 20, 106

problematic features of JavaScript, 101–114

number literal, 8

+ operator, 104

number.toExponential( ) method, 84

arrays, 105

number.toFixed( ) method, 85

bitwise operators, 112

number.toPrecision( ) method, 85

blockless statements, 111

number.toString( ) method, 85

continue statement, 111

numbers, 7, 20

equality operators, 109

methods, 8

eval function, 110

negative, 8

falsy values, 106

numbers object, 59

floating-point numbers, 104

function statement versus function

O

expression, 113

global variables, 101

object literals, 17, 59

hasOwnProperty method, 107

object specifiers, 50

increment and decrement operators, 112

Object.create method, 53, 63

NaN (not a number), 105

object.hasOwnProperty( ) method, 86

new operator, 114

Object.prototype, 62

objects, 107

objects, 20–25, 107

parseInt function, 104

|| operator, 21

reserved words, 103

creating new, 22

scope, 102

defined, 20

semicolons, 102

delegation, 23

single statement form, 111

delete operator, 24

string argument form, 111

durable, 55

switch statement, 111

enumeration, 24

typed wrappers, 114

for in statement, 24

typeof operator, 103

functions, 26

Unicode, 103

global variables, 25

void, 114

hasOwnProperty method, 23

with statement, 110

Index

|

151

prototypal inheritance, 3

elements, 72–77

prototypal inheritance language, 29

regexp choice, 72

prototypal pattern, 50

regexp class, 75

prototype property, 47

regexp class escape, 76

prototypes of basic types, 33

regexp escape, 73–74

pseudoclass, creating, 48

regexp factor, 73, 76

pseudoclassical pattern (inheritance), 47–49,

regexp group, 74

54

regexp quantifier, 76

punctuation characters or operators, 118

regexp sequence, 72

flags, 71

R

formfeed character, 73

matching digits, 70

railroad diagrams, 67

matching URLs, 66–70

recursion, 34–36

methods that work with, 65

Document Object Model (DOM), 34

negative lookahead group, 75

Fibonacci numbers, 44

newline character, 73

tail recursion optimization, 35

noncapturing group, 67, 75

Towers of Hanoi puzzle, 34

optional group, 68

reflection, 23

optional noncapturing group, 70

RegExp objects, properties, 72

positive lookahead group, 75

regexp.exec( ) method, 65, 86

railroad diagrams, 67

regexp.test( ) method, 65, 88

repeat zero or one time, 68

regular expressions, 65–77, 123

simple letter class, 74

$ character, 69

sloppy, 68

(...), 68

tab character, 73

(?! prefix, 75

Unicode characters, 73

(?: prefix, 75

reserved words, 7, 103

(?:...)?, 70

return statement, 14, 31, 122

(?= prefix, 75

rhino option (JSLint), 117

? character, 67

\1 character, 74

\b character, 73, 74

S

\d, 70

says method, 53

\D character, 73

scope, 10, 36, 102

\d character, 73

semicolons, 102, 118

\f character, 73

seqer object, 42

\n character, 73

setInterval function, 111

\r character, 73

setTimeout function, 111

\S character, 73

Simplified JavaScript, 98

\s character, 73

single statement form, 111

\t character, 73

spec object, 52, 53

\u character, 73

splice method (arrays), 60

\W character, 73

statements, 10–15

\w character, 73

blocks, 10

^ character, 67, 69

break, 12, 14

⁄ character, 68

case clause, 12

backslash character, 73–74

catch clause, 13

capturing group, 68, 74

do, 10, 13

carriage return character, 73

executable, 10

construction, 70–72

execution order, 10

152

|

Index

for, 10, 12

multiple statements, 95

for in, 13

structured statements, 95

if, 10

switch cases, 97

labeled, 14

super methods, 49

loop, 14

superior method, 54

looping, 12

switch statement, 10, 12, 14, 97, 111, 120

return, 14

syntax checker (see JSLint)

switch, 10, 12, 14

syntax diagrams, 125–135

then block, 10

throw, 14

T

try, 13

tail recursion optimization, 35

var, functions, 10

testing environment, 4

while, 10, 12

then block, 10

string argument form, 111

this keyword, 49

string literal, 8

Thompson, Ken, 65

String, augmenting with deentityify

throw statement, 14, 122

method, 40

Top Down Operator Precedence parser, 98

string.charAt( ) method, 88

Towers of Hanoi puzzle, 34

string.charCodeAt( ) method, 88

trim method, 33

string.concat( ) method, 88

try statement, 13

String.fromCharCode( ) method, 93

typed wrappers, 114

string.indexOf( ) method, 88

TypeError exception, 21

string.lastIndexOf( ) method, 89

typeof operator, 16, 61, 103, 106

string.localeCompare( ) method, 89

types, 20

string.match( ) method, 65, 89

prototypes of, 33

string.replace( ) method, 65, 90

string.search( ) method, 65, 91

string.slice( ) method, 91

U

string.split( ) method, 65, 91

undef option (JSLint), 117

string.substring( ) method, 92

undefined, 7, 12, 15, 20, 21, 23, 28, 31, 63,

string.toLocaleLowerCase( ) method, 92

106

string.toLocaleUpperCase( ) method, 92

Unicode, 103

string.toLowerCase( ) method, 92

string.toUpperCase( ) method, 93

V

strings, 8, 20

empty, 12

var statements, 120

immutability, 9

functions, 10

length property, 9

variables, 15, 116

structure of language (see grammar)

verifier (see JSLint)

structured statements, 95

void operator, 114, 123

style, 94–97

block comments, 96

W

braces, 96

while statement, 10, 12

comments, 96

white option (JSLint), 117

global variables, 97

whitespace, 5

good, 95

widget option (JSLint), 117

invocations, 95

Wilson, Greg, 98

K&R, 96

with statement, 110, 121

line comments, 96

wrappers, typed, 114

Index

|

153

About the Author

Douglas Crockford is a senior JavaScript architect at Yahoo! who is well known for discovering and popularizing the JSON (JavaScript Object Notation) format. He is the world’s foremost living authority on JavaScript. He speaks regularly at conferences about advanced web technology, and he also serves on the ECMAScript committee.

Colophon

The animal on the cover of JavaScript: The Good Parts is a Plain Tiger butterfly ( Danaus chrysippus). Outside of Asia, the insect is also known as the African Monarch. It is a medium-size butterfly characterized by bright orange wings with six black spots and alternating black-and-white stripes.

Its striking looks have been noted for millennia by scientists and artists. The writer Vladimir Nabokov—who was also a noted lepidopterist—had admiring words for the butterfly in an otherwise scathing NewYork Times book review of Alice Ford’s Audubon’s Butterflies, Moths, and Other Studies (The Studio Publications). In the book, Ford labels drawings made previous to and during Audubon’s time in the 19th century as「scientifi-cally [ sic] unsophisticated.」

In response to Ford, Nabokov writes,「The unsophistication is all her own. She might have looked up John Abbot’s prodigious representations of North American lepidoptera, 1797, or the splendid plates of 18th- and early-19th-century German lepidopterists. She might have traveled back some 33 centuries to the times of Tuth-mosis IV or Amenophis III and, instead of the obvious scarab, found there frescoes with a marvelous Egyptian butterfly (subtly combining the pattern of our Painted Lady and the body of an African ally of the Monarch).」

While the Plain Tiger’s beauty is part of its charm, its looks can also be deadly.

During its larval stages, the butterfly ingests alkaloids that are poisonous to birds—

its main predator—which are often attracted to the insect’s markings. After ingesting the Plain Tiger, a bird will vomit repeatedly—occasionally fatally. If the bird lives, it will let other birds know to avoid the insect, which can also be recognized by its leisurely, meandering pattern of flying low to the earth.

The cover image is from Dover’s Animals. The cover font is Adobe ITC Garamond.

The text font is Linotype Birka; the heading font is Adobe Myriad Condensed; and the code font is LucasFont’s TheSans Mono Condensed.

Document Outline

Table of Contents

Preface Conventions Used in This Book

Using Code Examples

Safari® Books Online

How to Contact Us

Acknowledgments

Good Parts Why JavaScript?

Analyzing JavaScript

A Simple Testing Ground

Grammar Whitespace

Names

Numbers

Strings

Statements

Expressions

Literals

Functions

Objects Object Literals

Retrieval

Update

Reference

Prototype

Reflection

Enumeration

Delete

Global Abatement

Functions Function Objects

Function Literal

Invocation The Method Invocation Pattern

The Function Invocation Pattern

The Constructor Invocation Pattern

The Apply Invocation Pattern

Arguments

Return

Exceptions

Augmenting Types

Recursion

Scope

Closure

Callbacks

Module

Cascade

Curry

Memoization

Inheritance Pseudoclassical

Object Specifiers

Prototypal

Functional

Parts

Arrays Array Literals

Length

Delete

Enumeration

Confusion

Methods

Dimensions

Regular Expressions An Example

Construction

Elements Regexp Choice

Regexp Sequence

Regexp Factor

Regexp Escape

Regexp Group

Regexp Class

Regexp Class Escape

Regexp Quantifier

Methods Array

Function

Number

Object

RegExp

String

Style

Beautiful Features

Awful Parts Global Variables

Scope

Semicolon Insertion

Reserved Words

Unicode

typeof

parseInt

+

Floating Point

NaN

Phony Arrays

Falsy Values

hasOwnProperty

Object

Bad Parts ==

with Statement

eval

continue Statement

switch Fall Through

Block-less Statements

++ --

Bitwise Operators

The function Statement Versus the function Expression

Typed Wrappers

new

void

JSLint Undefined Variables and Functions

Members

Options

Semicolon

Line Breaking

Comma

Required Blocks

Forbidden Blocks

Expression Statements

for in Statement

switch Statement

var Statement

with Statement

=

== and !=

Labels

Unreachable Code

Confusing Pluses and Minuses

++ and --

Bitwise Operators

eval Is Evil

void

Regular Expressions

Constructors and new

Not Looked For

HTML

JSON

Report

Syntax Diagrams

JSON JSON Syntax

Using JSON Securely

A JSON Parser

Index


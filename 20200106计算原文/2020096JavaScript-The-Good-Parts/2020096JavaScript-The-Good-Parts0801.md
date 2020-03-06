Prince of Denmark

JavaScript includes a small set of standard methods that are available on the standard types.

Array

array.concat( item…)

The concat method produces a new array containing a shallow copy of this array with the item s appended to it. If an item is an array, then each of its elements is appended individually. Also see array.push( item...) later in this chapter.

var a = ['a', 'b', 'c'];

var b = ['x', 'y', 'z'];

var c = a.concat(b, true);

// c is ['a', 'b', 'c', 'x', 'y', 'z', true]

array.join( separator) The join method makes a string from an array. It does this by making a string of each of the array’s elements, and then concatenating them all together with a separator between them. The default separator is ','. To join without separation, use an empty string as the separator.

If you are assembling a string from a large number of pieces, it is usually faster to put the pieces into an array and join them than it is to concatenate the pieces with the + operator: var a = ['a', 'b', 'c'];

a.push('d');

var c = a.join(''); // c is 'abcd';

78

array.pop( )

The pop and push methods make an array work like a stack. The pop method removes and returns the last element in this array. If the array is empty, it returns undefined.

var a = ['a', 'b', 'c'];

var c = a.pop( ); // a is ['a', 'b'] & c is 'c'

pop can be implemented like this:

Array.method('pop', function ( ) {

return this.splice(this.length - 1, 1)[0];

});

array.push( item…)

The push method appends items to the end of an array. Unlike the concat method, it modifies the array and appends array items whole. It returns the new length of the array: var a = ['a', 'b', 'c'];

var b = ['x', 'y', 'z'];

var c = a.push(b, true);

// a is ['a', 'b', 'c', ['x', 'y', 'z'], true]

// c is 5;

push can be implemented like this:

Array.method('push', function ( ) {

this.splice.apply(

this,

[this.length, 0].

concat(Array.prototype.slice.apply(arguments)));

return this.length;

});

array.reverse( )

The reverse method modifies the array by reversing the order of the elements. It returns the array:

var a = ['a', 'b', 'c'];

var b = a.reverse( );

// both a and b are ['c', 'b', 'a']

array.shift( )

The shift method removes the first element from an array and returns it. If the array is empty, it returns undefined. shift is usually much slower than pop: var a = ['a', 'b', 'c'];

var c = a.shift( ); // a is ['b', 'c'] & c is 'a'

shift can be implemented like this:

Array.method('shift', function ( ) {

return this.splice(0, 1)[0];

});

Array

|

79

array.slice( start, end) The slice method makes a shallow copy of a portion of an array. The first element copied will be array[ start]. It will stop before copying array[ end]. The end parameter is optional, and the default is array.length. If either parameter is negative, array.length will be added to them in an attempt to make them nonnegative. If start is greater than or equal to array.

length, the result will be a new empty array. Do not confuse slice with splice. Also see string.slice later in this chapter.

var a = ['a', 'b', 'c'];

var b = a.slice(0, 1); // b is ['a']

var c = a.slice(1); // c is ['b', 'c']

var d = a.slice(1, 2); // d is ['b']

array.sort( comparefn) The sort method sorts the contents of an array in place. It sorts arrays of numbers incorrectly:

var n = [4, 8, 15, 16, 23, 42];

n.sort( );

// n is [15, 16, 23, 4, 42, 8]

JavaScript’s default comparison function assumes that the elements to be sorted are strings.

It isn’t clever enough to test the type of the elements before comparing them, so it converts the numbers to strings as it compares them, ensuring a shockingly incorrect result.

Fortunately, you may replace the comparison function with your own. Your comparison function should take two parameters and return 0 if the two parameters are equal, a negative number if the first parameter should come first, and a positive number if the second parameter should come first. (Old-timers might be reminded of the FORTRAN II arithmetic IF statement.)

n.sort(function (a, b) {

return a - b;

});

// n is [4, 8, 15, 16, 23, 42];

That function will sort numbers, but it doesn’t sort strings. If we want to be able to sort any array of simple values, we must work harder:

var m = ['aa', 'bb', 'a', 4, 8, 15, 16, 23, 42];

m.sort(function (a, b) {

if (a === b) {

return 0;

}

if (typeof a === typeof b) {

return a < b ? -1 : 1;

}

return typeof a < typeof b ? -1 : 1;

});

// m is [4, 8, 15, 16, 23, 42, 'a', 'aa', 'bb']

If case is not significant, your comparison function should convert the operands to lowercase before comparing them. Also see string.localeCompare later in this chapter.

With a smarter comparison function, we can sort an array of objects. To make things easier for the general case, we will write a function that will make comparison functions: 80

|

Chapter 8: Methods

// Function by takes a member name string and returns

// a comparison function that can be used to sort an

// array of objects that contain that member.

var by = function (name) {

return function (o, p) {

var a, b;

if (typeof o === 'object' && typeof p === 'object' && o && p) {

a = o[name];

b = p[name];

if (a === b) {

return 0;

}

if (typeof a === typeof b) {

return a < b ? -1 : 1;

}

return typeof a < typeof b ? -1 : 1;

} else {

throw {

name: 'Error',

message: 'Expected an object when sorting by ' + name;

};

}

};

};

var s = [

{first: 'Joe', last: 'Besser'},

{first: 'Moe', last: 'Howard'},

{first: 'Joe', last: 'DeRita'},

{first: 'Shemp', last: 'Howard'},

{first: 'Larry', last: 'Fine'},

{first: 'Curly', last: 'Howard'}

];

s.sort(by('first')); // s is [

// {first: 'Curly', last: 'Howard'},

// {first: 'Joe', last: 'DeRita'},

// {first: 'Joe', last: 'Besser'},

// {first: 'Larry', last: 'Fine'},

// {first: 'Moe', last: 'Howard'},

// {first: 'Shemp', last: 'Howard'}

// ]

The sort method is not stable, so:

s.sort(by('first')).sort(by('last'));

is not guaranteed to produce the correct sequence. If you want to sort on multiple keys, youagain need to do more work. We can modify by to take a second parameter, another compare method that will be called to break ties when the major key produces a match:

// Function by takes a member name string and an

// optional minor comparison function and returns

// a comparison function that can be used to sort an

// array of objects that contain that member. The

// minor comparison function is used to break ties

Array

|

81

// when the o[name] and p[name] are equal.

var by = function (name, minor) {

return function (o, p) {

var a, b;

if (o && p && typeof o === 'object' && typeof p === 'object') {

a = o[name];

b = p[name];

if (a === b) {

return typeof minor === 'function' ? minor(o, p) : 0;

}

if (typeof a === typeof b) {

return a < b ? -1 : 1;

}

return typeof a < typeof b ? -1 : 1;

} else {

throw {

name: 'Error',

message: 'Expected an object when sorting by ' + name;

};

}

};

};

s.sort(by('last', by('first'))); // s is [

// {first: 'Joe', last: 'Besser'},

// {first: 'Joe', last: 'DeRita'},

// {first: 'Larry', last: 'Fine'},

// {first: 'Curly', last: 'Howard'},

// {first: 'Moe', last: 'Howard'},

// {first: 'Shemp', last: 'Howard'}

// ]

array.splice( start, deleteCount, item…) The splice method removes elements from an array, replacing them with new item s. The start parameter is the number of a position within the array. The deleteCount parameter is the number of elements to delete starting from that position. If there are additional parameters, those item s will be inserted at the position. It returns an array containing the deleted elements.

The most popular use of splice is to delete elements from an array. Do not confuse splice with slice:

var a = ['a', 'b', 'c'];

var r = a.splice(1, 1, 'ache', 'bug');

// a is ['a', 'ache', 'bug', 'c']

// r is ['b']

splice can be implemented like this:

Array.method('splice', function (start, deleteCount) {

var max = Math.max,

min = Math.min,

delta,

element,

82

|

Chapter 8: Methods

insertCount = max(arguments.length - 2, 0), k = 0,

len = this.length,

new_len,

result = [],

shift_count;

start = start || 0;

if (start < 0) {

start += len;

}

start = max(min(start, len), 0);

deleteCount = max(min(typeof deleteCount === 'number' ?

deleteCount : len, len - start), 0);

delta = insertCount - deleteCount;

new_len = len + delta;

while (k < deleteCount) {

element = this[start + k];

if (element !== undefined) {

result[k] = element;

}

k += 1;

}

shift_count = len - start - deleteCount;

if (delta < 0) {

k = start + insertCount;

while (shift_count) {

this[k] = this[k - delta];

k += 1;

shift_count -= 1;

}

this.length = new_len;

} else if (delta > 0) {

k = 1;

while (shift_count) {

this[new_len - k] = this[len - k];

k += 1;

shift_count -= 1;

}

}

for (k = 0; k < insertCount; k += 1) {

this[start + k] = arguments[k + 2];

}

return result;

});

array.unshift( item…)

The unshift method is like the push method except that it shoves the item s onto the front of this array instead of at the end. It returns the array’s new length: var a = ['a', 'b', 'c'];

var r = a.unshift('?', '@');

// a is ['?', '@', 'a', 'b', 'c']

// r is 5

Array

|

83

unshift can be implemented like this: Array.method('unshift', function ( ) {

this.splice.apply(this,

[0, 0].concat(Array.prototype.slice.apply(arguments))); return this.length;

});

Function

function.apply( thisArg, argArray) The apply method invokes a function, passing in the object that will be bound to this and an optional array of arguments. The apply method is used in the apply invocation pattern

(Chapter 4):

Function.method('bind', function (that) {

// Return a function that will call this function as

// though it is a method of that object.

var method = this,

slice = Array.prototype.slice,

args = slice.apply(arguments, [1]);

return function ( ) {

return method.apply(that,

args.concat(slice.apply(arguments, [0])));

};

});

var x = function ( ) {

return this.value;

}.bind({value: 666});

alert(x( )); // 666

Number

number.toExponential( fractionDigits) The toExponential method converts this number to a string in the exponential form. The optional fractionDigits parameter controls the number of decimal places. It should be between 0 and 20:

document.writeln(Math.PI.toExponential(0));

document.writeln(Math.PI.toExponential(2));

document.writeln(Math.PI.toExponential(7));

document.writeln(Math.PI.toExponential(16));

document.writeln(Math.PI.toExponential( ));

// Produces

84

|

Chapter 8: Methods

3e+0

3.14e+0

3.1415927e+0

3.1415926535897930e+0

3.141592653589793e+0

number.toFixed( fractionDigits) The toFixed method converts this number to a string in the decimal form. The optional fractionDigits parameter controls the number of decimal places. It should be between 0

and 20. The default is 0:

document.writeln(Math.PI.toFixed(0));

document.writeln(Math.PI.toFixed(2));

document.writeln(Math.PI.toFixed(7));

document.writeln(Math.PI.toFixed(16));

document.writeln(Math.PI.toFixed( ));

// Produces

3

3.14

3.1415927

3.1415926535897930

3

number.toPrecision( precision) The toPrecision method converts this number to a string in the decimal form. The optional precision parameter controls the number of digits of precision. It should be between 1 and 21:

document.writeln(Math.PI.toPrecision(2));

document.writeln(Math.PI.toPrecision(7));

document.writeln(Math.PI.toPrecision(16));

document.writeln(Math.PI.toPrecision( ));

// Produces

3.1

3.141593

3.141592653589793

3.141592653589793

number.toString( radix) The toString method converts this number to a string. The optional radix parameter controls radix, or base. It should be between 2 and 36. The default radix is base 10. The radix parameter is most commonly used with integers, but it can be used on any number.

The most common case, number.toString( ), can be written more simply as String( number): document.writeln(Math.PI.toString(2));

document.writeln(Math.PI.toString(8));

document.writeln(Math.PI.toString(16));

document.writeln(Math.PI.toString( ));

Number

|

85

// Produces

11.001001000011111101101010100010001000010110100011

3.1103755242102643

3.243f6a8885a3

3.141592653589793

Object

object.hasOwnProperty( name) The hasOwnProperty method returns true if the object contains a property having the name.

The prototype chain is not examined. This method is useless if the name is hasOwnProperty: var a = {member: true};

var b = Object.create(a); // from Chapter 3

var t = a.hasOwnProperty('member'); // t is true

var u = b.hasOwnProperty('member'); // u is false

var v = b.member; // v is true

RegExp

regexp.exec( string)

The exec method is the most powerful (and slowest) of the methods that use regular expressions. If it successfully matches the regexp and the string, it returns an array. The 0

element of the array will contain the substring that matched the regexp. The 1 element is the text captured by group 1, the 2 element is the text captured by group 2, and so on. If the match fails, it returns null.

If the regexp has a g flag, things are a little more complicated. The searching begins not at position 0 of the string, but at position regexp.lastIndex (which is initially zero). If the match is successful, then regexp.lastIndex will be set to the position of the first character after the match. An unsuccessful match resets regexp.lastIndex to 0.

This allows youto search for several occurrences of a pattern in a string by calling exec in a loop. There are a couple things to watch out for. If you exit the loop early, you must reset regexp.lastIndex to 0 yourself before entering the loop again. Also, the ^ factor matches only when regexp.lastIndex is 0:

// Break a simple html text into tags and texts.

// (See string.replace for the entityify method.)

// For each tag or text, produce an array containing

// [0] The full matched tag or text

// [1] The tag name

// [2] The /, if there is one

// [3] The attributes, if any

var text = '<html><body bgcolor=linen><p>' +

'This is <b>bold<\/b>!<\/p><\/body><\/html>'; 86

|

Chapter 8: Methods

var tags = /[^<>]+|<(\/?)([A-Za-z]+)([^<>]*)>/g; var a, i;

while ((a = tags.exec(text))) {

for (i = 0; i < a.length; i += 1) {

document.writeln(('// [' + i + '] ' + a[i]).entityify( ));

}

document.writeln( );

}

// Result:

// [0] <html>

// [1]

// [2] html

// [3]

// [0] <body bgcolor=linen>

// [1]

// [2] body

// [3] bgcolor=linen

// [0] <p>

// [1]

// [2] p

// [3]

// [0] This is

// [1] undefined

// [2] undefined

// [3] undefined

// [0] <b>

// [1]

// [2] b

// [3]

// [0] bold

// [1] undefined

// [2] undefined

// [3] undefined

// [0] </b>

// [1] /

// [2] b

// [3]

// [0] !

// [1] undefined

// [2] undefined

// [3] undefined

// [0] </p>

// [1] /

RegExp

|

87

// [2] p

// [3]

regexp.test( string)

The test method is the simplest (and fastest) of the methods that use regular expressions.

If the regexp matches the string, it returns true; otherwise, it returns false. Do not use the g flag with this method:

var b = /&.+;/.test('frank &amp; beans');

// b is true

test could be implemented as:

RegExp.method('test', function (string) {

return this.exec(string) !== null;

});

String

string.charAt( pos)

The charAt method returns the character at position pos in this string. If pos is less than zero or greater than or equal to string.length, it returns the empty string. JavaScript does not have a character type. The result of this method is a string: var name = 'Curly';

var initial = name.charAt(0); // initial is 'C'

charAt could be implemented as:

String.method('charAt', function (pos) {

return this.slice(pos, pos + 1);

});

string.charCodeAt( pos) The charCodeAt method is the same as charAt except that instead of returning a string, it returns an integer representation of the code point value of the character at position pos in that string. If pos is less than zero or greater than or equal to string.length, it returns NaN: var name = 'Curly';

var initial = name.charCodeAt(0); // initial is 67

string.concat( string…) The concat method makes a new string by concatenating other strings together. It is rarely used because the + operator is more convenient:

var s = 'C'.concat('a', 't'); // s is 'Cat'

string.indexOf( searchString, position) The indexOf method searches for a searchString within a string. If it is found, it returns the position of the first matched character; otherwise, it returns –1. The optional position parameter causes the search to begin at some specified position in the string: 88

|

Chapter 8: Methods

var text = 'Mississippi';

var p = text.indexOf('ss'); // p is 2

p = text.indexOf('ss', 3); // p is 5

p = text.indexOf('ss', 6); // p is -1

string.lastIndexOf( searchString, position) The lastIndexOf method is like the indexOf method, except that it searches from the end of the string instead of the front:

var text = 'Mississippi';

var p = text.lastIndexOf('ss'); // p is 5

p = text.lastIndexOf('ss', 3); // p is 2

p = text.lastIndexOf('ss', 6); // p is 5

string.localeCompare( that) The localCompare method compares two strings. The rules for how the strings are compared are not specified. If this string is less than that string, the result is negative. If they are equal, the result is zero. This is similar to the convention for the array.sort comparison function:

var m = ['AAA', 'A', 'aa', 'a', 'Aa', 'aaa'];

m.sort(function (a, b) {

return a.localeCompare(b);

});

// m (in some locale) is

// ['a', 'A', 'aa', 'Aa', 'aaa', 'AAA']

string.match( regexp)

The match method matches a string and a regular expression. How it does this depends on the g flag. If there is no g flag, then the result of calling string.match( regexp) is the same as calling regexp.exec( string). However, if the regexp has the g flag, then it produces an array of all the matches but excludes the capturing groups:

var text = '<html><body bgcolor=linen><p>' +

'This is <b>bold<\/b>!<\/p><\/body><\/html>'; var tags = /[^<>]+|<(\/?)([A-Za-z]+)([^<>]*)>/g; var a, i;

a = text.match(tags);

for (i = 0; i < a.length; i += 1) {

document.writeln(('// [' + i + '] ' + a[i]).entityify( ));

}

// The result is

// [0] <html>

// [1] <body bgcolor=linen>

// [2] <p>

// [3] This is

// [4] <b>

// [5] bold

// [6] </b>

// [7] !

String

|

89

// [8] </p>

// [9] </body>

// [10] </html>

string.replace( searchValue, replaceValue) The replace method does a search and replace operation on this string, producing a new string. The searchValue argument can be a string or a regular expression object. If it is a string, only the first occurrence of the searchValue is replaced, so: var result = "mother_in_law".replace('_', '-'); will produce "mother-in_law", which might be a disappointment.

If searchValue is a regular expression and if it has the g flag, then it will replace all occurrences. If it does not have the g flag, then it will replace only the first occurrence.

The replaceValue can be a string or a function. If replaceValue is a string, the character $

has special meaning:

// Capture 3 digits within parens

var oldareacode = /\((\d{3})\)/g;

var p = '(555)666-1212'.replace(oldareacode, '$1-');

// p is '555-555-1212'

Dollar sequence

Replacement

$$

$

$&

The matched text

$ number

Capture group text

$`

The text preceding the match

$'

The text following the match

If the replaceValue is a function, it will be called for each match, and the string returned by the function will be used as the replacement text. The first parameter passed to the function is the matched text. The second parameter is the text of capture group 1, the next parameter is the text of capture group 2, and so on:

String.method('entityify', function ( ) {

var character = {

'<' : '&lt;',

'>' : '&gt;',

'&' : '&amp;',

'"' : '&quot;'

};

// Return the string.entityify method, which

// returns the result of calling the replace method.

// Its replaceValue function returns the result of

// looking a character up in an object. This use of

// an object usually outperforms switch statements.

90

|

Chapter 8: Methods

return function ( ) {

return this.replace(/[<>&"]/g, function (c) {

return character[c];

});

};

}( ));

alert("<&>".entityify( )); // &lt;&amp;&gt;

string.search( regexp) The search method is like the indexOf method, except that it takes a regular expression object instead of a string. It returns the position of the first character of the first match, if there is one, or –1 if the search fails. The g flag is ignored. There is no position parameter: var text = 'and in it he says "Any damn fool could'; var pos = text.search(/["']/); // pos is 18

string.slice( start, end) The slice method makes a new string by copying a portion of another string. If the start parameter is negative, it adds string.length to it. The end parameter is optional, and its default value is string.length. If the end parameter is negative, then string.length is added to it. The end parameter is one greater than the position of the last character. To get n characters starting at position p, u se string.slice(p,p + n). Also see string.substring and array.slice, later and earlier in this chapter, respectively.

var text = 'and in it he says "Any damn fool could'; var a = text.slice(18);

// a is '"Any damn fool could'

var b = text.slice(0, 3);

// b is 'and'

var c = text.slice(-5);

// c is 'could'

var d = text.slice(19, 32);

// d is 'Any damn fool'

string.split( separator, limit) The split method creates an array of strings by splitting this string into pieces. The optional limit parameter can limit the number of pieces that will be split. The separator parameter can be a string or a regular expression.

If the separator is the empty string, an array of single characters is produced: var digits = '0123456789';

var a = digits.split('', 5);

// a is ['0', '1', '2', '3', '456789']

Otherwise, the string is searched for all occurrences of the separator. Each unit of text between the separators is copied into the array. The g flag is ignored: var ip = '192.168.1.0';

var b = ip.split('.');

// b is ['192', '168', '1', '0']

var c = '|a|b|c|'.split('|');

// c is ['', 'a', 'b', 'c', '']

String

|

91

var text = 'last, first ,middle';

var d = text.split(/\s*,\s*/);

// d is [

// 'last',

// 'first',

// 'middle'

// ]

There are some special cases to watch out for. Text from capturing groups will be included in the split:

var e = text.split(/\s*(,)\s*/);

// e is [

// 'last',

// ',',

// 'first',

// ',',

// 'middle'

// ]

Some implementations suppress empty strings in the output array when the separator is a regular expression:

var f = '|a|b|c|'.split(/\|/);

// f is ['a', 'b', 'c'] on some systems, and

// f is ['', 'a', 'b', 'c', ''] on others

string.substring( start, end) The substring method is the same as the slice method except that it doesn’t handle the adjustment for negative parameters. There is no reason to use the substring method. Use slice instead.

string.toLocaleLowerCase( )

The toLocaleLowerCase method produces a new string that is made by converting this string to lowercase using the rules for the locale. This is primarily for the benefit of Turkish because in that language ‘I’ converts to ı, not ‘i’.

string.toLocaleUpperCase( )

The toLocaleUpperCase method produces a new string that is made by converting this string to uppercase using the rules for the locale. This is primarily for the benefit of Turkish, because in that language ‘i’ converts to ‘ ’, not ‘I’.

string.toLowerCase( )

The toLowerCase method produces a new string that is made by converting this string to lowercase.

92

|

Chapter 8: Methods

string.toUpperCase( ) The toUpperCase method produces a new string that is made by converting this string to uppercase.

String.fromCharCode( char…)

The String.fromCharCode function produces a string from a series of numbers.

var a = String.fromCharCode(67, 97, 116);

// a is 'Cat'

String

|

93

Chapter 9

CHAPTER 9

Style

9


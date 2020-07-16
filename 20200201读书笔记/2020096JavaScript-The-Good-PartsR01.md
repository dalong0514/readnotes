# 2020096JavaScript-The-Good-PartsR01

## 记忆时间

2020-04-21

## 0201. Grammar

### 1. 逻辑脉络

JS 的语法内容，包括空白符、命令规则、各基本类型、语句、表达式、字面量和函数。

### 2. 摘录及评论

This chapter introduces the grammar of the good parts of JavaScript, presenting a quick overview of how the language is structured. We will represent the grammar with railroad diagrams. The rules for interpreting these diagrams are simple: 1) You start on the left edge and follow the tracks to the right edge. 2) As you go, you will encounter literals in ovals, and rules or descriptions in rectangles.『图里面圆形的是 literals，矩形的是 rules or descriptions. 』3) Any sequence that can be made by following the tracks is legal. 4) Any sequence that cannot be made by following the tracks is not legal. 5) Railroad diagrams with one bar at each end allow whitespace to be inserted between any pair of tokens. Railroad diagrams with two bars at each end do not.

The grammar of the good parts presented in this chapter is significantly simpler than the grammar of the whole language.

### 2.1 Whitespace

Whitespace can take the form of formatting characters or comments. Whitespace is usually insignificant, but it is occasionally necessary to use whitespace to separate sequences of characters that would otherwise be combined into a single token. For example, in:

    var that = this;

the space between var and that cannot be removed, but the other spaces can be removed.

JavaScript offers two forms of comments. Obsolete comments are worse than no comments. The /* */ form of block comments came from a language called PL/I. PL/I chose those strange pairs as the symbols for comments because they were unlikely to occur in that language’s programs, except perhaps in string literals. In JavaScript, those pairs can also occur in regular expression literals, so block comments are not safe for commenting out blocks of code. For example:

```js
/*
var rm_a = /a*/.match(s);
*/
```

causes a syntax error. So, it is recommended that /* */ comments be avoided and // comments be used instead. In this book, // will be used exclusively.

### 2.2 Names

A name is a letter optionally followed by one or more letters, digits, or underbars. A name cannot be one of these reserved words:

```js
abstract 
boolean break byte 
case catch char class const continue 
debugger default delete do double
else enum export extends 
false final finally float for function 
goto 
if implements import in instanceof int interface
long 
native new null 
package private protected public 
return 
short static super switch synchronized 
this throw throws transient true try typeof 
var volatile void
while with
```

Most of the reserved words in this list are not used in the language. The list does not include some words that should have been reserved but were not, such as undefined, NaN, and Infinity. It is not permitted to name a variable or parameter with a reserved word. Worse, it is not permitted to use a reserved word as the name of an object property in an object literal or following a dot in a refinement. Names are used for statements, variables, parameters, property names, operators, and labels.

### 2.3 Numbers

JavaScript has a single number type. Internally, it is represented as 64-bit floating point, the same as Java’s double. Unlike most other programming languages, there is no separate integer type, so 1 and 1.0 are the same value. This is a significant convenience because problems of overflow in short integers are completely avoided, and all you need to know about a number is that it is a number. A large class of numeric type errors is avoided.

If a number literal has an exponent part, then the value of the literal is computed by multiplying the part before the e by 10 raised to the power of the part after the e. So 100 and 1e2 are the same number. Negative numbers can be formed by using the – prefix operator. The value NaN is a number value that is the result of an operation that cannot produce a normal result. NaN is not equal to any value, including itself. You can detect NaN with the isNaN (number) function. The value Infinity represents all values greater than 1.79769313486231570e+308. Numbers have methods (see Chapter 8). JavaScript has a Math object that contains a set of methods that act on numbers. For example, the Math.floor (number) method can be used to convert a number into an integer.

1『 JS 里的对象 Math 包含一系列对数字处理的方法。』

### 2.4 Strings

A string literal can be wrapped in single quotes or double quotes. It can contain zero or more characters. The \ (backslash) is the escape character. JavaScript was built at a time when Unicode was a 16-bit character set, so all characters in JavaScript are 16 bits wide. JavaScript does not have a character type. To represent a character, make a string with just one character in it.

The escape sequences allow for inserting characters into strings that are not normally permitted, such as backslashes, quotes, and control characters. The \u convention allows for specifying character code points numerically.

    "A" === "\u0041"

Strings have a length property. For example, "seven".length is 5. Strings are immutable. Once it is made, a string can never be changed. But it is easy to make a new string by concatenating other strings together with the + operator. Two strings containing exactly the same characters in the same order are considered to be the same string. So:

    'c' + 'a' + 't' === 'cat'

is true. Strings have methods (see Chapter 8):

    'cat'.toUpperCase( ) === 'CAT'

### 2.5 Statements

A compilation unit contains a set of executable statements. In web browsers, each \<script> tag delivers a compilation unit that is compiled and immediately executed. Lacking a linker, JavaScript throws them all together in a common global namespace. There is more on global variables in Appendix A.

1『链接器（Linker）是编程语言或操作系统提供的工具，它的工作就是解析未定义的符号引用，将目标文件中的占位符替换为符号地址。』

When used inside of a function, the var statement defines the function’s private variables. The switch, while, for, and do statements are allowed to have an optional label prefix that interacts with the break statement.

1『原来在函数内部用 var 申明的变量是函数的私有变量；label prefix 是指这种形式「label: expressions statement;」』

Statements tend to be executed in order from top to bottom. The sequence of execution can be altered by the conditional statements (if and switch), by the looping statements (while, for, and do), by the disruptive statements (break, return, and throw), and by function invocation.

A block is a set of statements wrapped in curly braces. Unlike many other languages, blocks in JavaScript do not create a new scope, so variables should be defined at the top of the function, not in blocks.

The if statement changes the flow of the program based on the value of the expression. The then block is executed if the expression is truthy; otherwise, the optional else branch is taken. Here are the falsy values: 1) false. 2) null. 3) undefined. 4) The empty string ''. 5) The number 0. 6) The number NaN.

All other values are truthy, including true, the string 'false', and all objects. The switch statement performs a multiway branch. It compares the expression for equality with all of the specified cases. The expression can produce a number or a string. When an exact match is found, the statements of the matching case clause are executed. If there is no match, the optional default statements are executed.

A case clause contains one or more case expressions. The case expressions need not be constants. The statement following a clause should be a disruptive statement to prevent fall through into the next case. The break statement can be used to exit from a switch.

The while statement performs a simple loop. If the expression is falsy, then the loop will break. While the expression is truthy, the block will be executed.

The for statement is a more complicated looping statement. It comes in two forms.

The conventional form is controlled by three optional clauses: the initialization, the condition, and the increment. First, the initialization is done, which typically initializes the loop variable. Then, the condition is evaluated. Typically, this tests the loop variable against a completion criterion. If the condition is omitted, then a condition of true is assumed. If the condition is falsy, the loop breaks. Otherwise, the block is executed, then the increment executes, and then the loop repeats with the condition.

The other form (called for in) enumerates the property names (or keys) of an object. On each iteration, another property name string from the object is assigned to the variable. It is usually necessary to test object.hasOwnProperty(variable) to determine whether the property name is truly a member of the object or was found instead on the prototype chain.

『可以通过这个方法来检测这个属性名是该对象的成员，还是来自于原型链。』

```js
for (myvar in obj) {
    if (obj.hasOwnProperty(myvar)) {
    ...
    }
}
```

The do statement is like the while statement except that the expression is tested after the block is executed instead of before. That means that the block will always be executed at least once.

The try statement executes a block and catches any exceptions that were thrown by the block. The catch clause defines a new variable that will receive the exception object.

The throw statement raises an exception. If the throw statement is in a try block, then control goes to the catch clause. Otherwise, the function invocation is abandoned, and control goes to the catch clause of the try in the calling function. The expression is usually an object literal containing a name property and a message property. The catcher of the exception can use that information to determine what to do.

Throw 语句抛出一个异常。如果 throw 语句在一个 try 代码块中，那么控制流会跳转到 catch 从句中。如果 throw 语句在函数中，则该函数调用被放弃，控制流跳转到调用该函数的 try 语句的 catch 从句中。throw 语句中的表达式通常是一个对象字面量，它包含一个 name 属性和一个 message 属性。异常捕获器可以使用这些信息去决定该做什么。

The return statement causes the early return from a function. It can also specify the value to be returned. If a return expression is not specified, then the return value will be undefined. JavaScript does not allow a line end between the return and the expression.

The break statement causes the exit from a loop statement or a switch statement. It can optionally have a label that will cause an exit from the labeled statement. JavaScript does not allow a line end between the break and the label.

An expression statement can either assign values to one or more variables or members, invoke a method, delete a property from an object. The = operator is used for assignment. Do not confuse it with the === equality operator. The += operator can add or concatenate.

### 2.6 Expressions

The simplest expressions are a literal value (such as a string or number), a variable, a built-in value (true, false, null, undefined, NaN, or Infinity), an invocation expression preceded by new, a refinement expression preceded by delete, an expression wrapped in parentheses, an expression preceded by a prefix operator, or an expression followed by: 1) An infix operator and another expression. 2) The ? ternary operator followed by another expression, then by :, and then by yet another expression. 3) An invocation. 4) A refinement.

The ? ternary operator takes three operands. If the first operand is truthy, it produces the value of the second operand. But if the first operand is falsy, it produces the value of the third operand.

The operators at the top of the operator precedence list in Table 2-1 have higher precedence. They bind the tightest. The operators at the bottom have the lowest precedence. Parentheses can be used to alter the normal precedence, so: 

```js
2 + 3 * 5 === 17
(2 + 3) * 5 === 25
```

The values produced by typeof are 'number', 'string', 'boolean', 'undefined', 'function', and 'object'. If the operand is an array or null, then the result is 'object', which is wrong. There will be more about typeof in Chapter 6 and Appendix A.

If the operand of ! is truthy, it produces false. Otherwise, it produces true. The + operator adds or concatenates. If you want it to add, make sure both operands are numbers. The / operator can produce a noninteger result even if both operands are integers. The && operator produces the value of its first operand if the first operand is falsy. Otherwise, it produces the value of the second operand.

1『在编程语言中，结合性（associativity）是操作符在没有圆括号分组的情况下决定其优先的一种属性。它可能是从左向右结合（left-associative）、从右向左结合（right-associative）或无结合。比如加运算符的结合性是从左向右，而一元运算符、赋値运算将及三元条件运算特的结合性是从右向左。关于更多的运算符结合性的信息，请参阅《Javascript 权成指南》中译第 5 版。在 Javascript 语言里 % 不是通常数学意义上的模运算，而实际上是「求余」运算。两个运算数为正数时，求模运算和求余运算的值相同；两个运算数中存在负数时，求模运算和求余运算的值则不相同。』

The || operator produces the value of its first operand if the first operand is truthy. Otherwise, it produces the value of the second operand.

Invocation causes the execution of a function value. The invocation operator is a pair of parentheses that follow the function value. The parentheses can contain arguments that will be delivered to the function. There will be much more about functions in Chapter 4.

1『 Invocation 指函数调用。』

A refinement is used to specify a property or element of an object or array. This will be described in detail in the next chapter.

### 2.7 Literals

Object literals are a convenient notation for specifying new objects. The names of the properties can be specified as names or as strings. The names are treated as literal names, not as variable names, so the names of the properties of the object must be known at compile time. The values of the properties are expressions. There will be more about object literals in the next chapter. Array literals are a convenient notation for specifying new arrays. There will be more about array literals in Chapter 6. There will be more about regular expressions in Chapter 7.

『 Literals 即字面量。对象字面量是一种可以方便地按指定规格创建新对象的表示法。属性名可以是标识符或字符串。这些名字被当做字面量名而不是变量名来对待，所以对象的属性名在编译时才能知道。属性的值就是表达式。』

### 2.8 Functions

A function literal defines a function value. It can have an optional name that it can use to call itself recursively. It can specify a list of parameters that will act as variables initialized by the invocation arguments. The body of the function includes variable definitions and statements. There will be more about functions in Chapter 4.

## 0301. Objects

### 1. 逻辑脉络

对象是一系列「属性」的集合，属性有属性名和属性值，属性名可以是字符串、空值和 symbol 类型，属性值可以是除 undefined 外的任何东西；对象是可变的，可以动态的添加属性；对象的传递是通过引用而非复制，比如「var x = stooge; 」是把 stooge 对象的引用复制给 x 变量，或者说 stooge 和 x 指向同一个对象，或者说将变量 x 绑定到 stooge 指向的对象上；所有的对象都是链接到其原型对象上的，创建的时候是从其原型对象上继承了所有属性。所有通过字面量创建的对象其原型对象都是「Object.prototype」。

### 2. 摘录及评论

The simple types of JavaScript are numbers, strings, booleans (true and false), null, and undefined. All other values are objects. Numbers, strings, and booleans are object-like in that they have methods, but they are immutable. Objects in JavaScript are mutable keyed collections. In JavaScript, arrays are objects, functions are objects, regular expressions are objects, and, of course, objects are objects.

An object is a container of properties, where a property has a name and a value. A property name can be any string, including the empty string. A property value can be any JavaScript value except for undefined.

Objects in JavaScript are class-free. There is no constraint on the names of new properties or on the values of properties. Objects are useful for collecting and organizing data. Objects can contain other objects, so they can easily represent tree or graph structures. JavaScript includes a prototype linkage feature that allows one object to inherit the properties of another. When used well, this can reduce object initialization time and memory consumption.

1『 JS 中的对象是无类型的（class-free）。』

### 3.1 Object Literals

Object literals provide a very convenient notation for creating new object values. An object literal is a pair of curly braces surrounding zero or more name/value pairs. An object literal can appear anywhere an expression can appear: 

1『字面量只是下面等号右边的部分，它是一个 notation，可以方便的创建对象、数组等。对字面量的理解又加深了一步。（2020-03-29）』

```js
var empty_object = {};

var stooge = {
    "first-name": "Jerome",
    "last-name": "Howard"
};
```

A property’s name can be any string, including the empty string. The quotes around a property’s name in an object literal are optional if the name would be a legal JavaScript name and not a reserved word. So quotes are required around "first-name", but are optional around first-name. Commas are used to separate the pairs. A property’s value can be obtained from any expression, including another object literal. Objects can nest:

```js
var flight = {
    airline: "Oceanic",
    number: 815,
    departure: {
        IATA: "SYD",
        time: "2004-09-22 14:55",
        city: "Sydney"
    },
    arrival: {
        IATA: "LAX",
        time: "2004-09-23 10:42",
        city: "Los Angeles"
    }
};
```

### 3.2 Retrieval

Values can be retrieved from an object by wrapping a string expression in a [ ] suffix. If the string expression is a constant, and if it is a legal JavaScript name and not a reserved word, then the . notation can be used instead. The . notation is preferred because it is more compact and it reads better:

```js
stooge["first-name"] // "Joe"
flight.departure.IATA // "SYD"
```

The undefined value is produced if an attempt is made to retrieve a nonexistent member:

```js
stooge["middle-name"] // undefined
flight.status // undefined
stooge["FIRST-NAME"] // undefined
```

The || operator can be used to fill in default values: 

```js
var middle = stooge["middle-name"] || "(none)"; 
var status = flight.status || "unknown";
```

Attempting to retrieve values from undefined will throw a TypeError exception. This can be guarded against with the && operator:

```js
flight.equipment // undefined flight.equipment.model // throw "TypeError"
flight.equipment && flight.equipment.model // undefined Retrieval
```

### 3.3 Update

A value in an object can be updated by assignment. If the property name already exists in the object, the property value is replaced:

    stooge['first-name'] = 'Jerome';

If the object does not already have that property name, the object is augmented: 

```js
stooge['middle-name'] = 'Lester';
stooge.nickname = 'Curly';
flight.equipment = {
    model: 'Boeing 777'
};
flight.status = 'overdue';
```

### 3.4 Reference

Objects are passed around by reference. They are never copied: 

```js
var x = stooge;
x.nickname = 'Curly';
var nick = stooge.nickname;
    // nick is 'Curly' because x and stooge are references to the same object

var a = {}, b = {}, c = {};
// a, b, and c each refer to a different empty object

a = b = c = {};
// a, b, and c all refer to the same empty object
```

### 3.5 Prototype

Every object is linked to a prototype object from which it can inherit properties. All objects created from object literals are linked to Object.prototype, an object that comes standard with JavaScript. When you make a new object, you can select the object that should be its prototype.

The mechanism that JavaScript provides to do this is messy and complex, but it can be significantly simplified. We will add a create method to the Object function. The create method creates a new object that uses an old object as its prototype. There will be much more about functions in the next chapter.

```js
if (typeof Object.create !== 'function') {
    Object.create = function (o) {
    var F = function () {};
    F.prototype = o;
    return new F();
};
}

var another_stooge = Object.create(stooge);
```

3『「2019013程勋非的重学前端R01.md」

有这个例子：这段代码创建了一个空函数作为类，并把传入的原型挂在了它的 prototype，最后创建了一个它的实例，根据 new 的行为，这将产生一个以传入的第一个参数为原型的对象。这个函数无法做到与原生的 Object.create 一致，一个是不支持第二个参数，另一个是不支持 null 作为原型，所以放到今天意义已经不大了。ES6 以来，JavaScript 提供了一系列内置函数，以便更为直接地访问操纵原型。三个方法分别为：1）Object.create 根据指定的原型创建新对象，原型可以是 null；2）Object.getPrototypeOf 获得一个对象的原型；3）Object.setPrototypeOf 设置一个对象的原型。利用这三个方法，我们可以完全抛开类的思维，利用原型来实现抽象和复用。ES6 中加入了新特性 class，new 跟 function 搭配的怪异行为终于可以退休了（虽然运行时没有改变），在任何场景，我都推荐使用 ES6 的语法来定义类，而令 function 回归原本的函数语义。』

1『注意，winter 只是建议在用使用基于类的面向对象时使用新语法 class 来定义类，有些场景下照样可以用基于原型的面向对象。』

The prototype link has no effect on updating. When we make changes to an object, the object’s prototype is not touched:

```js
another_stooge['first-name'] = 'Harry';
another_stooge['middle-name'] = 'Moses';
another_stooge.nickname = 'Moe';
```

The prototype link is used only in retrieval. If we try to retrieve a property value from an object, and if the object lacks the property name, then JavaScript attempts to retrieve the property value from the prototype object. And if that object is lacking the property, then it goes to its prototype, and so on until the process finally bottoms out with Object.prototype. If the desired property exists nowhere in the prototype chain, then the result is the undefined value. This is called delegation.

The prototype relationship is a dynamic relationship. If we add a new property to a prototype, that property will immediately be visible in all of the objects that are based on that prototype:

```js
stooge.profession = 'actor';
another_stooge.profession // 'actor'
```

We will see more about the prototype chain in Chapter 6.

2『

通过作者提供的方法可以阻断子对象触达父对象的原型链。做一张计算机的信息卡片。

```js
// 阻断子对象触达父对象的原型链
if (typeof Object.create !== 'function') {
    Object.create = function (o) {
        var F = function () {};
        F.prototype = o;
        return new F(); 
    };
}

var stooge = {
    "firstname": "Feng",
    "lastname": "Dalong",
};

console.log(stooge);

stooge['middlename'] = 'hahei';
stooge.nickname = 'dalong';
console.log(stooge);

var x = stooge;
x.height = '168cm';
console.log(stooge);

var y = Object.create(stooge);
y.food = 'apple';
console.log(stooge);

stooge.programming = 'JS';
console.log('x: ' + x.programming);
console.log('y: ' + y.programming);
```

』

### 3.6 Reflection

It is easy to inspect an object to determine what properties it has by attempting to retrieve the properties and examining the values obtained. The typeof operator can be very helpful in determining the type of a property: 

```js
typeof flight.number // 'number'
typeof flight.status // 'string'
typeof flight.arrival // 'object'
typeof flight.manifest // 'undefined'
```

Some care must be taken because any property on the prototype chain can produce a value:

```js
typeof flight.toString // 'function'
typeof flight.constructor // 'function'
```

There are two approaches to dealing with these undesired properties. The first is to have your program look for and reject function values. Generally, when you are reflecting, you are interested in data, and so you should be aware that some values could be functions. The other approach is to use the hasOwnProperty method, which returns true if the object has a particular property. The hasOwnProperty method does not look at the prototype chain:

```js
flight.hasOwnProperty('number') // true
flight.hasOwnProperty('constructor') // false
```

1『两种方法剔除掉原型链上原生的属性，一是自己写方法剔除，一是用 hasOwnProperty() 来过滤。』

### 3.7 Enumeration

The for in statement can loop over all of the property names in an object. The enumeration will include all of the properties—including functions and prototype properties that you might not be interested in—so it is necessary to filter out the values you don’t want. The most common filters are the hasOwnProperty method and using typeof to exclude functions:

```js
var name;
for (name in another_stooge) {
    if (typeof another_stooge[name] !== 'function') {
    document.writeln(name + ': ' + another_stooge[name]);
    }
}
```

1『上面的方法可以经常拿来用。』

There is no guarantee on the order of the names, so be prepared for the names to appear in any order. If you want to assure that the properties appear in a particular order, it is best to avoid the for in statement entirely and instead make an array containing the names of the properties in the correct order: 

```js
var i;
var properties = [
    'first-name',
    'middle-name',
    'last-name',
    'profession'
];

for (i = 0; i < properties.length; i += 1) {
    document.writeln(properties[i] + ': ' + another_stooge[properties[i]]);
}
```

By using for instead of for in, we were able to get the properties we wanted without worrying about what might be dredged up from the prototype chain, and we got them in the correct order.

1『使用 for 来遍历更佳，但前提是要有需要遍历的属性名的数组。』

### 3.8 Delete

The delete operator can be used to remove a property from an object. It will remove a property from the object if it has one. It will not touch any of the objects in the prototype linkage. Removing a property from an object may allow a property from the prototype linkage to shine through:

```js
another_stooge.nickname // 'Moe'
// Remove nickname from another_stooge, revealing the nickname of the prototype.
delete another_stooge.nickname;
another_stooge.nickname // 'Curly'
```

1『之前用 Object.create() 封装，让子对象不能触达父对象的原型链，此时删除掉子对象的这个属性后，其父对象原型链上的属性也就暴露出来了。』

### 3.9 Global Abatement

JavaScript makes it easy to define global variables that can hold all of the assets of your application. Unfortunately, global variables weaken the resiliency of programs and should be avoided. One way to minimize the use of global variables is to create a single global variable for your application:

    var MYAPP = {};

That variable then becomes the container for your application: 

```js
MYAPP.stooge = {
    "first-name": "Joe",
    "last-name": "Howard"
};

MYAPP.flight = {
    airline: "Oceanic",
    number: 815,
    departure: {
        IATA: "SYD",
        time: "2004-09-22 14:55",
        city: "Sydney"
    },
    arrival: {
        IATA: "LAX",
        time: "2004-09-23 10:42",
        city: "Los Angeles"
    }
};
```

1『就用一个全局变量，所有的东西全塞进这个全局对象里，哈哈。』

By reducing your global footprint to a single name, you significantly reduce the chance of bad interactions with other applications, widgets, or libraries. Your program also becomes easier to read because it is obvious that MYAPP.stooge refers to a top-level structure. In the next chapter, we will see ways to use closure for information hiding, which is another effective global abatement technique.

1『用闭包来 information hiding，闭包也是一种减少全局变量污染的有效手段。』

## 0401. Function

The best thing about JavaScript is its implementation of functions. It got almost everything right. But, as you should expect with JavaScript, it didn’t get everything right. A function encloses a set of statements. Functions are the fundamental modular unit of JavaScript. They are used for code reuse, information hiding, and composition. Functions are used to specify the behavior of objects. Generally, the craft of programming is the factoring of a set of requirements into a set of functions and data structures.

1『函数是 JS 的灵魂所在，函数式编程。』

### 4.1 Function Objects

Functions in JavaScript are objects. Objects are collections of name/value pairs having a hidden link to a prototype object. Objects produced from object literals are linked to Object.prototype. Function objects are linked to Function.prototype (which is itself linked to Object.prototype). Every function is also created with two additional hidden properties: the function’s context and the code that implements the function’s behavior.

1『 function’s context 是函数的上下文；函数对象在被创建时默认有 2 个隐藏属性：函数上下文和实现函数行为的 code（目前的理解即为调用属性）。函数上下文这个隐藏属性跟闭包密切相关，甚至于就是闭包。（2020-03-29）』

3『 Javascript 创建一个函数对象时，会给该对象设置一个「调用」属性。当 Javascript 调用一个函数时，可理解为调用此函数的「调用」属性。详细的描述请参阅 Ecmascript 规范的「13.2 Creating Function Objects」。』

2『去找规范里的「Creating Function Objects」看。』

Every function object is also created with a prototype property. Its value is an object with a constructor property whose value is the function. This is distinct from the hidden link to Function.prototype. The meaning of this convoluted construction will be revealed in the next chapter.

Since functions are objects, they can be used like any other value. Functions can be stored in variables, objects, and arrays. Functions can be passed as arguments to functions, and functions can be returned from functions. Also, since functions are objects, functions can have methods. The thing that is special about functions is that they can be invoked.

### 4.2 Function Literal

Function objects are created with function literals:

```js
// Create a variable called add and store a function
// in it that adds two numbers.
var add = function (a, b) {
    return a + b;
};
```

A function literal has four parts. The first part is the reserved word function. The optional second part is the function’s name. The function can use its name to call itself recursively. The name can also be used by debuggers and development tools to identify the function. If a function is not given a name, as shown in the previous example, it is said to be anonymous. 

The third part is the set of parameters of the function, wrapped in parentheses. Within the parentheses is a set of zero or more parameter names, separated by commas. These names will be defined as variables in the function. Unlike ordinary variables, instead of being initialized to undefined, they will be initialized to the arguments supplied when the function is invoked. The fourth part is a set of statements wrapped in curly braces. These statements are the body of the function. They are executed when the function is invoked.

函数的参数不像普通的变量那样将被初始化为 undefined，而是在该函数被调用时初始化为实际提供的参数的值。

A function literal can appear anywhere that an expression can appear. Functions can be defined inside of other functions. An inner function of course has access to its parameters and variables. An inner function also enjoys access to the parameters and variables of the functions it is nested within. The function object created by a function literal contains a link to that outer context. This is called closure. This is the source of enormous expressive power.

函数也可以被定义在其他函数中个内部函数，除了可以访问自己的参数和变量，同时它也能自由访问把它嵌套在其中的父函数的参数与变量。通过函数字面量创建的函数对象包含一个连到外部上下文的连接。这被称为闭包（closure）。它是 Javascript 强大表现力的来源。

1『字面量创建的函数对象包含一个连到外部上下文的连接。那么通过原型对象创建的函数对象呢？』

### 4.3 Invocation

Invoking a function suspends the execution of the current function, passing control and parameters to the new function. In addition to the declared parameters, every function receives two additional parameters: this and arguments. The this parameter is very important in object oriented programming, and its value is determined by the invocation pattern. There are four patterns of invocation in JavaScript: the method invocation pattern, the function invocation pattern, the constructor invocation pattern, and the apply invocation pattern. The patterns differ in how the bonus parameter this is initialized.

2『 this 的值取决于调用模式（invocation pattern）：1）the method invocation pattern，方法式调用，this 绑定到该方法所隶属的对象（函数作为一个对象的某个属性值的时候才被称为方法），这个绑定是在调用时发生的；2）the function invocation pattern，函数式调用，this 绑定到全局变量上（JS 公认的设计错误），这导致内部函数无法通过 this 来访问外部函数的数据，即没法帮外部函数处理一些事情了，不过可以通过「var that = this; 」来解决；3）the constructor invocation pattern，构造函数式调用。这其实是对基于类的面向对象的妥协，用「new + 构造器函数」来调用构造器函数，会创建一个连接到构造函数原型链的新对象，this 绑定到这个新对象上。new 还会改变 return 语句的行为；4）the apply invocation pattern，apply 式调用。Quo.prototype.get_status.apply(statusObject); 是指定 this 绑定到 apply() 调用时传递的参数，在这里即 statusObject，所以 get_status 函数里的 this.statu 即 statusObject 对象里的 status 属性值。做一张术语卡片。』

The invocation operator is a pair of parentheses that follow any expression that produces a function value. The parentheses can contain zero or more expressions, separated by commas. Each expression produces one argument value. Each of the argument values will be assigned to the function’s parameter names. There is no runtime error when the number of arguments and the number of parameters do not match. If there are too many argument values, the extra argument values will be ignored. If there are too few argument values, the undefined value will be substituted for the missing values. There is no type checking on the argument values: any type of value can be passed to any parameter.

1『醍醐灌顶，函数调用和用字面量创建函数是两码事，调用最关键的是那对圆括号 ()，圆括号前面可以是函数名，也可以是函数字面量。而圆括号里面是要传递进函数的实参；parameter 实参，调用函数时传递进来的。argument 形参，定义函数时设定的。』

#### 4.3.1 The Method Invocation Pattern

When a function is stored as a property of an object, we call it a method. When a method is invoked, this is bound to that object. If an invocation expression contains a refinement (that is, a . dot expression or [subscript] expression), it is invoked as a method:

```js
// Create myObject. It has a value and an increment
// method. The increment method takes an optional
// parameter. If the argument is not a number, then 1
// is used as the default.
var myObject = {
    value: 0,
    increment: function (inc) {
    this.value += typeof inc === 'number' ? inc : 1;
    }
};

myObject.increment( );
document.writeln(myObject.value); // 1

myObject.increment(2);
document.writeln(myObject.value); // 3
```

A method can use this to access the object so that it can retrieve values from the object or modify the object. The binding of this to the object happens at invocation time. This very late binding makes functions that use this highly reusable. Methods that get their object context from this are called public methods.

1『对于「方法调用模式」，this 绑定其所属的对象，是发生在调用的时候。』

#### 4.3.2 The Function Invocation Pattern

When a function is not the property of an object, then it is invoked as a function: 

    var sum = add(3, 4); // sum is 7

When a function is invoked with this pattern, this is bound to the global object. This was a mistake in the design of the language. Had the language been designed correctly, when the inner function is invoked, this would still be bound to the this  variable of the outer function. A consequence of this error is that a method cannot employ an inner function to help it do its work because the inner function does not share the method’s access to the object as its this is bound to the wrong value. Fortunately, there is an easy workaround. If the method defines a variable and assigns it the value of this, the inner function will have access to this through that variable. By convention, the name of that variable is that:

对于「函数调用模式」，this 绑定到了全局对象上，这是 JS 的设计失误。倘若语言设计正确，那么当内部函数被调用时，this 应该仍然绑定到外部函数的 this 变量。这个设计错误的后果就是方法不能利用内部函数来帮助它工作，因为内部函数的 this 被绑定了错误的值，所以不能共享该方法对对象的访问权。幸运的是，有一个很容易的解决方案：如果该方法定义一个变量并给它赋值为 this，那么内部函数就可以通过那个变量访问到 this。按照约定，我把那个变量命名为 that。

```js
var myObject = {
    value: 0,
    increment: function (inc) {
    this.value += typeof inc === 'number' ? inc : 1;
    }
};

// Augment myObject with a double method.
myObject.double = function ( ) {
    var that = this; // Workaround.
    var helper = function ( ) {
        that.value = add(that.value, that.value);
    };
    helper( ); // Invoke helper as a function.
};

// Invoke double as a method.
myObject.double( );
document.writeln(myObject.getValue( )); // 6
```

1『方法模式调用，用 . 来调用；函数模式调用用 function(); 来调用（比如上面例子里的 help(); ）。』

#### 4.3.3 The Constructor Invocation Pattern

JavaScript is a prototypal inheritance language. That means that objects can inherit properties directly from other objects. The language is class-free. This is a radical departure from the current fashion. Most languages today are classical. Prototypal inheritance is powerfully expressive, but is not widely understood.

JavaScript itself is not confident in its prototypal nature, so it offers an object-making syntax that is reminiscent of the classical languages. Few classical programmers found prototypal inheritance to be acceptable, and classically inspired syntax obscures the language’s true prototypal nature. It is the worst of both worlds.

If a function is invoked with the new prefix, then a new object will be created with a hidden link to the value of the function’s prototype member, and this will be bound to that new object. The new prefix also changes the behavior of the return statement. We will see more about that next.

如果在一个函数前面带上 new 来调用，那么背地里将会创建一个连接到该函数的 prototype 成员的新对象，同时 this 会被绑定到那个新对象上。new 也会改变 return 语句的行为。

1『小程序里 let DBdata = new DBdevice(); 新对象 DBdata 被创建的时候有一个隐藏的连接，这个连接连到 DBdevice 的原型对象，即通过提取字符可以方法到原型对象里的方法，比如 DBdata.gettypedata()，同时在创建的时候，this 值是绑定到 DBdata 对象上的。』

```js
// Create a constructor function called Quo.
// It makes an object with a status property.
var Quo = function (string) {
    this.status = string;
};

// Give all instances of Quo a public method
// called get_status.
Quo.prototype.get_status = function ( ) {
    return this.status;
};

// Make an instance of Quo.
var myQuo = new Quo("confused");
document.writeln(myQuo.get_status( )); // confused
```

Functions that are intended to be used with the new prefix are called constructors. By convention, they are kept in variables with a capitalized name. If a constructor is called without the new prefix, very bad things can happen without a compile-time or runtime warning, so the capitalization convention is really important. Use of this style of constructor functions is not recommended. We will see better alternatives in the next chapter.

作为构造器的函数名约定首个字母大写，这样看到大写的就知道是构造器，不会漏掉 new 来构建新对象，如果漏掉的话会造成很严重的后果；不建议使用上面形式的构造器函数。

1『上面形式创建的对象没有私有属性，后面的章节是利用闭包特性来实现私有属性的。』

#### 4.3.4 The Apply Invocation Pattern

Because JavaScript is a functional object-oriented language, functions can have methods. The apply method lets us construct an array of arguments to use to invoke a function. It also lets us choose the value of this. The apply method takes two parameters. The first is the value that should be bound to this. The second is an array of parameters.

```js
// Make an array of 2 numbers and add them.
var array = [3, 4];
var sum = add.apply(null, array); // sum is 7

// Make an object with a status member.
var statusObject = {
    status: 'A-OK'
};

Quo.prototype.get_status = function ( ) {
    return this.status;
};

// statusObject does not inherit from Quo.prototype,
// but we can invoke the get_status method on
// statusObject even though statusObject does not have
// a get_status method.
var status = Quo.prototype.get_status.apply(statusObject);
// status is 'A-OK'
```

1『 Quo.prototype.get_status.apply(statusObject); 是指定 this 绑定到 apply() 调用时传递的参数，在这里即 statusObject，所以 get_status 函数里的 this.statu 即 statusObject 对象里的 status 属性值。』

### 4.4 Arguments

A bonus parameter that is available to functions when they are invoked is the arguments array. It gives the function access to all of the arguments that were supplied with the invocation, including excess arguments that were not assigned to parameters. This makes it possible to write functions that take an unspecified number of parameters:

当函数被调用时，会得到一个「免费」配送的参数，那就是 arguments 数组。函数可以通过此参数访问所有它被调用时传递给它的参数列表，包括那些没有被分配给函数声明时定义的形式参数的多余参数。这使得编写一个无须指定参数个数的函数成为可能。

1『印证了之前说的，函数在调用的时候额外接收 2 个参数，this 和 parameters。In addition to the declared parameters, every function receives two additional parameters: this and arguments. 印象中后面有说到，arguments 数组可以是一个键值对象（待确认）。』

```js
// Make a function that adds a lot of stuff.
// Note that defining the variable sum inside of
// the function does not interfere with the sum
// defined outside of the function. The function only sees the inner one.

var sum = function ( ) {
    var i, sum = 0;
    for (i = 0; i < arguments.length; i += 1) {
        sum += arguments[i];
    }
    return sum;
};
document.writeln(sum(4, 8, 15, 16, 23, 42)); // 108
```

This is not a particularly useful pattern. In Chapter 6, we will see how we can add a similar method to an array. Because of a design error, arguments is not really an array. It is an array-like object. arguments has a length property, but it lacks all of the array methods. We will see a consequence of that design error at the end of this chapter.

1『上面默认参数（parameters）的用法很赞。』

### 4.5 Return

When a function is invoked, it begins execution with the first statement, and ends when it hits the } that closes the function body. That causes the function to return control to the part of the program that invoked the function.

The return statement can be used to cause the function to return early. When return is executed, the function returns immediately without executing the remaining statements. A function always returns a value. If the return value is not specified, then undefined is returned. If the function was invoked with the new prefix and the return value is not an object, then this (the new object) is returned instead.

如果函数调用时在前面加上了 new 前缀，且返回值不是一个对象，则返回 this（该新对象）。

### 4.6 Exceptions

JavaScript provides an exception handling mechanism. Exceptions are unusual (but not completely unexpected) mishaps that interfere with the normal flow of a program. When such a mishap is detected, your program should throw an exception: 

```js
var add = function (a, b) {
    if (typeof a !== 'number' || typeof b !== 'number') {
    throw {
        name: 'TypeError',
        message: 'add needs numbers'
    };
    }
    return a + b;
}
```

The throw statement interrupts execution of the function. It should be given an exception object containing a name property that identifies the type of the exception, and a descriptive message property. You can also add other properties.

The exception object will be delivered to the catch clause of a try statement:

```js
// Make a try_it function that calls the new add
// function incorrectly.
var try_it = function ( ) {
    try {
        add("seven");
    } catch (e) {
    document.writeln(e.name + ': ' + e.message);
    }
}
try_it( );
```

If an exception is thrown within a try block, control will go to its catch clause. A try statement has a single catch block that will catch all exceptions. If your handling depends on the type of the exception, then the exception handler will have to inspect the name to determine the type of the exception.

1『如果在 try 代码块内抛出了一个异常，控制权就会跳转到它的 catch 从句。』

### 4.7 Augmenting Types

JavaScript allows the basic types of the language to be augmented. In Chapter 3, we saw that adding a method to Object.prototype makes that method available to all objects. This also works for functions, arrays, strings, numbers, regular expressions, and booleans. For example, by augmenting Function.prototype, we can make a method available to all functions:

```js
Function.prototype.method = function (name, func) {
    this.prototype[name] = func;
    return this;
};
```

By augmenting Function.prototype with a method method, we no longer have to type the name of the prototype property. That bit of ugliness can now be hidden. JavaScript does not have a separate integer type, so it is sometimes necessary to extract just the integer part of a number. The method JavaScript provides to do that is ugly. We can fix it by adding an integer method to Number.prototype. It uses either Math.ceiling or Math.floor, depending on the sign of the number: 

```js
Number.method('integer', function ( ) {
    return Math[this < 0 ? 'ceiling' : 'floor'](this);
});

document.writeln((-10 / 3).integer( )); // -3
```

JavaScript lacks a method that removes spaces from the ends of a string. That is an easy oversight to fix:

```js
String.method('trim', function ( ) {
    return this.replace(/^\s+|\s+$/g, '');
});

document.writeln('"' + " neat ".trim( ) + '"'); 
```

Our trim method uses a regular expression. We will see much more about regular expressions in Chapter 7. By augmenting the basic types, we can make significant improvements to the expressiveness of the language. Because of the dynamic nature of JavaScript’s prototypal inheritance, all values are immediately endowed with the new methods, even values that were created before the methods were created.

1『扩充类型体现了 JS 动态特性。上面的 2 个例子需要反复研究。』

The prototypes of the basic types are public structures, so care must be taken when mixing libraries. One defensive technique is to add a method only if the method is known to be missing:

基本类型的原型是公用结构，所以在类库混用时务必小心。一个保险的做法就是只在确定没有该方法时才添加它。

```js
// Add a method conditionally.
Function.prototype.method = function (name, func) {
    if (!this.prototype[name]) {
        this.prototype[name] = func;
    }
};
```

Another concern is that the for in statement interacts badly with prototypes. We saw a couple of ways to mitigate that in Chapter 3: we can use the hasOwnProperty method to screen out inherited properties, and we can look for specific types.

### 4.8 Recursion

A recursive function is a function that calls itself, either directly or indirectly. Recursion is a powerful programming technique in which a problem is divided into a set of similar subproblems, each solved with a trivial solution. Generally, a recursive function calls itself to solve its subproblems.

1『 Recursion 体现了解决问题时采用分解的思维模式。』

The Towers of Hanoi is a famous puzzle. The equipment includes three posts and a set of discs of various diameters with holes in their centers. The setup stacks all of the discs on the source post with smaller discs on top of larger discs. The goal is to move the stack to the destination post by moving one disc at a time to another post, never placing a larger disc on a smaller disc. This puzzle has a trivial recursive solution: 

```js
var hanoi = function (disc, src, aux, dst) {
    if (disc > 0) {
        hanoi(disc - 1, src, dst, aux);
        document.writeln('Move disc ' + disc + ' from ' + src + ' to ' + dst);
        hanoi(disc - 1, aux, src, dst);
    }
};

hanoi(3, 'Src', 'Aux', 'Dst');

It produces this solution for three discs:

Move disc 1 from Src to Dst
Move disc 2 from Src to Aux
Move disc 1 from Dst to Aux
Move disc 3 from Src to Dst
Move disc 1 from Aux to Src
Move disc 2 from Aux to Dst
Move disc 1 from Src to Dst
```

2『汉诺塔的代码反复去看，吃透其递归的实现方式。』

The hanoi function moves a stack of discs from one post to another, using the auxiliary post if necessary. It breaks the problem into three subproblems. First, it uncovers the bottom disc by moving the substack above it to the auxiliary post. It can then move the bottom disc to the destination post. Finally, it can move the substack from the auxiliary post to the destination post. The movement of the substack is handled by calling itself recursively to work out those subproblems.

The hanoi function is passed the number of the disc it is to move and the three posts it is to use. When it calls itself, it is to deal with the disc that is above the disc it is currently working on. Eventually, it will be called with a nonexistent disc number. In that case, it does nothing. That act of nothingness gives us confidence that the function does not recurse forever. Recursive functions can be very effective in manipulating tree structures such as the browser’s Document Object Model (DOM). Each recursive call is given a smaller piece of the tree to work on:

传递给 hanoi 函数的参数包括当前移动的圆盘编号和它将要用到的 3 根柱子。当它调用自身的时候，它去处理当前正在处理的圆盘之上的圆盘。最终，它会以一个不存在的圆盘编号去调用。在这样的情况下，它不执行任何操作。由于该函数对非法值不予理会，我们也就不必担心它会导致死循环。递归函数可以非常高效地操作树形结构，比如浏览器端的文档对象模型（DOM）。每次递归调用时处理指定的树的一小段。

```js
// Define a walk_the_DOM function that visits every
// node of the tree in HTML source order, starting
// from some given node. It invokes a function,
// passing it each node in turn. walk_the_DOM calls
// itself to process each of the child nodes.

var walk_the_DOM = function walk(node, func) {
    func(node);
    node = node.firstChild;
    while (node) {
        walk(node, func);
        node = node.nextSibling;
    }
};

// Define a getElementsByAttribute function. It
// takes an attribute name string and an optional
// matching value. It calls walk_the_DOM, passing it a
// function that looks for an attribute name in the
// node. The matching nodes are accumulated in a
// results array.

var getElementsByAttribute = function (att, value) {
    var results = [];
    walk_the_DOM(document.body, function (node) {
        var actual = node.nodeType === 1 && node.getAttribute(att); 
        if (typeof actual === 'string' && (actual === value || typeof value !== 'string')) {
            results.push(node);
        }
    });
    
    return results;
};
```

Some languages offer the tail recursion optimization. This means that if a function returns the result of invoking itself recursively, then the invocation is replaced with a loop, which can significantly speed things up. Unfortunately, JavaScript does not currently provide tail recursion optimization. Functions that recurse very deeply can fail by exhausting the return stack:

一些语言提供了「尾递归」优化。这意味着如果一个函数返回自身递归调用的结果，那么调用的过程会被替换为一个循环，它可以显著提高速度。遗憾的是，Javascript 当前并没有提供尾递归优化。深度递归的函数可能会因为堆栈溢出而运行失败。尾递归（tail recursion 或 tail-end recursion）是一种在函数的最后执行递归调用语句的特殊形式的递归。

```js
// Make a factorial function with tail
// recursion. It is tail recursive because
// it returns the result of calling itself.
// JavaScript does not currently optimize this form.

var factorial = function factorial(i, a) {
    a = a || 1;
    if (i < 2) {
        return a;
    }
    return factorial(i - 1, a * i);
};

document.writeln(factorial(4)); // 24
```

### 4.9 Scope

Scope in a programming language controls the visibility and lifetimes of variables and parameters. This is an important service to the programmer because it reduces naming collisions and provides automatic memory management: 

```js
var foo = function ( ) {
    var a = 3, b = 5;
    var bar = function ( ) {
        var b = 7, c = 11;
        // At this point, a is 3, b is 7, and c is 11
        a += b + c;
        // At this point, a is 21, b is 7, and c is 11
    };
    // At this point, a is 3, b is 5, and c is not defined 
    bar( );
    // At this point, a is 21, b is 5
};
```

1『 JS 里函数就是一种对象，既然是对象那么所有针对对象的操作都可以针对函数，比如当作一个参数、比如赋值给一个变量等等。而函数的声明有两大类，一是常规的函数式，一是函数表达式（就把整个函数当作一个表达式，可以用 () 把整个函数包起来）。』

Most languages with C syntax have block scope. All variables defined in a block (a list of statements wrapped with curly braces) are not visible from outside of the block. The variables defined in a block can be released when execution of the block is finished. This is a good thing.

Unfortunately, JavaScript does not have block scope even though its block syntax suggests that it does. This confusion can be a source of errors. JavaScript does have function scope. That means that the parameters and variables defined in a function are not visible outside of the function, and that a variable defined anywhere within a function is visible everywhere within the function.

1『ES6 新增的 let 和 const 拥有块级作用域；理解 JS 的函数作用域很重要。』

In many modern languages, it is recommended that variables be declared as late as possible, at the first point of use. That turns out to be bad advice for JavaScript because it lacks block scope. So instead, it is best to declare all of the variables used in a function at the top of the function body.

糟糕的是，尽管 Javascript 的代码块语法貌似支持块级作用域，但实际上 Javascript 并不支持。这个混淆之处可能成为错误之源。Javascript 确实有函数作用域。那意味着定义在函数中的参数和变量在函数外部是不可见的，而在一个函数内部任何位置定义的变量，在该函数内部任何地方都可见。很多现代语言都推荐尽可能延迟声明变量。而用在 Javascript 上的话却会成为槽糕的建议，因为它缺少块级作用域。所以，最好的做法是在函数体的顶部声明函数中可能用到的所有变量。

### 4.10 Closure

The good news about scope is that inner functions get access to the parameters and variables of the functions they are defined within (with the exception of this and arguments). This is a very good thing. Our getElementsByAttribute function worked because it declared a results variable, and the inner function that it passed to walk\_the\_DOM also had access to the results variable.

A more interesting case is when the inner function has a longer lifetime than its outer function. Earlier, we made a myObject that had a value and an increment method. Suppose we wanted to protect the value from unauthorized changes.

Instead of initializing myObject with an object literal, we will initialize myObject by calling a function that returns an object literal. That function defines a value variable. That variable is always available to the increment and getValue methods, but the function’s scope keeps it hidden from the rest of the program: 

我们的 getelementsbyattribute 函数可以工作，是因为它声明了一个 results 变量，而传递给 walk\_the_DOM 的内部函数也可以访问 results 变量。一个更有趣的情形是内部函数拥有比它的外部函数更长的生命周期。之前，我们构造了一个 myObject 对象，它拥有一个 value 属性和一个 increment 方法。假定我们希望保护该值不会被非法更改。和以对象字面量形式去初始化 myObject 不同，我们通过调用一个函数的形式去初始化 myObject，该函数会返回一个对象字面量。函数里定义了一个 value 变量。该变量对 increment 和 getValue 方法总是可用的，但函数的作用域使得它对其他的程序来说是不可见的。

```js
var myObject = function ( ) {
    var value = 0;
    return {
        increment: function (inc) {
        value += typeof inc === 'number' ? inc : 1;
        },
        getValue: function ( ) {
            return value;
        }
    };
}( );
```

We are not assigning a function to myObject. We are assigning the result of invoking that function. Notice the ( ) on the last line. The function returns an object containing two methods, and those methods continue to enjoy the privilege of access to the value variable.

我们并没有把一个函数赋值给 myObject。我们是把调用该函数后返回的结果赋值给它。注意最后一行的（）。该函数返回一个包含两个方法的对象，并且这些方法继续享有访问 value 变量的特权。

1『绝妙的操作，这样可以把 value 值保护起来，不让外界直接可以修改这个值。关键点是函数后面的 ()，是把调用该函数后返回的结果赋值给这个变量，该函数返回的是一个对象，对象里包含 2 个方法，这两个方法都可以访问该函数体内定义的变量。这就理解了「通过调用一个函数的形式去初始化 myObject，该函数会返回一个对象字面量。」』

The Quo constructor from earlier in this chapter produced an object with a status property and a get_status method. But that doesn’t seem very interesting. Why would you call a getter method on a property you could access directly? It would be more useful if the status property were private. So, let’s define a different kind of quo function to do that:

本章之前的 Quo 构造器产生一个带有 status 属性和 get status 方法的对象。为什么要用一个 getter 方法去访问你本可以直接访问到的属性呢？如果 status 是私有属性，它才是更有意义的。所以，让我们定义另一种形式的 quo 函数来做此事：

1『这其实就是 JS 里实现私有属性的绝妙方式。』

```js
// Create a maker function called quo. It makes an
// object with a get_status method and a private status property.

var quo = function (status) {
    return {
        get_status: function ( ) {
            return status;
        }
    };
};

// Make an instance of quo.

var myQuo = quo("amazed");
document.writeln(myQuo.get_status( ));
```

This quo function is designed to be used without the new prefix, so the name is not capitalized. When we call quo, it returns a new object containing a get\_status method. A reference to that object is stored in myQuo. The get\_status method still has privileged access to quo’s status property even though quo has already returned.

get\_status does not have access to a copy of the parameter; it has access to the parameter itself. This is possible because the function has access to the context in which it was created. This is called closure.

当我们调用 quo 时，它返回包含 get\_status 方法的一个新对象。该对象的一个引用保存在 myQuo 中。即使 quo 已经返回了，但 get\_status 方法仍然享有访问 quo 对象的 status 属性的特权。get\_status 方法并不是访问该参数的一个副本，它访问的就是该参数本身。因为该函数可以访问它被创建时所处的上下文环境。这被称为闭包。

1『闭包的本质来了：该函数可以访问它被创建时所处的上下文环境，即为闭包。』

Let’s look at a more useful example:

```js
// Define a function that sets a DOM node's color
// to yellow and then fades it to white.

var fade = function (node) {
    var level = 1;
    var step = function ( ) {
        var hex = level.toString(16);
        node.style.backgroundColor = '#FFFF' + hex + hex;
        if (level < 15) {
            level += 1;
            setTimeout(step, 100);
        }
    };
    setTimeout(step, 100);
};

fade(document.body);
```

We call fade, passing it document.body (the node created by the HTML \<body> tag). fade sets level to 1. It defines a step function. It calls setTimeout, passing it the step function and a time (100 milliseconds). It then returns—fade has finished.

Suddenly, about a 10th of a second later, the step function gets invoked. It makes a base 16 character from fade’s level. It then modifies the background color of fade’s node. It then looks at fade’s level. If it hasn’t gotten to white yet, it then increments fade’s level and uses setTimeout to schedule itself to run again.

Suddenly, the step function gets invoked again. But this time, fade’s level is 2. fade returned a while ago, but its variables continue to live as long as they are needed by one or more of fade’s inner functions.

It is important to understand that the inner function has access to the actual variables of the outer functions and not copies in order to avoid the following problem:

fade 函数设置 level 为 1。它定义了一个 step 函数；接着调用 settimeout，并传递 step 函数和一个时间（100 毫秒）给它。然后它返回，fade 函数结東。在大约十分之一秒后，step 函数被调用。它把 fade 函数的 1evel 变量转化为 16 位字符。接着，它修改 fade 函数得到的节点的背景颜色。然后査看 fade 函数的 level 变量。如果背景色尚未变成白色，那么它增大 fade 函数的 level 变量，接着用 settimeout 预定让它自己再次运行。step 函数很快再次被调用。但这次，fade 函数的 level 变量值变成 2。fade 函数在之前已经返回了，但只要 fade 的内部函数需要，它的变量就会持续保留。为了避免下面的问题，理解内部函数能访问外部函数的实际变量而无须复制是很重要的。

```js
// BAD EXAMPLE
// Make a function that assigns event handler functions to an array of nodes the wrong way.
// When you click on a node, an alert box is supposed to display the ordinal of the node.
// But it always displays the number of nodes instead.

var add_the_handlers = function (nodes) {
    var i;
    for (i = 0; i < nodes.length; i += 1) {
        nodes[i].onclick = function (e) {
            alert(i);
        };
    }
};

// END BAD EXAMPLE
```

The add\_the_handlers function was intended to give each handler a unique number (i). It fails because the handler functions are bound to the variable i, not the value of the variable i at the time the function was made:

add\_the_handlers 函数的本意是想传递给每个事件处理器一个唯一值（i）。但它未能达到目的，因为事件处理器函数绑定了变量 i 本身，而不是函数在构造时的变量的值。

```js
// BETTER EXAMPLE
// Make a function that assigns event handler functions to an array of nodes the right way.
// When you click on a node, an alert box will display the ordinal of the node.

var add_the_handlers = function (nodes) {
    var i;
    for (i = 0; i < nodes.length; i += 1) {
        nodes[i].onclick = function (i) {
            return function (e) {
                alert(e);
            };
        }(i);
    }
};
```

Now, instead of assigning a function to onclick, we define a function and immediately invoke it, passing in i. That function will return an event handler function that is bound to the value of i that was passed in, not to the i defined in add\_the_handlers. That returned function is assigned to onclick.

避免在循环中创建函数，它可能只会带来无谓的计算，还会引起混淆，正如上面那个糟糕的例子。我们可以先在循环之外创建一个辅助函数，让这个辅助函数再返回一个绑定了当前立值的函数，这样就不会导致混淆了。

1『这里的知识点感觉很重要，目前还没弄明白。（2020-03-29）』

### 4.11 Callbacks

Functions can make it easier to deal with discontinuous events. For example, suppose there is a sequence that begins with a user interaction, making a request of the server, and finally displaying the server’s response. The native way to write that would be:

```js
request = prepare_the_request( );
response = send_request_synchronously(request);
display(response);
```

The problem with this approach is that a synchronous request over the network will leave the client in a frozen state. If either the network or the server is slow, the degradation in responsiveness will be unacceptable. A better approach is to make an asynchronous request, providing a callback function that will be invoked when the server’s response is received. An asynchronous function returns immediately, so the client isn’t blocked: 

```js
request = prepare_the_request( );
send_request_asynchronously(request, function (response) {
    display(response);
});
```

We pass a function parameter to the send\_request_asynchronously function that will be called when the response is available.

函数使得对不连续事件的处理变得更容易。例如，假定有这么一个序列，由用户交互行为触发，向服务器发送请求，最终显示服务器的响应。最自然的写法可能会是这样的；这种方式的问题在于，网络上的同步请求会导致客户端进入假死状态。如果网络传输或服务器很慢，响应会慢到让人不可接受。更好的方式是发起异步请求，提供一个当服务器的响应到达时随即触发的回调函数。异步函数立即返回，这样客户端就不会被阻塞。

1『回调函数目前的理解，把这个任务悬挂起来，做个标记，先干其他的事，等那边回复后再继续这个任务。』

### 4.12 Module

We can use functions and closure to make modules. A module is a function or object that presents an interface but that hides its state and implementation. By using functions to produce modules, we can almost completely eliminate our use of global variables, thereby mitigating one of JavaScript’s worst features.

For example, suppose we want to augment String with a deentityify method. Its job is to look for HTML entities in a string and replace them with their equivalents. It makes sense to keep the names of the entities and their equivalents in an object.

But where should we keep the object? We could put it in a global variable, but global variables are evil. We could define it in the function itself, but that has a runtime cost because the literal must be evaluated every time the function is invoked. The ideal approach is to put it in a closure, and perhaps provide an extra method that can add additional entities:

可以把它定义在该函数的内部，但是那会带来运行时的损耗，因为每次执行该函数的时候该字面量都会被求值一次。理想的方式是把它放入一个闭包，而且也许还能提供一个增加更多字符实体的扩展方法。

1『这又是闭包的一个应用场景。』

```js
String.method('deentityify', function ( ) {

    // The entity table. It maps entity names to characters.
    
    var entity = {
        quot: '"',
        lt: '<',
        gt: '>'
    };
    
    // Return the deentityify method.
    return function ( ) {
        // This is the deentityify method. It calls the string
        // replace method, looking for substrings that start
        // with '&' and end with ';'. If the characters in
        // between are in the entity table, then replace the
        // entity with the character from the table. It uses
        // a regular expression (Chapter 7).
        
        return this.replace(/&([^&;]+);/g,
            function (a, b) {
                var r = entity[b];
                return typeof r === 'string' ? r : a;
            }
        );
    };
}( );
```

Notice the last line. We immediately invoke the function we just made with the ( ) operator. That invocation creates and returns the function that becomes the deentityify method.

```js
document.writeln(
    '&lt;&quot;&gt;'.deentityify( )); // <"> 
```

The module pattern takes advantage of function scope and closure to create relationships that are binding and private. In this example, only the deentityify method has access to the entity data structure.

The general pattern of a module is a function that defines private variables and functions; creates privileged functions which, through closure, will have access to the private variables and functions; and that returns the privileged functions or stores them in an accessible place.

Use of the module pattern can eliminate the use of global variables. It promotes information hiding and other good design practices. It is very effective in encapsulat-ing applications and other singletons.

模块模式利用了函数作用域和闭包来创建被绑定对象与私有成员的关联，在这个例子中，只有 deentityify 方法有权访问字符实体表这个数据对象。模块模式的一般形式是：一个定义了私有变量和函数的函数；利用闭包创建可以访问私有变量和函数的特权函数；最后返回这个特权函数，或者把它们保存到一个可访问到的地方。使用模块模式就可以摒弃全局变量的使用。它促进了信息隐藏和其他优秀的设计实践。对于应用程序的封装，或者构造其他单例对象，模块模式非常有效。

3『模块模式通常结合单例模式（Singleton Pattern）使用。Javascript 的单例就是用对象字面量表示法创建的对象，对象的属性值可以是数值或函数，并且属性值在该对象的生命周期中不会发生变化。它通常作为工具为程序其他部分提供功能支持。』

It can also be used to produce objects that are secure. Let’s suppose we want to make an object that produces a serial number:

```js
var serial_maker = function ( ) {

    // Produce an object that produces unique strings. A
    // unique string is made up of two parts: a prefix
    // and a sequence number. The object comes with
    // methods for setting the prefix and sequence
    // number, and a gensym method that produces unique
    // strings.
    
    var prefix = '';
    var seq = 0;
    return {
        set_prefix: function (p) {
            prefix = String(p);
        },
        set_seq: function (s) {
            seq = s;
        },
        
        gensym: function ( ) {
            var result = prefix + seq;
            seq += 1;
            return result;
        }
    };
};

var seqer = serial_maker( );
seqer.set_prefix = ('Q';)
seqer.set_seq = (1000);
var unique = seqer.gensym( ); // unique is "Q1000"
```

The methods do not make use of this or that. As a result, there is no way to compromise the seqer. It isn’t possible to get or change the prefix or seq except as permitted by the methods. The seqer object is mutable, so the methods could be replaced, but that still does not give access to its secrets. seqer is simply a collection of functions, and those functions are capabilities that grant specific powers to use or modify the secret state.

If we passed seqer.gensym to a third party’s function, that function would be able to generate unique strings, but would be unable to change the prefix or seq.

Seder 包含的方法都没有用到 this 或 that，因此没有办法损害 seder。除非调用对应的方法，否则没法改变 prefix 或 seq 的值。seer 对象是可变的，所以它的方法可能会被替换掉，但替换后的方法依然不能访问私有成员。seder 就是一组函数的集合，而且那些函数被授予特权，拥有使用或修改私有状态的能力。如果我们把 seqer.gensym 作为一个值传递给第三方函数，那个函数能用它产生唯一字符串，但却不能通过它来改变 prefix 或 seq 的值。

### 4.13 Cascade

Some methods do not have a return value. For example, it is typical for methods that set or change the state of an object to return nothing. If we have those methods return this instead of undefined, we can enable cascades. In a cascade, we can call many methods on the same object in sequence in a single statement. An Ajax library that enables cascades would allow us to write in a style like this: 

如果我们让这些方法返回 this 而不是 undefined，就可以启用级联。在一个级联中，我们可以在单独一条语句中依次调用同一个对象的很多方法。一个启用级联的 Ajax 类库可能允许我们以这样的形式去编码。

```js
getElement('myBoxDiv').
    move(350, 150).
    width(100).
    height(100).
    color('red').
    border('10px outset'). padding('4px'). appendText("Please stand by").
    on('mousedown', function (m) { 
        this.startDrag(m, this.getNinth(m)); 
    }).
    on('mousemove', 'drag').
    on('mouseup', 'stopDrag').
    later(2000, function ( ) {
        this.
            color('yellow').
            setHTML("What hath God wraught?").
            slide(400, 40, 200, 200);
        }).
    tip('This box is resizeable');
```

In this example, the getElement function produces an object that gives functionality to the DOM element with id="myBoxDiv". The methods allow us to move the element, change its dimensions and styling, and add behavior. Each of those methods returns the object, so the result of the invocation can be used for the next invocation. Cascading can produce interfaces that are very expressive. It can help control the tendency to make interfaces that try to do too much at once.

级联技术可以产生出极富表现力的接口。它也能给那波构造「全能」接口的热潮降降温，一个接口没必要一次做太多事情。

### 4.14 Curry

Functions are values, and we can manipulate function values in interesting ways. Currying allows us to produce a new function by combining a function and an argument:

函数也是值，从而我们可以用有趣的方式去操作函数值。柯里化允许我们把函数与传递给它的参数相结合，产生出一个新的函数。

```js
var add1 = add.curry(1);
document.writeln(add1(6)); // 7
```

add1 is a function that was created by passing 1 to add’s curry method. The add1 function adds 1 to its argument. JavaScript does not have a curry method, but we can fix that by augmenting Function.prototype:

```js
Function.method('curry', function ( ) {
    var args = arguments, that = this;
    return function ( ) {
        return that.apply(null, args.concat(arguments));
    };
}); // Something isn't right...
```

The curry method works by creating a closure that holds that original function and the arguments to curry. It returns a function that, when invoked, returns the result of calling that original function, passing it all of the arguments from the invocation of curry and the current invocation. It uses the Array concat method to concatenate the two arrays of arguments together.

Unfortunately, as we saw earlier, the arguments array is not an array, so it does not have the concat method. To work around that, we will apply the array slice method on both of the arguments arrays. This produces arrays that behave correctly with the concat method:

Curry 方法通过创建一个保存着原始函数和要被套用的参数的闭包来工作。它返回另一个函数，该函数被调用时，会返回调用原始函数的结果，并传递调用 curry 时的参数加上当前调用的参数。它使用 Array 的 concat 方法连接两个参数数组。糟糕的是，就像我们先前看到的那样，arguments 数组并非一个真正的数组，所以它并没有 concat 方法。要避开这个向题，我们必须在两个 arguments 数组上都应用数组的 slice 方法。这样产生出拥有 concat 方法的常规数组。

```js
Function.method('curry', function ( ) {
    var slice = Array.prototype.slice,
    args = slice.apply(arguments),
    that = this;
    return function ( ) {
        return that.apply(null, args.concat(slice.apply(arguments)));
    };
});
```

3『柯里化，也常译为「局部套用」，是把多参数函数转换为一系列单参数函数并进行调用的技术。这项技术以数学家 Haskell Curry 的名字命名。』

### 4.15 Memoization

Functions can use objects to remember the results of previous operations, making it possible to avoid unnecessary work. This optimization is called memoization. JavaScript’s objects and arrays are very convenient for this. Let’s say we want a recursive function to compute Fibonacci numbers. A Fibonacci number is the sum of the two previous Fibonacci numbers. The first two are 0 and 1: 

```js
var fibonacci = function (n) {
    return n < 2 ? n : fibonacci(n - 1) + fibonacci(n - 2);
};
for (var i = 0; i <= 10; i += 1) {
    document.writeln('// ' + i + ': ' + fibonacci(i));
}

// 0: 0
// 1: 1
// 2: 1
// 3: 2
// 4: 3
// 5: 5
// 6: 8
// 7: 13
// 8: 21
// 9: 34
// 10: 55
```

This works, but it is doing a lot of unnecessary work. The fibonacci function is called 453 times. We call it 11 times, and it calls itself 442 times in computing values that were probably already recently computed. If we memoize the function, we can significantly reduce its workload. We will keep our memoized results in a memo array that we can hide in a closure. When our function is called, it first looks to see if it already knows the result. If it does, it can immediately return it:

我们在一个名为 memo 的数组里保存我们的存储结果，存储结果可以隐藏在闭包中。当函数被调用时，这个函数首先检査结果是否已存在，如果已经存在，就立即返回这个结果。

```js
var fibonacci = function ( ) {
    var memo = [0, 1];
    var fib = function (n) {
        var result = memo[n];
        if (typeof result !== 'number') {
            result = fib(n - 1) + fib(n - 2); memo[n] = result;
        }
        return result;
        };
    return fib;
}( );
```

This function returns the same results, but it is called only 29 times. We called it 11 times. It called itself 18 times to obtain the previously memoized results. We can generalize this by making a function that helps us make memoized functions. The memoizer function will take an initial memo array and the fundamental function. It returns a shell function that manages the memo store and that calls the fundamental function as needed. We pass the shell function and the function’s parameters to the fundamental function:

```js
var memoizer = function (memo, fundamental) {
    var shell = function (n) {
        var result = memo[n];
        if (typeof result !== 'number') {
            result = fundamental(shell, n);
            memo[n] = result;
        }
        return result;
    };
    return shell;
};
```

We can now define fibonacci with the memoizer, providing the initial memo array and fundamental function:

```js
var fibonacci = memoizer([0, 1], function (shell, n) {
    return shell(n - 1) + shell(n - 2);
});
```

By devising functions that produce other functions, we can significantly reduce the amount of work we have to do. For example, to produce a memoizing factorial function, we only need to supply the basic factorial formula: 

```js
var factorial = memoizer([1, 1], function (shell, n) {
    return n * shell(n - 1);
});
```

## 0501. Inheritance

Divides one thing entire to many objects; Like perspectives, which rightly gazed upon. Show nothing but confusion...

Inheritance is an important topic in most programming languages. In the classical languages (such as Java), inheritance (or extends) provides two useful services. First, it is a form of code reuse. If a new class is mostly similar to an existing class, you only have to specify the differences. Patterns of code reuse are extremely important because they have the potential to significantly reduce the cost of software development. The other benefit of classical inheritance is that it includes the specification of a system of types. This mostly frees the programmer from having to write explicit casting operations, which is a very good thing because when casting, the safety benefits of a type system are lost.

类继承的另一个好处是引入了一套类型系统的规范。由于程序员无需编写显式类型转换的代码，他们的工作量将大大减轻，这是一件很好的事情，因为类型转换会丧失类型系统在安全上的优势。

JavaScript, being a loosely typed language, never casts. The lineage of an object is irrelevant. What matters about an object is what it can do, not what it is descended from. JavaScript provides a much richer set of code reuse patterns. It can ape the classical pattern, but it also supports other patterns that are more expressive. The set of possible inheritance patterns in JavaScript is vast. In this chapter, we’ll look at a few of the most straightforward patterns. Much more complicated constructions are possible, but it is usually best to keep it simple. In classical languages, objects are instances of classes, and a class can inherit from another class. JavaScript is a prototypal language, which means that objects inherit directly from other objects.

1『作者的观点是没必要使用那些模拟基于类的面向对象（new 结合构造函数的语法），直接使用原生的基于原型的面向对象来编程。但 ES6 以后，模拟基于类的面向对象的那条线，升级为通过 class 关键字来实现了，那么其实也可以走那条线了。但一定得用 class 来声明类。（2020-05-30）』

### 5.1 Pseudoclassical

JavaScript is conflicted about its prototypal nature. Its prototype mechanism is obscured by some complicated syntactic business that looks vaguely classical. Instead of having objects inherit directly from other objects, an unnecessary level of indirection is inserted such that objects are produced by constructor functions.

Javascript 的原型存在着诸多矛盾。它的某些复杂的语法看起来就像那些基于类的语言，这些语法问题掩盖了它的原型机制。它不直接让对象从其他对象继承，反而插入了一个多余的间接层：通过构造器函数产生对象。

1『

作者说到点子上了，JS 放着好好的基于原型的面向对象特性不用，非要模仿基于类的面向对象，得不偿失。

基于原型的面向对象，老版可以采用下面方法实现。创建了一个空函数作为类，并把传入的原型挂在了它的 prototype，最后创建了一个它的实例，根据 new 的行为，这将产生一个以传入的第一个参数为原型的对象。这个函数无法做到与原生的 Object.create 一致，一个是不支持第二个参数，另一个是不支持 null 作为原型，所以放到今天意义已经不大了。ES6 以来，JavaScript 提供了一系列内置函数，以便更为直接地访问操纵原型。三个方法分别为：1）Object.create 根据指定的原型创建新对象，原型可以是 null；2）Object.getPrototypeOf 获得一个对象的原型；3）Object.setPrototypeOf 设置一个对象的原型。利用这三个方法，我们可以完全抛开类的思维，利用原型来实现抽象和复用。

基于类的面向对象，老版插入了一个多余的间接层：通过构造器函数产生对象。这个方法很繁琐，ES6 新增了 class 语法来定义类。

```js
if (typeof Object.create !== 'function') {
    Object.create = function (o) {
    var F = function () {};
    F.prototype = o;
    return new F();
};
}
var another_stooge = Object.create(stooge);  // 这个 create() 方法是自己定义的，新版的 JS 里提供了该方法。
```

』

When a function object is created, the Function constructor that produces the function object runs some code like this:

```js
this.prototype = {constructor: this};
```

The new function object is given a prototype property whose value is an object containing a constructor property whose value is the new function object. The prototype object is the place where inherited traits are to be deposited. Every function gets a prototype object because the language does not provide a way of determining which functions are intended to be used as constructors. The constructor property is not useful. It is the prototype object that is important.

When a function is invoked with the constructor invocation pattern using the new prefix, this modifies the way in which the function is executed. If the new operator were a method instead of an operator, it could have been implemented like this: 

新函数对象被赋予一个 prototype 属性，它的值是一个包含 constructor 属性且属性值为该新函数的对象。这个 prototype 对象是存放继承特征的地方。因为 Javascript 语言没有提供一种方法去确定哪个函数是打算用来做构造器的，所以每个函数都会得到一个 prototype 对象。constructor 属性没什么用，重要的是 prototype 对象。当采用构造器调用模式，即用 new 前缀去调用一个函数时，函数执行的方式会被修改。如果 new 运算符是一个方法而不是一个运算符，它可能会像这样执行：

1『理清了之前的困惑，用 new 构建一个函数，等价于采用构造器来构造函数。函数被创建时，最重要是其原型对象，因为一些列要继承的方法是在原型对象里面。新创建的函数对象会自带一个原型对象，该原型对象里有一个构造器属性（对象），其属性值就是这个新函数的对象。』

```js
Function.method('new', function ( ) {
    // Create a new object that inherits from the constructor's prototype.
    var that = Object.create(this.prototype);
    
    // Invoke the constructor, binding –this- to the new object.
    var other = this.apply(that, arguments);
    
    // If its return value isn't an object, substitute the new object.
    return (typeof other === 'object' && other) || that;
});
```

We can define a constructor and augment its prototype: 

```js
var Mammal = function (name) {
    this.name = name;
};

Mammal.prototype.get_name = function ( ) {
    return this.name;
};

Mammal.prototype.says = function ( ) {
    return this.saying || '';
};
```

Now, we can make an instance:

```js
var myMammal = new Mammal('Herb the Mammal');
var name = myMammal.get_name( ); // 'Herb the Mammal'
```

We can make another pseudoclass that inherits from Mammal by defining its constructor function and replacing its prototype with an instance of Mammal: 

```js
// 下面的不是函数调用，记牢，调用有 ()，只是一个函数声明
var Cat = function (name) {
    this.name = name;
    this.saying = 'meow';
};

// Replace Cat.prototype with a new instance of Mammal 
Cat.prototype = new Mammal( );

// Augment the new prototype with purr and get_name methods.
Cat.prototype.purr = function (n) {
    var i, s = '';
    for (i = 0; i < n; i += 1) {
        if (s) {
            s += '-';
        }
        s += 'r';
    }
    return s;
};

Cat.prototype.get_name = function ( ) {
    return this.says( ) + ' ' + this.name + ' ' + this.says( );
};

var myCat = new Cat('Henrietta');
var says = myCat.says( ); // 'meow'
var purr = myCat.purr(5); // 'r-r-r-r-r'
var name = myCat.get_name( ); // 'meow Henrietta meow'
```

The pseudoclassical pattern was intended to look sort of object-oriented, but it is looking quite alien. We can hide some of the ugliness by using the method method and defining an inherits method:

伪类模式本意是想向面向对象常拢，但它看起来格格不入。我们可以隐藏一些丑陋的细节，通过使用 method 方法来定义一个 inherits 方法实现：

```js
Function.method('inherits', function (Parent) {
    this.prototype = new Parent( );
    return this;
});
```

Our inherits and method methods return this, allowing us to program in a cascade style. We can now make our Cat with one statement.

我们的 inherits 和 method 方法都返回 this，这样允许我们可以采用级联的形式编程。现在可以只用一行语句构造我们的 cat 对象。

```js
var Cat = function (name) {
    this.name = name;
    this.saying = 'meow';
}.

.inherits(Mammal)
.method('purr', function (n) {
    var i, s = '';
    for (i = 0; i < n; i += 1) {
        if (s) {
            s += '-';
        }
        s += 'r';
    }
    return s;
}).

.method('get_name', function ( ) {
    return this.says( ) + ' ' + this.name + ' ' + this.says( );
});
```

By hiding the prototype jazz, it now looks a bit less alien. But have we really improved anything? We now have constructor functions that act like classes, but at the edges, there may be surprising behavior. There is no privacy; all properties are public. There is no access to super methods.

Even worse, there is a serious hazard with the use of constructor functions. If you forget to include the new prefix when calling a constructor function, then this will not be bound to a new object. Sadly, this will be bound to the global object, so instead of augmenting your new object, you will be clobbering global variables. That is really bad. There is no compile warning, and there is no runtime warning.

This is a serious design error in the language. To mitigate this problem, there is a convention that all constructor functions are named with an initial capital, and that nothing else is spelled with an initial capital. This gives us a prayer that visual inspection can find a missing new. A much better alternative is to not use new at all.

The pseudoclassical form can provide comfort to programmers who are unfamiliar with JavaScript, but it also hides the true nature of the language. The classically inspired notation can induce programmers to compose hierarchies that are unnecessarily deep and complicated. Much of the complexity of class hierarchies is motivated by the constraints of static type checking. JavaScript is completely free of those constraints. In classical languages, class inheritance is the only form of code reuse. JavaScript has more and better options.

我们现在有了行为像「类」的构造器函数，但仔细看它们，你会惊讶地发现：没有私有环境，所有的属性都是公开的。无法访问 super（父类）的方法。更糟糕的是，使用构造器函数存在一个严重的危害。如果你在调用构造器函数时忘记了在前面加上 new 前缀，那么 this 将不会被绑定到一个新对象上。悲剧的是，this 将被绑定到全局对象上，所以你不但没有扩充新对象，反而破坏了全局变量环境。那真是糟透了。发生那样的情况时，既没有编译时警告，也没有运行时警告。这是一个严重的语言设计错误。为了降低这个问题帯来的风险，所有的构造器函数都约定命名成首字母大写的形式，并且不以首字母大写的形式拼写任何其他的东西。这样我们至少可以通过目视检査去发现是否缺少了 new 前级。一个更好的备选方案就是根本不使用 new。「伪类」形式可以给不熟悉 Javascript 的程序员提供便利，但它也隐藏了该语言的真实的本质。借鉴类的表示法可能误导程序员去编写过于深入与复杂的层次结构。许多复杂的类层次结构产生的原因就是静态类型检査的约束。Javascript 完全摆脱了那些约束。在基于类的语言中，类继承是代码重用的唯一方式。而 Javascript 有着更多且更好的选择。

1『许多复杂的类层次结构产生的原因就是静态类型检査的约束。Javascript 完全摆脱了那些约束，这是 JS 又一大优点，弱类型。』

### 5.2 Object Specifiers

It sometimes happens that a constructor is given a very large number of parameters. This can be troublesome because it can be very difficult to remember the order of the arguments. In such cases, it can be much friendlier if we write the constructor to accept a single object specifier instead. That object contains the specification of the object to be constructed. So, instead of:

有时候，构造器要接受一大串参数。这可能令人烦恼，因为要记住参数的顺序非常困难。在这种情况下，如果我们在编写构造器时让它接受一个简单的对象说明符，可能会更加友好。

```js
var myObject = maker(f, l, m, c, s);
```

we can write:

```js
var myObject = maker({
    first: f,
    last: l,
    state: s,
    city: c
});
```

The arguments can now be listed in any order, arguments can be left out if the constructor is smart about defaults, and the code is much easier to read. This can have a secondary benefit when working with JSON (see Appendix E). JSON text can only describe data, but sometimes the data represents an object, and it would be useful to associate the data with its methods. This can be done trivially if the constructor takes an object specifier because we can simply pass the JSON object to the constructor and it will return a fully constituted object.

当与 JSON 一起工作时，这种形式还可以有一个间接的好处。JSON 文本只能描述数据，但有时数据表示的是一个对象，把该数据与它的方法关联起来是有用的。如果构造器取得一个对象说明符，就能让它轻松实现，因为我们可以筒单地把 JSON 对象传递给构造器，而它将返回一个构造完全的对象。

### 5.3 Prototypal

In a purely prototypal pattern, we dispense with classes. We focus instead on the objects. Prototypal inheritance is conceptually simpler than classical inheritance: a new object can inherit the properties of an old object. This is perhaps unfamiliar, but it is really easy to understand. You start by making a useful object. You can then make many more objects that are like that one. The classification process of breaking an application down into a set of nested abstract classes can be completely avoided.

1『摒弃基于类的面向对象，直接用基于原型的面向对象。』

Let’s start by using an object literal to make a useful object: 

```js
var myMammal = {
    name : 'Herb the Mammal',
    get_name : function ( ) {
        return this.name;
    },
    says : function ( ) {
        return this.saying || '';
    }
};
```

Once we have an object that we like, we can make more instances with the Object. create method from Chapter 3. We can then customize the new instances:

```js
var myCat = Object.create(myMammal);  // 基于 myMammal 为原型对象创建新对象
// 下面的属性都是新对象 myCat 的属性
myCat.name = 'Henrietta';
myCat.saying = 'meow';
myCat.purr = function (n) {
    var i, s = '';
    for (i = 0; i < n; i += 1) {
        if (s) {
            s += '-';
        }
        s += 'r';
    }
    return s;
};
myCat.get_name = function ( ) {
    return this.says( ) + ' ' + this.name + ' ' + this.says( );
};
```

1『基于原型链的写法比基于类的写法简洁多了。』

This is differential inheritance. By customizing a new object, we specify the differences from the object on which it is based. Sometimes is it useful for data structures to inherit from other data structures. Here is an example: Suppose we are parsing a language such as JavaScript or TEX in which a pair of curly braces indicates a scope. Items defined in a scope are not visible outside of the scope. In a sense, an inner scope inherits from its outer scope. JavaScript objects are very good at representing this relationship. The block function is called when a left curly brace is encountered. The parse function will look up symbols from scope, and augment scope when it defines new symbols:

有时候，它对某些数据结构继承于其他数据结构的情形非常有用。这里就有一个例子：假定我们要解析一门类似 Javascript 或 TEX 那样用一对花括号指示作用域的语言。定义在某个作用域里定义的条目在该作用域之外是不可见的。但在某种意义上，一个内部作用域会继承它的外部作用域。Javascript 在表示这样的关系上做得非常好。当遇到一个左花括号时 block 函数被调用。parse 函数将从 scope 中寻找符号，并且当它定义了新的符号时扩充 scope。

1『 JS 里强大的函数（一种特殊的对象）可以解决私有属性的问题，用闭包来解决。』

```js
var block = function ( ) {
// Remember the current scope. Make a new scope that includes everything from the current one.
var oldScope = scope;
scope = Object.create(scope);

// Advance past the left curly brace.
advance('{');

// Parse using the new scope.
parse(scope);

// Advance past the right curly brace and discard the new scope, restoring the old one.
advance('}');
scope = oldScope;
};
```

### 5.4 Functional

One weakness of the inheritance patterns we have seen so far is that we get no privacy. All properties of an object are visible. We get no private variables and no private methods. Sometimes that doesn’t matter, but sometimes it matters a lot. In frustration, some uninformed programmers have adopted a pattern of pretend privacy. If they have a property that they wish to make private, they give it an odd-looking name, with the hope that other users of the code will pretend that they cannot see the odd looking members. Fortunately, we have a much better alternative in an application of the module pattern.

一些无知的程序员接受了一种伪装私有（pretend privacy）的模式。如果想构造一个私有属性，他们就给它起一个怪模怪样的名字，并且希望其他使用代码的用户假装看不到这些奇怪的成员。

We start by making a function that will produce objects. We will give it a name that starts with a lowercase letter because it will not require the use of the new prefix. The function contains four steps:

1. It creates a new object. There are lots of ways to make an object. It can make an object literal, or it can call a constructor function with the new prefix, or it can use the Object.create method to make a new instance from an existing object, or it can call any function that returns an object.

2. It optionally defines private instance variables and methods. These are just ordinary vars of the function.

3. It augments that new object with methods. Those methods will have privileged access to the parameters and the vars defined in the second step.

4. It returns that new object.

Here is a pseudocode template for a functional constructor (boldface text added for emphasis):

我们从构造一个生成对象的函数开始。我们以小写字母开头来命名它，因为它并不需要使用 new 前缀。

1『第 1 步里说的「创建新对象」其实对应于之前重点提到的，函数调用所用的 4 种方法；第 3 步的思想是核心，在大函数里专门定义一个用于返回的函数（对象），由于存在闭包，这个对象的函数可以访问到大函数里所有的数值和方法，可以访问等价于继承了这些数值和方法。』

```js
var constructor = function (spec, my) {
var that, other private instance variables;

my = my || {};
Add shared variables and functions to my

that = a new object;
Add privileged methods to that

return that;

};
```

The spec object contains all of the information that the constructor needs to make an instance. The contents of the spec could be copied into private variables or transformed by other functions. Or the methods can access information from spec as they need it. (A simplification is to replace spec with a single value. This is useful when the object being constructed does not need a whole spec object.) The my object is a container of secrets that are shared by the constructors in the inheritance chain. The use of the my object is optional. If a my object is not passed in, then a my object is made.

Next, declare the private instance variables and private methods for the object. This is done by simply declaring variables. The variables and inner functions of the constructor become the private members of the instance. The inner functions have access to spec and my and that and the private variables. Next, add the shared secrets to the my object. This is done by assignment: 

```js
my.member = value;
```

Now, we make a new object and assign it to that. There are lots of ways to make a new object. We can use an object literal. We can call a pseudoclassical constructor with the new operator. We can use the Object.create method on a prototype object.

Or, we can call another functional constructor, passing it a spec object (possibly the same spec object that was passed to this constructor) and the my object. The my object allows the other constructor to share the material that we put into my. The other constructor may also put its own shared secrets into my so that our constructor can take advantage of it.

Next, we augment that, adding the privileged methods that make up the object’s interface. We can assign new functions to members of that. Or, more securely, we can define the functions first as private methods, and then assign them to that: 

```js
var methodical = function ( ) {
...
};
that.methodical = methodical;
```

The advantage to defining methodical in two steps is that if other methods want to call methodical, they can call methodical() instead of that.methodical(). If the instance is damaged or tampered with so that that.methodical is replaced, the methods that call methodical will continue to work the same because their private methodical is not affected by modification of the instance. Finally, we return that. 

Let’s apply this pattern to our mammal example. We don’t need my here, so we’ll just leave it out, but we will use a spec object. The name and saying properties are now completely private. They are accessible only via the privileged get_name and says methods:

spec 对象包含构造器需要构造一个新实例的所有信息。spec 的内容可能会被复制到私有变量中，或者被其他函数改变，或者方法可以在需要的时候访问 spec 的信息。（一个简化的方式是替换 spec 为一个单一的值。当构造对象过程中并不需要整个 spec 对象的时候，这是有用的。）my 对象是一个为继承链中的构造器提供秘密共享的容器。my 对象可以选择性地使用。如果没有传入一个 my 对象，那么会创建一个 my 对象。

接下来，声明该对象私有的实例变量和方法。通过简单地声明变量就可以做到。构造器的变量和内部函数变成了该实例的私有成员。内部函数可以访问 spec、my、that，以及其他私有变量。接下来，给 my 对象添加共享的秘密成员。这是通过赋值语句来实现的。

现在，我们构造了一个新对象并把它赋值给 that。有很多方式可以构造一个新对象。我们可以使用对象字面量，可以用 new 运算符调用一个伪类构造器，可以在一个原型对象上使 Object.create 方法，或者可以调用另一个函数化的构造器，传给它一个 spec 对象（可能就是传递给当前构造器的同一个 spec 对象）和 my 对象。my 对象允许其他的构造器分享我们放到 my 中的资料。其他构造器可能也会把自己可分享的秘密成员放进 my 对象里以便我们的构造器可以利用它。接下来，我们扩充 that，加入组成该对象接口的特权方法。我们可以分配一个新函数成为 that 的成员方法。或者，更安全地，我们可以先把函数定义为私有方法，然后再把它们配给 that。

分两步去定义 methodical 的好处是，如果其他方法想要调用 methodical，它们可以直接调用 methodical() 而不是 that.methodical()。如果该实例被破坏或纂改，甚至 that.methodical 被替换掉了，调用 methodical 的方法同样会继续工作，因为它们私有的 methodical 不受该实例被修改的影响。最后，我们返回 that。

让我们把这个模式应用到 mammal 例子里。此处不需要 my，所以我们先地开它，但会使用一个 spec 对象。name 和 saying 属性现在是完全私有的。只有通过 get_name 和 says 两个特权方法才可以访问它们。

```js
var mammal = function (spec) {
var that = {};
that.get_name = function ( ) {
    return spec.name;
};
that.says = function ( ) {
    return spec.saying || '';
};
return that;
};

var myMammal = mammal({name: 'Herb'});
```

In the pseudoclassical pattern, the Cat constructor function had to duplicate work that was done by the Mammal constructor. That isn’t necessary in the functional pattern because the Cat constructor will call the Mammal constructor, letting Mammal do most of the work of object creation, so Cat only has to concern itself with the differences: 

在伪类模式里，构造器函数 cat 不得不重复构造器 Mammal 已经完成的工作。在函数化模式中那不再需要了，因为构造器 cat 将会调用构造器 Mammal，让 Mammal 去做对象创建中的大部分工作，所以 cat 只需关注自身的差异即可。

```js
var cat = function (spec) {
    spec.saying = spec.saying || 'meow';
    var that = mammal(spec);
    that.purr = function (n) {
        var i, s = '';
        for (i = 0; i < n; i += 1) {
            if (s) {
                s += '-';
            }
            s += 'r';
        }
        return s;
    };
    that.get_name = function () {
        return that.says( ) + ' ' + spec.name + ' ' + that.says( );
    };
    return that;
};

var myCat = cat({name: 'Henrietta'});
```

1『从这里开始，下面的代码还是没有吃透。（2020-05-31）』

The functional pattern also gives us a way to deal with super methods. We will make a superior method that takes a method name and returns a function that invokes that method. The function will invoke the original method even if the property is changed:

我们会构造一个 superior 方法，它取得一个方法名并返回调用那个方法的函数。该函数会调用原来的方法，尽管属性已经变化了。

```js
Object.method('superior', function (name) {
var that = this,
method = that[name];
return function ( ) {
    return method.apply(that, arguments);
};
});
```

Let’s try it out on a coolcat that is just like cat except it has a cooler get\_name method that calls the super method. It requires just a little bit of preparation. We will declare a super\_get\_name variable and assign it the result of invoking the superior method:

```js
var coolcat = function (spec) {
    var that = cat(spec),
    super_get_name = that.superior('get_name');
    that.get_name = function (n) {
        return 'like ' + super_get_name( ) + ' baby';
    };
    return that;
};

var myCoolCat = coolcat({name: 'Bix'});
var name = myCoolCat.get_name( );
// 'like meow Bix meow baby'
```

The functional pattern has a great deal of flexibility. It requires less effort than the pseudoclassical pattern, and gives us better encapsulation and information hiding and access to super methods. If all of the state of an object is private, then the object is tamper-proof. Properties of the object can be replaced or deleted, but the integrity of the object is not compromised. If we create an object in the functional style, and if all of the methods of the object make no use of this or that, then the object is durable. A durable object is simply a collection of functions that act as capabilities.

A durable object cannot be compromised. Access to a durable object does not give an attacker the ability to access the internal state of the object except as permitted by the methods.

函数化模式有很大的灵活性。它相比伪类模式不仅带来的工作更少，还让我们得到更好的封装和信息隐藏，以及访问父类方法的能力。如果对象的所有状态都是私有的，那么该对象就成为一个「防伪」（tamper-proof）对象。该对象的属性可以被替换或删除，但该对象的完整性不会受到损害。如果我们用函数化的样式创建一个对象，并且该对象的所有方法都不使用 this 或 that，那么该对象就是持久性（durable）的。一个持久性对象就是一个简单功能函数的集合。一个持久性的对象不会被入侵。访问一个持久性的对象时，除非有方法授权，否则攻击者不能访问对象的内部状态。

### 5.5 Parts

We can compose objects out of sets of parts. For example, we can make a function that can add simple event processing features to any object. It adds an on method, a fire method, and a private event registry:

我们可以从一套部件中把对象组装出来。例如，我们可以构造一个给任何对象添加简单事件处理特性的函数。它会给对象添加一个 on 方法、一个 fire 方法和一个私有的事件注册。

```js
var eventuality = function (that) {
var registry = {};
that.fire = function (event) {
    // Fire an event on an object. The event can be either a string containing the name of the event or an
    // object containing a type property containing the name of the event. Handlers registered by the 'on'
    // method that match the event name will be invoked.
    var array,
    func,
    handler,
    i,
    type = typeof event === 'string' ?
    event : event.type;
    
    // If an array of handlers exist for this event, then loop through it and execute the handlers in order.
    if (registry.hasOwnProperty(type)) {
        array = registry[type];
        for (i = 0; i < array.length; i += 1) {
            handler = array[i];
            
            // A handler record contains a method and an optional array of parameters. If the method is a name, look
            // up the function.
            
            func = handler.method;
            if (typeof func === 'string') {
                func = this[func];
            }
            
            // Invoke a handler. If the record contained parameters, then pass them. Otherwise, pass the event object.
            func.apply(this,
            handler.parameters || [event]);
        }
    }
    return this;
};

that.on = function (type, method, parameters) {

    // Register an event. Make a handler record. Put it in a handler array, making one if it doesn't yet
    // exist for this type.
    var handler = {
        method: method,
        parameters: parameters
    };
    
    if (registry.hasOwnProperty(type)) {
        registry[type].push(handler);
        } else {
            registry[type] = [handler];
        }
        return this;
    };
    return that;
};
```

We could call eventuality on any individual object, bestowing it with event handling methods. We could also call it in a constructor function before that is returned: 

    eventuality(that);

In this way, a constructor could assemble objects from a set of parts. JavaScript’s loose typing is a big benefit here because we are not burdened with a type system that is concerned about the lineage of classes. Instead, we can focus on the character of their contents. If we wanted eventuality to have access to the object’s private state, we could pass it the my bundle.

我们可以在任何单独的对象上调用 eventuality，授予它事件处理方法。我们也可以赶在 that 被返回前在一个构造器函数中调用它；用这种方式，一个构造器函数可以从一套部件中把对象组装出来。Javascript 的弱类型在此处是一个巨大的优势，因为我们无须花费精力去了解对象在类型系统中的继承关系。相反我们只需专注于它们的个性特征。如果我们想要 eventuality 访问该对象的私有状态，可以把私有成员集 my 传递给它。
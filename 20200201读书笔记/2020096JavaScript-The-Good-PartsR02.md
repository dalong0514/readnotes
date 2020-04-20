## 05. Inheritance

Divides one thing entire to many objects; Like perspectives, which rightly gazed upon. Show nothing but confusion...

Inheritance is an important topic in most programming languages. In the classical languages (such as Java), inheritance (or extends) provides two useful services. First, it is a form of code reuse. If a new class is mostly similar to an existing class, you only have to specify the differences. Patterns of code reuse are extremely important because they have the potential to significantly reduce the cost of software development. The other benefit of classical inheritance is that it includes the specification of a system of types. This mostly frees the programmer from having to write explicit casting operations, which is a very good thing because when casting, the safety benefits of a type system are lost.

类继承的另一个好处是引入了一套类型系统的规范。由于程序员无需编写显式类型转换的代码，他们的工作量将大大减轻，这是一件很好的事情，因为类型转换会丧失类型系统在安全上的优势。

JavaScript, being a loosely typed language, never casts. The lineage of an object is irrelevant. What matters about an object is what it can do, not what it is descended from. JavaScript provides a much richer set of code reuse patterns. It can ape the classical pattern, but it also supports other patterns that are more expressive. The set of possible inheritance patterns in JavaScript is vast. In this chapter, we’ll look at a few of the most straightforward patterns. Much more complicated constructions are possible, but it is usually best to keep it simple. In classical languages, objects are instances of classes, and a class can inherit from another class. JavaScript is a prototypal language, which means that objects inherit directly from other objects.

### 01. Pseudoclassical

JavaScript is conflicted about its prototypal nature. Its prototype mechanism is obscured by some complicated syntactic business that looks vaguely classical. Instead of having objects inherit directly from other objects, an unnecessary level of indirection is inserted such that objects are produced by constructor functions.

Javascript 的原型存在着诸多矛盾。它的某些复杂的语法看起来就像那些基于类的语言，这些语法问题掩盖了它的原型机制。它不直接让对象从其他对象继承，反而插入了一个多余的间接层：通过构造器函数产生对象。

1『

作者说到点子上了，JS 放着好好的基于原型的面向对象特性不用，非要模仿基于类的面向对象，得不偿失。

基于原型的面向对象，老版可以采用下面方法实现。创建了一个空函数作为类，并把传入的原型挂在了它的 prototype，最后创建了一个它的实例，根据 new 的行为，这将产生一个以传入的第一个参数为原型的对象。这个函数无法做到与原生的 Object.create 一致，一个是不支持第二个参数，另一个是不支持 null 作为原型，所以放到今天意义已经不大了。ES6 以来，JavaScript 提供了一系列内置函数，以便更为直接地访问操纵原型。三个方法分别为：1）Object.create 根据指定的原型创建新对象，原型可以是 null；2）Object.getPrototypeOf 获得一个对象的原型；3）Object.setPrototypeOf 设置一个对象的原型。利用这三个方法，我们可以完全抛开类的思维，利用原型来实现抽象和复用。

基于类的面向对象，老版是通过插入了一个多余的间接层：通过构造器函数产生对象。这个方法很繁琐，ES6 新增了 class 语法来定义类。

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

    this.prototype = {constructor: this};

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

### 02. Object Specifiers

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

### 03. Prototypal

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

### 04. Functional

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

    my.member = value;

Now, we make a new object and assign it to that. There are lots of ways to make a new object. We can use an object literal. We can call a pseudoclassical constructor with the new operator. We can use the Object.create method on a prototype object.

Or, we can call another functional constructor, passing it a spec object (possibly the same spec object that was passed to this constructor) and the my object. The my object allows the other constructor to share the material that we put into my. The other constructor may also put its own shared secrets into my so that our constructor can take advantage of it.

Next, we augment that, adding the privileged methods that make up the object’s interface. We can assign new functions to members of that. Or, more securely, we can define the functions first as private methods, and then assign them to that: 

```js
var methodical = function ( ) {
...
};
that.methodical = methodical;
```

The advantage to defining methodical in two steps is that if other methods want to call methodical, they can call methodical( ) instead of that.methodical( ). If the instance is damaged or tampered with so that that.methodical is replaced, the methods that call methodical will continue to work the same because their private methodical is not affected by modification of the instance. Finally, we return that. 

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
that.get_name = function ( ) {
    return that.says( ) + ' ' + spec.name + ' ' + that.says( );
    return that;
};

var myCat = cat({name: 'Henrietta'});
```

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

### 05. Parts

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

## 06. Arrays

An array is a linear allocation of memory in which elements are accessed by integers that are used to compute offsets. Arrays can be very fast data structures. Unfortunately, JavaScript does not have anything like this kind of array. Instead, JavaScript provides an object that has some array-like characteristics. It converts array subscripts into strings that are used to make properties. It is significantly slower than a real array, but it can be more convenient to use. Retrieval and updating of properties work the same as with objects, except that there is a special trick with integer property names. Arrays have their own literal format. Arrays also have a much more useful set of built-in methods, described in Chapter 8.

数知是一段线性分配的内存，它通过整数计算偏移并访问其中的元素。数组是一种性能出色的数据结构。不幸的是，Javascript 没有像此类数组一样的数据结构。作为替代，Javascript 提供了一种拥有一些类数组（aray-like）特性的对象。它把数组的下标转变成字符串，用其作为属性。它明显地比一个真正的数组慢，但它使用起来更方便。它的属性的检索和更新的方式与对象一模一样，只不过多一个可以用整数作为属性名的特性。数组有自己的字面量格式。数组也有一套非常有用的内置方法。

### 01. Array Literals

Array literals provide a very convenient notation for creating new array values. An array literal is a pair of square brackets surrounding zero or more values separated by commas. An array literal can appear anywhere an expression can appear. The first value will get the property name '0', the second value will get the property name '1', and so on:

```js
var empty = [];
var numbers = [
    'zero', 'one', 'two', 'three', 'four',
    'five', 'six', 'seven', 'eight', 'nine'
];

empty[1] // undefined
numbers[1] // 'one'
empty.length // 0
numbers.length // 10
```

The object literal:

```js
var numbers_object = {
    '0': 'zero', '1': 'one', '2': 'two',
    '3': 'three', '4': 'four', '5': 'five',
    '6': 'six', '7': 'seven', '8': 'eight',
    '9': 'nine'
};
```

produces a similar result. Both numbers and number\_object are objects containing 10 properties, and those properties have exactly the same names and values. But there are also significant differences. numbers inherits from Array.prototype, whereas number\_object inherits from Object.prototype, so numbers inherits a larger set of useful methods. Also, numbers gets the mysterious length property, while number\_object does not. In most languages, the elements of an array are all required to be of the same type. JavaScript allows an array to contain any mixture of values: 

```js
var misc = [
    'string', 98.6, true, false, null, undefined,
    ['nested', 'array'], {object: true}, NaN,
    Infinity
];

misc.length // 10
```

1『 JS 里数组的各个元素可以是不同的类型，这个是「对象模拟数组」的一个体现。』

### 02. Length

Every array has a length property. Unlike most other languages, JavaScript’s array length is not an upper bound. If you store an element with a subscript that is greater than or equal to the current length, the length will increase to contain the new element. There is no array bounds error. The length property is the largest integer property name in the array plus one. This is not necessarily the number of properties in the array: 

1『 JS 的数组长度没上限，可以自动增加长度。注意：数组的长度跟其元素里的整数属性名挂钩，印象中 php 的数组也是，待验证。』

```js
var myArray = [];
myArray.length // 0
myArray[1000000] = true;
myArray.length // 1000001
// myArray contains one property.
```

The [] postfix subscript operator converts its expression to a string using the expression’s toString method if it has one. That string will be used as the property name. If the string looks like a positive integer that is greater than or equal to the array’s current length and is less than 4,294,967,295, then the length of the array is set to the new subscript plus one.

The length can be set explicitly. Making the length larger does not allocate more space for the array. Making the length smaller will cause all properties with a subscript that is greater than or equal to the new length to be deleted: 

 [] 后置下标运算符把它所含的表达式转换成一个字符串，如果该表达式有 tostring 方法就使用该方法的值。这个字符串将被用做属性名。如果这个字符串看起来像一个大于等于这个数组当前的  length 且小于 4294967295 的正整数，那么这个数组的 length 就会被重新设置为新的下标加 1。

```js
numbers.length = 3;
// numbers is ['zero', 'one', 'two']
```

A new element can be appended to the end of an array by assigning to the array’s current length:

```
numbers[numbers.length] = 'shi';
// numbers is ['zero', 'one', 'two', 'shi']
```

It is sometimes more convenient to use the push method to accomplish the same thing:

```
numbers.push('go');
// numbers is ['zero', 'one', 'two', 'shi', 'go']
```

### 03. Delete

Since JavaScript’s arrays are really objects, the delete operator can be used to remove elements from an array:

```
delete numbers[2];
// numbers is ['zero', 'one', undefined, 'shi', 'go']
```

Unfortunately, that leaves a hole in the array. This is because the elements to the right of the deleted element retain their original names. What you usually want is to decrement the names of each of the elements to the right.

1『超级不建议用这种方式直接删数组里的元素。』

Fortunately, JavaScript arrays have a splice method. It can do surgery on an array, deleting some number of elements and replacing them with other elements. The first argument is an ordinal in the array. The second argument is the number of elements to delete. Any additional arguments get inserted into the array at that point: 

这是因为排在被删除元素之后的元素保留着它们最初的属性。而你通常想要的是递减后面每个元素的属性。幸运的是，Javascript 数组有一个 splice 方法。它可以对数组做个手术，删除一些元素并将它们替换为其他的元素。第 1 个参数是数组中的一个序号，第 2 个参数是要刑除的元素个数。任何额外的参数会在序号那个点的位置被插入到数组中。

```js
numbers.splice(2, 1);
// numbers is ['zero', 'one', 'shi', 'go']
```

The property whose value is 'shi' has its key changed from '4' to '3'. Because every property after the deleted property must be removed and reinserted with a new key, this might not go quickly for large arrays.

### 04. Enumeration

Since JavaScript’s arrays are really objects, the for in statement can be used to iterate over all of the properties of an array. Unfortunately, for in makes no guarantee about the order of the properties, and most array applications expect the elements to be produced in numerical order. Also, there is still the problem with unexpected properties being dredged up from the prototype chain.

遗憾的是，for in 无法保证属性的顺序，而大多数要遍历数组的场合都期望按照阿拉伯数字顺序来产生元素。此外，可能从原型链中得到意外属性的问题依旧存在。

Fortunately, the conventional for statement avoids these problems. JavaScript’s for statement is similar to that in most C-like languages. It is controlled by three clauses—the first initializes the loop, the second is the while condition, and the third does the increment:

```js
var i;
for (i = 0; i < myArray.length; i += 1) {
    document.writeln(myArray[i]);
}
```

### 05. Confusion

A common error in JavaScript programs is to use an object when an array is required or an array when an object is required. The rule is simple: when the property names are small sequential integers, you should use an array. Otherwise, use an object. JavaScript itself is confused about the difference between arrays and objects. The typeof operator reports that the type of an array is 'object', which isn’t very helpful. JavaScript does not have a good mechanism for distinguishing between arrays and objects. We can work around that deficiency by defining our own is\_array function: 

```js
var is_array = function (value) {
    return value &&
        typeof value === 'object' &&
        value.constructor === Array;
};
```

Unfortunately, it fails to identify arrays that were constructed in a different window or frame. If we want to accurately detect those foreign arrays, we have to work a little harder:

```js
var is_array = function (value) {
    return value &&
    typeof value === 'object' &&
    typeof value.length === 'number' &&
    typeof value.splice === 'function' &&
    !(value.propertyIsEnumerable('length'));
};
```

First, we ask if the value is truthy. We do this to reject null and other falsy values. Second, we ask if the typeof value is 'object'. This will be true for objects, arrays, and (weirdly) null. Third, we ask if the value has a length property that is a number. This will always be true for arrays, but usually not for objects. Fourth, we ask if the value contains a splice method. This again will be true for all arrays. Finally, we ask if the length property is enumerable (will length be produced by a for in loop?). That will be false for all arrays. This is the most reliable test for arrayness that I have found. It is unfortunate that it is so complicated.

Having such a test, it is possible to write functions that do one thing when passed a single value and lots of things when passed an array of values.

1『

中文版里给的判断方法不同：

```js
var is_array = function() {
    return Object,prototype.toString.apply(value) === '[object Arrary]';
};
```

』

### 06. Methods

JavaScript provides a set of methods for acting on arrays. The methods are functions stored in Array.prototype. In Chapter 3, we saw that Object.prototype can be augmented. Array.prototype can be augmented as well. For example, suppose we want to add an array method that will allow us to do computation on an array:

```js
Array.method('reduce', function (f, value) {
    var i;
    for (i = 0; i < this.length; i += 1) {
        value = f(this[i], value);
    }
    return value;
});
```

By adding a function to Array.prototype, every array inherits the method. In this case, we defined a reduce method that takes a function and a starting value. For each element of the array, it calls the function with an element and the value, and computes a new value. When it is finished, it returns the value. If we pass in a function that adds two numbers, it computes the sum. If we pass in a function that multiplies two numbers, it computes the product:

```js
// Create an array of numbers.
var data = [4, 8, 15, 16, 23, 42];

// Define two simple functions. One will add two
// numbers. The other will multiply two numbers.
var add = function (a, b) {
    return a + b;
};

var mult = function (a, b) {
    return a * b;
};

// Invoke the data's reduce method, passing in the add function.
var sum = data.reduce(add, 0); // sum is 108

// Invoke the reduce method again, this time passing in the multiply function.
var product = data.reduce(mult, 1); // product is 7418880
```

Because an array is really an object, we can add methods directly to an individual array:

```js
// Give the data array a total function.

data.total = function ( ) {
    return this.reduce(add, 0);
};
total = data.total( ); // total is 108
```

Since the string 'total' is not an integer, adding a total property to an array does not change its length. Arrays are most useful when the property names are integers, but they are still objects, and objects can accept any string as a property name. It is not useful to use the Object.create method from Chapter 3 on arrays because it produces an object, not an array. The object produced will inherit the array’s values and methods, but it will not have the special length property.

### 07. Dimensions

JavaScript arrays usually are not initialized. If you ask for a new array with [], it will be empty. If you access a missing element, you will get the undefined value. If you are aware of that, or if you will naturally set every element before you attempt to retrieve it, then all is well. But if you are implementing algorithms that assume that every element starts with a known value (such as 0), then you must prep the array yourself. JavaScript should have provided some form of an Array.dim method to do this, but we can easily correct this oversight:

```js
Array.dim = function (dimension, initial) {
    var a = [], i;
    for (i = 0; i < dimension; i += 1) {
        a[i] = initial;
    }
    return a;
};

// Make an array containing 10 zeros.
var myArray = Array.dim(10, 0);
```

JavaScript does not have arrays of more than one dimension, but like most C languages, it can have arrays of arrays:

```js
var matrix = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8]
];

matrix[2][1] // 7
```

To make a two-dimensional array or an array of arrays, you must build the arrays yourself:

```js
for (i = 0; i < n; i += 1) {
    my_array[i] = [];
}
// Note: Array.dim(n, []) will not work here.
// Each element would get a reference to the same
// array, which would be very bad.
```

The cells of an empty matrix will initially have the value undefined. If youwant them to have a different initial value, you must explicitly set them. Again, JavaScript should have provided better support for matrixes. We can correct that, too: 

```js
Array.matrix = function (m, n, initial) {
    var a, i, j, mat = [];
    for (i = 0; i < m; i += 1) {
        a = [];
    for (j = 0; j < n; j += 1) {
        a[j] = initial;
    }
    mat[i] = a;
    }
    return mat;
};

// Make a 4 * 4 matrix filled with zeros.
var myMatrix = Array.matrix(4, 4, 0);
document.writeln(myMatrix[3][3]); // 0

// Method to make an identity matrix.
Array.identity = function (n) {
    var i, mat = Array.matrix(n, n, 0);
    for (i = 0; i < n; i += 1) {
        mat[i][i] = 1;
    }
    return mat;
};
myMatrix = Array.identity(4);
document.writeln(myMatrix[3][3]); // 1
```

## 07. Regular Expressions

Many of JavaScript’s features were borrowed from other languages. The syntax came from Java, functions came from Scheme, and prototypal inheritance came from Self. JavaScript’s Regular Expression feature was borrowed from Perl.

A regular expression is the specification of the syntax of a simple language. Regular expressions are used with methods to search, replace, and extract information from strings. The methods that work with regular expressions are regexp.exec, regexp.test, string.match, string.replace, string.search, and string.split. These will all be described in Chapter 8. Regular expressions usually have a significant performance advantage over equivalent string operations in JavaScript.

Regular expressions came from the mathematical study of formal languages. Ken Thompson adapted Stephen Kleene’s theoretical work on type-3 languages into a practical pattern matcher that could be embedded in tools such as text editors and programming languages.

The syntax of regular expressions in JavaScript conforms closely to the original formulations from Bell Labs, with some reinterpretation and extension adopted from Perl. The rules for writing regular expressions can be surprisingly complex because they interpret characters in some positions as operators, and in slightly different positions as literals. Worse than being hard to write, this makes regular expressions hard to read and dangerous to modify. It is necessary to have a fairly complete understanding of the full complexity of regular expressions to correctly read them.

To mitigate this, I have simplified the rules a little. As presented here, regular expressions will be slightly less terse, but they will also be slightly easier to use correctly. And that is a good thing because regular expressions can be very difficult to maintain and debug.

Today’s regular expressions are not strictly regular, but they can be very useful. Regular expressions tend to be extremely terse, even cryptic. They are easy to use in their simplest form, but they can quickly become bewildering. JavaScript’s regular expressions are difficult to read in part because they do not allow comments or whitespace.

正则表达式起源于对形式语言（formal language）的数学研究。Ken Thompson 基于 Stephen Kleene 对 type-3 语言的理论研究写出了一个切实可用的模式匹配器，它能够被嵌入到编程语言和像文本编辑器这样的工具中。在 Javascript 中，正则表达式的语法是对 Perl 版本的改进和发展，它非常接近于贝尔实验室（Bell Labs）最初提出的构想。正则表达式的书写规则出奇地复杂，在某些位置上的字符串可能解析为运算符，而仅在位置上稍微不同的相同字符串却可能被当做字面量。比不易书写更糟糕的是，这使得正则表达式不仅难以阅读，而且修改时充满危险。要想正确地阅读它们，就必须对正则表达式的整个复杂性有相当透彻的理解。为了缓解这个问题，我对它的规则进行了些许简化。这里所展示的正则表达式可能稍微有些不够简洁，但使用它们的时候不会那么容易出错。这是值得的，因为维护和调试正则表达式可能非常困难。

All of the parts of a regular expression are pushed tightly together, making them almost indecipherable. This is a particular concern when they are used in security applications for scanning and validation. If you cannot read and understand a regular expression, how can you have confidence that it will work correctly for all inputs? Yet, despite their obvious drawbacks, regular expressions are widely used.

3『Scheme，一种多范型的蝙程语言，它是两种 Iisp 主要的方言之一。而 Iisp（全名 LISt Processor，即链表处理语言）是由约输·麦卡锡在 1960 年左右创造的一种基于 lambda 演算的函数式编程语言；Self 语言，是一种基于原型的面向对象程序设计语言，于 1986 年由范乐帕洛阿尔托研究中心的 David Ungar 和 Randy Smith 给出了最初的设计；在数学、逻辑和计算机科学中，形式语言是用精确的数学或机器可处理的公式定义的语言。』

### 01. An Example

Here is an example. It is a regular expression that matches URLs. The pages of this book are not infinitely wide, so I broke it into two lines. In a JavaScript program, the regular expression must be on a single line. Whitespace is significant: 

Let’s call parse_url’s exec method. If it successfully matches the string that we pass it, it will return an array containing pieces extracted from the url: 

```js
var parse_url = /^(?:([A-Za-z]+):)?(\/{0,3})([0-9.\-A-Za-z]+) (?::(\d+))?(?:\/([^?#]*))?(?:\?([^#]*))?(?:#(.*))?$/;
var url = "http://www.ora.com:80/goodparts?q#fragment"; 
var result = parse_url.exec(url);

var names = ['url', 'scheme', 'slash', 'host', 'port', 'path', 'query', 'hash'];
var blanks = ' ';
var i;
for (i = 0; i < names.length; i += 1) {
    document.writeln(names[i] + ':' +
    blanks.substring(names[i].length), result[i]);
}
```

This produces:

```js
url: http://www.ora.com:80/goodparts?q#fragment
scheme: http
slash: //
host: www.ora.com
port: 80
path: goodparts
query: q
hash: fragment
```

In Chapter 2, we used railroad diagrams to describe the JavaScript language. We can also use them to describe the languages defined by regular expressions. That may make it easier to see what a regular expression does. This is a railroad diagram for parse_url.

Regular expressions cannot be broken into smaller pieces the way that functions can, so the track representing parse_url is a long one.

Let’s factor parse_url into its parts to see how it works:

    ^

The ^ character indicates the beginning of the string. It is an anchor that prevents exec from skipping over a non-URL-like prefix:

    (?:([A-Za-z]+):)?

This factor matches a scheme name, but only if it is followed by a : (colon). The (?:...) indicates a noncapturing group. The suffix ? indicates that the group is optional.

1『这里的扩展表示法「?:」表示非捕获型分组，即匹配返回的对象不会供后续使用；The suffix ? indicates that the group is optional. 末尾的 ? 表示可选，其原意是匹配 0 次或 1 次。』

It means repeat zero or one time. The (...) indicates a capturing group. A capturing group copies the text it matches and places it in the result array. Each capturing group is given a number. This first capturing group is 1, so a copy of the text matched by this capturing group will appear in result[1]. The [...] indicates a character class. This character class, A-Za-z, contains 26 uppercase letters and 26 lowercase letters. The hyphens indicate ranges, from A to Z. The suffix + indicates that the character class will be matched one or more times. The group is followed by the : character, which will be matched literally:

这个因子匹配一个协议名，但仅当它后面限随一个：（冒号）的时候才匹配。（？表示一个非捕获型分组（noncapturing group）。后缀 ？表示这个分组是可选的。它表示重复 0 次或 1 次表示一个捕获型分组（capturing group）。一个捕获型分组会复制它所匹配的文本，并把其放到 result 数组里。每个捕获型分组都会被指定一个编号。第一个捕获型分组的编号是 1，所以该分组所匹配的文本副本会出现在 result [1] 表示一个字符类。A-Za-z 这个字符类包含 26 个大写字母和 26 个小写字母。连字符（-）表示范围从 A 到 Z。后级 + 表示这个字符类会被匹配一次或多次。这个组后面跟着字符：，它会按字面进行匹配。

3『扩展表示法，它们是以问号开始（?…）。 它们通常用于在判断匹配之前提供标记，实现一个前视（或者后视）匹配，或者条件检查。尽管圆括号使用这些符号，但是只有（?P\<name>）表述一个分组匹配。所有其他的都没有创建一个分组。然而，你仍然需要知道它们是什么，因为它们可能最适合用于你所需要完成的任务。「2019082Core-PythonR00.md」』

    (\/{0,3})

The next factor is capturing group 2. \/ indicates that a / (slash) character should be matched. It is escaped with \ (backslash) so that it is not misinterpreted as the end of the regular expression literal. The suffix {0,3} indicates that the / will be matched 0 or 1 or 2 or 3 times:

    ([0-9.\-A-Za-z]+)

1『「-」连号也需要用转义字符来实现。』

The next factor is capturing group 3. It will match a host name, which is made up of one or more digits, letters, or . or –. The – was escaped as \- to prevent it from being confused with a range hyphen:

    (?::(\d+))?

The next factor optionally matches a port number, which is a sequence of one or more digits preceded by a :. \d represents a digit character. The series of one or more digits will be capturing group 4:

    (?:\/([^?#]*))?

We have another optional group. This one begins with a /. The character class [^?#] begins with a ^, which indicates that the class includes all characters except ? and #. The * indicates that the character class is matched zero or more times.

Note that I am being sloppy here. The class of all characters except ? and # includes line-ending characters, control characters, and lots of other characters that really shouldn’t be matched here. Most of the time this will do want we want, but there is a risk that some bad text could slip through. Sloppy regular expressions are a popular source of security exploits. It is a lot easier to write sloppy regular expressions than rigorous regular expressions:

    (?:\?([^#]*))?

Next, we have an optional group that begins with a ?. It contains capturing group 6, which contains zero or more characters that are not #: 

    (?:#(.*))?

We have a final optional group that begins with #. The . will match any character except a line-ending character:

    $

The \$ represents the end of the string. It assures us that there was no extra material after the end of the URL.

Those are the factors of the regular expression parse_url.

It is possible to make regular expressions that are more complex than parse_url, bu t I wouldn’t recommend it. Regular expressions are best when they are short and simple. Only then can we have confidence that they are working correctly and that they could be successfully modified if necessary.

There is a very high degree of compatibility between JavaScript language processors.

The part of the language that is least portable is the implementation of regular expressions. Regular expressions that are very complicated or convoluted are more likely to have portability problems. Nested regular expressions can also suffer horrible performance problems in some implementations. Simplicity is the best strategy.

Javascript 的语言处理程序之间兼容性非常高。这门语言中最没有移植性的部分就是对正则表达式的实现。结构复杂或令人费解的正则表达式很有可能导致移植性问题。在执行某些匹配时，嵌套的正则表达式也能导致极恶劣的性能问题。因此简单是最好的策略。

Let’s look at another example: a regular expression that matches numbers. Numbers can have an integer part with an optional minus sign, an optional fractional part, and an optional exponent part:

```js
var parse_number = /^-?\d+(?:\.\d*)?(?:e[+\-]?\d+)?$/i; 
var test = function (num) {
    document.writeln(parse_number.test(num));
};

test('1'); // true
test('number'); // false
test('98.6'); // true
test('132.21.86.100'); // false
test('123.45E-67'); // true
test('123.45D-67'); // false
```

parse_number successfully identified the strings that conformed to our specification and those that did not, but for those that did not, it gives us no information on why or where they failed the number test. Let’s break down parse\_number:

    /^ $/i

We again use ^ and \$ to anchor the regular expression. This causes all of the characters in the text to be matched against the regular expression. If we had omitted the anchors, the regular expression would tell us if a string contains a number. With the anchors, it tells us if the string contains only a number. If we included just the ^, it would match strings starting with a number. If we included just the \$, it would match strings ending with a number.

『我们又用 ^ 和 \$ 来框定这个正则表达式。它指引这个正则表达式对文本中的所有字符都进行匹配。如果我们省略了这些标识，那么只要一个字符串包含一个数字，这个正则表达式就会进行匹配。但有了这些标识，只有当一个字符串的内容仅为一个数字时，它才会告诉我们。如果我们仅包含 ^，它将匹配以一个数字开头的字符串。如果我们仅包含 \$，则匹配以个数字结尾的字符串。』

1『指定起始很重要，做匹配的时候要养成习惯。但在做替换的时候应该是不需要的。（2020-03-29）』

The i flag causes case to be ignored when matching letters. The only letter in our pattern is e. We want that e to also match E. We could have written the e factor as [Ee] or (?:E|e), but we didn’t have to because we used the i flag:

『 i 标识表示匹配字母时忽略大小写。在我们的模式中唯一可能出现的字母是 e。我们希望既能匹配 e，也能匹配 E。我们可以把 e 因子写成 [Ee] 或 (?:E|e)，但不必这么麻烦，因为我们使用了标识符 i。』

    -?

The ? suffix on the minus sign indicates that the minus sign is optional:

    \d+

\d means the same as [0-9]. It matches a digit. The + suffix causes it to match one or more digits:

    (?:\.\d*)?

The (?:...)? indicates an optional noncapturing group. It is usually better to use noncapturing groups instead of the less ugly capturing groups because capturing has a performance penalty. The group will match a decimal point followed by zero or more digits:

1『通常用非捕获型分组来替代少量不优美获型分组是很好的方法，因为捕获会有性能上的损失。』

    (?:e[+\-]?\d+)?

This is another optional noncapturing group. It matches e (or E), an optional sign, and one or more digits.

### 02. Construction

There are two ways to make a RegExp object. The preferred way, as we saw in the examples, is to use a regular expression literal. Regular expression literals are enclosed in slashes. This can be a little tricky because slash is also used as the division operator and in comments. There are three flags that can be set on a RegExp. They are indicated by the letters g, i, and m, as listed in Table 7-1. The flags are appended directly to the end of the RegExp literal:

```js
// Make a regular expression object that matches
// a JavaScript string.
var my_regexp = /"(?:\\.|[^\\\"])*"/g;
```

1) g, Global (match multiple times; the precise meaning of this varies with the method). 2) i, Insensitive (ignore character case). 3) m, Multiline (^ and \$ can match line-ending characters).

The other way to make a regular expression is to use the RegExp constructor. The constructor takes a string and compiles it into a RegExp object. Some care must be taken in building the string because backslashes have a somewhat different meaning in regular expressions than in string literals. It is usually necessary to double the backslashes and escape the quotes:

创建这个字符串时请多加小心，因为反斜杠在正则表达式和在字符串字面量中有一些不同的含义。通常需要双写反斜杠，以及对引号进行转义。

```js
// Make a regular expression object that matches
// a JavaScript string.

var my_regexp = new RegExp("\"(?:\\.|[^\\\\\\\"])*\"", 'g'); 
```

The second parameter is a string specifying the flags. The RegExp constructor is useful when a regular expression must be generated at runtime using material that is not available to the programmer. RegExp objects contain the properties listed in Table 7-2.

Table 7-2. Properties of RegExp objects (Property | Use). 1) global. true if the g flag was used. 2) ignoreCase. true if the i flag was used. 3) lastIndex. The index at which to start the next exec match. Initially it is zero. 4) multiline. true if the m flag was used. 5) source. The source text of the regular expression.

RegExp objects made by regular expression literals share a single instance: 

```js
function make\_a\_matcher( ) {
    return /a/gi;
}

var x = make_a_matcher( );
var y = make_a_matcher( );

// Beware: x and y are the same object!
x.lastIndex = 10;
document.writeln(y.lastIndex); // 10
```

### 03. Elements

Let’s look more closely at the elements that make up regular expressions.

1『正则表达式里的元素，这个概念加进自学正则表达式的知识框架内，目前的体系里有正则的结构、元素。』

#### 1. Regexp Choice

A regexp choice contains one or more regexp sequences. The sequences are separated by the | (vertical bar) character. The choice matches if any of the sequences match. It attempts to match each of the sequences in order. So:

    "into".match(/in|int/)

matches the in in into. It wouldn’t match int because the match of in was successful.

#### 2. Regexp Sequence

A regexp sequence contains one or more regexp factors. Each factor can optionally be followed by a quantifier that determines how many times the factor is allowed to appear. If there is no quantifier, then the factor will be matched one time.

#### 3. Regexp Factor

A regexp factor can be a character, a parenthesized group, a character class, or an escape sequence. All characters are treated literally except for the control characters and the special characters:

    \ / [ ] ( ) { } ? + * | . ^ $

1『正则里的特殊字符就上面的几个，牢记哦。』

which must be escaped with a \ prefix if they are to be matched literally. When in doubt, any special character can be given a \ prefix to make it literal. The \ prefix does not make letters or digits literal.

An unescaped . matches any character except a line-ending character. An unescaped ^ matches the beginning of the text when the lastIndex property is zero. It can also match line-ending characters when the m flag is specified. An unescaped \$ matches the end of the text. It can also match line-ending characters when the m flag is specified.

1『加上标识符 (?s) 的话，点号也可以匹配换行符 \n。』

当 lastindex 属性值为 0 时，一个未转义的 ^ 会匹配文本的开始。当指定了 m 标识时，它也能匹配行结束符。一个未转义的 \$ 将匹配文本的结束。当指定了 m 标识时，它也能匹配行结束符。

#### 4. Regexp Escape

The backslash character indicates escapement in regexp factors as well as in strings, but in regexp factors, it works a little differently.

As in strings, \f is the formfeed character, \n is the newline character, \r is the carriage return character, \t is the tab character, and \u allows for specifying a Unicode character as a 16-bit hex constant. In regexp factors, \b is not the backspace character. \d is the same as [0-9]. It matches a digit. \D is the opposite: [^0-9]. 

\s is the same as [\f\n\r\t\u000B\u0020\u00A0\u2028\u2029]. This is a partial set of Unicode whitespace characters. \S is the opposite: [^\f\n\r\t\u000B\u0020\u00A0\u2028\ u2029].

\w is the same as [0-9A-Z_a-z]. \W is the opposite: [^0-9A-Z_a-z]. This is supposed to represent the characters that appear in words. Unfortunately, the class it defines is useless for working with virtually any real language. If you need to match a class of letters, you must specify your own class.

像在字符串中一样，\f 是换页符，\n 是换行符，\r 是回车符，\t 是制表（tab）符，并且\ u 允许指定一个 Unicode 字符来表示一个十六进制的常量。但在正则表达式因子中，\b 不是退格（backspace）符。\w 本意是希望表示出现在话语中的字符。遗憾的是，它所定义的类实际上对任何真正的语言来说都不起作用，如果你需要匹配信件一类的文本，你必须指定自己的类。

A simple letter class is [A-Za-z\u00C0-\u1FFF\u2800-\uFFFD]. It includes all of Unicode’s letters, but it also includes thousands of characters that are not letters. Unicode is large and complex. An exact letter class of the Basic Multilingual Plane is possible, but would be huge and inefficient. JavaScript’s regular expressions provide extremely poor support for internationalization.

\b was intended to be a word-boundary anchor that would make it easier to match text on word boundaries. Unfortunately, it uses \w to find word boundaries, so it is completely useless for multilingual applications. This is not a good part.

\1 is a reference to the text that was captured by group 1 so that it can be matched again. For example, you could search text for duplicated words with: 

doubled_words looks for occurrences of words (strings containing 1 or more letters) followed by whitespace followed by the same word. \2 is a reference to group 2, \3 is a reference to group 3, and so on.

```js
var doubled_words =
    /[A-Za-z\u00C0-\u1FFF\u2800-\uFFFD'\-]+\s+\1/gi;
```

\b 被指定为一个字边界标识，它方便用于对文本的字边界进行匹配。遗憾的是，它使用 \w 去寻找字边界，所以它对多语言应用来说是完全无用的。这并不是个好的特性。\1 是指向分组 1 所捕获到的文本的一个引用，所以它能被再次匹配。例如，你能用下面的正则表达式来搜索文本中的重复的单词。Doubled words 会寻找重复的单词（包含一个或多个字母的字符串），该单词的后面跟着个或多个空白，然后再跟着与它相同的单词。

#### 5. Regexp Group

There are four kinds of groups:

1) Capturing. A capturing group is a regexp choice wrapped in parentheses. The characters that match the group will be captured. Every capture group is given a number. The first capturing ( in the regular expression is group 1. The second capturing ( in the regular expression is group 2.

2) Noncapturing. A noncapturing group has a (?: prefix. A noncapturing group simply matches; it does not capture the matched text. This has the advantage of slight faster performance. Noncapturing groups do not interfere with the numbering of capturing groups.

3) Positive lookahead. A positive lookahead group has a (?= prefix. It is like a noncapturing group except that after the group matches, the text is rewound to where the group started, effectively matching nothing. This is not a good part. 4) Negative lookahead. A negative lookahead group has a (?! prefix. It is like a positive lookahead group, except that it matches only if it fails to match. This is not a good part.

非捕获型分组有一个 (?: 前缀。非捕获型分组仅做简单的匹配，并不会捕获所匹配的文本。这会带来微弱的性能优势。非捕获型分组不会干扰捕获型分组的编号。向前正向匹配分组类似于非捕获型分组，但在这个组匹配后，文本会倒回到它开始的地方，实际上并不匹配任何东西。这不是一个好的特性。向前负向匹配分组类似于向前正向匹配分组，但只有当它匹配失败时它才继续向前进行匹配。这不是一个好的特性。

#### 6. Regexp Class

1『 Regexp Class 指字符集。』

A regexp class is a convenient way of specifying one of a set of characters. For example, if we wanted to match a vowel, we could write (?:a | e | i | o | u), but it is more conveniently written as the class [aeiou]. Classes provide two other conveniences. The first is that ranges of characters can be specified. So, the set of 32 ASCII special characters:

```js
! " # $ % & ' ( ) * + , - . / :
; < = > ? @ [ \ ] ^ _ ` { | } ~
```

could be written as:

    (?:!|"|#|\$|%|&|'|\(|\)|\*|\+|,|-|\.|\/|:|;|<|=|>|@|\[|\\|]|\^|_|` |\{|\||\}|~) 

but is slightly more nicely written as:

    [!-\/:-@\[-`{-~]

which includes the characters from ! through / and : through @ and [ through ànd { through ~. It is still pretty nasty looking. The other convenience is the complementing of a class. If the first character after the [ is ^, then the class excludes the specified characters. So [^!-\/:-@\[-`{-~] matches any character that is not one of the ASCII special characters.

它包括从 ！到 /、从 ：到 、从（ 到 ` 和从 [ 到 ~ 的字符。但它看起来依旧相当难以阅读。另一个方便之处是类的求反。如果 [ 后的第一个字符是 ^，那么这个类会排除这些特殊字符，所以取反的正则会匹配任何一个非 ASCI 特殊字符的字符。

#### 7. Regexp Class Escape

The rules of escapement within a character class are slightly different than those for a regexp factor. [\b] is the backspace character. Here are the special characters that should be escaped in a character class:

    - / [ \ ] ^

#### 8. Regexp Quantifier

A regexp factor may have a regexp quantifier suffix that determines how many times the factor should match. A number wrapped in curly braces means that the factor should match that many times. So, /www/ matches the same as /w{3}/. {3,6} will match 3, 4, 5, or 6 times. {3,} will match 3 or more times. ? is the same as {0,1}. * is the same as {0,}. + is the same as {1,}.

Matching tends to be greedy, matching as many repetitions as possible up to the limit, if there is one. If the quantifier has an extra ? suffix, then matching tends to be lazy, attempting to match as few repetitions as possible. It is usually best to stick with the greedy matching.

如果只有一个量词，表示趋向于进行贪梦性匹配，即匹配尽可能多的副本直至达到上限。如果这个量词附加一个后缀 ?，则表示趋向于进行非贪梦匹配，即只匹配必要的副本就好。一般情况下最好坚持使用贪婪性匹配。

## 09. Style

Here is a silly stately style indeed!

—William Shakespeare, The First Part of Henry the Sixth Computer 

programs are the most complex things that humans make. Programs are made up of a huge number of parts, expressed as functions, statements, and expressions that are arranged in sequences that must be virtually free of error. The runtime behavior has little resemblance to the program that implements it. Software is usually expected to be modified over the course of its productive life. The process of converting one correct program into a different correct program is extremely challenging.

运行时行为（runtime behavior）几乎和实现它的程序没有什么相似之处。在软件的产品生命周期中，它们通常都会被修改。把一个正确的程序转化为另一个同样正确但风格不同的程序，是一个极具挑战性的过程。

Good programs have a structure that anticipates—but is not overly burdened by—the possible modifications that will be required in the future. Good programs also have a clear presentation. If a program is expressed well, then we have the best chance of being able to understand it so that it can be successfully modified or repaired.

优秀的程序拥有一个前瞻性的结构，它会预见到在未来才可能需要的修改，但不会让其成为过度的负担。优秀的程序还会具备一种清晰的表达方式。如果一个程序被表达得很好，那么我们就能更加容易地去理解它，以便成功地改造或修补它。这些观点适用于所有的编程语言，而对 Javascript 来说尤为如此。Javascript 的弱类型和过度的容错性导致程序质量无法在编译时获得保障，所以为了弥补，我们应该按照严格的规范进行编码。

These concerns are true for all programming languages, and are especially true for JavaScript. JavaScript’s loose typing and excessive error tolerance provide little compile-time assurance of our programs’ quality, so to compensate, we should code with strict discipline.

JavaScript contains a large set of weak or problematic features that can undermine our attempts to write good programs. We should obviously avoid JavaScript’s worst features. Surprisingly, perhaps, we should also avoid the features that are often useful but occasionally hazardous. Such features are attractive nuisances, and by avoiding them, a large class of potential errors is avoided.

The long-term value of software to an organization is in direct proportion to the quality of the codebase. Over its lifetime, a program will be handled by many pairs of hands and eyes. If a program is able to clearly communicate its structure and characteristics, it is less likely to break when it is modified in the never-too-distant future.

对于一个组织机构来说，软件的长远价值和代码库的质量成正比。在程序的生命周期里，会经历很多人的测试、使用和修改。如果一个程序能很清楚地传达它的结构和特性，那么当它在井不遥远的将来被修改时，它被破坏的可能性就小很多。

JavaScript code is often sent directly to the public. It should always be of publication quality. Neatness counts. By writing in a clear and consistent style, your programs become easier to read.

Programmers can debate endlessly on what constitutes good style. Most programmers are firmly rooted in what they’re used to, such as the prevailing style where they went to school, or at their first job. Some have had profitable careers with no sense of style at all. Isn’t that proof that style doesn’t matter? And even if style doesn’t matter, isn’t one style as good as any other? It turns out that style matters in programming for the same reason that it matters in writing. It makes for better reading.

Javascript 代码经常被直接发布。它应该自始至终具备发布质量，要干净利落。通过在一个清晰且始终如一的风格下编写，你的程序会变得易于阅读。程序员会无休止地讨论良好的风格是由什么构成的。大多数程序员会坚持他们过去的应用经验，比如他们在学校或在他们第一份工作时学到的流行的风格。他们中的一些人拥有高薪的工作，但完全没有代码风格的意识。这是否证明了风格其实根本不重要？就算风格不重要，风格之间是否有优劣之分呢？事实证明代码风格在编程中是很重要的，就像文字风格对于写作很重要一样。好的风格让代码能更好地被阅读。

Computer programs are sometimes thought of as a write-only medium, so it matters little how it is written as long as it works. But it turns out that the likelihood a program will work is significantly enhanced by our ability to read it, which also increases the likelihood that it actually works as intended. It is also the nature of software to be extensively modified over its productive life. If we can read and understand it, then we can hope to modify and improve it.

电脑程序有时候被认为不是用来读的，所以只要它能工作，写成怎样是不重要的。但是结果证明，如果程序可读性强，它正常运行的可能性，以及是否准确按照我们的意图去工作的可能性也显著增强。它还决定了软件在其生命周期中能否进行扩展。如果我们能阅读并且理解程序，那么就有希望去修改和完善它。

Throughout this book I have used a consistent style. My intention was to make the code examples as easy to read as possible. I used whitespace consistently to give you more cues about the meaning of my programs.

I indented the contents of blocks and object literals four spaces. I placed a space between if and ( so that the if didn’t look like a function invocation. Only in invocations do I make ( adjacent with the preceding symbol. I put spaces around all infix operators except for . and [, which do not get spaces because they have higher precedence. I use a space after every comma and colon. I put at most one statement on a line. Multiple statements on a line can be misread.

If a statement doesn’t fit on a line, I will break it after a comma or a binary operator. That gives more protection against copy/paste errors that are masked by semicolon insertion. (The tragedy of semicolon insertion will be revealed in Appendix A.) I indent the remainder of the statement an extra four spaces, or eight spaces if four would be ambiguous (such as a line break in the condition part of an if statement). I always use blocks with structured statements such as if and while because it is less error prone. I have seen:

贯穿本书，我始终采用一致的风格。我的目的是使代码实例尽可能易于阅读。我使用一致的留白来帮助你理解我的程序的逻辑思路。我对代码块内容和对象字面量缩进 4 个空格。我放了一个空格在 if 和 ( 之间，以致 if 不会看起来像一个函数调用。只有真的是在调用时，我才使 ( 和其前面的符号相毗连。我在除了 . 和 [ 外的所有中置运算符的两边都放了空格，它们俩无须空格是因为它们有更高的优先级。我在每个逗号和冒号后面都使用一个空格。

我在每行最多放一个语句，在一行里放多条语句可能会被误读。如果一个语句一行放不下，我会在一个冒号或二元运算符后拆开它，这将更好地防止自动插入分号的机制掩盖复制 / 粘贴的错误（自动插入分号带来的悲剧会在附录 A 里披露）。我给折断后的语句的其余部分多缩进 4 个空格，如果 4 个还不够明显，就缩进 8 个空格（例如在一个 if 语句的条件部分插入一个换行符的时候）。在诸如 if 和 while 这样结构化的语句里，我始终使用代码块，因为这样会减少出错的概率。

2『上面的代码风格做一张信息卡片，进行刻意练习。』

```js
if (a)
    b( );
```

become:

```js
if (a)
    b( );
    c( );
```

which is an error that is very difficult to spot. It looks like: 

```js
if (a) {
    b( );
    c( );
}
```

but it means:

```js
if (a) {
    b( );
}
c( );
```

Code that appears to mean one thing but actually means another is likely to cause bugs. A pair of braces is really cheap protection against bugs that can be expensive to find.

看起来想要做一件事情但实际上却在做另一件事情的代码很可能导致 bug。一对花括号可以用很低廉的成本去防止那些需要昂贵的代价才能发现的 bug。

1『指上面的代码示例。』

I always use the K&R style, putting the { at the end of a line instead of the front, because it avoids a horrible design blunder in JavaScript’s return statement. I included some comments. I like to put comments in my programs to leave information that will be read at a later time by people (possibly myself) who will need to understand what I was thinking. Sometimes I think about comments as a time machine that I use to send important messages to future me. I struggle to keep comments up-to-date. Erroneous comments can make programs even harder to read and understand. I can’t afford that.

我一直使用 K&R 风格，把 { 放在一行的结尾而不是下一行的开头，因为它会避免 Javascript 的 return 语句中的一个可怕的设计错误。

2『 K&R 风格，因在 Kernighan 与 Ritchie 合著的 The C Programming Language 一书中广泛用而得名。它是最为遍的 C 语言代码风格。已下载书籍「2019045C程序设计语言2Ed | 2019045The-C-Programming-Language」。』

I tried to not waste your time with useless comments like this: 

    i = 0; // Set i to zero.

In JavaScript, I prefer to use line comments. I reserve block comments for formal documentation and for commenting out. I prefer to make the structure of my programs self-illuminating, eliminating the need for comments. I am not always successful, so while my programs are awaiting perfection, I am writing comments.

在 Javascript 里，我更喜欢用行注释。我把块注释用于正式的文档记录和注释。我更喜欢使我的程序结构能自我说明（self- illuminating），从而消除对注释的需要。我并非每次都能做到，所以只要我的程序还不尽完美，我就会编写注释。

JavaScript has C syntax, but its blocks don’t have scope. So, the convention that variables should be declared at their first use is really bad advice in JavaScript. JavaScript has function scope, but not block scope, so I declare all of my variables at the beginning of each function. JavaScript allows variables to be declared after they are used. That feels like a mistake to me, and I don’t want to write programs that look like mistakes. I want my mistakes to stand out. Similarly, I never use an assignment expression in the condition part of an if because:

    if (a = b) { ... }

is probably intended to be:

    if (a === b) { ... }

I want to avoid idioms that look like mistakes.

1『 ES6 新增的 let、const 解决了作者的难题。』

I never allow switch cases to fall through to the next case. I once found a bug in my code caused by an unintended fall through immediately after having made a vigorous speech about why fall through was sometimes useful. I was fortunate in that I was able to learn from the experience. When reviewing the features of a language, I now pay special attention to features that are sometimes useful but occasionally dangerous. Those are the worst parts because it is difficult to tell whether they are being used correctly. That is a place where bugs hide.

我绝不允许 switch 语句块中的条件穿越到下一个 case 语句。我曾经在我的代码里发现了一个无意识的「穿越」导致的 bug，而在此之前，我刚刚激情澎湃地做完一次关于如何妙用「穿越」有时很有用的演讲。我很幸运能够从这个教训中有所收获。当我现在评审一门语言的特性的时候，我把注意力放在那些有时很有用但偶尔很危险的特性上。那些是量糟的部分，因为我们很难辨别它们是否被正确使用。那是 bug 的藏身之地。

Quality was not a motivating concern in the design, implementation, or standardization of JavaScript. That puts a greater burden on the users of the language to resist the language’s weaknesses. JavaScript provides support for large programs, but it also provides forms and idioms that work against large programs. For example, JavaScript provides conveniences for the use of global variables, but global variables become increasingly problematic as programs scale in complexity.

I use a single global variable to contain an application or library. Every object has its own namespace, so it is easy to use objects to organize my code. Use of closure provides further information hiding, increasing the strength of my modules.

在 Javascript 的设计、实现和标准化的过程中，质量没有被特别关注。这给使用这门语言的用户增加了避免其缺陷的难度。Javascript 为大型程序提供了支持，但它也带有不利于大型程序的形式和习惯用法。举例来说：Javascript 可以方便地使用全局变量，但随着程序的日益复杂，全局变量逐渐变得问题重重。对一个脚本应用或工具库，我只用唯一一个全局变量。每个对象都有它自己的命名空间，所以我很容易使用对象去管理代码。使用闭包能提供进一步的信息隐藏，增强我的模块的建壮性。

3『

作者的这个思想在 YAHOO 的 Javascript 库 YUI 中得到了底的贯彻。在 YUI 中仅用到两个全局变量：YAHO 和 YAHOO_config。YUI 的一切都是基于一种模块模式来实现的。

github 上找到下面代码：[javascript 模块模式实现](https://gist.github.com/tangyangzhe/4276560)

```js
// http://dancewithnet.com/2007/12/04/a-javascript-module-pattern/
<script type="text/javascript" src="http://yui.yahooapis.com/2.2.2/build/utilities/utilities.js"></script>
<ul id="myList">
    <li class="draggable">一项</li>
    <li>二项</li>
    <li class="draggable">三项</li>
</ul>
<script>
    YAHOO.namespace("myProject");
    YAHOO.myProject.myModule = function () {
        var yue = YAHOO.util.Event,
            yud = YAHOO.util.Dom;
        //私有方法
        var getListItems = function () {
            var elList = yud.get("myList");
            var aListItems = yud.getElementsByClassName("li", elList);
            return aListItems;
        };
        //这个放回的对象将变成YAHOO.myProject.myModule:
        return {
            aDragObjects: [], //可对外访问的，存储DD对象
            init: function () {
                //直到DOM完全加载好，才实现列表项可拖拽：
                yue.onDOMReady(this.makeLIsDraggable, this, true);
            },
            makeLIsDraggable: function () {
                var aListItems = getListItems(); //我们可以拖拽的那些元素
                for (var i = 0, j = aListItems.length; i < j; i++) {
                    this.aDragObjects.push(new YAHOO.util.DD(aListItems[i]));
                }
            }
        };
    }();
    //上面的代码已经执行，所以我们能立即访问init方法：
    YAHOO.myProject.myModule.init();
</script>
```
medium 上的一篇文章：[Module Pattern in JavaScript - Level Up Coding](https://levelup.gitconnected.com/data-hiding-with-javascript-module-pattern-62b71520bddd)

』

## 10. Beautiful Features

Thus, expecting thy reply, I profane my lips on thy foot, my eyes on thy picture, and my heart on thy every part. Thine, in the dearest design of industry...

—William Shakespeare, Love’s Labor’s Lost

I was invited last year to contribute a chapter to Andy Oram’s and Greg Wilson’s Beautiful Code (O’Reilly), an anthology on the theme of beauty as expressed in computer programs. I wanted to write my chapter in JavaScript. I wanted to use it to present something abstract, powerful, and useful to show that the language was up to it. And I wanted to avoid the browser and other venues in which JavaScript is typecast. I wanted to show something respectable with some heft to it.

I immediately thought of Vaughn Pratt’s Top Down Operator Precedence parser, which I use in JSLint (see Appendix C). Parsing is an important topic in computing. The ability to write a compiler for a language in itself is still a test for the complete-ness of a language.

I wanted to include all of the code for a parser in JavaScript that parses JavaScript. But my chapter was just one of 30 or 40, so I felt constrained in the number of pages I could consume. A further complication was that most of my readers would have no experience with JavaScript, so I also would have to introduce the language and its peculiarities.

2『已下载书籍「2020119代码之美 | 2020119Beautiful-Code」；作者的文章「Top Down Operator Precedence parser」。』

So, I decided to subset the language. That way, I wouldn’t have to parse the whole language, and I wouldn’t have to describe the whole language. I called the subset Simplified JavaScript. Selecting the subset was easy: it included just the features that I needed to write a parser. This is how I described it in Beautiful Code: 

1. Simplified JavaScript is just the good stuff, including: Functions as first class objects. Functions in Simplified JavaScript are lambdas with lexical scoping.

2. Dynamic objects with prototypal inheritance Objects are class-free. We can add a new member to any object by ordinary assignment. An object can inherit members from another object.

3. Object literals and array literals. This is a very convenient notation for creating new objects and arrays. JavaScript literals were the inspiration for the JSON data interchange format.

JS 的 3 大精华：1）函数是顶级对象。在精简 Javascrip 中，函数是有词法作用域的闭包（(lambda）。2）基于原型继承的动态对象。对象是无类别的。我们可以通过普通的赋值给任何对象增加一个新成员属性。一个对象可以从另一个对象继承成员属性。3）对象字面量和数组字面量。这对创建新的对象和数组来说是一种非常方便的表示法。Javascript 字面量是数据交换格式 JSON 的灵感之源。

The subset contained the best of the Good Parts. Even though it was a small language, it was very expressive and powerful. JavaScript has lots of additional features that really don’t add very much, and as you’ll find in the appendixes that follow, it has a lot of features with negative value. There was nothing ugly or bad in the subset. All of that fell away.

Simplified JavaScript isn’t strictly a subset. I added a few new features. The simplest was adding pi as a simple constant. I did that to demonstrate a feature of the parser. I also demonstrated a better reserved word policy and showed that reserved words are unnecessary. In a function, a word cannot be used as both a variable or parameter name and a language feature. You can use a word for one or the other, and the programmer gets to choose. That makes a language easier to learn because you don’t need to be aware of features you don’t use. And it makes the language easier to extend because it isn’t necessary to reserve more words to add new features.

精简的 Javascript 不是一个严格的子集。我添加了少许新特性。最简单的是增加了 pi 作为个简单的常量。我这么做是为了证明解析器的一个特性。我也展示了一个更好的保留字策路并证明哪些保留字是多余的。在一个函数中，一个单词不能既被用做变量或参数名，又被用做一个语言特性。你可以让某个单词用在其中之一上，井允许程序员自己选择。这会使一门语言易于学习，因为你没必要知道你不会使用的特性。并且它会使这门语言易于扩展，因为它无须保留更多的保留字来增加新特性。

I also added block scope. Block scope is not a necessary feature, but not having it confuses experienced programmers. I included block scope because I anticipated that my parser would be used to parse languages that are not JavaScript, and those languages would do scoping correctly. The code I wrote for the parser is written in a style that doesn’t care if block scope is available or not. I recommend that youwrite that way, too. When I started thinking about this book, I wanted to take the subset idea further, to show how to take an existing programming language and make significant improvements to it by making no changes except to exclude the low-value features.

我也增加了块级作用域。块级作用域不是一个必需的特性，但没有它会让有经验的程序员感到困惑。包含块级作用城是因为我预期解析器可能会被用于解析非 Javascript 语言，并且那些语言能正确地界定作用域。我编写这个解析器的代码风格不关心块作用域是否可用我推荐你也采用这种方式来写。当开始构思本书的时候，我想进一步地发展这个子集，我想展示除了排除低价值特性外，如何通过不做任何改变来获得一个现有的编程语言，并且使它得到有效的改进。

We see a lot of feature-driven product design in which the cost of features is not properly accounted. Features can have a negative value to consumers because they make the products more difficult to understand and use. We are finding that people like products that just work. It turns out that designs that just work are much harder to produce than designs that assemble long lists of features.

我们看到大量的特性驱动的产品设计，其中特性的成本没有被正确计算。对于用户来说，某些特性可能有一些负面价值，因为它们使产品更加难以理解和使用。我们发现人们想要的产品其实只要能工作即可。事实证明产生恰好可以工作的设计比集合一大串特性的设计要困难得多。

Features have a specification cost, a design cost, and a development cost. There is a testing cost and a reliability cost. The more features there are, the more likely one will develop problems or will interact badly with another. In software systems, there is a storage cost, which was becoming negligible, but in mobile applications is becoming significant again. There are ascending performance costs because Moore’s Law doesn’t apply to batteries.

Features have a documentation cost. Every feature adds pages to the manual, increasing training costs. Features that offer value to a minority of users impose a cost on all users. So, in designing products and programming languages, we want to get the core features—the good parts—right because that is where we create most of the value.

特性有规定成本、设计成本和开发成本，还有测试成本和可靠性成本。特性越多，某个特性出现问题，或者和其他特性相互干扰的可能性就越大。在软件系统中，存储成本是无足轻重的，但在移动应用中，它又变得重要了。它们抬高了电池的效能成本，因为摩尔定律并不适用于电池。特性有文档成本。每个特性都会让产品指南变得更厚，从而增加了培训成本。只对少数用户有价值的特性增加了所有用户的成本。所以在设计产品和编程语言时，我们希望直接使用核心的精华部分，因为是这些精华创造了大部分的价值。

We all find the good parts in the products that we use. We value simplicity, and when simplicity isn’t offered to us, we make it ourselves. My microwave oven has tons of features, but the only ones I use are cook and the clock. And setting the clock is a struggle. We cope with the complexity of feature-driven design by finding and sticking with the good parts.

It would be nice if products and programming languages were designed to have only good parts.

在我们使用的产品中，总能找到好的部分。我们喜欢简单，追求简洁易用，但是当产品缺乏这种特性时，就要自己去创造它。微波炉有一大堆特性，但是我只会用烹调和定时，使用定时功能就足够麻烦的了。对于特性驱动型的设计，我们唯有靠找出它的精华并坚持使用，才能更好地应对其复杂性。如果产品和编程语言被设计得仅留下精华，那该有多好。

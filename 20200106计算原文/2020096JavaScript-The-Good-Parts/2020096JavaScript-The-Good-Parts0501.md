# 05 Inheritance

Divides one thing entire to many objects; 

Like perspectives, which rightly gazed upon

Show nothing but confusion...

—William Shakespeare, The Tragedy of King Richard the Second

Inheritance is an important topic in most programming languages.

In the classical languages (such as Java), inheritance (or extends) provides two useful services. First, it is a form of code reuse. If a new class is mostly similar to an existing class, you only have to specify the differences. Patterns of code reuse are extremely important because they have the potential to significantly reduce the cost of software development. The other benefit of classical inheritance is that it includes the specification of a system of types. This mostly frees the programmer from having to write explicit casting operations, which is a very good thing because when casting, the safety benefits of a type system are lost.

JavaScript, being a loosely typed language, never casts. The lineage of an object is irrelevant. What matters about an object is what it can do, not what it is descended from.

JavaScript provides a much richer set of code reuse patterns. It can ape the classical pattern, but it also supports other patterns that are more expressive. The set of possible inheritance patterns in JavaScript is vast. In this chapter, we’ll look at a few of the most straightforward patterns. Much more complicated constructions are possible, but it is usually best to keep it simple.

In classical languages, objects are instances of classes, and a class can inherit from another class. JavaScript is a prototypal language, which means that objects inherit directly from other objects.

## 01. Pseudoclassical

JavaScript is conflicted about its prototypal nature. Its prototype mechanism is obscured by some complicated syntactic business that looks vaguely classical. Instead of having objects inherit directly from other objects, an unnecessary level of indirection is inserted such that objects are produced by constructor functions.

Javascript 的原型存在着诸多矛盾。它的某些复杂的语法看起来就像那些基于类的语言，这些语法问题掩盖了它的原型机制。它不直接让对象从其他对象继承，反而插入了一个多余的间接层：通过构造器函数产生对象。

When a function object is created, the Function constructor that produces the function object runs some code like this:

    this.prototype = {constructor: this};

The new function object is given a prototype property whose value is an object containing a constructor property whose value is the new function object. The prototype object is the place where inherited traits are to be deposited. Every function gets a prototype object because the language does not provide a way of determining which functions are intended to be used as constructors. The constructor property is not useful. It is the prototype object that is important.

When a function is invoked with the constructor invocation pattern using the new prefix, this modifies the way in which the function is executed. If the new operator were a method instead of an operator, it could have been implemented like this: 

新函数对象被赋予一个 prototype 属性，它的值是一个包含 constructor 属性且属性值为该新函数的对象。这个 prototype 对象是存放继承特征的地方。因为 Javascript 语言没有提供一种方法去确定哪个函数是打算用来做构造器的，所以每个函数都会得到一个 prototype 对象。constructor 属性没什么用，重要的是 prototype 对象。当采用构造器调用模式，即用 new 前缀去调用一个函数时，函数执行的方式会被修改。如果 new 运算符是一个方法而不是一个运算符，它可能会像这样执行：

1『理清了之前的困惑，函数被创建时，最重要是其原型对象。被创建的函数会被给一个原型对象，这个原型对象里有一个构造器属性，其属性值就是这个新函数的对象。』


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

```
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

## 02. Object Specifiers

It sometimes happens that a constructor is given a very large number of parameters. This can be troublesome because it can be very difficult to remember the order of the arguments. In such cases, it can be much friendlier if we write the constructor to accept a single object specifier instead. That object contains the specification of the object to be constructed. So, instead of:

有时候，构造器要接受一大串参数。这可能令人烦恼，因为要记住参数的顺序非常困难。在这种情况下，如果我们在编写构造器时让它接受一个简单的对象说明符，可能会更加友好。那个对象包含了将要构建的对象规格说明。

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

## 03. Prototypal

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
var myCat = Object.create(myMammal);
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

## 04. Functional

One weakness of the inheritance patterns we have seen so far is that we get no privacy. All properties of an object are visible. We get no private variables and no private methods. Sometimes that doesn’t matter, but sometimes it matters a lot. In frustration, some uninformed programmers have adopted a pattern of pretend privacy. If they have a property that they wish to make private, they give it an odd-looking name, with the hope that other users of the code will pretend that they cannot see the odd looking members. Fortunately, we have a much better alternative in an application of the module pattern.

一些无知的程序员接受了一种伪装私有（pretend privacy）的模式。如果想构造一个私有属性，他们就给它起一个怪模怪样的名字，并且希望其他使用代码的用户假装看不到这些奇怪的成员。

We start by making a function that will produce objects. We will give it a name that starts with a lowercase letter because it will not require the use of the new prefix. The function contains four steps:

1. It creates a new object. There are lots of ways to make an object. It can make an object literal, or it can call a constructor function with the new prefix, or it can use the Object.create method to make a new instance from an existing object, or it can call any function that returns an object.

2. It optionally defines private instance variables and methods. These are just ordinary vars of the function.

3. It augments that new object with methods. Those methods will have privileged access to the parameters and the vars defined in the second step.

4. It returns that new object.

Here is a pseudocode template for a functional constructor (boldface text added for emphasis):

我们从构造一个生成对象的函数开始。我们以小写字母开头来命名它，因为它并不需要使用 new 前缀。

1『这里作者说的「创建新对象」其实对应于之前重点提到的，函数调用所用的 4 种方法。』


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

    my. member = value;

Now, we make a new object and assign it to that. There are lots of ways to make a new object. We can use an object literal. We can call a pseudoclassical constructor with the new operator. We can use the Object.create method on a prototype object.

Or, we can call another functional constructor, passing it a spec object (possibly the same spec object that was passed to this constructor) and the my object. The my object allows the other constructor to share the material that we put into my. The other constructor may also put its own shared secrets into my so that our constructor can take advantage of it.

Next, we augment that, adding the privileged methods that make up the object’s interface. We can assign new functions to members of that. Or, more securely, we can define the functions first as private methods, and then assign them to that: 

```
var methodical = function ( ) {
...
};
that.methodical = methodical;
```

The advantage to defining methodical in two steps is that if other methods want to call methodical, they can call methodical( ) instead of that.methodical( ). If the instance is damaged or tampered with so that that.methodical is replaced, the methods that call methodical will continue to work the same because their private methodical is not affected by modification of the instance. Finally, we return that. 

Let’s apply this pattern to our mammal example. We don’t need my here, so we’ll just leave it out, but we will use a spec object. The name and saying properties are now completely private. They are accessible only via the privileged get_name and says methods:

spec 对象包含构造器需要枃造一个新实例的所有信息。spec 的内容可能会被复制到私有变量中，或者被其他函数改变，或者方法可以在需要的时候访问 spec 的信息。（一个简化的方式是替换 spec 为一个单一的值。当构造对象过程中并不需要整个 spec 对象的时候，这是有用的。）my 对象是一个为继承链中的构造器提供秘密共享的容器。my 对象可以选择性地使用。如果没有传入一个 my 对象，那么会创建一个 my 对象。

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

函数化模式有很大的灵活性。它相比伪类模式不仅带来的工作更少，还让我们得到更好的封装和信息隐藏，以及访问父类方法的能力。如果对象的所有状态都是私有的，那么该对象就成为一个「防伪」（(tamper-proof）对象。该对象的属性可以被替换或删除，但该对象的完整性不会受到损害。如果我们用函数化的样式创建一个对象，并且该对象的所有方法都不使用 this 或 that，那么该对象就是持久性（durable）的。一个持久性对象就是一个简单功能函数的集合。一个持久性的对象不会被入侵。访问一个持久性的对象时，除非有方法授权，否则攻击者不能访问对象的内部状态。

## 05. Parts

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

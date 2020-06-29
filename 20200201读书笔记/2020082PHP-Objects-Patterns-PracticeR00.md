# 2020082PHP-Objects-Patterns-PracticeR00

Copyright © 2016 by Matt Zandstra

## 记忆时间

2020-06-18

## 卡片

### 0101. 主题卡——面向对象和面向过程的区别

One core difference between object-oriented and procedural code can be found in the way that responsibility is distributed. Procedural code takes the form of a sequential series of commands and method calls. The controlling code tends to take responsibility for handling differing conditions. This top-down control can result in the development of duplications and dependencies across a project. Object-oriented code tries to minimize these dependencies by moving responsibility for handling tasks away from client code and toward the objects in the system.

面向对象和过程式编程的一个核心区别是如何分配职责。过程式编程表现为一系列命令和方法的连续调用。控制代码根据不同的条件执行不同的职责。这种自顶向下的控制方式导致了重复和相互依赖的代码遍布于整个项目。面向对象编程则将职责从客户端代码中移到专门的对象中，尽量减少相互依赖。

### 0201. 术语卡——XP

Related topics also grew in prominence. Among them was eXtreme Programming (XP), championed by Kent Beck. XP is an approach to projects that encourages flexible, design-oriented, highly focused planning and execution. Prominent among XP’s principles is an insistence that testing is crucial to a project’s success. Tests should be automated, run often, and preferably designed before their target code is written.

XP also dictates that projects should be broken down into small (very small) iterations. Both code and requirements should be scrutinized at all times. Architecture and design should be a shared and constant issue, leading to the frequent revision of code.

### 0202. 术语卡——PHP 本质的两块内容

In the Beginning: PHP/FI. The genesis of PHP as we know it today lies with two tools developed by Rasmus Lerdorf using Perl. PHP stood for Personal Homepage Tools. FI stood for Form Interpreter. Together, they comprised macros for sending SQL statements to databases, processing forms, and flow control. 

### 0203. 术语卡——继承

单纯拆分后的弊端：1）很多重复代码或者重复的形式；2）共有的部分要更新的话每个都得更新，容易忘。3）传参的时候类型检测不好实现了。「继承」是分割与合并之间的平衡把握。

The CD and book aspects of the ShopProduct class don’t work well together but can’t live apart, it seems. I want to work with books and CDs as a single type while providing a separate implementation for each format. I want to provide common functionality in one place to avoid duplication, but allow each format to handle some method calls differently. I need to use inheritance.

### 0204. 术语卡——Interfaces 及其意义

接口才是纯模板，它只定义函数，而且这个函数没函数体。相比而言，抽象类里除了有抽象方法外，也可以有普通方法。

Although abstract classes let you provide some measure of implementation, interfaces are pure templates. An interface can only define functionality; it can never implement it. An interface is declared with the interface keyword. It can contain properties and method declarations but not method bodies. 

ShopProduct already had a getPrice() method, so why might it be useful to implement the Chargeable interface? Once again, the answer has to do with types. An implementing class takes on the type of the class it extends and the interface that it implements.（take on 是承担的意思。）

实现接口的类接受了它继承的类及实现的接口的类型。

As we have seen, interfaces help you manage the fact that, like Java, PHP does not support multiple inheritance. In other words, a class in PHP can only extend a single parent. However, you can make a class promise to implement as many interfaces as you like; for each interface it implements, the class takes on the corresponding type. So interfaces provide types without implementation. 

一个接口的实现过程，如同继承一个只包含抽象方法的抽象类。实现接口，相当于在定义接口的函数语句后面直接加上函数体。目前知道的用途：1）一个类只能继承一个基类，但可以实现多个接口，没实现一个接口对应着一个「type」。2）跟 traits 结合起来用。

```php
// listing 04.09
class ShopProduct implements Chargeable {    
    // ...    
    protected $price;    
    // ...
    public function getPrice(): float    {        
        return $this->price;    
    }    
    // ...
}
```

在类里实现接口的时候，配套的数据类型不能少，比如上面代码里的「public function getPrice(): float {}」。这点正好体现了后面一直强调的「实现多个指定类型」。

### 0205. 术语卡——Identity Map

Note: Why would I use a static factory method when a constructor performs the work of creating an object already? In Chapter 12, I’ll describe a pattern called Identity Map. an Identity Map component generates and manages a new object only if an object with the same distinguishing characteristics is not already under management. If the target object already exists, it is returned. a factory method like create() would make a good client for a component of this sort.

当构造函数创建对象时，我为什么使用静态工厂方法？第 12 章将介绍 Identity Map 模式。只有具有相同特征的对象没有被管理，Identity Map 组件才会生成并管理这个新对象。如果目标对象已经存在，就返回诚对象。像 create() 这样的工厂方法能为这类组件创建优秀的客户端。

### 0206. 术语卡——class

本书对「类」的定义：

If a class is a template for generating objects, it follows that an object is data that has been structured according to the template defined in a class. An object is said to be an instance of its class. It is of the type defined by the class.

### 0207. 术语卡——类型处理

Note: in the next section,「taking the hint: Object types,」I will describe a much better way of constraining the type of arguments passed to methods and functions. Converting a string argument on the client’s behalf would be friendly but would probably present other problems. in providing a conversion mechanism, you second-guess the context and intent of the client. by enforcing the boolean data type, on the other hand, you leave the client to decide whether to map strings to boolean values and determine which word should map to true or false. the outputAddresses() method, meanwhile, concentrates on the task it is designed to perform. this emphasis on performing a specific task in deliberate ignorance of the wider context is an important principle in object-oriented programming, and I will return to it frequently throughout the book.

这种方法强制性要求客户端代码提供正确的数据类型给 Resolve 参数。把字符串参数转化成布尔类型对于客户端代码来说更加友好，但是这可能会引起其他问题。在提供转换方法的情况下，我们需要猜测客户端代码的环境和意图。另一方面，通过强制规定参数为布尔型数据类型客户端代码需要决定是否将字符串映射为布尔值以及哪个单词映射为哪个值。这样，outputaddresses() 方法可以专注于执行它的任务。在面向对象开发中，「专注特定任务，忽略外界上下文」是一个重要的设计原则，我们将在本书中经常提到这一点。

In fact, your strategies for dealing with argument types will depend on the seriousness of any potential bugs on the one hand, and the benefits of flexibility on the other. PHP casts most primitive values for you, depending on context. Numbers in strings are converted to their integer or floating point equivalents when used in a mathematical expression, for example. So your code might be naturally forgiving of type errors. If you expect one of your method arguments to be an array, however, you may need to be more careful. Passing a nonarray value to one of PHP’s array functions will not produce a useful result and could cause a cascade of errors in your method.

事实上，采用哪种处理参数类型的策略，取决于任何潜在 bug 的严重程度。通常 PHP 会根据语境自动转换大多数基本数据类型。例如，在数学表达式中，字符串中的数字被转换成相等的整型或浮点型。因此你的代码多半会自然地容忍类型错误。但如果要求方法参数必须是一个数组，就需要更加小心。传递一个非数组值到 PHP 数组函数不会产生有用的结果，还可能会在方法中引起一连串的错误。因此，你需要在检测类型、转换类型和依赖良好清晰的文档（无论决定用哪一种，都应该提供文档）之间仔细权衡。

It is likely, therefore, that you will strike a balance among testing for type, converting from one type to another, and relying on good, clear documentation (you should provide the documentation, whatever else you decide to do). 

However you address problems of this kind, you can be sure of one thing—type matters. The fact that PHP is loosely typed makes it all the more important. You cannot rely on a compiler to prevent type-related bugs; you must consider the potential impact of unexpected types when they find their way into your arguments. You cannot afford to trust client coders to read your thoughts, and you should always consider how your methods will deal with incoming garbage.

无论你如何解决这类问题，都要认真思考一件事情：类型处理。PHP 是一种弱类型的语言这使得这件事更加重要。我们不能依靠编译器来防止类型相关的 bug，必须考虑到当非法数据类型的参数传递给方法时，会产生怎样的后果。我们不能完全信任客户端程序员，应该始终考虑如何在方法中处理他们引入的无用信息。

### 0208. 术语卡——Accessor Methods

一个原则，通过对象的方法去访问属性值，不要直接访问，把「方法」作为接口。

Even when client programmers need to work with values held by your class, it is often a good idea to deny direct access to properties, providing methods instead that relay the needed values. Such methods are known as accessors or getters and setters.

You have already seen one benefit afforded by accessor methods. You can use an accessor to filter a property value according to circumstances, as was illustrated by the getPrice() method. You can also use a setter method to enforce a property type. Type declarations can be used to constrain method arguments, but a property can contain data of any type. Remember the ShopProductWriter class that uses a ShopProduct object to output list data? I can develop this further, so that it writes any number of ShopProduct objects at one time:

之前已经看到由访问方法带来的一个好处。可以使用访问方法根据环境过滤属性，就像 getPrice() 方法那样。也可以使用 setter 方法来强制属性类型。我们已经见过，类的类型提示可以用于约束方法参数，但是它不能直接控制属性类型。还记得 ShopProductwriter 类使用 ShopProduct 输出清单数据吗？我们将改进它，使其一次可以输出许多 ShopProduct 对象。

### 0209. 术语卡——Abstract Classes

抽象类不能实例化，它是用来定义接口供其他类继承用的。抽象类里定义的抽象方法不能有「实现」，所以定义的时候没有函数体，跟调用的形式一样。关键是继承它的子类一定在子类里实现这个抽象方法。

An abstract class cannot be instantiated. Instead it defines (and, optionally, partially implements) the interface for any class that might extend it. You define an abstract class with the abstract keyword. In most cases, an abstract class will contain at least one abstract method. These are declared, once again, with the abstract keyword. An abstract method cannot have an implementation. You declare it in the normal way, but end the declaration with a semicolon rather than a method body. 

### 0210. 术语卡——Traits

traits 对于 class，如同 class 对于 object。traits 如同可以供多个类调用的公共代码。

As we have seen, interfaces help you manage the fact that, like Java, PHP does not support multiple inheritance. In other words, a class in PHP can only extend a single parent. However, you can make a class promise to implement as many interfaces as you like; for each interface it implements, the class takes on the corresponding type. So interfaces provide types without implementation. But what if you want to share an implementation across inheritance hierarchies? PHP 5.4 introduced traits, and these let you do just that.

1『 traits 的作用是实现局部继承：share an implementation across inheritance hierarchies. 可以当作类的组件模块，在类的定义里使用 use 关键词调用 trait。在 laravel 框架里看到很多 use 语句是放在 class 定义体之外的（这个的含义待确认，2020-06-29）。traits 能和接口结合起来一起用，还能跟抽象属性、抽象方法结合起来用，着实强大。』

A trait is a class-like structure that cannot itself be instantiated but can be incorporated into classes. Any methods defined in a trait become available as part of any class that uses it. A trait changes the structure of a class, but doesn’t change its type. Think of traits as includes for classes. Let’s look at why a trait might be useful.

### 0211. 术语卡——late static bindings

So self resolves to DomainObject, the place where create() is defined, and not to Document, the class on which it was called. Until PHP 5.3 this was a serious limitation, which spawned many rather clumsy workarounds. PHP 5.3 introduced a concept called late static bindings. The most obvious manifestation of this feature is the keyword: static. static is similar to self, except that it refers to the invoked rather than the containing class. In this case, it means that calling Document::create() results in a new Document object and not a doomed attempt to instantiate a DomainObject object. So now I can take advantage of my inheritance relationship in a static context:

因此，self 被解析为定义 create() 的 DomainObject，而不是解析为调用 self 的 Document 类。PHP 5.3 之前，在这方面都有严格的限制，产生过很多笨拙的解决方案。PHP 5.3 中引入了延迟静态绑定的概念。该特性最明显的标志就是新关键字 static。static 类似于 self，但它指的是被调用的类而不是包含类。在本例中，它的意思是调用 Document::create() 将生成一个新的 Document 对象，而不是试图实例化一个 DomainObject 对象。因此，现在在静态上下文中使用继承关系。

```php
abstract class DomainObject{    
    public static function create(): DomainObject    {        
        return new static();    
    }
}

class User extends DomainObject {

}

class Document extends DomainObject {

}

print_r(Document::create());
```

### 0301. 人名卡——Matt Zandstra

人名卡：Matt Zandstra（）

印象：本书的作者。

### 0401. 金句卡——code to an interface, not an implementation

As you will see, object-oriented design often uses a method declaration as a kind of contract. The method demands certain inputs and, reciprocally, it promises to give you a particular type of data back. PHP 5 programmers were forced to rely on comments, convention, and manual type checking to maintain contracts of this kind in many cases. Developers and commentators often complained about this. Here is a quote from the previous edition of this book:

…there is still no commitment to provide support for hinted return types. This would allow you to declare in a method or function’s declaration the object type that it returns. This would then be enforced by the PHP engine. Hinted return types would further improve PHP’s support for pattern principles (principles such as「code to an interface, not an implementation」). I hope one day to revise this book to cover that feature!

I’m pleased to write that the day has come! PHP 7 introduced scalar type declarations (previously known as type hints) and return type declarations, and you’ll see them used plenty in this edition. PHP 7 also provided other nice-to-haves, including anonymous classes and some namespace enhancements.

1『

强制规定输入输出的数据类型，这个真赞，数据流开发中就一直在用。

```php
    /**
     * 平时补风量
    */
    public function normalSupplyAir(): int
    {
        $nomal_supply_air = $this->diffpressAir() + $this->normalExhaustAir();
        return $nomal_supply_air;
    }
```
』

### 0402. 金句卡——Type determines the way data can be managed in your scripts

Type determines the way data can be managed in your scripts. You use the string type to display character data, for example, and manipulate such data with string functions. Integers are used in mathematical expressions, Booleans are used in test expressions, and so on. These categories are known as primitive types. On a higher level, though, a class defines a type. A ShopProduct object, therefore, belongs to the primitive type object, but it also belongs to the ShopProduct class type. In this section, I will look at types of both kinds in relation to class methods.

### 0501. 任意卡——设置私有属性、保护属性的原则

As a general rule, err on the side of privacy. Make properties private or protected at first and relax your restriction only as needed. Many (if not most) methods in your classes will be public, but once again, if in doubt, lock it down. A method that provides local functionality for other methods in your class has no relevance to your class’s users. Make it private or protected.

一般来说，我们倾向于严格控制可访问性。最好将类属性初始化为 private 或 protected 然后在需要的时候再放松限制条件。类中的许多（如果不是大多数）方法都可以是 public，但是如果拿不定主意的话，就限制一下。有些类方法只为类中其他方法提供本地功能，与类外部的代码没有任何联系，应该将其设置为 private 或 protected。

1『以上是设置私有属性、保护属性的原则。属性都设置为限制性的 private 或 protected 的，再根据应用场景放松限制；方法都设置为 public 的，再根据应用场景加强限制。』

### 0502. 任意卡——如何调用静态属性和静态方法

静态方法的调用形式都是「类名::静态方法」，唯一也用 :: 调用非静态方法的场景式在类继承定义里「parent::非静态方法」。所以，如果是访问那些显式声明的静态属性和静态方法的，都应该用 :: 去调用，除非是访问重载方法（这点还是不明白）。（2020-06-19）

Note: Making a method call using parent is the only circumstance in which you should use a static reference to a nonstatic method. unless you are accessing an overridden method, you should only ever use :: to access a method or property that has been explicitly declared static. In documentation, however, you will often see static syntax used to refer to a method or property. this does not mean that the item in question is necessarily static, just that it belongs to a certain class. the write() method of the ShopProductWriter class might be referred to as ShopProductWriter::write(), for example, even though the write() method is not static. You will see this syntax here when that level of specificity is appropriate.

只有在使用 parent 关健字调用方法的时候，才能对一个非静态方法进行静态形式的调用。除非是访问一个被写的方法，否则永远只能使用 :: 访问被明确声明为 static 的方法或属性。在文档中，你将会经常看到使用 static 语法来引用方法或属性。这并不意味着其中的方法或属性必须是静态的，只不过说明它属于特定的类。例如，shopProductWriter 类的方法 write() 可以表示为 Shopproductwriter::write()，虽然 write() 方法并不是静态的。你将在本书中看到这种语法形式。

### 0503. 任意卡——静态属性和静态方法的优势

So, why would you use a static method or property? Static elements have a number of characteristics that can be useful. First, they are available from anywhere in your script (assuming that you have access to the class). This means you can access functionality without needing to pass an instance of the class from object to object or, worse, storing an instance in a global variable. Second, a static property is available to every instance of a class, so you can set values that you want to be available to all members of a type. Finally, the fact that you don’t need an instance to access a static property or method can save you from instantiating an object purely to get at a simple function.

静态元素有很多有用的特性。首先，它们在代码中的任何地方都可用（假设你可以访问该类）。也就是说，你不需要在对象间传递类的实例，也不需要将实例存放在全局变量中，就可以访问类中的方法。其次，类的每个实例都可以访问类中定义的静态属性，所以你可以利用静态属性来设置值，该值可以被类的所有对象使用。最后，不需要实例对象就能访问静态属性或方法，这样我们就不用为了获取一个简单的功能而实例化对象。

### 0504. 任意卡——Combining Traits and Interfaces

Although traits are useful, they don’t change the type of the class to which they are applied. So when you apply the IdentityTrait trait to multiple classes, they won’t share a type that could be hinted for in a method signature. Luckily, traits play well with interfaces. I can define an interface that requires a generateId() method, and then declare that ShopProduct implements it:

单独的 traits 没法使用「type hinting」，但是结合 Interfaces 就能使用。

### 0505. 任意卡——类之间的关系以及对象间的关系

There are other relationships that you can define for your classes. You can create classes that are composed of other types or that manage lists of other type instances. You can design classes that simply use other objects. The potential for such relationships of composition or use is built into your classes (e.g., through the use of type declarations in method signatures), but the actual object relationships take place at runtime, which can add flexibility to your design. You will see how to model these relationships in this chapter, and we’ll explore them further throughout the book.

As part of the design process, you must decide when an operation should belong to a type and when it should belong to another class used by the type. Everywhere you turn, you are presented with choices, decisions that might lead to clarity and elegance or might mire you in compromise. In this chapter, I will examine some issues that might influence a few of these choices.

你还可以为类定义其他关系。你可以创建由其他类型的对象组成的类，也可以创建用于管理多个其他对象实例的类。你还可以创建只是简单地用到其他对象的类。类之间的潜在关系往往在类的结构中就已经确定（例如类方法参数中的类型提示指定了要使用的对象类型），但是对象之间的实际关系只在代码执行时才产生，这些对象间的关系增加了代码的灵活性。在本章中，我们将看到如何为这些关系建立模型。在设计过程中，必须决定某个操作何时属于某个类型，何时属于这个类型使用的另一个类。在每个地方你都面临选择，你的决定可能使代码更清晰、更优雅，也可能会让你陷入困境。

## 书评

### 01

每个段落先提出问题，给出实现，并讨论成效，对于 OO 入门有一定帮助，能够帮助开拓思路，对 OO 老鸟有参考价值，可以换换空气，让脑子清空一下，听听别人说什么，对开发新程序有一定作用。内容并不能说新颖，毕竟内容已经是 2007 的了，不过设计模式并不会随着技术的改进而有多少变化，毕竟理论层面上不会有什么改变的东西。

### 02

过程：花了一个月的时间把书中的主要部分，「面向对象」和「模式」部分。第三部分我只是选读了我认为比较有用的「单元测试」章节。翻译： 不错。没有咬文嚼字，通俗易懂，都是按照中国程序员对专属名词的普遍认识所翻译的。

内容部分——面向对象：在读面向对象部分时，我对本书还是抱有很大希望了，东西讲的比较深入，虽然有错误的地方，但是结构还是比较清晰。作者没有把读者当作是刚刚进入 php 世界的小孩子，而是认为读者有了一定的工作经验。所以在作者花了更多的精力来，讲解面向对象的高级特性，还为了给最重要的「模式」部分铺路，讲了一下「对象与设计」。

内容部分——模式： 我对第 7-11 章节还是比较满意的，作者没有太纠缠于任何一个复杂的设计模式，从一些原则开始讲起，譬如，「组合与继承」，「解耦」，「聚合」，「正交」等等。作者将这些零散而又重要的知识点一一呈现，并且细细讲清楚说明白，我还是觉得蛮受用的。一条「针对接口编程，而不是针对实现编程」贯彻始终。后面几个章节的各个小模式不管有用没用讲的也算是清晰（都画了 UML）。但是，个人认为最最恶心的第 12，13 章节让我彻底对这本书失望至极，如果说企业模式章节，是为了说明 MVC 结构的好，那我觉得还勉强说的过去，毕竟有对前面章节的一些知识点的升华，但是「数据库模式」章节，我就真的不能忍受了。一上来就搞了一个「数据库映射器」，我不知道该不该称其为模式。其作用是将数据库表中的行和列转换成项目中的数据结构，这么看感觉还是蛮有意义的，但是使用的方法比较复杂，最可气的是当你废了很大功夫搞懂之后，这一章的后半部分开始说这个方法有哪里哪里不好，我们应该把它细化，而使用的方法针对性很强，灵活性不高，感觉上只有「解耦和」这个作者的思想可以运用到实战中，书中提到的代码我看就算了吧。

都有更好的替代品：想获得面向对象的知识，可以看《php 手册》。想获得模式的知识，可以看《Head First 设计模式》。而第三部分「时间」的各个工具，我想也应该和 phpunit 一样有官方手册可以看吧。没有必要花时间在这本书上面。除非你已经很了解我上面提到的经典书籍里面的知识，想看看如何用 php 来实现模式的各个概念的，那就看看它吧。

### 04

读第一遍读到数据库模式，感觉吃不消了，所以跳过去直接读后面的实践部分。目前在读第二遍，希望这次能吃透作者讲的数据库模式。这绝对是一本每读一遍都会受益一便的好书，虽然书中讲的各种模式目前看来没有应用到工作中的机会，但是通过作者的讲解，你会看到这些模式一旦应用到项目中，会给整个代码的架构和质量带来多大的提升。

很久之前就想买一本介绍模式的书，看亚马逊的评论，有三个选择，四人帮的设计模式，head first desgin pattern 和这一本。如果你是 php 程序员，有一定的代码经验，想了解一下设计模式，这本书应该是你第一本入手的书。四人帮的设计模式应该是你的进阶书。而我个人来说不是那种中意类似看图学 XX 的读者，如果你是的话可能 head first design pattern 比较适合你。

该书的结构很清晰，作者行文也很流畅，虽然有个别语句可能读第一遍不很明白，但那很可能是你没有透彻理解当前的上下文，返回多读几遍便能了解作者的用意。翻译质量算很高的了。但是其中的错误（不知是印刷错误还是作者的错误还是译者的错误）有点多，我目前都有一个长长的列表，打算去官方勘误页面提交（不过貌似现在打不开......）

对象，模式和实践是本书的三个核心部分，有人说第三部分不是很必要，但是对于项目经验不是很丰富的程序员来说，第三部分绝对会对你项目开发流程的认识拓展很多，个人觉得是不能忽略的部分。对象部分对 php 对面向对象的支持和实现讲解的很透彻，不过重点是在实现，而不是设计，如果你需要面向对象设计方面的知识，这部分是远远不够的，但是对于 PHP 面向对象的实现，这部分应该是你需要读得唯一的东西了。

模式部分是本书的精华部分，我个人也在网上或视频教程中学过设计模式，但是还是感觉这本书对于模式的讲解最为透彻。包括项目中遇到的真实问题，可能的解决方案，每种解决方案的不足之处，引入设计模式，讲解模式的实现以及实现结果的优势和不足之处，实现的可能变种......等等方方面面。全面而透彻。

### 05

看到有人说这本书没有达到书名的目标，可能「深入」这个词让他产生的误解了吧，这本书更像一本实实在在的 PHP 进阶指南。本书全文分为三个方面：PHP 面向对象思想，PHP 设计模式，PHP 实践。这三个方面对于初级 PHP 工程师进阶来说都是很重要的内容。

PHP OOP，一般非直接通过 PHP 入门编程的童鞋对 OOP 都应该有一定的理解，这些内容对于 PHP 草根工程师更有帮助。此外，这一部分对 PHP 的一些 OOP 特性进行了阐述。

PHP 设计模式，这一块介绍了比较常用的设计模式，并且用 PHP 的语法进行了实现，对于对设计模式理解不到位的童鞋有帮助。此外，这一部分还涉及一些架构方面的内容，但是浅尝辄止，有兴趣的童鞋可以看一看《企业应用架构模式》一书。

2『在书籍「2020104Laravel实战入门」里也推荐过这本书，已下载书籍「2020105企业应用架构模式」以及原书「2020105Patterns-of-Enterprise-Application-Architecture」，有空一定要去读下。（2020-03-12）』

PHP 实践，对于不了解的童鞋帮助很大，对于有所了解的童鞋帮助很小。这一块比较成体系的介绍了 PHP 开发的相关工具，仔细看一遍还是有一些收获的。不过，关于包管理一节用到的 PEAR 包未免太落后了，可以不用学，把精力用来学 Composer 是更优的选择。至于版本管理，SVN 已经落伍了，不过学习一下倒也无妨，本书下一版本已经把 SVN 换成 Git 了。

### 06

设计模式一直以来很难懂，之前遇到很大的瓶颈，买回来这本书，读起来基本一目十行，不是因为内容太简单，而是该做的我都已经做过了，只是在模式上认识还不够清晰，概念体系不完整，所以想看书补补，觉得这本书设计模式部分写的非常好。甚至这本书应该只保留对象和设计模式部分，其它都是多余的。推荐已经了解并且实践过的同行们都来一读，模式这种东西基本上不会发生太大改变，这本书里描述的也算是非常精准了。

至于其它部分，变化太快，比如工具中，phar 没有讲到，发展历程中，错误的预计了 php 的发展方向：php6 搁浅了，phpng（也就是 php7）将在 2015 年推出第一个版本。不过也无怪于作者，毕竟写这本书的时候鸟哥都没有在 github 上提交过 php 的源码。去掉这些多余的部分这本书简直可以堪称完美，或者保留发展历史，把展望去掉，太不好展望了，需要充分了解开源社区中风起云涌的变化。

### 07

这是最好的 PHP 的 OO 书之一，另外一本是 PHP in Action。PHP 架构中常用的设计模式不多，书中基本都谈到了。我觉得学习设计模式最好是和框架一起进行，一个是理论，一个是实践，而且流行的框架基本代表了设计的最新思想，设计模式没有好坏之分，所以有空都应该学学。

## Introduction

When I first conceived of this book, object-oriented design in PHP was an esoteric topic. The intervening years have not only seen the inexorable rise of PHP as an object-oriented language, but also the march of the framework. Frameworks are incredibly useful, of course. They manage the guts and the glue of many (perhaps, these days, most) web applications. What’s more, they often exemplify precisely the principles of design that this book explores. 

There is, though, a danger for developers here, as there is in all useful APIs. This is the fear that one might find oneself relegated to userland, forced to wait for remote gurus to fix bugs or add features at their whim. It’s a short step from this standpoint to a kind of exile in which one is left regarding the innards of a framework as advanced magic, and one’s own work as not much more than a minor adornment stuck up on top of a mighty unknowable infrastructure.

Although I’m an inveterate reinventor of wheels, the thrust of my argument is not that we should all throw away our frameworks and build MVC applications from scratch (at least not always). It is rather that, as developers, we should understand the problems that frameworks solve, and the strategies they use to solve them. We should be able to evaluate frameworks not only functionally but in terms of the design decisions their creators have made, and to judge the quality of their implementations. And yes, when the conditions are right, we should go ahead and build our own spare and focused applications, and, over time, compile our own libraries of reusable code.

1『秉持不要重新造轮子的原则，善用框架，但是要有一个概念，必须得清楚这个框架设计的初衷，它解决了什么问题，它用了什么策略。』

## 0101. PHP: Design and Management

### 1. 逻辑脉络

一些面向编程的诉求；编程范式的发展。

### 2. 摘录及评论

I hope this book goes some way toward helping PHP developers apply design-oriented insights to their platforms and libraries, and provides some the conceptual tools needed when it’s time to go it alone. This is a book about object-oriented design and programming. It is also about tools for managing a PHP codebase from collaboration through to deployment.

These two themes address the same problem from different but complementary angles. The primary aim is to build systems that achieve their objectives and lend themselves well to collaborative development. A secondary goal lies in the aesthetics of software systems. 

As programmers, we build machines that have shape and action. We invest many hours of our working day, and many days of our lives, writing these shapes into being. We want the tools we build, whether individual classes and objects, software components, or end products, to form an elegant whole. The process of version control, testing, documentation, and build does more than support this objective: it is part of the shape we want to achieve. Just as we want clean and clever code, we want a codebase that is designed well for developers and users alike. The mechanics of sharing, reading, and deploying the project should be as important as the code itself.

1『编程两大主题：功能实现和代码简洁。』

In July 2004 PHP 5.0 was released. This version introduced a suite of radical enhancements. Perhaps first among these was radically improved support for object-oriented programming. This stimulated much interest in objects and design within the PHP community. In fact, this was an intensification of a process that began when version 4 first made object-oriented programming with PHP a serious reality.

1『 2004 年发布的 PHP 5.0 增加了面向对象的编程特性。』

In this chapter, I look at some of the needs that coding with objects can address. I very briefly summarize some aspects of the evolution of patterns and related practices. I also outline the topics covered by this book. I will look at the following: 1) The evolution of disaster: A project goes bad. 2) Design and PHP: How object-oriented design techniques took root in the PHP community. 3) This book: Objects. Patterns. Practice.

### 1.1 The Problem

You add utility functions (such as database access code) to files that can be included from page to page, and before you know it you have a working web application. You are well on the road to ruin. You don’t realize this, of course, because your site looks fantastic. It performs well, your clients are happy, and your users are spending money. Trouble strikes when you go back to the code to begin a new phase. Now you have a larger team, some more users, a bigger budget. Yet, without warning, things begin to go wrong. It’s as if your project has been poisoned.

Your new programmer is struggling to understand code that is second nature to you, although perhaps a little byzantine in its twists and turns. She is taking longer than you expected to reach full strength as a team member. A simple change, estimated at a day, takes three days when you discover that you must update 20 or more web pages as a result.

One of your coders saves his version of a file over major changes you made to the same code some time earlier. The loss is not discovered for three days, by which time you have amended your own local copy. It takes a day to sort out the mess, holding up a third developer who was also working on the file.

Because of the application’s popularity, you need to shift the code to a new server. The project has to be installed by hand, and you discover that file paths, database names, and passwords are hard-coded into many source files. You halt work during the move because you don’t want to overwrite the configuration changes the migration requires. The estimated two hours becomes eight as it is revealed that someone did something clever involving the Apache module ModRewrite, and the application now requires this to operate properly.

1『迁移数据（migration）是个需要提前考虑的工作。』

You finally launch phase 2. All is well for a day and a half. The first bug report comes in as you are about to leave the office. The client phones minutes later to complain. Her report is similar to the first, but a little more scrutiny reveals that it is a different bug causing similar behavior. You remember the simple change back at the start of the phase that necessitated extensive modifications throughout the rest of the project.

You realize that not all of the required modifications are in place. This is either because they were omitted to start with or because the files in question were overwritten in merge collisions. You hurriedly make the modifications needed to fix the bugs. You’re in too much of a hurry to test the changes, but they are a simple matter of copy-and-paste, so what can go wrong?

The next morning you arrive at the office to find that a shopping basket module has been down all night. The last-minute changes you made omitted a leading quotation mark, rendering the code unusable. Of course, while you were asleep, potential customers in other time zones were wide awake and ready to spend money at your store. You fix the problem, mollify the client, and gather the team for another day’s firefighting.

This everyday tale of coding folk may seem a little over the top, but I have seen all these things happen over and over again. Many PHP projects start their life small and evolve into monsters. Because the presentation layer also contains application logic, duplication creeps in early as database queries, authentication checks, form processing, and more are copied from page to page. Every time a change is required to one of these blocks of code, it must be made everywhere that the code is found, or bugs will surely follow.

1『原因在于展示层常常也包含很多其他层的东西，比如软件的逻辑层、数据库请求、表单处理等等。还常常没有文档系统、测试系统。』

Lack of documentation makes the code hard to read, and lack of testing allows obscure bugs to go undiscovered until deployment. The changing nature of a client’s business often means that code evolves away from its original purpose until it is performing tasks for which it is fundamentally unsuited. Because such code has often evolved as a seething, intermingled lump, it is hard, if not impossible, to switch out and rewrite parts of it to suit the new purpose.

Now, none of this is bad news if you are a freelance PHP consultant. Assessing and fixing a system like this can fund expensive espresso drinks and DVD box sets for six months or more. More seriously, though, problems of this sort can mean the difference between a business’s success or failure.

### 1.2 PHP and Other Languages

PHP’s phenomenal popularity meant that its boundaries were tested early and hard. As you will see in the next chapter, PHP started life as a set of macros for managing personal home pages. With the advent of PHP 3 and, to a greater extent, PHP 4, the language rapidly became the successful power behind large enterprise websites. In many ways, however, the legacy of PHP’s beginnings carried through into script design and project management. In some quarters, PHP retained an unfair reputation as a hobbyist language, best suited for presentation tasks.

1『 PHP 很多时候是拿来做展示层工作的，应该是被低估了。』

About this time (around the turn of the millennium), new ideas were gaining currency in other coding communities. An interest in object-oriented design galvanized the Java community. Since Java is an object-oriented language, you may think that this is a redundancy. Java provides a grain that is easier to work with than against, of course, but using classes and objects does not in itself determine a particular design approach.

The concept of the design pattern as a way of describing a problem, together with the essence of its solution, was first discussed in the 1970s. Perhaps aptly, the idea originated in the field of architecture, not computer science. By the early 1990s, object-oriented programmers were using the same technique to name and describe problems of software design. The seminal book on design patterns, Design Patterns: Elements of Reusable Object-Oriented Software (Addison-Wesley Professional, 1995) by Erich Gamma, Richard Helm, Ralph Johnson, and John Vlissides (henceforth referred to in this book by their affectionate nickname, the Gang of Four), is still indispensable today. The patterns it contains are a required first step for anyone starting out in this field, which is why most of the patterns in this book are drawn from it.

2『面向对象的范式起源于建筑工程领域而非计算机；已下载四人帮的原书「2019087Design-Patterns」。』

The Java language itself deployed many core patterns in its API but it wasn’t until the late 1990s that design patterns seeped into the consciousness of the coding community at large. Patterns quickly infected the computer sections of Main Street bookstores, and the first flame wars began on mailing lists and in forums. Whether you think that patterns are a powerful way of communicating craft knowledge or largely hot air (and, given the title of this book, you can probably guess where I stand on that issue), it is hard to deny that the emphasis on software design they have encouraged is beneficial in itself.

Related topics also grew in prominence. Among them was eXtreme Programming (XP), championed by Kent Beck. XP is an approach to projects that encourages flexible, design-oriented, highly focused planning and execution. Prominent among XP’s principles is an insistence that testing is crucial to a project’s success. Tests should be automated, run often, and preferably designed before their target code is written.

XP also dictates that projects should be broken down into small (very small) iterations. Both code and requirements should be scrutinized at all times. Architecture and design should be a shared and constant issue, leading to the frequent revision of code.

2『 XP 做一张术语卡片。』

If XP was the militant wing of the design movement, then the moderate tendency is well represented by one of the best books about programming that I have ever read: The Pragmatic Programmer: From Journeyman to Master by Andrew Hunt and David Thomas (Addison-Wesley Professional, 1999).

2『 2019 年出了新版，已下载原书「2020120The-Pragmatic-Programmer2Ed」，直觉上这本书一定要读；Martin Fowler 的《重构》2019 年也出了新版，已下载原书「2019030Refactoring2Ed」。』

XP was deemed a tad cultish by some, but it grew out of two decades of object-oriented practice at the highest level, and its principles were widely cannibalized. In particular, code revision, known as refactoring, was taken up as a powerful adjunct to patterns. Refactoring has evolved since the 1980s, but it was codified in Martin Fowler’s catalog of refactorings, Refactoring: Improving the Design of Existing Code (Addison-Wesley Professional), which was published in 1999 and defined the field.

Testing, too, became a hot issue with the rise to prominence of XP and patterns. The importance of automated tests was further underlined by the release of the powerful JUnit test platform, which became a key weapon in the Java programmer’s armory. A landmark article on the subject,「Test Infected: Programmers Love Writing Tests」by Kent Beck and Erich Gamma, gives an excellent introduction to the topic and remains hugely influential.

2『上面是篇论文，已下载论文「2020014Test Infected: Programmers Love Writing Tests」存入 Zotero。』

PHP 4 was released at about this time, bringing with it improvements in efficiency and, crucially, enhanced support for objects. These enhancements made fully object-oriented projects a possibility. Programmers embraced this feature, somewhat to the surprise of Zend founders Zeev Suraski and Andi Gutmans, who had joined Rasmus Lerdorf to manage PHP development. As you shall see in the next chapter, PHP’s object support was by no means perfect. But with discipline and careful use of syntax, one could really begin to think in objects and PHP at the same time.

Nevertheless, design disasters such as the one depicted at the start of this chapter remained common. Design culture was some way off, and almost nonexistent in books about PHP. Online, however, the interest was clear. Leon Atkinson wrote a piece about PHP and patterns for Zend in 2001, and Harry Fuecks launched his journal at www.phppatterns.com (now defunct) in 2002. Pattern-based framework projects such as BinaryCloud began to emerge, as well as tools for automated testing and documentation.

The release of the first PHP 5 beta in 2003 ensured the future of PHP as a language for object-oriented programming. The Zend 2 Engine provided greatly improved object support. Equally important, it sent a signal that objects and object-oriented design were now central to the PHP project. Over the years, PHP 5 has continued to evolve and improve, incorporating important new features such as namespaces and closures. During this time, it has secured its reputation as the best choice for server-side web programming.

PHP 7, released in December 2015, represents a continuation of this trend. In particular it provides support for scalar and return type declarations — two features that many developers (together with previous editions of this book) have been clamoring for over the years. If you don’t know what that means or why it's important, read on!

2『 PHP 7 的两个新特性很重要：support for scalar and return type declarations。PHP 7 发布的时间（2015 年）做一张信息卡片。』

### 1.3 About This Book

Instead, I examine, in the context of PHP, some well-established design principles and some key patterns (particularly those inscribed in Design Patterns, the classic Gang of Four book). Finally, I move beyond the strict limits of code to look at tools and techniques that can help to ensure the success of a project. Aside from this introduction and a brief conclusion, the book is divided into three main parts: objects, patterns, and practice.

Objects. I begin Part 2 with a quick look at the history of PHP and objects, charting their shift from afterthought in PHP 3 to core feature in PHP 5. You can still be an experienced and successful PHP programmer with little or no knowledge of objects. For this reason, I start from first principles to explain objects, classes, and inheritance. Even at this early stage, I look at some of the object enhancements that PHP 5 and PHP 7 introduced.

1『基于类的面向对象，其基础内容是对象、类和继承。』

The basics established, I delve deeper into our topic, examining PHP’s more advanced object-oriented features. I also devote a chapter to the tools that PHP provides to help you work with objects and classes. It is not enough, however, to know how to declare a class, and to use it to instantiate an object. You must first choose the right participants for your system and decide the best ways for them to interact. These choices are much harder to describe and to learn than the bald facts about object tools and syntax. I finish Part 2 with an introduction to object-oriented design with PHP.

Patterns. A pattern describes a problem in software design and provides the kernel of a solution.「Solution」here does not mean the kind of cut-and-paste code that you might find in a cookbook (excellent though cookbooks are as resources for the programmer). Instead, a design pattern describes an approach that can be taken to solve a problem. A sample implementation may be given, but it is less important than the concept that it serves to illustrate. 

1『设计模式是用来解决问题的；模式是可复用的解决问题的套路。』

Part 3 begins by defining design patterns and describing their structure. I also look at some of the reasons behind their popularity. Patterns tend to promote and follow certain core design principles. An understanding of these can help in analyzing a pattern’s motivation, and can usefully be applied to all programming. I discuss some of these principles. I also examine the Unified Modeling Language (UML), a platform-independent way of describing classes and their interactions.

Although this book is not a pattern catalog, I examine some of the most famous and useful patterns. I describe the problem that each pattern addresses, analyze the solution, and present an implementation example in PHP.

Practice. Even a beautifully balanced architecture will fail if it is not managed correctly. In Part 4, I look at the tools available to help you create a framework that ensures the success of your project. If the rest of the book is about the practice of design and programming, Part 4 is about the practice of managing your code. The tools that I examine can form a support structure for a project, helping to track bugs as they occur, promoting collaboration among programmers, and providing ease of installation and clarity of code.

I have already discussed the power of the automated test. I kick off Part 4 with an introductory chapter that gives an overview of problems and solutions in this area. Many programmers are guilty of giving in to the impulse to do everything themselves. Composer, together with Packagist, its main repository, offers access to thousands of dependency managed packages that can be stitched into projects with ease. I look at the tradeoffs between implementing a feature yourself and deploying a Composer package. While I’m on the topic of Composer, I look at the installation mechanism that makes the deployment of a package as simple as a single command.

1『 Composer 是 PHP 的包管理工具，类似于 Python 的 pip；要学会在自己实现和用 composer 之间取得平衡。』

Code is about collaboration. This fact can be rewarding. It can also be a complete nightmare. Git is a version control system that enables many programmers to work together on the same codebase without overwriting one another’s work. It lets you grab snapshots of your project at any stage in development, see who has made which changes, and split the project into mergeable branches. Git will save your project one day.

When people and libraries collaborate, they often bring different conventions and styles to the party. While this is healthy, it can also undermine interoperability. Words like conform and comply give me the shivers, but it is undeniable that the creativity of the Internet is underpinned by standards. By obeying certain conventions, we are freed to play in an unimaginably vast sandbox. So, in a new chapter, I explore PHP standards, how they can help us, and how and why we should, yes, comply.

Two facts seem inevitable. First, bugs often recur in the same region of code, making some work days an exercise in déjà vu. Second, often improvements break as much as, or more than, they fix. Automated testing can address both of these issues, providing an early warning system for problems in your code. I introduce PHPUnit, a powerful implementation of the so-called xUnit test platform designed first for Smalltalk but ported now to many languages, notably Java. I look in particular at PHPUnit’s features and more generally at the benefits, and some of the costs, of testing.

Applications are messy. They may need files to be installed in nonstandard locations, or want to set up databases, or need to patch server configuration. In short, applications need stuff to be done during installation. Phing is a faithful port of a Java tool called Ant. Phing and Ant interpret a build file and process your source files in any way you tell them to. This usually means copying them from a source directory to various target locations around your system, but, as your needs get more complex, Phing scales effortlessly to meet them.

Some companies enforce development platforms — but in many cases teams end up running an array of different operating systems. Contractors arrive wielding PC laptops (hello Paul Tregoing, fifth edition tech editor), some team members evangelize endlessly for their favorite Linux distro (that’s me and my Fedora), and many hold out for yet another sexy-looking PowerBook (the coffee bar and meeting room use of which doesn’t at all make you look like just another node in a hipster Borg army). All of these will run a LAMP stack with varying degrees of ease. Ideally, though, developers should run their code in environments that closely resemble the ultimate production system. I examine Vagrant, an application which uses virtualization so that team members can keep their idiosyncratic development platforms but run project code on a production-like system.

Testing and build are all very well, but you have to install and run your tests, and keep on doing so in order to reap the benefits. It’s easy to become complacent and let things slide if you don’t automate your builds and tests. I look at some tools and techniques that are lumped together in the category「continuous integration」that will help you do just that.

What’s New in the Fifth Edition. PHP is a living language, and as such it’s under constant review and development. This new edition, too, has been reviewed and thoroughly updated to take account of changes and new opportunities. I cover new features such as anonymous classes, and the long-awaited scalar argument hints and return types. Examples use PHP 7 features where appropriate, so be aware that you will need to run code against the PHP 7 interpreter — or be ready to do some work to downgrade.

In previous editions, I included a chapter on the PEAR package repository. Composer and the Packagist repository are plainly now the standard for PHP development, and I have rewritten the chapter accordingly. It seems that I’ve switched my version control coverage for every other edition or so of this book. I’m glad to say that I’m sticking with Git this time round. I have, however, spent some more time looking at Git repositories like GitHub since these are increasingly used by developers.

I include a new chapter on the previously mentioned Vagrant. In another new chapter, I examine PHP Standards. Since I endorse the value of complying with a style guide, I have reworked every code example in the book to meet the PSR-1 and PSR-2 standards. This was a much bigger commitment than I realized, and tech editor Paul Tregoing has worked valiantly to keep me honest.

## 0102.  PHP and Objects

### 1. 逻辑脉络

PHP 各版本的特性，特别是面向对象在各个版本中的演化。

### 2. 摘录及评论

This short chapter placed objects in their context in the PHP language. The future for PHP is very much bound up with object-oriented design. In the next few chapters, I take a snapshot of PHP’s current support for object features, and introduce some design issues.

Objects were not always a key part of the PHP project. In fact, they were once described as an afterthought by PHP’s designers. As afterthoughts go, this one has proved remarkably resilient. In this chapter, I introduce this book’s coverage of objects by summarizing the development of PHP’s object-oriented features.

1『面向对象并非一直是 php 的核心，php 5 才成为其核心的。』

We will look at the following: 1) PHP/FI 2.0: PHP, but not as we know it. 3) PHP 3: Objects make their first appearance. 4) PHP 4: Object-oriented programming grows up. 5) PHP 5: Objects at the heart of the language. 6) PHP 7: Closing the gap.

### 2.1 The Accidental Success of PHP Objects

With PHP’s extensive object support and so many object-oriented PHP libraries and applications in circulation, the rise of the object in PHP may seem like the culmination of a natural and inevitable process. In fact, nothing could be further from the truth.

In the Beginning: PHP/FI. The genesis of PHP as we know it today lies with two tools developed by Rasmus Lerdorf using Perl. PHP stood for Personal Homepage Tools. FI stood for Form Interpreter. Together, they comprised macros for sending SQL statements to databases, processing forms, and flow control. These tools were rewritten in C and combined under the name PHP/FI 2.0. The language at this stage looked different from the syntax we recognize today, but not that different. There was support for variables, associative arrays, and functions. Objects, however, were not even on the horizon.

1『PHP 本质的东西，两大块，一是  Personal Homepage Tools，二是 Form Interpreter。Together, they comprised macros for sending SQL statements to databases, processing forms, and flow control. 』

Syntactic Sugar: PHP 3. In fact, even as PHP 3 was in the planning stage, objects were off the agenda. The principal architects of PHP 3 were Zeev Suraski and Andi Gutmans. PHP 3 was a complete rewrite of PHP/FI 2.0, but objects were not deemed a necessary part of the new syntax. According to Zeev Suraski, support for classes was added almost as an afterthought (on 27 August 1997, to be precise). Classes and objects were actually just another way to define and access associative arrays.

Of course, the addition of methods and inheritance made classes much more than glorified associative arrays, but there were still severe limitations on what you might do with your classes. In particular, you could not access a parent class’s overridden methods (don’t worry if you don’t know what this means yet; I will explain later). Another disadvantage that I will examine in the next section was the less than optimal way that objects were passed around in PHP scripts.

1『 PHP 3 继承的类里面的方法无法重构，即没法覆盖掉父类里同样名称的方法。另外一个缺点是对象在 PHP 脚本中被传递的方式并非最佳。第二个缺点目前无法完全理解。（2020-06-18）』

That objects were a marginal issue at this time is underlined by their lack of prominence in official documentation. The manual devoted one sentence and a code example to objects. The example did not illustrate inheritance or properties.

PHP 4 and the Quiet Revolution. If PHP 4 was yet another groundbreaking step for the language, most of the core changes took place beneath the surface. The Zend Engine (its name derived from Zeev and Andi) was written from scratch to power the language. The Zend Engine is one of the main components that drive PHP. Any PHP function you might care to call is in fact part of the high-level extensions layer. These do the busy work they were named for, like talking to database APIs or juggling strings for you. Beneath that, the Zend Engine manages memory, delegates control to other components, and translates the familiar PHP syntax you work with every day into runnable bytecode. It is the Zend Engine that we have to thank for core language features like classes.

1『 The Zend Engine 是 php 的核心组件，它在底层干了很多很多事。』

From our objective perspective, the fact that PHP 4 made it possible to override parent methods and access them from child classes was a major benefit. A major drawback remained, however. Assigning an object to a variable, passing it to a function, or returning it from a method resulted in a copy being made. Consider an assignment like this:

1『 php 4 在父类、子类上改进了很多，但还遗留一个大问题：对象的赋值并非绑定引用，而是赋值其值（又分配一块内存）。』

```php
$my_obj = new User('bob');
$other = $my_obj;
```

This resulted in the existence of two User objects rather than two references to the same User object. In most object-oriented languages, you would expect assignment by reference rather than by value. This means that you would pass and assign handles that point to objects rather than copy the objects themselves. The default pass-by-value behavior resulted in many obscure bugs as programmers unwittingly modified objects in one part of a script, expecting the changes to be seen via references elsewhere. Throughout this book, you will see many examples in which I maintain multiple references to the same object.

1『创建对象时，通过引用而非通过复制值，上面一段信息很重要。』

Luckily, there was a way of enforcing pass-by-reference, but it meant remembering to use a clumsy construction. Here’s how you would assign by reference:


```php
$other =& $my_obj;
// $other and $my_obj point to same object

// This enforces pass by reference:
function setSchool(& $school)    
    {  
    // $school is now a reference to not a copy of passed object    
    }

//And here is return by reference:
function & getSchool()    
    {        
    // returning a reference not a copy        
    return $this->school;    
    }

```

Although this worked fine, it was easy to forget to add the ampersand, and that meant it was all too easy for bugs to creep into object-oriented code. These were particularly hard to track down, because they rarely caused any reported errors, just plausible but broken behavior.

Coverage of syntax in general, and objects in particular, was extended in the PHP manual, and object-oriented coding began to bubble up to the mainstream. Objects in PHP were not uncontroversial (then, as now, no doubt), and threads like「Do I need objects?」were common flame-bait in mailing lists. Indeed, the Zend site played host to articles that encouraged object-oriented programming side-by-side with others that sounded a warning note. Pass-by-reference issues and controversy notwithstanding, many coders just got on and peppered their code with ampersand characters. Object-oriented PHP grew in popularity. Zeev Suraski wrote this in an article for DevX.com:

3『 [The Object-Oriented Evolution of PHP](http://www.devx.com/webdev/Article/10007) 』

One of the biggest twists in PHP’s history was that despite the very limited functionality, and despite a host of problems and limitations, object-oriented programming in PHP thrived and became the most popular paradigm for the growing numbers of off-the-shelf PHP applications. This trend, which was mostly unexpected, caught PHP in a suboptimal situation.  It became apparent that objects were not behaving like objects in other OO languages, and were instead behaving like [associative] arrays.

As noted in the previous chapter, interest in object-oriented design became obvious in sites and articles online. PHP’s official software repository, PEAR, itself embraced object-oriented programming. With hindsight, it’s easy to think of PHP’s adoption of object-oriented support as a reluctant capitulation to an inevitable force. It’s important to remember that, although object-oriented programming has been around since the 1960s, it really gained ground in the mid-1990s. Java, the great popularizer, was not released until 1995. A superset of C, a procedural language, C++ has been around since 1979. After a long evolution, it arguably made the leap to the big time during the 1990s. Perl 5 was released in 1994, another revolution within a formerly procedural language that made it possible for its users to think in objects (although some argue that Perl’s object-oriented support also felt like something of an afterthought). For a small procedural language, PHP developed its object support remarkably fast, showing a real responsiveness to the requirements of its users.

2『面向对象的概念是 1960 年代提出来的，但真正开始流行成主流是在 1990 年代中后期，java 是 1995 年发布，c++ 是 1990s 大改动（1979 年发布），Perl 5 是 1994 年发布，这些语言都是主流的面向对象语言。上面的时间点做一张计算机信息卡片。』

Change Embraced: PHP 5. PHP 5 represented an explicit endorsement of objects and object-oriented programming. That is not to say that objects were the only way to work with PHP (this book does not say that either, by the way). Objects were, however, recognized as a powerful and important means for developing enterprise systems, and PHP fully supported them in its core design.

1『之前 PHP 对面向对象很不情愿，PHP 5 开始拥抱面向对象。最重要的转变是从「复制对象」升级到了「传递引用」。除了这点，还有很多其他新特性，比如 private and protected methods and properties, the static keyword, namespaces, type hints (now called type declarations), and exceptions。PHP 是服役最长的版本，差不多 12 年。』

Arguably, one significant effect of the enhancements in PHP 5 was the adoption of the language by larger Internet companies. Both Yahoo! And Facebook, for example, started using PHP extensively within their platforms. With version 5, PHP became one of the standard languages for development and enterprise on the internet.

Objects had moved from afterthought to language driver. Perhaps the most important change was the default pass-by-reference behavior which replaced the evils of object copying. That was only the beginning, however. Throughout this book, and particularly in this part of it, we will encounter many more enhancements, including private and protected methods and properties, the static keyword, namespaces, type hints (now called type declarations), and exceptions. PHP 5 was around for a long time (about twelve years), and important new features were released incrementally.

PHP 5.3, for example, brought namespaces. These let you create a named scope for classes and functions, so that you are less likely to run into duplicate names as you include libraries and expand your system. They also rescue you from ugly but necessary naming conventions such as this:

```php
class megaquiz_util_Conf
{
}
```

Class names such as this are one way of preventing clashes between packages, but they can make for tortuous code. We have also seen support for closures, generators, traits, and late static bindings.

1『 php 竟然也支持闭包（closures）、迭代器（generators）、traits、静态绑定（static binding）。』

PHP 7: Closing the Gap. Programmers are a demanding lot. For many lovers of design patterns, there were two key features that PHP still lacked. These were scalar type declarations and enforced return types. With PHP 5 it was possible to enforce the type of an argument passed to a function or method, so long as you only needed to require an object, an array, or later, callable code. Scalar values (like integers, strings, and floats) could not be enforced at all. Furthermore, if you wanted to declare a method or a function’s return type, you were altogether out of luck.

1『PHP 7 最大的改进是：scalar type declarations and enforced return types. 』

As you will see, object-oriented design often uses a method declaration as a kind of contract. The method demands certain inputs and, reciprocally, it promises to give you a particular type of data back. PHP 5 programmers were forced to rely on comments, convention, and manual type checking to maintain contracts of this kind in many cases. Developers and commentators often complained about this. Here is a quote from the previous edition of this book:

…there is still no commitment to provide support for hinted return types. This would allow you to declare in a method or function’s declaration the object type that it returns. This would then be enforced by the PHP engine. Hinted return types would further improve PHP’s support for pattern principles (principles such as「code to an interface, not an implementation」). I hope one day to revise this book to cover that feature!

I’m pleased to write that the day has come! PHP 7 introduced scalar type declarations (previously known as type hints) and return type declarations, and you’ll see them used plenty in this edition. PHP 7 also provided other nice-to-haves, including anonymous classes and some namespace enhancements.

### 2.2 Advocacy and Agnosticism: The Object Debate

Objects and object-oriented design seem to stir passions on both sides of the enthusiasm divide. Many excellent programmers have produced excellent code for years without using objects, and PHP continues to be a superb platform for procedural web programming.

This book naturally displays an object-oriented bias throughout, a bias that reflects my object-infected outlook. Because this book is a celebration of objects, and an introduction to object-oriented design, it is inevitable that the emphasis is unashamedly object-oriented. Nothing in this book is intended, however, to suggest that objects are the one true path to coding success with PHP.

Whether a developer chose to work with PHP as an object-oriented language was once a matter of preference. This is still true to the extent that one can create perfectly acceptable working systems using functions and global code. Some great tools (e.g., WordPress) are still procedural in their underlying architecture (though even these may make extensive use of objects these days). It is, however, becoming increasingly hard to work as a PHP programmer without using and understanding PHP’s support for objects, not least because the third party libraries you are likely to rely upon in your projects will themselves likely be object-oriented.

1『很多地方看到这种观点：面向对象和面向 function，其实没有绝对的优劣，要看具体的应用场景。』

Still, as you read, it is worth bearing in mind the famous Perl motto,「There’s more than one way to do it.」This is especially true of smaller scripts, where quickly getting a working example up and running is more important than building a structure that will scale well into a larger system (scratch projects of this sort are often known as「spikes」).

Code is a flexible medium. The trick is to know when your quick proof of concept is becoming the root of a larger development, and to call a halt before lasting design decisions are made for you by the sheer weight of your code. Now that you have decided to take a design-oriented approach to your growing project, I hope that this book provides the help that you need to get started building object-oriented architectures.
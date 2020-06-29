# 2020082PHP-Objects-Patterns-PracticeR02

## 记忆时间

## 0105. Object Tools

In this chapter, I covered some of the techniques and tools that you can use to manage your libraries and classes. I explored PHP’s namespace feature. You saw that we can combine include paths, namespaces, autoload, and the file system to provide flexible organization for classes. We also examined PHP’s object and class functions, before taking things to the next level with the powerful Reflection API. Finally, we used the Reflection classes to build a simple example that illustrates one of the potential uses that Reflection has to offer.

As we have seen, PHP supports object-oriented programming through language constructs such as classes and methods. The language also provides wider support through functions and classes designed to help you work with objects. In this chapter, we will look at some tools and techniques that you can use to organize, test, and manipulate objects and classes.

This chapter will cover the following tools and techniques: 1) Namespaces: Organize your code into discrete package-like compartments. 2) Include paths: Setting central accessible locations for your library code. 3) Class and object functions: Functions for testing objects, classes, properties, and methods. 4) The Reflection API: A powerful suite of built-in classes that provide unprecedented access to class information at runtime.

### 5.1 PHP and Packages

A package is a set of related classes, usually grouped together in some way. Packages can be used to separate parts of a system from one another. Some programming languages formally recognize packages and provide them with distinct namespaces. PHP has no native concept of a package, but as of PHP 5.3, it introduced namespaces. I’ll look at this feature in the next section. I’ll also take a look at the old way of organizing classes into package-like structures.

#### 5.1.1 PHP Packages and Namespaces

Although PHP does not intrinsically support the concept of a package, developers have traditionally used both naming schemes and the filesystem to organize their code into package-like structures. 

Until PHP 5.3, developers were forced to name their files in a global context. In other words, if you named a class ShoppingBasket, it would become instantly available across your system. This caused two major problems. First, and most damaging, was the possibility of naming collisions. You might think that this is unlikely. After all, all you have to do is remember to give all your classes unique names, right? The trouble is, we all rely increasingly on library code. This is a good thing, of course, because it promotes code reuse. But assume your project does this:

```php
// listing 05.01

require_once __DIR__ . "/../useful/Outputter.php";
class Outputter {    
    // output data
}
```

Now assume you incorporate the included file at useful/Outputter.php:

```php
// listing 05.02

class Outputter{    //}
```

Well, you can guess what will happen, right? This happens:

```
PHP Fatal error:  Cannot declare class Outputter because the name is already in use in  /var/popp/src/ch05/batch01/useful/Outputter.php on line 4
```

Back before the introduction of namespaces, there was a conventional workaround to this problem. The answer was to prepend package names to class names, so that class names were guaranteed to be unique:

```php
// listing 05.03
// my/Outputer.php

require_once __DIR__ . "/../useful/Outputter.php";
class my_Outputter{    // output data}

// listing 05.04
// useful/Outputter.php

class useful_Outputter{    //}
```

The problem here was that, as projects got more involved, class names grew longer and longer. It was not an enormous problem, but it resulted in issues with code readability, and made it harder to hold classnames in your head while you worked. Many cumulative coding hours were lost to typos. If you’re maintaining legacy code, you may well still see code that follows this convention. For that reason, I’ll return briefly to the old way of handling packages later in this chapter.

## 0106. Objects and Design

In this chapter, I went beyond the nuts and bolts of object-oriented programming to look at some key design issues. I examined features such as encapsulation, loose coupling, and cohesion that are essential aspects of a flexible and reusable object-oriented system. I went on to look at the UML, laying groundwork that will be essential in working with patterns later in the book.

Now that we have seen the mechanics of PHP’s object support in some detail, we will step back from the details and consider how best to use the tools that we have encountered. In this chapter, I introduce you to some of the issues surrounding objects and design. I will also look at the UML, a powerful graphical language for describing object-oriented systems.

This chapter will cover the following topics: 1) Design basics: What I mean by design, and how object-oriented design differs from procedural code. 2) Class scope: How to decide what to include in a class. 3) Encapsulation: Hiding implementation and data behind a class’s interface. 4) Polymorphism: Using a common supertype to allow the transparent substitution of specialized subtypes at runtime. 5) The UML: Using diagrams to describe object-oriented architectures.

1『多态，使用一个共同的父类，允许在运行时透明地替换特定的子类。面向对象里，学会用「多态」去替换条件语句。（2020-06-29）』

### 6.1 Defining Code Design

One sense of code design concerns the definition of a system: the determination of a system’s requirements, scope, and objectives. What does the system need to do? For whom does it need to do it? What are the outputs of the system? Do they meet the stated need? On a lower level, design can be taken to mean the process by which you define the participants of a system and organize their relationships. This chapter is concerned with the second sense: the definition and disposition of classes and objects.

对「代码设计」的理解涉及系统的定义：确定系统的需求、作用域和目标。系统需要做什么？谁需要使用它？系统输出的内容是什么？系统可以满足一定的需求吗？从底层上看，设计是定义系统组成并组织各组件间关系的过程。本章从另一个角度考虑：类和对象的定义与配置。

So what is a participant? An object-oriented system is made up of classes. It is important to decide the nature of these players in your system. Classes are made up, in part, of methods; so in defining your classes, you must decide which methods belong together. As you will see, though, classes are often combined in inheritance relationships to conform to common interfaces. It is these interfaces, or types, that should be your first port of call in designing your system.

那么什么是系统的参与者呢？面向对象的系统由一系列类组成。决定系统中这些类的角色是非常重要的，而类由方法组成，所以在定义类时，必须决定哪些方法应该放在一起。另外，类与类之间常常通过继承关系联系起来以便遵循公用的接口。因此，这些接口或类型应该是设计系统时首先要考虑的。

There are other relationships that you can define for your classes. You can create classes that are composed of other types or that manage lists of other type instances. You can design classes that simply use other objects. The potential for such relationships of composition or use is built into your classes (e.g., through the use of type declarations in method signatures), but the actual object relationships take place at runtime, which can add flexibility to your design. You will see how to model these relationships in this chapter, and we’ll explore them further throughout the book.

As part of the design process, you must decide when an operation should belong to a type and when it should belong to another class used by the type. Everywhere you turn, you are presented with choices, decisions that might lead to clarity and elegance or might mire you in compromise. In this chapter, I will examine some issues that might influence a few of these choices.

你还可以为类定义其他关系。你可以创建由其他类型的对象组成的类，也可以创建用于管理多个其他对象实例的类。你还可以创建只是简单地用到其他对象的类。类之间的潜在关系往往在类的结构中就已经确定（例如类方法参数中的类型提示指定了要使用的对象类型），但是对象之间的实际关系只在代码执行时才产生，这些对象间的关系增加了代码的灵活性。在本章中，我们将看到如何为这些关系建立模型。在本书的后续章节中，我们还会深入研究。在设计过程中，必须决定某个操作何时属于某个类型，何时属于这个类型使用的另一个类。在每个地方你都面临选择，你的决定可能使代码更清晰、更优雅，也可能会让你陷入困境。

2『类之间的潜在关系往往在类的结构中就已经确定（例如类方法参数中的类型提示指定了要使用的对象类型），但是对象之间的实际关系只在代码执行时才产生，这些对象间的关系增加了代码的灵活性。在设计过程中，必须决定某个操作何时属于某个类型，何时属于这个类型使用的另一个类。在每个地方你都面临选择，你的决定可能使代码更清晰、更优雅，也可能会让你陷入困境。做一张任意卡片。』——已完成

### 6.2 Object-Oriented and Procedural Programming

How does object-oriented design differ from the more traditional procedural code? It is tempting to say that the primary distinction is that object-oriented code has objects in it. This is neither true nor useful. In PHP, you will often find procedural code using objects. You may also come across classes that contain tracts of procedural code. The presence of classes does not guarantee object-oriented design, even in a language such as Java, which forces you to do most things inside a class.

One core difference between object-oriented and procedural code can be found in the way that responsibility is distributed. Procedural code takes the form of a sequential series of commands and method calls. The controlling code tends to take responsibility for handling differing conditions. This top-down control can result in the development of duplications and dependencies across a project. Object-oriented code tries to minimize these dependencies by moving responsibility for handling tasks away from client code and toward the objects in the system.

面向对象和过程式编程的一个核心区别是如何分配职责。过程式编程表现为一系列命令和方法的连续调用。控制代码根据不同的条件执行不同的职责。这种自顶向下的控制方式导致了重复和相互依赖的代码遍布于整个项目。面向对象编程则将职责从客户端代码中移到专门的对象中，尽量减少相互依赖。

2『面向对象和面向过程的区别，做一张主题卡片。』——已完成

In this section, I’ll set up a simple problem and then analyze it in terms of both object-oriented and procedural code to illustrate these points. My project is to build a quick tool for reading from and writing to configuration files. In order to maintain focus on the structures of the code, I will omit implementation details in these examples. I’ll begin with a procedural approach to this problem. To start with, I will read and write text in this format:

key:value

I need only two functions for this purpose:

```php
// listing 06.01

function readParams(string $source): array {    
    $params = [];    // read text parameters from $source    
    return $params;
}

function writeParams(array $params, string $source) {    
    // write text parameters to $source
}
```

The readParams function requires the name of a source file. It attempts to open it, and reads each line, looking for key/value pairs. It builds up an associative array as it goes. Finally, it returns the array to the controlling code. writeParams() accepts an associative array and the path to a source file. It loops through the associative array, writing each key/value pair to the file. Here’s some client code that works with the functions:

```php
// listing 06.02

$file = __DIR__ . "/params.txt";
$params = [
    "key1" => "val1",    
    "key2" => "val2",    
    "key3" => "val3",
];
writeParams($params, $file);
$output = readParams($file);
print_r($output);
```

This code is relatively compact and should be easy to maintain. The writeParams() function is called to create param.txt and to write to it with something like this:

```
key1:val1key2:val2key3:val3
```

The readParams() function parses the same format. In many projects, scope grows and evolves. Let’s fake this by introducing a new requirement. The code must now also handle an XML structure that looks like this:

```html
<params>    
    <param>        
        <key>my key</key>        
        <val>my val</val>    
    </param>
</params>
```

The parameter file should be read in XML mode if the parameter file ends in .xml. Although this is not difficult to accommodate, it threatens to make my code much harder to maintain. I really have two options at this stage. I can check the file extension in the controlling code, or I can test inside my read and write functions. Here I go for the latter approach:

```php
// listing 06.03

function readParams(string $source): array {    
    $params = [];    
    if (preg_match("/\.xml$/i", $source)) {        
        // read XML parameters from $source    
    } else {         
        // read text parameters from $source    
    }    
    return $params;
}

function writeParams(array $params, string $source) {    
    if (preg_match("/\.xml$/i", $source)) {       
        // write XML parameters to $source    
     } else {        
        // write text parameters to $source    
     }
}
```

 ■ Note: illustrative code always involves a difficult balancing act. it needs to be clear enough to make its point, which often means sacrificing error checking and fitness for its ostensible purpose. in other words, the example here is really intended to illustrate issues of design and duplication rather than the best way to parse and write file data. For this reason, i omit implementation where it is not relevant to the issue at hand.

示例代码总是在寻求平街。它需要足够清晰以抓住要点，所以通常省略了错误检查。也就是说，这里的代码主要是说明设计和代码重复的问题，并不是提供解析和写入文件数据的最佳途径。因此，代码中忽略了与设计不相关的内容。

As you can see, I have had to use the test for the XML extension in each of the functions. It is this repetition that might cause us problems down the line. If I were to be asked to include yet another parameter format, I would need to remember to keep the readParams() and writeParams() functions in line with one another. 

Now I’ll address the same problem with some simple classes. First, I create an abstract base class that will define the interface for the type:

```php
// listing 06.04

abstract class ParamHandler {    
    protected $source;    
    protected $params = [];

    public function __construct(string $source)    {        
        $this->source = $source;    
    }

    public function addParam(string $key, string $val)    {        
        $this->params[$key] = $val;    
    }

    public function getAllParams(): array    {        
        return $this->params;    
    }

    public static function getInstance(string $filename): ParamHandler {        
        if (preg_match("/\.xml$/i", $filename)) {            
            return new XmlParamHandler($filename);        
        }        
        return new TextParamHandler($filename);    
    }    
    
    abstract public function write(): bool;    
    abstract public function read(): bool;
}
```

I define the addParam() method to allow the user to add parameters to the protected \$params property and getAllParams() to provide access to a copy of the array. I also create a static getInstance() method that tests the file extension and returns a particular subclass according to the results. Crucially, I define two abstract methods, read() and write(), ensuring that any subclasses will support this interface.

 ■ Note: placing a static method for generating child objects in the parent class is convenient. such a design decision has its own consequences, however. the ParamHandler type is now essentially limited to working with the concrete classes in this central conditional statement. What happens if you need to handle another format? Of course, if you are the maintainer of ParamHandler, you can always amend the getInstance() method. if you are a client coder, however, changing this library class may not be so easy (in fact, changing it won’t be hard, but you face the prospect of having to reapply your patch every time you reinstall the package that provides it). i will discuss issues of object creation in Chapter 9.

把一个用于生成子对象的静态方法放在父类中是很方便的，然而这样的设计也有不足之处。ParamHandler 类型现在只能与条件语句中规定的类一起工作。如果需要处理其他格式的文件，怎么办呢？当然，如果你是 ParamHandler 的维护者，可以修改 getinstance() 方法。但是如果你只是这段代码的使用者，修改这个类就不是那么容易了（实际上，修改它并不难，但是每次重新安装这个包的时候都需要再次修改）。我们将会在第 9 章中讨论对象创建的问题。

1『哇塞，这里的知识点醍醐灌顶，代码的可维护性不仅仅要从开发者的角度考虑，有时候得站在使用者的角度。』

Now, I’ll define the subclasses, once again omitting the details of implementation to keep the example clean:

```php
// listing 06.05

class XmlParamHandler extends ParamHandler {    
    public function write(): bool    {        
        // write XML        
        // using $this->params    
    }

    public function read(): bool    {        
        // read XML        
        // and populate $this->params    
    }
}

// listing 06.06

class TextParamHandler extends ParamHandler {    
    public function write(): bool    {        
        // write text        
        // using $this->params    
    }

    public function read(): bool    {        
        // read text        
        // and populate $this->params    
    }
}
```

These classes simply provide implementations of the write() and read() methods. Each class will write and read according to the appropriate format. Client code will write to both text and XML formats entirely transparently, according to the file extension:

```php
// listing 06.07

$test = ParamHandler::getInstance(__DIR__ . "/params.xml");
$test->addParam("key1", "val1");
$test->addParam("key2", "val2");
$test->addParam("key3", "val3");
$test->write(); // writing in XML format
```

We can also read from either file format:

```
// listing 06.08

$test = ParamHandler::getInstance(__DIR__ . "/params.txt");
$test->read(); // reading in text format
$params = $test->getAllParams();
print_r($params);
```

So, what can we learn from these two approaches?

#### 6.2.1 Responsibility

The controlling code in the procedural example takes responsibility for deciding about format—not once, but twice. The conditional code is tidied away into functions, certainly, but this merely disguises the fact of a single flow, making decisions as it goes. Calls to readParams() and to writeParams() take place in different contexts, so we are forced to repeat the file extension test in each function (or to perform variations on this test().

In the object-oriented version, this choice about file format is made in the static getInstance() method, which tests the file extension only once, serving up the correct subclass. The client code takes no responsibility for implementation. It uses the provided object with no knowledge of, or interest in, the particular subclass it belongs to. It knows only that it is working with a ParamHandler object, and that it will support write() and read(). While the procedural code busies itself about details, the object-oriented code works only with an interface, unconcerned about the details of implementation. Because responsibility for implementation lies with the objects and not with the client code, it would be easy to switch in support for new formats transparently.

在过程式编程的例子中，控制代码的职责是判断文件格式，它判断了两次而不是一次。条件语句被绑定到函数中，但这仅是将判断的流程隐藏起来。对 readparams() 的调用和对 writeparams() 的调用必须发生在不同的地方，因此我们不得不在每个函数中重复检测文件扩展名（或执行其他检测操作）。在面向对象代码中，我们在静态方法 getinstance() 中进行文件格式的选择，并且仅在 getinstance() 中检测文件扩展名一次，就可以决定使用哪一个合适的子类。客户端代码并不负责实现读写功能。它不需要知道自己属于哪个子类就可以使用给定的对象。它只需要知道自己正在使用 Paramhandler 对象，并且 Paramhandler 对象支持 write() 和 read() 方法。过程式代码忙于处理细节，而面向对象代码只需一个接口即可工作，并且不用考虑实现的细节。由于实现由对象负责，而不是由客户端代码负贵，所以我们能够很方便地增加对新格式的支持。

#### 6.2.2 Cohesion

Cohesion is the extent to which proximate procedures are related to one another. Ideally, you should create components that share a clear responsibility. If your code spreads related routines widely, you will find them harder to maintain as you have to hunt around to make changes.

Our ParamHandler classes collect related procedures into a common context. The methods for working with XML share a context in which they can share data and where changes to one method can easily be reflected in another if necessary (e.g., if you needed to change an XML element name). The ParamHandler classes can therefore be said to have high cohesion. The procedural example, on the other hand, separates related procedures. The code for working with XML is spread across functions.

内聚（cohesion）是一个模块内部各成分之间相关联程度的度量。理想情况下，你应该使各组件职责清晰、分工明确。如果代码间的关联范围太广，维护就会很困难，因为你需要在修改某部分代码的同时修改相关的代码。前面的 Paramhandler 类将相关的处理过程集中起来。用于处理 XML 的类方法间可以共享数据，并且一个类方法中的改变可以很容易地反映到另一个方法中（比如改变 XML 元素名）。因此，我们可以说 Paramhandler 类是高度内聚的。另一方面，过程式的例子则把相关的过程分离开，导致处理 XML 的代码在多个函数中同时出现。

#### 6.2.3 Coupling

Tight coupling occurs when discrete parts of a system’s code are tightly bound up with one another so that a change in one part necessitates changes in the others. Tight coupling is by no means unique to procedural code, though the sequential nature of such code makes it prone to the problem.

You can see this kind of coupling in the procedural example. The writeParams() and readParams() functions run the same test on a file extension to determine how they should work with data. Any change in logic you make to one will have to be implemented in the other. If you were to add a new format, for example, you would have to bring the functions into line with one another, so that they both implement a new file extension test in the same way. This problem can only get worse as you add new parameter-related functions.

The object-oriented example decouples the individual subclasses from one another and from the client code. If you were required to add a new parameter format, you could simply create a new subclass, amending a single test in the static getInstance() method.

当系统各部分代码紧密绑在一起时，就会产生紧密耦合，这时在一个组件中的变化会迫使其他部件随之改变。紧密耦合并不是过程式代码特有的，但是过程式代码比较容易产生耦合问题。我们可以在过程式示例中看到耦合的产生。在writeparams() 和 readparams() 函数中，使用了相同的文件扩展名测试来决定如何处理数据。因此，我们要改写一个函数，就不得不同时改写另一个函数。例如，如果要增加一种新的文件格式，就要在两个函数中按相同的方式都加上相应的扩展名检査代码，这样两个函数才能保持一致。当我们要新增参数相关的函数时，问题只会更复杂。面向对象的示例中则将每个子类彼此分开，也将其与客户端代码分开。如果需要增加新的参数格式，只需简单地创建相应的子类，并在父类的静态方法 getinstance() 中增加一行文件检测代码即可。

#### 6.2.4 Orthogonality

The killer combination of components with tightly defined responsibilities that are also independent from the wider system is sometimes referred to as orthogonality. Andrew Hunt and David Thomas discuss this subject in their book, The Pragmatic Programmer: From Journeyman to Master (Addison-Wesley Professional, 1999).

Orthogonality, it is argued, promotes reuse in that components can be plugged into new systems without needing any special configuration. Such components will have clear inputs and outputs, independent of any wider context. Orthogonal code makes change easier because the impact of altering an implementation will be localized to the component being altered. Finally, orthogonal code is safer. The effects of bugs should be limited in scope. An error in highly interdependent code can easily cause knock-on effects in the wider system.

There is nothing automatic about loose coupling and high cohesion in a class context. We could, after all, embed our entire procedural example into one misguided class. So how can we achieve this balance in our code? I usually start by considering the classes that should live in my system.

正交（orthogonality）指将职责相关的组件紧紧组合在一起，而与外部系统环境隔开，保持独立。Andrew Hunt 和 David Thomas 在 The Pragmatic Programmer 一书（Addison- Wesley, 1999） 中有所介绍。正交主张重用组件，期望不需要任何特殊配置就能把一个组件插入到新系统中。这样的组件有明确的与环境无关的输入和输出。正交代码使修改变得更简单，因为修改一个实现只会影响到被改动的组件本身。最后，正交代码更加安全。bug 的影响只局限于它的作用域之中。内部高度相互依赖的代码发生错误时，很容易在系统中引起连锁反应。如果只有一个类，松散耦合和高聚合是无从谈起的。毕竟，我们可以把整个过程式示例的全部代码塞到一个被误导的类里。因此，我们如何才能在代码中达到一个平衡呢？通常，首先考虑哪些类应该存在于系统之中。

2『 The Pragmatic Programmer 这本书已经出新版了，已下载「2020120The-Pragmatic-Programmer2Ed」。』

### 6.3 Choosing Your Classes

It can be surprisingly difficult to define the boundaries of your classes, especially as they will evolve with any system that you build.

It can seem straightforward when you are modeling the real world. Object-oriented systems often feature software representations of real things—Person, Invoice, and Shop classes abound. This would seem to suggest that defining a class is a matter of finding the things in your system and then giving them agency through methods. This is not a bad starting point, but it does have its dangers. If you see a class as a noun, a subject for any number of verbs, then you may find it bloating as ongoing development and requirement changes call for it to do more and more things.

模拟真实世界是比较直接的办法。面向对象系统经常反映真实的事物 Person、Invoice 和 shop 类等，即定义一个类就是找到系统中的事物，然后通过方法给予它们动作。这个想法不错，但也有不足之处。如果把类看做名词：一系列动作的执行者，那么随着开发和需求的改变，你会发现它因为需要而做越来越多的事情。

Let’s consider the ShopProduct example that we created in Chapter 3. Our system exists to offer products to a customer, so defining a ShopProduct class is an obvious choice. But is that the only decision we need to make? We provide methods such as getTitle() and getPrice() for accessing product data. When we are asked to provide a mechanism for outputting summary information for invoices and delivery notes, it seems to make sense to define a write() method. When the client asks us to provide the product summaries in different formats, we look again at our class. We duly create writeXML() and writeHTML() methods in addition to the write() method. Or we add conditional code to write() to output different formats, according to an option flag.

Either way, the problem here is that the ShopProduct class is now trying to do too much. It is struggling to manage strategies for display, as well as for managing product data.

我们回顾一下在第 3 章中创建的 ShopProduct。系统为了给顾客提供产品，因此要定义一个 ShopProduct 类，但是这是唯一的办法吗？为了访问产品数据，我们需要提供诸如 getTitle() 和 getPrice() 等方法。当我们需要输出发票和提货单的摘要信息时，需要定义 write() 方法。当顾客要求得到不同格式的产品摘要信息时，除了创建 write() 方法之外，还要创建 writeXML() 和 writeHTML() 方法。否则，需要增加条件代码到 write() 中并根据选项标志输出不同格式。无论哪一种方式，ShopProduct 类现在做了太多的事情。它忙着管理显示方案及产品数据。

How should you think about defining classes? The best approach is to think of a class as having a primary responsibility and to make that responsibility as singular and focused as possible. Put the responsibility into words. It has been said that you should be able to describe a class’s responsibility in 25 words or less, rarely using the words「and」or「or.」If your sentence gets too long or mired in clauses, it is probably time to consider defining new classes along the lines of some of the responsibilities you have described.

So, ShopProduct classes are responsible for managing product data. If we add methods for writing to different formats, we begin to add a new area of responsibility: product display. As you saw in Chapter 3, we actually defined two types based on these separate responsibilities. The ShopProduct type remained responsible for product data, and the ShopProductWriter type took on responsibility for displaying product information. Individual subclasses refined these responsibilities.

我们应该如何定义类呢？最好的办法是让一个类只有一个主要的职责，并且任务要尽可能独立。你可以把类的职责用多个词来形容，最好不超过 25 个词，不要用到词「且」或者「或」。如果句子太长或者有复杂的子句，就应该考虑用你所描述的一部分任务来定义新类。因此，ShopProduct 类应该主要负责处理产品数据。如果我们显示不同格式的摘要信息，则有了一个新的职责：产品显示。正如第 3 章所述，我们实际上基于这两个不同的职责定义了两个类型：ShopProduct 类型负责处理产品数据；ShopProductWriter 类型负责显示产品信息。每个类只承担自己的任务。

 ■ Note:  Very few design rules are entirely inflexible. You will sometimes see code for saving object data in an otherwise unrelated class, for example. although this would seem to violate the rule that a class should have a singular responsibility, it can be the most convenient place for the functionality to live because a method has to have full access to an instance’s fields. Using local methods for persistence can also save us from creating a parallel hierarchy of persistence classes mirroring our savable classes, and thereby introducing unavoidable coupling. We deal with other strategies for object persistence in Chapter 12. avoid religious adherence to design rules; they are not a substitute for analyzing the problem before you. try to remain alive to the reasoning behind the rule, and emphasize that over the rule itself.

设计原则并非一成不变。比如，有时你会看到在另一个不相关的类中出现了保存对象数据的代码。这似乎违反了类应该有单一职责的原则，但事实上，这样做可以为类方法完全访问对象实例的属性提供最大的便利。使用本地方法进行对象持久化也可让我们不用创建与被保存的相对应的持久化美，避免产生依赖。我们会在第 12 章中介绍更多对象持久化的策略。记住要避免对于设计原则的宗教性崇拜。设计原则并不能代替你来分析问题。要掌提设计原则背后的内涵，这比设计原则本身史为重要。








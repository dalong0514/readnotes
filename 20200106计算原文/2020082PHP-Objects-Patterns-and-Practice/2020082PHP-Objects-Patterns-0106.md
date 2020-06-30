# 0106. Objects and Design

Now that we have seen the mechanics of PHP’s object support in some detail, we will step back from the details and consider how best to use the tools that we have encountered. In this chapter, I introduce you to some of the issues surrounding objects and design. I will also look at the UML, a powerful graphical language for describing object-oriented systems.

This chapter will cover the following topics:

Design basics: What I mean by design, and how object-oriented design differs from procedural code.

Class scope: How to decide what to include in a class.

Encapsulation: Hiding implementation and data behind a class’s interface.

Polymorphism: Using a common supertype to allow the transparent substitution of specialized subtypes at runtime.

The UML: Using diagrams to describe object-oriented architectures.

## 6.1 Defining Code Design

One sense of code design concerns the definition of a system: the determination of a system’s requirements, scope, and objectives. What does the system need to do? For whom does it need to do it? What are the outputs of the system? Do they meet the stated need? On a lower level, design can be taken to mean the process by which you define the participants of a system and organize their relationships. This chapter is concerned with the second sense: the definition and disposition of classes and objects.

对「代码设计」的理解涉及系统的定义：确定系统的需求、作用域和目标。系统需要做什么？谁需要使用它？系统输出的内容是什么？系统可以满足一定的需求吗？从底层上看，设计是定义系统组成并组织各组件间关系的过程。本章从另一个角度考虑：类和对象的定义与配置。

So what is a participant? An object-oriented system is made up of classes. It is important to decide the nature of these players in your system. Classes are made up, in part, of methods; so in defining your classes, you must decide which methods belong together. As you will see, though, classes are often combined in inheritance relationships to conform to common interfaces. It is these interfaces, or types, that should be your first port of call in designing your system.

那么什么是系统的参与者呢？面向对象的系统由一系列类组成。决定系统中这些类的角色是非常重要的，而类由方法组成，所以在定义类时，必须决定哪些方法应该放在一起。另外，类与类之问常常通过继承关系联系起来以便遵循公用的接口。因此，这些接口或类型应该是设计系统时首先要考虑的。

There are other relationships that you can define for your classes. You can create classes that are composed of other types or that manage lists of other type instances. You can design classes that simply use other objects. The potential for such relationships of composition or use is built into your classes (e.g., through the use of type declarations in method signatures), but the actual object relationships take place at runtime, which can add flexibility to your design. You will see how to model these relationships in this chapter, and we’ll explore them further throughout the book.

As part of the design process, you must decide when an operation should belong to a type and when it should belong to another class used by the type. Everywhere you turn, you are presented with choices, decisions that might lead to clarity and elegance or might mire you in compromise. In this chapter, I will examine some issues that might influence a few of these choices.

你还可以为类定义其他关系。你可以创建由其他类型的对象组成的类，也可以创建用于管理多个其他对象实例的类。你还可以创建只是简单地用到其他对象的类。类之间的潜在关系往往在类的结构中就已经确定（例如类方法参数中的类型提示指定了要使用的对象类型），但是对象之间的实际关系只在代码执行时才产生，这些对象间的关系增加了代码的灵活性。在本章中，我们将看到如何为这些关系建立模型。在本书的后续章节中，我们还会深入研究。在设计过程中，必须决定某个操作何时属于某个类型，何时属于这个类型使用的另一个类。在每个地方你都面临选择，你的决定可能使代码更清晰、更优雅，也可能会让你陷入困境。

## 6.2 Object-Oriented and Procedural Programming

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

### 6.2.1 Responsibility

The controlling code in the procedural example takes responsibility for deciding about format—not once, but twice. The conditional code is tidied away into functions, certainly, but this merely disguises the fact of a single flow, making decisions as it goes. Calls to readParams() and to writeParams() take place in different contexts, so we are forced to repeat the file extension test in each function (or to perform variations on this test().

In the object-oriented version, this choice about file format is made in the static getInstance() method, which tests the file extension only once, serving up the correct subclass. The client code takes no responsibility for implementation. It uses the provided object with no knowledge of, or interest in, the particular subclass it belongs to. It knows only that it is working with a ParamHandler object, and that it will support write() and read(). While the procedural code busies itself about details, the object-oriented code works only with an interface, unconcerned about the details of implementation. Because responsibility for implementation lies with the objects and not with the client code, it would be easy to switch in support for new formats transparently.

在过程式编程的例子中，控制代码的职责是判断文件格式，它判断了两次而不是一次。条件语句被绑定到函数中，但这仅是将判断的流程隐藏起来。对 readparams() 的调用和对 writeparams() 的调用必须发生在不同的地方，因此我们不得不在每个函数中重复检测文件扩展名（或执行其他检测操作）。在面向对象代码中，我们在静态方法 getinstance() 中进行文件格式的选择，并且仅在 getinstance() 中检测文件扩展名一次，就可以决定使用哪一个合适的子类。客户端代码并不负责实现读写功能。它不需要知道自己属于哪个子类就可以使用给定的对象。它只需要知道自己正在使用 Paramhandler 对象，并且 Paramhandler 对象支持 write() 和 read() 方法。过程式代码忙于处理细节，而面向对象代码只需一个接口即可工作，并且不用考虑实现的细节。由于实现由对象负责，而不是由客户端代码负贵，所以我们能够很方便地增加对新格式的支持。

### 6.2.2 Cohesion

Cohesion is the extent to which proximate procedures are related to one another. Ideally, you should create components that share a clear responsibility. If your code spreads related routines widely, you will find them harder to maintain as you have to hunt around to make changes.

Our ParamHandler classes collect related procedures into a common context. The methods for working with XML share a context in which they can share data and where changes to one method can easily be reflected in another if necessary (e.g., if you needed to change an XML element name). The ParamHandler classes can therefore be said to have high cohesion. The procedural example, on the other hand, separates related procedures. The code for working with XML is spread across functions.

内聚（cohesion）是一个模块内部各成分之间相关联程度的度量。理想情况下，你应该使各组件职责清晰、分工明确。如果代码间的关联范围太广，维护就会很困难，因为你需要在修改某部分代码的同时修改相关的代码。前面的 Paramhandler 类将相关的处理过程集中起来。用于处理 XML 的类方法间可以共享数据，并且一个类方法中的改变可以很容易地反映到另一个方法中（比如改变 XML 元素名）。因此，我们可以说 Paramhandler 类是高度内聚的。另一方面，过程式的例子则把相关的过程分离开，导致处理 XML 的代码在多个函数中同时出现。

### 6.2.3 Coupling

Tight coupling occurs when discrete parts of a system’s code are tightly bound up with one another so that a change in one part necessitates changes in the others. Tight coupling is by no means unique to procedural code, though the sequential nature of such code makes it prone to the problem.

You can see this kind of coupling in the procedural example. The writeParams() and readParams() functions run the same test on a file extension to determine how they should work with data. Any change in logic you make to one will have to be implemented in the other. If you were to add a new format, for example, you would have to bring the functions into line with one another, so that they both implement a new file extension test in the same way. This problem can only get worse as you add new parameter-related functions.

The object-oriented example decouples the individual subclasses from one another and from the client code. If you were required to add a new parameter format, you could simply create a new subclass, amending a single test in the static getInstance() method.

当系统各部分代码紧密绑在一起时，就会产生紧密耦合，这时在一个组件中的变化会迫使其他部件随之改变。紧密耦合并不是过程式代码特有的，但是过程式代码比较容易产生耦合问题。我们可以在过程式示例中看到耦合的产生。在writeparams() 和 readparams() 函数中，使用了相同的文件扩展名测试来决定如何处理数据。因此，我们要改写一个函数，就不得不同时改写另一个函数。例如，如果要增加一种新的文件格式，就要在两个函数中按相同的方式都加上相应的扩展名检査代码，这样两个函数才能保持一致。当我们要新增参数相关的函数时，问题只会更复杂。面向对象的示例中则将每个子类彼此分开，也将其与客户端代码分开。如果需要增加新的参数格式，只需简单地创建相应的子类，并在父类的静态方法 getinstance() 中增加一行文件检测代码即可。

### 6.2.4 Orthogonality

The killer combination of components with tightly defined responsibilities that are also independent from the wider system is sometimes referred to as orthogonality. Andrew Hunt and David Thomas discuss this subject in their book, The Pragmatic Programmer: From Journeyman to Master (Addison-Wesley Professional, 1999).

Orthogonality, it is argued, promotes reuse in that components can be plugged into new systems without needing any special configuration. Such components will have clear inputs and outputs, independent of any wider context. Orthogonal code makes change easier because the impact of altering an implementation will be localized to the component being altered. Finally, orthogonal code is safer. The effects of bugs should be limited in scope. An error in highly interdependent code can easily cause knock-on effects in the wider system.

There is nothing automatic about loose coupling and high cohesion in a class context. We could, after all, embed our entire procedural example into one misguided class. So how can we achieve this balance in our code? I usually start by considering the classes that should live in my system.

正交（orthogonality）指将职责相关的组件紧紧组合在一起，而与外部系统环境隔开，保持独立。Andrew Hunt 和 David Thomas 在 The Pragmatic Programmer 一书（Addison- Wesley, 1999） 中有所介绍。正交主张重用组件，期望不需要任何特殊配置就能把一个组件插入到新系统中。这样的组件有明确的与环境无关的输入和输出。正交代码使修改变得更简单，因为修改一个实现只会影响到被改动的组件本身。最后，正交代码更加安全。bug 的影响只局限于它的作用域之中。内部高度相互依赖的代码发生错误时，很容易在系统中引起连锁反应。如果只有一个类，松散耦合和高聚合是无从谈起的。毕竟，我们可以把整个过程式示例的全部代码塞到一个被误导的类里。因此，我们如何才能在代码中达到一个平衡呢？通常，首先考虑哪些类应该存在于系统之中。

2『 The Pragmatic Programmer 这本书已经出新版了，已下载「2020120The-Pragmatic-Programmer2Ed」。』

在理想的正交情况下，任何操作都没有副作用。每个组件发生的改变都只影响到其自身。一一译者注

## 6.3 Choosing Your Classes

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

## 6.4 Polymorphism

Polymorphism, or class switching, is a common feature of object-oriented systems. You have encountered it several times already in this book. Polymorphism is the maintenance of multiple implementations behind a common interface. This sounds complicated, but in fact, it should be very familiar to you by now. The need for polymorphism is often signaled by the presence of extensive conditional statements in your code.

如果代码中存在大量条件语句，就说明需要使用多态。

When I first created the ShopProduct class in Chapter 3, I experimented with a single class which managed functionality for books and CDs, in addition to generic products. In order to provide summary information, I relied on a conditional statement:

```php
// listing 03.31

public function getSummaryLine()    {        
    $base  = "{$this->title} ( {$this->producerMainName}, ";        
    $base .= "{$this->producerFirstName} )";        
    if ($this->type == 'book') {            
        $base .= ": page count - {$this->numPages}";        
    } elseif ($this->type == 'cd') {
        $base .= ": playing time - {$this->playLength}";        
    }        
    return $base;    
}
```

These statements suggested the shape for the two subclasses: CdProduct and BookProduct. By the same token, the conditional statements in my procedural parameter example contained the seeds of the object-oriented structure I finally arrived at. I repeated the same condition in two parts of the script:

同样，在上文面向过程的例子中我们也使用了条件语句，这些语句中暗含了我们最终要实现的面向对象结构的萌芽。我们在代码的两个部分重复使用相同的条件语句。

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

Each clause suggested one of the subclasses I finally produced: XmlParamHandler and TextParamHandler. These extended the abstract base class ParamHandler’s write() and read() methods:

```php
// listing 06.09
// could return XmlParamHandler or TextParamHandler

$test = ParamHandler::getInstance($file);
$test->read();  // could be XmlParamHandler::read() or TextParamHandler::read()
$test->addParam("newkey1", "newval1");
$test->write(); // could be XmlParamHandler::write() or TextParamHandler::write()
```

It is important to note that polymorphism doesn’t banish conditionals. Methods such as ParamHandler::getInstance() will often determine which objects to return based on switch or if statements. These tend to centralize the conditional code into one place, though.

As you have seen, PHP enforces the interfaces defined by abstract classes. This is useful because we can be sure that a concrete child class will support exactly the same method signatures as those defined by an abstract parent. This includes type declarations and access controls. Client code can, therefore, treat all children of a common superclass interchangeably (as long it only relies on only functionality defined in the parent).

就像我们看到的那样，PHP 强制接口由抽象类定义。这非常有用，因为我们可以确定子类将会实现抽象父类中定义的所有方法，包括类类型提示和方法的访问控制。客户端代码因此可以使用一个公共父类的任意子类而不需要改写代码（只要客户端代码仅依赖于父类中定义的功能）。这个规则唯一的缺憾是：无法强制规定类方法返回的数据类型。

1『 PHP 7 已经支持返回特定的数据类型了。（2020-06-30）』

## 6.5 Encapsulation

Encapsulation simply means the hiding of data and functionality from a client. And once again, it is a key object-oriented concept.

On the simplest level, you encapsulate data by declaring properties private or protected. By hiding a property from client code, you enforce an interface and prevent the accidental corruption of an object’s data. Polymorphism illustrates another kind of encapsulation. By placing different implementations behind a common interface, you hide these underlying strategies from the client. This means that any changes that are made behind this interface are transparent to the wider system. You can add new classes or change the code in a class without causing errors. The interface is what matters, not the mechanisms working beneath it. The more independent these mechanisms are kept, the less chance that changes or repairs will have a knock-on effect in your projects.

要实现封装，最简单的办法是将属性定义为 private 或 protected。通过对客户端代码隐藏属性，我们创建了一个接口并防止在偶然情况下污染对象中的数据。多态是另外一种封装。通过把不同的实现放在公共接口之后，我们对客户端代码隐藏了功能的实现。也就是说，任何在接口背后发生的改变对外界的系统来说都是可忽略的。我们可以增加新类或改变类中的代码，而不会产生错误。接口与其背后的工作机制是分开来的。这些机制越独立，改进或修正代码对系统的影响越小。

Encapsulation is, in some ways, the key to object-oriented programming. Your objective should be to make each part as independent as possible from its peers. Classes and methods should receive as much information as is necessary to perform their allotted tasks, which should be limited in scope and clearly identified. The introduction of the private, protected, and public keywords have made encapsulation easier. 

Encapsulation is also a state of mind, though. PHP 4 provided no formal support for hiding data. Privacy had to be signaled using documentation and naming conventions. An underscore, for example, is a common way of signaling a private property:

从某种程度上说，封装是面向对象编程的关键。我们的目标是使系统中的每一部分都尽可能独立。类和方法应当能够接收到足够的信息来执行它们承担的任务，而这些任务应该非常清晰，有明确的定义和范围。在 PHP 5 中，private、protected 和 public 关键字的引入使封装变得容易。尽管如此，在使用封裝时还是要深思熟虑。但 PHP 4 并没有正式支持隐藏数据，你不得不使用文档和命名惯例来说明数据的隐私性。例如，以下划线开头的属性通常是私有属性：

```php
var $_touchezpas;
```

Code had to be checked closely, of course, because privacy was not strictly enforced. Interestingly, though, errors were rare because the structure and style of the code made it pretty clear which properties wanted to be left alone. By the same token, even after PHP 5 arrived, we could break the rules and discover the exact subtype of an object that we were using in a class-switching context simply by using the instanceof operator:

```php
function workWithProducts(ShopProduct $prod)    {        
    if ($prod instanceof CdProduct) {            
        // do cd thing        
    } else if ($prod instanceof BookProduct) {            
        // do book thing        
    }    
}
```

You may have a very good reason to do this, but, in general, it carries a slightly uncertain odor. By querying the specific subtype in the example, I am setting up a dependency. Although the specifics of the subtype were hidden by polymorphism, it would have been possible to have changed the ShopProduct inheritance hierarchy entirely with no ill effects. This code ends that. Now, if I need to rationalize the CdProduct and BookProduct classes, I may create unexpected side effects in the workWithProducts() method.

There are two lessons to take away from this example. First, encapsulation helps you to create orthogonal code. Second, the extent to which encapsulation is enforceable is beside the point. Encapsulation is a technique that should be observed equally by classes and their clients.

1『 Encapsulation is a technique that should be observed equally by classes and their clients. 有关封装的第二个说明事项目前还理解不了。（2020-06-30）』

这样做通常有很好的理由，但通常来说会带来一些不确定的因素。在代码中査询特定子类型时会产生一个依赖关系。如果我们利用多态来隐藏特定子类型的特性，ShopProduct 的继承关系改变时就不会产生任何错误。但上面的代码会破坏这种情况。使用上面的代码时，如果我们改写了 CdProduct 和 BookProduct 类，就有可能在 workwithproducts() 方法中产生预想不到的错误。

这个例子说明了两件事。首先，封装可以帮助我们创建正交的代码。其次，封装的范围不怎么重要，无论封装的规模是大是小，类和客户端代码都必须同时关注封装的实现。

## 6.6 Forget How to Do It

If you are like me, the mention of a problem will set your mind racing, looking for mechanisms that might provide a solution. You might select functions that will address an issue, revisit clever regular expressions, track down Composer packages. You probably have some pasteable code in an old project that does something somewhat similar. At the design stage, you can profit by setting all that aside for a while. Empty your head of procedures and mechanisms.

如果你和我一样，可能会一遇到问题就开始努力寻找解决办法：设计函数来解决一个问题，或构造一个正则表达式，或者下载 Composer 包，或者可能会从旧的项目中寻找解决类似问题的代码来使用。在设计阶段，让大脑空自一段时间会给你带来意想不到的好处。清清空脑海中这些和细节相关的念头。

Think only about the key participants of your system: the types it will need and their interfaces. Of course, your knowledge of process will inform your thinking. A class that opens a file will need a path, database code will need to manage table names and passwords, and so on. Let the structures and relationships in your code lead you, though. You will find that the implementation falls into place easily behind a well-defined interface. You then have the flexibility to switch out, improve, or extend an implementation should you need to, without affecting the wider system.

1『做好接口 -> 实现 -> 重构。』

你可以只考虑系统中的关键参与者：项目需要的对象类型和这些对象的接口。当然，你的经验会告诉你如何思考：一个打开文件的类需要一个路径，数据库代码需要管理表名和密码等。但最好不要被经验所左右，而要让代码中的结构和关系来引导你，你会发现在一个定义良好的接口之后加入实现代码是很容易的。接着你可以灵活地选择、改进或扩展一个可能需要的实现，而不会影响到外界的系统。

In order to emphasize interface, think in terms of abstract base classes rather than concrete children. In my parameter-fetching code, for example, the interface is the most important aspect of the design. I want a type that reads and writes name/value pairs. It is this responsibility that is important about the type, not the actual persistence medium or the means of storing and retrieving data. I design the system around the abstract ParamHandler class, and only add in the concrete strategies for actually reading and writing parameters later on. In this way, I build both polymorphism and encapsulation into my system from the start. The structure lends itself to class switching.

为了强调接口，我们按抽象基类而不是具体的子类来思考。例如，在之前的参数读取示例代码中，接口是设计中最重要的部分。我们需要一个可以读写键值对的对象类型。对于该对象类型来说，读写键/值对就是最重要的职责，而不是持久存储或获取数据。我们围绕着抽象类 ParamHandler 来设计系统，并只为实际读写需要增加具体的处理方案。用这种方法，我们一开始就在系统中使用了多态和封装。这个结构也具有类切换的能力。

Having said that, of course, I knew from the start that there would be text and XML implementations of ParamHandler, and there is no question that this influenced my interface. There is always a certain amount of mental juggling to do when designing interfaces.

In Design Patterns: Elements of Reusable Object-Oriented Software (Addison-Wesley Professional, 1995), the Gang of Four summed up this principle with the phrase,「Program to an interface, not an implementation.」It is a good one to add to your coder’s handbook.

我们一开始就已经知道将会有文本和 XML 两种类型的 Paramhandler 实现，这毫无疑问会影响我们对于接口的设计。这些具体的实现有可能会干扰到我们设计出抽象的接口，因为我们思考的东西增加了。设计接口的时候我们或多或少总得花一番心思。「四人组」在《设计模式》一书中用一句话总结了这个规则——「为接口而不是实现而编程」（Program to an interface, not an implementation）。

设计软件的时候，克服复杂度是一个非常重要的原则。我们应尽量减少同一时间在脑中思考的对象，要能分清主次，把问题抽象出来。所谓的「心智把戏」，指的是权衡哪些东西是真正需要放到系统中的过程。Code Complete 一书中有涉及相关话题。一一译者注

## 6.7 Four Signposts

Very few people get it absolutely right at the design stage. Most of us amend our code as requirements change or as we gain a deeper understanding of the nature of the problem we are addressing. As you amend your code, it can easily drift beyond your control. A method is added here and a new class there, and gradually your system begins to decay. As you have seen already, your code can point the way to its own improvement. These pointers in code are sometimes referred to as code smells—that is, features in code that may suggest particular fixes or at least call you to look again at your design. In this section, I distill some of the points already made into four signs that you should watch out for as you code.

Code Duplication. Duplication is one of the great evils in code. If you get a strange sense of déjà vu as you write a routine, chances are you have a problem. Take a look at the instances of repetition in your system. Perhaps they belong together. Duplication generally means tight coupling. If you change something fundamental about one routine, will the similar routines need amendment? If this is the case, they probably belong in the same class.

The Class Who Knew Too Much. It can be a pain passing parameters around from method to method. Why not simply reduce the pain by using a global variable? With a global, everyone can get at the data. Global variables have their place, but they do need to be viewed with some level of suspicion. That’s quite a high level of suspicion, by the way. By using a global variable, or by giving a class any kind of knowledge about its wider domain, you anchor it into its context, making it less reusable and dependent on code beyond its control. Remember, you want to decouple your classes and routines and not create interdependence. Try to limit a class’s knowledge of its context. I will look at some strategies for doing this later in the book.

从一个方法传递参数到另一个方法时可能会产生问题。为什么不使用全局变量减少麻烦呢？使用全局变量可以让所有的方法都能获得数据。全局变量有它们自己的作用，但使用时一定要慎重考虑。使用全局变量或者允许一个类知道它之外的领域的内容，你就可以把这个类绑定到外部环境中，让它很难重用，并无法保持独立。记住，我们要解开类及例程之间的耦合，尽量避免产生相互的依赖关系。我们要尽量把一个类限制在自己的环境中。

The Jack of All TradesIs. your class trying to do too many things at once? If so, see if you can list the responsibilities of the class. You may find that one of them will form the basis of a good class itself. Leaving an overzealous class unchanged can cause particular problems if you create subclasses. Which responsibility are you extending with the subclass? What would you do if you needed a subclass for more than one responsibility? You are likely to end up with too many subclasses or an over-reliance on conditional code.

你的类是否尝试一次完成很多工作？如果是的话，就要检查类的职责列表了。你会发现其中的一些功能可以提取出来，成为一个基类。如果类的职责过多，那么在创建子类的时候会产生问题。你要用子类扩展什么样的功能？如果想要让子类负责更多的事情，该怎么办？这样可能会产生太多的子类或者过度依赖于条件语句。

Conditional Statements. You will use if and switch statements with perfectly good reason throughout your projects. Sometimes, though, such structures can be a cry for polymorphism. If you find that you are testing for certain conditions frequently within a class, especially if you find these tests mirrored across more than one method, this could be a sign that your one class should be two or more. See whether the structure of the conditional code suggests responsibilities that could be expressed in classes. The new classes should implement a shared abstract base class. Chances are that you will then have to work out how to pass the right class to client code. I will cover some patterns for creating objects in Chapter 9.

在项目中我们常有非常好的理由来使用 if 和 switch 语句，但有时这样的结构会让我们不得不使用多态。如果你发现在一个类中频繁地进行特定条件的判断，特别是当你发现这些条件判断在多个方法中出现时，就说明这个类需要拆分成两个或者更多。检查一下条件代码的结构，看看是否应该将某些功能独立出来放在独立类中。拆分出来的几个类应该有一个共享的抽象基类，这时你需要知道如何传递正确的子类给客户端代码。

2『重构的 4 个方向：代码重复、类知道的太多（慎用全局变量）、万能的类和条件语句。代码重复往往意味着高耦合，一个地方的代码需要修改，另一个地方同样的代码也要跟着改；尽量把一个类限制在自己的环境中；如果类的职责过多，那么在创建子类的时候会产生问题。你要用子类扩展什么样的功能？做一张术语卡片。』——已完成

## 6.8 The UML

So far in this book, I have let the code speak for itself, and I have used short examples to illustrate concepts such as inheritance and polymorphism. This is useful because PHP is a common currency here: it’s a language we have in common, if you have read this far. As our examples grow in size and complexity, though, using code alone to illustrate the broad sweep of design becomes somewhat absurd. It is hard to see an overview in a few lines of code.

UML stands for Unified Modeling Language. The initials are correctly used with the definite article. This isn’t just a unified modeling language, it is the Unified Modeling Language.

1『统一建模语言，注意要用定冠词 the。』

Perhaps this magisterial tone derives from the circumstances of the language’s forging. According to Martin Fowler (UML Distilled, Addison-Wesley Professional, 1999), the UML emerged as a standard only after long years of intellectual and bureaucratic sparring among the great and good of the object-oriented design community. The result of this struggle is a powerful graphical syntax for describing object-oriented systems. We will only scratch the surface in this section, but you will soon find that a little UML (sorry, a little of the UML) goes a long way.

Class diagrams in particular can describe structures and patterns so that their meaning shines through. This luminous clarity is often harder to find in code fragments and bullet points.

### 6.8.1 Class Diagrams

Although class diagrams are only one aspect of the UML, they are perhaps the most ubiquitous. Because they are particularly useful for describing object-oriented relationships, I will primarily use these in this book. 

Representing Classes. As you might expect, classes are the main constituents of class diagrams. A class is represented by a named box (see Figure 6-1).

Figure 6-1.  A class

The class is divided into three sections, with the name displayed in the first. These dividing lines are optional when we present no more information than the class name. In designing a class diagram, we may find that the level of detail in Figure 6-1 is enough for some classes. We are not obligated to represent every field and method, or even every class in a class diagram.

Abstract classes are represented either by italicizing the class name (see Figure 6-2) or by adding {abstract} to the class name (see Figure 6-3). The first method is the more common of the two, but the second is more useful when you are making notes.

{abstract} 语法是约束的一个例子。「约束」在类图中用于描述特定元素将被使用。花括号中的文字并没有特殊的结构，它只是提供一个将应用于该元素的条件声明。

Figure 6-2.  An abstract class

Figure 6-3.  An abstract class defined using a constraint

 ■ Note:  the {abstract} syntax is an example of a constraint. Constraints are used in class diagrams to describe the way in which specific elements should be used. there is no special structure for the text between the braces; it should simply provide a short clarification of any conditions that may apply to the element.

Interfaces are defined in the same way as classes, except that they must include a stereotype (that is, an extension to the UML), as shown in Figure 6-4.

Figure 6-4.  An interface

AttributesBroadly speaking, attributes describe a class’s properties. Attributes are listed in the section directly beneath the class name (see Figure 6-5).

Figure 6-5.  An attribute

Let’s take a close look at the attribute in the example. The initial symbol represents the level of visibility, or access control, for the attribute. Table 6-1 shows the three symbols available.

Table 6-1.  Visibility Symbols

The visibility symbol is followed by the name of the attribute. In this case, I am describing the ShopProduct::\$price property. A colon is used to separate the attribute name from its type (and optionally, its default value). Once again, you need only include as much detail as is necessary for clarity.

### 6.8.2 Operations

Operations describe methods; or, more properly, they describe the calls that can be made on an instance of a class. Figure 6-6 shows two operations in the ShopProduct class.







Figure 6-6.  Operations

As you can see, operations use a similar syntax to that used by attributes. The visibility symbol precedes 

the method name. A list of parameters is enclosed in parentheses. The method’s return type, if any, is delineated by a colon. Parameters are separated by commas and follow the attribute syntax, with the attribute name separated from its type by a colon.

As you might expect, this syntax is relatively flexible. You can omit the visibility flag and the return type. 

Parameters are often represented by their type alone, as the argument name is not usually significant.

Describing Inheritance and ImplementationThe UML describes the inheritance relationship as generalization. This relationship is signified by a line leading from the subclass to its parent. The line is tipped with an empty closed arrow.

Figure 6-7 shows the relationship between the ShopProduct class and its child classes.

Figure 6-7.  Describing inheritance

The UML describes the relationship between an interface and the classes that implement it as 

realization. So, if the ShopProduct class were to implement the Chargeable interface, we could add it to our class diagram, as in Figure 6-8.

Figure 6-8.  Describing interface implementation

AssociationsInheritance is only one of a number of relationships in an object-oriented system. An association occurs when a class property is declared to hold a reference to an instance (or instances) of another class.

In Figure 6-9, we model two classes and create an association between them.

Figure 6-9.  A class association

At this stage, we are vague about the nature of this relationship. We have only specified that a Teacher object 

will have a reference to one or more Pupil objects, or vice versa. This relationship may or may not be reciprocal.You can use arrows to describe the direction of the association. If the Teacher class has an instance of the Pupil class but not the other way round, then you should make your association an arrow leading from the Teacher to the Pupil class. This association, which is called unidirectional, is shown in Figure 6-10.

Figure 6-10.  A unidirectional association

If each class has a reference to the other, you can use a double-headed arrow to describe a bidirectional 

relationship, as in Figure 6-11).

Figure 6-11.  A bidirectional association

You can also specify the number of instances of a class that are referenced by another in an association. You do this by placing a number or range beside each class. You can also use an asterisk (*) to stand for any number. In Figure 6-12, there can be one Teacher object and zero or more Pupil objects.

Figure 6-12.  Defining multiplicity for an association

In Figure 6-13, there can be one Teacher object and between five and ten Pupil objects in the association.

Figure 6-13.  Defining multiplicity for an association

Aggregation and CompositionAggregation and composition are similar to association. All describe a situation in which a class holds a permanent reference to one or more instances of another. With aggregation and composition, though, the referenced instances form an intrinsic part of the referring object.

In the case of aggregation, the contained objects are a core part of the container, but they can also be 

contained by other objects at the same time. The aggregation relationship is illustrated by a line that begins with an unfilled diamond.

In Figure 6-14, I define two classes: SchoolClass and Pupil. The SchoolClass class aggregates Pupil.Pupils make up a class, but the same Pupil object can be referred to by different SchoolClass instances at the same time. If I were to dissolve a school class, I would not necessarily delete the pupil, who may attend other classes.

Figure 6-14.  Aggregation

Composition represents an even stronger relationship than this. In composition, the contained object 

can be referenced by its container only. It should be deleted when the container is deleted. Composition relationships are depicted in the same way as aggregation relationships, except that the diamond should be filled (see Figure 6-15).

Figure 6-15.  Composition

A Person class maintains a reference to a SocialSecurityData object. The contained instance can 

belong only to the containing Person object.

Describing UseThe use relationship is described as a dependency in the UML. It is the most transient of the relationships discussed in this section because it does not describe a permanent link between classes.A used class may be passed as an argument or acquired as a result of a method call.The Report class in Figure 6-16 uses a ShopProductWriter object. The use relationship is shown by the broken line and open arrow that connects the two. It does not, however, maintain this reference as a property in the same way that a ShopProductWriter object maintains an array of ShopProduct objects.

Figure 6-16.  A dependency relationship

Using NotesClass diagrams can capture the structure of a system, but they provide no sense of process. Figure 6-16 tells us about the classes in our system. From Figure 6-16, you know that a Report object uses a ShopProductWriter, but you don’t know the mechanics of this. In Figure 6-17, I use a note to clarify things somewhat.

Figure 6-17.  Using a note to clarify a dependency

As you can see, a note consists of a box with a folded corner. It will often contain scraps of pseudo-code.This clarifies Figure 6-16; you can now see that the Report object uses a ShopProductWriter to output 

product data. This is hardly a revelation, but use relationships are not always so obvious. In some cases, even a note might not provide enough information. Luckily, you can model the interactions of objects in your system, as well as the structure of your classes.

Sequence DiagramsA sequence diagram is object-based rather than class-based. It is used to model a process in a system step-by-step.

Let’s build up a simple diagram, modeling the means by which a Report object writes product data. A 

sequence diagram presents the participants of a system from left to right (see Figure 6-18).

Figure 6-18.  Objects in a sequence diagram

I have labeled my objects with class names alone. If I had more than one instance of the same class 

working independently in my diagram, I would include an object name using the format, label:class (e.g., product1:ShopProduct).

You show the lifetime of the process you are modeling from top to bottom, as in Figure 6-19.

Figure 6-19.  Object lifelines in a sequence diagram

The vertical broken lines represent the lifetime of the objects in the system. The larger boxes that follow 

the lifelines represent the focus of a process. If you read Figure 6-19 from top to bottom, you can see how the process moves among objects in the system. This is hard to read without showing the messages that are passed between the objects. I add these in Figure 6-20.

Figure 6-20.  The complete sequence diagram

The arrows represent the messages sent from one object to another. Return values are often left 

implicit (although they can be represented by a broken line, passing from the invoked object to the message originator). Each message is labeled using the relevant method call. You can be quite flexible with your labeling, although there is some syntax. Square brackets represent a condition:

[okToPrint]write()

This snippet means that the write() invocation should only be made if the correct condition is met. An 

asterisk is used to indicate a repetition; optionally, further clarification can be in square brackets:

*[for each ShopProduct]write()

You can interpret Figure 6-20 from top to bottom. First, a Report object acquires a list of ShopProduct 

objects from a ProductStore object. It passes these to a ShopProductWriter object, which stores references to them (though we can only infer this from the diagram). The ShopProductWriter object calls ShopProduct::getSummaryLine() for every ShopProduct object it references, adding the result to its output.

As you can see, sequence diagrams can model processes, freezing slices of dynamic interaction and 

presenting them with surprising clarity.

Note  Look at Figures 6-16 and 6-20. notice how the class diagram illustrates polymorphism, showing the classes derived from ShopProductWriter and ShopProduct. now notice how this detail becomes transparent when we model the communication among objects. Where possible, we want objects to work with the most general types available, so that we can hide the details of implementation.

## Summary

In this chapter, I went beyond the nuts and bolts of object-oriented programming to look at some key design issues. I examined features such as encapsulation, loose coupling, and cohesion that are essential aspects of a flexible and reusable object-oriented system. I went on to look at the UML, laying groundwork that will be essential in working with patterns later in the book.
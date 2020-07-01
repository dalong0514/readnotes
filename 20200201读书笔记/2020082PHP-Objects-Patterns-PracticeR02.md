# 2020082PHP-Objects-Patterns-PracticeR02

## 记忆时间

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

### 6.4 Polymorphism

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

### 6.5 Encapsulation

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

这样做通常有很好的理由，但通常来说会带来一些不确定的因素。在代码中査询特定子类型时会产生一个依赖关系。如果我们利用多态来隐藏特定子类型的特性，ShopProduct 的继承关系改变时就不会产生任何错误。但上面的代码会破坏这种情况。使用上面的代码时，如果我们改写了 CdProduct 和 BookProduct 类，就有可能在 workwithproducts() 方法中产生预想不到的错误。这个例子说明了两件事。首先，封装可以帮助我们创建正交的代码。其次，封装的范围不怎么重要，无论封装的规模是大是小，类和客户端代码都必须同时关注封装的实现。

### 6.6 Forget How to Do It

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

### 6.7 Four Signposts

Very few people get it absolutely right at the design stage. Most of us amend our code as requirements change or as we gain a deeper understanding of the nature of the problem we are addressing. As you amend your code, it can easily drift beyond your control. A method is added here and a new class there, and gradually your system begins to decay. As you have seen already, your code can point the way to its own improvement. These pointers in code are sometimes referred to as code smells—that is, features in code that may suggest particular fixes or at least call you to look again at your design. In this section, I distill some of the points already made into four signs that you should watch out for as you code.

Code Duplication. Duplication is one of the great evils in code. If you get a strange sense of déjà vu as you write a routine, chances are you have a problem. Take a look at the instances of repetition in your system. Perhaps they belong together. Duplication generally means tight coupling. If you change something fundamental about one routine, will the similar routines need amendment? If this is the case, they probably belong in the same class.

The Class Who Knew Too Much. It can be a pain passing parameters around from method to method. Why not simply reduce the pain by using a global variable? With a global, everyone can get at the data. Global variables have their place, but they do need to be viewed with some level of suspicion. That’s quite a high level of suspicion, by the way. By using a global variable, or by giving a class any kind of knowledge about its wider domain, you anchor it into its context, making it less reusable and dependent on code beyond its control. Remember, you want to decouple your classes and routines and not create interdependence. Try to limit a class’s knowledge of its context. I will look at some strategies for doing this later in the book.

从一个方法传递参数到另一个方法时可能会产生问题。为什么不使用全局变量减少麻烦呢？使用全局变量可以让所有的方法都能获得数据。全局变量有它们自己的作用，但使用时一定要慎重考虑。使用全局变量或者允许一个类知道它之外的领域的内容，你就可以把这个类绑定到外部环境中，让它很难重用，并无法保持独立。记住，我们要解开类及例程之间的耦合，尽量避免产生相互的依赖关系。我们要尽量把一个类限制在自己的环境中。

The Jack of All TradesIs. your class trying to do too many things at once? If so, see if you can list the responsibilities of the class. You may find that one of them will form the basis of a good class itself. Leaving an overzealous class unchanged can cause particular problems if you create subclasses. Which responsibility are you extending with the subclass? What would you do if you needed a subclass for more than one responsibility? You are likely to end up with too many subclasses or an over-reliance on conditional code.

你的类是否尝试一次完成很多工作？如果是的话，就要检查类的职责列表了。你会发现其中的一些功能可以提取出来，成为一个基类。如果类的职责过多，那么在创建子类的时候会产生问题。你要用子类扩展什么样的功能？如果想要让子类负责更多的事情，该怎么办？这样可能会产生太多的子类或者过度依赖于条件语句。

Conditional Statements. You will use if and switch statements with perfectly good reason throughout your projects. Sometimes, though, such structures can be a cry for polymorphism. If you find that you are testing for certain conditions frequently within a class, especially if you find these tests mirrored across more than one method, this could be a sign that your one class should be two or more. See whether the structure of the conditional code suggests responsibilities that could be expressed in classes. The new classes should implement a shared abstract base class. Chances are that you will then have to work out how to pass the right class to client code. I will cover some patterns for creating objects in Chapter 9.

在项目中我们常有非常好的理由来使用 if 和 switch 语句，但有时这样的结构会让我们不得不使用多态。如果你发现在一个类中频繁地进行特定条件的判断，特别是当你发现这些条件判断在多个方法中出现时，就说明这个类需要拆分成两个或者更多。检查一下条件代码的结构，看看是否应该将某些功能独立出来放在独立类中。拆分出来的几个类应该有一个共享的抽象基类，这时你需要知道如何传递正确的子类给客户端代码。

2『重构的 4 个方向：代码重复、类知道的太多（慎用全局变量）、万能的类和条件语句。代码重复往往意味着高耦合，一个地方的代码需要修改，另一个地方同样的代码也要跟着改；尽量把一个类限制在自己的环境中；如果类的职责过多，那么在创建子类的时候会产生问题。你要用子类扩展什么样的功能？做一张术语卡片。』——已完成

### 6.8 The UML

So far in this book, I have let the code speak for itself, and I have used short examples to illustrate concepts such as inheritance and polymorphism. This is useful because PHP is a common currency here: it’s a language we have in common, if you have read this far. As our examples grow in size and complexity, though, using code alone to illustrate the broad sweep of design becomes somewhat absurd. It is hard to see an overview in a few lines of code.

UML stands for Unified Modeling Language. The initials are correctly used with the definite article. This isn’t just a unified modeling language, it is the Unified Modeling Language.

1『统一建模语言，注意要用定冠词 the。』

Perhaps this magisterial tone derives from the circumstances of the language’s forging. According to Martin Fowler (UML Distilled, Addison-Wesley Professional, 1999), the UML emerged as a standard only after long years of intellectual and bureaucratic sparring among the great and good of the object-oriented design community. The result of this struggle is a powerful graphical syntax for describing object-oriented systems. We will only scratch the surface in this section, but you will soon find that a little UML (sorry, a little of the UML) goes a long way.

Class diagrams in particular can describe structures and patterns so that their meaning shines through. This luminous clarity is often harder to find in code fragments and bullet points.

## 0201. What Are Design Patterns? Why Use Them?

In this chapter, I introduced design patterns, showed you their structure (using the Gang of Four form), and suggested some reasons why you might want to use design patterns in your scripts. It is important to remember that design patterns are not snap-on solutions that can be combined like components to build a project. They are suggested approaches to common problems. These solutions embody some key design principles. It is these that we will examine in the next chapter.

要记住，设计模式并非像组件那样能被合并来构建系统的固定解决方案。它们是解决一般性问题的通用方法。这些解决方案体现了一些关键的设计原则。

Most problems we encounter as programmers have been handled time and again by others in our community. Design patterns can provide us with the means to mine that wisdom. Once a pattern becomes a common currency, it enriches our language, making it easy to share design ideas and their consequences. Design patterns simply distill common problems, define tested solutions, and describe likely outcomes. 

Many books and articles focus on the details of computer languages, such as the available functions, classes and methods, and so on. Pattern catalogs concentrate instead on how you can move on from these basics (the「what」) to an understanding of the problems and potential solutions in your projects (the「why」and「how」).

In this chapter, I introduce you to design patterns and look at some of the reasons for their popularity. This chapter will cover the following: 1) Pattern basics: What are design patterns? 2) Pattern structure: What are the key elements of a design pattern? 3) Pattern benefits: Why are patterns worth your time?

### 1.1 What Are Design Patterns?

In the world of software, a pattern is a tangible manifestation of an organization’s tribal memory. [A pattern is] a solution to a problem in a context.

—The Gang of Four, Design Patterns: Elements of Reusable Object-Oriented Software

在软件世界中，每个开发机构就像一个部落，而模式就是对部落的某种共同记忆的一种有形表现。

As these quotations imply, a design pattern is a problem analyzed with good practice for its solution explained. Problems tend to recur, and as web programmers we must solve them time and time again. How should we handle an incoming request? How can we translate this data into instructions for our system? How should we acquire data? Present results? Over time, we answer these questions with a greater or lesser degree of elegance and evolve an informal set of techniques that we use and reuse in our projects. These techniques are patterns of design.

正如上述引语所暗示的，设计模式便是分析过的问题和问题解决方案所阐释的优秀实践。同样的问题总是不断出现，而我们作为 Web 程序员必须一次又ー次地解决它们。比如如何处理一个请求？如何将请求数据转换成系统对应的指令？应该如何获得数据？又如何显示结果？随着时间流逝和经验积累，我们会或优雅或困难地回答这些问题，并总结出一些非正式的、可在项目中重复使用的解决方案，而这些解决方案便是设计模式。

Design patterns inscribe and formalize these problems and solutions, making hard-won experience available to the wider programming community. Patterns are (or should be) essentially bottom-up and not top-down. They are rooted in practice and not theory. That is not to say that there isn’t a strong theoretical element to design patterns (as we will see in the next chapter), but patterns are based on real-world techniques used by real programmers. Renowned pattern-hatcher Martin Fowler says that he discovers patterns, he does not invent them. For this reason, many patterns will engender a sense of déjà vu as you recognize techniques you have used yourself.

设计模式记录并规范化了这些问题及解决方案，使更广泛的开发社区可获得这些来之不易的经验。模式在本质上讲是（或者说应该是）自下而上而非自上而下的。它们来源于实践而不是空洞的理论。这并非指设计模式没有强有力的理论基础（你会在下一章中看到这些理论基础），但是模式是以真正的程序员使用的真实世界的技术为基础的的。著名的模式专家 Martin Fowler 便说他是在发现模式，而不是发明模式。正是因为这样的原因，许多模式都会给你造成似曾相识（a sense of deja）的感觉。

A catalog of patterns is not a cookbook. Recipes can be followed slavishly; code can be copied and slotted into a project with minor changes. You do not always need even to understand all the code used in a recipe. Design patterns inscribe approaches to particular problems. The details of implementation may vary enormously according to the wider context. This context might include the programming language you are using, the nature of your application, the size of your project, and the specifics of the problem.

Let’s say, for example, that your project requires that you create a templating system. Given the name of a template file, you must parse it and build a tree of objects to represent the tags you encounter.

You start off with a default parser that scans the text for trigger tokens. When it finds a match, it hands off responsibility for the hunt to another parser object, which is specialized for reading the internals of tags. This continues examining template data until it either fails, finishes, or finds another trigger. If it finds a trigger, it, too, must hand off responsibility to a specialist—perhaps an argument parser. Collectively, these components form what is known as a recursive descent parser.

So these are your participants: a MainParser, a TagParser, and an ArgumentParser. You create a ParserFactory class to create and return these objects. Of course, nothing is easy, and you’re informed late in the game that you must support more than one syntax in your templates. Now, you need to create a parallel set of parsers according to syntax: an OtherTagParser, an OtherArgumentParser, and so on.

一个模式目录并不是一本食谱。食谱中的配方可以直接遵循；具体的程序代码也可以只做很小改动便被复制和安置在一个项目中。你也不必理解使用的所有代码。设计模式只负责记录特定问题的解决方法，对于大范围的上下文环境，具体的实现细节可能差别甚大，而这些上下文环境包括所使用的编程语言、应用程序的性质、项目的大小及问题的细节等。比方说，如果项目要求创建一个模板系统。根据所给的模板文件名，你必须解析它并建立一个对象树来代表所遇到的标签。

首先我们需要一个可以扫描文本的默认解析器，用于触发标记。当解析器找到一个匹配的标签时，它把找到的标签传递给另一个专门读内部标签的解析器。解析器继续解析模板数据，一直到解析失败或者完成，或者找到另一个触发标记。如果找到了一个触发标记，也必须传递它给另一个专门的处理器一一可能是一个参数解析器。这些部件共同组成一个递归下降解析器。

因此我们将需要这些解析器：Mainparser（核心解析器）、Tagparser（标签解析器）和 Argumentparser（参数解析器）。我们可以创建 Parserfactory 类来创建并返回这些对象。当然，现实中并没有这么简单的事情。你总是会在事后才被告知必须在模板里面支持多种语法。现在，只能根据语法来创建一组相应的解析器：OtherTagParser 和 OtherArgumentParser 等。

This is your problem: you need to generate a different set of objects according to the circumstance, and you want this to be more or less transparent to other components in the system. It just so happens that the Gang of Four define the following problem in their book’s summary page for the pattern Abstract Factory,「Provide an interface for creating families of related or dependent objects without specifying their concrete classes.」That fits nicely. It is the nature of our problem that determines and shapes our use of this pattern. There is nothing cut and paste about the solution either, as you can see in Chapter 9, in which I cover Abstract Factory.

The very act of naming a pattern is valuable, it contributes to the kind of common vocabulary that has arisen naturally over the years in older crafts and professions. Such shorthand greatly aids collaborative design as alternative approaches and their various consequences are weighed and tested. When you discuss your alternative parser families, for example, you can simply tell colleagues that the system creates each set of objects using the Abstract Factory pattern. They will nod sagely, either immediately enlightened or making a mental note to look it up later. The point is that this bundle of concepts and consequences has a handle, which makes for a useful shorthand, as I’ll illustrate later in this chapter.

这时你的问题便是：需要根据不同的情况创建一组不同的对象，同时要这组对象在系统里相对于其他组件来说或多或少是透明的。这恰恰就是《设计模式》一书的摘要中为抽象工厂（Abstract Factory）模式所定义的问题：为一个相关或相依赖的对象家族提供统一的创建接口，并无需指定实体类。这和我们的问题十分符合。正是问题的本质决定和形成了我们对该模式的使用。没有任何对解决方案的剪切和粘贴，而在第 9 章中，你可以看到对于抽象工厂模式的详细介绍。

恰当地为一个模式命名是很有意义的，因为模式命名象征着长期的专业过程中自然形成的公认的词汇表。这样的简写名称大大促进了软件设计的合作，并且它们的结论是经过量化及测试的。比如当你讨论系列解析器时，你可以简单地告诉同事，系统会使用抽象工厂模式来创建每组相应的解析器。你的同事会明智地点头同意，无论立刻觉悟还是先记下稍后再查阅该模式的相关资料。也就是说，模式命名象征着一系列概念，这对于程序员间的交流非常有好处，这在本章后面会详细介绍。

Finally, it is illegal, according to international law, to write about patterns without quoting Christopher Alexander, an architecture academic whose work heavily influenced the original object-oriented pattern advocates. He states in A Pattern Language (Oxford University Press, 1977):

Each pattern describes a problem which occurs over and over again in our environment, and then describes the core of the solution to that problem, in such a way that you can use this solution a million times over, without ever doing it the same way twice.

最后，根据国际惯例，介绍模式时应当提及 Christopher Alexander。他是一个建筑学家，极大地影响了初期的面向对象模式。他在 A Pattern Language（牛津大学出版社，1977) 一书中写道：每个模式都描述着一种在我们的环境中一遍又一遍地出现的问题，并描述了对该问题的核心解决方策。以此方式你可以使用该方案上百万次，而从不需要重复做同样的事情。

2『做一张金句卡片。』——已完成

It is significant that this definition (which applies to architectural problems and solutions) begins with the problem and its wider setting, and then proceeds to a solution. There has been some criticism in recent years that design patterns have been overused, especially by inexperienced programmers. This is often a sign that solutions have been applied where the problem and context are not present. Patterns are more than a particular organization of classes and objects, cooperating in a particular way. Patterns are structured to define the conditions in which solutions should be applied and to discuss the effects of the solution.

In this book, I will focus on a particularly influential strand in the patterns field: the form described in Design Patterns: Elements of Reusable Object-Oriented Software by the Gang of Four (Addison-Wesley Professional, 1995). It concentrates on patterns in object-oriented software development and inscribes some of the classic patterns that are present in most modern object-oriented projects.

The Gang of Four book is important because it inscribes key patterns, but also because it describes the design principles that inform and motivate these patterns. We will look at some of these principles in the next chapter.

这个始于问题及其广泛的环境继而进入解决方案的定义（被应用于建筑问题及解决方案）意义重大。这几年有一些对设计模式被滥用的指责，特别是被没经验的程序员所使用时。解决方案被应用于并不符合的问题及上下文中通常是滥用的信号。模式是类和对象的一种特殊组织形式是以定义解决方案的应用条件并讨论其效果的形式来组织的。本书中，我们将关注模式领域中特别具有影响力的一部分，即 Erich Gamma、Richard Helm、Ralph Johnson 和 John Vlissidek 所著的《设计模式——可复用面向对象软件的基础》（Addison- Wesley 1995) 一书中所描述的模式。该书集中介绍了面向对象软件开发中的模式，并记录了一些在大多数现代面向对象项目中出现的传统模式。《设计模式》一书非常重要，不仅因为它记录了关键模式，而且因为它也描述了形成和推动这些模式的设计原则。在下一章中我们便会看到其中的一些原则。

 ■ Note: the patterns described by the gang of Four and in this book are really instances of a pattern language. a pattern language is a catalog of problems and solutions organized together so that they complement one another, forming an interrelated whole. there are pattern languages for other problem spaces, such as visual design and project management (and architecture, of course). When I discuss design patterns here, I refer to problems and solutions in object-oriented software development.

《设计模式》及本书中所描述的模式是模式语言的真实实例，这些模式便是组织在一起的问题和解决方策的一个目录，以使模式可相互补充而形成一个相互关联的整体。当然也存在其他问题的模式语言，如视觉设计和项目管理（当然还有建筑）。但在此我所讨论的设计模式都是针对面向对象软件开发的问题和解决方案的。

### 1.2 A Design Pattern Overview

At heart, a design pattern consists of four parts: the name, the problem, the solution, and the consequences.

#### 1.2.1 Name

Names matter. They enrich the language of programmers; a few short words can stand in for quite complex problems and solutions. They must balance brevity and description. The Gang of Four claims,「Finding good names has been one of the hardest parts of developing our catalog.」

Martin Fowler agrees:「Pattern names are crucial, because part of the purpose of patterns is to create a vocabulary that allows developers to communicate more effectively」(Patterns of Enterprise Application Architecture, Addison-Wesley Professional, 2002).

In Patterns of Enterprise Application Architecture, Martin Fowler refines a database access pattern I first encountered in Core J2EE Patterns by Deepak Alur, Dan Malks, and John Crupi (Prentice Hall, 2001). Fowler defines two patterns that describe specializations of the older pattern. The logic of his approach is clearly correct (one of the new patterns models domain objects, while the other models database tables, a distinction that was vague in the earlier work). Nonetheless, it was hard to train myself to think in terms of the new patterns. I had been using the name of the original in design sessions and documents for so long that it had become part of my language.

2『已下载书籍「2020105企业应用架构模式 | 2020105Patterns-of-Enterprise-Application-Architecture」、「2020151J2EE核心模式 | 2020151Core-J2EE-Patterns」。』

在《企业应用架构模式》一书中，Martin Fowler 改进了一个我曾在《J2EE 核心模式》（Deepak Alur、Dan Malks 和 John Crupia 著，Prentice Hall, 2003）中了解到的数据库访问模式。他定义了两个新模式来描述旧模式的特例。显然他的逻辑是正确的：新模式之一，对领域对象（domain object）进行了建模；另一个新模式对数据库表进行了建模。这区分了之前模式中含糊不清的地方。但最初我很不习惯他所采用的新术语，因为我使用旧的命名方式已经很长时间了，以至于旧的命名已经成为我的语言中的一部分。

#### 1.2.2 The Problem

No matter how elegant the solution (and some are very elegant indeed), the problem and its context are the grounds of a pattern. Recognizing a problem is harder than applying any one of the solutions in a pattern catalog. This is one reason that some pattern solutions can be misapplied or overused.

Patterns describe a problem space with great care. The problem is described in brief and then contextualized, often with a typical example and one or more diagrams. It is broken down into its specifics, its various manifestations. Any warning signs that might help in identifying the problem are described.

无论解决方案如何优雅（有些的确非常优雅），问题及问题发生的环境都是一个模式的基础。找出问题比使用模式目录中的解决方案更难。这正是某些模式的解决方案被误用或过度使用的原因之一。模式会小心谨慎地描述问题的空间（问题发生的条件和环境）。问题会被置于环境中简明扼要地描述，通常还会带有典型的范例及一个或多个图表。问题会被分解为不同细节和各种表现。同时任何可以帮助发现问题的警告标志都会在模式中被描述。

#### 1.2.3 The Solution

The solution is summarized initially in conjunction with the problem. It is also described in detail, often using UML class and interaction diagrams. The pattern usually includes a code example.

Although code may be presented, the solution is never cut-and-paste. The pattern describes an approach to a problem. There may be hundreds of nuances in its implementation. Think about instructions for sowing a food crop. If you simply follow a set of steps blindly, you are likely to go hungry come harvest time. More useful would be a pattern-based approach that covers the various conditions that may apply. The basic solution to the problem (making your crop grow) will always be the same (prepare soil, plant seeds, irrigate, harvest crop), but the actual steps you take will depend on all sorts of factors, such as your soil type, your location, the orientation of your land, local pests, and so on.

Martin Fowler refers to solutions in patterns as「half-baked.」That is, the coder must take away the concept and finish it for himself.

解决方案最初是和问题放在一起的，并常用 UML 类图和交互图更详细地进行描述。而模式通常也包含一个代码范例。尽管代码也许是现成的，但解决方案从来不是简单的剪切及粘贴。模式描述了一个问题的解决方法，但在实现时可能会有上百种细微的差别。这就像农作物播种的操作，如果你简单地盲目遵循书本上的步骤，那么在收获季节很可能会挨饿。以模式为基础，但又能针对各种情况随机应变的方法会更实用。虽然问题的基本解决方案（使你的庄稼成长）总是相同的（播种、灌溉、收割），但是实际采用的步骤依赖于各种因素，如土壤类别、地理位置、土地的方位和当地的害虫等。于是 Martin Fowler 把模式中的解决方案称为「半成品」。换句话说，编码人员必须理解概念并自己来完成具体的实现。

#### 1.2.4 Consequences

Every design decision you make will have wider consequences. This should include the satisfactory resolution of the problem in question, of course. A solution, once deployed, may be ideally suited to work with other patterns. There may also be dangers to watch for.

在设计代码的时候，你所做的每一个决定都会带来不同的结果。当然我们总是希望能得到令人满意的针对问题的解决方案。解决方案一旦被部署，理想情况下它也许会非常适合与其他模式一同工作，但也要留心是否会带来风险。

### 1.3 The Gang of Four Format

As I write, I have five pattern catalogs on the desk in front of me. A quick look at the patterns in each confirms that none of them use the same structure. Some are formal; some are fine-grained, with many subsections; and others are discursive.

There are a number of well-defined pattern structures, including the original form developed by Christopher Alexander (the Alexandrian form), and the narrative approach favored by the Portland Pattern Repository (the Portland form). Because the Gang of Four book is so influential, and because we will cover many of the patterns they describe, let’s examine a few of the sections they include in their patterns:

1. Intent: A brief statement of the pattern’s purpose. You should be able to see the point of the pattern at a glance.

2. Motivation: The problem described, often in terms of a typical situation. The anecdotal approach can help make the pattern easy to grasp.

3. Applicability: An examination of the different situations in which you might apply the pattern. While the motivation describes a typical problem, this section defines specific situations and weighs the merits of the solution in the context of each.

4. Structure/Interaction: These sections may contain UML class and interaction diagrams describing the relationships among classes and objects in the solution.

5. Implementation: This section looks at the details of the solution. It examines any issues that may come up when applying the technique and provides tips for deployment.

6. Sample Code: I always skip ahead to this section. I find that a simple code example often provides a way into a pattern. The example is often chopped down to the basics in order to lay the solution bare. It could be in any object-oriented language. Of course, in this book, it will always be PHP.

7. Known Uses: These describe real systems in which the pattern (problem, context, and solution) occurs. Some people say that for a pattern to be genuine, it must be found in at least three publicly available contexts. This is sometimes called the「rule of three.」

8. Related Patterns: Some patterns imply others. In applying one solution, you can create the context in which another becomes useful. This section examines these synergies. It may also discuss patterns that have similarities to the problem or the solution, as well as any antecedents (i.e., patterns defined elsewhere on which the current pattern builds).

2『设计模式结构（pattern structures）做一张术语卡片。』——已完成

编写本书时，在我桌上有 5 份模式目录。看一下每个目录的模式，便可发现每一个都使用不样的结构：其中一些比较正式；一些比较细致，有着许多的子分类；还有一些则比较松散。这些目录中有一些定义良好的模式结构，其中包括由 Christopher Alexander 原创的格式（Alexandrian 格式）和 Portland 模式库所钟爱的叙述性格式（Portland 格式）。不过因为《设计模式》书极具影响力，而且我们也会介绍该书所描述的很多模式，所以先研究一下该书所采用的模式结构。其主要组成部分如下所示。

1、意图：模式目的的简要概括。你应该一眼就能看出模式的要点。

2、动机；需要被解决的问题，通常根据一个典型的情况。叙述性的方式有助于使模式更容易被领会。

3、适用性：检验不同情况下你是否可以应用某模式。动机描述了一个典型问题，而适用性定义了特殊的情况，并衡量该解决方案在每种情况下的价值。

4、结构/交互：可能包含 UML 类图和交互图，用于描述解决方案中类和对象之间的关系。

5、实现：着眼于解决方案的细节，介绍了应用解决方案时可能发生的问题，并提供了部署的技巧。

6、示例代码：我总是先跳到这一部分。我发现简单的代码范例是理解模式的捷径。范例通常都会被简化以突出解决方案的核心内容。示例代码可以用任何一种面向对象语言编写，当然本书中使用的是 PHP。

7、已知应用：使用该模式（问题、上下文及解决方案）的真实系统。有些人会说一个模式要变得真实，它就必须出现在至少 3 个公开存在的真实系统中。这有时会被称为「三法则」（rule of three，意思是解决某个特定问题所采取的设计，一次出现是偶然现象，两次是巧合，3 次出现才可称为一个模式）。

8、相关模式：一些模式意味着其他模式也要被采用。在使用某个设计模式时，可以创造出另一个模式适用的条件。这部分内容研究了可能存在的模式间的合作，也可能会讨论那些问题或解决方案中具有相似点的模式及任何需要预先使用的模式（当前模式可能以其他模式为基础）。

### 1.4 Why Use Design Patterns?

So what benefits can patterns bring? Given that a pattern is a problem defined and a solution described, the answer should be obvious. Patterns can help you to solve common problems. There is more to patterns, of course.

#### 1.4.1 A Design Pattern Defines a Problem

How many times have you reached a stage in a project and found that there is no going forward? Chances are you must backtrack some way before starting out again. By defining common problems, patterns can help you to improve your design. Sometimes, the first step to a solution is recognizing that you have a problem.

有多少次在项目到了某个阶段时你发现无法继续？这时你很可能必须以某种方式返回而不是继续尝试前进。通过定义共性问题，模式能帮助你改进设计。有时找到解决方案的第一步便是认清你面对的问题。

#### 1.4.2 A Design Pattern Defines a Solution

Having defined and recognized the problem (and made certain that it is the right problem), a pattern gives you access to a solution, together with an analysis of the consequences of its use. Although a pattern does not absolve you of the responsibility to consider the implications of a design decision, you can at least be certain that you are using a tried-and-tested technique.

在定义和识别当前存在的问题后，模式给你提供了解决方案及应用该方案所得结果的分析。尽管模式并不能代替你来作出决策，但至少能确认你使用的是一个可靠并经过测试的技术。

#### 1.4.3 Design Patterns Are Language Independent

Patterns define objects and solutions in object-oriented terms. This means that many patterns apply equally in more than one language. When I first started using patterns, I read code examples in C++ and Smalltalk, and then deployed my solutions in Java. Others transfer with modifications to the pattern’s applicability or consequences, but remain valid. Either way, patterns can help you as you move between languages. Equally, an application that is built on good object-oriented design principles can be relatively easy to port between languages (although there are always issues that must be addressed).

模式以面向对象的方式来定义对象和解决方案。这意味着大多数模式可被直接应用于多种编程语言中。例如我第一次使用模式时阅读的是 C++和 Smalltalk 的代码范例，却在 Java 环境中部署我的解决方案。另一些模式针对不同语言可能有不同的适用性或效果，但总是可行的。无论是哪种情况，模式总可以在不同语言中给你帮助。同时，一个建立于优秀的面向对象设计原则之上的应用能被相对简单地在不同语言中移植（尽管总有些问题需要处理）。

#### 1.4.4 Patterns Define a Vocabulary

By providing developers with names for techniques, patterns make communication richer. Imagine a design meeting. I have already described my Abstract Factory solution, and now I need to describe my strategy for managing the data the system compiles. I describe my plans to Bob:

Me: I’m thinking of using a Composite.

Bob: I don’t think you’ve thought that through.

Okay, Bob didn’t agree with me. He never does. But he knew what I was talking about, and therefore why my idea sucked. Let’s play that scene through again without a design vocabulary.

Me: I intend to use a tree of objects that share the same type. The type’s interface will provide methods for adding child objects of its own type. In this way, we can build up complex combinations of implementing objects at runtime.

Bob: Huh?

Patterns, or the techniques they describe, tend to interoperate. The Composite pattern lends itself to collaboration with the Visitor pattern, for example:

Me: And then we can use Visitors to summarize the data.

Bob: You’re missing the point.

Ignore Bob. I won’t describe the tortuous nonpattern version of this; I will cover Composite in Chapter 10 and Visitor in Chapter 11.

The point is that, without a pattern language, we would still use these techniques. They precede their naming and organization. If patterns did not exist, they would evolve on their own, anyway. Any tool that is used sufficiently will eventually acquire a name.

1『确实，任何一个好的技术只要足够好，到最后肯定会有一个大家都知道的名字。』

#### 1.4.5 Patterns Are Tried and Tested

So if patterns document good practice, is naming the only truly original thing about pattern catalogs? In some senses, that would seem to be true. Patterns represent best practice in an object-oriented context. To some highly experienced programmers, this may seem an exercise in repackaging the obvious. To the rest of us, patterns provide access to problems and solutions we would otherwise have to discover the hard way. Patterns make design accessible. As pattern catalogs emerge for more and more specializations, even the highly experienced can find benefits as they move into new aspects of their fields. A GUI programmer can gain fast access to common problems and solutions in enterprise programming, for example. A web programmer can quickly chart strategies for avoiding the pitfalls that lurk in tablet and smart phone projects.

如果模式验证了高质量的实践，那么名称是否是模式目录仅有的真正原创的东西？从某种意义上说，好像是这样的。在面向对象的环境中，模式代表着最佳实践。对于一些经验非常丰富的程序员来说，这就像是再包装明显的最佳实践。对于我们而言，模式提供了发现问题和解决方案的途径，否则我们将不得不非常辛苦地去发掘。模式使我们更容易得到好的设计方案。当模式目录变得越来越专业化，即使经验丰富的程序员也会在进入新领域的时候从中受益。例如，图形用户界面程序员可以快速理解企业级开发中的常见问题和解决方案。Web 程序员能快速制定策略来避免 PDA 和智能手机项目的缺陷。

#### 1.4.6 Patterns Are Designed for Collaboration

By their nature, patterns should be generative and composable. This means that you should be able to apply one pattern and thereby create conditions suitable for the application of another. In other words, in using a pattern you may find other doors opened for you.

Pattern catalogs are usually designed with this kind of collaboration in mind, and the potential for pattern composition is always documented in the pattern itself.

模式生来就是「可生成的」（generative）和「可组成的」（composable）。这意味着你能应用一个模式，并因此创建适合应用另一个模式的条件。换句话说，在使用某个模式时你也许会发现另一扇门为你敞开了，你可以同时使用其他模式。模式目录通常会关注于这类协作，而模式本身也会介绍潜在的模式组合。

#### 1.4.7 Design Patterns Promote Good Design

Design patterns demonstrate and apply principles of object-oriented design. So, a study of design patterns can yield more than a specific solution in a context. You can come away with a new perspective on the ways that objects and classes can be combined to achieve an objective.

设计模式示范并应用了面向对象设计原则。因此设计模式能在一个具体环境中产生多个特定的解决方案，而你可以从一个新的角度来学习如何组合对象和类来达到目标。

#### 1.4.8 Design Patterns are Used By Popular Frameworks

This book is primarily about designing from the ground up. The patterns and principles covered here should enable you to design your own core frameworks with the needs of your projects in mind. However, laziness is also a virtue, and you may wish to work with (or you may inherit code that already uses) a framework such as Zend, Laravel, or Symfony. A good understanding of core design patterns will help you as you engage with these framework APIs.

### 1.5 PHP and Design Patterns

There is little in this chapter that is specific to PHP, which is characteristic of our topic to some extent. Many patterns apply to many object-capable languages with few or no implementation issues.

This is not always the case, of course. Some enterprise patterns work well in languages in which an application process continues to run between server requests. PHP does not work that way. A new script execution is kicked off for every request. This means that some patterns need to be treated with more care. Front Controller, for example, often requires some serious initialization time. This is fine when the initialization takes place once at application startup, but it’s more of an issue when it must take place for every request. That is not to say that we can’t use the pattern; I have deployed it with very good results in the past. We must simply ensure that we take account of PHP-related issues when we discuss the pattern. PHP forms the context for all the patterns that this book examines.

I referred to object-capable languages earlier in this section. You could code in PHP without defining any classes at all. With a few notable exceptions, however, objects and object-oriented design lie at the heart of most PHP projects and libraries.

本章中只有很小一部分是专门针对 PHP 的，从某种程度上说它算是本章的一点特色。许多模式都可以应用于各种具有面向对象能力的语言，实现起来通常不会有什么问题。当然，并不总是这样。一些企业模式只有在服务器请求对应一个应用进程的情况下オ能很好地工作。PHP 并不能以那样的方式工作。在 PHP 中，每一个请求都会开始一个新的脚本执行。这意味着要更谨慎地对待一些模式。例如，前端控制器（Front Controller）模式通常需要较多的初始化时间。如果初始化仅在应用启动时发生一次，那么还没问题，但如果每次请求都需要初始化，就会导致问题。这并不是说我们不能使用该模式，因为我在以前成功地使用过该模式。我们必须确保在讨论模式的时候考虑到 PHP 相关的问题，因为 PHP 正是本书研究所有模式时的具体环境。

在本节开头我提到过「具有对象能力的语言」。你根本不必定义任何类就可编写 PHP 代码（但如果使用 PEAR，你将会使用到一些对象）。虽然本书几乎完全关注于用面向对象解决方案来解决编程问题，但并不是在鼓吹面向对象。模式和 PHP 能被有效地混合，而且它们也形成了本书的核心，另外它们也能与许多传统方式很好地共存。对此 PEAR 便是一个极好的证明。PEAR 包优雅地使用了设计模式，它们在本质上趋于面向对象。但这个特性使它们在过程式项目中更加实用（而非不实用）。因为 PEAR 包是自我封装的，并将它们自身的复杂性都隐藏在十分干净的接口下，所以它们能被轻松地嵌入任何类型的项目中。

## 0202. Some Pattern Principles

In this chapter, I examined some of the principles that underpin many design patterns. I looked at the use of composition to enable object combination and recombination at runtime, resulting in more flexible structures than would be available using inheritance alone. I also introduced you to decoupling, the practice of extracting software components from their context to make them more generally applicable. Finally, I reviewed the importance of interface as a means of decoupling clients from the details of implementation. In the coming chapters, I will examine some design patterns in detail.

学习了一些设计模式背后的设计原则，讨论了在运行时使用组合来合并及再合并对象（这比单独使用继承的灵活性更高），介绍了解耦并提取组件来使它们更具适用性，回顾了接口（它将客户端代码与实现的具体细节相分离）的重要性。

Although design patterns simply describe solutions to problems, they tend to emphasize solutions that promote reusability and flexibility. To achieve this, they manifest some key object-oriented design principles. We will encounter some of them in this chapter and in more detail throughout the rest of the book.

This chapter will cover the following topics: 1) Composition: How to use object aggregation to achieve greater flexibility than you could with inheritance alone. 2) Decoupling: How to reduce dependency between elements in a system. 3) The power of the interface: Patterns and polymorphism. 4) Pattern categories: The types of patterns that this book will cover.

### 2.1 The Pattern Revelation

I first started working with objects in the Java language. As you might expect, it took a while before some concepts clicked. When it did happen, though, it happened very fast, almost with the force of revelation. The elegance of inheritance and encapsulation bowled me over. I could sense that this was a different way of defining and building systems. I got polymorphism, working with a type and switching implementations at runtime. It seemed to me that this understanding would solve most of my design problems, and help me design beautiful and elegant systems.

1『又见多态，可以替代条件语句的功能。working with a type and switching implementations at runtime. 』

All the books on my desk at the time focused on language features and the very many APIs available to the Java programmer. Beyond a brief definition of polymorphism, there was little attempt to examine design strategies. Language features alone do not engender object-oriented design. Although my projects fulfilled their functional requirements, the kind of design that inheritance, encapsulation and polymorphism had seemed to offer continued to elude me.

My inheritance hierarchies grew wider and deeper as I attempted to build a new class for every eventuality. The structure of my systems made it hard to convey messages from one tier to another without giving intermediate classes too much awareness of their surroundings, binding them into the application and making them unusable in new contexts.

It wasn’t until I discovered Design Patterns: Elements of Reusable Object-Oriented Software (Addison-Wesley Professional, 1995), otherwise known as the Gang of Four book, that I realized I had missed an entire design dimension. By that time, I had already discovered some of the core patterns for myself, but others contributed to a new way of thinking.

I found that I had over-privileged inheritance in my designs, trying to build too much functionality into my classes. But where else can functionality go in an object-oriented system?

I found the answer in composition. Software components can be defined at runtime by combining objects in flexible relationships. The Gang of Four boiled this down into a principle:「favor composition over inheritance.」The patterns described ways in which objects could be combined at runtime to achieve a level of flexibility impossible in an inheritance tree alone.

1『金子知识啊，组合替代继承。』

因为我努力地为每一个可能性建造新类，所以我的继承层次体系逐渐变得更广、更深。而在这样的系统结构中，如果中间类对于环境没有足够的了解，如果没有将它们绑定到具体应用中，如果没有使它们只可用于当前局部环境中，那么在系统的层级中传递信息将会变得十分困难。直到发现《设计模式》一书，我才意识到原来我没有完全理解什么是设计。虽然那时我自己也已经发现了一些核心模式，但是书中介绍的其他模式则提供了一种全新的思维方式。

我在设计中给了继承过多的特权，总是试图为我的类构建太多的功能。在面向对象系统里还有别的地方可以放置这些功能吗？我在组合模式中找到了答案。通过以灵活的关系来组合对象，组件能在运行时被定义。《设计模式》将这提炼成了一个原则：组合优于继承（favor composition over inheritance）。在该模式中，运行时组合对象所达到的灵活性非常高，而这在单独的继承树中是不可能达到的。

### 2.2 Composition and Inheritance

Inheritance is a powerful way of designing for changing circumstances or contexts. It can limit flexibility, however, especially when classes take on multiple responsibilities.

1『所以才会有单一职责原则，当类有太多职责的时候，就可以考虑使用多台来拆解。』

#### 2.2.1 The Problem

As you know, child classes inherit the methods and properties of their parents (as long as they are protected or public elements). You can use this fact to design child classes that provide specialized functionality.

Figure 8-1 presents a simple example using the UML. The abstract Lesson class in Figure 8-1 models a lesson in a college. It defines abstract cost() and chargeType() methods. The diagram shows two implementing classes, FixedPriceLesson and TimedPriceLesson, which provide distinct charging mechanisms for lessons.

Using this inheritance scheme, I can switch between lesson implementations. Client code will know only that it is dealing with a Lesson object, so the details of cost will be transparent.

What happens, though, if I introduce a new set of specializations? I need to handle lectures and seminars. Because these organize enrollment and lesson notes in different ways, they require separate classes. Now I have two forces that operate upon my design. I need to handle pricing strategies, and separate lectures and seminars.

Figure 8-2 shows a hierarchy that is clearly faulty. I can no longer use the inheritance tree to manage my pricing mechanisms without duplicating great swathes of functionality. The pricing strategies are mirrored across the Lecture and Seminar class families.

At this stage, I might consider using conditional statements in the Lesson super class, removing those unfortunate duplications. Essentially, I remove the pricing logic from the inheritance tree altogether, moving it up into the super class. This is the reverse of the usual refactoring, where you replace a conditional with polymorphism. Here is an amended Lesson class:

利用这种继承模式，我们可以在课程的实现之间切换。而客户端代码只知道它是在处理一个 Lesson 对象，因此费用的细节就会变得透明。可是如果引入一组新的特殊性，又会怎样呢？比如我们需要处理演讲和研讨会。因为演讲和研讨会会以不同的方式注册登记和教授课程，所以它们会要求独立的类。因此在设计上现在会有两个分支。我们需要处理不同的定价策略并区分演讲和研讨会。

图 8-2 的体系明显是有缺陷的。在该体系中，我们不得不大量重复开发功能，否则无法使用继承树来管理价格机制。定价策略在 Lecture 和 Seminar 类的子类中被重复实现。我们可能要考虑在父类 Lesson 中使用条件语句来移除那些不适宜的重复。我们是把定价逻辑从继承树中一并移除并迁移到父类中，但这与我们通常用多态替换条件的重构思想背道而驰。下面是一个修改过的 Lesson 类。

```php
<?php
// declare(strict_types=1);  // 显式声明类型检查为严格模式

// listing 0801

abstract class Lesson {
    protected $duration;
    const FIXED= 1;
    const TIMED = 2;
    private $costtype;

    public function __construct(int $duration, int $costtype = 1) {
        $this->duration = $duration;
        $this->costtype = $costtype;
    }

    public function cost(): int {
        switch ($this->costtype) {
            case self::TIMED:
                return (5 * $this->duration);
                break;
            case self::FIXED:
                return 30;
                break;
            default:
                $this->costtype = self::FIXED;
                return 30;
        }
    }

    public function chargeType(): string {
        switch ($this->costtype) {
            case self::TIMED:
                return "hourly rate";
                break;
            case self::FIXED:
                return "fixed rate";
                break;
            default:
                $this->costtype = self::FIXED;
                return "fixed rate";
        }
    }

    // more lesson methods...
}

class Lecture extends Lesson {
    // Lecture-specific implementions...
}

class Seminar extends Lesson {
    // Seminar-specific implementions...
}
```

Here’s how I might work with these classes:

```php
$lecture = new Lecture(5, Lesson::FIXED);
echo "{$lecture->cost()}({$lecture->chargeType()})\n";

$seminar = new Seminar(3, Seminar::TIMED);
echo "{$seminar->cost()}({$seminar->chargeType()})\n";
```

And here’s the output:

```
30 (fixed rate)
15 (hourly rate)
```

You can see the new class diagram in Figure 8-3. Inheritance hierarchy improved by removing cost calculations from subclasses.

I have made the class structure much more manageable, but at a cost. Using conditionals in this code is a retrograde step. Usually, you would try to replace a conditional statement with polymorphism. Here, I have done the opposite. As you can see, this has forced me to duplicate the conditional statement across the chargeType() and cost() methods. I seem doomed to duplicate code.

#### 2.2.2 Using Composition

I can use the Strategy pattern to compose my way out of trouble. Strategy is used to move a set of algorithms into a separate type. By moving cost calculations, I can simplify the Lesson type. You can see this in Figure 8-4.

Figure 8-4.  Moving algorithms into a separate type

I create an abstract class, CostStrategy, which defines the abstract methods, cost() and chargeType(). The cost() method requires an instance of Lesson, which it will use to generate cost data. I provide two implementations for CostStrategy. Lesson objects work only with the CostStrategy type, not a specific implementation, so I can add new cost algorithms at any time by subclassing CostStrategy. This would require no changes at all to any Lesson classes.

Here’s a simplified version of the new Lesson class illustrated in Figure 8-4:

```php
abstract class CostStrategy {
    abstract public function cost(Lesson $lesson): int;
    abstract public function chargeType(): string;
}

abstract class Lesson {
    private $duration;
    private $CostStrategy;

    public function __construct(int $duration, CostStrategy $strategy) {
        $this->duration = $duration;
        $this->CostStrategy = $strategy;
    }

    public function cost(): int {
        return $this->CostStrategy->cost($this);
    }

    public function chargeType(): string {
        return $this->CostStrategy->chargeType();
    }

    public function getDuration(): int {
        return $this->duration;
    }

    // more lesson methods...
}

class Lecture extends Lesson {
    // Lecture-specific implementions...
}

class Seminar extends Lesson {
    // Seminar-specific implementions...
}
```

The Lesson class requires a CostStrategy object, which it stores as a property. The Lesson::cost() method simply invokes CostStrategy::cost(). Equally, Lesson::chargeType() invokes CostStrategy::chargeType(). This explicit invocation of another object’s method in order to fulfill a request is known as delegation. In my example, the CostStrategy object is the delegate of Lesson. The Lesson class washes its hands of responsibility for cost calculations and passes on the task to a CostStrategy implementation. Here, it is caught in the act of delegation:

1『又见委托（delegation）。』

这种显式调用另一个对象的方法来执行一个请求的方式便是所谓的「委托」。在我们的示例中，Coststrategy 对象便是 Lesson 的委托方。Lesson 类不再负责计费，而是把计费任务传给 CostStrategy 类。下面的代码执行了委托操作：

```php
    public function cost(): int {
        return $this->CostStrategy->cost($this);
    }
```

Here is the CostStrategy class, together with its implementing children:

```php
abstract class CostStrategy {
    abstract public function cost(Lesson $lesson): int;
    abstract public function chargeType(): string;
}

class TimedCostStrategy extends CostStrategy {
    function cost(Lesson $lesson):int {
        return ($lesson->getDuration() * 5);
    }

    function chargeType(): string {
        return "hourly rate";
    }
}

class FixedCostStrategy extends CostStrategy {
    function cost(Lesson $lesson): int {
        return 30;
    }

    function chargeType(): string {
        return "fixed rate";
    }
}
```

I can change the way that any Lesson object calculates cost by passing it a different CostStrategy object at runtime. This approach then makes for highly flexible code. Rather than building functionality into my code structures statically, I can combine and recombine objects dynamically:

```php
$lessons[] = new Seminar(4, new TimedCostStrategy);
$lessons[] = new Lecture(4, new FixedCostStrategy);

foreach ($lessons as $lesson) {
    print "lesson charge {$lesson->cost()}. \n";
    echo "Charge type: {$lesson->chargeType()}\n";
}
```

```
lesson charge 20. Charge type: hourly rate
lesson charge 30. Charge type: fixed rate
```

1『通过组合 Lesson 和 CostStrategy 实现，在运行时根据不同的条件实施不同的行为，即条件语句实现的功能。』

As you can see, one effect of this structure is that I have focused the responsibilities of my classes. CostStrategy objects are responsible solely for calculating cost, and Lesson objects manage lesson data. So, composition can make your code more flexible because objects can be combined to handle tasks dynamically in many more ways than you can anticipate in an inheritance hierarchy alone. There can be a penalty with regard to readability, though. Because composition tends to result in more types, with relationships that aren’t fixed with the same predictability as they are in inheritance relationships, it can be slightly harder to digest the relationships in a system.

组合使用对象比使用继承体系更灵活，因为组合可以以多种方式动态地处理任务，不过这可能导致代码的可读性下降。因为组合需要更多的对象类型，而这些类型的关系并不像在继承关系中那般有固定的可预见性，所以要理解系统中类和对象的关系会有些困难。

### 2.3 Decoupling

You saw in Chapter 6 that it makes sense to build independent components. A system with highly interdependent classes can be hard to maintain. A change in one location can require a cascade of related changes across the system.

#### 2.3.1 The Problem

Reusability is one of the key objectives of object-oriented design, and tight coupling is its enemy. You can diagnose tight coupling when you see that a change to one component of a system necessitates many changes elsewhere. You should aspire to create independent components, so that you can make changes without a domino effect of unintended consequences. When you alter a component, the extent to which it is independent is related to the likelihood that your changes will cause other parts of your system to fail.

重用性是面向对象设计的主要目标之一，而紧耦合（tight-coupling）便是它的敌人。当我们看到系统中一个组件的改变迫使系统其他许多地方也发生改变的时候，就可诊断为紧耦合了。为了能安全地做变动，我们总是期望创建能够独立存在的组件。在修改组件时，其独立程度会决定你的修改对系统中其他组件的影响程度，系统的其他组件甚至有可能会因此失败。

2『紧耦合，做一张术语卡片。』——已完成

You saw an example of tight coupling in Figure 8-2. Because the cost logic was mirrored across the Lecture and Seminar types, a change to TimedPriceLecture would necessitate a parallel change to the same logic in TimedPriceSeminar. By updating one class and not the other, I would break my system—without any warning from the PHP engine. My first solution, using a conditional statement, produced a similar dependency between the cost() and chargeType() methods.

By applying the Strategy pattern, I distilled my cost algorithms into the CostStrategy type, locating them behind a common interface and implementing each only once.

在图 8-2 中，我们看到过紧耦合的例子。因为费用计算逻辑在 Lecture 和 Seminar 类型中都存在，所以对 TimedPriceLecture 的一个改变将会迫使在 TimedPriceSeminar 中同样逻辑的相应变化。如果仅改动一个类而不改动其他类的代码，系统将无法正常工作，而且没有来自 PHP 引擎的任何警告。而我们的第一个解决方案（使用条件语句）在 cost() 和 chargeType() 方法之间生成了一个类似的依赖关系。通过应用策略模式，我们将费用算法提取为 CostStrategy 类型，将算法放置在共同接口后并且每个算法只需实现一次。

Coupling of another sort can occur when many classes in a system are embedded explicitly into a platform or environment. Let’s say that you are building a system that works with a MySQL database, for example. You might use methods such as mysqli::query() to speak to the database server.

Should you be required to deploy the system on a server that does not support MySQL, you could convert your entire project to use SQLite. You would be forced to make changes throughout your code, though, and face the prospect of maintaining two parallel versions of your application.

不过当系统中许多类都显式嵌入到一个平台或环境中时，其他类型的耦合仍时有发生。比如建立了一个基于 MySQL 数据库的系统。你可能会用一些诸如 mysql\_connect() 和 mysql\_query() 的函数来与数据库服务器交互。如果现在你被要求在不支持 MySQL 的服务器上部署系统，比如要把整个项目都转换成使用 SQLite，那么你可能被迫要改变整个代码，并且面临维护应用程序的两个并行版本的状况。

1『中文是老版书籍，看来数据库的连接方法都改了哦。』

The problem here is not the system’s dependency on an external platform. Such a dependency is inevitable. You need to work with code that speaks to a database. The problem comes when such code is scattered throughout a project. Talking to databases is not the primary responsibility of most classes in a system, so the best strategy is to extract such code and group it together behind a common interface. In this way, you promote the independence of your classes. At the same time, by concentrating your gateway code in one place, you make it much easier to switch to a new platform without disturbing your wider system. This process, the hiding of implementation behind a clean interface, is known as encapsulation. The Doctrine database library solves this problem with the DBAL (database abstraction layer) project. This provides a single point of access for multiple databases.

1『如何隔离与数据库交互的代码，这个思路太赞了。这里有提高「Doctrine database library 」这个工具，就是为了解决这个问题的，记得去了解下。突然想到有本 python 的英文书里（那个作者写了好几本书），也有提高这种在程序和数据库之间抽象出来的中间层。』

这里的问题不在于系统对外部平台的依赖。这样的依赖是无法避免的。我们确实需要使用与数据库交互的代码。但当这样的代码散布在整个项目中时，问题就来了。与数据库交互不是系统中大部分类的首要责任，因此最好的策略就是提取这样的代码并将其组合在公共接口后。这可以使类之间相互独立。同时，通过在一个地方集中你的「入ロ」代码，就能更轻松地切换到一个新的平台而不会影响到系统中更大的部分。这个把具体实现隐藏在一个干净的接口后面的过程，正是大家所知道的「封装」。

PEAR 中的 PEAR::MDB2 包（沿袭自 PEAR::DB）可以解决这个问题。该包支持对多个数据库的访问。最新的 PDO 扩展已将此模型移植到 PHP 语言中。MDB2 类提供了一个静态方法 connect()，它接受一个 DSN (Data Source Name，数据源名）字符串参数。根据这个字符串的构成，它返回 MDB2\_Driver\_Comon 类的一个特定实现。因此对于字符串 "mysql://", connect() 方法返回一个 MmB2\_Driver\_mysql 对象，而对于一个以 "sqlite://" 开头的字符串，它将返回一个 MDB2 Driver\_sqlite，对象。可以在图 8-5 中看到该类的结构。

The DriverManager class provides a static method called getConnection() that accepts a parameters array. According to the makeup of this array, it returns a particular implementation of an interface called Doctrine\DBAL\Driver. You can see the class structure in Figure 8-5.

Figure 8-5.  The DBAL package decouples client code from database objects

The DBAL package, then, lets you decouple your application code from the specifics of your database platform. You should be able to run a single system with MySQL, SQLite, MSSQL, and others without changing a line of code (apart from your configuring parameters, of course).

#### 2.3.2 Loosening Your Coupling

To handle database code flexibly, you should decouple the application logic from the specifics of the database platform it uses. You will see lots of opportunities for this kind of separation of components in your own projects.

Imagine, for example, that the Lesson system must incorporate a registration component to add new lessons to the system. As part of the registration procedure, an administrator should be notified when a lesson is added. The system’s users can’t agree whether this notification should be sent by mail or by text message. In fact, they’re so argumentative that you suspect they might want to switch to a new mode of communication in the future. What’s more, they want to be notified of all sorts of things, so that a change to the notification mode in one place will mean a similar alteration in many other places.

If you’ve hard-coded calls to a Mailer class or a Texter class, then your system is tightly coupled to a particular notification mode, just as it would be tightly coupled to a database platform by the use of a specialized database API. Here is some code that hides the implementation details of a notifier from the system that uses it:

为了灵活处理数据库代码，我们应该将应用逻辑从数据库平台的特殊性中解耦出来。在你自己的项目中，你会看到很多这种需要分离组件的情况。例如，课程系统中应包含注册组件，从而向系统中添加新课程。添加了新课程后，应该通知管理员，这是注册程序的一部分。对于应该通过邮件发送通知还是通过文本消息发送通知，系统用户的意见不一致。实际上，他们太挑别了，以至于你怀疑将来他们会想使用一种新的信息传达模式。此外，他们希望发生任何事情都会收到通知。所以，修改了通知模式的一处意味着要对多处做同样的修改。

如果已经硬编码了对 Mailer 类或 Texter 类的调用，那么系统就与特殊的通知模式紧密相关了。就像利用专门的数据库 API 时，系统就与某数据库平台紧密相关一样。下面的这些代码对使用通知程序的系统隐藏了通知程序的实现细节。

```php
class RegistrationMgr {
    function register(Lesson $lesson) {
        // do something with the lesson

        // now tell someone
        $notifier = Notifier::getNotifier();
        $notifier->inform("new lesson: cost({$lesson->cost()})");
    }
}

abstract class Notifier {
    public static function getNotifier(): Notifier {
        // acquire concrete class according to configuration or other logic
        if (rand(1, 2) === 1) {
            return new MailNotifier();
        } else {
            return new TextNotifier();
        }
    }
}

class MailNotifier extends Notifier {
    public function inform($message) {
        echo "MAIL notification: {$message}\n";
    }
}

class TextNotifier extends Notifier {
    public function inform($message) {
        echo "TEXT notification: {$message}\n";
    }
}
```

I create RegistrationMgr, a sample client for my Notifier classes. The Notifier class is abstract, but it does implement a static method, getNotifier(), which fetches a concrete Notifier object (TextNotifier or MailNotifier). In a real project, the choice of Notifier would be determined by a flexible mechanism, such as a configuration file. Here, I cheat and make the choice randomly. MailNotifier and TextNotifier do nothing more than print out the message they are passed along with an identifier to show which one has been called.

Notice how the knowledge of which concrete Notifier should be used has been focused in the Notifier::getNotifier() method. I could send notifier messages from a hundred different parts of my system, and a change in Notifier would only have to be made in that one method. Here is some code that calls the RegistrationMgr:

注意，具体应该使用哪个 Notifier 对象取决于 Notifier::getnotifier() 方法。我可以从系统的上百个不同部分发送消息，但只需在该方法中对 Notifier 进行一项修改即可。


```php
$mrg = new RegistrationMgr();
$mrg->register(new Seminar(4, new TimedCostStrategy));
$mrg->register(new Lecture(4, new FixedCostStrategy));
```

And here’s the output from a typical run:

```
TEXT notification: new lesson: cost (20)MAIL notification: new lesson: cost (30)
```

Figure 8-6 shows these classes.Notice how similar the structure in Figure 8-6 is to that formed by the Doctrine components shown in Figure 8-5.

### 2.4 Code to an Interface, Not to an Implementation

This principle is one of the all-pervading themes of this book. You saw in Chapter 6 (and in the last section) that you can hide different implementations behind the common interface defined in a superclass. Client code can then require an object of the superclass’s type rather than that of an implementing class, unconcerned by the specific implementation it is actually getting.

Parallel conditional statements, like the ones I rooted out from Lesson::cost() and Lesson::chargeType(), are a common sign that polymorphism is needed. They make code hard to maintain because a change in one conditional expression necessitates a change in its siblings. Conditional statements are occasionally said to implement a「simulated inheritance.」

把不同的实现隐藏在父类所定义的共同接口下。然后客户端代码需要一个父类的对象而不是一个子类的对象，从而使客户端代码可以不用关心它实际得到的是哪个具体实现。我们在 Lesson::cost() 和 Lesson::cost() 中创建的并行条件语句，就是需要多态的常见标志。这样的条件语句使代码很难维护，因为条件表达式的改变必然要求与之对应的代码主体也随之改变，所以条件语句有时会被称作实现了一个「模拟继承」。

By placing the cost algorithms in separate classes that implement CostStrategy, I remove duplication. I also make it much easier should I need to add new cost strategies in the future.

From the perspective of client code, it is often a good idea to require abstract or general types in your methods’ parameters. By requiring more specific types, you could limit the flexibility of your code at runtime. Having said that, of course, the level of generality you choose in your argument hints is a matter of judgment. Make your choice too general, and your method may become less safe. If you require the specific functionality of a subtype, then accepting a differently equipped sibling into a method could be risky.

Still, make your choice of argument hint too restricted, and you lose the benefits of polymorphism. Take a look at this altered extract from the Lesson class:

而通过把计费算法放置在一个实现 CostStrategy 的独立的类中，我们可以移除重复代码，也可以使在未来加入新的计费策略变得更加容易。从客户端代码的角度看，类方法参数为抽象或通用类型通常都是不错的主意。如果参数对对象类型要求过于严格，就会限制代码在运行时的灵活性。

当然，如何使用参数类型提示来调整参数对象的「通用性」是需要仔细权衡的。选择过于通用，则会降低方法的安全性。而如果需要某个子类型的特有功能，那么方法接受另一个子类类型则可能会有风险。尽管如此，若参数的类型匹配限制过于严格，那么将无法得到多态带来的好处。下面是修改过的 Lesson 类里的一段代码。

```php
// listing 08.17    

public function __construct(int $duration, FixedCostStrategy $strategy)    {        
    $this->duration = $duration;        
    $this->costStrategy = $strategy;    
}
```

There are two issues arising from the design decision in this example. First, the Lesson object is now tied to a specific cost strategy, which closes down my ability to compose dynamic components. Second, the explicit reference to the FixedPriceStrategy class forces me to maintain that particular implementation.

By requiring a common interface, I can combine a Lesson object with any CostStrategy implementation:

```php
// listing 08.18    
public function __construct(int $duration, CostStrategy $strategy)    {        
    $this->duration = $duration;        
    $this->costStrategy = $strategy;    
}
```

1『 CostStrategy 只提供接口。』

I have, in other words, decoupled my Lesson class from the specifics of cost calculation. All that matters is the interface and the guarantee that the provided object will honor it. Of course, coding to an interface can often simply defer the question of how to instantiate your objects. 

When I say that a Lesson object can be combined with any CostStrategy interface at runtime, I beg the question,「But where does the CostStrategy object come from?」When you create an abstract superclass, there is always the issue of how its children should be instantiated. Which child do you choose and according to which condition? This subject forms a category of its own in the Gang of Four pattern catalog, and I will examine this further in the next chapter.

换句话说，我们把 Lesson 类从具体的费用计算中分离出来了。我们所做的就是提供接口并保证所提供的对象会实现接口。当然，面向接口编程无法回答如何实例化对象的问题。当我们说 Lesson 对象能在运行时与任何 Coststrategy 接口绑定时，我们回避了这么一个问题：「但是 coststrategy 对象从哪里来呢？」当创建一个抽象父类时，常会碰到如何实例化它的子类的问题。你会选择实例化哪个子类来对应相应的条件呢？这个主题在《设计模式》模式目录中形成了一个独立的类别，我们会在下章研究其中一些模式。

1『核心问题：当创建一个抽象父类时，常会碰到如何实例化它的子类的问题。你会选择实例化哪个子类来对应相应的条件呢？』

### 2.5 The Concept that Varies

It’s easy to interpret a design decision once it has been made, but how do you decide where to start?

The Gang of Four recommend that you「encapsulate the concept that varies.」In terms of my lesson example, the varying concept is the cost algorithm. Not only is the cost calculation one of two possible strategies in the example, but it is obviously a candidate for expansion: special offers, overseas student rates, introductory discounts-all sorts of possibilities present themselves.

1『核心观点：封装变化。』

I quickly established that subclassing for this variation was inappropriate, and I resorted to a conditional statement. By bringing my variation into the same class, I underlined its suitability for encapsulation.

The Gang of Four recommend that you actively seek varying elements in your classes and assess their suitability for encapsulation in a new type. Each alternative in a suspect conditional may be extracted to form a class that extends a common abstract parent. This new type can then be used by the class or classes from which it was extracted. This has the following effects: 1) Promoting flexibility through composition. 2) Making inheritance hierarchies more compact and focused. 3) Focusing responsibility. 4) Reducing duplication.

So how do you spot variation? One sign is the misuse of inheritance. This might include inheritance deployed according to multiple forces at one time (e.g., lecture/seminar and fixed/timed cost). It might also include subclassing on an algorithm where the algorithm is incidental to the core responsibility of the type. The other sign of variation suitable for encapsulation is, as you have seen, a conditional expression.

1『发现「变化点」的两个信号：误用继承和条件语句。』

我们发现为这个变化直接创建子类是不合适的，于是使用了条件语句。通过把变化的元素放入同一个类中，我们强调了封装的适用性。《设计模式》建议积极搜寻类中变化的元素，并评估它们是否适合用新类型来封装。根据一定条件，变化的元素（如计费算法）可被提取出来形成子类（如 TimedCostStrategy 和 FixedCostStrategy），而这些元素共同拥有一个抽象父类（Coststrategy）。而这个新类型（CostStrategy）能被其他类使用。这么做有以下好处：1）专注于职责。2）通过组合提高灵活性。3）使继承层级体系更紧凑和集中；4）减少重复。

那么如何发现变化的元素呢？误用继承便是一个标志。误用的表现可能包括一次实现不同分支（lecture/seminar and fixed/timed cost）的继承；也可能包括子类化某个算法，而该算法对于该对象类型的核心职责是偶然的。当然，适合封装「变化元素」的另一个标志便是出现了条件表达式。

### 2.6 Patternitis

One problem for which there is no pattern is the unnecessary or inappropriate use of patterns. This has earned patterns a bad name in some quarters. Because pattern solutions are neat, it is tempting to apply them wherever you see a fit, whether they truly fulfill a need or not.

The eXtreme Programming (XP) methodology offers a couple of principles that might apply here. The first is,「You aren’t going to need it」(often abbreviated to YAGNI). This is generally applied to application features, but it also makes sense for patterns.

When I build large environments in PHP, I tend to split my application into layers, separating application logic from presentation and persistence layers. I use all sorts of core and enterprise patterns in conjunction with one another.

When I am asked to build a feedback form for a small business web site, however, I may simply use procedural code in a single page script. I do not need enormous amounts of flexibility; I won’t be building on the initial release. I don’t need to use patterns that address problems in larger systems. Instead, I apply the second XP principle:「Do the simplest thing that works.」

When you work with a pattern catalog, the structure and process of the solution are what stick in the mind, consolidated by the code example. Before applying a pattern, though, pay close attention to the problem, or「when to use it,」section, and then read up on the pattern’s consequences. In some contexts, the cure may be worse than the disease.

模式的一个问题便是不必要或不恰当地使用模式。这让模式在某些领域名声不佳。因为模式解决方案很棒，所以它会引诱你把模式应用在任何你认为合适的地方，无论它们是否真的适合用来达到目标。极限编程（XP, extreme Programming）提供了几个可以使用的相关原则。第一个是「你还不需要它」。这通常被应用在应用程序的功能上，但是对于模式来说也有意义。

当使用 PHP 开发较大的项目时，我会把应用程序分离到各个层中，把应用程序逻辑从表现层和持久化层中分离开来。我通常联合使用各种核心模式和企业模式。然而当为一个小型商务网站建立一个用户反馈表单时，我可能只在单一页面脚本中使用过程式代码。此时，不需要大量的灵活性，不需要以后基于最初版本进行大量扩展，也不需要使用那些在更庞大的系统中解决问题的模式，而是应用极限编程的第二个原则：用最简单的方式来完成任务。

当使用模式目录时，通过示例代码能巩固你脑中解决方案的结构和流程。然而在应用模式之前，要特别注意目录中「问题」或者「何时使用」那部分，并且熟读模式的效用。在某些情况下，错误的治疗会比疾病本身更糟。

### 2.7 The Patterns

This book is not a pattern catalog. Nevertheless, in the coming chapters, I will introduce a few of the key patterns in use at the moment, providing PHP implementations and discussing them in the broad context of PHP programming.

The patterns described will be drawn from key catalogs, including Design Patterns: Elements of Reusable Object-Oriented Software, Patterns of Enterprise Application Architecture by Martin Fowler (Addison-Wesley Professional, 2002) and Core J2EE Patterns: Best Practices and Design Strategies (Prentice Hall, 2001) by Alur, et al. I use the Gang of Four’s categorization as a starting point, dividing patterns into five categories, as follows.

被描述的模式将会从主要的模式目录，包括《设计模式》、《企业应用架构模式》和《J2EE 核心模式》中提取出来，我将以《设计模式》一书的分类为起点，将模式分为以下几种。

2『这三本模式相关的经典一定要去读，真香，哈哈。』

1. Patterns for Generating Objects. These patterns are concerned with the instantiation of objects. This is an important category given the principle,「Code to an interface.」If you are working with abstract parent classes in your design, then you must develop strategies for instantiating objects from concrete subclasses. It is these objects that will be passed around your system.

2. Patterns for Organizing Objects and Classes. These patterns help you to organize the compositional relationships of your objects. More simply, these patterns show how you combine objects and classes.

3. Task-Oriented Patterns. These patterns describe the mechanisms by which classes and objects cooperate to achieve objectives.

4. Enterprise Patterns. I look at some patterns that describe typical Internet programming problems and solutions. Drawn largely from Patterns of Enterprise Application Architecture and Core J2EE Patterns: Best Practices and Design Strategies, the patterns deal with presentation and application logic.

5. Database PatternsAn examination of patterns that help with storing and retrieving data, and with mapping objects to and from databases.

1『在使用生成对象模式时，运行时期间，如何根据特定的条件实现特定的子类实例化对象是关键点。』

1、用于生成对象的模式。这类模式关注对象的实例化。考虑到「面向接口编程」原则，这是一个重要的分类。如果在设计中使用抽象父类，那么我们必须考虑从具体子类实例化对象的策略。实例化得到的对象会在系统中被传递。

2、用于组织对象和类的模式。这类模式帮助我们组织对象的组成关系。更简单地说，就是这些模式教我们如何合并对象和类。

3、面向任务的模式。这类模式描述了如何让类和对象合作来达成特定目标。

4、企业模式。我们着眼于一些描述典型因特网编程问题和解决方案的模式。它们很大程度上来自于《企业应用架构模式》和《J2EE 核心模式》这两本书，用于处理表现逻辑及应用逻辑。

5、数据库模式。数据库存取数据及对象一数据库映射的相关模式。

## 0203. Generating Objects

This chapter covered some of the tricks that you can use to generate objects. I began by examining the Singleton pattern, which provides global access to a single instance. Next, I looked at the Factory Method pattern, which applies the principle of polymorphism to object generation. And I combined Factory Method with the Abstract Factory pattern to generate creator classes that instantiate sets of related objects. I also looked at the Prototype pattern and saw how object cloning can allow composition to be used in object generation. Finally, I examined two strategies for object creation: Service Locator and Dependency Injection.

本章介绍了一些用于生成对象的窍门，讨论了支持全局访问实例的单例模式，以及应用多态原则生成对象的工厂方法模式。之后，我们结合使用工厂方法模式和抽象工厂模式来生成一系列创建者类，用于实例化一组相关对象。最后，研究了原型模式，学习了如何使用对象克隆使对象组合可用于生成对象。

Creating objects is a messy business. So, many object-oriented designs deal with nice, clean abstract classes, taking advantage of the impressive flexibility afforded by polymorphism (the switching of concrete implementations at runtime). To achieve this flexibility, though, I must devise strategies for object generation. This is the topic I will look at in this chapter.

This chapter will cover the following patterns: 1) The Singleton pattern: A special class that generates one—and only one—object instance. 2) The Factory Method pattern: Building an inheritance hierarchy of creator classes. 3) The Abstract Factory pattern: Grouping the creation of functionally related products. 4) The Prototype pattern: Using clone to generate objects. 5) The Service Locator pattern: Asking your system for objects. 6) The Dependency Injection pattern: Letting your system give you objects.

单例模式：生成一个且只生成一个对象实例的特殊类；工厂方法模式：构建创建者类的继承层级。抽象工厂模式：功能相关产品的创建。原型模式：使用克隆来生成对象。

### 3.1 Problems and Solutions in Generating Objects

Object creation can be a weak point in object-oriented design. In the previous chapter, you saw the principle,「Code to an interface, not to an implementation.」To this end, you are encouraged to work with abstract supertypes in your classes. This makes code more flexible, allowing you to use objects instantiated from different concrete subclasses at runtime. This has the side effect that object instantiation is deferred.

对象创建有时会成为面向对象设计的一个薄弱环节。在前一章中，我们看到「针对接口编程，而不是针对实现编程」的原则。就此而言，鼓励在类中使用抽象的超类。这使代码更具灵活性，可以让你在运行时使用从不同的具体子类中实例化的对象。但这样做也有副作用，那就是对象实例化被推迟。

Here’s a class that accepts a name string and instantiates a particular object:

```php
<?php

abstract class Employee {
    protected $name;

    public function __construct(string $name)
    {
        $this->name = $name;
    }

    abstract public function fire();
}

class Minion extends Employee {
    public function fire()
    {
        echo "{$this->name}: I'll clear my desk\n";
    }
}

class NastyBoss {
    private $employees = [];

    public function addEmployee(string $employeeName) {
        $this->employees[] = new Minion($employeeName);
    }

    public function projectFail() {
        if (count($this->employees) >0 ) {
            $emp = array_pop($this->employees);
            $emp->fire();
        }
    }
}

$boss = new NastyBoss();
$boss->addEmployee('harry');
$boss->addEmployee('bob');
$boss->addEmployee('mary');
$boss->projectFail();
```

```
mary: I'll clear my desk
```

As you can see, I define an abstract base class, Employee, with a downtrodden implementation, Minion. Given a name string, the NastyBoss::addEmployee() method instantiates a new Minion object. Whenever a NastyBoss object runs into trouble (via the NastyBoss::projectFails() method), it looks for a Minion to fire.

By instantiating a Minion object directly in the NastyBoss class, we limit flexibility. If a NastyBoss object could work with any instance of the Employee type, we could make our code amenable to variation at runtime as we add more Employee specializations. You should find the polymorphism in Figure 9-1 familiar.

如你所看到的，我们定义了一个抽象基类 Employee（雇员）以及一个受压迫员工的具体实现 Minion。NastyBoss::addEmployee() 方法通过接受的名字字符串来实例化新的 Minion。对象且 Nastyboss（苛刻的老板）对象遇到了麻烦（通过 NastyBoss::projectFails() 方法），它就会解雇一个 Minion。由于在 NastyBoss 类中直接实例化 Minion 对象，代码的灵活性受到了限制。如果 NastyBoss 对象可以使用 Employee 类的任何实例，那么代码在运行时就能应对更多特殊的 Employee。在图 9-1 中，应该可以找到你熟悉的多态。

Figure 9-1.  Working with an abstract type enables polymorphism

If the NastyBoss class does not instantiate a Minion object, where does it come from? Authors often duck out of this problem by constraining an argument type in a method declaration, and then conveniently omitting to show the instantiation in anything other than a test context:

如果 NastyBoss 类不实例化 Minion 对象，那么 Minion 对象从何而来？许多人通常在方法声明中限制参数类型来巧妙避开这个问题，然后除了在测试时实例化对象，在其他时候尽量避免提及。

1『抽象出一个状态类跟 NastyBoss 类组合起来呗，让 NastyBoss 调用状态类来实例化 Minion 对象。』

```php
<?php

abstract class Employee {
    protected $name;

    public function __construct(string $name)
    {
        $this->name = $name;
    }

    abstract public function fire();
}

class Minion extends Employee {
    public function fire()
    {
        echo "{$this->name}: I'll clear my desk\n";
    }
}

class CluedUp extends Employee {
    public function fire() {
        echo "{$this->name}: I'll call my lawyer\n";
    }
}

class NastyBoss {
    private $employees = [];

    public function addEmployee(Employee $employee) {
        $this->employees[] = $employee;
    }

    public function projectFail() {
        if (count($this->employees) >0 ) {
            $emp = array_pop($this->employees);
            $emp->fire();
        }
    }
}

$boss = new NastyBoss();
$boss->addEmployee(new Minion('harry'));
$boss->addEmployee(new CluedUp('bob'));
$boss->addEmployee(new Minion('mary'));
$boss->projectFail();
$boss->projectFail();
$boss->projectFail();
```

```
mary: I'll clear my desk
bob: I'll call my lawyer
harry: I'll clear my desk
```

Although this version of the NastyBoss class works with the Employee type, and therefore benefits from polymorphism, I still haven’t defined a strategy for object creation. Instantiating objects is a dirty business, but it has to be done. This chapter is about classes and objects that work with concrete classes, so that the rest of your classes do not have to.

If there is a principle to be found here, it is「delegate object instantiation.」I did this implicitly in the previous example by demanding that an Employee object be passed to the NastyBoss::addEmployee() method. I could, however, equally delegate to a separate class or method that takes responsibility for generating Employee objects. Here I add a static method to the Employee class that implements a strategy for object creation:

虽然这个版本的 NastyBoss 类能与 Employee 类型一起工作，而且也能从多态中获益，但我们仍旧没有定义创建对象的策略。实例化对象是一件麻烦事，但是我们又不得不去做。这一章讲的是使用具体类的类和对象。这样，不使用具体类的类和对象不一定非要实例化对象。如果说这里存在一个原则的话，那便是「把对象实例化的工作委托出来」。之前的示例已然隐含了这个原则，即要求将一个 Employee 对象传递给 NastyBoss::addEmployee() 方法。然而我们也可以委托一个独立的类或方法来生成 Employee 对象，其效果是一样的。下面给 Employee 类添加一个实现了对象创建策略的静态方法。

```php
abstract class Employee {
    protected $name;
    private static $types = ['Minion', 'CluedUp', 'WellConnected'];

    public static function recruit(string $name) {
        $num = rand(1, count(self::$types)) - 1;
        $class = __NAMESPACE__ . "\\" . self::$types[$num];
        return new $class($name);
    }

    public function __construct(string $name)
    {
        $this->name = $name;
    }

    abstract public function fire();
}

class Minion extends Employee {
    public function fire()
    {
        echo "{$this->name}: I'll clear my desk\n";
    }
}

class CluedUp extends Employee {
    public function fire() {
        echo "{$this->name}: I'll call my lawyer\n";
    }
}

class WellConnected extends Employee {
    public function fire() {
        echo "{$this->name}: I'll call my dad\n";
    }
}
```

As you can see, this takes a name string and uses it to instantiate a particular Employee subtype at random. I can now delegate the details of instantiation to the Employee class’s recruit() method:

```php
$boss = new NastyBoss();
$boss->addEmployee(Employee::recruit("harry"));
$boss->addEmployee(Employee::recruit("bob"));
$boss->addEmployee(Employee::recruit("mary"));
$boss->projectFail();
$boss->projectFail();
$boss->projectFail();
```

 ■ Note: I use the term「factory」frequently in this chapter. a factory is a class or method with responsibility for generating objects.
 
You saw a simple example of such a class in Chapter 4. I placed a static method in the ShopProduct class called getInstance(). 

getInstance() is responsible for generating the correct ShopProduct subclass based on a database query. The ShopProduct class, therefore, has a dual role. It defines the ShopProduct type, but it also acts as a factory for concrete ShopProduct objects:

```php
public static function getInstance(int $id, PDO $pdo): ShopProduct    {        
    $stmt = $pdo->prepare("select * from products where id=?");        
    $result = $stmt->execute([$id]);

    $row = $stmt->fetch();        
    if (empty($row)) {            
        return null;        
    }        
    if ($row['type'] == "book") {            
        // instantiate a BookProduct object        
    } elseif ($row['type'] == "cd") {            
        // instantiate a CdProduct object        
    } else {            
        // instantiate a ShopProduct object        
    }        
    $product->setId($row['id']);        
    $product->setDiscount($row['discount']);        
    return $product;    
}
```

The getInstance() method uses a large if/else statement to determine which subclass to instantiate. Conditionals like this are quite common in factory code. Although you should attempt to excise large conditional statements from your projects, doing so often has the effect of pushing the conditional back to the moment at which an object is generated. This is not generally a serious problem because you remove parallel conditionals from your code in pushing the decision-making back to this point. In this chapter, then, I will examine some of the key Gang of Four patterns for generating objects.

getinstance() 方法使用一系列 if/ese 语句来决定实例化哪个子类。像这样的条件语句在工厂代码中十分常见。尽管我们常尝试从项目中消除大量的条件语句，但生成对象确实需要使用这些条件语句。一般来说这不是一个严重问题，因为我们将代码中并行的条件语句转移到 getInstance() 来，由 getInstance() 来决定对象生成。在本章中，我们将研究一些用于生成对象的关键模式，它们来源于《设计模式》一书。

### 3.2 The Singleton Pattern

The global variable is one of the great bugbears of the object-oriented programmer. The reasons should be familiar to you by now. Global variables tie classes into their context, undermining encapsulation (see Chapter 6,「Objects and Design,」and Chapter 8,「Some Pattern Principles,」for more on this). A class that relies on global variables becomes impossible to pull out of one application and use in another, without first ensuring that the new application itself defines the same global variables.

全局变量是面向对象程序员遇到的引发 bug 的主要原因之一。这是因为全局变量将类捆绑于特定的环境，破坏了封装（参见第 6 章及第 8 章）。如果新的应用程序无法保证一开始就定义了相同的全局变量，那么一个依赖于全局变量的类就无法从一个应用程序中提取出来并应用到新应用程序中。

Although this is undesirable, the unprotected nature of global variables can be a greater problem. Once you start relying on global variables, it is perhaps just a matter of time before one of your libraries declares a global that clashes with another declared elsewhere. You have seen already that, if you are not using namespaces, PHP is vulnerable to class name clashes. But this is much worse. PHP will not warn you when globals collide. The first you will know about it is when your script begins to behave oddly. Worse still, you may not notice any issues at all in your development environment. By using globals, though, you potentially leave your users exposed to new and interesting conflicts when they attempt to deploy your library alongside others.

Globals remain a temptation, however. This is because there are times when the sin inherent in global access seems a price worth paying in order to give all of your classes access to an object.

As I hinted, namespaces provide some protection from this. You can at least scope variables to a package, which means that third-party libraries are less likely to clash with your own system. Even so, the risk of collision exists within the namespace itself.

尽管这并不是我们想要的，但全局变量不受保护的本质的确是个很大的问题。一旦开始依赖全局变量，那么某个类库中声明的全局变量和其他地方声明的全局变量迟早会发生冲突。我们已经看到过 PHP 易受到类名冲突的影响，但全局变量的冲突更加糟糕——PHP 并不会对全局变量冲突发出任何警告。你也许只是发现代码行为有些古怪。更糟的是，在开发环境中你也许根本发现不了任何问题。因此如果在类库中使用全局变量，用户可能在尝试将你的类库与其他类库一同部署时遇到冲突。

然而，全局变量仍是一个诱惑。因为有时我们为了使所有类都能访问某个对象，会不惜忍受全局访问的缺陷。我提到过，命名空间在一定程度上避免了命名冲突。你至少可以将变量的作用域定义在包中，这意味着第三方的库与你的系统产生冲突的可能性大大降低了。即便如此，命名空间内部还是存在命名冲突。

#### 3.2.1 The Problem

Well-designed systems generally pass object instances around via method calls. Each class retains its independence from the wider context, collaborating with other parts of the system via clear lines of communication. Sometimes, though, you find that this forces you to use some classes as conduits for objects that do not concern them, introducing dependencies in the name of good design.

经过良好设计的系统一般通过方法调用来传递对象实例。每个类都会与背景环境保持独立并通过清晰的通信方式来与系统中其他部分进行协作。有时你需要使用一些作为对象间沟通渠道的类，此时就不得不引入依赖关系。

Imagine a Preferences class that holds application-level information. We might use a Preferences object to store data such as DSN strings (Data Source Names hold table and user information about a database), URL roots, file paths, and so on. This is the sort of information that will vary from installation to installation. The object may also be used as a notice board, a central location for messages that could be set or retrieved by otherwise unrelated objects in a system.

Passing a Preferences object around from object to object may not always be a good idea. Many classes that do not otherwise use the object could be forced to accept it simply so that they could pass it on to the objects that they work with. This is just another kind of coupling.

假设有一个用于保存应用程序信息的 Preferences 类。我们可能会使用一个 Preferences 对象来保存诸如 DSN（用于保存数据库的表及用户信息）字符串，URL 根目录、文件路径等数据。这些信息在你每次部署程序时都可能会有所不同。该对象也可被用作一个「公告板」，它是可以被系统中其他无关对象设置和获取消息的中心。

但在对象中传递 Preferences 对象并不总是个好主意。你可以让原来并不使用 Preferences 对象的类强制性地接受 Preferences。对象，以便这些类能传递 Preferences 对象给其他对象。但这样做产生了另一种形式的耦合。

You also need to be sure that all objects in your system are working with the same Preferences object. You do not want objects setting values on one object, while others read from an entirely different one.

Let’s distill the forces in this problem: 1) A Preferences object should be available to any object in your system. 2) A Preferences object should not be stored in a global variable, which can be overwritten. 3) There should be no more than one Preferences object in play in the system. This means that object Y can set a property in the Preferences object, and object Z can retrieve the same property, without either one talking to the other directly (assuming both have access to the Preferences object).

我们还需要保证系统中的所有对象都使用同一个 Preferences 对象。我们不希望一些对象在一个 Preferences 对象上设值，而其他对象从另外一个完全不同的 Preferences 对象上读取数据。让我们提炼出这个问题的几个关键点：1）Preferences 对象应该可以被系统中的任何对象使用。2）Preferences 对象不应该被储存在会被覆写的全局变量中。3）系统中不应超过一个 Preferences，对象。也就是说，Y 对象可设置 Preferences 对象的一个属性，而 Z 对象不需要通过其他对象（假设 Y 和 Z 都可以访问 Preferences）对象就可以直接获得该属性的值。

#### 3.2.2 Implementation

To address this problem, I can start by asserting control over object instantiation. Here, I create a class that cannot be instantiated from outside of itself. That may sound difficult, but it’s simply a matter of defining a private constructor:

1『定义一个私有的构造函数，可以实现，创建一个不能从外部实例化的类。』

```php
<?php

class Preferences {
    private $props = [];

    private function __construct() {
        //
    }

    public function setProperty(string $key, string $val) {
        $this->props[$key] = $val;
    }

    public function getProperty(string $key): string {
        return $this->props[$key];
    }
}
```

Of course, at this point, the Preferences class is entirely unusable. I have taken access restriction to an absurd level. Because the constructor is declared private, no client code can instantiate an object from it. The setProperty() and getProperty() methods are therefore redundant. I can use a static method and a static property to mediate object instantiation:

```php
<?php

class Preferences {
    private $props = [];
    private static $instance;

    private function __construct() {
        //
    }

    public static function getInstance() {
        if (empty(self::$instance)) {
            self::$instance = new Preferences();
        }
        return self::$instance;
    }

    public function setProperty(string $key, string $val) {
        $this->props[$key] = $val;
    }

    public function getProperty(string $key): string {
        return $this->props[$key];
    }
}
```

The \$instance property is private and static, so it cannot be accessed from outside the class. The getInstance() method has access, though. Because getInstance() is public and static, it can be called via the class from anywhere in a script:

```php
// listing 09.12

$pref = Preferences::getInstance();
$pref->setProperty("name", "matt");
unset($pref);   // remove the reference
$pref2 = Preferences::getInstance();
$pref2->setProperty("name", "matt");
echo $pref2->getProperty("name") . "\n"; // demonstrate value is not lost
```

The output is the single value we added to the Preferences object initially, available through a separate access:

```
matt
```

A static method cannot access object properties because it is, by definition, invoked in a class and not an object context. It can, however, access a static property. When getInstance() is called, I check the Preferences::\$instance property. If it is empty, then I create an instance of the Preferences class and store it in the property. Then I return the instance to the calling code. Because the static getInstance() method is part of the Preferences class, I have no problem instantiating a Preferences object, even though the constructor is private.

静态方法不能访问普通的对象属性，因为根据静态的定义，它只能被类而不是对象调用。但静态方法可以访问一个静态属性。

### 3.2.3 Consequences

So, how does the Singleton approach compare to using a global variable? First, the bad news. Both Singletons and global variables are prone to misuse. Because Singletons can be accessed from anywhere in a system, they can serve to create dependencies that can be hard to debug. Change a Singleton, and classes that use it may be affected. Dependencies are not a problem in themselves. After all, we create a dependency every time we declare that a method requires an argument of a particular type. The problem is that the global nature of the Singleton lets a programmer bypass the lines of communication defined by class interfaces. When a Singleton is used, the dependency is hidden away inside a method and not declared in its signature. This can make it harder to trace the relationships within a system. Singleton classes should therefore be deployed sparingly and with care.

Nevertheless, I think that moderate use of the Singleton pattern can improve the design of a system, saving you from horrible contortions as you pass objects unnecessarily around your system. Singletons represent an improvement over global variables in an object-oriented context. You cannot overwrite a Singleton with the wrong kind of data.

那么使用单例对象与使用全局变量相比，又如何呢？首先是坏的一面。单例和全局变量都可能被误用。因为单例在系统任何地方都可以被访问，所以它们可能会导致很难调试的依赖关系。如果改变一个单例，那么所有使用该单例的类可能都会受到影响。在这里，依赖本身并不是问题。毕竟，我们在每次声明一个有特定类型参数的方法时，也就创建了依赖关系。问题是，单例对象的全局化的性质会使程序员绕过类接口定义的通信线路。当单例被使用时，依赖便会被隐藏在方法内部，而并不会出现在方法声明中。这使得系统中的依赖关系更加难以追踪，因此需要谨慎小心地部署单例类。

然而，我认为适度地使用单例模式可以改进系统的设计。在系统中传递那些不必要的对象令人厌烦，而单例可以让你从中解放出来。在面向对象的开发环境中，单例模式是一种对于全局变量的改进。你无法用错误类型的数据覆写一个单例。这种保护在不支持命名空间的 PHP 版本里尤其重要。因为在 PHP 中命名冲突会在编译时被捕获，并使脚本停止运行。

### 3.3 Factory Method Pattern

Object-oriented design emphasizes the abstract class over the implementation. That is, it works with generalizations rather than specializations. The Factory Method pattern addresses the problem of how to create object instances when your code focuses on abstract types. The answer? Let specialist classes handle instantiation.

1『用特定的类来处理实例化。』

#### 3.3.1 The Problem

Imagine a personal organizer project that manages Appointment objects, among other object types. Your business group has forged a relationship with another company, and you must communicate appointment data to it using a format called BloggsCal. The business group warns you that you may face yet more formats as time wears on, though.

Staying at the level of interface alone, you can identify two participants right away. You need a data encoder that converts your Appointment objects into a proprietary format. Let’s call that class ApptEncoder. You need a manager class that will retrieve an encoder and maybe work with it to communicate with a third party. You might call that CommsManager. Using the terminology of the pattern, the CommsManager is the creator, and the ApptEncoder is the product. You can see this structure in Figure 9-3.

假设有一个关于个人事务管理的项目，其功能之一是管理 Appointment（预约）对象。我们的业务团队和另一个公司建立了关系，目前需要用一个叫做 BloggsCal 的格式来和他们交流预约相关的数据。但是业务团队提醒我们将来可能要面对更多的数据格式。在接口级别上，我们可以立即定义两个类。其一是需要一个数据编码器来把 Appointment 对象转换成一个专有的格式，将这个编码器命名为 Apptencoder 类；另外需要一个管理员类来获得编码器，并使用编码器与第三方进行通信，我们将这个管理类命名为 CommsManager 类。使用模式术语来描述的话，CommsManager 便是创建者（creator），而 ApptEncoder 是产品（product）你可以在图 9-3 中看到这个结构。

How do you get your hands on a real concrete ApptEncoder, though? You could demand that an ApptEncoder be passed to the CommsManager, but that simply defers your problem, and you want the buck to stop about here. Here I instantiate a BloggsApptEncoder object directly within the CommsManager class:

但是如何得到一个具体的 ApptEncoder 对象？我们可以要求传递 ApptEncoder 给 CommsManager，但这只是延缓了问题，而我们希望问题在此可以彻底解决。因此，先在 CommsManager 类中直接实例化 BloggsApptEncoder 对象。

```php
<?php

abstract class ApptEncoder {
    abstract public function encode(): string;
}

class BloggsApptEncoder extends ApptEncoder {
    public function encode(): string
    {
        return "Appointment data encoded in BloggsCal format\n";
    }
}

class MegaApptEncoder extends ApptEncoder {
    public function encode(): string
    {
        return "Appointment data encoded in MegaCal format\n";
    }
}

class CommsManager {
    public function getApptEncoder(): ApptEncoder {
        return new BloggsApptEncoder();
    }
}
```

The CommsManager class is responsible for generating BloggsApptEncoder objects. When the sands of corporate allegiance inevitably shift, and we are asked to convert our system to work with a new format called MegaCal, we can simply add a conditional into the CommsManager::getApptEncoder() method. This is the strategy we have used in the past, after all. Let’s build a new implementation of CommsManager that handles both BloggsCal and MegaCal formats:

CommsManager 类负责生成 BloggsApptEncoder 对象。当团队合作关系发生改变，而我们被要求转换系统来使用一个新的格式 MegaCal 时，可以只添加一个条件语句到 CommsManager::getApptEncoder() 方法。毕竟，这是我们以前用过的策略。下面来建立一个新的可以同时处理 BloggsCal 和 MegaCal格式的 CommsManager 的实现。

```php
class CommsManager {
    const BLOGGS = 1;
    const MEGA = 2;
    private $mode;

    public function __construct(int $mode)
    {
        $this->mode = $mode;
    }
     
    public function getApptEncoder(): ApptEncoder {
        switch ($this->mode) {
            case (self::BLOGGS):
                return new BloggsApptEncoder();
            default:
                return new MegaApptEncoder();
        }
        
    }
}

$man = new CommsManager(CommsManager::MEGA);
echo (get_class($man->getApptEncoder())) . "\n";
$man = new CommsManager(CommsManager::BLOGGS);
echo (get_class($man->getApptEncoder())) . "\n";
```

I use constant flags to define two modes in which the script might be run: MEGA and BLOGGS. I use a switch statement in the getApptEncoder() method to test the \$mode property and instantiate the appropriate implementation of ApptEncoder.

There is little wrong with this approach. Conditionals are sometimes considered examples of bad 「code smells,」but object creation often requires a conditional at some point. You should be less sanguine if you see duplicate conditionals creeping into your code. The CommsManager class provides functionality for communicating calendar data. Imagine that the protocols you work with require you to provide header and footer data to delineate each appointment. I can extend the previous example to support a getHeaderText() method:

这种方式仍有点小小的缺陷。通常情况下，创建对象的确需要指定条件，但有时候条件语句会被当做坏的「代码味道」的象征。如果重复的条件语句蔓延在代码中，我们不应该感到乐观。CommsManager 类已经能够提供交流日历数据的功能。但是，假设我们所使用的协议要求提供页眉和页脚数据来描述每次预约，情况又将如何呢？下面扩展之前的例子来支持 getHeaderText() 方法。

```php
class CommsManager {
    const BLOGGS = 1;
    const MEGA = 2;
    private $mode;

    public function __construct(int $mode)
    {
        $this->mode = $mode;
    }
     
    public function getApptEncoder(): ApptEncoder {
        switch ($this->mode) {
            case (self::BLOGGS):
                return new BloggsApptEncoder();
            default:
                return new MegaApptEncoder();
        }
        
    }

    public function getHeaderText(): string {
        switch ($this->mode) {
            case (self::BLOGGS):
                return "BloggsCal header\n";
            default:
                return "MegaCal header\n";
        }
        
    }
}
```

As you can see, the need to support header output has forced me to duplicate the protocol conditional test. This will become unwieldy as I add new protocols, especially if I also add a getFooterText() method. 

So, let’s summarize the problem so far: 1) I do not know until runtime the kind of object I need to produce (BloggsApptEncoder or MegaApptEncoder). 2) I need to be able to add new product types with relative ease (SyncML support is just a new business deal away!). 3) Each product type is associated with a context that requires other customized operations (e.g., getHeaderText(), getFooterText()).

Additionally, I am using conditional statements, and you have seen already that these are naturally replaceable by polymorphism. The Factory Method pattern enables you to use inheritance and polymorphism to encapsulate the creation of concrete products. In other words, you create a CommsManager subclass for each protocol, each one implementing the getApptEncoder() method.

之前已介绍过这些条件语句可以被多态代替，而工厂方法模式恰好能让我们用继承和多态来封装具体产品的创建。换句话说，我们要为每种协议创建 CommsManager 的一个子类，而每一个子类都要实现 getApptEncoder() 方法。

#### 3.3.2 Implementation

The Factory Method pattern splits creator classes from the products they are designed to generate. The creator is a factory class that defines a method for generating a product object. If no default implementation is provided, it is left to creator child classes to perform the instantiation. Typically, each creator subclass instantiates a parallel product child class. I can redesignate CommsManager as an abstract class. That way, I keep a flexible superclass and put all my protocol-specific code in the concrete subclasses. You can see this alteration in Figure 9-4.

Here’s some simplified code:

```php
<?php

abstract class ApptEncoder {
    abstract public function encode(): string;
}

class BloggsApptEncoder extends ApptEncoder {
    public function encode(): string
    {
        return "Appointment data encoded in BloggsCal format\n";
    }
}

class MegaApptEncoder extends ApptEncoder {
    public function encode(): string
    {
        return "Appointment data encoded in MegaCal format\n";
    }
}

abstract class CommsManager {
    abstract public function getHeaderText(): string;
    abstract public function getApptEncoder(): ApptEncoder;
    abstract public function getFooterText(): string;
}

class BloggsCommsManager extends CommsManager {
     
    public function getApptEncoder(): ApptEncoder {
        return new BloggsApptEncoder();
    }

    public function getHeaderText(): string {
        return "BloggsCal header\n";
    }

    public function getFooterText(): string {
        return "BloggsCal footer\n";
    }
}

$mgr = new BloggsCommsManager();
echo $mgr->getHeaderText();
echo $mgr->getApptEncoder()->encode();
echo $mgr->getFooterText();
```

So, when I am required to implement MegaCal, supporting it is simply a matter of writing a new implementation for my abstract classes. Figure 9-5 shows the MegaCal classes.

### 3.3.3 Consequences

Notice that the creator classes mirror the product hierarchy. This is a common consequence of the Factory Method pattern and disliked by some as a special kind of code duplication. Another issue is the possibility that the pattern could encourage unnecessary subclassing. If your only reason for subclassing a creator is to deploy the Factory Method pattern, you may need to think again (that’s why I introduced the header and footer constraints to the example here).

1『对的，如果我只想创建 getApptEncoder 子类，目前的工厂模式额外创建了 getHeaderText 和 getFooterText 两个子类。』

I have focused only on appointments in my example. If I extend it somewhat to include to-do items and contacts, I face a new problem. I need a structure that will handle sets of related implementations at one time. The Factory Method pattern is often used with the Abstract Factory pattern, as you will see in the next section.

请注意我们的创建者类与产品的层次结构是非常相似的。这是使用工厂方法模式的常见结果，这形成了一种特殊的代码重复，因而被一些人所不喜欢。另一个问题是该模式可能会导致不必要的子类化。如果你为创建者类创建子类的原因只是为了实现工厂方法模式，那么最好再考虑下（这就是为什么在例子中引进页眉和页脚）。在示例中我们只关注「预约」功能。如果想扩展一下功能，使其能够处理「待办事宜」及联系人，那么将会遇到新问题。我们需要一个可以同时处理一组相关实现的架构。正如我们在下节中将看到的，工厂方法模式经常和抽象工厂模式一起使用。

### 3.4 Abstract Factory Pattern

In large applications, you may need factories that produce related sets of classes. The Abstract Factory pattern addresses this problem.

在大型应用中，我们很可能需要工厂来产生一组相关的类。抽象工厂模式可解决这个问题。

#### 3.4.1 The Problem

Let’s look again at the organizer example. I manage encoding in two formats, BloggsCal and MegaCal. I can grow this structure horizontally by adding more encoding formats, but how can I grow vertically, adding encoders for different types of PIM objects? In fact, I have been working toward this pattern already. In Figure 9-6, you can see the parallel families with which I will want to work. These are appointments (Appt), things to do (Ttd), and contacts (Contact).

再来看一下之前实现的个人事务管理的示例。我们以 BloggsCal 和 MegaCal 这两种格式管理编码。我们可以通过加入更多编码格式来使此结构「横向」增长，但如何通过给不同类型的 PM 对象加入编码器使它「纵向」增长呢？事实上，我们一直在应用该模式。在图 9-6 中，可以看到我们使用的相似的类层次结构，分别是预约（Appt）、待办事宜（Ttd）、和联系人（Contact）。

The BloggsCal classes are unrelated to one another by inheritance (although they could implement a common interface), but they are functionally parallel. If the system is currently working with BloggsTtdEncoder, it should also be working with BloggsContactEncoder. To see how I enforce this, you can begin with the interface, as I did with the Factory Method pattern (see Figure 9-7).

BloggsCal 的类与其他格式（如 MegaCal）互相没有关联（尽管它们实现了一个公共的接口），但它们的功能相似。所以如果系统目前正在使用 BloggsTtdEncoder，那么它应该也能使用 BloggsContactEncoder。看一下如何做到这一点。我们仍从接口开始着手，就如在工厂方法模式中所做的那样（见图 9-7)。

### 3.4.2 Implementation

The abstract CommsManager class defines the interface for generating each of the three products (ApptEncoder, TtdEncoder, and ContactEncoder). You need to implement a concrete creator in order to actually generate the concrete products for a particular family. I illustrate that for the BloggsCal format in Figure 9-8.

CommsManager 抽象类定义了用于生成 3 个产品（ApptEncoder、TtdEncoder 和 ContactEncoder）的接口。我们需要先实现一个具体的创建者，然后才能创建一个特定类型的具体产品。图 9-8 创建了 BloggsCal 格式的创建者。

Here is a code version of CommsManager and BloggsCommsManager:

```php
abstract class CommsManager {
    abstract public function getHeaderText(): string;
    abstract public function getApptEncoder(): ApptEncoder;
    abstract public function getTtdEncoder(): getTtdEncoder;
    abstract public function getContactEncoder(): getContactEncoder;
    abstract public function getFooterText(): string;
}

class BloggsCommsManager extends CommsManager {
    
    public function getHeaderText(): string {
        return "BloggsCal header\n";
    }

    public function getApptEncoder(): ApptEncoder {
        return new BloggsApptEncoder();
    }

    public function getTtdEncoder(): TtEncoder {
        return new BloggsTtdEncoder();
    }

    public function getContactEncoder(): ContactEncoder {
        return new BloggsContactEncoder();
    }

    public function getFooterText(): string {
        return "BloggsCal footer\n";
    }
}
```

Notice that I use the Factory Method pattern in this example. getContactEncoder() is abstract in CommsManager and implemented in BloggsCommsManager. Design patterns tend to work together in this way, one pattern creating the context that lends itself to another. In Figure 9-9, I add support for the MegaCal format.

请注意，在这个例子中使用了工厂方法模式。getContactEncoder() 是 CommsManager 的抽象方法，并在 BloggsCommsManager 中被实现。设计模式间经常会这样协作：一个模式创建可以把它自己引入到另一个模式的上下文环境。在图 9-9 中，我们加入了对 MegaCal 格式的支持。

#### 3.4.3 Consequences

So, let’s look at what this pattern buys: 1) First, I decouple my system from the details of implementation. I can add or remove any number of encoding formats in my example without causing a knock-on effect. 2) I enforce the grouping of functionally related elements of my system. So, by using BloggsCommsManager, I am guaranteed that I will work only with BloggsCal-related classes. 3) Adding new products can be a pain. Not only do I have to create concrete implementations of the new product, but I also have to amend the abstract creator and every one of its concrete implementers in order to support it.

首先，将系统与实现的细节分离开来。我们可以在示例中添加或移除任意数目的编码格式而不会影响系统；对系统中功能相关的元素强制进行组合。因此，通过使用 BloggsCommsManager，可以确保只使用与 BloggsCal 相关的类；添加新产品将会令人苦恼。因为不仅要创建新产品的具体实现，而且为了支持它，我们必须修改抽象创建者和它的每一个具体实现。

Many implementations of the Abstract Factory pattern use the Factory Method pattern. This may be because most examples are written in Java or C++. PHP, however, does not have to enforce a return type for a method (though it now can), which affords us some flexibility that we might leverage. Rather than create separate methods for each Factory Method, you can create a single make() method that uses a flag argument to determine which object to return:

抽象工厂模式的许多实现都会使用工厂方法模式，这可能是因为大多数范例都是用 Java 或者 C++ 写的。但是 PHP 并不会强制规定方法的返回类型，这给了我们一些可能利用的灵活性。我们可以创建一个使用标志参数来决定返回什么对象的单一的 make() 方法，而不用给每个工厂方法创建独立的方法。

```php
interface Encoder {
    public function encode(): string;
}

abstract class CommsManager {
    const APPT = 1;
    const TTD = 2;
    const CONTACT =3;
    abstract public function getHeaderText(): string;
    abstract public function make(int $flag_int): Encoder;
    abstract public function getFooterText(): string;
}

class BloggsCommsManager extends CommsManager {
    
    public function getHeaderText(): string {
        return "BloggsCal header\n";
    }

    public function make(int $flag_int): Encoder {
        switch ($flag_int) {
            case self::APPT:
                return new BloggsApptEncoder();
            case self::CONTACT:
                return new BloggsContactEncoder();
            case self::TTD:
                return new BloggsTtdEncoder();
        }
    }

    public function getFooterText(): string {
        return "BloggsCal footer\n";
    }
}
```

As you can see, I have made the class interface more compact. I’ve done this at a considerable cost, though. In using a factory method, I define a clear interface and force all concrete factory objects to honor it. In using a single make() method, I must remember to support all product objects in all the concrete creators. I also introduce parallel conditionals, as each concrete creator must implement the same flag tests. A client class cannot be certain that concrete creators generate all the products because the internals of make() are a matter of choice in each case.

On the other hand, I can build more flexible creators. The base creator class can provide a make() method that guarantees a default implementation of each product family. Concrete children could then modify this behavior selectively. It would be up to implementing creator classes to call the default make() method after providing their own implementation. You will see another variation on the Abstract Factory pattern in the next section.

可以看出，类的接口变得更加紧凑。但是这样做也有一定代价。在使用工厂方法时，我们定义了一个清晰的接口并强制所有具体的工厂对象遵循它。而使用单一的 make() 方法，我们必须在所有的具体创建者中支持所有的产品对象。同时，我们也引入了平行条件，因为每个具体创建者都必须实现相同的标志检测（flag test）。客户类无法确定具体的创建者是否可以生成所有产品，因为 make() 方法的内部需要对每种情况都进行考虑并作出选择。另一方面，我们可以创建更灵活的创建者。创建者基类可以提供 make() 方法来保证每个产品家族有一个默认实现。具体子类可以选择性地改变这一行为。子类可以实现自己的 make() 方法并调用，由此决定生成何种对象。这些创建者子类可以自行决定是否在执行自己的 make() 方法后调用父类的 make() 方法。我们会在下一节中介绍抽象工厂模式的另一个变形。

### 3.5 Prototype

The emergence of parallel inheritance hierarchies can be a problem with the Factory Method pattern. This is a kind of coupling that makes some programmers uncomfortable. Every time you add a product family, you are forced to create an associated concrete creator (the BloggsCal encoders are matched by BloggsCommsManager, for example). In a system that grows fast enough to encompass many products, maintaining this kind of relationship can quickly become tiresome.

One way of avoiding this dependency is to use PHP’s clone keyword to duplicate existing concrete products. The concrete product classes themselves then become the basis of their own generation. This is the Prototype pattern. It enables you to replace inheritance with composition. This in turn promotes runtime flexibility and reduces the number of classes you must create.

平行继承层次的出现是工厂方法模式带来的一个问题。这是一种让一些程序员不舒服的耦合。每次添加产品家族时，你就被迫去创建一个相关的具体创建者（比如编码器 BloggsCal 和 BloggsCommsManager 匹配）。在一个快速增长的系统里会包含越来越多的产品，而维护这种关系便会很快令人厌烦。一个避免这种依赖的办法是使用 PHP 的 clone 关键词复制已存在的具体产品。然后，具体产品类本身便成为它们自己生成的基础。这便是原型模式。使用该模式我们可以用组合代替继承。这样的转变则促进了代码运行时的灵活性，并减少了必须创建的类。

#### 3.5.1 The Problem

Imagine a Civilization-style web game in which units operate on a grid of tiles. Each tile can represent sea, plains, or forests. The terrain type constrains the movement and combat abilities of units occupying the tile. You might have a TerrainFactory object that serves up Sea, Forest, and Plains objects. You decide that you will allow the user to choose among radically different environments, so the Sea object is an abstract superclass implemented by MarsSea and EarthSea. Forest and Plains objects are similarly implemented. The forces here lend themselves to the Abstract Factory pattern. You have distinct product hierarchies (Sea, Plains, Forests), with strong family relationships cutting across inheritance (Earth, Mars). Figure 9-10 presents a class diagram that shows how you might deploy the Abstract Factory and Factory Method patterns to work with these products.

假设有一款「文明」风格的网络游戏，可在区块组成的格子中操作战斗单元（unit）。每个区块分别代表海洋、平原和森林。地形的类别约束了占有区块的单元的移动和格斗能力。我们可以有一个 TerrainFactory 对象来提供 sea、Forest 和 Plains 对象，我们决定允许用户在完全不同的环境里选择，于是 sea 可能是 MarsSea 和 Earthsea 的抽象父类。Forest（森林）和 Plains（平原）对象也会有相似的实现。这里的分支便构成了抽象工厂模式。我们有截然不同的产品体系（sea、Plains、Forest），而这些产品家族间有超越继承的紧密联系，如 Earth（地球）和 Mars（火星），它们都同时存在海洋、森林和平原地形。图 9-10 所示的类图展示了如何对这些产品应用抽象工厂和工厂方法模式。

As you can see, I rely on inheritance to group the terrain family for the products that a factory will generate. This is a workable solution, but it requires a large inheritance hierarchy, and it is relatively inflexible. When you do not want parallel inheritance hierarchies, and when you need to maximize runtime flexibility, the Prototype pattern can be used in a powerful variation on the Abstract Factory pattern.

你可以看到，我们依赖继承来组合工厂生成的 terrain（地形）家族产品。这的确是一个可行的解决方案，但这需要有一个大型的继承体系，并且相对来说不那么灵活。当你不想要平行的继承体系而需要最大化运行时的灵活性时，可以使用抽象工厂模式的强大变形——原型模式。

#### 3.5.2 Implementation

When you work with the Abstract Factory/Factory Method patterns, you must decide, at some point, which concrete creator you wish to use, probably by checking some kind of preference flag. As you must do this anyway, why not simply create a factory class that stores concrete products, and then populate this during initialization? You can cut down on a couple of classes this way and, as you shall see, take advantage of other benefits. Here’s some simple code that uses the Prototype pattern in a factory:

当使用抽象工厂模式或工厂方法模式时，必须决定使用哪个具体的创建者，这很可能是通过检査配置的值来决定的。既然必须这样做，那为什么不简单地创建一个保存具体产品的工厂类，并在初始化时就加入这种做法呢？这样除了可以减少类的数量，还有其他好处。下面是在工厂中使用原型模式的简单代码：

```php
<?php

class Sea {
    //
}

class EarthSea extends Sea {
    //
}

class MarsSea extends Sea {
    //
}

class Plains {
    //
}

class EarthPlains extends Plains {
    //
}

class MarsPlains extends Plains {
    //
}

class Forest {
    //
}

class EarthForest extends Forest {
    //
}

class MarsForest extends Forest {
    //
}

class TerrainFactory {
    private $sea;
    private $plains;
    private $forest;

    public function __construct(Sea $sea, Plains $plains, Forest $forest) {
        $this->sea = $sea;
        $this->plains = $plains;
        $this->forest = $forest;
    }

    public function getSea(): Sea {
        return clone $this->sea;
    }

    public function getPlains(): Plains {
        return clone $this->plains;
    }

    public function getForest(): Forest {
        return clone $this->forest;
    }
}

$factory = new TerrainFactory(
    new EarthSea(),
    new EarthPlains(),
    new EarthForest()
);

print_r($factory->getSea());
print_r($factory->getPlains());
print_r($factory->getForest());
```

As you can see, I load up a concrete TerrainFactory with instances of product objects. When a client calls getSea(), I return a clone of the Sea object that I cached during initialization. This structure buys me additional flexibility. Want to play a game on a new planet with Earth-like seas and forests, but Mars-like plains? No need to write a new creator class—you can simply change the mix of classes you add to TerrainFactory:

```php
$factory = new TerrainFactory(
    new EarthSea(),
    new MarsPlains(),
    new EarthForest()
);
```

So the Prototype pattern allows you to take advantage of the flexibility afforded by composition. We get more than that, though. Because you are storing and cloning objects at runtime, you reproduce object state when you generate new products. Imagine that Sea objects have a \$navigability property. The property influences the amount of movement energy a sea tile saps from a vessel and can be set to adjust the difficulty level of a game:

```php
class Sea {
    private $navigability = 0;

    public function __construct(int $navigability) {
        $this->navigability = $navigability;
    }
}
```

Now when I initialize the TerrainFactory object, I can add a Sea object with a navigability modifier. This will then hold true for all Sea objects served by TerrainFactory:

```php
$factory = new TerrainFactory(
    new EarthSea(-1),
    new EarthPlains(),
    new EarthForest()
);
```

This flexibility is also apparent when the object you wish to generate is composed of other objects.

 ■ Note: I covered object cloning in Chapter 4. the clone keyword generates a shallow copy of any object to which it is applied. this means that the product object will have the same properties as the source. if any of the source’s properties are objects, then these will not be copied into the product. instead, the product will reference the same object properties. it is up to you to change this default and to customize object copying in any other way, by implementing a \_\_clone() method. this is called automatically when the clone keyword is used.

我们在第 4 章中介绍了对象克隆。clone 关健字能给应用的对象生成一个浅复制（shallow copy）。也就是说，产品对象会具有和源对象一样的属性。如果源对象的任何属性是对象，那么这些对象属性不会被直接复制到产品中，相反产品会引用同样的对象属性。通过实现  \_\_clone() 方法，可以改变克隆的默认行为，并定制对象复制的方式，而这在 clone 关健词被使用时会被自动调用。

Perhaps all Sea objects can contain Resource objects (FishResource, OilResource, etc.). According to a preference flag, we might give all Sea objects a FishResource by default. Remember that if your products reference other objects, you should implement a \_\_clone() method to ensure that you make a deep copy:

如果你想生成的对象是由其他对象组合而成的，以上代码显然颇具灵活性。假设所有的 Sea 对象都能包含 Resource 对象（FishResource、OilResource 等）。通过配置的值，可以给所有的 Sea 对象默认提供一个 FishResource 对象。要记住的是如果产品对象引用了其他对象，那么你应该实现  \_\_clone() 方法来保证你得到的是深复制（deep copy）。

```php
class Contained {
}

class Container {    

    public $contained;

    function __construct()    {        
        $this->contained = new Contained();    
    }

    function __clone()   {        
        // Ensure that cloned object holds a        
        // clone of self::$contained and not a reference to it        
        $this->contained = clone $this->contained;    
    }
}
```


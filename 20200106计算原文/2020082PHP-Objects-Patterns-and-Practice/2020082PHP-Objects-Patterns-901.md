# 09 Generating Objects

Creating objects is a messy business. So, many object-oriented designs deal with nice, clean abstract classes, taking advantage of the impressive flexibility afforded by polymorphism (the switching of concrete implementations at runtime). To achieve this flexibility, though, I must devise strategies for object generation. This is the topic I will look at in this chapter.

This chapter will cover the following patterns:

The Singleton pattern: A special class that generates one—and only one—object instance

The Factory Method pattern: Building an inheritance hierarchy of creator classes

The Abstract Factory pattern: Grouping the creation of functionally related products

The Prototype pattern: Using clone to generate objects

The Service Locator pattern: Asking your system for objects

The Dependency Injection pattern: Letting your system give you objects

Problems and Solutions in Generating Objects

Object creation can be a weak point in object-oriented design. In the previous chapter, you saw the principle,「Code to an interface, not to an implementation.」To this end, you are encouraged to work with abstract supertypes in your classes. This makes code more flexible, allowing you to use objects instantiated from different concrete subclasses at runtime. This has the side effect that object instantiation is deferred.

Here’s a class that accepts a name string and instantiates a particular object:

// listing 09.01

abstract class Employee{    protected $name;

    public function __construct(string $name)    {        $this->name = $name;    }

    abstract public function fire();}

179

Chapter 9 ■ GeneratinG ObjeCts

// listing 09.02

class Minion extends Employee{    public function fire()    {        print "{$this->name}: I'll clear my desk\n";    }}

// listing 09.03

class NastyBoss{    private $employees = [];

    public function addEmployee(string $employeeName)    {        $this->employees[] = new Minion($employeeName);    }

    public function projectFails()    {        if (count($this->employees) > 0) {            $emp = array_pop($this->employees);            $emp->fire();        }    }}

// listing 09.04

$boss = new NastyBoss();$boss->addEmployee("harry");$boss->addEmployee("bob");$boss->addEmployee("mary");$boss->projectFails();

mary: I'll clear my desk

As you can see, I define an abstract base class, Employee, with a downtrodden implementation, Minion. 

Given a name string, the NastyBoss::addEmployee() method instantiates a new Minion object. Whenever a NastyBoss object runs into trouble (via the NastyBoss::projectFails() method), it looks for a Minion to fire.

By instantiating a Minion object directly in the NastyBoss class, we limit flexibility. If a NastyBoss 

object could work with any instance of the Employee type, we could make our code amenable to variation at runtime as we add more Employee specializations. You should find the polymorphism in Figure 9-1 familiar.

180

Chapter 9 ■ GeneratinG ObjeCts

Figure 9-1.  Working with an abstract type enables polymorphism

If the NastyBoss class does not instantiate a Minion object, where does it come from? Authors often 

duck out of this problem by constraining an argument type in a method declaration, and then conveniently omitting to show the instantiation in anything other than a test context:

// listing 09.05

class NastyBoss{    private $employees = [];

    public function addEmployee(Employee $employee)    {        $this->employees[] = $employee;    }

    public function projectFails()    {        if (count($this->employees)) {            $emp = array_pop($this->employees);            $emp->fire();        }    }}

// listing 09.06

// new Employee class...

class CluedUp extends Employee{    public function fire()    {

181

Chapter 9 ■ GeneratinG ObjeCts

        print "{$this->name}: I'll call my lawyer\n";    }}

// listing 09.07

$boss = new NastyBoss();$boss->addEmployee(new Minion("harry"));$boss->addEmployee(new CluedUp("bob"));$boss->addEmployee(new Minion("mary"));$boss->projectFails();$boss->projectFails();$boss->projectFails();

mary: I'll clear my deskbob: I'll call my lawyerharry: I'll clear my desk

Although this version of the NastyBoss class works with the Employee type, and therefore benefits from polymorphism, I still haven’t defined a strategy for object creation. Instantiating objects is a dirty business, but it has to be done. This chapter is about classes and objects that work with concrete classes, so that the rest of your classes do not have to.

If there is a principle to be found here, it is「delegate object instantiation.」I did this implicitly in the previous 

example by demanding that an Employee object be passed to the NastyBoss::addEmployee() method. I could, however, equally delegate to a separate class or method that takes responsibility for generating Employee objects. Here I add a static method to the Employee class that implements a strategy for object creation:

// listing 09.08abstract class Employee{    protected $name;    private static $types = ['Minion', 'CluedUp', 'WellConnected'];

    public static function recruit(string $name)    {        $num = rand(1, count(self::$types)) - 1;        $class = __NAMESPACE__ . "\\".self::$types[$num];        return new $class($name);    }

    public function __construct(string $name)    {        $this->name = $name;    }

    abstract public function fire();}

// listing 09.09

// new Employee class...

182

Chapter 9 ■ GeneratinG ObjeCts

class WellConnected extends Employee{    public function fire()    {        print "{$this->name}: I'll call my dad\n";    }}

As you can see, this takes a name string and uses it to instantiate a particular Employee subtype at 

random. I can now delegate the details of instantiation to the Employee class’s recruit() method:

// listing 09.10

$boss = new NastyBoss();$boss->addEmployee(Employee::recruit("harry"));$boss->addEmployee(Employee::recruit("bob"));$boss->addEmployee(Employee::recruit("mary"));

You saw a simple example of such a class in Chapter 4. I placed a static method in the ShopProduct class 

called getInstance().

 i use the term「factory」frequently in this chapter. a factory is a class or method with responsibility 

 ■ Note for generating objects.

getInstance() is responsible for generating the correct ShopProduct subclass based on a database 

query. The ShopProduct class, therefore, has a dual role. It defines the ShopProduct type, but it also acts as a factory for concrete ShopProduct objects:

    public static function getInstance(int $id, PDO $pdo): ShopProduct    {        $stmt = $pdo->prepare("select * from products where id=?");        $result = $stmt->execute([$id]);

        $row = $stmt->fetch();        if (empty($row)) {            return null;        }        if ($row['type'] == "book") {            // instantiate a BookProduct object        } elseif ($row['type'] == "cd") {            // instantiate a CdProduct object        } else {            // instantiate a ShopProduct object        }        $product->setId($row['id']);        $product->setDiscount($row['discount']);        return $product;    }

183

Chapter 9 ■ GeneratinG ObjeCts

The getInstance() method uses a large if/else statement to determine which subclass to instantiate. 

Conditionals like this are quite common in factory code. Although you should attempt to excise large conditional statements from your projects, doing so often has the effect of pushing the conditional back to the moment at which an object is generated. This is not generally a serious problem because you remove parallel conditionals from your code in pushing the decision-making back to this point.

In this chapter, then, I will examine some of the key Gang of Four patterns for generating objects.

The Singleton Pattern

The global variable is one of the great bugbears of the object-oriented programmer. The reasons should be familiar to you by now. Global variables tie classes into their context, undermining encapsulation (see Chapter 6,「Objects and Design,」and Chapter 8,「Some Pattern Principles,」for more on this). A class that relies on global variables becomes impossible to pull out of one application and use in another, without first ensuring that the new application itself defines the same global variables.

Although this is undesirable, the unprotected nature of global variables can be a greater problem. Once 

you start relying on global variables, it is perhaps just a matter of time before one of your libraries declares a global that clashes with another declared elsewhere. You have seen already that, if you are not using namespaces, PHP is vulnerable to class name clashes. But this is much worse. PHP will not warn you when globals collide. The first you will know about it is when your script begins to behave oddly. Worse still, you may not notice any issues at all in your development environment. By using globals, though, you potentially leave your users exposed to new and interesting conflicts when they attempt to deploy your library alongside others.

Globals remain a temptation, however. This is because there are times when the sin inherent in global 

access seems a price worth paying in order to give all of your classes access to an object.

As I hinted, namespaces provide some protection from this. You can at least scope variables to a 

package, which means that third-party libraries are less likely to clash with your own system. Even so, the risk of collision exists within the namespace itself.

The ProblemWell-designed systems generally pass object instances around via method calls. Each class retains its independence from the wider context, collaborating with other parts of the system via clear lines of communication. Sometimes, though, you find that this forces you to use some classes as conduits for objects that do not concern them, introducing dependencies in the name of good design.

Imagine a Preferences class that holds application-level information. We might use a Preferences 

object to store data such as DSN strings (Data Source Names hold table and user information about a database), URL roots, file paths, and so on. This is the sort of information that will vary from installation to installation. The object may also be used as a notice board, a central location for messages that could be set or retrieved by otherwise unrelated objects in a system.

Passing a Preferences object around from object to object may not always be a good idea. Many classes 

that do not otherwise use the object could be forced to accept it simply so that they could pass it on to the objects that they work with. This is just another kind of coupling.

You also need to be sure that all objects in your system are working with the same Preferences object. 

You do not want objects setting values on one object, while others read from an entirely different one.

Let’s distill the forces in this problem:

•	

A Preferences object should be available to any object in your system.

184

Chapter 9 ■ GeneratinG ObjeCts

•	

•	

A Preferences object should not be stored in a global variable, which can be overwritten.

There should be no more than one Preferences object in play in the system. This means that object Y can set a property in the Preferences object, and object Z can retrieve the same property, without either one talking to the other directly (assuming both have access to the Preferences object).

ImplementationTo address this problem, I can start by asserting control over object instantiation. Here, I create a class that cannot be instantiated from outside of itself. That may sound difficult, but it’s simply a matter of defining a private constructor:

class Preferences{    private $props = [];

    private function __construct()    {    }

    public function setProperty(string $key, string $val)    {        $this->props[$key] = $val;    }

    public function getProperty(string $key): string    {        return $this->props[$key];    }}

Of course, at this point, the Preferences class is entirely unusable. I have taken access restriction to an absurd level. Because the constructor is declared private, no client code can instantiate an object from it. The setProperty() and getProperty() methods are therefore redundant.

I can use a static method and a static property to mediate object instantiation:

// listing 09.11

class Preferences{    private $props = [];    private static $instance;

    private function __construct()    {    }

    public static function getInstance()    {

185

Chapter 9 ■ GeneratinG ObjeCts

        if (empty(self::$instance)) {            self::$instance = new Preferences();        }        return self::$instance;    }

    public function setProperty(string $key, string $val)    {        $this->props[$key] = $val;    }

    public function getProperty(string $key): string    {        return $this->props[$key];    }}

The $instance property is private and static, so it cannot be accessed from outside the class. The 

getInstance() method has access, though. Because getInstance() is public and static, it can be called via the class from anywhere in a script:

// listing 09.12

$pref = Preferences::getInstance();$pref->setProperty("name", "matt");unset($pref); // remove the reference$pref2 = Preferences::getInstance();print $pref2->getProperty("name") ."\n"; // demonstrate value is not lost

The output is the single value we added to the Preferences object initially, available through a separate 

access:

matt

A static method cannot access object properties because it is, by definition, invoked in a class and 

not an object context. It can, however, access a static property. When getInstance() is called, I check the Preferences::$instance property. If it is empty, then I create an instance of the Preferences class and store it in the property. Then I return the instance to the calling code. Because the static getInstance() method is part of the Preferences class, I have no problem instantiating a Preferences object, even though the constructor is private.

Figure 9-2 shows the Singleton pattern.

186

Chapter 9 ■ GeneratinG ObjeCts

Figure 9-2.  An example of the Singleton pattern

ConsequencesSo, how does the Singleton approach compare to using a global variable? First, the bad news. Both Singletons and global variables are prone to misuse. Because Singletons can be accessed from anywhere in a system, they can serve to create dependencies that can be hard to debug. Change a Singleton, and classes that use it may be affected. Dependencies are not a problem in themselves. After all, we create a dependency every time we declare that a method requires an argument of a particular type. The problem is that the global nature of the Singleton lets a programmer bypass the lines of communication defined by class interfaces. When a Singleton is used, the dependency is hidden away inside a method and not declared in its signature. This can make it harder to trace the relationships within a system. Singleton classes should therefore be deployed sparingly and with care.

Nevertheless, I think that moderate use of the Singleton pattern can improve the design of a system, 

saving you from horrible contortions as you pass objects unnecessarily around your system.

Singletons represent an improvement over global variables in an object-oriented context. You cannot 

overwrite a Singleton with the wrong kind of data.

Factory Method Pattern

Object-oriented design emphasizes the abstract class over the implementation. That is, it works with generalizations rather than specializations. The Factory Method pattern addresses the problem of how to create object instances when your code focuses on abstract types. The answer? Let specialist classes handle instantiation.

187

Chapter 9 ■ GeneratinG ObjeCts

The ProblemImagine a personal organizer project that manages Appointment objects, among other object types. Your business group has forged a relationship with another company, and you must communicate appointment data to it using a format called BloggsCal. The business group warns you that you may face yet more formats as time wears on, though.

Staying at the level of interface alone, you can identify two participants right away. You need a data 

encoder that converts your Appointment objects into a proprietary format. Let’s call that class ApptEncoder. You need a manager class that will retrieve an encoder and maybe work with it to communicate with a third party. You might call that CommsManager. Using the terminology of the pattern, the CommsManager is the creator, and the ApptEncoder is the product. You can see this structure in Figure 9-3.

Figure 9-3.  Abstract creator and product classes

How do you get your hands on a real concrete ApptEncoder, though?You could demand that an ApptEncoder be passed to the CommsManager, but that simply defers your 

problem, and you want the buck to stop about here. Here I instantiate a BloggsApptEncoder object directly within the CommsManager class:

// listing 09.13

abstract class ApptEncoder{    abstract public function encode(): string;}

// listing 09.14

class BloggsApptEncoder extends ApptEncoder{    public function encode(): string    {        return "Appointment data encoded in BloggsCal format\n";    }}

// listing 09.15

class MegaApptEncoder extends ApptEncoder{    public function encode(): string    {        return "Appointment data encoded in MegaCal format\n";    }}

188

Chapter 9 ■ GeneratinG ObjeCts

// listing 09.16

class CommsManager{    public function getApptEncoder(): ApptEncoder    {        return new BloggsApptEncoder();    }}

The CommsManager class is responsible for generating BloggsApptEncoder objects. When the sands 

of corporate allegiance inevitably shift, and we are asked to convert our system to work with a new format called MegaCal, we can simply add a conditional into the CommsManager::getApptEncoder() method. This is the strategy we have used in the past, after all. Let’s build a new implementation of CommsManager that handles both BloggsCal and MegaCal formats:

// listing 09.17

class CommsManager{    const BLOGGS = 1;    const MEGA = 2;    private $mode;

    public function __construct(int $mode)    {        $this->mode = $mode;    }

    public function getApptEncoder(): ApptEncoder    {        switch ($this->mode) {            case (self::MEGA):                return new MegaApptEncoder();            default:                return new BloggsApptEncoder();        }    }}

// listing 09.18

$man = new CommsManager(CommsManager::MEGA);print (get_class($man->getApptEncoder())) . "\n";$man = new CommsManager(CommsManager::BLOGGS);print (get_class($man->getApptEncoder())) . "\n";

I use constant flags to define two modes in which the script might be run: MEGA and BLOGGS. I use 

a switch statement in the getApptEncoder() method to test the $mode property and instantiate the appropriate implementation of ApptEncoder.

189

Chapter 9 ■ GeneratinG ObjeCts

There is little wrong with this approach. Conditionals are sometimes considered examples of bad 

「code smells,」but object creation often requires a conditional at some point. You should be less sanguine if you see duplicate conditionals creeping into your code. The CommsManager class provides functionality for communicating calendar data. Imagine that the protocols you work with require you to provide header and footer data to delineate each appointment. I can extend the previous example to support a getHeaderText() method:

// listing 09.19

class CommsManager{    const BLOGGS = 1;    const MEGA = 2;    private $mode;

    public function __construct(int $mode)    {        $this->mode = $mode;    }

    public function getApptEncoder(): ApptEncoder    {        switch ($this->mode) {            case (self::MEGA):                return new MegaApptEncoder();            default:                return new BloggsApptEncoder();        }    }

    public function getHeaderText(): string    {        switch ($this->mode) {            case (self::MEGA):                return "MegaCal header\n";            default:                return "BloggsCal header\n";        }    }}

As you can see, the need to support header output has forced me to duplicate the protocol conditional test. This will become unwieldy as I add new protocols, especially if I also add a getFooterText() method.

So, let’s summarize the problem so far:

I do not know until runtime the kind of object I need to produce (BloggsApptEncoder or MegaApptEncoder)

I need to be able to add new product types with relative ease (SyncML support is just a new business deal away!)

Each product type is associated with a context that requires other customized operations (e.g., getHeaderText(), getFooterText())

•	

•	

•	

190

Chapter 9 ■ GeneratinG ObjeCts

Additionally, I am using conditional statements, and you have seen already that these are naturally 

replaceable by polymorphism. The Factory Method pattern enables you to use inheritance and polymorphism to encapsulate the creation of concrete products. In other words, you create a CommsManager subclass for each protocol, each one implementing the getApptEncoder() method.

ImplementationThe Factory Method pattern splits creator classes from the products they are designed to generate. The creator is a factory class that defines a method for generating a product object. If no default implementation is provided, it is left to creator child classes to perform the instantiation. Typically, each creator subclass instantiates a parallel product child class.

I can redesignate CommsManager as an abstract class. That way, I keep a flexible superclass and put all my 

protocol-specific code in the concrete subclasses. You can see this alteration in Figure 9-4.

Figure 9-4.  Concrete creator and product classes

Here’s some simplified code:

// listing 09.20

abstract class ApptEncoder{    abstract public function encode(): string;}

// listing 09.21

class BloggsApptEncoder extends ApptEncoder{    public function encode(): string

191

Chapter 9 ■ GeneratinG ObjeCts

    {        return "Appointment data encode in BloggsCal format\n";    }}

// listing 09.22

abstract class CommsManager{    abstract public function getHeaderText(): string;    abstract public function getApptEncoder(): ApptEncoder;    abstract public function getFooterText(): string;}

// listing 09.23

class BloggsCommsManager extends CommsManager{    public function getHeaderText(): string    {        return "BloggsCal header\n";    }

    public function getApptEncoder(): ApptEncoder    {        return new BloggsApptEncoder();    }

    public function getFooterText(): string    {        return "BloggsCal footer\n";    }}

// listing 09.24

$mgr = new BloggsCommsManager();print $mgr->getHeaderText();print $mgr->getApptEncoder()->encode();print $mgr->getFooterText();

BloggsCal headerAppointment data encode in BloggsCal formatBloggsCal footer

So, when I am required to implement MegaCal, supporting it is simply a matter of writing a new 

implementation for my abstract classes. Figure 9-5 shows the MegaCal classes.

192

Chapter 9 ■ GeneratinG ObjeCts

Figure 9-5.  Extending the design to support a new protocol

ConsequencesNotice that the creator classes mirror the product hierarchy. This is a common consequence of the Factory Method pattern and disliked by some as a special kind of code duplication. Another issue is the possibility that the pattern could encourage unnecessary subclassing. If your only reason for subclassing a creator is to deploy the Factory Method pattern, you may need to think again (that’s why I introduced the header and footer constraints to the example here).

I have focused only on appointments in my example. If I extend it somewhat to include to-do items and 

contacts, I face a new problem. I need a structure that will handle sets of related implementations at one time. The Factory Method pattern is often used with the Abstract Factory pattern, as you will see in the next section.

Abstract Factory Pattern

In large applications, you may need factories that produce related sets of classes. The Abstract Factory pattern addresses this problem.

193

Chapter 9 ■ GeneratinG ObjeCts

The ProblemLet’s look again at the organizer example. I manage encoding in two formats, BloggsCal and MegaCal. I can grow this structure horizontally by adding more encoding formats, but how can I grow vertically, adding encoders for different types of PIM objects? In fact, I have been working toward this pattern already.

In Figure 9-6, you can see the parallel families with which I will want to work. These are appointments 

(Appt), things to do (Ttd), and contacts (Contact).

Figure 9-6.  Three product families

The BloggsCal classes are unrelated to one another by inheritance (although they could implement 

a common interface), but they are functionally parallel. If the system is currently working with BloggsTtdEncoder, it should also be working with BloggsContactEncoder.

To see how I enforce this, you can begin with the interface, as I did with the Factory Method pattern (see 

Figure 9-7).

194

Chapter 9 ■ GeneratinG ObjeCts

Figure 9-7.  An abstract creator and its abstract products

ImplementationThe abstract CommsManager class defines the interface for generating each of the three products (ApptEncoder, TtdEncoder, and ContactEncoder). You need to implement a concrete creator in order to actually generate the concrete products for a particular family. I illustrate that for the BloggsCal format in Figure 9-8.

Figure 9-8.  Adding a concrete creator and some concrete products

195

Chapter 9 ■ GeneratinG ObjeCts

Here is a code version of CommsManager and BloggsCommsManager:

// listing 09.25

abstract class CommsManager{    abstract public function getHeaderText(): string;    abstract public function getApptEncoder(): ApptEncoder;    abstract public function getTtdEncoder(): TtdEncoder;    abstract public function getContactEncoder(): ContactEncoder;    abstract public function getFooterText(): string;}

// listing 09.26

class BloggsCommsManager extends CommsManager{

    public function getHeaderText(): string    {        return "BloggsCal header\n";    }

    public function getApptEncoder(): ApptEncoder    {        return new BloggsApptEncoder();    }

    public function getTtdEncoder(): TtdEncoder    {        return new BloggsTtdEncoder();    }

    public function getContactEncoder(): ContactEncoder    {        return new BloggsContactEncoder();    }

    public function getFooterText(): string    {        return "BloggsCal footer\n";    }}

Notice that I use the Factory Method pattern in this example. getContactEncoder() is abstract in 

CommsManager and implemented in BloggsCommsManager. Design patterns tend to work together in this way, one pattern creating the context that lends itself to another. In Figure 9-9, I add support for the MegaCal format.

196

Chapter 9 ■ GeneratinG ObjeCts

Figure 9-9.  Adding concrete creators and some concrete products

ConsequencesSo, let’s look at what this pattern buys:

•	

•	

•	

First, I decouple my system from the details of implementation. I can add or remove any number of encoding formats in my example without causing a knock-on effect.

I enforce the grouping of functionally related elements of my system. So, by using BloggsCommsManager, I am guaranteed that I will work only with BloggsCal-related classes.

Adding new products can be a pain. Not only do I have to create concrete implementations of the new product, but I also have to amend the abstract creator and every one of its concrete implementers in order to support it.

Many implementations of the Abstract Factory pattern use the Factory Method pattern. This may be 

because most examples are written in Java or C++. PHP, however, does not have to enforce a return type for a method (though it now can), which affords us some flexibility that we might leverage.

Rather than create separate methods for each Factory Method, you can create a single make() method 

that uses a flag argument to determine which object to return:

// listing 09.27

interface Encoder{    public function encode(): string;}

197

Chapter 9 ■ GeneratinG ObjeCts

// listing 09.28

abstract class CommsManager{    const APPT    = 1;    const TTD     = 2;    const CONTACT = 3;    abstract public function getHeaderText(): string;    abstract public function make(int $flag_int): Encoder;    abstract public function getFooterText(): string;}

// listing 09.29

class BloggsCommsManager extends CommsManager{    public function getHeaderText(): string    {        return "BloggsCal header\n";    }

    public function make(int $flag_int): Encoder    {        switch ($flag_int) {            case self::APPT:                return new BloggsApptEncoder();            case self::CONTACT:                return new BloggsContactEncoder();            case self::TTD:                return new BloggsTtdEncoder();        }    }

    public function getFooterText(): string    {        return "BloggsCal footer\n";    }}

As you can see, I have made the class interface more compact. I’ve done this at a considerable cost, 

though. In using a factory method, I define a clear interface and force all concrete factory objects to honor it. In using a single make() method, I must remember to support all product objects in all the concrete creators. I also introduce parallel conditionals, as each concrete creator must implement the same flag tests. A client class cannot be certain that concrete creators generate all the products because the internals of make() are a matter of choice in each case.

On the other hand, I can build more flexible creators. The base creator class can provide a make() 

method that guarantees a default implementation of each product family. Concrete children could then modify this behavior selectively. It would be up to implementing creator classes to call the default make() method after providing their own implementation.

You will see another variation on the Abstract Factory pattern in the next section.

198

Chapter 9 ■ GeneratinG ObjeCts

Prototype

The emergence of parallel inheritance hierarchies can be a problem with the Factory Method pattern. This is a kind of coupling that makes some programmers uncomfortable. Every time you add a product family, you are forced to create an associated concrete creator (the BloggsCal encoders are matched by BloggsCommsManager, for example). In a system that grows fast enough to encompass many products, maintaining this kind of relationship can quickly become tiresome.

One way of avoiding this dependency is to use PHP’s clone keyword to duplicate existing concrete 

products. The concrete product classes themselves then become the basis of their own generation. This is the Prototype pattern. It enables you to replace inheritance with composition. This in turn promotes runtime flexibility and reduces the number of classes you must create.

The ProblemImagine a Civilization-style web game in which units operate on a grid of tiles. Each tile can represent sea, plains, or forests. The terrain type constrains the movement and combat abilities of units occupying the tile. You might have a TerrainFactory object that serves up Sea, Forest, and Plains objects. You decide that you will allow the user to choose among radically different environments, so the Sea object is an abstract superclass implemented by MarsSea and EarthSea. Forest and Plains objects are similarly implemented. The forces here lend themselves to the Abstract Factory pattern. You have distinct product hierarchies (Sea, Plains, Forests), with strong family relationships cutting across inheritance (Earth, Mars). Figure 9-10 presents a class diagram that shows how you might deploy the Abstract Factory and Factory Method patterns to work with these products.

Figure 9-10.  Handling terrains with the Abstract Factory method

199

Chapter 9 ■ GeneratinG ObjeCts

As you can see, I rely on inheritance to group the terrain family for the products that a factory will 

generate. This is a workable solution, but it requires a large inheritance hierarchy, and it is relatively inflexible. When you do not want parallel inheritance hierarchies, and when you need to maximize runtime flexibility, the Prototype pattern can be used in a powerful variation on the Abstract Factory pattern.

ImplementationWhen you work with the Abstract Factory/Factory Method patterns, you must decide, at some point, which concrete creator you wish to use, probably by checking some kind of preference flag. As you must do this anyway, why not simply create a factory class that stores concrete products, and then populate this during initialization? You can cut down on a couple of classes this way and, as you shall see, take advantage of other benefits. Here’s some simple code that uses the Prototype pattern in a factory:

// listing 09.30

class Sea{}

class EarthSea extends Sea{}

class MarsSea extends Sea{}

class Plains{}

class EarthPlains extends Plains{}

class MarsPlains extends Plains{}

class Forest{}

class EarthForest extends Forest{}

class MarsForest extends Forest{}

200

Chapter 9 ■ GeneratinG ObjeCts

// listing 09.31

class TerrainFactory{    private $sea;    private $forest;    private $plains;

    public function __construct(Sea $sea, Plains $plains, Forest $forest)    {        $this->sea = $sea;        $this->plains = $plains;        $this->forest = $forest;    }

    public function getSea(): Sea    {        return clone $this->sea;    }

    public function getPlains(): Plains    {        return clone $this->plains;    }

    public function getForest(): Forest    {        return clone $this->forest;    }}

// listing 09.32

$factory = new TerrainFactory(    new EarthSea(),    new EarthPlains(),    new EarthForest());print_r($factory->getSea());print_r($factory->getPlains());print_r($factory->getForest());

popp\ch09\batch11\EarthSea Object()popp\ch09\batch11\EarthPlains Object()popp\ch09\batch11\EarthForest Object()

201

Chapter 9 ■ GeneratinG ObjeCts

As you can see, I load up a concrete TerrainFactory with instances of product objects. When a client 

calls getSea(), I return a clone of the Sea object that I cached during initialization. This structure buys me additional flexibility. Want to play a game on a new planet with Earth-like seas and forests, but Mars-like plains? No need to write a new creator class—you can simply change the mix of classes you add to TerrainFactory:

$factory = new TerrainFactory(    new EarthSea(),    new MarsPlains(),    new EarthForest());

So the Prototype pattern allows you to take advantage of the flexibility afforded by composition. We get more than that, though. Because you are storing and cloning objects at runtime, you reproduce object state when you generate new products. Imagine that Sea objects have a $navigability property. The property influences the amount of movement energy a sea tile saps from a vessel and can be set to adjust the difficulty level of a game:

// listing 09.33

class Sea{    private $navigability = 0;

    public function __construct(int $navigability)    {        $this->navigability = $navigability;    }}

Now when I initialize the TerrainFactory object, I can add a Sea object with a navigability modifier. 

This will then hold true for all Sea objects served by TerrainFactory:

// listing 09.34

$factory = new TerrainFactory(    new EarthSea(-1),    new EarthPlains(),    new EarthForest());

This flexibility is also apparent when the object you wish to generate is composed of other objects.

 ■ Note  i covered object cloning in Chapter 4. the clone keyword generates a shallow copy of any object to which it is applied. this means that the product object will have the same properties as the source. if any of the source’s properties are objects, then these will not be copied into the product. instead, the product will reference the same object properties. it is up to you to change this default and to customize object copying in any other way, by implementing a __clone() method. this is called automatically when the clone keyword is used.

202

Perhaps all Sea objects can contain Resource objects (FishResource, OilResource, etc.). According to a preference flag, we might give all Sea objects a FishResource by default. Remember that if your products reference other objects, you should implement a __clone() method to ensure that you make a deep copy:

Chapter 9 ■ GeneratinG ObjeCts

class Contained{}

class Container{    public $contained;

    function __construct()    {        $this->contained = new Contained();    }

    function __clone()   {        // Ensure that cloned object holds a        // clone of self::$contained and not        // a reference to it        $this->contained = clone $this->contained;    }}

Pushing to the Edge: Service Locator

I promised that this chapter would deal with the logic of object creation, doing away with the sneaky buck-passing of many object-oriented examples. Yet some patterns here have slyly dodged the decision-making part of object creation, if not the creation itself.

The Singleton pattern is not guilty. The logic for object creation is built-in and unambiguous. The 

Abstract Factory pattern groups the creation of product families into distinct concrete creators. How do we decide which concrete creator to use, though? The Prototype pattern presents us with a similar problem. Both these patterns handle the creation of objects, but they defer the decision as to which object or group of objects should be created.

The particular concrete creator that a system chooses is often decided according to the value of a 

configuration switch of some kind. This could be located in a database, a configuration file, or a server file (such as Apache’s directory-level configuration file, usually called .htaccess), or it could even be hard-coded as a PHP variable or property. Because PHP applications must be reconfigured for every request, you need script initialization to be as painless as possible. For this reason, I often opt to hard-code configuration flags in PHP code. This can be done by hand or by writing a script that autogenerates a class file. Here’s a crude class that includes a flag for calendar protocol types:

// listing 09.35class Settings{    static $COMMSTYPE = 'Bloggs';}

203

Chapter 9 ■ GeneratinG ObjeCts

Now that I have a flag (however inelegant), I can create a class that uses it to decide which CommsManager 

to serve on request. It is quite common to see a Singleton used in conjunction with the Abstract Factory pattern, so let’s do that:

// listing 09.36

class AppConfig{    private static $instance;    private $commsManager;

    private function __construct()    {        // will run once only        $this->init();    }

    private function init()    {        switch (Settings::$COMMSTYPE) {            case 'Mega':                $this->commsManager = new MegaCommsManager();                break;            default:                $this->commsManager = new BloggsCommsManager();        }    }

    public static function getInstance(): AppConfig    {        if (empty(self::$instance)) {            self::$instance = new self();        }        return self::$instance;    }

    public function getCommsManager(): CommsManager    {        return $this->commsManager;    }}

The AppConfig class is a standard Singleton. For that reason, I can get an AppConfig instance anywhere 

in the system, and I will always get the same one. The init() method is invoked by the class’s constructor and is therefore only run once in a process. It tests the Settings::$COMMSTYPE property, instantiating a concrete CommsManager object according to its value. Now my script can get a CommsManager object and work with it without ever knowing about its concrete implementations or the concrete classes it generates:

$commsMgr = AppConfig::getInstance()->getCommsManager();$commsMgr->getApptEncoder()->encode();

204

Chapter 9 ■ GeneratinG ObjeCts

Because AppConfig manages the work of finding and creating components for us, it is an instance of what’s known as the Service Locator pattern. It’s neat (and we’ll see it again in more detail in Chapter 12), but it does introduce a more benign dependency than direct instantiation. Any classes using its service must explicitly invoke this monolith, binding them to the wider system. For this reason, some prefer another approach.

Splendid Isolation: Dependency Injection

In the previous section, I used a flag and a conditional statement within a factory to determine which of two CommsManager classes to serve up. The solution was not as flexible as it might have been. The classes on offer were hard-coded within a single locator, with a choice of two components built-in to a conditional. That inflexibility was a facet of my demonstration code, though, rather than a problem with Service Locator, per se. I could have used any number of strategies to locate, instantiate, and return objects on behalf of client code. The real reason Service Locator is often treated with suspicion, however, is the fact that a component must explicitly invoke the locator. This feels a little, well, global. And object-oriented developers are rightly suspicious of all things global.

The ProblemWhenever you use the new operator, you close down the possibility of polymorphism within that scope. Imagine a method that deploys a hard-coded BloggsApptEncoder object, for example:

// listing 09.37

class AppointmentMaker{    public function makeAppointment()    {        $encoder = new BloggsApptEncoder();        return $encoder->encode();    }}

This might work for our initial needs, but it will not allow any other ApptEncoder implementation to be switched in at runtime. That limits the ways in which the class can be used, and it makes the class harder to test. Much of this chapter addresses precisely this kind of inflexibility. But, as I pointed out in the previous section, I have skated over the fact that, even if we use the Prototype or Abstract Factory patterns, instantiation has to happen somewhere. Here again is a fragment of code that creates a Prototype object:

// listing 09.32

$factory = new TerrainFactory(    new EarthSea(),    new EarthPlains(),    new EarthForest());

205

Chapter 9 ■ GeneratinG ObjeCts

The Prototype TerrainFactory class called here is a step in the right direction—it demands generic 

types: Sea, Plains, and Forest. The class leaves it up to the client code to determine which implementations should be provided. But how is this done?

ImplementationMuch of our code calls out to factories. As we have seen, this model is known as the Service Locator pattern. A method delegates responsibility to a provider which it trusts to find and serve up an instance of the desired type. The Prototype example inverts this; it simply expects the instantiating code to provide implementations at call time. There’s no magic here—it’s simply a matter of requiring types in a constructor’s signature, instead of creating them directly within the method. A variation on this is to provide setter methods, so that clients can pass in objects before invoking a method that uses them.

So let’s fix up AppointmentMaker in this way:

// listing 09.38

class AppointmentMaker2{    private $encoder;

    public function __construct(ApptEncoder $encoder) {        $this->encoder = $encoder;    }

    public function makeAppointment()    {        return $this->encoder->encode();    }}

AppointmentMaker2 has given up control—it no longer creates the BloggsApptEncoder, and we have 

gained flexibility. What about the logic for the actual creation of objects, though? Where do the dreaded new statements live? We need an assembler component to take on the job. Typically, this approach uses a configuration file to figure out which implementations should be instantiated. There are tools to help us with this, but this book is all about doing it ourselves, so let’s build a very naive implementation. I’ll start with a crude XML format which describes the relationships between classes in our system and the concrete types that should be passed to their constructors:

<objects>    <class name="\popp\ch09\batch11\TerrainFactory">        <arg num="0" inst="\popp\ch09\batch11\EarthSea" />        <arg num="1" inst="\popp\ch09\batch11\MarsPlains" />        <arg num="2" inst="\popp\ch09\batch11\EarthForest" />    </class>

    <class name="\popp\ch09\batch14\AppointmentMaker2">        <arg num="0" inst="\popp\ch09\batch06\BloggsApptEncoder" />    </class></objects>

206

I’ve described two classes from this chapter: TerrainFactory and AppointmentMaker2. I want 

TerrainFactory to be instantiated with an EarthSea object, a MarsPlains object, and an EarthForest object. I would also like AppointmentMaker2 to be passed a BloggsApptEncoder object.

Here’s a very simple assembler class that reads this configuration data and instantiates objects on 

Chapter 9 ■ GeneratinG ObjeCts

demand:

// listing 09.39class ObjectAssembler{    private $components = [];

    public function __construct(string $conf)    {        $this->configure($conf);    }

    private function configure(string $conf)    {        $data = simplexml:load_file($conf);        foreach ($data->class as $class) {            $args = [];            $name = (string)$class['name'];            foreach ($class->arg as $arg) {                $argclass = (string)$arg['inst'];                $args[(int)$arg['num']] = $argclass;            }            ksort($args);            $this->components[$name] = function () use ($name, $args) {                $expandedargs = [];                foreach ($args as $arg) {                    $expandedargs[] = new $arg();                }                $rclass = new \ReflectionClass($name);                return $rclass->newInstanceArgs($expandedargs);            };        }    }

    public function getComponent(string $class)    {        if (! isset($this->components[$class])) {            throw new \Exception("unknown component '$class'");        }        $ret = $this->components[$class]();        return $ret;    }}

This is pretty crude, and it is a little dense at first reading, so let’s work through it briefly. Most of the 

real action takes place in configure(). The method accepts a path which is passed on from the constructor. It uses the simplexml extension to parse the configuration XML. In a real project, of course, we’d add more error handling here and throughout. For now, I’m pretty trusting of the XML I’m parsing. For every <class> 

element, I extract the fully qualified class name and store it in the $name variable. Then I acquire all the <arg> subelements, all of which have their own class names. I store the arguments in an array named $args, ordered according to the XML num argument. I pack all of this in an anonymous function which I store in the $components property. This function, which instantiates a requested class and all its required objects, is only invoked when getComponent() is called with the correct class name. In this way the ObjectAssembler can maintain a pretty small footprint. Note the use of a closure here. The anonymous function has access to the $name and $args variables declared in the scope of its creation, thanks to the use keyword.

Of course, this is really toy code. In addition to improved error checking, a robust implementation would need to handle the possibility that the objects to be injected into a component might themselves require arguments. We might also want to address issues around caching. For example, should a contained object be instantiated for every call, or only once?

 if you are considering building a Dependency injection assembler/container, you should look at a 

 ■ Note couple of options: pimple (notwithstanding its unpleasant name) and symfony Di. You can find out more about pimple at http://pimple.sensiolabs.org/; you can learn more about the symfony Di component at http://symfony.com/doc/current/components/dependency_injection/introduction.html.

Nevertheless, we can now maintain the flexibility of our components and handle instantiation 

dynamically. Let’s try out the ObjectAssembler:

// listing 09.40$assembler = new ObjectAssembler("src/ch09/batch14/objects.xml");$apptmaker = $assembler->getComponent("\\popp\\ch09\\batch14\\AppointmentMaker2");$out = $apptmaker->makeAppointment();print $out;

Once we have an ObjectAssembler, object acquisition takes up a single statement. The 

AppointmentMaker2 class is free of its previous hard-coded dependency on an ApptEncoder instance. A developer can now use the configuration file to control what classes are used at runtime, as well as to test AppointmentMaker2 in isolation from the wider system.

ConsequencesSo, now we’ve seen two options for object creation. The AppConfig class was an instance of Service Locator (i.e., a class with the ability to find components or services on behalf of its client). Using dependency injection certainly makes for more elegant client code. The AppointmentMaker2 class is blissfully unaware of strategies for object creation. It simply does its job. This is the ideal for a class, of course. We want to design classes that can focus on their responsibilities, isolated as far as possible from the wider system. However, this purity does come at a price. The object assembler component hides a lot of magic. We must treat it as a black box and trust it to conjure up objects on our behalf. This is fine, so long as the magic works. Unexpected behavior can be hard to debug.

The Service Locator pattern, on the other hand, is simpler, though it embeds your components into a wider system. It is not the case that, used well, a Service Locator makes testing harder. Nor does it make a system inflexible. A Service Locator can be configured to serve up arbitrary components for testing or according to configuration. But a hard-coded call to a service locator makes a component dependent upon it. Because the call is made from within the body of a method, the relationship between the client and the target component (which is provided by the Service Locator) is also somewhat obscured. This relationship is made explicit in the Dependency Injection example because it is declared in the constructor method’s signature.

So, which approach should we choose? To some extent it’s a matter of preference. For my own part, I tend to prefer to start with the simplest solution, and then to refactor to greater complexity, if needed. For that reason, I usually opt for Service Locator. I can create a Registry class in a few lines of code, and increase its flexibility according to the requirements. My components are a little more knowing than I would like, but since I rarely move classes from one system to another, I have not suffered too much from the embedding effect. When I have moved a system-based class into a standalone library, I have not found it particularly hard to refactor the Service Locator dependency away.

Dependency Injection offers purity, but it requires another kind of embedding. You must buy in to the 

magic of the assembler. If you are already working within a framework which offers this functionality, there is no reason not to avail yourself of it. The Symfony  DependencyInjection component, for example, provides a hybrid solution of Service Locator (known as the「service container」) and Dependency Injection. The service container manages the instantiation of objects according to the configuration (or code, if you prefer) and provides a simple interface for clients to obtain those objects. The service container even allows the use of factories for object creation. On the other hand, if you are rolling your own, or using components from various frameworks, you may wish to keep things simple at the cost of some elegance.

## Summary

This chapter covered some of the tricks that you can use to generate objects. I began by examining the Singleton pattern, which provides global access to a single instance. Next, I looked at the Factory Method pattern, which applies the principle of polymorphism to object generation. And I combined Factory Method with the Abstract Factory pattern to generate creator classes that instantiate sets of related objects. I also looked at the Prototype pattern and saw how object cloning can allow composition to be used in object generation. Finally, I examined two strategies for object creation: Service Locator and Dependency Injection.

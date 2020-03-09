Advanced Features

You have already seen how class type hinting and access control give you more control over a class’s interface. In this chapter, I will delve deeper into PHP’s object-oriented features.

This chapter will cover several subjects:

•	

Static methods and properties: Accessing data and functionality through classes rather than objects

Abstract classes and interfaces: Separating design from implementation

Traits: Sharing implementation between class hierarchies

Error handling: Introducing exceptions

Final classes and methods: Limiting inheritance

•	•	•	•	•	•	 Destructor methods: Cleaning up after your objects•	•	•	

Interceptor methods: Automating delegation

Cloning objects: Making object copies

Resolving objects to strings: Creating a summary method

Callbacks: Adding functionality to components with anonymous functions and classes

Static Methods and Properties

All of the examples in the previous chapter worked with objects. I characterized classes as templates from which objects are produced, and objects as active instances of classes—the things whose methods you invoke and whose properties you access. I implied that, in object-oriented programming, the real work is done by instances of classes. Classes, after all, are merely templates for objects.

In fact, it is not that simple. You can access both methods and properties in the context of a class rather than that of an object. Such methods and properties are「static」and must be declared as such by using the static keyword:

// listing 04.01class StaticExample{    static public $aNum = 0;    public static function sayHello()    {

© Matt Zandstra 2016 M. Zandstra, PHP Objects, Patterns, and Practice, DOI 10.1007/978-1-4842-1996-6_4

47

Chapter 4 ■ advanCed Features

        print "hello";    }}

Static methods are functions with class scope. They cannot themselves access any normal properties in the class because these would belong to an object; however, they can access static properties. If you change a static property, all instances of that class are able to access the new value.

Because you access a static element via a class and not an instance, you do not need a variable that 

references an object. Instead, you use the class name in conjunction with ::, as in this example:

print StaticExample::$aNum;StaticExample::sayHello();

This syntax should be familiar from the previous chapter. I used :: in conjunction with parent to access 

an overridden method. Now, as then, I am accessing class rather than object data. Class code can use the parent keyword to access a superclass without using its class name. To access a static method or property from within the same class (rather than from a child), I would use the self keyword. self is to classes what the $this pseudo-variable is to objects. So from outside the StaticExample class, I access the $aNum property using its class name:

StaticExample::$aNum;

From within the StaticExample class, I can use the self keyword:

// listing 04.02class StaticExample{    static public $aNum = 0;    public static function sayHello()    {        self::$aNum++;        print "hello (".self::$aNum.")\n";    }}

 Making a method call using parent is the only circumstance in which you should use a static 

 ■ Note reference to a nonstatic method.

unless you are accessing an overridden method, you should only ever use :: to access a method or property that has been explicitly declared static.

In documentation, however, you will often see static syntax used to refer to a method or property. this does not mean that the item in question is necessarily static, just that it belongs to a certain class. the write() method of the ShopProductWriter class might be referred to as ShopProductWriter::write(), for example, even though the write() method is not static. You will see this syntax here when that level of specificity is appropriate.

48

Chapter 4 ■ advanCed Features

By definition, static methods and properties are invoked on classes and not objects. For this reason, they are often referred to as class variables and properties. As a consequence of this class orientation, you cannot use the $this pseudo-variable inside a static method.

So, why would you use a static method or property? Static elements have a number of characteristics that can be useful. First, they are available from anywhere in your script (assuming that you have access to the class). This means you can access functionality without needing to pass an instance of the class from object to object or, worse, storing an instance in a global variable. Second, a static property is available to every instance of a class, so you can set values that you want to be available to all members of a type. Finally, the fact that you don’t need an instance to access a static property or method can save you from instantiating an object purely to get at a simple function.

To illustrate this, I will build a static method for the ShopProduct class that automates the instantiation 

of ShopProduct objects. Using SQLite, I might define a products table like this:

CREATE TABLE products (                            id INTEGER PRIMARY KEY AUTOINCREMENT,                            type TEXT,                            firstname TEXT,                            mainname TEXT,                            title TEXT,                            price float,                            numpages int,                            playlength int,                            discount int )

Now I want to build a getInstance() method that accepts a row ID and PDO object, uses them to 

acquire a database row, and then returns a ShopProduct object. I can add these methods to the ShopProduct class I created in the previous chapter. As you probably know, PDO stands for PHP Data Object. The PDO class provides a common interface to different database applications:

// listing 04.03

// ShopProduct class...

    private $id = 0;    // ...

    public function setID(int $id)    {        $this->id = $id;    }    // ...

    public static function getInstance(int $id, \PDO $pdo): ShopProduct    {        $stmt = $pdo->prepare("select * from products where id=?");        $result = $stmt->execute([$id]);        $row = $stmt->fetch();        if (empty($row)) {            return null;        }

49

Chapter 4 ■ advanCed Features

        if ($row['type'] == "book") {            $product = new BookProduct(                $row['title'],                $row['firstname'],                $row['mainname'],                (float) $row['price'],                (int) $row['numpages']            );        } elseif ($row['type'] == "cd") {            $product = new CdProduct(                $row['title'],                $row['firstname'],                $row['mainname'],                (float) $row['price'],                (int) $row['playlength']            );        } else {            $firstname = (is_null($row['firstname'])) ? "" : $row['firstname'];            $product = new ShopProduct(                $row['title'],                $firstname,                $row['mainname'],                (float) $row['price']            );        }        $product->setId((int) $row['id']);        $product->setDiscount((int) $row['discount']);        return $product;    }

As you can see, the getInstance() method returns a ShopProduct object and, based on a type flag, is 

smart enough to work out the precise specialization it should instantiate. I have omitted any error handling to keep the example compact. In a real-world version of this, for example, I would not be so trusting as to assume that the provided PDO object was initialized to talk to the correct database. In fact, I probably wrap the PDO with a class that would guarantee this behavior. You can read more about object-oriented coding and databases in Chapter 13.

This method is more useful in a class context than an object context. It lets you convert raw data from the database into an object easily, without requiring that you have a ShopProduct object to start with. The method does not use any instance properties or methods, so there is no reason why it should not be declared static. Given a valid PDO object, I can invoke the method from anywhere in an application:

$dsn = "sqlite:/".__DIR__."/products.db";$pdo = new \PDO($dsn, null, null);$pdo->setAttribute(\PDO::ATTR_ERRMODE, \PDO::ERRMODE_EXCEPTION);$obj = ShopProduct::getInstance(1, $pdo);

Methods like this act as「factories」in that they take raw materials (such as row data or configuration information) and use them to produce objects. The term factory is applied to code designed to generate object instances. You will encounter factory examples again in future chapters.

In some ways, of course, this example poses as many problems as it solves. Although I make the ShopProduct::getInstance() method accessible from anywhere in a system without the need for an ShopProduct instance, I also demand that client code provides a PDO object. Where is this to be found? 

50

Chapter 4 ■ advanCed Features

And is it really good practice for a parent class to have such intimate knowledge of its children? (Hint: no, it is not.) Problems of this kind—where to acquire key objects and values and how much classes should know about one another—are very common in object-oriented programming. I examine various approaches to object generation in Chapter 9.

Constant Properties

Some properties should not be changed. The Answer to Life, the Universe, and Everything is 42, and you want it to stay that way. Error and status flags will often be hard-coded into your classes. Although they should be publicly and statically available, client code should not be able to change them.

PHP allows you to define constant properties within a class. Like global constants, class constants 

cannot be changed once they are set. A constant property is declared with the const keyword. Constants are not prefixed with a dollar sign like regular properties. By convention, they are often named using only uppercase characters:

// listing 04.04class ShopProduct{    const AVAILABLE      = 0;    const OUT_OF_STOCK   = 1;    // ...

Constant properties can contain only primitive values. You cannot assign an object to a constant. Like 

static properties, constant properties are accessed through the class and not an instance. Just as you define a constant without a dollar sign, no leading symbol is required when you refer to one:

print ShopProduct::AVAILABLE;

Attempting to set a value on a constant once it has been declared will cause a parse error.You should use constants when your property needs to be available across all instances of a class, as 

well as when the property value needs to be fixed and unchanging.

Abstract Classes

An abstract class cannot be instantiated. Instead it defines (and, optionally, partially implements) the interface for any class that might extend it.

You define an abstract class with the abstract keyword. Here I redefine the ShopProductWriter class I 

created in the previous chapter, this time as an abstract class:

// listing 04.05abstract class ShopProductWriter{    protected $products = [];

    public function addProduct(ShopProduct $shopProduct)    {        $this->products[] = $shopProduct;    }}

51

Chapter 4 ■ advanCed Features

You can create methods and properties as normal, but any attempt to instantiate an abstract object in 

this way will cause an error:

$writer = new ShopProductWriter();

You can see the error in this output:

Error: Cannot instantiate abstract class popp\ch04\batch03\ShopProductWriter

In most cases, an abstract class will contain at least one abstract method. These are declared, once 

again, with the abstract keyword. An abstract method cannot have an implementation. You declare it in the normal way, but end the declaration with a semicolon rather than a method body. Here I add an abstract write() method to the ShopProductWriter class:

abstract class ShopProductWriter{    protected $products = [];

    public function addProduct(ShopProduct $shopProduct)    {        $this->products[]=$shopProduct;    }

    abstract public function write();}

In creating an abstract method, you ensure that an implementation will be available in all concrete 

child classes, but you leave the details of that implementation undefined.

Assume I were to create a class derived from ShopProductWriter that does not implement the write() 

method, as in this example:

class ErroredWriter extends ShopProductWriter{}

I would face the following error:

PHP Fatal error:  Class ErroredWriter contains 1 abstract method andmust therefore be declared abstract or implement the remaining methods (ShopProductWriter::write) in...

So any class that extends an abstract class must implement all abstract methods or itself be declared 

abstract. An extending class is responsible for more than simply implementing an abstract method. In doing so, it must reproduce the method signature. This means that the access control of the implementing method cannot be stricter than that of the abstract method. The implementing method should also require the same number of arguments as the abstract method, reproducing any class type hinting.

52

Chapter 4 ■ advanCed Features

Here are two implementations of ShopProductWriter:

// listing 04.06class XmlProductWriter extends ShopProductWriter{

    public function write()    {        $writer = new \XMLWriter();        $writer->openMemory();        $writer->startDocument('1.0', 'UTF-8');        $writer->startElement("products");        foreach ($this->products as $shopProduct) {            $writer->startElement("product");            $writer->writeAttribute("title", $shopProduct->getTitle());            $writer->startElement("summary");            $writer->text($shopProduct->getSummaryLine());            $writer->endElement(); // summary            $writer->endElement(); // product        }        $writer->endElement(); // products        $writer->endDocument();        print $writer->flush();    }}

// listing 04.07class TextProductWriter extends ShopProductWriter{    public function write()    {        $str = "PRODUCTS:\n";        foreach ($this->products as $shopProduct) {            $str .= $shopProduct->getSummaryLine()."\n";        }        print $str;    }}

I create two classes, each with its own implementation of the write() method. The first outputs XML 

and the second outputs text. A method that requires a ShopProductWriter object will not know which of these two classes it is receiving, but it can be absolutely certain that a write() method is implemented. Note that I don’t test the type of $products before treating it as an array. This is because this property is initialized as an empty array in the ShopProductWriter.

Interfaces

Although abstract classes let you provide some measure of implementation, interfaces are pure templates. An interface can only define functionality; it can never implement it. An interface is declared with the interface keyword. It can contain properties and method declarations but not method bodies.

53

Chapter 4 ■ advanCed Features

Here’s an interface:

// listing 04.08interface Chargeable{    public function getPrice(): float;}

As you can see, an interface looks very much like a class. Any class that incorporates this interface 

commits to implementing all the methods it defines, or it must be declared abstract.

A class can implement an interface using the implements keyword in its declaration. Once you have 

done this, the process of implementing an interface is the same as extending an abstract class that contains only abstract methods. Now I will make the ShopProduct class implement Chargeable:

// listing 04.09class ShopProduct implements Chargeable{    // ...    protected $price;    // ...

    public function getPrice(): float    {        return $this->price;    }    // ...}

ShopProduct already had a getPrice() method, so why might it be useful to implement the Chargeable interface? Once again, the answer has to do with types. An implementing class takes on the type of the class it extends and the interface that it implements.

This means that the CdProduct class belongs to the following:

CdProductShopProductChargeable

This can be exploited by client code. To know an object’s type is to know its capabilities. Consider this 

method:

    public function cdInfo(CdProduct $prod)    {        // ...    }

The method knows that the $prod object has a getPlayLength() method in addition to all the methods 

defined in the ShopProduct class and Chargeable interface.

Passed the same object, the method knows that $prod supports all the methods in ShopProduct:

    public function addProduct(ShopProduct $prod)    {

54

Chapter 4 ■ advanCed Features

         // ...    }

Without further testing, however, the method will know nothing of the getPlayLength() method.Once again, passed the same CdProduct object, the method knows nothing at all of the ShopProduct or 

CdProduct types:

    public function addChargeableItem(Chargeable $item)    {        //...    }

However, this method is only concerned with whether the $item argument contains a getPrice() method.Because any class can implement an interface (in fact, a class can implement any number of interfaces), 

interfaces effectively join types that are otherwise unrelated. I might define an entirely new class that implements Chargeable:

class Shipping implements Chargeable{    public function getPrice(): float    {        //...    }}

I can pass a Shipping object to the addChargeableItem method just as I can pass it a ShopProduct object.The important thing to a client working with a Chargeable object is that it can call a getPrice() 

method. Any other available methods are associated with other types, whether through the object’s own class, a superclass, or another interface. These are irrelevant to the client.

A class can both extend a superclass and implement any number of interfaces. The extends clause 

should precede the implements clause:

class Consultancy extends TimedService implements Bookable, Chargeable{    // ...}

Notice that the Consultancy class implements more than one interface. Multiple interfaces follow the 

implements keyword in a comma-separated list.

PHP only supports inheritance from a single parent, so the extends keyword can precede a single class 

name only.

Traits

As we have seen, interfaces help you manage the fact that, like Java, PHP does not support multiple inheritance. In other words, a class in PHP can only extend a single parent. However, you can make a class promise to implement as many interfaces as you like; for each interface it implements, the class takes on the corresponding type.

So interfaces provide types without implementation. But what if you want to share an implementation 

across inheritance hierarchies? PHP 5.4 introduced traits, and these let you do just that.

55

Chapter 4 ■ advanCed Features

A trait is a class-like structure that cannot itself be instantiated but can be incorporated into classes. Any methods defined in a trait become available as part of any class that uses it. A trait changes the structure of a class, but doesn’t change its type. Think of traits as includes for classes.

Let’s look at why a trait might be useful.

A Problem for Traits to SolveHere is a version of the ShopProduct class with a calculateTax() method:

// listing 04.10

class ShopProduct{    private $taxrate = 17;

// ...

    public function calculateTax(float $price): float    {        return (($this->taxrate / 100) * $price);    }}

// listing 04.11$p = new ShopProduct("Fine Soap", "", "Bob's Bathroom", 1.33);print $p->calculateTax(100) . "\n";

The calculateTax() method accepts a $price argument and calculates a sales tax amount based on 

the private $taxrate property.

Of course, a subclass gains access to calculateTax(). But what about entirely different class 

hierarchies? Imagine a class named UtilityService, which inherits from another class, Service. If UtilityService needs to use an identical routine, I might find myself duplicating calculateTax() in its entirety:

abstract class Service{    // service oriented stuff}

class UtilityService extends Service{    private $taxrate = 17;

    function calculateTax(float $price): float    {        return ( ( $this->taxrate/100 ) * $price );    }}

$u = new UtilityService();print $u->calculateTax(100)."\n";

56

Chapter 4 ■ advanCed Features

Defining and Using a TraitOne of the core object-oriented design goals I will cover in this book is the removal of duplication. As you will see in Chapter 11, one solution to this kind of duplication is to factor it out into a reusable strategy class. Traits provide another approach—less elegant, perhaps, but certainly effective.

Here I declare a single trait that defines a calculateTax() method, and then I include it in both 

ShopProduct and UtilityService:

// listing 04.12trait PriceUtilities{    private $taxrate = 17;

    public function calculateTax(float $price): float    {        return (($this->taxrate / 100) * $price);    }

    // other utilities}

// listing 04.13class ShopProduct{    use PriceUtilities;}

// listing 04.14abstract class Service{    // service oriented stuff}

// listing 04.15class UtilityService extends Service{    use PriceUtilities;}

// listing 04.16$p = new ShopProduct();print $p->calculateTax(100) . "\n";

$u = new UtilityService();print $u->calculateTax(100) . "\n";

I declare the PriceUtilities trait with the trait keyword. The body of a trait looks very similar to that of a class. It is simply a set of methods and properties collected within braces. Once I have declared it, I can access the PriceUtilities trait from within my classes. I do this with the use keyword followed by the name of the trait I wish to incorporate. So having declared and implemented the calculateTax() method in a single place, I go ahead and incorporate it into both the ShopProduct and the UtilityService classes.

57

Chapter 4 ■ advanCed Features

Using More than One TraitYou can include multiple traits in a class by listing each one after the use keyword, separated by commas. In this example, I define and apply a new trait, IdentityTrait, keeping my original PriceUtilities trait:

// listing 04.17trait IdentityTrait{    public function generateId(): string    {        return uniqid();    }}

// listing 04.18class ShopProduct{    use PriceUtilities, IdentityTrait;}

// listing 04.19$p = new ShopProduct();print $p->calculateTax(100) . "\n";print $p->generateId() . "\n";

By applying both PriceUtilities and IdentityTrait with the use keyword, I make the 

calculateTax() and the generateId() methods available to the ShopProduct class. This means the class offers both the calculateTax() and generateId() methods.

 ■ Note  the IdentityTrait trait provides the generateId() method. In fact, a database often generates identifiers for objects, but you might switch in a local implementation for testing purposes. You can find out more about objects, databases, and unique identifiers in Chapter 12, which covers the Identity Map pattern. You can learn more about testing and mocking in Chapter 18.

Combining Traits and InterfacesAlthough traits are useful, they don’t change the type of the class to which they are applied. So when you apply the IdentityTrait trait to multiple classes, they won’t share a type that could be hinted for in a method signature.

Luckily, traits play well with interfaces. I can define an interface that requires a generateId() method, 

and then declare that ShopProduct implements it:

// listing 04.20interface IdentityObject{    public function generateId(): string;}

58

Chapter 4 ■ advanCed Features

// listing 04.21trait IdentityTrait{    public function generateId(): string    {        return uniqid();    }}

// listing 04.22class ShopProduct implements IdentityObject{    use PriceUtilities, IdentityTrait;}

As before, ShopProduct uses the IdentityTrait trait. However, the method this imports, generateId() now also fulfills a commitment to the IdentityObject interface. This means that we can pass ShopProduct objects to methods and functions that use type hinting to demand IdentityObject instances, like this:

// listing 04.23    public static function storeIdentityObject(IdentityObject $idobj)    {        // do something with the IdentityObject    }

// listing 04.24$p = new ShopProduct();self::storeIdentityObject($p);print $p->calculateTax(100) . "\n";print $p->generateId() . "\n";

Managing Method Name Conflicts with insteadofThe ability to combine traits is a nice feature, but sooner or later conflicts are inevitable. Consider what would happen, for example, if I were to use two traits that provide a calculateTax() method:

// listing 04.25trait TaxTools{    function calculateTax(float $price): float    {        return 222;    }}

// listing 04.26trait PriceUtilities{    private $taxrate = 17;

    public function calculateTax(float $price): float    {

59

Chapter 4 ■ advanCed Features

        return (($this->taxrate / 100) * $price);    }

    // other utilities}

// listing 04.27class UtilityService extends Service{    use PriceUtilities, TaxTools;}

// listing 04.28$u = new UtilityService();print $u->calculateTax(100) . "\n";

Because I have included two traits that contain calculateTax() methods, PHP is unable to work out 

which should override the other. The result is a fatal error:

PHP Fatal error:  Trait method calculateTax has not been applied, because thereare collisions with other trait methods on...

To fix this problem, I can use the insteadof keyword. Here’s how:

// listing 04.29class UtilityService extends Service{    use PriceUtilities, TaxTools {        TaxTools::calculateTax insteadof PriceUtilities;    }}

// listing 04.30$u = new UtilityService();print $u->calculateTax(100) . "\n";

In order to apply further directives to a use statement, I must first add a body. I do this with opening and closing braces. Within this block, I use the insteadof operator. This requires a fully qualified method reference (i.e., one that identifies both the trait and the method names, separated by a scope resolution operator) on the left-hand side. On the right-hand side, insteadof requires the name of the trait whose equivalent method should be overridden:

TaxTools::calculateTax insteadof PriceUtilities;

The preceding snippet means,「Use the calculateTax() method of TaxTools instead of the method of 

the same name in PriceUtilities.」

So when I run this code, I get the dummy output I planted in TaxTools::calculateTax():

222

60

Chapter 4 ■ advanCed Features

Aliasing overridden trait methodsWe have seen that you can use insteadof to disambiguate between methods. What do you do, though, if you want to then access the overridden method? The as operator allows you to alias trait methods. Once again, the as operator requires a full reference to a method on its left-hand side. On the right-hand side of the operator, you should put the name of the alias. So here, for example, I reinstate the calculateTax() method of the PriceUtilities trait using the new name basicTax():

// listing 04.31class UtilityService extends Service{

    use PriceUtilities, TaxTools {        TaxTools::calculateTax insteadof PriceUtilities;        PriceUtilities::calculateTax as basicTax;    }}

// listing 04.32$u = new UtilityService();print $u->calculateTax(100) . "\n";print $u->basicTax(100) . "\n";

This gives the following output:

22217

So PriceUtilities::calculateTax() has been resurrected as part of the UtilityService class under 

the name basicTax().

 Where a method name clashes between traits, it is not enough to alias one of the method names in 

 ■ Note the use block. You must first determine which method supercedes the other using the insteadof operator. then you can reassign the discarded method a new name with the as operator.

Incidentally, you can also use method name aliasing where there is no name clash. You might, for 

example, want to use a trait method to implement an abstract method signature declared in a parent class or in an interface.

Using static methods in traitsMost of the examples you have seen so far could use static methods because they do not store instance data. There’s nothing complicated about placing a static method in a trait. Here I change the PriceUtilities::$taxrate property and the PriceUtilities::calculateTax() methods so that they are static:

// listing 04.33trait PriceUtilities{

61

Chapter 4 ■ advanCed Features

    private static $taxrate = 17;

    public static function calculateTax(float $price): float    {        return ((self::$taxrate / 100) * $price);    }

    // other utilities}

// listing 04.34class UtilityService extends Service{    use PriceUtilities;}

// listing 04.35$u = new UtilityService();print $u::calculateTax(100) . "\n";

As you might expect, this script outputs the following:

17

So, static methods are declared in traits and accessed via the host class in the normal way.

Accessing Host Class PropertiesYou might assume that static methods are really the only way to go as far as traits are concerned. Even trait methods that are not declared static are essentially static in nature, right? Well, wrong, in fact—you can access properties and methods in a host class:

// listing 04.36trait PriceUtilities{    function calculateTax(float $price): float    {        // is this good design?        return (($this->taxrate / 100) * $price);    }

    // other utilities}

// listing 04.37class UtilityService extends Service{    public $taxrate = 17;    use PriceUtilities;}

62

Chapter 4 ■ advanCed Features

// listing 04.38$u = new UtilityService();print $u->calculateTax(100) . "\n";

In the preceding code, I amend the PriceUtilities trait so that it accesses a property in its host class. If you think that this is bad design, you’re right. It’s spectacularly bad design. Although it’s useful for the trait to access data set by its host class, there is nothing to require the UtilityService class to actually provide a $taxrate property. Remember that traits should be usable across many different classes. What is the guarantee or even the likelihood that any host classes will declare a $taxrate?

On the other hand, it would be great to be able to establish a contract that says, essentially,「If you use 

this trait, then you must provide it certain resources.」

In fact, you can achieve exactly this effect. Traits support abstract methods.

Defining Abstract Methods in TraitsYou can define abstract methods in a trait in just the same way you would in a class. When a trait is used by a class, it takes on the commitment to implement any abstract methods it declares.

Armed with this knowledge, I can reimplement my previous example so that the trait forces the using 

class to provide tax rate information:

// listing 04.39trait PriceUtilities{    function calculateTax(float $price): float    {        // better design.. we know getTaxRate() is implemented        return (($this->getTaxRate() / 100) * $price);    }

    abstract function getTaxRate(): float;    // other utilities}

// listing 04.40class UtilityService extends Service{    use PriceUtilities;

    public function getTaxRate(): float    {        return 17;    }}

// listing 04.41$u = new UtilityService();print $u->calculateTax(100) . "\n";

By declaring an abstract getTaxRate() method in the PriceUtilities trait, I force the UtilityService class to provide an implementation. Of course, since PHP does not constrain return types, the UtilityService::calculateTax() method cannot be absolutely certain it’s going to get a sane value from getTaxRate(). 

63

Chapter 4 ■ advanCed Features

You could overcome this to some extent by writing all sorts of checking routines, but this misses the point. It is probably adequate just to signal to a client coder that she should provide certain information by requiring the implementation of a method or two.

Changing Access Rights to Trait MethodsYou can, of course, declare a trait method public, private, or protected. However, you can also change this access from within the class that uses the trait. You have already seen that the as operator can be used to alias a method name. If you use an access modifier on the right-hand side of this operator, it will change the method’s access level rather than its name.

Imagine, for example, you would like to use calculateTax() from within UtilityService, but not 

make it available to implementing code. Here’s how you would change the use statement:

// listing 04.42trait PriceUtilities{    public function calculateTax(float $price): float    {        return (($this->getTaxRate() / 100) * $price);    }    public abstract function getTaxRate(): float;    // other utilities}

// listing 04.43class UtilityService extends Service{    use PriceUtilities {        PriceUtilities::calculateTax as private;    }

    private $price;

    public function __construct(float $price)    {        $this->price = $price;    }

    public function getTaxRate(): float    {        return 17;    }

    public function getFinalPrice(): float    {        return ($this->price + $this->calculateTax($this->price));    }}

64

Chapter 4 ■ advanCed Features

// listing 04.44$u = new UtilityService(100);print $u->getFinalPrice() . "\n";

I deploy the as operator in conjunction with the private keyword in order to set private access to 

calculateTax(). This means I can access the method from getFinalPrice(). Here’s an external attempt to access calculateTax():

$u = new UtilityService(100);print $u->calculateTax()."\n";

Unfortunately, this code will generate an error:

Error: Call to private method popp\ch04\batch06_9\UtilityService::calculateTax() from context ...

Late Static Bindings: The static Keyword

Now that you’ve seen abstract classes, traits, and interfaces, it’s time to return briefly to static methods. You saw that a static method can be used as factory, a way of generating instances of the containing class. If you’re as lazy a coder as me, you might chafe at the duplication in an example like this:

// listing 04.45abstract class DomainObject{

}

// listing 04.46class User extends DomainObject{    public static function create(): User    {        return new User();    }}

// listing 04.47class Document extends DomainObject{    public static function create(): Document    {        return new Document();    }}

I create a super class named DomainObject. In a real-world project, of course, this would contain 

functionality common to its extending classes. Then I create two child classes, User and Document. I would like my concrete classes to have static create() methods.

65

Chapter 4 ■ advanCed Features

 Why would I use a static factory method when a constructor performs the work of creating an 

 ■ Note object already? In Chapter 12, I’ll describe a pattern called Identity Map. an Identity Map component generates and manages a new object only if an object with the same distinguishing characteristics is not already under management. If the target object already exists, it is returned. a factory method like create() would make a good client for a component of this sort.

This code works fine, but it has an annoying amount of duplication. I don’t want to have to create 

boilerplate code like this for every DomainObject child class that I create. Instead, I’ll try pushing the create() method up to the superclass:

// listing 04.48abstract class DomainObject{    public static function create(): DomainObject    {        return new self();    }}

// listing 04.49class User extends DomainObject{}

// listing 04.50class Document extends DomainObject{}

// listing 04.51Document::create();

Well, that looks neat. I now have common code in one place, and I’ve used self as a reference to the 

class. But I have made an assumption about the self keyword. In fact, it does not act for classes exactly the same way that $this does for objects. self does not refer to the calling context; it refers to the context of resolution. So if I run the previous example, I get this:

Error: Cannot instantiate abstract class popp\ch04\batch06\DomainObject

So self resolves to DomainObject, the place where create() is defined, and not to Document, the class 

on which it was called. Until PHP 5.3 this was a serious limitation, which spawned many rather clumsy workarounds. PHP 5.3 introduced a concept called late static bindings. The most obvious manifestation of this feature is the keyword: static. static is similar to self, except that it refers to the invoked rather than the containing class. In this case, it means that calling Document::create() results in a new Document object and not a doomed attempt to instantiate a DomainObject object.

66

So now I can take advantage of my inheritance relationship in a static context:

Chapter 4 ■ advanCed Features

abstract class DomainObject{    public static function create(): DomainObject    {        return new static();    }}

class User extends DomainObject{}

class Document extends DomainObject{}

print_r(Document::create());

Document Object()

The static keyword can be used for more than just instantiation. Like self and parent, static can be used as an identifier for static method calls, even from a non-static context. Let’s say I want to include the concept of a group for my DomainObject classes. By default in my new classification, all classes fall into category「default,」but I’d like to be able override this for some branches of my inheritance hierarchy:

// listing 04.52abstract class DomainObject{    private $group;

    public function __construct()    {        $this->group = static::getGroup();    }

    public static function create(): DomainObject    {        return new static();    }

    public static function getGroup(): string    {        return "default";    }}

67

Chapter 4 ■ advanCed Features

// listing 04.53class User extends DomainObject{}

// listing 04.54class Document extends DomainObject{    public static function getGroup(): string    {        return "document";    }}

// listing 04.55class SpreadSheet extends Document{}

// listing 04.56print_r(User::create());print_r(SpreadSheet::create());

I introduced a constructor to the DomainObject class. It uses the static keyword to invoke a static 

method: getGroup(). DomainObject provides the default implementation, but Document overrides it. I also created a new class, SpreadSheet, that extends Document. Here’s the output:

popp\ch04\batch07\User Object(    [group:popp\ch04\batch07\DomainObject:private] => default)popp\ch04\batch07\SpreadSheet Object(    [group:popp\ch04\batch07\DomainObject:private] => document)

For the User class, not much clever needs to happen. The DomainObject constructor calls getGroup() and finds it locally. In the case of SpreadSheet, though, the search begins at the invoked class, SpreadSheet itself. It provides no implementation, so the getGroup() method in the Document class is invoked. Before PHP 5.3 and late static binding, I would have been stuck with the self keyword here, which would only look for getGroup() in the DomainObject class.

Handling Errors

Things go wrong. Files are misplaced, database servers are left uninitialized, URLs are changed, XML files are mangled, permissions are poorly set, disk quotas are exceeded. The list goes on and on. In the fight to anticipate every problem, a simple method can sometimes sink under the weight of its own error-handling code.

68

Here is a simple Conf class that stores, retrieves, and sets data in an XML configuration file:

Chapter 4 ■ advanCed Features

// listing 04.57class Conf{    private $file;    private $xml;    private $lastmatch;

    public function __construct(string $file)    {        $this->file = $file;        $this->xml = simplexml:load_file($file);    }

    public function write()    {        file_put_contents($this->file, $this->xml->asXML());    }

    public function get(string $str)    {        $matches = $this->xml->xpath("/conf/item[@name=\"$str\"]");        if (count($matches)) {            $this->lastmatch = $matches[0];            return (string)$matches[0];        }        return null;    }

    public function set(string $key, string $value)    {        if (! is_null($this->get($key))) {            $this->lastmatch[0]=$value;            return;        }        $conf = $this->xml->conf;        $this->xml->addChild('item', $value)->addAttribute('name', $key);    }}

The Conf class uses the SimpleXml extension to access name value pairs. Here’s the kind of format with 

which it is designed to work:

<?xml version="1.0"?><conf>    <item name="user">bob</item>    <item name="pass">newpass</item>    <item name="host">localhost</item></conf>

69

Chapter 4 ■ advanCed Features

The Conf class’s constructor accepts a file path, which it passes to simplexml:load_file().It stores the resulting SimpleXmlElement object in a property called $xml. The get() method uses XPath to locate an item element with the given name attribute, returning its value. set() either changes the value of an existing item or creates a new one. Finally, the write() method saves the new configuration data back to the file.

Like much example code, the Conf class is highly simplified. In particular, it has no strategy for handling 

nonexistent or unwriteable files. It is also optimistic in outlook. It assumes that the XML document will be well-formed and will contain the expected elements.

Testing for these error conditions is relatively trivial, but I must still decide how to respond to them 

should they arise. There are generally two options.

First, I could end execution. This is simple but drastic. My humble class would then take responsibility 

for bringing an entire script crashing down around it. Although methods such as __construct() and write() are well placed to detect errors, they do not have the information to decide how to handle them.

Rather than handle the error in my class, then, I could return an error flag of some kind. This could be a Boolean or an integer value such as 0 or -1. Some classes will also set an error string or flag, so that the client code can request more information after a failure.

Many PEAR packages combine these two approaches by returning an error object (an instance of PEAR_

Error), which acts both as notification that an error has occurred and contains the error message within it. This approach is now deprecated, but plenty of classes have not been upgraded, not least because client code often depends on the old behavior.

The problem here is that you pollute your return value. You have to rely on the client coder to test for the 

return type every time your error-prone method is called. This can be risky. Trust no one!

When you return an error value to calling code, there is no guarantee that the client will be any better equipped than your method to decide how to handle the error. If this is the case, then the problem begins all over again. The client method will have to determine how to respond to the error condition, maybe even implementing a different error-reporting strategy.

ExceptionsPHP 5 introduced exceptions to PHP, a radically different way of handling error conditions. Different for PHP, that is. You will find them hauntingly familiar if you have Java or C++ experience. Exceptions address all of the issues that I have raised so far in this section.

An exception is a special object instantiated from the built-in Exception class (or from a derived class). 

Objects of type Exception are designed to hold and report error information.

The Exception class constructor accepts two optional arguments, a message string and an error code. 

The class provides some useful methods for analyzing error conditions. These are described in Table 4-1.

The Exception class is fantastically useful for providing error notification and debugging information 

(the getTrace() and getTraceAsString() methods are particularly helpful in this regard). In fact, it is almost identical to the PEAR_Error class that was discussed earlier. There is much more to an exception than the information it holds, though.

70

Chapter 4 ■ advanCed Features

Table 4-1.  The Exception Class’s Public Methods

Method

Description

getMessage()

getCode()

getFile()

getLine()

getPrevious()

getTrace()

Get the message string that was passed to the constructorGet the code integer that was passed to the constructorGet the file in which the exception was generatedGet the line number at which the exception was generatedGet a nested Exception objectGet a multidimensional array tracing the method calls that led to the exception, including method, class, file, and argument data

getTraceAsString() Get a string version of the data returned by getTrace()

__toString()

Called automatically when the Exception object is used in string context. Returns a string describing the exception details

Throwing an ExceptionThe throw keyword is used in conjunction with an Exception object. It halts execution of the current method and passes responsibility for handling the error back to the calling code. Here I amend the __construct() method to use the throw statement:

// listing 04.58    public function __construct(string $file)    {        $this->file = $file;        if (! file_exists($file)) {            throw new \Exception("file '$file' does not exist");        }        $this->xml = simplexml:load_file($file);    }

The write() method can use a similar construct:

// listing 04.59    public function write()    {        if (! is_writeable($this->file)) {            throw new \Exception("file '{$this->file}' is not writeable");        }        file_put_contents($this->file, $this->xml->asXML());    }

71

Chapter 4 ■ advanCed Features

The __construct() and write() methods can now check diligently for file errors as they do their work, 

but they let code more fitted for the purpose decide how to respond to any errors detected.

So how does client code know how to handle an exception when thrown? When you invoke a method 

that may throw an exception, you can wrap your call in a try clause. A try clause is made up of the try keyword followed by braces. The try clause must be followed by at least one catch clause in which you can handle any error, like this:

// listing 04.60try {    $conf = new Conf(__DIR__ . "/conf01.xml");    print "user: " . $conf->get('user') . "\n";    print "host: " . $conf->get('host') . "\n";    $conf->set("pass", "newpass");    $conf->write();} catch (\Exception $e) {    die($e->__toString());}

As you can see, the catch clause superficially resembles a method declaration. When an exception is 

thrown, the catch clause in the invoking scope is called. The Exception object is automatically passed in as the argument variable.

Just as execution is halted within the throwing method when an exception is thrown, so it is within the 

try clause—control passes directly to the catch clause.

Subclassing ExceptionYou can create classes that extend the Exception class as you would with any user-defined class. There are two reasons why you might want to do this. First, you can extend the class’s functionality. Second, the fact that a derived class defines a new class type can aid error handling in itself.

You can, in fact, define as many catch clauses as you need for a try statement. The particular catch 

clause invoked will depend on the type of the thrown exception and the class type hint in the argument list. Here are some simple classes that extend Exception:

// listing 04.61class XmlException extends \Exception{    private $error;

    public function __construct(\LibXmlError $error)    {        $shortfile = basename($error->file);        $msg = "[{$shortfile}, line {$error->line}, col {$error->column}] {$error->message}";        $this->error = $error;        parent::__construct($msg, $error->code);    }

    public function getLibXmlError()    {        return $this->error;    }

72

Chapter 4 ■ advanCed Features

}

// listing 04.62class FileException extends \Exception{}

// listing 04.63class ConfException extends \Exception{}

The LibXmlError class is generated behind the scenes when SimpleXml encounters a broken XML file. It 

has $message and $code properties, and it resembles the Exception class. I take advantage of this similarity and use the LibXmlError object in the XmlException class. The FileException and ConfException classes do nothing more than subclass Exception. I can now use these classes in my code and amend both __construct() and write():

// listing 04.64

// Conf class...

    function __construct(string $file)    {        $this->file = $file;        if (! file_exists($file)) {            throw new FileException("file '$file' does not exist");        }        $this->xml = simplexml:load_file($file, null, LIBXML_NOERROR);        if (! is_object($this->xml)) {            throw new XmlException(libxml:get_last_error());        }        $matches = $this->xml->xpath("/conf");        if (! count($matches)) {            throw new ConfException("could not find root element: conf");        }    }

    function write()    {        if (! is_writeable($this->file)) {            throw new FileException("file '{$this->file}' is not writeable");        }        file_put_contents($this->file, $this->xml->asXML());    }

__construct() throws either an XmlException, a FileException, or a ConfException, depending on 

the kind of error it encounters. Note that I pass the option flag LIBXML_NOERROR to simplexml:load_file(). This suppresses warnings, leaving me free to handle them with my XmlException class after the fact. If I encounter a malformed XML file, I know that an error has occurred because simplexml:load_file() won’t have returned an object. I can then access the error using libxml:get_last_error().

73

Chapter 4 ■ advanCed Features

The write() method throws a FileException if the $file property points to an unwritable entity.So, I have established that __construct() might throw one of three possible exceptions. How can I take 

advantage of this? Here’s some code that instantiates a Conf object:

// listing 04.65    public static function init()    {        try {            $conf = new Conf(__DIR__."/conf.broken.xml");            print "user: " . $conf->get('user') . "\n";            print "host: " . $conf->get('host') . "\n";            $conf->set("pass", "newpass");            $conf->write();        } catch (FileException $e) {            // permissions issue or non-existent file        } catch (XmlException $e) {            // broken xml        } catch (ConfException $e) {            // wrong kind of XML file        } catch (\Exception $e) {            // backstop: should not be called        }    }

I provide a catch clause for each class type. The clause invoked depends on the exception type thrown. 

The first to match will be executed, so remember to place the most generic type at the end and the most specialized at the start. For example, if you were to place the catch clause for Exception ahead of the clause for XmlException and ConfException, neither of these would ever be invoked. This is because both of these classes belong to the Exception type, and would therefore match the first clause.

The first catch clause (FileException) is invoked if there is a problem with the configuration file (if the file is nonexistent or unwriteable). The second clause (XmlException) is invoked if an error occurs in parsing the XML file (e.g., if an element is not closed). The third clause (ConfException) is invoked if a valid XML file does not contain the expected root conf element. The final clause (Exception) should not be reached because my methods only generate the three exceptions, which are explicitly handled. It is often a good idea to have a「backstop」clause like this, in case you add new exceptions to the code during development.

 If you do provide a「backstop」catch clause, you should ensure that you actually do something about 

 ■ Note the exception in most instances—failing silently can cause bugs which are hard to diagnose.

The benefit of these fine-grained catch clauses is that they allow you to apply different recovery or failure mechanisms to different errors. For example, you may decide to end execution, log the error and continue, or explicitly rethrow an error:

        try {            //...        } catch ( FileException $e ) {            throw $e;        }

74

Chapter 4 ■ advanCed Features

Another trick you can play here is to throw a new exception that wraps the current one. This allows you to stake a claim to the error and add your own contextual information, while retaining the data encapsulated by the exception you have caught. You can read more about this technique in Chapter 15.

So what happens if an exception is not caught by client code? It is implicitly rethrown, and the client’s 

own calling code is given the opportunity to catch it. This process continues either until the exception is caught or until it can no longer be thrown. At this point, a fatal error occurs. Here’s what would happen if I did not catch one of the exceptions in my example:

PHP Fatal error:  Uncaught exception 'FileException' with message'file 'nonexistent/not_there.xml' does not exist' in ...

So, when you throw an exception, you force the client to take responsibility for handling it. This is not an abdication of responsibility. An exception should be thrown when a method has detected an error, but does not have the contextual information to be able to handle it intelligently. The write() method in my example knows when the attempt to write will fail, and it knows why, but it does not know what to do about it. This is as it should be. If I were to make the Conf class more knowledgeable than it currently is, it would lose focus and become less reusable.

Cleaning Up After try/catch Clauses with finallyThe way that code flow is affected by exceptions can cause unexpected problems. For example, clean-up code or other essential housekeeping may not be performed after an exception is generated within a try clause. As you have seen, if an exception is generated within a try clause, flow moves directly to the relevant catch clause. Code that closes database connections or file handles may not get called, and status information might not be updated.

Imagine, for example, that Runner::init() keeps a log of its actions. It logs the start of the initialization 

process, any errors encountered, and then it logs the end of the initialization process. Here I provide a typically simplified example of this kind of logging:

// listing 04.66    public static function init()    {        try {            $fh = fopen(__DIR__ . "/log.txt", "a");            fputs($fh, "start\n");            $conf = new Conf(dirname(__FILE__) . "/conf.broken.xml");            print "user: " . $conf->get('user') . "\n";            print "host: " . $conf->get('host') . "\n";            $conf->set("pass", "newpass");            $conf->write();            fputs($fh, "end\n");            fclose($fh);        } catch (FileException $e) {            // permissions issue or non-existent file            fputs($fh, "file exception\n");            throw $e;        } catch (XmlException $e) {            fputs($fh, "xml exception\n");

75

Chapter 4 ■ advanCed Features

            // broken xml        } catch (ConfException $e) {            fputs($fh, "conf exception\n");            // wrong kind of XML file        } catch (\Exception $e) {            fputs($fh, "general exception\n");            // backstop: should not be called        }    }

I open a file, log.txt; I write to it; and then I call my configuration code. If an exception is encountered 

in this process, I log this fact in the relevant catch clause. I end the try clause by writing to the log and closing its file handle.

Of course, this last step will never be reached if an exception is encountered. Flow passes straight to the relevant catch block, and the rest of the try clause is never run. Here is the log output when a file exception is generated:

startfile exception

As you can see, the logging began, and the file exception was noted, but the portion of code that 

registers the end of logging was never reached, and so the log was not updated with that.

You might think that the solution would be to place the final logging step outside of the try /catch 

block altogether. This would not work reliably. If a generated exception is caught, and the try block allows execution to continue, then flow will move beyond the try / catch construct. However, a catch clause could rethrow the exception, or it might end script execution altogether.

To help programmers deal with problems like this, PHP 5.5 introduced a new clause: finally. If you’re 

familiar with Java, it’s likely you’ll have seen this clause before. Although catch clauses are only conditionally run when matching exceptions are thrown, the finally clause is always run, whether or not an exception is generated within the try block.

I can fix this problem by moving my log write and code to close to a finally clause:

    public static function init()    {        $fh = fopen(__DIR__ . "/log.txt", "a");        try {            fputs($fh, "start\n");            $conf = new Conf(dirname(__FILE__) . "/conf.broken.xml");            print "user: " . $conf->get('user') . "\n";            print "host: " . $conf->get('host') . "\n";            $conf->set("pass", "newpass");            $conf->write();        } catch (FileException $e) {            // permissions issue or non-existent file            fputs($fh, "file exception\n");        } catch (XmlException $e) {            fputs($fh, "xml exception\n");            // broken xml        } catch (ConfException $e) {            fputs($fh, "conf exception\n");

76

Chapter 4 ■ advanCed Features

            // wrong kind of XML file        } catch (Exception $e) {            fputs($fh, "general exception\n");            // backstop: should not be called        } finally {            fputs($fh, "end\n");            fclose($fh);        }    }

Because the log write and the fclose() invocation are wrapped in a finally clause, these statements 

will be run even if, as is the case when a FileException is caught, the exception is rethrown.

Here, again, is the log text when a FileException is generated:

startfile exceptionend

 a finally clause will be run if an invoked catch clause rethrows an exception or returns a value. 

 ■ Note however, calling die() or exit() in a try or catch block will end script execution, and the finally clause will not be run.

Final Classes and Methods

Inheritance allows for enormous flexibility within a class hierarchy. You can override a class or method so that a call in a client method will achieve radically different effects, according to which class instance it has been passed. Sometimes, though, a class or method should remain fixed and unchanging. If you have achieved the definitive functionality for your class or method, and you feel that overriding it can only damage the ultimate perfection of your work, you may need the final keyword.

final puts a stop to inheritance. A final class cannot be subclassed. Less drastically, a final method 

cannot be overridden.

Here’s a final class:

// listing 04.67final class Checkout{    // ...}

Here’s an attempt to subclass the Checkout class:

// listing 04.68class IllegalCheckout extends Checkout{    // ...}

77

Chapter 4 ■ advanCed Features

This produces an error:

PHP Fatal error:  Class IllegalCheckout may not inherit from final class (Checkout) in ....

I could relax matters somewhat by declaring a method in Checkout final, rather than the whole class. The final keyword should be placed in front of any other modifiers such as protected or static, like this:

// listing 04.69class Checkout{    final public function totalize()    {        // calculate bill    }}

I can now subclass Checkout, but any attempt to override totalize() will cause a fatal error:

// listing 04.70class IllegalCheckout extends Checkout{    final public function totalize()    {        // change bill calculation    }}

PHP Fatal error:  Cannot override final method popp\ch04\batch14\Checkout::totalize() ...

Good object-oriented code tends to emphasize the well-defined interface. Behind the interface, 

though, implementations will often vary. Different classes or combinations of classes conform to common interfaces but behave differently in different circumstances. By declaring a class or method final, you limit this flexibility. There will be times when this is desirable, and you will see some of them later in the book. However, you should think carefully before declaring something final. Are there really no circumstances in which overriding would be useful? You could always change your mind later on, of course, but this might not be so easy if you are distributing a library for others to use. Use final with care.

The Internal Error Class

Back when exceptions were first introduced, the world of trying and catching applied primarily to code written in PHP and not the core engine. Internally generated errors maintained their own logic. This could get messy if you wanted to manage core errors in the same way as code-generated exceptions. PHP 7 has made a start on addressing this issue with the Error class. This implements Throwable—the same built-in interface that the Exception class implements, and therefore it can be treated in the same way. This also means the methods described in Table 4-1 are honored. Error is subclassed for individual error types. Here’s how you might catch a parse error generated by an eval statement:

78

Chapter 4 ■ advanCed Features

        try {            eval("illegal code");        } catch (\Error $e) {            print get_class($e)."\n";        } catch (\Exception $e) {            // do something with an Exception        }

Here’s the output:

ParseError

So you can match some types of internal errors in catch clauses, either by specifying the Error 

superclass or by specifying a more specific subclass. Table 4-2 shows the current Error subclasses.

Table 4-2.  The Built-in Error Classes Introduced by PHP 7

Error

Description

ArithmeticError

Thrown for math-related errors—particularly those related to bitwise arithmeticThrown when the assert() language construct (used in debugging) fails

AssertionErrorDivisionByZeroError Thrown when an attempt is made to divide a number by zeroParseError

Thrown when a runtime attempt to parse PHP (using eval(), for example) fails

TypeError

Thrown when an argument of the wrong type is passed to a method, a method returns a value of the wrong type, or an incorrect number of arguments are passed to a method

 ■ Note  at the time of this writing, an attempt to call Error::getMessage() fails with an error, despite the fact that this is declared in the Throwable interface. It is likely that this issue will have been fixed by the time you read this!

Working with Interceptors

PHP provides built-in interceptor methods that can intercept messages sent to undefined methods and properties. This is also known as overloading, but as that term means something quite different in Java and C++, I think it is better to talk in terms of interception.

PHP supports three built-in interceptor methods. Like __construct(), these are invoked for you when 

the right conditions are met. Table 4-3 describes the methods.

79

Chapter 4 ■ advanCed Features

Table 4-3.  The Interceptor Methods

Method

Description

__get($property)

__set($property, $value)

__isset($property)

__unset($property)

__call($method, $arg_array)

Invoked when an undefined property is accessedInvoked when a value is assigned to an undefined propertyInvoked when isset() is called on an undefined propertyInvoked when unset() is called on an undefined propertyInvoked when an undefined non-static method is called

__callStatic($method, $arg_array)

Invoked when an undefined static method is called

The __get() and __set() methods are designed for working with properties that have not been 

declared in a class (or its parents).

__get()is invoked when client code attempts to read an undeclared property. It is called automatically 

with a single string argument containing the name of the property that the client is attempting to access. Whatever you return from the __get() method will be sent back to the client as if the target property exists with that value. Here’s a quick example:

// listing 04.71class Person{    public function __get(string $property)    {        $method = "get{$property}";        if (method_exists($this, $method)) {            return $this->$method();        }    }

    public function getName(): string    {        return "Bob";    }

    public function getAge(): int    {        return 44;    }}

When a client attempts to access an undefined property, the __get() method is invoked. I have 

implemented __get() to take the property name and construct a new string, prepending the word「get」. I pass this string to a function called method_exists(), which accepts an object and a method name and tests for method existence. If the method does exist, I invoke it and pass its return value to the client. Assume the client requests a $name property:

$p = new Person();print $p->name;

80

Chapter 4 ■ advanCed Features

In this case, the getName() method is invoked behind the scenes:

Bob

If the method does not exist, I do nothing. The property that the user is attempting to access will resolve 

to NULL.

The __isset() method works in a similar way to __get(). It is invoked after the client calls isset() on 

an undefined property. Here’s how I might extend Person:

// listing 04.72    public function __isset(string $property)    {        $method = "get{$property}";        return (method_exists($this, $method));    }

Now a cautious user can test a property before working with it:

if (isset($p->name)) {    print $p->name;}

The __set() method is invoked when client code attempts to assign to an undefined property. It is 

passed two arguments: the name of the property and the value the client is attempting to set. You can then decide how to work with these arguments. Here I further amend the Person class:

// listing 04.73class Person{    private $myname;    private $myage;

    public function __set(string $property, string $value)    {        $method = "set{$property}";        if (method_exists($this, $method)) {            return $this->$method($value);        }    }

    public function setName(string $name)    {        $this->myname = $name;        if (! is_null($name)) {            $this->myname = strtoupper($this->myname);        }    }

81

Chapter 4 ■ advanCed Features

    public function setAge(int $age)    {        $this->myage = $age;    }}

In this example, I work with「setter」methods rather than「getters.」If a user attempts to assign to an 

undefined property, the __set() method is invoked with the property name and the assigned value. I test for the existence of the appropriate method and invoke it if it exists. In this way, I can filter the assigned value.

 ■ Note  remember that methods and properties in php documentation are frequently spoken of in static terms in order to identify them with their classes. so you might talk about the Person::$name property, even though the property is not declared static and would in fact be accessed via an object.

So if I create a Person object and then attempt to set a property called Person::$name, the __set() method is invoked because this class does not define a $name property. The method is passed the string "name" and the value that the client assigned. How the value is then used depends on the implementation of __set(). In this example, I construct a method name out of the property argument combined with the string, "set". The setName() method is found and duly invoked. This transforms the incoming value and stores it in a real property:

$p = new Person();$p->name = "bob";// the $myname property becomes 'BOB'

As you might expect, __unset() mirrors __set(). When unset() is called on an undefined property, __unset() is invoked with the name of the property. You can then do what you like with the information. This example passes null to a method resolved using the same technique that you saw used by __set():

// listing 04.74    public function __unset(string $property)    {        $method = "set{$property}";        if (method_exists($this, $method)) {            $this->$method(null);        }    }

The __call() method is probably the most useful of all the interceptor methods. It is invoked when an undefined method is called by client code. __call() is invoked with the method name and an array holding all arguments passed by the client. Any value that you return from the __call() method is returned to the client as if it were returned by the method invoked.

The __call() method can be useful for delegation. Delegation is the mechanism by which one object 

passes method invocations on to a second. It is similar to inheritance, in that a child class passes on a method call to its parent implementation. With inheritance the relationship between child and parent is fixed, so the ability to switch the receiving object at runtime means that delegation can be more flexible than inheritance. An example clarifies things a little. Here is a simple class for formatting information from the Person class:

82

Chapter 4 ■ advanCed Features

// listing 04.75class PersonWriter{

    public function writeName(Person $p)    {        print $p->getName() . "\n";    }

    public function writeAge(Person $p)    {        print $p->getAge() . "\n";    }}

I could, of course, subclass this to output Person data in various ways. Here is an implementation of the 

Person class that uses both a PersonWriter object and the __call() method: 

// listing 04.76class Person{    private $writer;

    public function __construct(PersonWriter $writer)    {        $this->writer = $writer;    }

    public function __call(string $method, array $args)    {        if (method_exists($this->writer, $method)) {            return $this->writer->$method($this);        }    }

    public function getName(): string    {        return "Bob";    }    public function getAge(): int    {        return 44;    }}

The Person class here demands a PersonWriter object as a constructor argument and stores it in a 

property variable. In the __call() method, I use the provided $method argument, testing for a method of the same name in the PersonWriter object I have stored. If I encounter such a method, I delegate the method call to the PersonWriter object, passing my current instance to it (in the $this pseudo-variable). Consider what happens if the client makes this call to Person:

83

Chapter 4 ■ advanCed Features

$person = new Person(new PersonWriter());$person->writeName();

In this case, the __call() method is invoked. I find a method called writeName() in my PersonWriter 

object and invoke it. This saves me from manually invoking the delegated method like this:

function writeName() {    $this->writer->writeName($this);}

The Person class has magically gained two new methods. Although automated delegation can save a lot of legwork, there can be a cost in clarity. If you rely too much on delegation, you present the world with a dynamic interface that resists reflection (the runtime examination of class facets) and is not always clear to the client coder at first glance. This is because the logic that governs the interaction between a delegating class and its target can be obscure—buried in methods like __call() rather than signaled up front by inheritance relationships or method type hints, as is the case for similar relationships. The interceptor methods have their place, but they should be used with care, and classes that rely on them should document this fact very clearly.

I will return to the topics of delegation and reflection later in the book.The __get() and __set() interceptor methods can also be used to manage composite properties. 

This can be a convenience for the client programmer. Imagine, for example, an Address class that manages a house number and a street name. Ultimately this object data will be written to database fields, so the separation of number and street is sensible. But if house numbers and street names are commonly acquired in undifferentiated lumps, then you might want to help the class’s user. Here is a class that manages a composite property, Address::$streetaddress:

// listing 04.77class Address{    private $number;    private $street;

    public function __construct(string $maybenumber, string $maybestreet = null)    {        if (is_null($maybestreet)) {            $this->streetaddress = $maybenumber;        } else {            $this->number = $maybenumber;            $this->street = $maybestreet;        }    }

    public function __set(string $property, string $value)    {        if ($property === "streetaddress") {            if (preg_match("/^(\d+.*?)[\s,]+(.+)$/", $value, $matches)) {                $this->number = $matches[1];                $this->street = $matches[2];            } else {                throw new \Exception("unable to parse street address: '{$value}'");            }

84

Chapter 4 ■ advanCed Features

        }    }

    public function __get(string $property)    {        if ($property === "streetaddress") {            return $this->number . " " . $this->street;        }    }}

// listing 04.78$address = new Address("441b Bakers Street");print "street address: {$address->streetaddress}\n";$address = new Address("15", "Albert Mews");print "street address: {$address->streetaddress}\n";$address->streetaddress = "34, West 24th Avenue";print "street address: {$address->streetaddress}\n";

When a user attempts to set the (nonexistent) Address::$streetaddress property, the interceptor 

method __call() is invoked. There, I test for the property name, streetaddress. Before I can set the $number and $street properties, I must first ensure that the provided value can be parsed, and then go ahead and extract the fields. For this example, I have set simple rules. An address can be parsed if it begins with a number and has spaces or commas ahead of a second part. Thanks to back references, if the check passes, I already have the data I’m looking for in the $matches array, and I assign values to the $number and $street properties. If the parse fails, I throw an exception. So when a string such as 441b Bakers Street is assigned to Address::$streetaddress, it’s actually the $number and $street properties that get populated. I can demonstrate this with print_r():

$address = new Address("441b Bakers Street");print_r($address);

Address Object(    [number:Address:private] => 441b    [street:Address:private] => Bakers Street)

The __get() method is much more straightforward, of course. Whenever the 

Address::$streetaddress property is accessed, __get() is invoked. In my implementation of this interceptor, I test for streetaddress and, if I find a match, I return a concatenation of the $number and $street properties.

Defining Destructor Methods

You have seen that the __construct() method is automatically invoked when an object is instantiated. PHP 5 also introduced the __destruct() method. This is invoked just before an object is garbage-collected; that is, before it is expunged from memory. You can use this method to perform any final cleaning up that might be necessary.

85

Chapter 4 ■ advanCed Features

Imagine, for example, a class that saves itself to a database when so ordered. I could use the __

destruct() method to ensure that an instance saves its data when it is deleted:

// listing 04.79class Person{    protected $name;    private   $age;    private   $id;

    public function __construct(string $name, int $age)    {        $this->name = $name;        $this->age  = $age;    }

    public function setId(int $id)    {        $this->id = $id;    }

    public function __destruct()    {        if (! empty($this->id)) {            // save Person data            print "saving person\n";        }    }}

The __destruct() method is invoked whenever a Person object is removed from memory. This will 

happen either when you call the unset() function with the object in question or when no further references to the object exist in the process. So if I create and destroy a Person object, you can see the __destruct() method come into play:

// listing 04.80$person = new Person("bob", 44);$person->setId(343);unset($person);// output:// saving person

Although tricks like this are fun, it’s worth sounding a note of caution. __call(), __destruct(), and 

their colleagues are sometimes called magic methods. As you will know if you have ever read a fantasy novel, magic is not always a good thing. Magic is arbitrary and unexpected. Magic bends the rules. Magic incurs hidden costs.

In the case of __destruct(), for example, you can end up saddling clients with unwelcome surprises. 

Think about the Person class—it performs a database write in its __destruct() method. Now imagine a novice developer idly putting the Person class through its paces. He doesn’t spot the __destruct() method, and he sets about instantiating a set of Person objects. Passing values to the constructor, he assigns the CEO’s secret and faintly obscene nickname to the $name property, and then sets $age at 150. He runs his test script a few times, trying out colorful name and age combinations.

86

Chapter 4 ■ advanCed Features

The next morning, his manager asks him to step into a meeting room to explain why the database 

contains insulting Person data. The moral? Do not trust magic.

Copying Objects with __clone()

In PHP 4, copying an object was a simple matter of assigning from one variable to another:

class CopyMe{}$first = new CopyMe();$second = $first;// PHP 4: $second and $first are 2 distinct objects// PHP 5 plus: $second and $first refer to one object

This「simple matter」was a source of many bugs, as object copies were accidentally spawned when 

variables were assigned, methods were called, and objects were returned. This was made worse by the fact that there was no way of testing two variables to see whether they referred to the same object. Equivalence tests would tell you whether all fields were the same (==) or whether both variables were objects (===), but not whether they pointed to the same object.

In PHP, objects are always assigned and passed around by reference. This means that when my previous example is run with PHP 5, $first and $second contain references to the same object instead of two copies. Although this is generally what you want when working with objects, there will be occasions when you need to get a copy of an object rather than a reference to an object.

PHP provides the clone keyword for just this purpose. clone operates on an object instance, producing 

a by-value copy:

class CopyMe{}$first  = new CopyMe();$second = clone $first;// PHP 5 plus: $second and $first are 2 distinct objects

The issues surrounding object copying only start here. Consider the Person class that I implemented in 

the previous section. A default copy of a Person object would contain the identifier (the $id property), which in a full implementation I would use to locate the correct row in a database. If I allow this property to be copied, a client coder can end up with two distinct objects referencing the same data source, which is probably not what she wanted when she made her copy. An update in one object will affect the other, and vice versa.Luckily, you can control what is copied when clone is invoked on an object. You do this by 

implementing a special method called __clone() (note the leading two underscores that are characteristic of built-in methods). __clone() is called automatically when the clone keyword is invoked on an object.

When you implement __clone(),it is important to understand the context in which the method runs. __clone() is run on the copied object and not the original. Here I add __clone() to yet another version of the Person class:

// listing 04.81class Person{    private $name;

87

Chapter 4 ■ advanCed Features

    private $age;    private $id;

    public function __construct(string $name, int $age)    {        $this->name = $name;        $this->age = $age;    }

    public function setId(int $id)    {        $this->id = $id;    }

    public function __clone()    {        $this->id = 0;    }}

When clone is invoked on a Person object, a new shallow copy is made, and its __clone() method is 

invoked. This means that anything I do in __clone() overwrites the default copy I already made. In this case, I ensure that the copied object’s $id property is set to zero:

// listing 04.82$person = new Person("bob", 44);$person->setId(343);$person2 = clone $person;// $person2 ://     name: bob//     age: 44//     id: 0.

A shallow copy ensures that primitive properties are copied from the old object to the new. Object 

properties, though, are copied by reference, which may not be what you want or expect when cloning an object. Say that I give the Person object an Account object property. This object holds a balance that I want copied to the cloned object. What I don’t want, though, is for both Person objects to hold references to the same account:

// listing 04.83class Account{    public $balance;

    public function __construct(float $balance)    {        $this->balance = $balance;    }}

// listing 04.84class Person

88

Chapter 4 ■ advanCed Features

{    private $name;    private $age;    private $id;    public  $account;

    public function __construct(string $name, int $age, Account $account)    {        $this->name = $name;        $this->age  = $age;        $this->account = $account;    }

    public function setId(int $id)    {        $this->id = $id;    }

    public function __clone()    {        $this->id   = 0;    }}

// listing 04.85$person = new Person("bob", 44, new Account(200));$person->setId(343);$person2 = clone $person;

// give $person some money$person->account->balance += 10;// $person2 sees the credit tooprint $person2->account->balance;

This gives the following output:

210

$person holds a reference to an Account object that I have kept publicly accessible for the sake of brevity (as you know, I would usually restrict access to a property, providing an accessor method, if necessary). When the clone is created, it holds a reference to the same Account object that $person references. I demonstrate this by adding to the $person object’s Account and confirming the increased balance via $person2.

If I do not want an object property to be shared after a clone operation, then it is up to me to clone it 

explicitly in the __clone() method:

    function __clone()    {        $this->id   = 0;        $this->account = clone $this->account;    }

89

Chapter 4 ■ advanCed Features

Defining String Values for Your Objects

Another Java-inspired feature introduced by PHP 5 was the __toString() method. Before PHP 5.2, when you printed an object, it would resolve to a string like this:

// listing 04.86class StringThing{}

// listing 04.87$st = new StringThing();print $st;

Object id #1

Since PHP 5.2, this code will produce an error like this:

Object of class popp\ch04\batch22\StringThing could not be converted to string ...

By implementing a __toString() method, you can control how your objects represent themselves 

when printed. __toString() should be written to return a string value. The method is invoked automatically when your object is passed to print or echo, and its return value is substituted. Here I add a __toString() version to a minimal Person class:

// listing 04.88class Person{    function getName(): string    {        return "Bob";    }

    function getAge(): int    {        return 44;    }

    function __toString(): string    {        $desc  = $this->getName() . " (age ";        $desc .= $this->getAge() . ")";        return $desc;    }}

Now when I print a Person object, the object will resolve to this:

$person = new Person();

90

Chapter 4 ■ advanCed Features

print $person;

Bob (age 44)

The __toString() method is particularly useful for logging and error reporting, as well as for classes 

whose main task is to convey information. The Exception class, for example, summarizes exception data in its __toString() method.

Callbacks, Anonymous Functions, and Closures

Although not strictly an object-oriented feature, anonymous functions are useful enough to mention here because you may encounter them in object-oriented applications that utilize callbacks.

To kick things off, here are a couple of classes:

// listing 04.89

class Product {    public $name;    public $price;

    public function __construct(string $name, float $price)    {        $this->name = $name;        $this->price = $price;    }}

class ProcessSale{    private $callbacks;

    public function registerCallback(callable $callback)    {        if (! is_callable($callback)) {            throw new Exception("callback not callable");        }        $this->callbacks[] = $callback;    }

    public function sale(Product $product)    {        print "{$product->name}: processing \n";        foreach ($this->callbacks as $callback) {            call_user_func($callback, $product);        }    }}

91

Chapter 4 ■ advanCed Features

This code is designed to run my various callbacks. It consists of two classes, Product and ProcessSale. 

Product simply stores $name and $price properties. I’ve made these public for the purposes of brevity. Remember, in the real world, you’d probably want to make your properties private or protected and provide accessor methods. ProcessSale consists of two methods.

The first, registerCallback(), accepts an unhinted scalar, tests it, and adds it to a callback array. The 

test, a built-in function called is_callable(), ensures that whatever I’ve been given can be invoked by a function such as call_user_func() or array_walk().

The second method, sale(), accepts a Product object, outputs a message about it, and then loops 

through the $callback array property. It passes each element to call_user_func(), which calls the code, passing it a reference to the product. All of the following examples will work with the framework.

Why are callbacks useful? They allow you to plug functionality into a component at runtime that is not directly related to that component’s core task. By making a component callback aware, you give others the power to extend your code in contexts you don’t yet know about.

Imagine, for example, that a future user of ProcessSale wants to create a log of sales. If the user has 

access to the class, she might add logging code directly to the sale() method. This isn’t always a good idea, though. If she is not the maintainer of the package that provides ProcessSale, then her amendments will be overwritten the next time the package is upgraded. Even if she is the maintainer of the component, adding many incidental tasks to the sale() method will begin to overwhelm its core responsibility, and potentially make it less usable across projects. I will return to these themes in the next section.

Luckily, though, I made ProcessSale callback-aware. Here I create a callback that simulates logging:

// listing 04.90$logger = create_function(    '$product',    'print "    logging ({$product->name})\n";');

$processor = new ProcessSale();$processor->registerCallback($logger);

$processor->sale(new Product("shoes", 6));print "\n";$processor->sale(new Product("coffee", 6));

I use create_function() to build my callback. As you can see, it accepts two string arguments: first, a list of parameters; and second, the function body. The result is often called an anonymous function as it’s not named in the manner of a standard function. Instead, it can be stored in a variable and passed to functions and methods as a parameter. That’s just what I do, storing the function in the $logger variable and passing it to ProcessSale::registerCallback(). Finally, I create a couple of products and pass them to the sale() method. You have already seen what happens there. The sale is processed (in reality a simple message is printed about the product) and any callbacks are executed. Here is the code in action:

shoes: processing    logging (shoes)

coffee: processing    logging (coffee)

Look again at that create_function() example. See how ugly it is? Placing code designed to be executed 

inside a string is always a pain. You need to escape variables and quotation marks, and, if the callback grows to any size, it can be very hard to read, indeed. Wouldn’t it be neater if there were a more elegant way of 

92

creating anonymous functions? Well, since PHP 5.3, there is a much better way of doing it. You can simply declare and assign a function in one statement. Here’s the previous example using the new syntax:

Chapter 4 ■ advanCed Features

// listing 04.91$logger2 = function ($product) {    print "    logging ({$product->name})\n";};

$processor = new ProcessSale();$processor->registerCallback($logger2);

$processor->sale(new Product("shoes", 6));print "\n";$processor->sale(new Product("coffee", 6));

The only difference here lies in the creation of the anonymous function. As you can see, it’s a lot neater. 

I simply use the function keyword inline, and without a function name. Note that because this is an inline statement, a semicolon is required at the end of the code block. The output here is the same as that of the previous example.

Of course, callbacks needn’t be anonymous. You can use the name of a function, or even an object 

reference and a method, as a callback. Here I do just that:

// listing 04.92class Mailer{    public function doMail(Product $product)    {        print "    mailing ({$product->name})\n";    }}

// listing 04.93$processor = new ProcessSale();$processor->registerCallback([new Mailer(), "doMail"]);

$processor->sale(new Product("shoes", 6));print "\n";$processor->sale(new Product("coffee", 6));

I create a class: Mailer. Its single method, doMail(), accepts a Product object and outputs a message about it. When I call registerCallback(), I pass it an array. The first element is a Mailer object, and the second is a string that matches the name of the method I want invoked. Remember that registerCallback() checks its argument for callability. is_callable() is smart enough to test arrays of this sort. A valid callback in array form should have an object as its first element, and the name of a method as its second element. I pass that test here, and here is my output:

shoes: process

ing    mailing (shoes)

coffee: processing    mailing (coffee)

93

Chapter 4 ■ advanCed Features

You can have a method return an anonymous function—something like this:

// listing 04.94class Totalizer{    public static function warnAmount()    {        return function (Product $product) {            if ($product->price > 5) {                print "    reached high price: {$product->price}\n";            }        };    }}

// listing 04.95$processor = new ProcessSale();$processor->registerCallback(Totalizer::warnAmount());// ...

Apart from the convenience of using the warnAmount() method as a factory for the anonymous 

function, I have not added much of interest here. But this structure allows me to do much more than just generate an anonymous function. It allows me to take advantage of closures. The new style anonymous functions can reference variables declared in the anonymous functions parent scope. This is a hard concept to grasp at times. It’s as if the anonymous function continues to remember the context in which it was created. Imagine that I want Totalizer::warnAmount() to do two things. First of all, I’d like it to accept an arbitrary target amount. Second, I want it to keep a tally of prices as products are sold. When the total exceeds the target amount, the function will perform an action (in this case, as you might have guessed, it will simply write a message).

I can make my anonymous function track variables from its wider scope with a use clause:

// listing 04.96class Totalizer2{    public static function warnAmount($amt)    {        $count=0;        return function ($product) use ($amt, &$count) {            $count += $product->price;            print "   count: $count\n";            if ($count > $amt) {                print "   high price reached: {$count}\n";            }        };    }}

// listing 04.97$processor = new ProcessSale();$processor->registerCallback(Totalizer2::warnAmount(8));

94

Chapter 4 ■ advanCed Features

$processor->sale(new Product("shoes", 6));print "\n";$processor->sale(new Product("coffee", 6));

The anonymous function returned by Totalizer2::warnAmount() specifies two variables in its use clause. The first is $amt. This is the argument that warnAmount() accepted. The second closure variable is $count. $count is declared in the body of warnAmount() and set initially to zero. Notice that I prepend an ampersand to the $count variable in the use clause. This means the variable will be accessed by reference rather than by value in the anonymous function. In the body of the anonymous function, I increment $count by the product’s value, and then test the new total against $amt. If the target value has been reached, I output a notification.

Here is the code in action:

shoes: processing   count: 6

coffee: processing   count: 12

   high price reached: 12

This demonstrates that the callback is keeping track of $count between invocations. Both $count and 

$amt remain associated with the function because they were present to the context of its declaration and because they were specified in its use clause.

Anonymous Classes

As of PHP 7 you can declare anonymous classes as well as functions. These are especially useful when you need to create and derive an instance from a small class. This is especially useful when the class in question is simple and specific to the local context.

Let’s return to our PersonWriter example. I’ll start off by creating an interface this time:

// listing 04.98interface PersonWriter{    public function write(Person $person);}

Now, here’s a version of the Person class that can use a PersonWriter object:

// listing 04.99class Person{    public function output(PersonWriter $writer)    {        $writer->write($this);    }

95

Chapter 4 ■ advanCed Features

    public function getName(): string    {        return "Bob";    }

    public function getAge(): int    {        return 44;    }}

The output() method accepts a PersonWriter instance, and then passes an instance of the current class to its write() method. In this way, the Person class is nicely insulated from the implementation of the writer.Moving on to client code, if we need a writer to print name and age values for a Person object, we might 

go ahead and create a class in the usual way. But it’s such a trivial implementation that we could equally create a class and pass it to Person at the same time:

// listing 04.100        $person = new Person();        $person->output(            new class implements PersonWriter {                public function write(Person $person)                {                    print $person->getName(). " " . $person->getAge() . "\n";                }            }        );

As you can see, you can declare an anonymous class with the keywords, new class. You can then add 

any extends and implements clauses required before creating the class block.

Anonymous classes do not support closures. In other words, variables declared in a wider scope cannot be accessed within the class. However you can pass values to an anonymous class’s constructor. Let’s create a slightly more complex PersonWriter:

// listing 04.101        $person = new Person();        $person->output(            new class("/tmp/persondump") implements PersonWriter {                private $path;

                public function __construct(string $path)                {                    $this->path = $path;                }

                public function write(Person $person)                {                     file_put_contents($this->path, $person->getName(). " " . $person 

->getAge() . "\n");

                }            }        );

96

Chapter 4 ■ advanCed Features

I passed a path argument to the constructor. This value was stored in the $path property and eventually 

used by the write() method.

Of course, if your anonymous class begins to grow in size and complexity, it becomes more sensible to 

create a named class in a class file. This is especially true if you find yourself duplicating your anonymous class in more than one place.

Summary

In this chapter, we came to grips with PHP’s advanced object-oriented features. Some of these will become familiar as you work through the book. In particular, I will return frequently to abstract classes, exceptions, and static methods.

In the next chapter, I take a step back from built-in object features and look at classes and functions 

designed to help you work with objects.

97

CHAPTER 5


# 2020082PHP-Objects-Patterns-PracticeR02

## 记忆时间

## 模板

### 1. 逻辑脉络

用自己的话总结主题，梳理逻辑脉络，也就是这本书整个地图里这一章所在的节点。

### 2. 摘录及评论

## 04. Advanced Features

You have already seen how class type hinting and access control give you more control over a class’s interface. In this chapter, I will delve deeper into PHP’s object-oriented features. This chapter will cover several subjects: 1) Static methods and properties: Accessing data and functionality through classes rather than objects. 2) Abstract classes and interfaces: Separating design from implementation. 3) Traits: Sharing implementation between class hierarchies. 4) Error handling: Introducing exceptions. 5) Final classes and methods: Limiting inheritance. 6) Destructor methods: Cleaning up after your objects. 7) Interceptor methods: Automating delegation. 8) Cloning objects: Making object copies. 9) Resolving objects to strings: Creating a summary method. 10) Callbacks: Adding functionality to components with anonymous functions and classes.

In this chapter, we came to grips with PHP’s advanced object-oriented features. Some of these will become familiar as you work through the book. In particular, I will return frequently to abstract classes, exceptions, and static methods. In the next chapter, I take a step back from built-in object features and look at classes and functions designed to help you work with objects.

### 4.1 Static Methods and Properties

All of the examples in the previous chapter worked with objects. I characterized classes as templates from which objects are produced, and objects as active instances of classes—the things whose methods you invoke and whose properties you access. I implied that, in object-oriented programming, the real work is done by instances of classes. Classes, after all, are merely templates for objects. In fact, it is not that simple. You can access both methods and properties in the context of a class rather than that of an object. Such methods and properties are「static」and must be declared as such by using the static keyword:

```php
// listing 04.01
class StaticExample{    
    static public $aNum = 0;    
    public static function sayHello() {
        print "hello";    
    }
}
```

Static methods are functions with class scope. They cannot themselves access any normal properties in the class because these would belong to an object; however, they can access static properties. If you change a static property, all instances of that class are able to access the new value. Because you access a static element via a class and not an instance, you do not need a variable that references an object. Instead, you use the class name in conjunction with ::, as in this example:

1『直接修改基类的静态方法、静态属性的强大在于，修改的数据会更新到所有基于该类的实例化对象身上。后面有一段内容专门说了静态属性和静态方法的 3 个优势。』

```php
print StaticExample::$aNum;
StaticExample::sayHello();
```

This syntax should be familiar from the previous chapter. I used :: in conjunction with parent to access an overridden method. Now, as then, I am accessing class rather than object data. Class code can use the parent keyword to access a superclass without using its class name. To access a static method or property from within the same class (rather than from a child), I would use the self keyword. self is to classes what the \$this pseudo-variable is to objects. So from outside the StaticExample class, I access the \$aNum property using its class name:

1『访问静态属性和静态方法，在外面用「classname::staticproperty」，在类定义里用「self::staticproperty」。在类定义里，self 关键词绑定到该「类」如同 \$this 绑定到通过该类实例化后的「对象」。』

```php
StaticExample::$aNum;
```

From within the StaticExample class, I can use the self keyword:

```php
// listing 04.02
class StaticExample{    
    static public $aNum = 0;    
    public static function sayHello()    {        
        self::$aNum++;        
        print "hello (".self::$aNum.")\n";    
    }
}
```

Note: Making a method call using parent is the only circumstance in which you should use a static reference to a nonstatic method. unless you are accessing an overridden method, you should only ever use :: to access a method or property that has been explicitly declared static. In documentation, however, you will often see static syntax used to refer to a method or property. this does not mean that the item in question is necessarily static, just that it belongs to a certain class. the write() method of the ShopProductWriter class might be referred to as ShopProductWriter::write(), for example, even though the write() method is not static. You will see this syntax here when that level of specificity is appropriate.

1『除非重载方法，不应该用 :: 去访问那些显式声明的静态属性和静态方法。目前还没弄清楚这个概念。（2020-04-27）』

By definition, static methods and properties are invoked on classes and not objects. For this reason, they are often referred to as class variables and properties. As a consequence of this class orientation, you cannot use the \$this pseudo-variable inside a static method.

So, why would you use a static method or property? Static elements have a number of characteristics that can be useful. First, they are available from anywhere in your script (assuming that you have access to the class). This means you can access functionality without needing to pass an instance of the class from object to object or, worse, storing an instance in a global variable. Second, a static property is available to every instance of a class, so you can set values that you want to be available to all members of a type. Finally, the fact that you don’t need an instance to access a static property or method can save you from instantiating an object purely to get at a simple function.

To illustrate this, I will build a static method for the ShopProduct class that automates the instantiation of ShopProduct objects. Using SQLite, I might define a products table like this:

```php
CREATE TABLE products (                            
        id INTEGER PRIMARY KEY AUTOINCREMENT,                            
        type TEXT,                            
        firstname TEXT,                            
        mainname TEXT,                            
        title TEXT,                            
        price float,                            
        numpages int,                            
        playlength int,                            
        discount int 
)
```

Now I want to build a getInstance() method that accepts a row ID and PDO object, uses them to acquire a database row, and then returns a ShopProduct object. I can add these methods to the ShopProduct class I created in the previous chapter. As you probably know, PDO stands for PHP Data Object. The PDO class provides a common interface to different database applications:

```php
// listing 04.03
// ShopProduct class...

    private $id = 0;    // ...

    public function setID(int $id)    {        
        $this->id = $id;    
    }    
    // ...

    public static function getInstance(int $id, \PDO $pdo): ShopProduct    {        
        $stmt = $pdo->prepare("select * from products where id=?");        
        $result = $stmt->execute([$id]);        
        $row = $stmt->fetch();        
        if (empty($row)) {            
            return null;        
        }
        if ($row['type'] == "book") {            
        $product = new BookProduct(                
            $row['title'],                
            $row['firstname'],                
            $row['mainname'],                
            (float) $row['price'],                
            (int) $row['numpages']            
            );        
        } elseif ($row['type'] == "cd") {            
        $product = new CdProduct(                
            $row['title'],                
            $row['firstname'],                
            $row['mainname'],                
            (float) $row['price'],                
            (int) $row['playlength']            
            );        
        } else {            
            $firstname = (is_null($row['firstname'])) ? "" : $row['firstname'];            
            $product = new ShopProduct(                
                $row['title'],                
                $firstname,                
                $row['mainname'],                
                (float) $row['price']            
            );        
        }        
        $product->setId((int) $row['id']);        
        $product->setDiscount((int) $row['discount']);        
        return $product;    
    }
```

As you can see, the getInstance() method returns a ShopProduct object and, based on a type flag, is smart enough to work out the precise specialization it should instantiate. I have omitted any error handling to keep the example compact. In a real-world version of this, for example, I would not be so trusting as to assume that the provided PDO object was initialized to talk to the correct database. In fact, I probably wrap the PDO with a class that would guarantee this behavior. You can read more about object-oriented coding and databases in Chapter 13.

2『读完后面有关数据库的内容后，再回头来仔细研究下上面的代码。（2020-04-27）』

This method is more useful in a class context than an object context. It lets you convert raw data from the database into an object easily, without requiring that you have a ShopProduct object to start with. The method does not use any instance properties or methods, so there is no reason why it should not be declared static. Given a valid PDO object, I can invoke the method from anywhere in an application:

```php
$dsn = "sqlite:/".__DIR__."/products.db";
$pdo = new \PDO($dsn, null, null);
$pdo->setAttribute(\PDO::ATTR_ERRMODE, \PDO::ERRMODE_EXCEPTION);
$obj = ShopProduct::getInstance(1, $pdo);
```

Methods like this act as「factories」in that they take raw materials (such as row data or configuration information) and use them to produce objects. The term factory is applied to code designed to generate object instances. You will encounter factory examples again in future chapters.

In some ways, of course, this example poses as many problems as it solves. Although I make the ShopProduct::getInstance() method accessible from anywhere in a system without the need for an ShopProduct instance, I also demand that client code provides a PDO object. Where is this to be found? 

And is it really good practice for a parent class to have such intimate knowledge of its children? (Hint: no, it is not.) Problems of this kind—where to acquire key objects and values and how much classes should know about one another—are very common in object-oriented programming. I examine various approaches to object generation in Chapter 9.

1『真实环环相扣，上面的知识点消化需要第 9 章的内容。』

### 4.2 Constant Properties

Some properties should not be changed. The Answer to Life, the Universe, and Everything is 42, and you want it to stay that way. Error and status flags will often be hard-coded into your classes. Although they should be publicly and statically available, client code should not be able to change them.

PHP allows you to define constant properties within a class. Like global constants, class constants cannot be changed once they are set. A constant property is declared with the const keyword. Constants are not prefixed with a dollar sign like regular properties. By convention, they are often named using only uppercase characters:

```php
// listing 04.04
class ShopProduct{    
    const AVAILABLE      = 0;    
    const OUT_OF_STOCK   = 1;   
    // ...
```

Constant properties can contain only primitive values. You cannot assign an object to a constant. Like static properties, constant properties are accessed through the class and not an instance. Just as you define a constant without a dollar sign, no leading symbol is required when you refer to one:

```php
print ShopProduct::AVAILABLE;
```

1『常量属性的方位跟静态属性一样，类名后面加域运算符再加常量名（不需要 \$）。』

Attempting to set a value on a constant once it has been declared will cause a parse error. You should use constants when your property needs to be available across all instances of a class, as well as when the property value needs to be fixed and unchanging.

### 4.3 Abstract Classes

An abstract class cannot be instantiated. Instead it defines (and, optionally, partially implements) the interface for any class that might extend it. You define an abstract class with the abstract keyword. Here I redefine the ShopProductWriter class I created in the previous chapter, this time as an abstract class:

```php
// listing 04.05
abstract class ShopProductWriter {    
    protected $products = [];
    public function addProduct(ShopProduct $shopProduct)    {        
        $this->products[] = $shopProduct;    
    }
}
```

You can create methods and properties as normal, but any attempt to instantiate an abstract object in this way will cause an error:

```php
$writer = new ShopProductWriter();
```

You can see the error in this output:

    Error: Cannot instantiate abstract class popp\ch04\batch03\ShopProductWriter

1『抽象类不能实例化，它是用来定义接口供其他类继承用的。抽象类里定义的抽象方法不能有「实现」，所以定义的时候没有函数体，跟调用的形式一样。关键是继承它的子类一定在子类里实现这个抽象方法。』

In most cases, an abstract class will contain at least one abstract method. These are declared, once again, with the abstract keyword. An abstract method cannot have an implementation. You declare it in the normal way, but end the declaration with a semicolon rather than a method body. Here I add an abstract write() method to the ShopProductWriter class:

```php
abstract class ShopProductWriter {    
    protected $products = [];
    public function addProduct(ShopProduct $shopProduct)    {        
        $this->products[]=$shopProduct;    
    }
    abstract public function write();
}
```

In creating an abstract method, you ensure that an implementation will be available in all concrete child classes, but you leave the details of that implementation undefined.

Assume I were to create a class derived from ShopProductWriter that does not implement the write() method, as in this example:

```php
class ErroredWriter extends ShopProductWriter{}
```

I would face the following error:

    PHP Fatal error:  Class ErroredWriter contains 1 abstract method and must therefore be declared abstract or implement the remaining methods (ShopProductWriter::write) in...

So any class that extends an abstract class must implement all abstract methods or itself be declared abstract. An extending class is responsible for more than simply implementing an abstract method. In doing so, it must reproduce the method signature. This means that the access control of the implementing method cannot be stricter than that of the abstract method. The implementing method should also require the same number of arguments as the abstract method, reproducing any class type hinting. Here are two implementations of ShopProductWriter:

```php
// listing 04.06
class XmlProductWriter extends ShopProductWriter{

    public function write()    {        
        $writer = new \XMLWriter();        
        $writer->openMemory();        
        $writer->startDocument('1.0', 'UTF-8');        
        $writer->startElement("products");        
        foreach ($this->products as $shopProduct) {            
            $writer->startElement("product");            
            $writer->writeAttribute("title", $shopProduct->getTitle());            
            $writer->startElement("summary");            
            $writer->text($shopProduct->getSummaryLine());            
            $writer->endElement(); // summary            
            $writer->endElement(); // product        
        }        
        $writer->endElement(); // products        
        $writer->endDocument();        
        print $writer->flush();    
    }
}

// listing 04.07

class TextProductWriter extends ShopProductWriter {    
    public function write()    {        
        $str = "PRODUCTS:\n";        
        foreach ($this->products as $shopProduct) {            
            $str .= $shopProduct->getSummaryLine()."\n";        
        }        
        print $str;    
    }
}
```

I create two classes, each with its own implementation of the write() method. The first outputs XML and the second outputs text. A method that requires a ShopProductWriter object will not know which of these two classes it is receiving, but it can be absolutely certain that a write() method is implemented. Note that I don’t test the type of \$products before treating it as an array. This is because this property is initialized as an empty array in the ShopProductWriter.

### 4.4 Interfaces

Although abstract classes let you provide some measure of implementation, interfaces are pure templates. An interface can only define functionality; it can never implement it. An interface is declared with the interface keyword. It can contain properties and method declarations but not method bodies. Here’s an interface:

1『接口才是纯模板，它只定义函数，而且这个函数没函数体。』

```php
// listing 04.08
interface Chargeable {    
    public function getPrice(): float;
}
```

As you can see, an interface looks very much like a class. Any class that incorporates this interface commits to implementing all the methods it defines, or it must be declared abstract. A class can implement an interface using the implements keyword in its declaration. Once you have done this, the process of implementing an interface is the same as extending an abstract class that contains only abstract methods. Now I will make the ShopProduct class implement Chargeable:

1『一个接口的实现过程，如同继承一个只包含抽象方法的抽象类。下面实现接口的例子很清楚了，相当于在定义接口的函数语句后面直接加上函数体。』

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

ShopProduct already had a getPrice() method, so why might it be useful to implement the Chargeable interface? Once again, the answer has to do with types. An implementing class takes on the type of the class it extends and the interface that it implements. This means that the CdProduct class belongs to the following:

1『

上面说了接口的用途，应该是跟类型有关，目前没弄明白。目前知道的用途：1）一个类只能继承一个基类，但可以实现多个接口，没实现一个接口对应着一个「type」。2）跟 traits 结合起来用。（2020-04-27）

回复：

As we have seen, interfaces help you manage the fact that, like Java, PHP does not support multiple inheritance. In other words, a class in PHP can only extend a single parent. However, you can make a class promise to implement as many interfaces as you like; for each interface it implements, the class takes on the corresponding type. So interfaces provide types without implementation. 

』

```
CdProduct
ShopProduct
Chargeable
```

This can be exploited by client code. To know an object’s type is to know its capabilities. Consider this method:

```php
public function cdInfo(CdProduct $prod)    {        
    // ...    
}
```

The method knows that the \$prod object has a getPlayLength() method in addition to all the methods defined in the ShopProduct class and Chargeable interface. Passed the same object, the method knows that \$prod supports all the methods in ShopProduct:

```php
public function addProduct(ShopProduct $prod)    {
     // ...    
}
```

Without further testing, however, the method will know nothing of the getPlayLength() method. Once again, passed the same CdProduct object, the method knows nothing at all of the ShopProduct or CdProduct types:

```php
public function addChargeableItem(Chargeable $item)    {        
    //...    
}
```

However, this method is only concerned with whether the \$item argument contains a getPrice() method. Because any class can implement an interface (in fact, a class can implement any number of interfaces), interfaces effectively join types that are otherwise unrelated. I might define an entirely new class that implements Chargeable:

```php
class Shipping implements Chargeable{    
    public function getPrice(): float    {        
        //...    
    }
}
```

I can pass a Shipping object to the addChargeableItem method just as I can pass it a ShopProduct object. The important thing to a client working with a Chargeable object is that it can call a getPrice() method. Any other available methods are associated with other types, whether through the object’s own class, a superclass, or another interface. These are irrelevant to the client.

A class can both extend a superclass and implement any number of interfaces. The extends clause should precede the implements clause:

```php
class Consultancy extends TimedService implements Bookable, Chargeable {    
    // ...
}
```

1『好强大，继承和接口实现同时进行。』

Notice that the Consultancy class implements more than one interface. Multiple interfaces follow the implements keyword in a comma-separated list. PHP only supports inheritance from a single parent, so the extends keyword can precede a single class name only.

### 4.5 Traits

As we have seen, interfaces help you manage the fact that, like Java, PHP does not support multiple inheritance. In other words, a class in PHP can only extend a single parent. However, you can make a class promise to implement as many interfaces as you like; for each interface it implements, the class takes on the corresponding type. So interfaces provide types without implementation. But what if you want to share an implementation across inheritance hierarchies? PHP 5.4 introduced traits, and these let you do just that.

1『 traits 的作用是为了：share an implementation across inheritance hierarchies. 可以当作类的组件模块，在类的定义里使用 use 关键词调用 trait。』

A trait is a class-like structure that cannot itself be instantiated but can be incorporated into classes. Any methods defined in a trait become available as part of any class that uses it. A trait changes the structure of a class, but doesn’t change its type. Think of traits as includes for classes. Let’s look at why a trait might be useful.

#### 4.5.1 A Problem for Traits to Solve

Here is a version of the ShopProduct class with a calculateTax() method:

```php
// listing 04.10
class ShopProduct {    
    private $taxrate = 17;
    // ...

    public function calculateTax(float $price): float    {        
        return (($this->taxrate / 100) * $price);    
    }
}

// listing 04.11
$p = new ShopProduct("Fine Soap", "", "Bob's Bathroom", 1.33);
print $p->calculateTax(100) . "\n";
```

The calculateTax() method accepts a \$price argument and calculates a sales tax amount based on the private \$taxrate property. Of course, a subclass gains access to calculateTax(). But what about entirely different class hierarchies? Imagine a class named UtilityService, which inherits from another class, Service. If UtilityService needs to use an identical routine, I might find myself duplicating calculateTax() in its entirety:

```php
abstract class Service {    
    // service oriented stuff
}

class UtilityService extends Service {    
    private $taxrate = 17;
    function calculateTax(float $price): float    {        
        return ( ( $this->taxrate/100 ) * $price );    
    }
}

$u = new UtilityService();
print $u->calculateTax(100)."\n";
```

#### 4.5.2 Defining and Using a Trait

One of the core object-oriented design goals I will cover in this book is the removal of duplication. As you will see in Chapter 11, one solution to this kind of duplication is to factor it out into a reusable strategy class. Traits provide another approach—less elegant, perhaps, but certainly effective. Here I declare a single trait that defines a calculateTax() method, and then I include it in both ShopProduct and UtilityService:

```php
// listing 04.12
trait PriceUtilities {    
    private $taxrate = 17;
    public function calculateTax(float $price): float    {        
        return (($this->taxrate / 100) * $price);    
    }
    // other utilities
}

// listing 04.13
class ShopProduct {    
    use PriceUtilities;
}

// listing 04.14
abstract class Service {    
    // service oriented stuff
}

// listing 04.15
class UtilityService extends Service {    
    use PriceUtilities;
}

// listing 04.16
$p = new ShopProduct();
print $p->calculateTax(100) . "\n";
$u = new UtilityService();
print $u->calculateTax(100) . "\n";
```

I declare the PriceUtilities trait with the trait keyword. The body of a trait looks very similar to that of a class. It is simply a set of methods and properties collected within braces. Once I have declared it, I can access the PriceUtilities trait from within my classes. I do this with the use keyword followed by the name of the trait I wish to incorporate. So having declared and implemented the calculateTax() method in a single place, I go ahead and incorporate it into both the ShopProduct and the UtilityService classes.

#### 4.5.3 Using More than One Trait

You can include multiple traits in a class by listing each one after the use keyword, separated by commas. In this example, I define and apply a new trait, IdentityTrait, keeping my original PriceUtilities trait:

```php
// listing 04.17
trait IdentityTrait {    
    public function generateId(): string    {        
        return uniqid();    
    }
}

// listing 04.18
class ShopProduct {    
    use PriceUtilities, IdentityTrait;
}

// listing 04.19
$p = new ShopProduct();
print $p->calculateTax(100) . "\n";print $p->generateId() . "\n";
```

By applying both PriceUtilities and IdentityTrait with the use keyword, I make the calculateTax() and the generateId() methods available to the ShopProduct class. This means the class offers both the calculateTax() and generateId() methods.

Note: the IdentityTrait trait provides the generateId() method. In fact, a database often generates identifiers for objects, but you might switch in a local implementation for testing purposes. You can find out more about objects, databases, and unique identifiers in Chapter 12, which covers the Identity Map pattern. You can learn more about testing and mocking in Chapter 18.

#### 4.5.4 Combining Traits and Interfaces

Although traits are useful, they don’t change the type of the class to which they are applied. So when you apply the IdentityTrait trait to multiple classes, they won’t share a type that could be hinted for in a method signature. Luckily, traits play well with interfaces. I can define an interface that requires a generateId() method, and then declare that ShopProduct implements it:

```php
// listing 04.20
interface IdentityObject {    
    public function generateId(): string;
}

// listing 04.21
trait IdentityTrait {    
    public function generateId(): string    {        
        return uniqid();    
    }
}

// listing 04.22
class ShopProduct implements IdentityObject {    
    use PriceUtilities, IdentityTrait;
}
```

As before, ShopProduct uses the IdentityTrait trait. However, the method this imports, generateId() now also fulfills a commitment to the IdentityObject interface. This means that we can pass ShopProduct objects to methods and functions that use type hinting to demand IdentityObject instances, like this:

```php
// listing 04.23    
public static function storeIdentityObject(IdentityObject $idobj)    {        
    // do something with the IdentityObject    
}

// listing 04.24$p = new ShopProduct();
self::storeIdentityObject($p);
print $p->calculateTax(100) . "\n";
print $p->generateId() . "\n";
```

#### 4.5.5 Managing Method Name Conflicts with insteadof

The ability to combine traits is a nice feature, but sooner or later conflicts are inevitable. Consider what would happen, for example, if I were to use two traits that provide a calculateTax() method:

```php
// listing 04.25
trait TaxTools {    
    function calculateTax(float $price): float    {        
        return 222;    
    }
}

// listing 04.26
trait PriceUtilities {    
    private $taxrate = 17;
    public function calculateTax(float $price): float    {
        return (($this->taxrate / 100) * $price);    
    }
    // other utilities
}

// listing 04.27
class UtilityService extends Service {    
    use PriceUtilities, TaxTools;
}

// listing 04.28
$u = new UtilityService();
print $u->calculateTax(100) . "\n";
```

Because I have included two traits that contain calculateTax() methods, PHP is unable to work out which should override the other. The result is a fatal error:

    PHP Fatal error:  Trait method calculateTax has not been applied, because thereare collisions with other trait methods on...

To fix this problem, I can use the insteadof keyword. Here’s how:

```php
// listing 04.29
class UtilityService extends Service {    
    use PriceUtilities, TaxTools {        
        TaxTools::calculateTax insteadof PriceUtilities;    
    }
}

// listing 04.30
$u = new UtilityService();
print $u->calculateTax(100) . "\n";
```

In order to apply further directives to a use statement, I must first add a body. I do this with opening and closing braces. Within this block, I use the insteadof operator. This requires a fully qualified method reference (i.e., one that identifies both the trait and the method names, separated by a scope resolution operator) on the left-hand side. On the right-hand side, insteadof requires the name of the trait whose equivalent method should be overridden:

```php
TaxTools::calculateTax insteadof PriceUtilities;
```

The preceding snippet means,「Use the calculateTax() method of TaxTools instead of the method of he same name in PriceUtilities.」So when I run this code, I get the dummy output I planted in TaxTools::calculateTax():

    222

#### 4.5.6 Aliasing overridden trait methods

We have seen that you can use insteadof to disambiguate between methods. What do you do, though, if you want to then access the overridden method? The as operator allows you to alias trait methods. Once again, the as operator requires a full reference to a method on its left-hand side. On the right-hand side of the operator, you should put the name of the alias. So here, for example, I reinstate the calculateTax() method of the PriceUtilities trait using the new name basicTax():

```php
// listing 04.31
class UtilityService extends Service {
    use PriceUtilities, TaxTools {        
    TaxTools::calculateTax insteadof PriceUtilities;        
    PriceUtilities::calculateTax as basicTax;    
    }
}

// listing 04.32
$u = new UtilityService();
print $u->calculateTax(100) . "\n";
print $u->basicTax(100) . "\n";
```

This gives the following output:

    22217

So PriceUtilities::calculateTax() has been resurrected as part of the UtilityService class under the name basicTax(). 

Note: Where a method name clashes between traits, it is not enough to alias one of the method names in the use block. You must first determine which method supercedes the other using the insteadof operator. then you can reassign the discarded method a new name with the as operator.

1『只是用别名是没用的，必须先用 insteadof 语句确定默认哪个方法。』

Incidentally, you can also use method name aliasing where there is no name clash. You might, for example, want to use a trait method to implement an abstract method signature declared in a parent class or in an interface.

#### 4.5.7 Using static methods in traits

Most of the examples you have seen so far could use static methods because they do not store instance data. There’s nothing complicated about placing a static method in a trait. Here I change the PriceUtilities::\$taxrate property and the PriceUtilities::calculateTax() methods so that they are static:

```php
// listing 04.33
trait PriceUtilities {
    private static $taxrate = 17;
    public static function calculateTax(float $price): float    {        
        return ((self::$taxrate / 100) * $price);    
    }
    // other utilities
}

// listing 04.34
class UtilityService extends Service {    
    use PriceUtilities;
}

// listing 04.35
$u = new UtilityService();
print $u::calculateTax(100) . "\n";
```

As you might expect, this script outputs the following:

    17

So, static methods are declared in traits and accessed via the host class in the normal way.

#### 4.5.8 Accessing Host Class Properties

You might assume that static methods are really the only way to go as far as traits are concerned. Even trait methods that are not declared static are essentially static in nature, right? Well, wrong, in fact—you can access properties and methods in a host class:

```php
// listing 04.36
trait PriceUtilities {    
    function calculateTax(float $price): float    {        
        // is this good design?        
        return (($this->taxrate / 100) * $price);    
    }
    // other utilities
}

// listing 04.37
class UtilityService extends Service {    
    public $taxrate = 17;    
    use PriceUtilities;
}

// listing 04.38
$u = new UtilityService();
print $u->calculateTax(100) . "\n";
```

In the preceding code, I amend the PriceUtilities trait so that it accesses a property in its host class. If you think that this is bad design, you’re right. It’s spectacularly bad design. Although it’s useful for the trait to access data set by its host class, there is nothing to require the UtilityService class to actually provide a \$taxrate property. Remember that traits should be usable across many different classes. What is the guarantee or even the likelihood that any host classes will declare a \$taxrate?

On the other hand, it would be great to be able to establish a contract that says, essentially,「If you use this trait, then you must provide it certain resources.」In fact, you can achieve exactly this effect. Traits support abstract methods.

1『使用 traits 要注意的一点是「Traits support abstract methods」，上面作者表达的注意事项目前没弄透。（2020-04-27）』

#### 4.5.9 Defining Abstract Methods in Traits

You can define abstract methods in a trait in just the same way you would in a class. When a trait is used by a class, it takes on the commitment to implement any abstract methods it declares. Armed with this knowledge, I can reimplement my previous example so that the trait forces the using class to provide tax rate information:

```php
// listing 04.39
trait PriceUtilities {    
    function calculateTax(float $price): float    {        
        // better design.. we know getTaxRate() is implemented        
        return (($this->getTaxRate() / 100) * $price);    
    }
    abstract function getTaxRate(): float;    // other utilities
}

// listing 04.40
class UtilityService extends Service {    
    use PriceUtilities;
    public function getTaxRate(): float    {        
        return 17;    
    }
}

// listing 04.41
$u = new UtilityService();
print $u->calculateTax(100) . "\n";
```

By declaring an abstract getTaxRate() method in the PriceUtilities trait, I force the UtilityService class to provide an implementation. Of course, since PHP does not constrain return types, the UtilityService::calculateTax() method cannot be absolutely certain it’s going to get a sane value from getTaxRate(). 

You could overcome this to some extent by writing all sorts of checking routines, but this misses the point. It is probably adequate just to signal to a client coder that she should provide certain information by requiring the implementation of a method or two.

#### 4.5.10 Changing Access Rights to Trait Methods

You can, of course, declare a trait method public, private, or protected. However, you can also change this access from within the class that uses the trait. You have already seen that the as operator can be used to alias a method name. If you use an access modifier on the right-hand side of this operator, it will change the method’s access level rather than its name.

Imagine, for example, you would like to use calculateTax() from within UtilityService, but not make it available to implementing code. Here’s how you would change the use statement:

```php
// listing 04.42
trait PriceUtilities {    
    public function calculateTax(float $price): float    {        
    r   eturn (($this->getTaxRate() / 100) * $price);    
    }    
    public abstract function getTaxRate(): float;    // other utilities
}

// listing 04.43
class UtilityService extends Service {    
    use PriceUtilities {        
        PriceUtilities::calculateTax as private;    
    }
    private $price;
    public function __construct(float $price)    {        
        $this->price = $price;    
    }
    public function getTaxRate(): float    {        
        return 17;    
    }
    public function getFinalPrice(): float    {        
        return ($this->price + $this->calculateTax($this->price));    
    }
}

// listing 04.44$u = new UtilityService(100);
print $u->getFinalPrice() . "\n";
```

I deploy the as operator in conjunction with the private keyword in order to set private access to calculateTax(). This means I can access the method from getFinalPrice(). Here’s an external attempt to access calculateTax():

```php
$u = new UtilityService(100);
print $u->calculateTax()."\n";
```

Unfortunately, this code will generate an error:

    Error: Call to private method popp\ch04\batch06_9\UtilityService::calculateTax() from context ...





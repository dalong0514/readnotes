## 记忆时间

## 0103. Object Basics

This chapter covered a lot of ground, taking a class from an empty implementation through to a fully featured inheritance hierarchy. You took in some design issues, particularly with regard to type and inheritance. You saw PHP’s support for visibility and explored some of its uses. In the next chapter, I will show you more of PHP’s object-oriented features.

Objects and classes lie at the heart of this book and, since the introduction of PHP 5 over a decade ago, they have lain at the heart of PHP, too. In this chapter, I lay down the groundwork for more in-depth coverage of objects and design by examining PHP’s core object-oriented features. If you are new to object-oriented programming, you should read this chapter carefully.

This chapter will cover the following topics: 1) Constructor methods: Automating the setup of your objects. 2) Classes and objects: Declaring classes and instantiating objects. 3) Primitive and class types: Why type matters. 4) Inheritance: Why we need inheritance and how to use it. 5) Visibility: Streamlining your object interfaces and protecting your methods and properties from meddling.

### 3.1 Classes and Objects

The first barrier to understanding object-oriented programming is the strange and wonderful relationship between the class and the object. For many people, it is this relationship that represents the first moment of revelation, the first flash of object-oriented excitement. So let’s not skimp on the fundamentals.

#### 3.1.1 A First Class

Classes are often described in terms of objects. This is interesting, because objects are often described in terms of classes. This circularity can make the first steps in object-oriented programming hard going. Because it’s classes that shape objects, we should begin by defining a class.

In short, a class is a code template used to generate one or more objects. You declare a class with the class keyword and an arbitrary class name. Class names can be any combination of numbers and letters, although they must not begin with a number. The code associated with a class must be enclosed within braces. Here I combine these elements to build a class:

```php
// listing 03.01

class ShopProduct
{    
    // class body
}
```

The ShopProduct class in the example is already a legal class, although it is not terribly useful yet. I have done something quite significant, however. I have defined a type; that is, I have created a category of data that I can use in my scripts. The power of this should become clearer as you work through the chapter.

#### 3.1.2 A First Object (or Two)

If a class is a template for generating objects, it follows that an object is data that has been structured according to the template defined in a class. An object is said to be an instance of its class. It is of the type defined by the class. I use the ShopProduct class as a mold for generating ShopProduct objects. To do this, I need the new operator. The new operator is used in conjunction with the name of a class, like this:

1『 php 里类实例化为对象，用 new 操作符。』

```php
// listing 03.02

$product1 = new ShopProduct();
$product2 = new ShopProduct();
```

The new operator is invoked with a class name as its only operand and returns an instance of that class; in our example, it generates a ShopProduct object.

I have used the ShopProduct class as a template to generate two ShopProduct objects. Although they are functionally identical (that is, empty), \$product1 and \$product2 are different objects of the same type generated from a single class. If you are still confused, try this analogy. Think of a class as a cast in a machine that makes plastic ducks. 

1『体现了对象三元素之一的「唯一标识性」，另外 2 个是状态和行为。』

Our objects are the ducks that this machine generates. The type of thing generated is determined by the mold from which it is pressed. The ducks look identical in every way, but they are distinct entities. In other words, they are different instances of the same type. The ducks may even have their own serial numbers to prove their identities. Every object that is created in a PHP script is also given its own unique identifier. (Note that the identifier is unique for the life of the object; that is, PHP reuses identifiers, even within a process).  I can demonstrate this by printing out the \$product1 and \$product2 objects:

```php
// listing 03.03

var_dump($product1);
var_dump($product2);
```

Executing these functions produces the following output:

```
object(popp\ch03\batch01\ShopProduct)#235 (0) {}
object(popp\ch03\batch01\ShopProduct)#234 (0) {}
```

Note: in ancient versions of php (up to version 5.1), you could print an object directly. this casted the object to a string containing the object’s iD. From php 5.2 onward, the language no longer supports this magic, and any attempt to treat an object as a string now causes an error unless a method named \_\_toString() is defined in the object’s class. I look at methods later in this chapter, and I cover \_\_toString() in Chapter 4「advanced Features.」

By passing the objects to var\_dump(), I extract useful information including, after the hash sign, each object’s internal identifier. In order to make these objects more interesting, I can amend the ShopProduct class to support special data fields called properties.

### 3.2 Setting Properties in a Class

Classes can define special variables called properties. A property, also known as a member variable, holds data that can vary from object to object. So in the case of ShopProduct objects, you may wish to manipulate title and price fields, for example.

A property in a class looks similar to a standard variable except that, in declaring a property, you must precede the property variable with a visibility keyword. This can be public, protected, or private, and it determines the scope from which the property can be accessed. 

Note: scope refers to the function or class context in which a variable has meaning (it refers in the same way to methods, which I will cover later in this chapter). so a variable defined in a function exists in local scope, and a variable defined outside of the function exists in global scope. as a rule of thumb, it is not possible to access data defined in a scope that is more local than the current one. so if you define a variable inside a function, you cannot later access it from outside that function. Objects are more permeable than this, in that some object variables can sometimes be accessed from other contexts. Which variables can be accessed and from what context is determined by the public, protected, and private keywords, as you shall see.

I will return to these keywords and the issue of visibility later in this chapter. For now, I will declare some properties using the public keyword:

```php
// listing 03.04

class ShopProduct{    
    public $title = "default product";    
    public $producerMainName = "main name";    
    public $producerFirstName = "first name";    
    public $price  = 0;
}
```

As you can see, I set up four properties, assigning a default value to each of them. Any objects I instantiate from the ShopProduct class will now be prepopulated with default data. The public keyword in each property declaration ensures that I can access the property from outside of the object context.

You can access property variables on an object-by-object basis using the characters '->' (the object operator) in conjunction with an object variable and property name, like this:

```php
// listing 03.05

$product1 = new ShopProduct();
print $product1->title;
```

    default product

Because the properties are defined as public, you can assign values to them just as you can read them, replacing any default value set in the class:

```php
// listing 03.06

$product1 = new ShopProduct();
$product2 = new ShopProduct();
$product1->title="My Antonia";
$product2->title="Catch 22";
```

By declaring and setting the \$title property in the ShopProduct class, I ensure that all ShopProduct objects have this property when first created. This means code that uses this class can work with ShopProduct objects based on that assumption. Because I can reset it, though, the value of \$title may vary from object to object.

Note: Code that uses a class, function, or method is often described as the class’s, function’s, or method’s client or as client code. You will see this term frequently in the coming chapters.

In fact, PHP does not force us to declare all our properties in the class. You could add properties dynamically to an object, like this:

```php
// listing 03.07

$product1->arbitraryAddition = "treehouse";
```

However, this method of assigning properties to objects is not considered good practice in object-oriented programming. Why is it bad practice to set properties dynamically? When you create a class you define a type. You inform the world that your class (and any object instantiated from it) consists of a particular set of fields and functions. If your ShopProduct class defines a \$title property, then any code that works with ShopProduct objects can proceed on the assumption that a \$title property will be available. There can be no guarantees about properties that have been dynamically set, though.

1『这不是跟 JS 一样，可以动态添加属性了嘛，赞。但作者却不建议，理由是不好控制。而且可能误加不想要的属性，比如属性名字打错了（后面有例子）。』

My objects are still cumbersome at this stage. When I need to work with an object’s properties, I must currently do so from outside the object. I reach in to set and get property information. Setting multiple properties on multiple objects will soon become a chore:

```php
// listing 03.08

$product1 = new ShopProduct();
$product1->title = "My Antonia";
$product1->producerMainName  = "Cather";
$product1->producerFirstName = "Willa";
$product1->price = 5.99;
```

I work once again with the ShopProduct class, overriding all the default property values one by one until I have set all product details. Now that I have set some data, I can also access it:

```php
// listing 03.09

print "author: {$product1->producerFirstName} "    
    . "{$product1->producerMainName}\n";
```

This outputs the following:

    author: Willa Cather

There are a number of problems with this approach to setting property values. Because PHP lets you set properties dynamically, you will not get warned if you misspell or forget a property name. For example, assume I want to type this line:

```php
$product1->producerMainName  = "Cather";
```

Unfortunately, I mistakenly type it like this:

```php
$product1->producerSecondName  = "Cather";
```

As far as the PHP engine is concerned, this code is perfectly legal, and I would not be warned. When I come to print the author’s name, though, I will get unexpected results.

Another problem is that my class is altogether too relaxed. I am not forced to set a title, a price, or producer names. Client code can be sure that these properties exist, but is likely to be confronted with default values as often as not. Ideally, I would like to encourage anyone who instantiates a ShopProduct object to set meaningful property values.

Finally, I have to jump through hoops to do something that I will probably want to do quite often. As we have seen, printing the full author name is a tiresome process. It would be nice to have the object handle such drudgery on my behalf. All of these problems can be addressed by giving the ShopProduct object its own set of functions that can be used to manipulate property data from within the object context.

1『对象里的成员方法，就是为了解决上面场景遇到的问题而生的，其可以在对象内部操作对象里的数据属性。数据属性声明为私有，在外面只能通过调用成员方法来操作对象里的数据属性，这就解决了在外面误改对象数据属性的可能性。』

### 3.3 Working with Methods

Just as properties allow your objects to store data, methods allow your objects to perform tasks. Methods are special functions declared within a class. As you might expect, a method declaration resembles a function declaration. The function keyword precedes a method name, followed by an optional list of argument variables in parentheses. The method body is enclosed by braces:

```php
public function myMethod($argument, $another)    
{        
    // ...    
}
```

Unlike functions, methods must be declared in the body of a class. They can also accept a number of qualifiers, including a visibility keyword. Like properties, methods can be declared public, protected, or private. By declaring a method public, you ensure that it can be invoked from outside of the current object. If you omit the visibility keyword in your method declaration, the method will be declared public implicitly. It is considered good practice, however, to declare visibility explicitly for all methods (I will return to method modifiers later in the chapter).

```php
// listing 03.10

class ShopProduct
{

    public $title = "default product";    
    public $producerMainName = "main name";    
    public $producerFirstName = "first name";    
    public $price = 0;

    public function getProducer()    {        
    return $this->producerFirstName . " "            
        . $this->producerMainName;    
    }
}
```

In most circumstances, you will invoke a method using an object variable in conjunction with the object operator, ->, and the method name. You must use parentheses in your method call as you would if you were calling a function (even if you are not passing any arguments to the method):

I add the getProducer() method to the ShopProduct class. Notice that I declare getProducer() public, which means it can be called from outside the class. I introduce a feature in this method’s body. The \$this pseudo-variable is the mechanism by which a class can refer to an object instance. If you find this concept hard to swallow, try replacing \$this with the phrase「the current instance.」Consider the following statement:

```php
$this->producerFirstName
```

This translates to the following: the \$producerFirstName property of the current instance. So the getProducer() method combines and returns the \$producerFirstName and \$producerMainName properties, saving me from the chore of performing this task every time I need to quote the full producer name. This has improved the class a little. I am still stuck with a great deal of unwanted flexibility, though. 

I rely on the client coder to change a ShopProduct object’s properties from their default values. This is problematic in two ways. First, it takes five lines to properly initialize a ShopProduct object, and no coder will thank you for that. Second, I have no way of ensuring that any of the properties are set when a ShopProduct object is initialized. What I need is a method that is called automatically when an object is instantiated from a class.

#### 3.3.1 Creating a Constructor Method

A constructor method is invoked when an object is created. You can use it to set things up, ensuring that essential properties are assigned values and any necessary preliminary work is completed.

Note: in versions previous to php 5, a constructor method took on the name of the class that enclosed it. so the ShopProduct class would use a ShopProduct() method as its constructor. this no longer works in all circumstances and was deprecated as of php 7. Name your constructor method \_\_construct().

Note that the method name begins with two underscore characters. You will see this naming convention for many other special methods in PHP classes. Here I define a constructor for the ShopProduct class:

```php
// listing 03.12

class ShopProduct
{    
    public $title;    
    public $producerMainName;    
    public $producerFirstName;    
    public $price = 0;

    public function __construct(        
        $title,        
        $firstName,        
        $mainName,        
        $price    ) {        
        $this->title = $title;        
        $this->producerFirstName = $firstName;        
        $this->producerMainName = $mainName;        
        $this->price = $price;    
        }

    public function getProducer()    {        
    return $this->producerFirstName . " "            
        . $this->producerMainName;    
    }
}
```

1『注意，构造函数里的「\$this->title」，title 前没有 \$。』

Once again, I gather functionality into the class, saving effort and duplication in the code that uses it. The \_\_construct() method is invoked when an object is created using the new operator:

Any arguments supplied are passed to the constructor. So in my example, I pass the title, the first name, the main name, and the product price to the constructor. The constructor method uses the pseudo-variable \$this to assign values to each of the object’s properties.

Note:  a ShopProduct object is now easier to instantiate and safer to use. instantiation and setup are completed in a single statement. any code that uses a ShopProduct object can be reasonably sure that all its properties are initialized.

This predictability is an important aspect of object-oriented programming. You should design your classes so that users of objects can be sure of their features. One way you can make an object safe is to render predictable the types of data it holds in its properties. One might ensure that a \$name property is always made up of character data, for example. But how can you achieve this if property data is passed in from outside the class? In the next section, I examine a mechanism you can use to enforce object types in method declarations.

1『传参的类型检验很重要。』

1『

在 laravel 里的实现：

```php
<?php

// use APP\ShopProduct;

class ShopProduct {
    public $title = 'default product';
    public $productMainName = 'main name';
    public $productFirstName = 'first name';
    public $price = 0;

    public function __construct(
        $title,
        $firstName,
        $mainName,
        $price) {
        $this->title = $title;
        $this->productMainName = $mainName;
        $this->productFirstName = $firstName;
        $this->price = $price;
    }

    public function getProducer() {
        return $this->productFirstName . ' ' . $this->productMainName;
    }
}

$product = new ShopProduct('testname', 'first', 'main', 'da');  // 这里 price 就传入了一个错误类型字符串
dd($product);
```

』

### 3.4 Arguments and Types

Type determines the way data can be managed in your scripts. You use the string type to display character data, for example, and manipulate such data with string functions. Integers are used in mathematical expressions, Booleans are used in test expressions, and so on. These categories are known as primitive types. On a higher level, though, a class defines a type. A ShopProduct object, therefore, belongs to the primitive type object, but it also belongs to the ShopProduct class type. In this section, I will look at types of both kinds in relation to class methods.

1『 primitive types 类比于 JS 里的 7 大基本语言类型。』

2『Type determines the way data can be managed in your scripts. 做一张金句卡片。』——已完成

Method and function definitions do not necessarily require that an argument should be of a particular type. This is both a curse and a blessing. The fact that an argument can be of any type offers you flexibility. You can build methods that respond intelligently to different data types, tailoring functionality to changing circumstances. This flexibility can also cause ambiguity to creep into code when a method body expects an argument to hold one type but gets another.

在 PHP 中，定义方法和函数时不需要指定参数的数据类型。这既是一种麻烦，也是一种便利。参数可以是任何类型给我们提供了很大的灵活性。你可以创建灵活响应不同数据类型的方法，根据不同的环境调整其功能。但当类方法希望一个参数必须是某种数据类型（而不是其他类型）时，这种灵活性可能会引起代码的歧义。

#### 3.4.1 Primitive Types

PHP is a loosely typed language. This means that there is no necessity for a variable to be declared to hold a particular data type. The variable \$number could hold the value 2 and the string "two" within the same scope. In strongly typed languages, such as C or Java, you must declare the type of a variable before assigning a value to it, and, of course, the value must be of the specified type.

This does not mean that PHP has no concept of type. Every value that can be assigned to a variable has a type. You can determine the type of a variable’s value using one of PHP’s type-checking functions. Table 3-1  lists the primitive types recognized in PHP and their corresponding test functions. Each function accepts a variable or value and returns true if this argument is of the relevant type.

1『表里有检查类型的库函数，基本都是类型名字前面加了个 is\_ ，比如 is\_integer()。』

Checking the type of a variable can be particularly important when you work with method and function arguments.

Primitive Types Matter: An Example. You need to keep a close eye on type in your code. Here’s an example of one of the many type-related problems that you could encounter.

Imagine that you are extracting configuration settings from an XML file. The \<resolvedomains> XML element tells your application whether it should attempt to resolve IP addresses to domain names, a useful but relatively expensive process. Here is some sample XML:

```
<!-- listing 03.14 -->
<settings>    
    <resolvedomains>false</resolvedomains>
</settings>
```

The string "false" is extracted by your application and passed as a flag to a method called outputAddresses(), which displays IP address data. Here is outputAddresses():

```php
// listing 03.15

class AddressManager
{    
    private $addresses = ["209.131.36.159", "216.58.213.174"];

    public function outputAddresses($resolve)    {        
        foreach ($this->addresses as $address) {            
            print $address;            
            if ($resolve) {                
                print " (".gethostbyaddr($address).")";            
            }            
            print "\n";
        }    
    }
}
```

Of course, the AddressManager class could do with some improvement. It’s not very useful to hardcode IP addresses into a class, for example. Nevertheless, the outputAddresses() method loops through the \$addresses array property, printing each element. If the \$resolve argument variable itself resolves to true, the method outputs the domain name, as well as the IP address.

Here’s one approach that uses the settings XML configuration element in conjunction with the AddressManager class. See if you can spot how it is flawed:

```php
// listing 03.16

$settings = simplexml:load_file(__DIR__."/resolve.xml");
$manager = new AddressManager();
$manager->outputAddresses((string)$settings->resolvedomains);
```

The code fragment uses the SimpleXML API to acquire a value for the resolvedomains element. In this example, I know that this value is the text element "false", and I cast it to a string as the SimpleXML documentation suggests I should.

1『因为知道会误传参 "false"，做了相应的处理，如果不知道会误传何种类型呢？』

This code will not behave as you might expect. In passing the string "false" to the outputAddresses() method, I misunderstand the implicit assumption the method makes about the argument. The method is expecting a Boolean value (that is true or false). The string "false" will, in fact, resolve to true in a test. This is because PHP will helpfully cast a nonempty string value to the Boolean true for you in a test context. Consider this code:

```php
if ( "false" ) {    
    // ...
}
```

It is actually equivalent to this:

```php
if ( true ) {   
    // ...
 }
```

There are a number of approaches you might take to fix this. You could make the outputAddresses() method more forgiving, so that it recognizes a string and applies some basic rules to convert it to a Boolean equivalent:

```php
// listing 03.17

public function outputAddresses($resolve)    {        
if (is_string($resolve)) {            
$resolve =               
    (preg_match("/^(false|no|off)$/i", $resolve) ) ? false : true;        
    }        
    // ...    
}
```

There are good design reasons for avoiding an approach like this, however. Generally speaking, it is better to provide a clear and strict interface for a method or function than it is to offer a fuzzily forgiving one. Fuzzy and forgiving functions and methods can promote confusion and thereby breed bugs.

1『相比于对传入的参数先逻辑判断再进行处理，更好的方式是「提供一个清晰、严格的接口」。』

You could take another approach: Leave the outputAddresses() method as it is and include a comment containing clear instructions that the \$resolve argument should contain a Boolean value. This approach essentially tells the coder to read the small print or reap the consequences:

```php
/**     
* Outputs the list of addresses.     
* If $resolve is true then each address will be resolved     
* @param    $resolve    boolean    Resolve the address?     
*/    f

unction outputAddresses($resolve)    
{       
    // ...    
}
```

This is a reasonable approach, assuming your client coders are diligent readers of documentation. Finally, you could make outputAddresses() strict about the type of data it is prepared to find in the \$resolve argument. For primitive types like boolean, there was really only one way to do this prior to the release of PHP 7. You would have to write code to examine incoming data and take some kind of action if it does not match the required type:

```php
function outputAddresses($resolve)    
{        
    if (! is_bool($resolve)) {            
        // do something drastic        
    }        
    //...    
}
```

This approach can be used to force client code to provide the correct data type in the \$resolve argument or to issue a warning.

Note: in the next section,「taking the hint: Object types,」I will describe a much better way of constraining the type of arguments passed to methods and functions. Converting a string argument on the client’s behalf would be friendly but would probably present other problems. in providing a conversion mechanism, you second-guess the context and intent of the client. by enforcing the boolean data type, on the other hand, you leave the client to decide whether to map strings to boolean values and determine which word should map to true or false. the outputAddresses() method, meanwhile, concentrates on the task it is designed to perform. this emphasis on performing a specific task in deliberate ignorance of the wider context is an important principle in object-oriented programming, and I will return to it frequently throughout the book.

1『更好的实现方法在下节「taking the hint: Object types」里，心痒痒啊。』

这种方法强制性要求客户端代码提供正确的数据类型给 Resolve 参数。把字符串参数转化成布尔类型对于客户端代码来说更加友好，但是这可能会引起其他问题。在提供转换方法的情况下，我们需要猜测客户端代码的环境和意图。另一方面，通过强制规定参数为布尔型数据类型客户端代码需要决定是否将字符串映射为布尔值以及哪个单词映射为哪个值。这样，outputaddresses() 方法可以专注于执行它的任务。在面向对象开发中，「专注特定任务，忽略外界上下文」是一个重要的设计原则，我们将在本书中经常提到这一点。

In fact, your strategies for dealing with argument types will depend on the seriousness of any potential bugs on the one hand, and the benefits of flexibility on the other. PHP casts most primitive values for you, depending on context. Numbers in strings are converted to their integer or floating point equivalents when used in a mathematical expression, for example. So your code might be naturally forgiving of type errors. If you expect one of your method arguments to be an array, however, you may need to be more careful. Passing a nonarray value to one of PHP’s array functions will not produce a useful result and could cause a cascade of errors in your method.

1『一定要注意，不要把非数组的数据传入接受数组参数的函数里。』

事实上，采用哪种处理参数类型的策略，取决于任何潜在 bug 的严重程度。通常 PHP 会根据语境自动转换大多数基本数据类型。例如，在数学表达式中，字符串中的数字被转换成相等的整型或浮点型。因此你的代码多半会自然地容忍类型错误。但如果要求方法参数必须是一个数组，就需要更加小心。传递一个非数组值到 PHP 数组函数不会产生有用的结果，还可能会在方法中引起一连串的错误。因此，你需要在检测类型、转换类型和依赖良好清晰的文档（无论决定用哪一种，都应该提供文档）之间仔细权衡。

无论你如何解决这类问题，都要认真思考一件事情：类型处理。PHP 是一种弱类型的语言这使得这件事更加重要。我们不能依靠编译器来防止类型相关的 bug，必须考虑到当非法数据类型的参数传递给方法时，会产生怎样的后果。我们不能完全信任客户端程序员，应该始终考虑如何在方法中处理他们引入的无用信息。

It is likely, therefore, that you will strike a balance among testing for type, converting from one type to another, and relying on good, clear documentation (you should provide the documentation, whatever else you decide to do). 

However you address problems of this kind, you can be sure of one thing—type matters. The fact that PHP is loosely typed makes it all the more important. You cannot rely on a compiler to prevent type-related bugs; you must consider the potential impact of unexpected types when they find their way into your arguments. You cannot afford to trust client coders to read your thoughts, and you should always consider how your methods will deal with incoming garbage.

1『类型检验问题是 php 里是个大问题，同样为弱类型语言的 JS，应该也存在着相同的问题。』

#### 3.4.2 Taking the Hint: Object Types

获得提示：对象类型

Just as an argument variable can contain any primitive type, by default it can contain an object of any type. This flexibility has its uses, but can present problems in the context of a method definition. Imagine a method designed to work with a ShopProduct object:

```php
// listing 03.18

class ShopProductWriter
{    
    public function write($shopProduct)    {        
    $str  = $shopProduct->title . ": "            
        . $shopProduct->getProducer()            
        . " (" . $shopProduct->price . ")\n";        
    print $str;    }
}
```

1『注意，这里 ")\n" 只有用双引号，换行符才生效。』

You can test this class like this:

```php
// listing 03.19

$product1 = new ShopProduct("My Antonia", "Willa", "Cather", 5.99);
$writer = new ShopProductWriter();
$writer->write($product1);
```

This outputs the following:

    My Antonia: Willa Cather (5.99)

The ShopProductWriter class contains a single method, write(). The write() method accepts a ShopProduct object and uses its properties and methods to construct and print a summary string. I used the name of the argument variable, \$shopProduct, as a signal that the method expects a ShopProduct object, but I did not enforce this. That means I could be passed an unexpected object or primitive type and be none the wiser until I begin trying to work with the \$shopProduct argument. By that time, my code may already have acted on the assumption that it has been passed a genuine ShopProduct object.

Note: You might wonder why I didn't add the write() method directly to ShopProduct. the reason lies with areas of responsibility. the ShopProduct class is responsible for managing product data; the ShopProductWriter is responsible for writing it. You will begin to see why this division of labor can be useful as you read this chapter.

1『按业务（功能）划分代码。』

To address this problem, PHP 5 introduced class type declarations (known then as type hints). To add a class type declaration to a method argument, you simply place a class name in front of the method argument you need to constrain. So I can amend the write() method thus:

```php
// listing 03.20

    public function write(ShopProduct $shopProduct)    
    {        
        // ...    
    }
```

Now the write() method will only accept the \$shopProduct argument if it contains an object of type ShopProduct. This snippet tries to call write() with a dodgy object:

```php
// listing 03.21

class Wrong
{
}

$writer = new ShopProductWriter();
$writer->write(new Wrong());
```

Because the write() method contains a class type declaration, passing it a Wrong object causes a fatal error.

    TypeError: Argument 1 passed to ShopProductWriter::write() must be an instance of ShopProduct, instance of Wrong given, called in Runner.php on ...

This saves me from having to test the type of the argument before I work with it. It also makes the method signature much clearer for the client coder. She can see the requirements of the write() method at a glance. She does not have to worry about some obscure bug arising from a type error because the declaration is rigidly enforced.

1『传递给函数的参数，如果类型不对是一个大问题。PHP 5 引入的 type hints 为此而生，在函数传递的参数前面直接指定类型。其他基本类型比如 string 之类的，不知道是否可以指定，待确认。（2020-04-21）回复：标量类型的声明指定是 PHP 7 新增的特性，下面正好有个例子。』

3『「2020121Full-Stack-Vuejs2-R01」

做路由的时候用到这个语法：

```php
Route::get('/listing/{listing}', function(ListingModel $listing) {
    $model = $listing->toArray();
    return view('app', [ 'model' => $model ]);
})
```

』

Even though this automated type checking is a great way of preventing bugs, it is important to understand that type declarations are checked at runtime. This means that a class declaration will only report an error at the moment that an unwanted object is passed to the method. If a call to write() is buried in a conditional clause that only runs on Christmas morning, you may find yourself working the holiday if you haven’t checked your code carefully.

虽然自动类型检查是防止 bug 的极佳途径，但我们要知道类型提示是在运行时才生效的。也就是说，类提示只有在错误的对象被传递给方法时オ会报错。如果对 write() 的调用隐藏在条件子句中（例如只在圣诞节早上才运行），那么如果没有仔细检査代码的话，很难发现错误。

Armed with scalar type declarations, I can add some constraints to the ShopProduct class:

1『标量类型检验没记错的话，应该是 PHP 7 新增的特性，赞！』

```php
// listing 03.22

class ShopProduct
{    
    public $title;    
    public $producerMainName;    
    public $producerFirstName;    
    public $price = 0;

    public function __construct(        
    string $title,        
    string $firstName,        
    string $mainName,        
    float $price    
    ) {        
    $this->title = $title;        
    $this->producerFirstName = $firstName;        
    $this->producerMainName = $mainName;        
    $this->price = $price;    }

    // ...
}
```

With the constructor method shored up in this way, I can be sure that the \$title, \$firstName, \$mainName arguments will always contain string data, and that \$price will contain a float. I can demonstrate this by instantiating ShopProduct with the wrong information:

```php
// listing 03.23

// will fail
$product = new ShopProduct("title", "first", "main", []);
```

I attempt to instantiate a ShopProduct object. I pass three strings to the constructor, but I fail at the final hurdle by passing in an empty array instead of the required float. Thanks to type declarations, PHP won’t let me get away with that:

    TypeError: Argument 4 passed to ShopProduct::__construct() must be of the type float, array given, called in...

By default, PHP will implicitly cast arguments to the required type, where possible. This is an example of the tension between safety and flexibility we encountered earlier. The new implementation of the ShopProduct class, for example, will quietly turn a string into a float for us. So, this instantiation would not fail:

```php
// listing 03.24

$product = new ShopProduct("title", "first", "main", "4.22");
```

Behind the scenes, the string "4.22" becomes the float 4.22. So far, so useful. But think back to the problem we encountered with the AddressManager class. The string "false" was quietly resolving to the Boolean true. By default, this will still happen if I use a bool type declaration in the AddressManager::outputAddresses() method like this:

```php
// listing 03.25

    public function outputAddresses(bool $resolve)    
    {        
        // ...    
    }
```

Now consider a call that passes along a string like this:

```php
// listing 03.26

$manager->outputAddresses("false");
```

Because of implicit casting, it is functionally identical to one that passes the Boolean value true. You can make scalar type declarations strict, although only on a file by file basis. Here, I turn on strict type declarations and call outputAddresses() with a string once again:

```php
// listing 03.27

declare(strict_types=1);
$manager->outputAddresses("false");
```

1『原来可以自己指定是否采用严格模式。』

Because I declare strict typing, this call causes a TypeError to be thrown:

    TypeError: Argument 1 passed to AddressManager::outputAddresses() must be of the type boolean, string given, called in ...

Note:  a strict\_types declaration applies to the file from which a call is made, and not to the file in which a function or method is implemented. so it’s up to client code to enforce strictness.

You may need to make an argument optional, but nonetheless constrain its type if it is provided. You can do this by providing a default value:

```php
// listing 03.28

class ConfReader{

    public function getValues(array $default = null)    
    {        
        $values = [];

        // do something to get values
        // merge the provided defaults (it will always be an array)
        $values = array_merge($default, $values);        
        return $values;    
    }
}
```

In Table 3-2, I list the type declarations supported by PHP. 1) array. An array. Can default to null or an array. 2) int. An integer Can default to null or an integer. 3) float. A floating point number (a number with a decimal point). An integer will be accepted—even with strict mode enabled. Can default to null, a float, or an integer. 4) callable. Callable code (such as an anonymous function). Can default to null. 5) bool. A Boolean. Can default to null or a Boolean. 6) string. Character data. Can default to null or a string. 7) self. A reference to the containing class. 8) [a class type]. The type of a class or interface. Can default to null.

When I described class type declarations, I implied that types and classes are synonymous. There is a key difference between the two, however. When you define a class, you also define a type, but a type can describe an entire family of classes. The mechanism by which different classes can be grouped together under a type is called inheritance. I discuss inheritance in the next section.

1『

laravel 里代码实现：

```php
<?php
// declare(strict_types=1);  // 显式声明类型检查为严格模式
// use APP\ShopProduct;

class ShopProduct {
    public $title = 'default product';
    public $productMainName = 'main name';
    public $productFirstName = 'first name';
    public $price = 0;

    public function __construct(
        string $title,
        string $firstName,
        string $mainName,
        float $price) {
        $this->title = $title;
        $this->productMainName = $mainName;
        $this->productFirstName = $firstName;
        $this->price = $price;
    }

    public function getProducer() {
        return $this->productFirstName . ' ' . $this->productMainName;
    }
}

class ShopProductWriter {
    public function write(ShopProduct $shopProduct) {
        $str = $shopProduct->title . ': '
            . $shopProduct->getProducer()
            . '(' . $shopProduct->price . ")\n";
        print $str;
    }
}

$product = new ShopProduct('My Antonia', 'Willa', 'Cather', '6.6');
$write = new ShopProductWriter();
$write->write($product);
```

』

### 3.5 Inheritance

Inheritance is the means by which one or more classes can be derived from a base class. A class that inherits from another is said to be a subclass of it. This relationship is often described in terms of parents and children. A child class is derived from and inherits characteristics from the parent. These characteristics consist of both properties and methods. The child class will typically add new functionality to that provided by its parent (also known as a superclass); for this reason, a child class is said to extend its parent. Before I dive into the syntax of inheritance, I’ll examine the problems it can help you to solve. 

#### 3.5.1 The Inheritance Problem

Look again at the ShopProduct class. At the moment, it is nicely generic. It can handle all sorts of products:

```php
// listing 03.29

$product1 = new ShopProduct("My Antonia", "Willa", "Cather", 5.99);
$product2 = new ShopProduct(    "Exile on Coldharbour Lane",    "The", "Alabama 3",    10.99);
print "author: " . $product1->getProducer() . "\n";
print "artist: " . $product2->getProducer() . "\n";
```

Here’s the output:

```
author: Willa Cather
artist: The Alabama 3
```

Separating the producer name into two parts works well with both books and CDs. I want to be able to sort on「Alabama 3」and「Cather」, not on「The」and「Willa」. Laziness is an excellent design strategy, so there is no need to worry about using ShopProduct for more than one kind of product at this stage.

If I add some new requirements to my example, however, things rapidly become more complicated. Imagine, for example, that you need to represent data specific to books and CDs. For CDs, you must store the total playing time; for books, the total number of pages. There could be any number of other differences, but this will serve to illustrate the issue.

How can I extend my example to accommodate these changes? Two options immediately present themselves. First, I could throw all the data into the ShopProduct class. Second, I could split ShopProduct into two separate classes. 

Let’s examine the first approach. Here, I combine CD- and book-related data in a single class:

```php
// listing 03.30

class ShopProduct{    
    public $numPages;    
    public $playLength;    
    public $title;    
    public $producerMainName;    
    public $producerFirstName;    
    public $price;

    public function __construct(        
        string $title,        
        string $firstName,        
        string $mainName,        
        float $price,        
        int $numPages = 0,        
        int $playLength = 0    ) {        
        $this->title = $title;        
        $this->producerFirstName = $firstName;        
        $this->producerMainName  = $mainName;        
        $this->price = $price;        
        $this->numPages = $numPages;        
        $this->playLength = $playLength;    
        }

    public function getNumberOfPages()    {        
        return $this->numPages;    
    }

    public function getPlayLength()    {        
        return $this->playLength;   
    }

    public function getProducer()    {        
        return $this->producerFirstName . " "            
            . $this->producerMainName;    
    }
}
```

I have provided method access to the \$numPages and \$playLength properties to illustrate the divergent forces at work here. An object instantiated from this class will include a redundant method and, for a CD, must be instantiated using an unnecessary constructor argument: a CD will store information and functionality relating to book pages, and a book will support play-length data. This is probably something you could live with right now. But what would happen if I added more product types, each with its own methods, and then added more methods for each type? Our class would become increasingly complex and hard to manage.

So forcing fields that don’t belong together into a single class leads to bloated objects with redundant properties and methods.

因此强行将不同类的字段合并到一个类中，会导致对象臃肿，产生冗余的属性和方法。

The problem doesn’t end with data, either. I run into difficulties with functionality as well. Consider a method that summarizes a product. The sales department has requested a clear summary line for use in invoices. They want me to include the playing time for CDs and a page count for books, so I will be forced to provide different implementations for each type. I could try using a flag to keep track of the object’s format. Here’s an example:

1『看到这句「I could try using a flag to keep track of the object’s format」以及下面条件语句的实现，突然领悟到「重构」里，用对象的多态取代条件语句的意义。（2020-06-18）』

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

In order to set the \$type property, I could test the \$numPages argument to the constructor. Still, once again, the ShopProduct class has become more complex than necessary. As I add more differences to my formats, or add new formats, these functional differences will become even harder to manage. Perhaps I should try another approach to this problem.

1『上面可以说是明明白白阐述了，如果没有「继承」情况有多糟糕。』

As ShopProduct is beginning to feel like two classes in one, I could accept this and create two types rather than one. Here’s how I might do it:

```php
// listing 03.32

class CdProduct{    
    public $playLength;    
    public $title;    
    public $producerMainName;    
    public $producerFirstName;    
    public $price;

    public function __construct(        
        string $title,        
        string $firstName,        
        string $mainName,        
        float  $price,        
        int    $playLength    
    ) {        
        $this->title             = $title;        
        $this->producerFirstName = $firstName;        
        $this->producerMainName  = $mainName;        
        $this->price             = $price;        
        $this->playLength        = $playLength;    
    }

    public function getPlayLength()    {        
        return $this->playLength;    
    }

    public function getSummaryLine()    {        
        $base  = "{$this->title} ( {$this->producerMainName}, ";        
        $base .= "{$this->producerFirstName} )";        
        $base .= ": playing time - {$this->playLength}";        
        return $base;    
    }

    public function getProducer()    {        
    return $this->producerFirstName . " "            
        . $this->producerMainName;    
    }
}
```

```php
// listing 03.33

class BookProduct{    
    public $numPages;    
    public $title;    
    public $producerMainName;

    public $producerFirstName;    
    public $price;

    public function __construct(        
        string $title,        
        string $firstName,        
        string $mainName,        
        float  $price,        
        int    $numPages    
    ) {        
        $this->title             = $title;        
        $this->producerFirstName = $firstName;        
        $this->producerMainName  = $mainName;        
        $this->price             = $price;        
        $this->numPages          = $numPages;    
    }

    public function getNumberOfPages()    {        
        return $this->numPages;    
    }

    public function getSummaryLine()    {        
        $base  = "{$this->title} ( {$this->producerMainName}, ";        
        $base .= "{$this->producerFirstName} )";        
        $base .= ": page count - {$this->numPages}";        
        return $base;    
    }

    public function getProducer()    {        
        return $this->producerFirstName . " "            
            . $this->producerMainName;    
    }
}
```

I have addressed the complexity issue, but at a cost. I can now create a getSummaryLine() method for each format without having to test a flag. Neither class maintains fields or methods that are not relevant to it. The cost lies in duplication. The getProducerName() method is exactly the same in each class. Each constructor sets a number of identical properties in the same way. This is another unpleasant odor you should train yourself to sniff out.

这时我们解决了「复杂性」问题，但是我们付出了代价。现在不需要测试特征值，就可以为每种产品创建 getSummaryline() 方法。类也不再包含和它不相关的字段或方法。

If I need the getProducer() methods to behave identically for each class, any changes I make to one implementation will need to be made for the other. Without care, the classes will soon slip out of synchronization. Even if I am confident that I can maintain the duplication, my worries are not over. I now have two types rather than one.

1『拆分后的弊端：1）很多重复代码或者重复的形式；2）共有的部分要更新的话每个都得更新，容易忘。3）传参的时候类型检测不好实现了。』

Remember the ShopProductWriter class? Its write() method is designed to work with a single type: ShopProduct. How can I amend this to work as before? I could remove the class type declaration from the method signature, but then I must trust to luck that write() is passed an object of the correct type. I could add my own type checking code to the body of the method:

```php
// listing 03.34

class ShopProductWriter{    
    public function write($shopProduct)    {        
        if (            
            ! ($shopProduct instanceof CdProduct)  &&            
            ! ($shopProduct instanceof BookProduct)        
        ) {            
            die("wrong type supplied");        
        }        
        $str  = "{$shopProduct->title}: "            
            . $shopProduct->getProducer()            
            . " ({$shopProduct->price})\n";        
        print $str;    
    }
}
```

Notice the instanceof operator in the example; instanceof resolves to true if the object in the left-hand operand is of the type represented by the right-hand operand.

Once again, I have been forced to include a new layer of complexity. Not only do I have to test the \$shopProduct argument against two types in the write() method, but I have to trust that each type will continue to support the same fields and methods as the other. It was all much neater when I simply demanded a single type because I could use a class type declaration and because I could be confident that the ShopProduct class supported a particular interface.

The CD and book aspects of the ShopProduct class don’t work well together but can’t live apart, it seems. I want to work with books and CDs as a single type while providing a separate implementation for each format. I want to provide common functionality in one place to avoid duplication, but allow each format to handle some method calls differently. I need to use inheritance.

1『为什么要发明「继承」特性，作者真的是把当时遇到问题的场景描述清楚了，很赞。任何新的好的特性都是为了解决某一个难题而创造出来的。「继承」是分割与合并之间的平衡把握。』

我们被迫再次增加了代码的复杂性。不仅要检测 \$shopproduct 是否符合 write() 方法中的两种类型，还要确保每种类型和另一种类型一样，都支持相同的字段和方法。如果我们可以限制参数必须为特定的一种产品类型，就可以在方法参数中使用类型提示，那么代码会更加清楚简洁，而且也因为此时可以确定 Shopproduct 类只支持某一种接口。Shopproduct 类中的 CD 和图书这两部分合并之后不能很好地工作，但是它们似乎也不能分开存在。我们希望能为每种类型提供一个单独的工具，把书和 CD 当做单独的类型，但同时希望提供公用的功能来避免重复，又允许每种类型处理不同的方法调用。这正是我们使用继承的原因。

#### 3.5.2 Working with Inheritance

The first step in building an inheritance tree is to find the elements of the base class that don’t fit together or that need to be handled differently. I know that the getPlayLength() and getNumberOfPages() methods do not belong together. I also know that I need to create different implementations for the getSummaryLine() method. Let’s use these differences as the basis for two derived classes:

```php
// listing 03.35

class ShopProduct{    
    public $numPages;    
    public $playLength;    
    public $title;    
    public $producerMainName;    
    public $producerFirstName;    
    public $price;    
    
    public function __construct(        
        string $title,
        string $firstName,        
        string $mainName,        
        float  $price,        
        int    $numPages = 0,        
        int    $playLength = 0    
    ) {        
        $this->title             = $title;        
        $this->producerFirstName = $firstName;        
        $this->producerMainName  = $mainName;        
        $this->price             = $price;        
        $this->numPages          = $numPages;        
        $this->playLength        = $playLength;    
    }

    public function getProducer()    {        
        return $this->producerFirstName . " "            
            . $this->producerMainName;    
    }

    public function getSummaryLine()    {        
        $base  = "{$this->title} ( {$this->producerMainName}, ";        
        $base .= "{$this->producerFirstName} )";        
        return $base;    
    }
}
```

```php
// listing 03.36

class CdProduct extends ShopProduct{    
    public function getPlayLength()    {        
        return $this->playLength;    
    }

    public function getSummaryLine()    {        
        $base  = "{$this->title} ( {$this->producerMainName}, ";        
        $base .= "{$this->producerFirstName} )";        
        $base .= ": playing time - {$this->playLength}";        
        return $base;    
    }
}
```

```php
// listing 03.37

class BookProduct extends ShopProduct{    
    public function getNumberOfPages() {        
        return $this->numPages;    
    }

    public function getSummaryLine()    {        
        $base  = "{$this->title} ( {$this->producerMainName}, ";        
        $base .= "{$this->producerFirstName} )";        
        $base .= ": page count - {$this->numPages}";        
        return $base;    
    }
}
```

1『注意，字符串里带变量的话，字符串必须得用双引号，单引号是无效的。已经碰到好几个场景单引号无效了，所以必须该习惯，以后所有的字符串都使用双引号。（2020-06-19）』

To create a child class, you must use the extends keyword in the class declaration. In the example, I created two new classes, BookProduct and CdProduct. Both extend the ShopProduct class.

Because the derived classes do not define constructors, the parent class’s constructor is automatically invoked when they are instantiated. The child classes inherit access to all the parent’s public and protected methods (though not to private methods or properties). This means that you can call the getProducer() method on an object instantiated from the CdProduct class, even though getProducer() is defined in the ShopProduct class:

1『子类里如果没有构造函数的话，默认调用父类的构造函数。』

```php
// listing 03.38

$product2 = new CdProduct(    
    "Exile on Coldharbour Lane",    
    "The",    
    "Alabama 3",    
    10.99,    
    0,    
    60.33
);
print "artist: {$product2->getProducer()}\n";
```

So both the child classes inherit the behavior of the common parent. You can treat a BookProduct object as if it were a ShopProduct object. You can pass a BookProduct or CdProduct object to the ShopProductWriter class’s write() method and all will work as expected.

Notice that both the CdProduct and BookProduct classes override the getSummaryLine() method, providing their own implementation. Derived classes can extend but also alter the functionality of their parents.

The super class’s implementation of this method might seem redundant because it is overridden by both its children. Nevertheless, it provides basic functionality that new child classes might use. The method’s presence also provides a guarantee to client code that all ShopProduct objects will provide a getSummaryLine() method. Later on you will see how it is possible to make this promise in a base class without providing any implementation at all. Each child ShopProduct class inherits its parent’s properties. Both BookProduct and CdProduct access the \$title property in their versions of getSummaryLine().

1『重载的好处比之前自己想象的要大很多，不仅仅是表面上的覆盖。』

Inheritance can be a difficult concept to grasp at first. By defining a class that extends another, you ensure that an object instantiated from it is defined by the characteristics of first the child and then the parent class. Another way of thinking about this is in terms of searching. When I invoke \$product2->getProducer(), there is no such method to be found in the CdProduct class, and the invocation falls through to the default implementation in ShopProduct. When I invoke \$product2->getSummaryLine(), on the other hand, the getSummaryLine() method is found in CdProduct and invoked.

1『跟 JS 里的委托异曲同工，调用对象里的某个属性时，好不到就去它的原型对象里找，再找不到就去其原型对象的原型对象里去，直到找到根原型对象。』

The same is true of property accesses. When I access \$title in the BookProduct class’s getSummaryLine() method, the property is not found in the BookProduct class. It is acquired instead from the parent class, from ShopProduct. The \$title property applies equally to both subclasses, and therefore, it belongs in the superclass.

A quick look at the ShopProduct constructor, however, shows that I am still managing data in the base class that should be handled by its children. The BookProduct class should handle the \$numPages argument and property, and the CdProduct class should handle the \$playLength argument and property. To make this work, I will define constructor methods in each of the child classes.

#### 3.5.2.1 Constructors and Inheritance

When you define a constructor in a child class, you become responsible for passing any arguments on to the parent. If you fail to do this, you can end up with a partially constructed object. To invoke a method in a parent class, you must first find a way of referring to the class itself: a handle. 

PHP provides us with the parent keyword for this purpose. To refer to a method in the context of a class rather than an object, you use :: rather than ->:

```php
parent::__construct()
```

1『上面语句其实是个调用，里面要传入的参数，是父类里的基本属性。作者没写分号，之前没想到这点。』

The preceding means,「Invoke the \_\_construct() method of the parent class.」Here I amend my example so that each class handles only the data that is appropriate to it:

```php
// listing 03.39

class ShopProduct{    
    public $title;    
    public $producerMainName;    
    public $producerFirstName;    
    public $price;

    function __construct(        
        $title,        
        $firstName,        
        $mainName,        
        $price    
    ) {        
    $this->title             = $title;        
    $this->producerFirstName = $firstName;        
    $this->producerMainName  = $mainName;        
    $this->price             = $price;    
    }

    function getProducer()    {        
        return $this->producerFirstName . " "            
            . $this->producerMainName;    
    }

    function getSummaryLine()    {
        $base  = "{$this->title} ( {$this->producerMainName}, ";        
        $base .= "{$this->producerFirstName} )";        r
        return $base;    
    }
}
```

```php
// listing 03.40

class BookProduct extends ShopProduct{    
    public $numPages;

    public function __construct(        
        string $title,        
        string $firstName,        
        string $mainName,        
        float  $price,        
        int    $numPages    
    ) {        
        parent::__construct(            
            $title,            
            $firstName,            
            $mainName,            
            $price        
        );        
        $this->numPages = $numPages;    
    }

    public function getNumberOfPages()    {        
        return $this->numPages;    
    }

    public function getSummaryLine()    {        
        $base  = "{$this->title} ( $this->producerMainName, ";        
        $base .= "$this->producerFirstName )";        
        $base .= ": page count – {$this->numPages}";        
        return $base;    
    }
}
```

```php
// listing 03.41

class CdProduct extends ShopProduct{    
    public $playLength;

    public function __construct(        
        string $title,        
        string $firstName,
        string $mainName,        
        float  $price,        
        int    $playLength    
    ) {        
        parent::__construct(            
            $title,            
            $firstName,            
            $mainName,            
            $price        
    );        
    $this->playLength = $playLength;    
    }

    public function getPlayLength()    {        
        return $this->playLength;    
    }

    public function getSummaryLine()    {        
        $base  = "{$this->title} ( {$this->producerMainName}, ";        
        $base .= "{$this->producerFirstName} )";        
        $base .= ": playing time - {$this->playLength}";        
        return $base;    
    }
}
```

Each child class invokes the constructor of its parent before setting its own properties. The base class now knows only about its own data. Child classes are generally specializations of their parents. As a rule of thumb, you should avoid giving parent classes any special knowledge about their children.

每个子类都会在设置自己的属性前调用父类的构造方法。基类现在仅知道自己的数据。子类一般是父类的特例。我们应该避免告诉父类任何关于子类的信息，这是一条经验规则。

1『上面的方法，实现了父类里基本属性与子类的分离，子类只有通过构造函数才能访问到父类里的那些基本属性。』

Note: prior to php 5, constructors took on the name of the enclosing class. the new unified constructors use the name \_\_construct(). Using the old syntax, a call to a parent constructor would tie you to that particular class: parent::ShopProduct();. the old constructor syntax was deprecated in php 7.0 and should not be used.

#### 3.5.2.2 Invoking an Overridden Method

The parent keyword can be used with any method that overrides its counterpart in a parent class. When you override a method, you may not wish to obliterate the functionality of the parent, but rather to extend it. You can achieve this by calling the parent class’s method in the current object’s context. If you look again at the getSummaryLine() method implementations, you will see that they duplicate a lot of code. It would be better to use rather than reproduce the functionality already developed in the ShopProduct class:

Parent 关键字可以在任何覆写父类方法的方法中使用。覆写一个父类的方法时，我们并不希望删除父类的功能，而是扩展它，通过在当前对象中调用父类的方法可达到这个目的。如果回头看两个类中 getsummaryline() 方法的实现，将会发现它们重复了许多代码。事实上，我们应该利用 Shopproduct 类中已经存在的功能，而不应该重复开发。

```php
// listing 03.42

// ShopProduct class...

function getSummaryLine() {        
    $base  = "{$this->title} ( {$this->producerMainName}, ";        
    $base .= "{$this->producerFirstName} )";        
    return $base;    
}
`
// listing 03.43

// BookProduct class...

public function getSummaryLine() {        
    $base  = parent::getSummaryLine();        
    $base .= ": page count - $this->numPages";        
    return $base;    
}
```

I set up the core functionality for the getSummaryLine() method in the ShopProduct base class. Rather than reproduce this in the CdProduct and BookProduct subclasses, I simply call the parent method before proceeding to add more data to the summary string.

1『子类里的成员函数的重载也可以借鉴构造函数的思路，不用全部重载，父类里有的部分代码可以直接调用。』

Now that you have seen the basics of inheritance, I will reexamine property and method visibility in light of the full picture.

#### 3.5.3 Public, Private, and Protected: Managing Access to Your Classes

So far, I have declared all properties public. Public access is the default setting for methods and for properties if you use the old var keyword in your property declaration. Elements in your classes can be declared public, private, or protected: 1) Public properties and methods can be accessed from any context. 2) A private method or property can only be accessed from within the enclosing class. Even subclasses have no access. 3) A protected method or property can only be accessed from within either the enclosing class or from a subclass. No external code is granted access.

So how is this useful to us? Visibility keywords allow you to expose only those aspects of a class that are required by a client. This sets a clear interface for your object. By preventing a client from accessing certain properties, access control can also help prevent bugs in your code. Imagine, for example, that you want to allow ShopProduct objects to support a discount. You could add a \$discount property and a setDiscount() method:

```php
// listing 03.44

// ShopProduct class

public $discount = 0;
//...

public function setDiscount(int $num)    {        
    $this->discount = $num;    
}
```

Armed with a mechanism for setting a discount, you can create a getPrice() method that takes account of the discount that has been applied:

```php
public function getPrice()    {        
    return ($this->price - $this->discount);    
}
```

At this point, you have a problem. You only want to expose the adjusted price to the world, but a client can easily bypass the getPrice() method and access the \$price property:

```php
print "The price is {$product1->price}\n";
```

This will print the raw price and not the discount-adjusted price you wish to present. You can put a stop to this straight away by making the \$price property private. This will prevent direct access, forcing clients to use the getPrice() method. Any attempt from outside the ShopProduct class to access the \$price property will fail. As far as the wider world is concerned, this property has ceased to exist.

Setting properties to private can be an overzealous strategy. A private property cannot be accessed by a child class. Imagine that our business rules state that books alone should be ineligible for discounts. You could override the getPrice() method so that it returns the \$price property, applying no discount:

```php
// listing 03.45

// BookProduct

public function getPrice()    {        
    return $this->price;    
}
```

As the private \$price property is declared in the ShopProduct class and not BookProduct, the attempt to access it here will fail. The solution to this problem is to declare \$price protected, thereby granting access to descendant classes. Remember that a protected property or method cannot be accessed from outside the class hierarchy in which it was declared. It can only be accessed from within its originating class or from within children of the originating class.

As a general rule, err on the side of privacy. Make properties private or protected at first and relax your restriction only as needed. Many (if not most) methods in your classes will be public, but once again, if in doubt, lock it down. A method that provides local functionality for other methods in your class has no relevance to your class’s users. Make it private or protected.

一般来说，我们倾向于严格控制可访问性。最好将类属性初始化为 private 或 protected 然后在需要的时候再放松限制条件。类中的许多（如果不是大多数）方法都可以是 public，但是如果拿不定主意的话，就限制一下。有些类方法只为类中其他方法提供本地功能，与类外部的代码没有任何联系，应该将其设置为 private 或 protected。

1『以上是设置私有属性、保护属性的原则。属性都设置为限制性的 private 或 protected 的，再根据应用场景放松限制；方法都设置为 public 的，再根据应用场景加强限制。做一张任意卡片。』——已完成

#### 3.5.3.1 Accessor Methods

Even when client programmers need to work with values held by your class, it is often a good idea to deny direct access to properties, providing methods instead that relay the needed values. Such methods are known as accessors or getters and setters.

2『一个原则，通说对象的方法去访问属性值，不要直接访问，把「方法」作为接口。访问方法做一张术语卡片。』——已完成

You have already seen one benefit afforded by accessor methods. You can use an accessor to filter a property value according to circumstances, as was illustrated by the getPrice() method. You can also use a setter method to enforce a property type. Type declarations can be used to constrain method arguments, but a property can contain data of any type. Remember the ShopProductWriter class that uses a ShopProduct object to output list data? I can develop this further, so that it writes any number of ShopProduct objects at one time:

之前已经看到由访问方法带来的一个好处。可以使用访问方法根据环境过滤属性，就像 getPrice() 方法那样。也可以使用 setter 方法来强制属性类型。我们已经见过，类的类型提示可以用于约束方法参数，但是它不能直接控制属性类型。还记得 ShopProductwriter 类使用 Shopi 输出清单数据吗？我们将改进它，使其一次可以输出许多 ShopProduct 对象。

```php
// listing 03.46

class ShopProductWriter{    
    public $products = [];
    
    public function addProduct(ShopProduct $shopProduct)    {        
        $this->products[] = $shopProduct;    
    }

    public function write()    {        
        $str =  "";        
        foreach ($this->products as $shopProduct) {            
        $str .= "{$shopProduct->title}: ";            
        $str .= $shopProduct->getProducer();            
        $str .= " ({$shopProduct->getPrice()})\n";        
        }        
    print $str;    
    }
}
```

The ShopProduct Writer class is now much more useful. It can hold many ShopProduct objects and write data for them all in one go. I must trust my client coders to respect the intentions of the class, though. Despite the fact that I have provided an addProduct() method, I have not prevented programmers from manipulating the \$products property directly. Not only could someone add the wrong kind of object to the \$products array property, but he could even overwrite the entire array and replace it with a primitive value. I can prevent this by making the \$products property private:

```php
class ShopProductWriter {    
    private $products = [];
    //...
```

It’s now impossible for external code to damage the \$products property. All access must be via the addProduct() method, and the class type declaration I use in the method declaration ensures that only ShopProduct objects can be added to the array property.

#### 3.5.3.2 The ShopProduct Classes

Let’s close this chapter by amending the ShopProduct class and its children to lock down access control:

```php
// listing 03.48

class ShopProduct{    
    private   $title;    
    private   $producerMainName;    
    private   $producerFirstName;    
    protected $price;    
    private   $discount = 0;

    public function __construct(        
        string $title,        
        string $firstName,        
        string $mainName,        
        float  $price    
    ) {        
        $this->title             = $title;        
        $this->producerFirstName = $firstName;        
        $this->producerMainName  = $mainName;        
        $this->price             = $price;    
    }

    public function getProducerFirstName()    {        
        return $this->producerFirstName;    
    }

    public function getProducerMainName()    {        
        return $this->producerMainName;    
    }

    public function setDiscount($num)    {        
        $this->discount = $num;   
    }

    public function getDiscount()    {        
        return $this->discount;    
    }

    public function getTitle()    {        
        return $this->title;    
    }

    public function getPrice()    {        
        return ($this->price - $this->discount);    
    }

    public function getProducer()    {        
        return $this->producerFirstName . ""           
            . $this->producerMainName;    
    }

    public function getSummaryLine()    {        
        $base  = "{$this->title} ( {$this->producerMainName}, ";        
        $base .= "{$this->producerFirstName} )";
        return $base;    
    }
}

// listing 03.49

class CdProduct extends ShopProduct{    
    private $playLength;    
    public function __construct(        
        string $title,        
        string $firstName,        
        string $mainName,        
        float  $price,        
        int    $playLength    
    ) {        
    parent::__construct(            
        $title,            
        $firstName,            
        $mainName,            
        $price        
    );        
        $this->playLength = $playLength;    
    }

    public function getPlayLength()    {        
        return $this->playLength;    
    }

    public function getSummaryLine()    {        
        $base  = "{$this->title} ( {$this->producerMainName}, ";        
        $base .= "{$this->producerFirstName} )";        
        $base .= ": playing time - {$this->playLength}";        
        return $base;    
    }
}

// listing 03.50

class BookProduct extends ShopProduct{    
    private $numPages;
    public function __construct(        
        string $title,        
        string $firstName,        
        string $mainName,        
        float  $price,        
        int    $numPages    
    ) {
    parent::__construct(            
        $title,            
        $firstName,            
        $mainName,            
        $price        
    );        
        $this->numPages = $numPages;    
    }

    public function getNumberOfPages()    {        
        return $this->numPages;    
    }

    public function getSummaryLine()    {        
        $base  = parent::getSummaryLine();        
        $base .= ": page count - $this->numPages";        
        return $base;    
    }

    public function getPrice()    {        
        return $this->price;    
    }
}
```

There is nothing substantially new in this version of the ShopProduct family. All properties are either private or protected, and I added a number of accessor methods to round things off.

## 0104. Advanced Features

You have already seen how class type hinting and access control give you more control over a class’s interface. In this chapter, I will delve deeper into PHP’s object-oriented features. This chapter will cover several subjects: 1) Static methods and properties: Accessing data and functionality through classes rather than objects. 2) Abstract classes and interfaces: Separating design from implementation. 3) Traits: Sharing implementation between class hierarchies. 4) Error handling: Introducing exceptions. 5) Final classes and methods: Limiting inheritance. 6) Destructor methods: Cleaning up after your objects. 7) Interceptor methods: Automating delegation. 8) Cloning objects: Making object copies. 9) Resolving objects to strings: Creating a summary method. 10) Callbacks: Adding functionality to components with anonymous functions and classes.

In this chapter, we came to grips with PHP’s advanced object-oriented features. Some of these will become familiar as you work through the book. In particular, I will return frequently to abstract classes, exceptions, and static methods. In the next chapter, I take a step back from built-in object features and look at classes and functions designed to help you work with objects.

### 4.1 Static Methods and Properties

All of the examples in the previous chapter worked with objects. I characterized classes as templates from which objects are produced, and objects as active instances of classes—the things whose methods you invoke and whose properties you access. I implied that, in object-oriented programming, the real work is done by instances of classes. Classes, after all, are merely templates for objects. In fact, it is not that simple. You can access both methods and properties in the context of a class rather than that of an object. Such methods and properties are「static」and must be declared as such by using the static keyword:

```php
// listing 04.01
class StaticExample {    
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

只有在使用 parent 关健字调用方法的时候，才能对一个非静态方法进行静态形式的调用。除非是访问一个被写的方法，否则永远只能使用 :: 访问被明确声明为 static 的方法或属性。在文档中，你将会经常看到使用 static 语法来引用方法或属性。这并不意味着其中的方法或属性必须是静态的，只不过说明它属于特定的类。例如，shopProductWriter 类的方法 write() 可以衣示为 Shopproductwriter::write()，虽然 write() 方法并不是静态的。你将在本书中看到这种语法形式。

2『除非重载方法，用 :: 去访问那些显式声明的静态属性和静态方法。目前还没弄清楚这个概念。（2020-04-27）回复：首先，静态方法的调用形式都是「类名::静态方法」，唯一也用 :: 调用非静态方法的场景式在类继承定义里「parent::非静态方法」。所以，如果是访问那些显式声明的静态属性和静态方法的，都应该用 :: 去调用，除非是访问重载方法（这点还是不明白）。（2020-06-19）如何调用静态属性和静态方法，做一张任意卡片。』——已完成

By definition, static methods and properties are invoked on classes and not objects. For this reason, they are often referred to as class variables and properties. As a consequence of this class orientation, you cannot use the \$this pseudo-variable inside a static method.

So, why would you use a static method or property? Static elements have a number of characteristics that can be useful. First, they are available from anywhere in your script (assuming that you have access to the class). This means you can access functionality without needing to pass an instance of the class from object to object or, worse, storing an instance in a global variable. Second, a static property is available to every instance of a class, so you can set values that you want to be available to all members of a type. Finally, the fact that you don’t need an instance to access a static property or method can save you from instantiating an object purely to get at a simple function.

静态元素有很多有用的特性。首先，它们在代码中的任何地方都可用（假设你可以访问该类）。也就是说，你不需要在对象间传递类的实例，也不需要将实例存放在全局变量中，就可以访问类中的方法。其次，类的每个实例都可以访问类中定义的静态属性，所以你可以利用静态属性来设置值，该值可以被类的所有对象使用。最后，不需要实例对象就能访问静态属性或方法，这样我们就不用为了获取一个简单的功能而实例化对象。

2『静态属性和静态方法的优势做一张任意卡片。』——已完成

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

这样的方法就像「工厂」一样，可以接受原始数据（比如一列数据或配置信息），然后据此产生对象。「工厂」这一术语在代码设计中用于生成对象实例。我们会在后面介绍工厂模式的例子。

In some ways, of course, this example poses as many problems as it solves. Although I make the ShopProduct::getInstance() method accessible from anywhere in a system without the need for an ShopProduct instance, I also demand that client code provides a PDO object. Where is this to be found? 

And is it really good practice for a parent class to have such intimate knowledge of its children? (Hint: no, it is not.) Problems of this kind—where to acquire key objects and values and how much classes should know about one another—are very common in object-oriented programming. I examine various approaches to object generation in Chapter 9.

1『真是环环相扣，上面的知识点消化需要第 9 章的内容。』

### 4.2 Constant Properties

Some properties should not be changed. The Answer to Life, the Universe, and Everything is 42, and you want it to stay that way. Error and status flags will often be hard-coded into your classes. Although they should be publicly and statically available, client code should not be able to change them.

1『所以错误和状态标志都应该设为常量属性。』

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

1『常量属性的调用方法跟静态属性一样，类名后面加域运算符再加常量名（不需要 \$，且全大写）。』

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

2『抽象类不能实例化，它是用来定义接口供其他类继承用的。抽象类里定义的抽象方法不能有「实现」，所以定义的时候没有函数体，跟调用的形式一样。关键是继承它的子类一定在子类里实现这个抽象方法。抽象类做一张术语卡片。』——已完成

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

1『这倒是提供了一个不用写「类型检查」的办法，初始化一个该类型的空值。』

### 4.4 Interfaces

Although abstract classes let you provide some measure of implementation, interfaces are pure templates. An interface can only define functionality; it can never implement it. An interface is declared with the interface keyword. It can contain properties and method declarations but not method bodies. Here’s an interface:

2『接口才是纯模板，它只定义函数，而且这个函数没函数体。相比而言，抽象类里除了有抽象方法外，也可以有普通方法。接口，做一张术语卡片。』——已完成

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

1『注意，在类里实现接口的时候，配套的数据类型不能少，比如上面代码里的「public function getPrice(): float {}」。这点正好体现了后面一直强调的「实现多个指定类型」。』

ShopProduct already had a getPrice() method, so why might it be useful to implement the Chargeable interface? Once again, the answer has to do with types. An implementing class takes on the type of the class it extends and the interface that it implements. This means that the CdProduct class belongs to the following:

实现接口的类接受了它继承的类及实现的接口的类型。

```
CdProduct
ShopProduct
Chargeable
```

1『

上面说了接口的用途，应该是跟「多类型」有关，目前没彻底吃透。现阶段知道的用途：1）一个类只能继承一个基类，但可以实现多个接口，每实现一个接口对应着一个「type」。2）跟 traits 结合起来用。（2020-04-27）

回复：

As we have seen, interfaces help you manage the fact that, like Java, PHP does not support multiple inheritance. In other words, a class in PHP can only extend a single parent. However, you can make a class promise to implement as many interfaces as you like; for each interface it implements, the class takes on the corresponding type. So interfaces provide types without implementation. 

』

This can be exploited by client code. To know an object’s type is to know its capabilities. Consider this method:

```php
public function cdInfo(CdProduct $prod)    {        
    // ...    
}
```

The method knows that the \$prod object has a getPlayLength() method in addition to all the methods defined in the ShopProduct class and Chargeable interface. Passed the same object, the method knows that \$prod supports all the methods in ShopProduct:

这可以被客户端代码很方便地使用。你只要知道一个对象的类型，就知道它能做什么。现在知道 \$prod 对象除了拥有 ShopProduct 类和 Chargeable 接口中定义的所有方法之外，还有 getPlayLength() 方法。

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

由于任何类都可以实现接口（实际上，一个类可以实现多个接口），接口可以有效地将不相关的类型联结起来。

```php
class Shipping implements Chargeable{    
    public function getPrice(): float    {        
        //...    
    }
}
```

I can pass a Shipping object to the addChargeableItem method just as I can pass it a ShopProduct object. The important thing to a client working with a Chargeable object is that it can call a getPrice() method. Any other available methods are associated with other types, whether through the object’s own class, a superclass, or another interface. These are irrelevant to the client.

将 shipping 对象传递给 addChargeableItem() 方法，就像将其传递给 ShopProduct 对象一样。使用 Chargeable 对象的代码（即客户端代码）可以随时调用 getPrice() 方法，而对象中的任何其他方法都要和其类型关联起来，无论是通过对象自己的类、父类还是其他接口。这些都是客户端代码不需要关注的。

1『上面的信息目前没吃透。（2020-06-19）』

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

1『 traits 的作用是实现局部继承：share an implementation across inheritance hierarchies. 可以当作类的组件模块，在类的定义里使用 use 关键词调用 trait。在 laravel 框架里看到很多 use 语句是放在 class 定义体之外的。traits 能和接口结合起来一起用，还能跟抽象属性、抽象方法结合起来用，着实强大。』

A trait is a class-like structure that cannot itself be instantiated but can be incorporated into classes. Any methods defined in a trait become available as part of any class that uses it. A trait changes the structure of a class, but doesn’t change its type. Think of traits as includes for classes. Let’s look at why a trait might be useful.

2『 traits 做一张术语卡片。』——已完成

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

1『上面场景里的问题，除了用 traits 解决外，第 11 章还提供了方案（facor it out into a reusable class）。use 语句调用 traits 可以放在 class 体内。』

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

1『单独的 traits 没法使用「type hinting」，但是结合 Interfaces 就能使用。下面的例子目前还没消化。（2020-05-03）』

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

// listing 04.24
$p = new ShopProduct();
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

1『 traits 定义里可以通过 \$this->XX 来调用宿主类（即调用该 traits 的 class）里的属性，作者认为是个坏设计，因为你怎么能确定宿主类里就一定有这个属性的声明呢。所以如果能结合 abstract methods 的话即可解决这个问题。这个特性跟 JS 里的闭包很像。』

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

### 4.6 Late Static Bindings: The static Keyword

Now that you’ve seen abstract classes, traits, and interfaces, it’s time to return briefly to static methods. You saw that a static method can be used as factory, a way of generating instances of the containing class. If you’re as lazy a coder as me, you might chafe at the duplication in an example like this:

```php
// listing 04.45
abstract class DomainObject{

}

// listing 04.46
class User extends DomainObject{    
    public static function create(): User    {        
        return new User();    
    }
}

// listing 04.47
class Document extends DomainObject{    
    public static function create(): Document    {        
        return new Document();    
    }
}
```

I create a super class named DomainObject. In a real-world project, of course, this would contain functionality common to its extending classes. Then I create two child classes, User and Document. I would like my concrete classes to have static create() methods.

Note: Why would I use a static factory method when a constructor performs the work of creating an object already? In Chapter 12, I’ll describe a pattern called Identity Map. an Identity Map component generates and manages a new object only if an object with the same distinguishing characteristics is not already under management. If the target object already exists, it is returned. a factory method like create() would make a good client for a component of this sort.

当构造函数创建对象时，我为什么使用静态工厂方法？第 12 章将介绍 Identity Map 模式。只有具有相同特征的对象没有被管理，Identity Map 组件才会生成并管理这个新对象。如果目标对象已经存在，就返回诚对象。像 create() 这样的工厂方法能为这类组件创建优秀的客户端。

2『体现了 Identity Map 设计模式。做张术语卡片。（目前还无法理解这个模式）』——已完成

This code works fine, but it has an annoying amount of duplication. I don’t want to have to create boilerplate code like this for every DomainObject child class that I create. Instead, I’ll try pushing the create() method up to the superclass:

```php
// listing 04.48
abstract class DomainObject{    
    public static function create(): DomainObject    {        
        return new self();    
    }
}

// listing 04.49
class User extends DomainObject {

}

// listing 04.50
class Document extends DomainObject {

}

// listing 04.51Document::create();
```

Well, that looks neat. I now have common code in one place, and I’ve used self as a reference to the class. But I have made an assumption about the self keyword. In fact, it does not act for classes exactly the same way that \$this does for objects. self does not refer to the calling context; it refers to the context of resolution. So if I run the previous example, I get this:

self 指的不是调用上下文，它指的是解析上下文。

    Error: Cannot instantiate abstract class popp\ch04\batch06\DomainObject

So self resolves to DomainObject, the place where create() is defined, and not to Document, the class on which it was called. Until PHP 5.3 this was a serious limitation, which spawned many rather clumsy workarounds. PHP 5.3 introduced a concept called late static bindings. The most obvious manifestation of this feature is the keyword: static. static is similar to self, except that it refers to the invoked rather than the containing class. In this case, it means that calling Document::create() results in a new Document object and not a doomed attempt to instantiate a DomainObject object. So now I can take advantage of my inheritance relationship in a static context:

因此，self 被解析为定义 create() 的 DomainObject，而不是解析为调用 self 的 Document 类。PHP 5.3 之前，在这方面都有严格的限制，产生过很多笨拙的解决方案。PHP 5.3 中引入了延迟静态绑定的概念。该特性最明显的标志就是新关键字 static。static 类似于 self，但它指的是被调用的类而不是包含类。在本例中，它的意思是调用 Document::create() 将生成一个新的 Document 对象，而不是试图实例化一个 DomainObject 对象。因此，现在在静态上下文中使用继承关系。

2『延迟静态绑定，做一张术语卡片。』——已完成

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

    Document Object()

1『上面才是正确的实现方法，需要使用 Static Bindings。』

3『

数据流开发时用到了这个知识实现了工厂模式。

```php
<?php

namespace App\Logic;

use App\Exceptions\LogicExceptions;
use App\Model\BaseModel;

class BaseLogic
{
    protected $model;

    public function __construct()
    {
    }

    /**
     * @param BaseModel $model
     * @return static
     */
    public static function build(BaseModel $model)
    {
        return (new static())->setModel($model);
    }

    private function setModel(BaseModel $model)
    {
        $this->model = $model;
        return $this;
    }

    /**
     * 抛出错误信息
     * @param string msg
     * @param int code
     * @throws LogicExceptions
     */
    public function error($msg = '错误', $code = 1001)
    {
        throw new LogicExceptions($msg, $code);
    }
}
```

』

The static keyword can be used for more than just instantiation. Like self and parent, static can be used as an identifier for static method calls, even from a non-static context. Let’s say I want to include the concept of a group for my DomainObject classes. By default in my new classification, all classes fall into category「default」, but I’d like to be able override this for some branches of my inheritance hierarchy:

static 关键字不仅仅可以用于实例化。和 self 和 parent 一样，static 还可以作为静态方法调用的标识符，甚至是从非静态上下文中调用。假设我想为 DomainObject 引入组的概念。默认情况下，所有类都属于 default 类别，但我想能为继承层次结构的某些分支重写类别。

```php
// listing 04.52
abstract class DomainObject{    
    private $group;

    public function __construct()    {        
        $this->group = static::getGroup();    
    }

    public static function create(): DomainObject    {        
        return new static();    
    }

    public static function getGroup(): string    {        
        return "default";    
    }
}

// listing 04.53
class User extends DomainObject {

}

// listing 04.54
class Document extends DomainObject{    
    public static function getGroup(): string    {        
        return "document";    
    }
}

// listing 04.55
class SpreadSheet extends Document {

}

// listing 04.56
print_r(User::create());
print_r(SpreadSheet::create());
```

I introduced a constructor to the DomainObject class. It uses the static keyword to invoke a static method: getGroup(). DomainObject provides the default implementation, but Document overrides it. I also created a new class, SpreadSheet, that extends Document. Here’s the output:

```
popp\ch04\batch07\User Object
(    
[group:popp\ch04\batch07\DomainObject:private] => default
)

popp\ch04\batch07\SpreadSheet Object
(    
[group:popp\ch04\batch07\DomainObject:private] => document
)
```

For the User class, not much clever needs to happen. The DomainObject constructor calls getGroup() and finds it locally. In the case of SpreadSheet, though, the search begins at the invoked class, SpreadSheet itself. It provides no implementation, so the getGroup() method in the Document class is invoked. Before PHP 5.3 and late static binding, I would have been stuck with the self keyword here, which would only look for getGroup() in the DomainObject class.

User 类不需要实现太多功能。DomainObject 构造函数调用了 getGroup() 类，并在本地进行查找。对于 SpreadSheet，虽然搜索从被调用的类 SpreadSheet 本身开始，但它没有提供任何实现，因此调用类 Document 中的 getGroup() 方法。PHP 5.3 以前未引入延迟静态绑定，self 关键字只查找 DomainObject 类中的 getGroup()，因此遇到 self 关键字的时候我无计可施。

1『妙啊妙啊，这样的话基类的定义就更灵活了。但这一节的内容还是没有吃透。』

### 4.7 Handling Errors

Things go wrong. Files are misplaced, database servers are left uninitialized, URLs are changed, XML files are mangled, permissions are poorly set, disk quotas are exceeded. The list goes on and on. In the fight to anticipate every problem, a simple method can sometimes sink under the weight of its own error-handling code.

1『 bug 是永远不可能全部消除的，能做的就是有效的管理 bug，周全的设计出错后该如何处理。』

Here is a simple Conf class that stores, retrieves, and sets data in an XML configuration file:

```php
// listing 04.57
class Conf{    
    private $file;    
    private $xml;    
    private $lastmatch;

    public function __construct(string $file)    {        
        $this->file = $file;        
        $this->xml = simplexml:load_file($file);    
    }

    public function write()    {        
        file_put_contents($this->file, $this->xml->asXML());    
    }

    public function get(string $str)    {        
        $matches = $this->xml->xpath("/conf/item[@name=\"$str\"]");        
        if (count($matches)) {            
            $this->lastmatch = $matches[0];            
            return (string)$matches[0];        
        }        
        return null;    
    }

    public function set(string $key, string $value)    {        
        if (! is_null($this->get($key))) {            
            $this->lastmatch[0]=$value;            
            return;        
        }        
        $conf = $this->xml->conf;        
        $this->xml->addChild('item', $value)->addAttribute('name', $key);    
    }
}
```

The Conf class uses the SimpleXml extension to access name value pairs. Here’s the kind of format with which it is designed to work:

```xml
<?xml version="1.0"?>
<conf>    
    <item name="user">bob</item>    
    <item name="pass">newpass</item>    
    <item name="host">localhost</item>
</conf>
```

The Conf class’s constructor accepts a file path, which it passes to simplexml:load_file(). It stores the resulting SimpleXmlElement object in a property called \$xml. The get() method uses XPath to locate an item element with the given name attribute, returning its value. set() either changes the value of an existing item or creates a new one. Finally, the write() method saves the new configuration data back to the file.

Like much example code, the Conf class is highly simplified. In particular, it has no strategy for handling nonexistent or unwriteable files. It is also optimistic in outlook. It assumes that the XML document will be well-formed and will contain the expected elements.

Conf 类的构造器接受一个文件路径，然后传递给 simplexml_load_file()。它将得到的 SimpleXmlElement 对象放在 \$xml 属性中。get() 方法使用 Xpath 和给定的 name 属性来定位 item 元素，并返回值。set() 改变已存在项的值或创建一个新项。最后，write() 方法将新的配置数据保存到文件中。和许多示例代码一样，conf 类非常简单。特别是，它没有任何处理配置信息不存在或不可写的策略。它看起来很乐观，假定 XML 文档的格式正确并且包含了需要的元素。

Testing for these error conditions is relatively trivial, but I must still decide how to respond to them should they arise. There are generally two options.

First, I could end execution. This is simple but drastic. My humble class would then take responsibility for bringing an entire script crashing down around it. Although methods such as __construct() and write() are well placed to detect errors, they do not have the information to decide how to handle them.

Rather than handle the error in my class, then, I could return an error flag of some kind. This could be a Boolean or an integer value such as 0 or -1. Some classes will also set an error string or flag, so that the client code can request more information after a failure.

Many PEAR packages combine these two approaches by returning an error object (an instance of PEAR\_Error), which acts both as notification that an error has occurred and contains the error message within it. This approach is now deprecated, but plenty of classes have not been upgraded, not least because client code often depends on the old behavior.

测试这些错误条件比较琐碎，但是我们仍然需要决定当它们发生时该如何应对。通常有两种选择。首先，可以停止执行代码。这个办法很简单，但是过于激烈。这个粗陋的类会导致整个程序停止执行。虽然 \_\_construct() 和 write() 这样的方法可以检测到错误，但是它们并不知道该如何处理错误。其次，不在类中直接处理错误，而只返回某种错误标志。错误标志可以是布尔值（true 或 false）或整数值（比如 0 或 -1）。一些类也可以设置错误字符串或标志，让客户端代码在失败之后可以获得更多信息。许多 PEAR 包结合使用这两种方法，在发生错误时返回一个错误对象（PEAR_Error 的实例），该对象标志着有错误发生，同时也包含错误的信息。虽然这种方法已经过时了，但是大量的 PEAR 类还没有升级，因为很多客户端代码还依赖于这些旧的错误处理方式。

The problem here is that you pollute your return value. You have to rely on the client coder to test for the return type every time your error-prone method is called. This can be risky. Trust no one!

When you return an error value to calling code, there is no guarantee that the client will be any better equipped than your method to decide how to handle the error. If this is the case, then the problem begins all over again. The client method will have to determine how to respond to the error condition, maybe even implementing a different error-reporting strategy.

这里有个问题，我们的返回值是不定的。PHP 语言本身没有强制规定统一的返回值。在写作本书时，PHP 还不支持返回对象的类型提示，所以有时本应返回一个对象或者基本类型的数据，但实际上返回的可能是一个错误标志。这时候，我们不得不依赖客户程序员来测试每次调用易于出错方法时返回的数据类型。这样做是很危险的，没有谁可以被信赖！当返回一个错误值给调用代码时，不能确保客户端代码能比我们的方法更好地决定如何处理错误。在这种情况下，问题又回到原点。客户端代码不得不决定如何响应错误条件，甚至要重新设计一个处理错误的方法。

#### 4.7.1 Exceptions

通常我们希望封装好的类是完整和独立的，不需要从外部干预内部代码的执行，所以依赖程序员另外写代码来测试一个类中的方法是否出错，这是非常不合理的。

简单地说，我们需要把错误处理的责任集中放在类的内部，而不能依赖于调用该类的程序员和外部代码，因为通常使用该类的程序员并不知道怎么处理类内部的方法所引发的错误。本节主要强调了 PHP4 中各种错误处理方法的局限性，读者看过后面的内容后再回过头来对比一下，会更易于理解。——译者注

PHP 5 introduced exceptions to PHP, a radically different way of handling error conditions. Different for PHP, that is. You will find them hauntingly familiar if you have Java or C++ experience. Exceptions address all of the issues that I have raised so far in this section.

An exception is a special object instantiated from the built-in Exception class (or from a derived class). Objects of type Exception are designed to hold and report error information. The Exception class constructor accepts two optional arguments, a message string and an error code. The class provides some useful methods for analyzing error conditions. These are described in Table 4-1.

The Exception class is fantastically useful for providing error notification and debugging information (the getTrace() and getTraceAsString() methods are particularly helpful in this regard). In fact, it is almost identical to the PEAR_Error class that was discussed earlier. There is much more to an exception than the information it holds, though.

Table 4-1.  The Exception Class’s Public Methods

1『 PHP 里的错误是个对象，是内置 Exception 类的实例化对象。』

#### 4.7.1.1 Throwing an Exception

The throw keyword is used in conjunction with an Exception object. It halts execution of the current method and passes responsibility for handling the error back to the calling code. Here I amend the __construct() method to use the throw statement:

```php
// listing 04.58    
public function __construct(string $file)    {        
    $this->file = $file;        
    if (! file_exists($file)) {           
        throw new \Exception("file '$file' does not exist");        
    }        
    $this->xml = simplexml:load_file($file);    
}
```

The write() method can use a similar construct:

```php
// listing 04.59    
public function write()    {        
    if (! is_writeable($this->file)) {            
        throw new \Exception("file '{$this->file}' is not writeable");        
    }        
    file_put_contents($this->file, $this->xml->asXML());    
}
```

The \_\_construct() and write() methods can now check diligently for file errors as they do their work, but they let code more fitted for the purpose decide how to respond to any errors detected. So how does client code know how to handle an exception when thrown? When you invoke a method that may throw an exception, you can wrap your call in a try clause. A try clause is made up of the try keyword followed by braces. The try clause must be followed by at least one catch clause in which you can handle any error, like this:

```php
// listing 04.60
try {    
    $conf = new Conf(__DIR__ . "/conf01.xml");    
    print "user: " . $conf->get('user') . "\n";    
    print "host: " . $conf->get('host') . "\n";    
    $conf->set("pass", "newpass");    
    $conf->write();
    } catch (\Exception $e) {    
    die($e->__toString());
    }
```

As you can see, the catch clause superficially resembles a method declaration. When an exception is thrown, the catch clause in the invoking scope is called. The Exception object is automatically passed in as the argument variable.

Just as execution is halted within the throwing method when an exception is thrown, so it is within the try clause—control passes directly to the catch clause.

#### 4.7.1.2 Subclassing Exception

You can create classes that extend the Exception class as you would with any user-defined class. There are two reasons why you might want to do this. First, you can extend the class’s functionality. Second, the fact that a derived class defines a new class type can aid error handling in itself.

You can, in fact, define as many catch clauses as you need for a try statement. The particular catch clause invoked will depend on the type of the thrown exception and the class type hint in the argument list. Here are some simple classes that extend Exception:

```php
// listing 04.61
class XmlException extends \Exception{    
    private $error;

    public function __construct(\LibXmlError $error)    {        
        $shortfile = basename($error->file);        
        $msg = "[{$shortfile}, line {$error->line}, col {$error->column}] {$error->message}";        
        $this->error = $error;        
        parent::__construct($msg, $error->code);    
    }

    public function getLibXmlError()    {        
        return $this->error;    
    }

}

// listing 04.62
class FileException extends \Exception{}

// listing 04.63
class ConfException extends \Exception{}
```

The LibXmlError class is generated behind the scenes when SimpleXml encounters a broken XML file. It has \$message and \$code properties, and it resembles the Exception class. I take advantage of this similarity and use the LibXmlError object in the XmlException class. The FileException and ConfException classes do nothing more than subclass Exception. I can now use these classes in my code and amend both \_\_construct() and write():

```php
// listing 04.64

// Conf class...

    function __construct(string $file)    {        
        $this->file = $file;        
        if (! file_exists($file)) {            
            throw new FileException("file '$file' does not exist");        
        }        
        $this->xml = simplexml:load_file($file, null, LIBXML_NOERROR);        
        if (! is_object($this->xml)) {            
            throw new XmlException(libxml:get_last_error());        
        }        
        $matches = $this->xml->xpath("/conf");        
        if (! count($matches)) {            
            throw new ConfException("could not find root element: conf");        
        }    
    }

    function write()    {        
        if (! is_writeable($this->file)) {            
            throw new FileException("file '{$this->file}' is not writeable");        
        }        
        file_put_contents($this->file, $this->xml->asXML());    
    }
```

\_\_construct() throws either an XmlException, a FileException, or a ConfException, depending on the kind of error it encounters. Note that I pass the option flag LIBXML\_NOERROR to simplexml:load\_file(). This suppresses warnings, leaving me free to handle them with my XmlException class after the fact. If I encounter a malformed XML file, I know that an error has occurred because simplexml:load\_file() won’t have returned an object. I can then access the error using libxml:get\_last\_error().

The write() method throws a FileException if the \$file property points to an unwritable entity. So, I have established that \_\_construct() might throw one of three possible exceptions. How can I take advantage of this? Here’s some code that instantiates a Conf object:

```php
// listing 04.65    
public static function init()    {        
    try {            
        $conf = new Conf(__DIR__."/conf.broken.xml");            
        print "user: " . $conf->get('user') . "\n";            
        print "host: " . $conf->get('host') . "\n";            
        $conf->set("pass", "newpass");            
        $conf->write();        
    } catch (FileException $e) {            
        // permissions issue or non-existent file        
    } catch (XmlException $e) {            
        // broken xml        
    } catch (ConfException $e) {            
        // wrong kind of XML file        
    } catch (\Exception $e) {            
        // backstop: should not be called        
    }    
}
```

I provide a catch clause for each class type. The clause invoked depends on the exception type thrown. 

The first to match will be executed, so remember to place the most generic type at the end and the most specialized at the start. For example, if you were to place the catch clause for Exception ahead of the clause for XmlException and ConfException, neither of these would ever be invoked. This is because both of these classes belong to the Exception type, and would therefore match the first clause.

The first catch clause (FileException) is invoked if there is a problem with the configuration file (if the file is nonexistent or unwriteable). The second clause (XmlException) is invoked if an error occurs in parsing the XML file (e.g., if an element is not closed). The third clause (ConfException) is invoked if a valid XML file does not contain the expected root conf element. The final clause (Exception) should not be reached because my methods only generate the three exceptions, which are explicitly handled. It is often a good idea to have a「backstop」clause like this, in case you add new exceptions to the code during development.

Note: If you do provide a「backstop」catch clause, you should ensure that you actually do something about the exception in most instances—failing silently can cause bugs which are hard to diagnose.

The benefit of these fine-grained catch clauses is that they allow you to apply different recovery or failure mechanisms to different errors. For example, you may decide to end execution, log the error and continue, or explicitly rethrow an error:

```php
try {            
    //...        
} catch ( FileException $e ) {            
throw $e;        
}
```

Another trick you can play here is to throw a new exception that wraps the current one. This allows you to stake a claim to the error and add your own contextual information, while retaining the data encapsulated by the exception you have caught. You can read more about this technique in Chapter 15.

1『上面的代码实现了一个如何处理「多错误」场景，需好好消化，目前没吃透。（2020-05-03）』

So what happens if an exception is not caught by client code? It is implicitly rethrown, and the client’s own calling code is given the opportunity to catch it. This process continues either until the exception is caught or until it can no longer be thrown. At this point, a fatal error occurs. Here’s what would happen if I did not catch one of the exceptions in my example:

```
PHP Fatal error:  Uncaught exception 'FileException' with message
'file 'nonexistent/not_there.xml' does not exist' in ...
```

So, when you throw an exception, you force the client to take responsibility for handling it. This is not an abdication of responsibility. An exception should be thrown when a method has detected an error, but does not have the contextual information to be able to handle it intelligently. The write() method in my example knows when the attempt to write will fail, and it knows why, but it does not know what to do about it. This is as it should be. If I were to make the Conf class more knowledgeable than it currently is, it would lose focus and become less reusable.

#### 4.7.1.3 Cleaning Up After try/catch Clauses with finally

The way that code flow is affected by exceptions can cause unexpected problems. For example, clean-up code or other essential housekeeping may not be performed after an exception is generated within a try clause. As you have seen, if an exception is generated within a try clause, flow moves directly to the relevant catch clause. Code that closes database connections or file handles may not get called, and status information might not be updated.

Imagine, for example, that Runner::init() keeps a log of its actions. It logs the start of the initialization process, any errors encountered, and then it logs the end of the initialization process. Here I provide a typically simplified example of this kind of logging:

```php
// listing 04.66    
public static function init()    {        
    try {            
        $fh = fopen(__DIR__ . "/log.txt", "a");            
        fputs($fh, "start\n");            
        $conf = new Conf(dirname(__FILE__) . "/conf.broken.xml");            
        print "user: " . $conf->get('user') . "\n";            
        print "host: " . $conf->get('host') . "\n";            
        $conf->set("pass", "newpass");            
        $conf->write();            
        fputs($fh, "end\n");            
        fclose($fh);        
    } catch (FileException $e) {            
        // permissions issue or non-existent file            
        fputs($fh, "file exception\n");            
        throw $e;        
    } catch (XmlException $e) {            
        fputs($fh, "xml exception\n");
            // broken xml        
    } catch (ConfException $e) {            
        fputs($fh, "conf exception\n");            
        // wrong kind of XML file        
    } catch (\Exception $e) {            
        fputs($fh, "general exception\n");            
        // backstop: should not be called        
    }    
}
```

I open a file, log.txt; I write to it; and then I call my configuration code. If an exception is encountered in this process, I log this fact in the relevant catch clause. I end the try clause by writing to the log and closing its file handle.

Of course, this last step will never be reached if an exception is encountered. Flow passes straight to the relevant catch block, and the rest of the try clause is never run. Here is the log output when a file exception is generated:

```
start
file exception
```

As you can see, the logging began, and the file exception was noted, but the portion of code that registers the end of logging was never reached, and so the log was not updated with that.

You might think that the solution would be to place the final logging step outside of the try /catch block altogether. This would not work reliably. If a generated exception is caught, and the try block allows execution to continue, then flow will move beyond the try / catch construct. However, a catch clause could rethrow the exception, or it might end script execution altogether.

To help programmers deal with problems like this, PHP 5.5 introduced a new clause: finally. If you’re familiar with Java, it’s likely you’ll have seen this clause before. Although catch clauses are only conditionally run when matching exceptions are thrown, the finally clause is always run, whether or not an exception is generated within the try block. I can fix this problem by moving my log write and code to close to a finally clause:

```php
public static function init()    {        
    $fh = fopen(__DIR__ . "/log.txt", "a");        
    try {            
        fputs($fh, "start\n");            
        $conf = new Conf(dirname(__FILE__) . "/conf.broken.xml");            
        print "user: " . $conf->get('user') . "\n";            
        print "host: " . $conf->get('host') . "\n";            
        $conf->set("pass", "newpass");            
        $conf->write();        
    } catch (FileException $e) {            
        // permissions issue or non-existent file            
        fputs($fh, "file exception\n");        
    } catch (XmlException $e) {            
        fputs($fh, "xml exception\n");            
        // broken xml        
    } catch (ConfException $e) {            
        fputs($fh, "conf exception\n");
        // wrong kind of XML file        
    } catch (Exception $e) {            
        fputs($fh, "general exception\n");            
        // backstop: should not be called        
    } finally {            
        fputs($fh, "end\n");           
        fclose($fh);    
    }    
}
```

Because the log write and the fclose() invocation are wrapped in a finally clause, these statements will be run even if, as is the case when a FileException is caught, the exception is rethrown. Here, again, is the log text when a FileException is generated: 

```
start
file exception
end
```

Note:  a finally clause will be run if an invoked catch clause rethrows an exception or returns a value. however, calling die() or exit() in a try or catch block will end script execution, and the finally clause will not be run.

### 4.8 Final Classes and Methods

Inheritance allows for enormous flexibility within a class hierarchy. You can override a class or method so that a call in a client method will achieve radically different effects, according to which class instance it has been passed. Sometimes, though, a class or method should remain fixed and unchanging. If you have achieved the definitive functionality for your class or method, and you feel that overriding it can only damage the ultimate perfection of your work, you may need the final keyword. final puts a stop to inheritance. A final class cannot be subclassed. Less drastically, a final method cannot be overridden. Here’s a final class:

继承为类层次（class hierarchy）内部带来了巨大的灵活性。通过覆写类或方法，根据调用的是哪个类实例，调用同样的类方法可以得到完全不同的结果。但有时候，你可能需要类或方法保持不变。如果希望类或方法完成确定不变的功能，担心覆写它会破坏这个功能，那么需要使用 final 关键字。final 关键字可以终止类的继承。final 类不能有子类，final 方法不能被覆写。

```php
// listing 04.67
final class Checkout {    
    // ...
}
```

Here’s an attempt to subclass the Checkout class:

```php
// listing 04.68
class IllegalCheckout extends Checkout {    
    //...
}
```

This produces an error:

    PHP Fatal error:  Class IllegalCheckout may not inherit from final class (Checkout) in ....

I could relax matters somewhat by declaring a method in Checkout final, rather than the whole class. The final keyword should be placed in front of any other modifiers such as protected or static, like this:

```php
// listing 04.69
class Checkout {    
    final public function totalize() {        
        // calculate bill    
    }
}
```

I can now subclass Checkout, but any attempt to override totalize() will cause a fatal error:

```php
// listing 04.70
class IllegalCheckout extends Checkout {    
    final public function totalize() {        
        // change bill calculation    
    }
}
```

    PHP Fatal error:  Cannot override final method popp\ch04\batch14\Checkout::totalize() ...

Good object-oriented code tends to emphasize the well-defined interface. Behind the interface, though, implementations will often vary. Different classes or combinations of classes conform to common interfaces but behave differently in different circumstances. By declaring a class or method final, you limit this flexibility. There will be times when this is desirable, and you will see some of them later in the book. However, you should think carefully before declaring something final. Are there really no circumstances in which overriding would be useful? You could always change your mind later on, of course, but this might not be so easy if you are distributing a library for others to use. Use final with care.

### 4.9 The Internal Error Class

Back when exceptions were first introduced, the world of trying and catching applied primarily to code written in PHP and not the core engine. Internally generated errors maintained their own logic. This could get messy if you wanted to manage core errors in the same way as code-generated exceptions. PHP 7 has made a start on addressing this issue with the Error class. This implements Throwable—the same built-in interface that the Exception class implements, and therefore it can be treated in the same way. This also means the methods described in Table 4-1 are honored. Error is subclassed for individual error types. Here’s how you might catch a parse error generated by an eval statement:

```php
try {            
    eval("illegal code");        
} catch (\Error $e) {            
    print get_class($e)."\n";        
} catch (\Exception $e) {            
    // do something with an Exception        
}
```

Here’s the output:

    ParseError

So you can match some types of internal errors in catch clauses, either by specifying the Error superclass or by specifying a more specific subclass. Table 4-2 shows the current Error subclasses.

Table 4-2.  The Built-in Error Classes Introduced by PHP 7

Note: at the time of this writing, an attempt to call Error::getMessage() fails with an error, despite the fact that this is declared in the Throwable interface. It is likely that this issue will have been fixed by the time you read this!

### 4.10 Working with Interceptors

PHP provides built-in interceptor methods that can intercept messages sent to undefined methods and properties. This is also known as overloading, but as that term means something quite different in Java and C++, I think it is better to talk in terms of interception.

PHP 提供了内置的拦截器（Interceptor）方法，它可以「拦截」发送到未定义方法和属性的消息。它也被称为重载（overloading），但是自从这个术语在 Java 和 C++中被赋予不同的含义之后，我认为它还是叫做拦截器比较好。

PHP supports three built-in interceptor methods. Like __construct(), these are invoked for you when the right conditions are met. Table 4-3 describes the methods.

Table 4-3.  The Interceptor Methods

The \_\_get() and \_\_set() methods are designed for working with properties that have not been declared in a class (or its parents).

\_\_get() is invoked when client code attempts to read an undeclared property. It is called automatically with a single string argument containing the name of the property that the client is attempting to access. Whatever you return from the \_\_get() method will be sent back to the client as if the target property exists with that value. Here’s a quick example:

```php
// listing 04.71
class Person {    
    public function __get(string $property) {        
        $method = "get{$property}";        
        if (method_exists($this, $method)) {            
            return $this->$method();        
        }    
    }

    public function getName(): string    {        
        return "Bob";    
    }

    public function getAge(): int    {       
        return 44;    
    }
}
```

When a client attempts to access an undefined property, the \_\_get() method is invoked. I have implemented \_\_get() to take the property name and construct a new string, prepending the word「get」. I pass this string to a function called method\_exists(), which accepts an object and a method name and tests for method existence. If the method does exist, I invoke it and pass its return value to the client. Assume the client requests a \$name property:

```php
$p = new Person();print $p->name;
```

In this case, the getName() method is invoked behind the scenes:

    Bob

If the method does not exist, I do nothing. The property that the user is attempting to access will resolve to NULL.

The \_\_isset() method works in a similar way to \_\_get(). It is invoked after the client calls isset() on an undefined property. Here’s how I might extend Person:

```php
// listing 04.72    
public function __isset(string $property)    {        
    $method = "get{$property}";        
    return (method_exists($this, $method));    
}
```

Now a cautious user can test a property before working with it:

```php
if (isset($p->name)) {    
    print $p->name;
}
```

The \_\_set() method is invoked when client code attempts to assign to an undefined property. It is passed two arguments: the name of the property and the value the client is attempting to set. You can then decide how to work with these arguments. Here I further amend the Person class:

```php
// listing 04.73
class Person {    
    private $myname;    
    private $myage;

    public function __set(string $property, string $value)    {        
        $method = "set{$property}";       
        if (method_exists($this, $method)) {            
            return $this->$method($value);        
        }    
    }

    public function setName(string $name)    {        
        $this->myname = $name;        
            if (! is_null($name)) {            
            $this->myname = strtoupper($this->myname);        
        }    
    }

    public function setAge(int $age)    {        
        $this->myage = $age;   
    }
}
```

In this example, I work with「setter」methods rather than「getters.」If a user attempts to assign to an undefined property, the \_\_set() method is invoked with the property name and the assigned value. I test for the existence of the appropriate method and invoke it if it exists. In this way, I can filter the assigned value.

Note: remember that methods and properties in php documentation are frequently spoken of in static terms in order to identify them with their classes. so you might talk about the Person::\$name property, even though the property is not declared static and would in fact be accessed via an object.

So if I create a Person object and then attempt to set a property called Person::\$name, the \_\_set() method is invoked because this class does not define a \$name property. The method is passed the string "name" and the value that the client assigned. How the value is then used depends on the implementation of \_\_set(). In this example, I construct a method name out of the property argument combined with the string, "set". The setName() method is found and duly invoked. This transforms the incoming value and stores it in a real property:

```php
$p = new Person();
$p->name = "bob";// the $myname property becomes 'BOB'
```

As you might expect, \_\_unset() mirrors \_\_set(). When unset() is called on an undefined property, \_\_unset() is invoked with the name of the property. You can then do what you like with the information. This example passes null to a method resolved using the same technique that you saw used by \_\_set():

```php
// listing 04.74    
public function __unset(string $property)    {        
    $method = "set{$property}";        
    if (method_exists($this, $method)) {            
        $this->$method(null);        
    }    
}
```

The \_\_call() method is probably the most useful of all the interceptor methods. It is invoked when an undefined method is called by client code. \_\_call() is invoked with the method name and an array holding all arguments passed by the client. Any value that you return from the \_\_call() method is returned to the client as if it were returned by the method invoked.

The \_\_call() method can be useful for delegation. Delegation is the mechanism by which one object passes method invocations on to a second. It is similar to inheritance, in that a child class passes on a method call to its parent implementation. With inheritance the relationship between child and parent is fixed, so the ability to switch the receiving object at runtime means that delegation can be more flexible than inheritance. An example clarifies things a little. Here is a simple class for formatting information from the Person class:

```php
// listing 04.75class PersonWriter {

    public function writeName(Person $p)    {        
        print $p->getName() . "\n";    
    }

    public function writeAge(Person $p)    {        
        print $p->getAge() . "\n";    
    }
}
```

I could, of course, subclass this to output Person data in various ways. Here is an implementation of the Person class that uses both a PersonWriter object and the \_\_call() method: 

```php
// listing 04.76
class Person {    
    private $writer;

    public function __construct(PersonWriter $writer)    {        
        $this->writer = $writer;    
    }

    public function __call(string $method, array $args)    {        
        if (method_exists($this->writer, $method)) {            
            return $this->writer->$method($this);        
        }    
    }

    public function getName(): string    {        
        return "Bob";    
    }    
    public function getAge(): int    {        
        return 44;    
    }
}
```

The Person class here demands a PersonWriter object as a constructor argument and stores it in a property variable. In the \_\_call() method, I use the provided \$method argument, testing for a method of the same name in the PersonWriter object I have stored. If I encounter such a method, I delegate the method call to the PersonWriter object, passing my current instance to it (in the \$this pseudo-variable). Consider what happens if the client makes this call to Person:

```php
$person = new Person(new PersonWriter());
$person->writeName();
```

In this case, the \_\_call() method is invoked. I find a method called writeName() in my PersonWriter object and invoke it. This saves me from manually invoking the delegated method like this:

```php
function writeName() {    
    $this->writer->writeName($this);
}
```

The Person class has magically gained two new methods. Although automated delegation can save a lot of legwork, there can be a cost in clarity. If you rely too much on delegation, you present the world with a dynamic interface that resists reflection (the runtime examination of class facets) and is not always clear to the client coder at first glance. This is because the logic that governs the interaction between a delegating class and its target can be obscure—buried in methods like \_\_call() rather than signaled up front by inheritance relationships or method type hints, as is the case for similar relationships. The interceptor methods have their place, but they should be used with care, and classes that rely on them should document this fact very clearly.

I will return to the topics of delegation and reflection later in the book.The \_\_get() and \_\_set() interceptor methods can also be used to manage composite properties. 

This can be a convenience for the client programmer. Imagine, for example, an Address class that manages a house number and a street name. Ultimately this object data will be written to database fields, so the separation of number and street is sensible. But if house numbers and street names are commonly acquired in undifferentiated lumps, then you might want to help the class’s user. Here is a class that manages a composite property, Address::\$streetaddress:

```php
// listing 04.77
class Address {    
    private $number;    
    private $street;

    public function __construct(string $maybenumber, string $maybestreet = null)    {        
        if (is_null($maybestreet)) {            
            $this->streetaddress = $maybenumber;        
        } else {            
            $this->number = $maybenumber;            
            $this->street = $maybestreet;        
        }    
    }

    public function __set(string $property, string $value)    {        
        if ($property === "streetaddress") {            
            if (preg_match("/^(\d+.*?)[\s,]+(.+)$/", $value, $matches)) {                
                $this->number = $matches[1];                
                $this->street = $matches[2];            
            } else {                
                throw new \Exception("unable to parse street address: '{$value}'");            
            }
        }    
    }

    public function __get(string $property)    {        
        if ($property === "streetaddress") {            
            return $this->number . " " . $this->street;        
        }    
    }
}

// listing 04.78
$address = new Address("441b Bakers Street");
print "street address: {$address->streetaddress}\n";
$address = new Address("15", "Albert Mews");
print "street address: {$address->streetaddress}\n";
$address->streetaddress = "34, West 24th Avenue";
print "street address: {$address->streetaddress}\n";
```

When a user attempts to set the (nonexistent) Address::\$streetaddress property, the interceptor method \_\_call() is invoked. There, I test for the property name, streetaddress. Before I can set the \$number and \$street properties, I must first ensure that the provided value can be parsed, and then go ahead and extract the fields. For this example, I have set simple rules. An address can be parsed if it begins with a number and has spaces or commas ahead of a second part. Thanks to back references, if the check passes, I already have the data I’m looking for in the \$matches array, and I assign values to the \$number and \$street properties. If the parse fails, I throw an exception. So when a string such as 441b Bakers Street is assigned to Address::\$streetaddress, it’s actually the \$number and \$street properties that get populated. I can demonstrate this with print_r():

```php
$address = new Address("441b Bakers Street");
print_r($address);

Address Object (    
    [number:Address:private] => 441b    
    [street:Address:private] => Bakers Street
)
```

The \_\_get() method is much more straightforward, of course. Whenever the Address::\$streetaddress property is accessed, \_\_get() is invoked. In my implementation of this interceptor, I test for streetaddress and, if I find a match, I return a concatenation of the \$number and \$street properties.

### 4.11 Defining Destructor Methods

You have seen that the \_\_construct() method is automatically invoked when an object is instantiated. PHP 5 also introduced the \_\_destruct() method. This is invoked just before an object is garbage-collected; that is, before it is expunged from memory. You can use this method to perform any final cleaning up that might be necessary.

Imagine, for example, a class that saves itself to a database when so ordered. I could use the \_\_destruct() method to ensure that an instance saves its data when it is deleted:

```php
// listing 04.79
class Person {    
    protected $name;    
    private   $age;    
    private   $id;

    public function __construct(string $name, int $age)    {        
        $this->name = $name;        
        $this->age  = $age;   
    }

    public function setId(int $id)    {        
        $this->id = $id;    
    }

    public function __destruct()    {        
        if (! empty($this->id)) {            
            // save Person data            
            print "saving person\n";        
        }    
    }
}
```

The \_\_destruct() method is invoked whenever a Person object is removed from memory. This will happen either when you call the unset() function with the object in question or when no further references to the object exist in the process. So if I create and destroy a Person object, you can see the \_\_destruct() method come into play:

```php
// listing 04.80
$person = new Person("bob", 44);
$person->setId(343);
unset($person);
// output:
// saving person
```

Although tricks like this are fun, it’s worth sounding a note of caution. \_\_call(), \_\_destruct(), and their colleagues are sometimes called magic methods. As you will know if you have ever read a fantasy novel, magic is not always a good thing. Magic is arbitrary and unexpected. Magic bends the rules. Magic incurs hidden costs.

In the case of \_\_destruct(), for example, you can end up saddling clients with unwelcome surprises. Think about the Person class—it performs a database write in its \_\_destruct() method. Now imagine a novice developer idly putting the Person class through its paces. He doesn’t spot the \_\_destruct() method, and he sets about instantiating a set of Person objects. Passing values to the constructor, he assigns the CEO’s secret and faintly obscene nickname to the \$name property, and then sets \$age at 150. He runs his test script a few times, trying out colorful name and age combinations.

The next morning, his manager asks him to step into a meeting room to explain why the database contains insulting Person data. The moral? Do not trust magic.

### 4.12 Copying Objects with \_\_clone()

In PHP 4, copying an object was a simple matter of assigning from one variable to another:

```php
class CopyMe {
}

$first = new CopyMe();
$second = $first;/
// PHP 4: $second and $first are 2 distinct objects
// PHP 5 plus: $second and $first refer to one object
```

This「simple matter」was a source of many bugs, as object copies were accidentally spawned when variables were assigned, methods were called, and objects were returned. This was made worse by the fact that there was no way of testing two variables to see whether they referred to the same object. Equivalence tests would tell you whether all fields were the same (\=\=) or whether both variables were objects (===), but not whether they pointed to the same object.

In PHP, objects are always assigned and passed around by reference. This means that when my previous example is run with PHP 5, \$first and \$second contain references to the same object instead of two copies. Although this is generally what you want when working with objects, there will be occasions when you need to get a copy of an object rather than a reference to an object.

PHP 4 的这种用法可能会引发很多 bug，因为在变量赋值、调用方法、返回对象时都常常会无意中进行对象复制，而你可能并不知道。更糟的是，我们无法检査两个变量是否指向相同的对象。等值检测只会告诉你两者是否相等（\=\=）或者两者是否相等且都是对象（\=\=\=），但不会告诉你两者是否指向同一个对象。在 PHP 中，对象的赋值和传递都是通过引用进行的。这意味着当我们之前的代码运行在 PHP 5 时，First 和 Ssecond 这两个变量包含指向同一个对象的引用，而没有各自保留一份相同的副本，这正是我们处理对象时所希望的，但有时候我们也需要获得一个对象的副本，而不是引用。

PHP provides the clone keyword for just this purpose. clone operates on an object instance, producing a by-value copy:

```php
class CopyMe {
}

$first  = new CopyMe();
$second = clone $first;
// PHP 5 plus: $second and $first are 2 distinct objects
```

The issues surrounding object copying only start here. Consider the Person class that I implemented in the previous section. A default copy of a Person object would contain the identifier (the \$id property), which in a full implementation I would use to locate the correct row in a database. If I allow this property to be copied, a client coder can end up with two distinct objects referencing the same data source, which is probably not what she wanted when she made her copy. An update in one object will affect the other, and vice versa.

Luckily, you can control what is copied when clone is invoked on an object. You do this by implementing a special method called \_\_clone() (note the leading two underscores that are characteristic of built-in methods). \_\_clone() is called automatically when the clone keyword is invoked on an object.

但这样复制对象还有问题。请回顾一下我们在上一节中实现的 Person 类。默认情况下，每个 Person 对象都会有其标识符（即 \$id 属性）。在实际开发中，\$id 属性可能会与数据库表中的某一条记录一一对应。如果允许复制 \$id 属性，那么可能会有两个完全不同的对象指向数据库中的同一条记录，这显然不是客户程序员想要的结果。此时对一个对象所做的更新会影响另一个，反之亦然。幸运的是，在对象上调用 clone 时，我们可以控制复制什么。我们可以通过实现一个特殊的方法 clone() 来达到这个目的（注意所有以两个下划线开头的方法都是 PHP 内置的方法）。当在一个对象上调用 clone 关键字时，其 \_\_clone() 方法就会被自动调用。实现 \_\_clone() 方法时，要注意当前方法执行的环境。\_\_clone() 方法是在复制得到的对象上运行的，而不是在原始对象上运行的。我们给 Person 类添加上 \_\_clone() 方法方法：

When you implement \_\_clone(), it is important to understand the context in which the method runs. \_\_clone() is run on the copied object and not the original. Here I add \_\_clone() to yet another version of the Person class:

```php
// listing 04.81
class Person {    
    private $name;

    private $age;    
    private $id;

    public function __construct(string $name, int $age)    {        
        $this->name = $name;        
        $this->age = $age;    
    }

    public function setId(int $id)    {        
        $this->id = $id;    
    }

    public function __clone()    {        
        $this->id = 0;    
    }
}
```

When clone is invoked on a Person object, a new shallow copy is made, and its \_\_clone() method is invoked. This means that anything I do in \_\_clone() overwrites the default copy I already made. In this case, I ensure that the copied object’s \$id property is set to zero:

```php
// listing 04.82
$person = new Person("bob", 44);
$person->setId(343);
$person2 = clone $person;
// $person2 :
//     name: bob
//     age: 44
//     id: 0.
```

A shallow copy ensures that primitive properties are copied from the old object to the new. Object properties, though, are copied by reference, which may not be what you want or expect when cloning an object. Say that I give the Person object an Account object property. This object holds a balance that I want copied to the cloned object. What I don’t want, though, is for both Person objects to hold references to the same account:

```php
// listing 04.83
class Account {    
    public $balance;

    public function __construct(float $balance)    {        
        $this->balance = $balance;    
    }
}

// listing 04.84
class Person {    
    private $name;    
    private $age;    
    private $id;    
    public  $account;

    public function __construct(string $name, int $age, Account $account)    {        
        $this->name = $name;        
        $this->age  = $age;        
        $this->account = $account;    
    }

    public function setId(int $id)    {        
        $this->id = $id;    
    }

    public function __clone()    {        
        $this->id   = 0;    
    }
}

// listing 04.85
$person = new Person("bob", 44, new Account(200));
$person->setId(343);
$person2 = clone $person;

// give $person some money
$person->account->balance += 10;
// $person2 sees the credit tooprint 
$person2->account->balance;
```

This gives the following output:

    210

\$person holds a reference to an Account object that I have kept publicly accessible for the sake of brevity (as you know, I would usually restrict access to a property, providing an accessor method, if necessary). When the clone is created, it holds a reference to the same Account object that \$person references. I demonstrate this by adding to the \$person object’s Account and confirming the increased balance via \$person2. If I do not want an object property to be shared after a clone operation, then it is up to me to clone it explicitly in the \_\_clone() method:

```php
function __clone()    {        
    $this->id   = 0;        
    $this->account = clone $this->account;    
}
```

如果不希望对象属性在被复制之后被共享，那么可以显式地在 \_\_clone() 方法中复制指向的对象。

1『上面显示的在  \_\_clone() 里指定规则，目前还没吃透，更达不到随心应用的地步。（2020-06-19）』

### 4.13 Defining String Values for Your Objects

Another Java-inspired feature introduced by PHP 5 was the \_\_toString() method. Before PHP 5.2, when you printed an object, it would resolve to a string like this:

```php
// listing 04.86
class StringThing{
}

// listing 04.87
$st = new StringThing();
print $st;
```

```
Object id #1

Since PHP 5.2, this code will produce an error like this:

Object of class popp\ch04\batch22\StringThing could not be converted to string ...
```

By implementing a \_\_toString() method, you can control how your objects represent themselves when printed. \_\_toString() should be written to return a string value. The method is invoked automatically when your object is passed to print or echo, and its return value is substituted. Here I add a \_\_toString() version to a minimal Person class:

```php
// listing 04.88
class Person {    
    function getName(): string    {        
        return "Bob";    
    }

    function getAge(): int    {        
        return 44;    
    }

    function __toString(): string    {        
        $desc  = $this->getName() . " (age ";        
        $desc .= $this->getAge() . ")";        
        return $desc;    
    }
}
```

Now when I print a Person object, the object will resolve to this:

```php
$person = new Person();

print $person;
```

    Bob (age 44)

The \_\_toString() method is particularly useful for logging and error reporting, as well as for classes whose main task is to convey information. The Exception class, for example, summarizes exception data in its \_\_toString() method.

对于日志和错误报告，\_\_toString() 方法非常有用。 \_\_toString() 方法也可用于设计专门用来传递信息的类，比如 Exception 类可以把关于异常数据的总结信息写到 \_\_toString() 方法中。

### 4.14 Callbacks, Anonymous Functions, and Closures

Although not strictly an object-oriented feature, anonymous functions are useful enough to mention here because you may encounter them in object-oriented applications that utilize callbacks. To kick things off, here are a couple of classes:

```php
// listing 04.89
class Product {    
    public $name;    
    public $price;

    public function __construct(string $name, float $price)    {        
        $this->name = $name;        
        $this->price = $price;    
    }
}

class ProcessSale {    
    private $callbacks;

    public function registerCallback(callable $callback)    {        
        if (! is_callable($callback)) {            
            throw new Exception("callback not callable");        
        }        
        $this->callbacks[] = $callback;    
    }

    public function sale(Product $product)    {        
        print "{$product->name}: processing \n";        
        foreach ($this->callbacks as $callback) {            
            call_user_func($callback, $product);        
        }    
    }
}
```

This code is designed to run my various callbacks. It consists of two classes, Product and ProcessSale. Product simply stores \$name and \$price properties. I’ve made these public for the purposes of brevity. Remember, in the real world, you’d probably want to make your properties private or protected and provide accessor methods. ProcessSale consists of two methods.

The first, registerCallback(), accepts an unhinted scalar, tests it, and adds it to a callback array. The test, a built-in function called is\_callable(), ensures that whatever I’ve been given can be invoked by a function such as call\_user\_func() or array\_walk().

The second method, sale(), accepts a Product object, outputs a message about it, and then loops through the \$callback array property. It passes each element to call\_user\_func(), which calls the code, passing it a reference to the product. All of the following examples will work with the framework.

Why are callbacks useful? They allow you to plug functionality into a component at runtime that is not directly related to that component’s core task. By making a component callback aware, you give others the power to extend your code in contexts you don’t yet know about.

回调为什么有用？利用回调，你可以在运行时将与组件的核心任务没有直接关系的功能插入到组件中。有了组件回调，你就赋予了其他人在你不知道的上下文中扩展你的代码的权利。

1『回调函数的好处，下面还举了个例子。如何用好回调函数一直是个短板。（2020-05-03）』

Imagine, for example, that a future user of ProcessSale wants to create a log of sales. If the user has access to the class, she might add logging code directly to the sale() method. This isn’t always a good idea, though. If she is not the maintainer of the package that provides ProcessSale, then her amendments will be overwritten the next time the package is upgraded. Even if she is the maintainer of the component, adding many incidental tasks to the sale() method will begin to overwhelm its core responsibility, and potentially make it less usable across projects. I will return to these themes in the next section.

例如，假设 ProcessSale 类的一个用户想创建一条销售记录。如果该用户可以访问该类，那么他可能会直接在 sale() 方法中添加记录代码，但有时这种做法并不好。如果他不是 ProcessSale 类所在的包的维护者，那么他对该方法的修改会在下次更新包时被覆盖。即使他是该组件的维护者，向 sale() 方法中添加那么多附加的任务也是本末倒置，无法体现该方法的核心功能，这可能会导致该方法跨项目的可用性降低。

Luckily, though, I made ProcessSale callback-aware. Here I create a callback that simulates logging:

```php
// listing 04.90
$logger = create_function(    
    '$product',    
    'print "    logging ({$product->name})\n";'
);

$processor = new ProcessSale();
$processor->registerCallback($logger);

$processor->sale(new Product("shoes", 6));
print "\n";
$processor->sale(new Product("coffee", 6));
```

I use create\_function() to build my callback. As you can see, it accepts two string arguments: first, a list of parameters; and second, the function body. The result is often called an anonymous function as it’s not named in the manner of a standard function. Instead, it can be stored in a variable and passed to functions and methods as a parameter. That’s just what I do, storing the function in the \$logger variable and passing it to ProcessSale::registerCallback(). Finally, I create a couple of products and pass them to the sale() method. You have already seen what happens there. The sale is processed (in reality a simple message is printed about the product) and any callbacks are executed. Here is the code in action:

我使用 create\_function() 创建回调。你可以看到，它的参数是两个字符串。首先是一个参数列表，接着是函数体。结果通常被称为匿名函数，因为它没有以标准函数的方式命名，但它可被存储在一个变量中，作为参数传递给函数和方法。这就是我所做的：将函数存储在 \$logger 变量中，然后将其传递给 ProcessSale::registerCallback()。最后创建了两个产品并将其传递给 sale() 方法。你已经看到了所发生的事情，处理销售记录（实际上是输出与该产品有关的条简单的消息），并且执行所有回调。

```
shoes: processing    logging (shoes)
coffee: processing    logging (coffee)
```

1『

两个问题，首先 create_function() 已经被废弃了，直接用匿名函数。其次，\$callbacks 必须申明为空数组。

```php
class Product {
    public $name;
    public $price;

    public function __construct(string $name, float $price) {
        $this->name = $name;
        $this->price = $price;
    }
}

class ProcessSale {
    private $callbacks = [];

    public function registerCallback(callable $callback) {
        if (! is_callable($callback)) {
            throw new Exception("callback not callable");
            $this->callbacks[] = $callback;
        }
    }

    public function sale(Product $product) {
        print "{$product->name}: processing \n";
        foreach ($this->callbacks as $callback) {
            call_user_func($callback, $product);
        }
    }
}

$logger = function($product) {
    print "logging({$product->name})\n";
};

$processor = new ProcessSale();
$processor->registerCallback($logger);
$processor->sale(new Product("shoes", 6));
print "\n";
$processor->sale(new Product("coffee", 6));
print "\n";
```

还是不对，发现「\$processor->registerCallback(\$logger);」压根没调用，待解决。回复：解决了，是自己把「\$this->callbacks[] = \$callback;」写到条件语句里面去了，拿出来即可，而且修正后 \$callbacks 就不需要赋值为空数组了。（2020-06-19）

```php
    public function registerCallback(callable $callback) {
        if (! is_callable($callback)) {
            throw new Exception("callback not callable");
        } 
        $this->callbacks[] = $callback;
    }
```

』

Look again at that create\_function() example. See how ugly it is? Placing code designed to be executed inside a string is always a pain. You need to escape variables and quotation marks, and, if the callback grows to any size, it can be very hard to read, indeed. Wouldn’t it be neater if there were a more elegant way of creating anonymous functions? Well, since PHP 5.3, there is a much better way of doing it. You can simply declare and assign a function in one statement. Here’s the previous example using the new syntax:

再来看一下 create\_function() 这个例子。看看它有多难看。将要执行的代码放在一个字符串中是水远的痛。你需要转义变量和引号，并且如果回调达到了一定的大小，实际上它会变得」分难读。如果能找到一种优雅的方式来创建匿名函数，这个例子不就能变得整洁一些了吗？PHP5.3 及其后续版本提供了更好的方法来实现该功能。你可以简单地在一条语句中声明并分配函数。使用了新语法后的 Create_ function（）示例如下所示：

```php
// listing 04.91
$logger2 = function ($product) {    
    print "    logging ({$product->name})\n";
};

$processor = new ProcessSale();
$processor->registerCallback($logger2);

$processor->sale(new Product("shoes", 6));
print "\n";
$processor->sale(new Product("coffee", 6));
```

The only difference here lies in the creation of the anonymous function. As you can see, it’s a lot neater. I simply use the function keyword inline, and without a function name. Note that because this is an inline statement, a semicolon is required at the end of the code block. The output here is the same as that of the previous example.

1『确实，匿名函数后面有个分号。』

1『哇塞，这里看到了内联语句 inline statement，正好加深了对「重构」里内联函数的理解。』

Of course, callbacks needn’t be anonymous. You can use the name of a function, or even an object reference and a method, as a callback. Here I do just that:

```php
// listing 04.92
class Mailer{    
    public function doMail(Product $product)    {        
        print "    mailing ({$product->name})\n";    
    }
}

// listing 04.93
$processor = new ProcessSale();
$processor->registerCallback([new Mailer(), "doMail"]);

$processor->sale(new Product("shoes", 6));
print "\n";
$processor->sale(new Product("coffee", 6));
```

I create a class: Mailer. Its single method, doMail(), accepts a Product object and outputs a message about it. When I call registerCallback(), I pass it an array. The first element is a Mailer object, and the second is a string that matches the name of the method I want invoked. Remember that registerCallback() checks its argument for callability. is\_callable() is smart enough to test arrays of this sort. A valid callback in array form should have an object as its first element, and the name of a method as its second element. I pass that test here, and here is my output:

我创建了 Mailer 类，该类只有一个方法 doMail()，接受 Product 对象并输出与该对象有关的一条消息。调用 registerCallback() 时，我传递给它一个数组。数组的第一个元素是 Mailer 对象，第二个元素是字符串（该字符串与我想要调用的方法的名称匹配）。记住，registerCallback() 会检查其参数的可调用性。is\_callable() 非常智能，能够测试这类数组。数组形式的有效回调应该以对象作为其第一个元素，以方法名作为其第二个元素。

```
shoes: processing    
    mailing (shoes)

coffee: processing    
    mailing (coffee)
```

You can have a method return an anonymous function—something like this:

```php
// listing 04.94
class Totalizer {    
    public static function warnAmount()    {        
        return function (Product $product) {            
            if ($product->price > 5) {                
                print "    reached high price: {$product->price}\n";            
            }        
        };    
    }
}

// listing 04.95
$processor = new ProcessSale();
$processor->registerCallback(Totalizer::warnAmount());
// ...
```

Apart from the convenience of using the warnAmount() method as a factory for the anonymous function, I have not added much of interest here. But this structure allows me to do much more than just generate an anonymous function. It allows me to take advantage of closures. The new style anonymous functions can reference variables declared in the anonymous functions parent scope. This is a hard concept to grasp at times. It’s as if the anonymous function continues to remember the context in which it was created. Imagine that I want Totalizer::warnAmount() to do two things. First of all, I’d like it to accept an arbitrary target amount. Second, I want it to keep a tally of prices as products are sold. When the total exceeds the target amount, the function will perform an action (in this case, as you might have guessed, it will simply write a message).

I can make my anonymous function track variables from its wider scope with a use clause:

除了使用 warnAmount() 作为匿名函数的工厂方法很方便之外，这里没有什么有趣的内容了。但除了生成匿名函数之外，利用该结构还可以做更多的事情，比如利用闭包。这些新风格的匿名函数可以引用在其父作用域中声明的变量。这个概念有时候很难理解。打个比方来说，就好像匿名函数还记得它被创建时所在的作用域。假设我想让 Totalizer::warnAmount() 做两件事：首先是让它接受一个随机的目标金额；其次是记录售出产品的总价格。当总价格超出目标金额时，让该函数执行一项操作（你可能猜到了，在本例中就是输出一条消息）。利用 use 子句，就可以让匿名函数追踪来自其父作用域的变量：

```php
// listing 04.96
class Totalizer2 {    
    public static function warnAmount($amt)    {        
        $count=0;        
        return function ($product) use ($amt, &$count) {            
            $count += $product->price;            
            print "   count: $count\n";            
            if ($count > $amt) {                
                print "   high price reached: {$count}\n";            
            }        
        };    
    }
}

// listing 04.97
$processor = new ProcessSale();
$processor->registerCallback(Totalizer2::warnAmount(8));

$processor->sale(new Product("shoes", 6));
print "\n";
$processor->sale(new Product("coffee", 6));
```

The anonymous function returned by Totalizer2::warnAmount() specifies two variables in its use clause. The first is \$amt. This is the argument that warnAmount() accepted. The second closure variable is \$count. \$count is declared in the body of warnAmount() and set initially to zero. Notice that I prepend an ampersand to the \$count variable in the use clause. This means the variable will be accessed by reference rather than by value in the anonymous function. In the body of the anonymous function, I increment \$count by the product’s value, and then test the new total against \$amt. If the target value has been reached, I output a notification. Here is the code in action:

Totalizer2::warnAmount() 返回的匿名函数在其 use 子句中指定了两个变量：第一个变量是 \$amt，它是 warnAmount() 的实参；第二个闭包变量是 \$count。\$count 在 warnAmount() 函数体中声明，初始值为 0。注意，在 use 子句中我在 \$count 变量前面加了一个 &。这意味着该变量可以用匿名函数中的引用而不是值来访问。在匿名函数的函数体中，我为 \$count 增加了产品的价格（\$product 的值），然后测试新的总计值是否超过 \$amt。如果已经达到目标值，就输出一个通知。

1『上面的代码对理解匿名函数、闭包的概念帮助很大，需要反复研读。』

```
shoes: processing   
    count: 6

coffee: processing   
    count: 12

   high price reached: 12
```

This demonstrates that the callback is keeping track of \$count between invocations. Both \$count and \$amt remain associated with the function because they were present to the context of its declaration and because they were specified in its use clause.

这段代码说明了回调跟踪了两次调用之间的 \$count。\$count 和 \$amt 仍然和函数相关，因为它们出现在声明时所在的作用域中，并且在 use 子句中指定。

### 4.15 Anonymous Classes

As of PHP 7 you can declare anonymous classes as well as functions. These are especially useful when you need to create and derive an instance from a small class. This is especially useful when the class in question is simple and specific to the local context. Let’s return to our PersonWriter example. I’ll start off by creating an interface this time:

```php
// listing 04.98
interface PersonWriter {    
    public function write(Person $person);
}
```

Now, here’s a version of the Person class that can use a PersonWriter object:

```php
// listing 04.99
class Person {    
    public function output(PersonWriter $writer)    {        
        $writer->write($this);    
    }

    public function getName(): string    {        
        return "Bob";    
    }

    public function getAge(): int    {        
        return 44;    
    }
}
```

The output() method accepts a PersonWriter instance, and then passes an instance of the current class to its write() method. In this way, the Person class is nicely insulated from the implementation of the writer. Moving on to client code, if we need a writer to print name and age values for a Person object, we might go ahead and create a class in the usual way. But it’s such a trivial implementation that we could equally create a class and pass it to Person at the same time:

```php
// listing 04.100        
$person = new Person();        
$person->output (            
    new class implements PersonWriter {                
        public function write(Person $person) {                    
            print $person->getName(). " " . $person->getAge() . "\n";                
        }            
    }        
);
```

As you can see, you can declare an anonymous class with the keywords, new class. You can then add any extends and implements clauses required before creating the class block.

Anonymous classes do not support closures. In other words, variables declared in a wider scope cannot be accessed within the class. However you can pass values to an anonymous class’s constructor. Let’s create a slightly more complex PersonWriter:

```php
// listing 04.101        
$person = new Person();        
$person->output(            
    new class("/tmp/persondump") implements PersonWriter {                
        private $path;

        public function __construct(string $path) {                    
            $this->path = $path;                
        }

        public function write(Person $person) {                     
            file_put_contents($this->path, $person->getName(). " " . $person 
            ->getAge() . "\n");
       }            
    }        
);
```

I passed a path argument to the constructor. This value was stored in the \$path property and eventually used by the write() method. Of course, if your anonymous class begins to grow in size and complexity, it becomes more sensible to create a named class in a class file. This is especially true if you find yourself duplicating your anonymous class in more than one place.

1『匿名类不支持闭包，匿名类的这块知识还没吃透。（2020-06-19）』

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

1『小细节知识，__ DIR__ 可直接获取当前文件所在的路径，赞。』

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

2『注意，这里的代码有正则的代码，PHP 的正则语法抽时间学习下，哈哈。』

 ■ Note: illustrative code always involves a difficult balancing act. it needs to be clear enough to make its point, which often means sacrificing error checking and fitness for its ostensible purpose. in other words, the example here is really intended to illustrate issues of design and duplication rather than the best way to parse and write file data. For this reason, I omit implementation where it is not relevant to the issue at hand.

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

 ■ Note: placing a static method for generating child objects in the parent class is convenient. such a design decision has its own consequences, however. the ParamHandler type is now essentially limited to working with the concrete classes in this central conditional statement. What happens if you need to handle another format? Of course, if you are the maintainer of ParamHandler, you can always amend the getInstance() method. if you are a client coder, however, changing this library class may not be so easy (in fact, changing it won’t be hard, but you face the prospect of having to reapply your patch every time you reinstall the package that provides it). I will discuss issues of object creation in Chapter 9.

1『在父类里设置一个静态方法来构建子类的对象，是一个不错的方法，但这种生成「对象」的方法还能再优化。再优化的方法应该是用设计模式中的「工厂方法」。（2020-07-13）』

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

```php
// listing 06.08

$test = ParamHandler::getInstance(__DIR__ . "/params.txt");
$test->read(); // reading in text format
$params = $test->getAllParams();
print_r($params);
```

So, what can we learn from these two approaches?

1『当然是第二种用「对象」来实现的方法更简单了。（2020-07-13）』

#### 6.2.1 Responsibility

The controlling code in the procedural example takes responsibility for deciding about format—not once, but twice. The conditional code is tidied away into functions, certainly, but this merely disguises the fact of a single flow, making decisions as it goes. Calls to readParams() and to writeParams() take place in different contexts, so we are forced to repeat the file extension test in each function (or to perform variations on this test().

1『很有道理，写和读其实是 2 个行为，读的时候其实是没必要检测扩展名的，但在面向过程的代码里，每次进行「写」和「读」的行为前，必须进行文件名的扩展检测，是一种重复。（2020-07-13）』

In the object-oriented version, this choice about file format is made in the static getInstance() method, which tests the file extension only once, serving up the correct subclass. The client code takes no responsibility for implementation. It uses the provided object with no knowledge of, or interest in, the particular subclass it belongs to. It knows only that it is working with a ParamHandler object, and that it will support write() and read(). While the procedural code busies itself about details, the object-oriented code works only with an interface, unconcerned about the details of implementation. Because responsibility for implementation lies with the objects and not with the client code, it would be easy to switch in support for new formats transparently.

在过程式编程的例子中，控制代码的职责是判断文件格式，它判断了两次而不是一次。条件语句被绑定到函数中，但这仅是将判断的流程隐藏起来。对 readparams() 的调用和对 writeparams() 的调用必须发生在不同的地方，因此我们不得不在每个函数中重复检测文件扩展名（或执行其他检测操作）。在面向对象代码中，我们在静态方法 getinstance() 中进行文件格式的选择，并且仅在 getinstance() 中检测文件扩展名一次，就可以决定使用哪一个合适的子类。客户端代码并不负责实现读写功能。它不需要知道自己属于哪个子类就可以使用给定的对象。它只需要知道自己正在使用 Paramhandler 对象，并且 Paramhandler 对象支持 write() 和 read() 方法。过程式代码忙于处理细节，而面向对象代码只需一个接口即可工作，并且不用考虑实现的细节。由于实现由对象负责，而不是由客户端代码负贵，所以我们能够很方便地增加对新格式的支持。

2『实现由对象负责，而非由客户端（父类，父类只提供接口），这句话醍醐灌顶。把上面的内容放进「面向过程与面向对象」主题卡里。』——已完成

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

2『 The Pragmatic Programmer 这本书已经出新版了，已下载「2020120The-Pragmatic-Programmer2Ed」。正交的概念做一张术语卡片。』——已完成

### 6.3 Choosing Your Classes

It can be surprisingly difficult to define the boundaries of your classes, especially as they will evolve with any system that you build.

1『确实，界定类的边界，即如何抽象出模型是最难的。（2020-07-13）』

It can seem straightforward when you are modeling the real world. Object-oriented systems often feature software representations of real things—Person, Invoice, and Shop classes abound. This would seem to suggest that defining a class is a matter of finding the things in your system and then giving them agency through methods. This is not a bad starting point, but it does have its dangers. If you see a class as a noun, a subject for any number of verbs, then you may find it bloating as ongoing development and requirement changes call for it to do more and more things.

模拟真实世界是比较直接的办法。面向对象系统经常反映真实的事物 Person、Invoice 和 shop 类等，即定义一个类就是找到系统中的事物，然后通过方法给予它们动作。这个想法不错，但也有不足之处。如果把类看做名词：一系列动作的执行者，那么随着开发和需求的改变，你会发现它因为需要而做越来越多的事情。

Let’s consider the ShopProduct example that we created in Chapter 3. Our system exists to offer products to a customer, so defining a ShopProduct class is an obvious choice. But is that the only decision we need to make? We provide methods such as getTitle() and getPrice() for accessing product data. When we are asked to provide a mechanism for outputting summary information for invoices and delivery notes, it seems to make sense to define a write() method. When the client asks us to provide the product summaries in different formats, we look again at our class. We duly create writeXML() and writeHTML() methods in addition to the write() method. Or we add conditional code to write() to output different formats, according to an option flag.

Either way, the problem here is that the ShopProduct class is now trying to do too much. It is struggling to manage strategies for display, as well as for managing product data.

我们回顾一下在第 3 章中创建的 ShopProduct。系统为了给顾客提供产品，因此要定义一个 ShopProduct 类，但是这是唯一的办法吗？为了访问产品数据，我们需要提供诸如 getTitle() 和 getPrice() 等方法。当我们需要输出发票和提货单的摘要信息时，需要定义 write() 方法。当顾客要求得到不同格式的产品摘要信息时，除了创建 write() 方法之外，还要创建 writeXML() 和 writeHTML() 方法。否则，需要增加条件代码到 write() 中并根据选项标志输出不同格式。无论哪一种方式，ShopProduct 类现在做了太多的事情。它忙着管理显示方案及产品数据。

How should you think about defining classes? The best approach is to think of a class as having a primary responsibility and to make that responsibility as singular and focused as possible. Put the responsibility into words. It has been said that you should be able to describe a class’s responsibility in 25 words or less, rarely using the words「and」or「or」. If your sentence gets too long or mired in clauses, it is probably time to consider defining new classes along the lines of some of the responsibilities you have described.

So, ShopProduct classes are responsible for managing product data. If we add methods for writing to different formats, we begin to add a new area of responsibility: product display. As you saw in Chapter 3, we actually defined two types based on these separate responsibilities. The ShopProduct type remained responsible for product data, and the ShopProductWriter type took on responsibility for displaying product information. Individual subclasses refined these responsibilities.

2『如何定义类，做一张任意卡片。』——已完成

我们应该如何定义类呢？最好的办法是让一个类只有一个主要的职责，并且任务要尽可能独立。你可以把类的职责用多个词来形容，最好不超过 25 个词，不要用到词「且」或者「或」。如果句子太长或者有复杂的子句，就应该考虑用你所描述的一部分任务来定义新类。因此，ShopProduct 类应该主要负责处理产品数据。如果我们显示不同格式的摘要信息，则有了一个新的职责：产品显示。正如第 3 章所述，我们实际上基于这两个不同的职责定义了两个类型：ShopProduct 类型负责处理产品数据；ShopProductWriter 类型负责显示产品信息。每个类只承担自己的任务。

 ■ Note:  Very few design rules are entirely inflexible. You will sometimes see code for saving object data in an otherwise unrelated class, for example. although this would seem to violate the rule that a class should have a singular responsibility, it can be the most convenient place for the functionality to live because a method has to have full access to an instance’s fields. Using local methods for persistence can also save us from creating a parallel hierarchy of persistence classes mirroring our savable classes, and thereby introducing unavoidable coupling. We deal with other strategies for object persistence in Chapter 12. avoid religious adherence to design rules; they are not a substitute for analyzing the problem before you. try to remain alive to the reasoning behind the rule, and emphasize that over the rule itself.

1『说到心坎里去了，无招胜有招，哈哈。』

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

1『多态只是把条件语句集中封装到了一个地方。』

As you have seen, PHP enforces the interfaces defined by abstract classes. This is useful because we can be sure that a concrete child class will support exactly the same method signatures as those defined by an abstract parent. This includes type declarations and access controls. Client code can, therefore, treat all children of a common superclass interchangeably (as long it only relies on only functionality defined in the parent).

就像我们看到的那样，PHP 强制接口由抽象类定义。这非常有用，因为我们可以确定子类将会实现抽象父类中定义的所有方法，包括类类型提示和方法的访问控制。客户端代码因此可以使用一个公共父类的任意子类而不需要改写代码（只要客户端代码仅依赖于父类中定义的功能）。这个规则唯一的缺憾是：无法强制规定类方法返回的数据类型。

1『 PHP 7 已经支持返回特定的数据类型了。（2020-06-30）』

### 6.5 Encapsulation

Encapsulation simply means the hiding of data and functionality from a client. And once again, it is a key object-oriented concept.

On the simplest level, you encapsulate data by declaring properties private or protected. By hiding a property from client code, you enforce an interface and prevent the accidental corruption of an object’s data. Polymorphism illustrates another kind of encapsulation. By placing different implementations behind a common interface, you hide these underlying strategies from the client. This means that any changes that are made behind this interface are transparent to the wider system. You can add new classes or change the code in a class without causing errors. The interface is what matters, not the mechanisms working beneath it. The more independent these mechanisms are kept, the less chance that changes or repairs will have a knock-on effect in your projects.

要实现封装，最简单的办法是将属性定义为 private 或 protected。通过对客户端代码隐藏属性，我们创建了一个接口并防止在偶然情况下污染对象中的数据。多态是另外一种封装。通过把不同的实现放在公共接口之后，我们对客户端代码隐藏了功能的实现。也就是说，任何在接口背后发生的改变对外界的系统来说都是可忽略的。我们可以增加新类或改变类中的代码，而不会产生错误。接口与其背后的工作机制是分开来的。这些机制越独立，改进或修正代码对系统的影响越小。

1『确实，多态也是一种封装，客户端看到的只是「接口」，而接口的实现他是看不到的，即使实现换了一个方法，对客户端来说，没感觉。接口用来分割「变」与「不变」，不变的东西抽象成接口，放到一个父类里，即袁英杰在其文章「小类大对象」中的小类。而变的东西，放到具体的实现里，对应于「大对象」。』

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

1『细节知识，用 \$prod instanceof CdProduct 语句，来判断传进来的参数术语哪个类，开发数据流（暖通全面通风）时就用到该知识点。』

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
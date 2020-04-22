# 2020082PHP-Objects-Patterns-PracticeR02

## 记忆时间

## 模板

### 1. 逻辑脉络

用自己的话总结主题，梳理逻辑脉络，也就是这本书整个地图里这一章所在的节点。

### 2. 摘录及评论

## 04. Advanced Features

You have already seen how class type hinting and access control give you more control over a class’s interface. In this chapter, I will delve deeper into PHP’s object-oriented features. This chapter will cover several subjects: 1) Static methods and properties: Accessing data and functionality through classes rather than objects. 2) Abstract classes and interfaces: Separating design from implementation. 3) Traits: Sharing implementation between class hierarchies. 4) Error handling: Introducing exceptions. 5) Final classes and methods: Limiting inheritance. 6) Destructor methods: Cleaning up after your objects. 7) Interceptor methods: Automating delegation. 8) Cloning objects: Making object copies. 9) Resolving objects to strings: Creating a summary method. 10) Callbacks: Adding functionality to components with anonymous functions and classes.

In this chapter, we came to grips with PHP’s advanced object-oriented features. Some of these will become familiar as you work through the book. In particular, I will return frequently to abstract classes, exceptions, and static methods. In the next chapter, I take a step back from built-in object features and look at classes and functions designed to help you work with objects.

### 01. Static Methods and Properties

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

```php
print StaticExample::$aNum;
StaticExample::sayHello();
```

This syntax should be familiar from the previous chapter. I used :: in conjunction with parent to access an overridden method. Now, as then, I am accessing class rather than object data. Class code can use the parent keyword to access a superclass without using its class name. To access a static method or property from within the same class (rather than from a child), I would use the self keyword. self is to classes what the \$this pseudo-variable is to objects. So from outside the StaticExample class, I access the \$aNum property using its class name:

    StaticExample::$aNum;

From within the StaticExample class, I can use the self keyword:

```
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


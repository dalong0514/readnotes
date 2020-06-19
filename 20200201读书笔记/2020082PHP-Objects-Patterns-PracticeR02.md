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

## 0106. Object-Oriented PHP

This chapter explains concepts of object-oriented (OO) development and shows how they can be implemented in PHP. PHP’s OO implementation has all the features you would expect in a fully object-oriented language. We point out each of these features as we go through this chapter. Key topics covered in this chapter include: 1) Object-oriented concepts. 2) Classes, attributes, and operations. 3) Class attributes. 4) Per-class constants. 5) Class method invocation. 6) Inheritance. 7) Access modifiers. 8) Static methods. 9) Type hinting. 10) Late static bindings. 11) Object cloning. 12) Abstract classes. 13) Class design. 14) Implementation of your design. 15) Advanced OO functionality.

The next chapter explains PHP’s exception handling capabilities. Exceptions provide an elegant mechanism for dealing with runtime errors.

### 6.1 Understanding Object-Oriented Concepts

Modern programming languages usually support or even require an object-oriented approach to software development. Object-oriented development attempts to use the classifications, relationships, and properties of the objects in the system to aid in program development and code reuse.

#### 6.1.1 Classes and Objects

In the context of OO software, an object can be almost any item or concept—a physical object such as a desk or a customer; or a conceptual object that exists only in software, such as a text input area or a file. Generally, you will be most interested in objects, including both real-world objects and conceptual objects, that need to be represented in software.

Object-oriented software is designed and built as a set of self-contained objects with both attributes and operations that interact to meet your needs. Attributes are properties or variables that relate to the object. Operations are methods, actions, or functions that the object can perform to modify itself or perform for some external effect. (You will hear the term attribute used interchangeably with the terms member variable and property, and the term operation used interchangeably with method.)

Object-oriented software’s central advantage is its capability to support and encourage  encapsulation—also known as data hiding. Essentially, access to the data within an object is available only via the object’s operations, known as the interface of the object.

An object’s functionality is bound to the data it uses. You can easily alter the details controlling how the object is implemented to improve performance, add new features, or fix bugs without having to change the interface. Changing the interface could have ripple effects throughout the project, but encapsulation allows you to make changes and fix bugs without your actions cascading to other parts of the project.

In other areas of software development, object orientation is the norm, and procedural or function-oriented software is considered old fashioned. However, many web applications are still designed and written using an ad hoc approach following a function-oriented methodology.

A number of reasons for using this approach exist. Many web projects are relatively small and straightforward. You can get away with picking up a saw and building a wooden spice rack without planning your approach, and you can successfully complete the majority of web software projects in the same way because of their small size. However, if you picked up a saw and attempted to build a house without formal planning, you wouldn’t get quality results, if you got results at all. The same is true for large software projects.

Many web projects evolve from a set of hyperlinked pages into a complex application. Complex applications, whether presented via dialog boxes and windows or via dynamically generated HTML pages, need a properly thought-out development methodology. Object orientation can help you to manage the complexity in your projects, increase code reusability, and thereby reduce maintenance costs.

In OO software, an object is a unique and identifiable collection of stored data and operations that operate on that data. For instance, you might have two objects that represent buttons. Even if both have a label「OK,」a width of 60 pixels, a height of 20 pixels, and any other attributes that are identical, you still need to be able to deal with one button or the other. In software, separate variables act as handles (unique identifiers) for the objects.

Objects can be grouped into classes. Classes represent a set of objects that might vary from individual to individual, but must have a certain amount in common. A class contains objects that all have the same operations behaving in the same way and the same attributes representing the same things, although the values of those attributes vary from object to object.

You can think of the noun bicycle as a class of objects describing many distinct bicycles with many common features or attributes—such as two wheels, a color, and a size—and operations, such as move. My own bicycle can be thought of as an object that fits into the class bicycle. It has all the common features of all bicycles, including a move operation that behaves the same as most other bicycles move—even if it is used more rarely. My bicycle’s attributes have unique values because my bicycle is green, and not all bicycles are that color.

#### 6.1.2 Polymorphism

An object-oriented programming language must support polymorphism, which means that different classes can have different behaviors for the same operation. If, for instance, you have a class car and a class bicycle, each can have different move operations. For real-world objects, this would rarely be a problem. Bicycles are not likely to become confused and start using a car’s move operation instead. However, a programming language does not possess the common sense of the real world, so the language must support polymorphism to know which move operation to use on a particular object.

Polymorphism is more a characteristic of behaviors than it is of objects. In PHP, only member functions of a class can be polymorphic. A real-world comparison is that of verbs in natural languages, which are equivalent to member functions. Consider the ways a bicycle can be used in real life. You can clean it, move it, disassemble it, repair it, or paint it, among other things.

1『只有类里的成员函数可以多态，成员函数类比于语言里的动词，很赞。』

These verbs describe generic actions because you don’t know what kind of object is being acted on. (This type of abstraction of objects and actions is one of the distinguishing characteristics of human intelligence.)

For example, moving a bicycle requires completely different actions from those required for moving a car, even though the concepts are similar. The verb move can be associated with a particular set of actions only after the object acted on is made known.

#### 6.1.3 Inheritance

Inheritance allows you to create a hierarchical relationship between classes using subclasses. A subclass inherits attributes and operations from its superclass. For example, car and bicycle have some things in common. You could use a class vehicle to contain the things such as a color attribute and a move operation that all vehicles have, and then let the car and bicycle classes inherit from vehicle. You will hear subclass, derived class, and child used interchangeably. Similarly, you will hear superclass and parent used interchangeably.

With inheritance, you can build on and add to existing classes. From a simple base class, you can derive more complex and specialized classes as the need arises. This capability makes your code more reusable, which is one of the important advantages of an object-oriented approach.

Using inheritance might save you work if operations can be written once in a superclass rather than many times in separate subclasses. It might also allow you to more accurately model  real-world relationships. If a sentence about two classes makes sense with「is a」between the classes, inheritance is probably appropriate. The sentence「a car is a vehicle」makes sense, but the sentence「a vehicle is a car」does not make sense because not all vehicles are cars. Therefore, car can inherit from vehicle.





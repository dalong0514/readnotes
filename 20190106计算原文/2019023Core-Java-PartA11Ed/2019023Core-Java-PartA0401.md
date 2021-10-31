## 0401. Objects and Classes

In this chapter:

4.1 Introduction to Object-Oriented Programming

4.2 Using Predefined Classes

4.3 Defining Your Own Classes

4.4 Static Fields and Methods

4.5 Method Parameters

4.6 Object Construction

4.7 Packages

4.8 JAR Files

4.9 Documentation Comments

4.10 Class Design Hints

In this chapter, we Introduce you to object-oriented programming;

Show you how you can create objects that belong to classes from the standard Java library; and Show you how to write your own classes.

If you do not have a background in object-oriented programming, you will want to read this chapter carefully. Object-oriented programming requires a different way of thinking than procedural languages. The transition is not always easy, but you do need some familiarity with object concepts to go further with Java.

For experienced C++ programmers, this chapter, like the previous chapter, presents familiar information; however, there are enough differences between the two languages that you should read the later sections of this chapter carefully. You'll find the C++ notes helpful for making the transition.

这一章将主要介绍如下内容：

1、面向对象程序设计。

2、如何创建标准 Java 类库中的类对象。

3、如何编写自己的类。

如果你没有面向对象程序设计的应用背景，就一定要认真地阅读一下本章的内容。面向对象程序设计与面向过程程序设计在思维方式上存在着很大的差别。改变一种思维方式并不是一件很容易的事情，而且为了继续学习 Java 也要清楚对象的概念。对于具有使用 C++ 经历的程序员来说，与上一章相同，对本章的内容不会感到太陌生，但这两种语言还是存在着很多不同之处，所以要认真地阅读本章的后半部分内容，你将发现「C++ 注释」对学习 Java 语言会很有帮助。

### 4.1 Introduction to Object-Oriented Programming

Object-oriented programming, or OOP for short, is the dominant programming paradigm these days, having replaced the「structured」or procedural programming techniques that were developed in the 1970s. Since Java is object-oriented, you have to be familiar with OOP to become productive with Java.

An object-oriented program is made of objects. Each object has a specific functionality, exposed to its users, and a hidden implementation. Many objects in your programs will be taken「off-the-shelf」from a library; others will be custom-designed. Whether you build an object or buy it might depend on your budget or time. But, basically, as long as an object satisfies your specifications, you don't care how the functionality is implemented.

Traditional structured programming consists of designing a set of procedures (or algorithms) to solve a problem. Once the procedures are determined, the traditional next step was to find appropriate ways to store the data. This is why the designer of the Pascal language, Niklaus Wirth, called his famous book on programming Algorithms + Data Structures = Programs (Prentice Hall, 1975). Notice that in Wirth's title, algorithms come first, and data structures second. This reflects the way programmers worked at that time. First, they decided on the procedures for manipulating the data; then, they decided what structure to impose on the data to make the manipulations easier. OOP reverses the order: puts the data first, then looks at the algorithms to operate on the data.

For small problems, the breakdown into procedures works very well. But objects are more appropriate for larger problems. Consider a simple web browser. It might require 2,000 procedures for its implementation, all of which manipulate a set of global data. In the object-oriented style, there might be 100 classes with an average of 20 methods per class (see Figure 4.1). This structure is much easier for a programmer to grasp. It is also much easier to find bugs in. Suppose the data of a particular object is in an incorrect state. It is far easier to search for the culprit among the 20 methods that had access to that data item than among 2,000 procedures.

Figure 4.1 Procedural vs. OO programming

4.1 面向对象程序设计概述

面向对象程序设计（简称 OOP）是当今主流的程序设计范型，它已经取代了 20 世纪 70 年代的「结构化」过程化程序设计开发技术。Java 是完全面向对象的，必须熟悉 OOP 才能够编写 Java 程序。面向对象的程序是由对象组成的，每个对象包含对用户公开的特定功能部分和隐藏的实现部分。程序中的很多对象来自标准库，还有一些是自定义的。究竟是自己构造对象，还是从外界购买对象完全取决于开发项目的预算和时间。但是，从根本上说，只要对象能够满足要求，就不必关心其功能的具体实现过程。在 OOP 中，不必关心对象的具体实现，只要能够满足用户的需求即可。

传统的结构化程序设计通过设计一系列的过程（即算法）来求解问题。一旦确定了这些过程，就要开始考虑存储数据的方式。这就是 Pascal 语言的设计者 Niklaus Wirth 将其著作命名为《算法 + 数据结构 = 程序》（Algorithms + Data Structures = Programs，Prentice Hall，1975）的原因。需要注意的是，在 Wirth 命名的书名中，算法是第一位的，数据结构是第二位的，这就明确地表述了程序员的工作方式。首先要确定如何操作数据，然后再决定如何组织数据，以便于数据操作。而 OOP 却调换了这个次序，将数据放在第一位，然后再考虑操作数据的算法。对于一些规模较小的问题，将其分解为过程的开发方式比较理想。而面向对象更加适用于解决规模较大的问题。要想实现一个简单的 Web 浏览器可能需要大约 2000 个过程，这些过程可能需要对一组全局数据进行操作。采用面向对象的设计风格，可能只需要大约 100 个类，每个类平均包含 20 个方法（如图 4-1 所示）。后者更易于程序员掌握，也容易找到 bug。假设给定对象的数据出错了，在访问过这个数据项的 20 个方法中查找错误要比在 2000 个过程中查找容易得多。

图 4-1 面向过程与面向对象的程序设计对比

#### 4.1.1 Classes

A class is the template or blueprint from which objects are made. Think of classes as cookie cutters; objects are the cookies themselves. When you construct an object from a class, you are said to have created an instance of the class.

As you have seen, all code that you write in Java is inside a class. The standard Java library supplies several thousand classes for such diverse purposes as user interface design, dates and calendars, and network programming. Nonetheless, in Java you still have to create your own classes to describe the objects of your application's problem domain.

Encapsulation (sometimes called information hiding) is a key concept in working with objects. Formally, encapsulation is simply combining data and behavior in one package and hiding the implementation details from the users of the object. The bits of data in an object are called its instance fields, and the procedures that operate on the data are called its methods. A specific object that is an instance of a class will have specific values of its instance fields. The set of those values is the current state of the object. Whenever you invoke a method on an object, its state may change.

The key to making encapsulation work is to have methods never directly access instance fields in a class other than their own. Programs should interact with object data only through the object's methods. Encapsulation is the way to give an object its「black box」behavior, which is the key to reuse and reliability. This means a class may totally change how it stores its data, but as long as it continues to use the same methods to manipulate the data, no other object will know or care.

When you start writing your own classes in Java, another tenet of OOP will make this easier: Classes can be built by extending other classes. Java, in fact, comes with a「cosmic superclass」called Object. All other classes extend this class. You will learn more about the Object class in the next chapter.

When you extend an existing class, the new class has all the properties and methods of the class that you extend. You then supply new methods and data fields that apply to your new class only. The concept of extending a class to obtain another class is called inheritance. See the next chapter for more on inheritance.

4.1.1 类

类（class）是构造对象的模板或蓝图。我们可以将类想象成制作小甜饼的切割机，将对象想象为小甜饼。由类构造（construct）对象的过程称为创建类的实例（instance）。正如前面所看到的，用 Java 编写的所有代码都位于某个类的内部。标准的 Java 库提供了几千个类，可以用于用户界面设计、日期、日历和网络程序设计。尽管如此，还是需要在 Java 程序中创建一些自己的类，以便描述应用程序所对应的问题域中的对象。封装（encapsulation，有时称为数据隐藏）是与对象有关的一个重要概念。从形式上看，封装不过是将数据和行为组合在一个包中，并对对象的使用者隐藏了数据的实现方式。对象中的数据称为实例域（instance field），操纵数据的过程称为方法（method）。对于每个特定的类实例（对象）都有一组特定的实例域值。这些值的集合就是这个对象的当前状态（state）。无论何时，只要向对象发送一个消息，它的状态就有可能发生改变。

实现封装的关键在于绝对不能让类中的方法直接地访问其他类的实例域。程序仅通过对象的方法与对象数据进行交互。封装给对象赋予了「黑盒」特征，这是提高重用性和可靠性的关键。这意味着一个类可以全面地改变存储数据的方式，只要仍旧使用同样的方法操作数据，其他对象就不会知道或介意所发生的变化。OOP 的另一个原则会让用户自定义 Java 类变得轻而易举，这就是：可以通过扩展一个类来建立另外一个新的类。事实上，在 Java 中，所有的类都源自于一个「神通广大的超类」，它就是 Object。在下一章中，读者将可以看到有关 Object 类的详细介绍。在扩展一个已有的类时，这个扩展后的新类具有所扩展的类的全部属性和方法。在新类中，只需提供适用于这个新类的新方法和数据域就可以了。通过扩展一个类来建立另外一个类的过程称为继承（inheritance），有关继承的详细内容请参看下一章。

#### 4.1.2 Objects

To work with OOP, you should be able to identify three key characteristics of objects:

The object's behavior — what can you do with this object, or what methods can you apply to it?

The object's state — how does the object react when you invoke those methods?

The object's identity — how is the object distinguished from others that may have the same behavior and state?

All objects that are instances of the same class share a family resemblance by supporting the same behavior. The behavior of an object is defined by the methods that you can call.

Next, each object stores information about what it currently looks like. This is the object's state. An object's state may change over time, but not spontaneously. A change in the state of an object must be a consequence of method calls. (If an object's state changed without a method call on that object, someone broke encapsulation.)

However, the state of an object does not completely describe it, because each object has a distinct identity. For example, in an order processing system, two orders are distinct even if they request identical items. Notice that the individual objects that are instances of a class always differ in their identity and usually differ in their state.

These key characteristics can influence each other. For example, the state of an object can influence its behavior. (If an order is「shipped」or「paid,」it may reject a method call that asks it to add or remove items. Conversely, if an order is「empty」 — that is, no items have yet been ordered — it should not allow itself to be shipped.)

4.1.2 对象

要想使用 OOP，一定要清楚对象的三个主要特性：

1、对象的行为（behavior） ——  可以对对象施加哪些操作，或可以对对象施加哪些方法？

2、对象的状态（state） ——  当施加那些方法时，对象如何响应？

3、对象标识（identity） ——  如何辨别具有相同行为与状态的不同对象？

同一个类的所有对象实例，由于支持相同的行为而具有家族式的相似性。对象的行为是用可调用的方法定义的。此外，每个对象都保存着描述当前特征的信息。这就是对象的状态。对象的状态可能会随着时间而发生改变，但这种改变不会是自发的。对象状态的改变必须通过调用方法实现（如果不经过方法调用就可以改变对象状态，只能说明封装性遭到了破坏）。但是，对象的状态并不能完全描述一个对象。每个对象都有一个唯一的身份（identity）。例如，在一个订单处理系统中，任何两个订单都存在着不同之处，即使所订购的货物完全相同也是如此。需要注意，作为一个类的实例，每个对象的标识永远是不同的，状态常常也存在着差异。

对象的这些关键特性在彼此之间相互影响着。例如，对象的状态影响它的行为（如果一个订单「已送货」或「已付款」，就应该拒绝调用具有增删订单中条目的方法。反过来，如果订单是「空的」，即还没有加入预订的物品，这个订单就不应该进入「已送货」状态）。

#### 4.1.3 Identifying Classes

In a traditional procedural program, you start the process at the top, with the main function. When designing an object-oriented system, there is no「top,」and newcomers to OOP often wonder where to begin. The answer is: Identify your classes and then add methods to each class.

A simple rule of thumb in identifying classes is to look for nouns in the problem analysis. Methods, on the other hand, correspond to verbs.

For example, in an order-processing system, some of the nouns are:

Item

Order

Shipping address

Payment

Account

These nouns may lead to the classes Item, Order, and so on.

Next, look for verbs. Items are added to orders. Orders are shipped or canceled. Payments are applied to orders. With each verb, such as「add,」「ship,」「cancel,」or「apply,」you identify the object that has the major responsibility for carrying it out. For example, when a new item is added to an order, the order object should be the one in charge because it knows how it stores and sorts items. That is, add should be a method of the Order class that takes an Item object as a parameter.

Of course, the「noun and verb」is but a rule of thumb; only experience can help you decide which nouns and verbs are the important ones when building your classes.

4.1.3 识别类

传统的过程化程序设计，必须从顶部的 main 函数开始编写程序。在面向对象程序设计时没有所谓的「顶部」。对于学习 OOP 的初学者来说常常会感觉无从下手。答案是：首先从设计类开始，然后再往每个类中添加方法。识别类的简单规则是在分析问题的过程中寻找名词，而方法对应着动词。例如，在订单处理系统中，有这样一些名词：商品（Item）、订单（Order）、送货地址（Shipping address）、付款（Payment）、账户（Account），这些名词很可能成为类 Item、Order 等。

接下来，查看动词：商品被添加到订单中，订单被发送或取消，订单货款被支付。对于每一个动词如：「添加」、「发送」、「取消」以及「支付」，都要标识出主要负责完成相应动作的对象。例如，当一个新的商品添加到订单中时，那个订单对象就是被指定的对象，因为它知道如何存储商品以及如何对商品进行排序。也就是说，add 应该是 Order 类的一个方法，而 Item 对象是一个参数。当然，所谓「找名词与动词」原则只是一种经验，在创建类的时候，哪些名词和动词是重要的完全取决于个人的开发经验。

#### 4.1.4 Relationships between Classes

The most common relationships between classes are:

Dependence (uses–a)

Aggregation (has–a)

Inheritance (is–a)

The dependence, or「uses–a」relationship, is the most obvious and also the most general. For example, the Order class uses the Account class because Order objects need to access Account objects to check for credit status. But the Item class does not depend on the Account class, because Item objects never need to worry about customer accounts. Thus, a class depends on another class if its methods use or manipulate objects of that class.

Try to minimize the number of classes that depend on each other. The point is, if a class A is unaware of the existence of a class B, it is also unconcerned about any changes to B. (And this means that changes to B do not introduce bugs into A.) In software engineering terminology, you want to minimize the coupling between classes.

The aggregation, or「has–a」relationship, is easy to understand because it is concrete; for example, an Order object contains Item objects. Containment means that objects of class A contain objects of class B.

Note: Some methodologists view the concept of aggregation with disdain and prefer to use a more general「association」relationship. From the point of view of modeling, that is understandable. But for programmers, the「has–a」relationship makes a lot of sense. We like to use aggregation for another reason as well: The standard notation for associations is less clear. See Table 4.1.

Table 4.1 UML Notation for Class Relationships

| Relationship | UML Connector |
| --- | --- |
| Inheritance | - |
| Interface implementation | - |
| Dependency | - |
| Aggregation | - |
| Association | - |
| Directed association | - |

1『各关系对应的 UML 图形详见原文。（2021-10-30）』

The inheritance, or「is–a」relationship, expresses a relationship between a more special and a more general class. For example, a RushOrder class inherits from an Order class. The specialized RushOrder class has special methods for priority handling and a different method for computing shipping charges, but its other methods, such as adding items and billing, are inherited from the Order class. In general, if class A extends class B, class A inherits methods from class B but has more capabilities. (See the next chapter in which we discuss this important notion at some length.)

Many programmers use the UML (Unified Modeling Language) notation to draw class diagrams that describe the relationships between classes. You can see an example of such a diagram in Figure 4.2. You draw classes as rectangles, and relationships as arrows with various adornments. Table 4.1 shows the most common UML arrow styles.

Figure 4.2 A class diagram

4.1.4 类之间的关系

在类之间，最常见的关系有：依赖（uses-a）、聚合（has-a）、继承（is-a）。

1-3『之前看王铮的设计模式专栏课里提到，依赖是 use-a、继承是 has-a，感觉他就是从这里获取到这个说法的。（2021-10-30）』

依赖（dependence），即「uses-a」关系，是一种最明显的、最常见的关系。例如，Order 类使用 Account 类是因为 Order 对象需要访问 Account 对象查看信用状态。但是 Item 类不依赖于 Account 类，这是因为 Item 对象与客户账户无关。因此，如果一个类的方法操纵另一个类的对象，我们就说一个类依赖于另一个类。

应该尽可能地将相互依赖的类减至最少。如果类 A 不知道 B 的存在，它就不会关心 B 的任何改变（这意味着 B 的改变不会导致 A 产生任何 bug）。用软件工程的术语来说，就是让类之间的耦合度最小。

1『很有感触，架构整洁之道书籍里，详细讲解依赖倒置原则时弄清楚的概念，A 用到 B 的话，那么 A 依赖于 B。（2021-10-30）』

聚合（aggregation），即「has-a」关系，是一种具体且易于理解的关系。例如，一个 Order 对象包含一些 Item 对象。聚合关系意味着类 A 的对象包含类 B 的对象。注释：有些方法学家不喜欢聚合这个概念，而更加喜欢使用「关联」这个术语。从建模的角度看，这是可以理解的。但对于程序员来说，「has-a」显得更加形象。喜欢使用聚合的另一个理由是关联的标准符号不易区分，请参看表 4-1。

表 4-1 表达类关系的 UML 符号

继承（inheritance），即「is-a」关系，是一种用于表示特殊与一般关系的。例如，Rush Order 类由 Order 类继承而来。在具有特殊性的 RushOrder 类中包含了一些用于优先处理的特殊方法，以及一个计算运费的不同方法；而其他的方法，如添加商品、生成账单等都是从 Order 类继承来的。一般而言，如果类 A 扩展类 B，类 A 不但包含从类 B 继承的方法，还会拥有一些额外的功能（下一章将详细讨论继承，其中会用较多的篇幅讲述这个重要的概念）。很多程序员采用 UML（Unified Modeling Language，统一建模语言）绘制类图，用来描述类之间的关系。图 4-2 就是这样一个例子。类用矩形表示，类之间的关系用带有各种修饰的箭头表示。表 4-1 给出了 UML 中最常见的箭头样式。

图 4-2 类图

### 4.2 Using Predefined Classes

You can't do anything in Java without classes, and you have already seen several classes at work. However, not all of these show off the typical features of object orientation. Take, for example, the Math class. You have seen that you can use methods of the Math class, such as Math.random, without needing to know how they are implemented — all you need to know is the name and parameters (if any). That's the point of encapsulation, and it will certainly be true of all classes. But the Math class only encapsulates functionality; it neither needs nor hides data. Since there is no data, you do not need to worry about making objects and initializing their instance fields — there aren't any!

In the next section, we will look at a more typical class, the Date class. You will see how to construct objects and call methods of this class.

4.2 使用预定义

类在 Java 中，没有类就无法做任何事情，我们前面曾经接触过几个类。然而，并不是所有的类都具有面向对象特征。例如，Math 类。在程序中，可以使用 Math 类的方法，如 Math.random，并只需要知道方法名和参数（如果有的话），而不必了解它的具体实现过程。这正是封装的关键所在，当然所有类都是这样。但遗憾的是，Math 类只封装了功能，它不需要也不必隐藏数据。由于没有数据，因此也不必担心生成对象以及初始化实例域。下一节将会给出一个更典型的类 —— Date 类，从中可以看到如何构造对象，以及如何调用类的方法。

#### 4.2.1 Objects and Object Variables

To work with objects, you first construct them and specify their initial state. Then you apply methods to the objects.

In the Java programming language, you use constructors to construct new instances. A constructor is a special method whose purpose is to construct and initialize objects. Let us look at an example. The standard Java library contains a Date class. Its objects describe points in time, such as December 31, 1999, 23:59:59 GMT.

Note: You may be wondering: Why use a class to represent dates rather than (as in some languages) a built-in type? For example, Visual Basic has a built-in date type, and programmers can specify dates in the format #6/1/1995#. On the surface, this sounds convenient — programmers can simply use the built-in date type without worrying about classes. But actually, how suitable is the Visual Basic design? In some locales, dates are specified as month/day/year, in others as day/month/year. Are the language designers really equipped to foresee these kinds of issues? If they do a poor job, the language becomes an unpleasant muddle, but unhappy programmers are powerless to do anything about it. With classes, the design task is offloaded to a library designer. If the class is not perfect, other programmers can easily write their own classes to enhance or replace the system classes. (To prove the point: The Java date library started out a bit muddled, and it has been redesigned twice.)

Constructors always have the same name as the class name. Thus, the constructor for the Date class is called Date. To construct a Date object, combine the constructor with the new operator, as follows:

```java
new Date()
```

This expression constructs a new object. The object is initialized to the current date and time.

If you like, you can pass the object to a method:

```java
System.out.println(new Date());
```

Alternatively, you can apply a method to the object that you just constructed. One of the methods of the Date class is the toString method. That method yields a string representation of the date. Here is how you would apply the toString method to a newly constructed Date object:

```java
String s = new Date().toString();
```

In these two examples, the constructed object is used only once. Usually, you will want to hang on to the objects that you construct so that you can keep using them. Simply store the object in a variable:

```java
Date birthday = new Date();
```

Figure 4.3 shows the object variable birthday that refers to the newly constructed object.

Figure 4.3 Creating a new object

There is an important difference between objects and object variables. For example, the statement

```java
Date deadline; // deadline doesn't refer to any object
```

defines an object variable, deadline, that can refer to objects of type Date. It is important to realize that the variable deadline is not an object and, in fact, does not even refer to an object yet. You cannot use any Date methods on this variable at this time. The statement

```java
s = deadline.toString(); // not yet
```

would cause a compile-time error.

You must first initialize the deadline variable. You have two choices. Of course, you can initialize the variable so that it refers to a newly constructed object:

```java
deadline = new Date();
```

Or you can set the variable to refer to an existing object:

```java
deadline = birthday;
```

Now both variables refer to the same object (see Figure 4.4).

Figure 4.4 Object variables that refer to the same object

It is important to realize that an object variable doesn't actually contain an object. It only refers to an object.

In Java, the value of any object variable is a reference to an object that is stored elsewhere. The return value of the new operator is also a reference. A statement such as

```java
Date deadline = new Date();
```

has two parts. The expression new Date() makes an object of type Date, and its value is a reference to that newly created object. That reference is then stored in the deadline variable.

You can explicitly set an object variable to null to indicate that it currently refers to no object.

```java
deadline = null;

. . .

if (deadline != null)
		System.out.println(deadline);
```

We will discuss null in more detail in Section 4.3.6,「Working with null References,」on p.148.

C++ Note: Some people mistakenly believe that Java object variables behave like C++ references. But in C++ there are no null references, and references cannot be assigned. You should think of Java object variables as analogous to object pointers in C++. For example,

```java
Date birthday; // Java
```

is really the same as

```java
Date* birthday; // C++
```

Once you make this association, everything falls into place. Of course, a Date* pointer isn't initialized until you initialize it with a call to new. The syntax is almost the same in C++ and Java.

```java
Date* birthday = new Date(); // C++
```

If you copy one variable to another, then both variables refer to the same date — they are pointers to the same object. The equivalent of the Java null reference is the C++ NULL pointer.

All Java objects live on the heap. When an object contains another object variable, it contains just a pointer to yet another heap object.

In C++, pointers make you nervous because they are so error-prone. It is easy to create bad pointers or to mess up memory management. In Java, these problems simply go away. If you use an uninitialized pointer, the runtime system will reliably generate a runtime error instead of producing random results. You don't have to worry about memory management, because the garbage collector takes care of it.

C++ makes quite an effort, with its support for copy constructors and assignment operators, to allow the implementation of objects that copy themselves automatically. For example, a copy of a linked list is a new linked list with the same contents but with an independent set of links. This makes it possible to design classes with the same copy behavior as the built-in types. In Java, you must use the clone method to get a complete copy of an object.

4.2.1 对象与对象变量

要想使用对象，就必须首先构造对象，并指定其初始状态。然后，对对象应用方法。在 Java 程序设计语言中，使用构造器（constructor）构造新实例。构造器是一种特殊的方法，用来构造并初始化对象。下面看一个例子。在标准 Java 库中包含一个 Date 类。它的对象将描述一个时间点，例如：「December 31，1999，23：59：59 GMT」。

注释：你可能会感到奇怪：为什么用类描述时间，而不像其他语言那样用一个内置的（built-in）类型？例如，在 Visual Basic 中有一个内置的 date 类型，程序员可以采用 #6/1/1995# 格式指定日期。从表面上看，这似乎很方便，因为程序员使用内置的 date 类型，而不必为设计类而操心。但实际上，Visual Basic 这样设计的适应性如何呢？在有些地区日期表示为月 / 日 / 年，而另一些地区表示为日 / 月 / 年。语言设计者是否能够预见这些问题呢？如果没有处理好这类问题，语言就有可能陷入混乱，对此感到不满的程序员也会丧失使用这种语言的热情。如果使用类，这些设计任务就交给了类库的设计者。如果类设计的不完善，其他的操作员可以很容易地编写自己的类，以便增强或替代（replace）系统提供的类（作为这个问题的印证：Java 的日期类库有些混乱，已经重新设计了两次）。构造器的名字应该与类名相同。因此 Date 类的构造器名为 Date。要想构造一个 Date 对象，需要在构造器前面加上 new 操作符，如下所示：

这个表达式构造了一个新对象。这个对象被初始化为当前的日期和时间。

如果需要的话，也可以将这个对象传递给一个方法：

或者，也可以将一个方法应用于刚刚创建的对象。Date 类中有一个 toString 方法。这个方法将返回日期的字符串描述。下面的语句可以说明如何将 toString 方法应用于新构造的 Date 对象上。在这两个例子中，构造的对象仅使用了一次。通常，希望构造的对象可以多次使用，因此，需要将对象存放在一个变量中：

图 4-3 显示了引用新构造的对象变量 birthday。

图 4-3 创建一个新对象

在对象与对象变量之间存在着一个重要的区别。例如，语句：

定义了一个对象变量 deadline，它可以引用 Date 类型的对象。但是，一定要认识到：变量 deadline 不是一个对象，实际上也没有引用对象。此时，不能将任何 Date 方法应用于这个变量上。语句：

将产生编译错误。必须首先初始化变量 deadline，这里有两个选择。当然，可以用新构造的对象初始化这个变量：

也让这个变量引用一个已存在的对象：

现在，这两个变量引用同一个对象（请参见图 4-4）。

图 4-4 引用同一个对象的对象变量

一定要认识到：一个对象变量并没有实际包含一个对象，而仅仅引用一个对象。在 Java 中，任何对象变量的值都是对存储在另外一个地方的一个对象的引用。new 操作符的返回值也是一个引用。下列语句：

有两个部分。表达式 new Date() 构造了一个 Date 类型的对象，并且它的值是对新创建对象的引用。这个引用存储在变量 deadline 中。可以显式地将对象变量设置为 null，表明这个对象变量目前没有引用任何对象。如果将一个方法应用于一个值为 null 的对象上，那么就会产生运行时错误。局部变量不会自动地初始化为 null，而必须通过调用 new 或将它们设置为 null 进行初始化

C++ 注释：很多人错误地认为 Java 对象变量与 C++ 的引用类似。然而，在 C++ 中没有空引用，并且引用不能被赋值。可以将 Java 的对象变量看作 C++ 的对象指针。例如，实际上，等同于一旦理解了这一点，一切问题就迎刃而解了。当然，一个 `Date *` 指针只能通过调用 new 进行初始化。就这一点而言，C++ 与 Java 的语法几乎是一样的。如果把一个变量的值赋给另一个变量，两个变量就指向同一个日期，即它们是同一个对象的指针。在 Java 中的 null 引用对应 C++ 中的 NULL 指针。所有的 Java 对象都存储在堆中。当一个对象包含另一个对象变量时，这个变量依然包含着指向另一个堆对象的指针。

所有的 Java 对象都存储在堆中。当一个对象包含另一个对象变量时，这个变量依然包含着指向另一个堆对象的指针。在 C++ 中，指针十分令人头疼，并常常导致程序错误。稍不小心就会创建一个错误的指针，或者造成内存溢出。在 Java 语言中，这些问题都不复存在。如果使用一个没有初始化的指针，运行系统将会产生一个运行时错误，而不是生成一个随机的结果。同时，不必担心内存管理问题，垃圾收集器将会处理相关的事宜。C++ 确实做了很大的努力，它通过拷贝型构造器和复制操作符来实现对象的自动拷贝。例如，一个链表（linked list）拷贝的结果将会得到一个新链表，其内容与原始链表相同，但却是一组独立的链接。这使得将同样的拷贝行为内置在类中成为可能。在 Java 中，必须使用 clone 方法获得对象的完整拷贝。

#### 4.2.2 The LocalDate Class of the Java Library

In the preceding examples, we used the Date class that is a part of the standard Java library. An instance of the Date class has a state — namely, a particular point in time.

Although you don't need to know this when you use the Date class, the time is represented by the number of milliseconds (positive or negative) from a fixed point, the so-called epoch, which is 00:00:00 UTC, January 1, 1970. UTC is the Coordinated Universal Time, the scientific time standard which is, for practical purposes, the same as the more familiar GMT, or Greenwich Mean Time.

But as it turns out, the Date class is not very useful for manipulating the kind of calendar information that humans use for dates, such as「December 31, 1999」. This particular description of a day follows the Gregorian calendar, which is the calendar used in most countries of the world. The same point in time would be described quite differently in the Chinese or Hebrew lunar calendars, not to mention the calendar used by your customers from Mars.

Note: Throughout human history, civilizations grappled with the design of calendars to attach names to dates and bring order to the solar and lunar cycles. For a fascinating explanation of calendars around the world, from the French Revolutionary calendar to the Mayan long count, see Calendrical Calculations by Nachum Dershowitz and Edward M. Reingold (Cambridge University Press, 3rd ed., 2007).

The library designers decided to separate the concerns of keeping time and attaching names to points in time. Therefore, the standard Java library contains two separate classes: the Date class, which represents a point in time, and the LocalDate class, which expresses days in the familiar calendar notation. Java 8 introduced quite a few other classes for manipulating various aspects of date and time — see Chapter 6 of Volume II.

Separating time measurement from calendars is good object-oriented design. In general, it is a good idea to use different classes to express different concepts.

You do not use a constructor to construct objects of the LocalDate class. Instead, use static factory methods that call constructors on your behalf. The expression

```java
LocalDate.now()
```

constructs a new object that represents the date at which the object was constructed.

1『

```java
import java.time.LocalDate;
```

开始要引用包的。在 IEDA 里直接用快捷键 alt+enter 可以生成引用语句。

插曲：开始的时候把 LocalDate.now() 打错成小写的 localDate.now()，死活生成不了引用，还跑去 Google 查，也没解决。最后发现是字母打错小写的了，所以认识到 Java 里类都是大写开头的，这是常识。（2021-10-31）

』

You can construct an object for a specific date by supplying year, month, and day:

```java
LocalDate.of(1999, 12, 31)
```

Of course, you will usually want to store the constructed object in an object variable:

```java
LocalDate newYearsEve = LocalDate.of(1999, 12, 31);
```

Once you have a LocalDate object, you can find out the year, month, and day with the methods getYear, getMonthValue, and getDayOfMonth:

```java
int year = newYearsEve.getYear(); // 1999

int month = newYearsEve.getMonthValue(); // 12

int day = newYearsEve.getDayOfMonth(); // 31
```

This may seem pointless because they are the very same values that you just used to construct the object. But sometimes, you have a date that has been computed, and then you will want to invoke those methods to find out more about it. For example, the plusDays method yields a new LocalDate that is a given number of days away from the object to which you apply it:

```java
LocalDate aThousandDaysLater = newYearsEve.plusDays(1000);

year = aThousandDaysLater.getYear(); // 2002

month = aThousandDaysLater.getMonthValue(); // 09

day = aThousandDaysLater.getDayOfMonth(); // 26
```

The LocalDate class has encapsulated instance fields to maintain the date to which it is set. Without looking at the source code, it is impossible to know the representation that the class uses internally. But, of course, the point of encapsulation is that this doesn't matter. What matters are the methods that a class exposes.

Note: Actually, the Date class also has methods to get the day, month, and year, called getDay, getMonth, and getYear, but these methods are deprecated. A method is deprecated when a library designer realizes that the method should have never been introduced in the first place.

These methods were a part of the Date class before the library designers realized that it makes more sense to supply separate classes to deal with calendars. When an earlier set of calendar classes was introduced in Java 1.1, the Date methods were tagged as deprecated. You can still use them in your programs, but you will get unsightly compiler warnings if you do. It is a good idea to stay away from using deprecated methods because they may be removed in a future version of the library.

Tip: The JDK provides the jdeprscan tool for checking whether your code uses deprecated features of the Java API. See [jdeprscan](https://docs.oracle.com/javase/9/tools/jdeprscan.htm#JSWOR-GUID-2B7588B0-92DB-4A88-88D4-24D183660A62) for instructions.

4.2.2 Java 类库中的 LocalDate 类

在前面的例子中，已经使用了 Java 标准类库中的 Date 类。Date 类的实例有一个状态，即特定的时间点。

尽管在使用 Date 类时不必知道这一点，但时间是用距离一个固定时间点的毫秒数（可正可负）表示的，这个点就是所谓的纪元（epoch），它是 UTC 时间 1970 年 1 月 1 日 00:00:00。UTC 是 Coordinated Universal Time 的缩写，与大家熟悉的 GMT（即 Greenwich Mean Time，格林威治时间）一样，是一种具有实践意义的科学标准时间。但是，Date 类所提供的日期处理并没有太大的用途。Java 类库的设计者认为：像「December 31，1999，23:59:59」这样的日期表示法只是阳历的固有习惯。这种特定的描述法遵循了世界上大多数地区使用的 Gregorian 阳历表示法。但是，同一时间点采用中国的农历表示和采用希伯来的阴历表示就很不一样，对于火星历来说就更不可想象了。

注释：有史以来，人类的文明与历法的设计紧紧地相连，日历给日期命名、给太阳和月亮的周期排列次序。有关世界上各种日历的有趣解释，从法国革命的日历到玛雅人计算日期的方法等，请参看 Nachum Dershowitz 和 Edward M.Reingold 编写的《Calendrical Calculations》第 3 版（剑桥大学出版社，2007 年）。类库设计者决定将保存时间与给时间点命名分开。所以标准 Java 类库分别包含了两个类：一个是用来表示时间点的 Date 类；另一个是用来表示大家熟悉的日历表示法的 LocalDate 类。Java SE 8 引入了另外一些类来处理日期和时间的不同方面 —— 有关内容参见卷 Ⅱ 第 6 章。将时间与日历分开是一种很好的面向对象设计。通常，最好使用不同的类表示不同的概念。不要使用构造器来构造 LocalDate 类的对象。实际上，应当使用静态工厂方法（factory method）代表你调用构造器。下面的表达式会构造一个新对象，表示构造这个对象时的日期。可以提供年、月和日来构造对应一个特定日期的对象：

当然，通常都希望将构造的对象保存在一个对象变量中：一旦有了一个 LocalDate 对象，可以用方法 getYear、getMonthValue 和 getDayOfMonth 得到年、月和日：看起来这似乎没有多大的意义，因为这正是构造对象时使用的那些值。不过，有时可能某个日期是计算得到的，你希望调用这些方法来得到更多信息。例如，plusDays 方法会得到一个新的 LocalDate，如果把应用这个方法的对象称为当前对象，这个新日期对象则是距当前对象指定天数的一个新日期：LocalDate 类封装了实例域来维护所设置的日期。如果不查看源代码，就不可能知道类内部的日期表示。当然，封装的意义在于，这一点并不重要，重要的是类对外提供的方法。注释：实际上，Date 类还有 getDay、getMonth 以及 getYear 等方法，然而并不推荐使用这些方法。当类库设计者意识到某个方法不应该存在时，就把它标记为不鼓励使用。

类库设计者意识到应当单独提供类来处理日历，不过在此之前这些方法已经是 Date 类的一部分了。Java 1.1 中引入较早的一组日历类时，Date 方法被标为废弃不用。虽然仍然可以在程序中使用这些方法，不过如果这样做，编译时会出现警告。最好还是不要使用这些废弃不用的方法，因为将来的某个类库版本很有可能将它们完全删除。

#### 4.2.3 Mutator and Accessor Methods

Have another look at the plusDays method call that you saw in the preceding section:

```java
LocalDate aThousandDaysLater = newYearsEve.plusDays(1000);
```

What happens to newYearsEve after the call? Has it been changed to be a thousand days later? As it turns out, it has not. The plusDays method yields a new LocalDate object, which is then assigned to the aThousandDaysLater variable. The original object remains unchanged. We say that the plusDays method does not mutate the object on which it is invoked. (This is similar to the toUpperCase method of the String class that you saw in Chapter 3. When you call toUpperCase on a string, that string stays the same, and a new string with uppercase characters is returned.)

An earlier version of the Java library had a different class for dealing with calendars, called GregorianCalendar. Here is how you add a thousand days to a date represented by that class:

```java
GregorianCalendar someDay = new GregorianCalendar(1999, 11, 31);

// odd feature of that class: month numbers go from 0 to 11

someDay.add(Calendar.DAY_OF_MONTH, 1000);
```

Unlike the LocalDate.plusDays method, the GregorianCalendar.add method is a mutator method. After invoking it, the state of the someDay object has changed. Here is how you can find out the new state:

```java
year = someDay.get(Calendar.YEAR); // 2002

month = someDay.get(Calendar.MONTH) + 1; // 09

day = someDay.get(Calendar.DAY_OF_MONTH); // 26
```

That's why we called the variable someDay and not newYearsEve — it no longer is new year's eve after calling the mutator method.

In contrast, methods that only access objects without modifying them are sometimes called accessor methods. For example, LocalDate.getYear and GregorianCalendar.get are accessor methods.

C++ Note: In C++, the const suffix denotes accessor methods. A method that is not declared as const is assumed to be a mutator. However, in the Java programming language, no special syntax distinguishes accessors from mutators.

We finish this section with a program that puts the LocalDate class to work. The program displays a calendar for the current month, like this:

Mon Tue Wed Thu Fri Sat Sun

1

2 3 4 5 6 7 8

9 10 11 12 13 14 15

16 17 18 19 20 21 22

23 24 25 26* 27 28 29

30

The current day is marked with an asterisk (*). As you can see, the program needs to know how to compute the length of a month and the weekday of a given day.

Let us go through the key steps of the program. First, we construct an object that is initialized with the current date.

```java
LocalDate date = LocalDate.now();
```

We capture the current month and day.

```java
int month = date.getMonthValue();

int today = date.getDayOfMonth();
```

Then we set date to the first of the month and get the weekday of that date.

```java
date = date.minusDays(today - 1); // set to start of month

DayOfWeek weekday = date.getDayOfWeek();

int value = weekday.getValue(); // 1 = Monday, . . . , 7 = Sunday
```

The variable weekday is set to an object of type DayOfWeek. We call the getValue method of that object to get a numerical value for the weekday. This yields an integer that follows the international convention where the weekend comes at the end of the week, returning 1 for Monday, 2 for Tuesday, and so on. Sunday has value 7.

Note that the first line of the calendar is indented, so that the first day of the month falls on the appropriate weekday. Here is the code to print the header and the indentation for the first line:

```java
System.out.println("Mon Tue Wed Thu Fri Sat Sun");

for (int i = 1; i < value; i++)
    System.out.print(" ");
```

Now, we are ready to print the body of the calendar. We enter a loop in which date traverses the days of the month.

In each iteration, we print the date value. If date is today, the date is marked with an *. Then, we advance date to the next day. When we reach the beginning of each new week, we print a new line:

```java
while (date.getMonthValue() == month)
	{
		System.out.printf("%3d", date.getDayOfMonth());
		if (date.getDayOfMonth() == today)
			System.out.print("*");
		else
			System.out.print(" ");
		date = date.plusDays(1);
		if (date.getDayOfWeek().getValue() == 1)
			System.out.println();
	}
```

When do we stop? We don't know whether the month has 31, 30, 29, or 28 days. Instead, we keep iterating while date is still in the current month.

Listing 4.1 shows the complete program.

As you can see, the LocalDate class makes it possible to write a calendar program that takes care of complexities such as weekdays and the varying month lengths. You don't need to know how the LocalDate class computes months and weekdays. You just use the interface of the class — the methods such as plusDays and getDayOfWeek.

The point of this example program is to show you how you can use the interface of a class to carry out fairly sophisticated tasks without having to know the implementation details.

Listing 4.1 CalendarTest/CalendarTest.java

```java
import java.time.*;

/**
* @version 1.5 2015-05-08
* @author Cay Horstmann
*/

public class CalendarTest

{

	public static void main(String[] args)

	{

		LocalDate date = LocalDate.now();

		int month = date.getMonthValue();

		int today = date.getDayOfMonth();

		date = date.minusDays(today - 1); // set to start of month

		DayOfWeek weekday = date.getDayOfWeek();

		int value = weekday.getValue(); // 1 = Monday, . . . , 7 = Sunday

		System.out.println("Mon Tue Wed Thu Fri Sat Sun");

		for (int i = 1; i < value; i++)

			System.out.print(" ");

		while (date.getMonthValue() == month)

		{

			System.out.printf("%3d", date.getDayOfMonth());

			if (date.getDayOfMonth() == today)

				System.out.print("*");

			else

				System.out.print(" ");

			date = date.plusDays(1);

			if (date.getDayOfWeek().getValue() == 1) System.out.println();

		}

		if (date.getDayOfWeek().getValue() != 1) System.out.println();

	}
```

java.time.LocalDate 8

```java
static LocalDate now()
```

constructs an object that represents the current date.

```java
static LocalDate of(int year, int month, int day)
```

constructs an object that represents the given date.

```java
int getYear()

int getMonthValue()

int getDayOfMonth()
```

gets the year, month, and day of this date.

DayOfWeek getDayOfWeek

gets the weekday of this date as an instance of the DayOfWeek class. Call getValue to get a weekday between 1 (Monday) and 7 (Sunday).

```java
LocalDate plusDays(int n)

LocalDate minusDays(int n)
```

yields the date that is n days after or before this date.

4.2.3 更改器方法与访问器方法

再来看上一节中的 plusDays 方法调用：这个调用之后 newYearsEve 会有什么变化？它会改为 1000 天之后的日期吗？事实上，并没有。plusDays 方法会生成一个新的 LocalDate 对象，然后把这个新对象赋给 aThousandDaysLater 变量。原来的对象不做任何改动。我们说 plusDays 方法没有更改调用这个方法的对象。（这类似于第 3 章中见过的 String 类的 toUpperCase 方法。在一个字符串上调用 toUpperCase 时，这个字符串仍保持不变，会返回一个将字符大写的新字符串。）Java 库的一个较早版本曾经有另一个类来处理日历，名为 GregorianCalendar。可以如下为这个类表示的一个日期增加 1000 天：

与 LocalDate.plusDays 方法不同，GregorianCalendar.add 方法是一个更改器方法（mutator method）。调用这个方法后，someDay 对象的状态会改变。可以如下查看新状态：

正是因为这个原因，我们将变量命名为 someDay 而不是 newYearsEve ——  调用这个更改器方法之后，它不再是新年前夜。相反，只访问对象而不修改对象的方法有时称为访问器方法（accessormethod）。例如，LocalDate.getYear 和 GregorianCalendar.get 就是访问器方法。

C++ 注释：在 C++ 中，带有 const 后缀的方法是访问器方法；默认为更改器方法。但是，在 Java 语言中，访问器方法与更改器方法在语法上没有明显的区别。下面用一个应用 LocalDate 类的程序来结束本节内容的论述。这个程序将显示当前月的日历，其格式为：

当前的日用一个 `*` 号标记。可以看到，这个程序需要解决如何计算某月份的天数以及一个给定日期相应是星期几。下面看一下这个程序的关键步骤。首先，构造了一个日历对象，并用当前的日期和时间进行初始化。下面获得当前的月和日。然后，将 date 设置为这个月的第一天，并得到这一天为星期几。变量 weekday 设置为 DayOfWeek 类型的对象。我们调用这个对象的 getValue 方法来得到星期几的一个数值。这会得到一个整数，这里遵循国际惯例，即周末是一周的末尾，星期一就返回 1，星期二返回 2，依此类推。星期日则返回 7。注意，日历的第一行是缩进的，使得月份的第一天指向相应的星期几。下面的代码会打印表头和第一行的缩进：现在我们来打印日历的主体。进入一个循环，其中 date 遍历一个月中的每一天。每次迭代时，打印日期值。如果 date 是当前日期，这个日期则用一个 * 标记。接下来，把 date 推进到下一天。如果到达新的一周的第一天，则换行打印：

什么时候结束呢？我们不知道这个月有几天，是 31 天、30 天、29 天还是 28 天。实际上，只要 date 还在当月就要继续迭代。程序清单 4-1 给出了完整的程序。

程序清单 4-1 CalendarTest/CalendarTest.java

可以看到，利用 LocalDate 类可以编写一个日历程序，能处理星期几以及各月天数不同等复杂问题。你并不需要知道 LocalDate 类如何计算月和星期几。只需要使用这个类的接口，如 plusDays 和 getDayOfWeek 等方法。这个示例程序的重点是向你展示如何使用一个类的接口来完成相当复杂的任务，而无需了解实现细节。

java.time.LocalDate 8

static LocalTime now() 构造一个表示当前日期的对象。

static LocalTime of（int year，int month，int day）构造一个表示给定日期的对象。

int getYear()

int getMonthValue()

int getDayOfMonth()

得到当前日期的年、月和日。

DayOfWeek getDayOfWeek 得到当前日期是星期几，作为 DayOfWeek 类的一个实例返回。调用 getValue 来得到 1-7 之间的一个数，表示这是星期几，1 表示星期一，7 表示星期日。

LocalDate plusDays(int n)

LocalDate minusDays(int n)

生成当前日期之后或之前 n 天的日期。

### 4.3 Defining Your Own Classes

In Chapter 3, you started writing simple classes. However, all those classes had just a single main method. Now the time has come to show you how to write the kind of「workhorse classes」that are needed for more sophisticated applications. These classes typically do not have a main method. Instead, they have their own instance fields and methods. To build a complete program, you combine several classes, one of which has a main method.

4.3 用户自定义类

在第 3 章中，已经开始编写了一些简单的类。但是，那些类都只包含一个简单的 main 方法。现在开始学习如何设计复杂应用程序所需要的各种主力类（workhorse class）。通常，这些类没有 main 方法，却有自己的实例域和实例方法。要想创建一个完整的程序，应该将若干类组合在一起，其中只有一个类有 main 方法。

#### 4.3.1 An Employee Class

The simplest form for a class definition in Java is

```java
class ClassName

{

field1

field2

. . .

constructor1

constructor2

. . .

method1

method2

. . .

}
```

Consider the following, very simplified, version of an Employee class that might be used by a business in writing a payroll system:



class Employee

{

// instance fields

private String name;

private double salary;

private LocalDate hireDay;

// constructor

public Employee(String n, double s, int year, int month, int day)

{

name = n;

salary = s;

hireDay = LocalDate.of(year, month, day);

}

// a method

public String getName()

{

return name;

}

// more methods

. . .

}

We break down the implementation of this class, in some detail, in the sections that follow. First, though, Listing 4.2 is a program that shows the Employee class in action.

In the program, we construct an Employee array and fill it with three Employee objects:



Employee[] staff = new Employee[3];

staff[0] = new Employee("Carl Cracker", . . .);

staff[1] = new Employee("Harry Hacker", . . .);

staff[2] = new Employee("Tony Tester", . . .);

Next, we use the raiseSalary method of the Employee class to raise each employee's salary by 5%:



for (Employee e : staff)

e.raiseSalary(5);

Finally, we print out information about each employee, by calling the getName,



for (Employee e : staff)

System.out.println("name=" + e.getName()

+ ",salary=" + e.getSalary()

+ ",hireDay=" + e.getHireDay());

Note that the example program consists of two classes: the Employee class and a class EmployeeTest with the public access specifier. The main method with the instructions that we just described is contained in the EmployeeTest class.

The name of the source file is EmployeeTest.java because the name of the file must match the name of the public class. You can only have one public class in a source file, but you can have any number of nonpublic classes.

Next, when you compile this source code, the compiler creates two class files in the directory: EmployeeTest.class and Employee.class.

You then start the program by giving the bytecode interpreter the name of the class that contains the main method of your program:

java EmployeeTest

The bytecode interpreter starts running the code in the main method in the EmployeeTest class. This code in turn constructs three new Employee objects and shows you their state.

Listing 4.2 EmployeeTest/EmployeeTest.java



1 import java.time.*;

2

3 /**

4 * This program tests the Employee class.

5 * @version 1.13 2018-04-10

6 * @author Cay Horstmann

7 */

8 public class EmployeeTest

9 {

10 public static void main(String[] args)

11 {

12 // fill the staff array with three Employee objects

13 Employee[] staff = new Employee[3];

14

15 staff[0] = new Employee("Carl Cracker", 75000, 1987, 12, 15);

16 staff[1] = new Employee("Harry Hacker", 50000, 1989, 10, 1);

17 staff[2] = new Employee("Tony Tester", 40000, 1990, 3, 15);

18

19 // raise everyone's salary by 5%

20 for (Employee e : staff)

21 e.raiseSalary(5);

22

23 // print out information about all Employee objects

24 for (Employee e : staff)

25 System.out.println("name=" + e.getName() + ",salary=" + e.getSalary() + ",hireDay="

26 + e.getHireDay());

27 }

28 }

29

30 class Employee

31 {

32 private String name;

33 private double salary;

34 private LocalDate hireDay;

35

36 public Employee(String n, double s, int year, int month, int day)

37 {

38 name = n;

39 salary = s;

40 hireDay = LocalDate.of(year, month, day);

41 }

42

43 public String getName()

44 {

45 return name;

46 }

47

48 public double getSalary()

49 {

50 return salary;

51 }

52

53 public LocalDate getHireDay()

54 {

55 return hireDay;

56 }

57

58 public void raiseSalary(double byPercent)

59 {

60 double raise = salary * byPercent / 100;

61 salary += raise;

62 }

63 }

4.3.1 Employee 类

在 Java 中，最简单的类定义形式为：下面看一个非常简单的 Employee 类。在编写薪金管理系统时可能会用到。

这里将这个类的实现细节分成以下几个部分，并分别在稍后的几节中给予介绍。下面先看看程序清单 4-2，这个程序显示了一个 Employee 类的实际使用。程序清单 4-2 EmployeeTest/EmployeeTest.java

在这个程序中，构造了一个 Employee 数组，并填入了三个雇员对象：接下来，利用 Employee 类的 raiseSalary 方法将每个雇员的薪水提高 5%：最后，调用 getName 方法、getSalary 方法和 getHireDay 方法将每个雇员的信息打印出来：注意，在这个示例程序中包含两个类：Employee 类和带有 public 访问修饰符的 EmployeeTest 类。EmployeeTest 类包含了 main 方法，其中使用了前面介绍的指令。源文件名是 EmployeeTest.java，这是因为文件名必须与 public 类的名字相匹配。在一个源文件中，只能有一个公有类，但可以有任意数目的非公有类。接下来，当编译这段源代码的时候，编译器将在目录下创建两个类文件：EmployeeTest.class 和 Employee.class。将程序中包含 main 方法的类名提供给字节码解释器，以便启动这个程序：字节码解释器开始运行 EmployeeTest 类的 main 方法中的代码。在这段代码中，先后构造了三个新 Employee 对象，并显示它们的状态。


#### 4.3.2 Use of Multiple Source Files

The program in Listing 4.2 has two classes in a single source file. Many programmers prefer to put each class into its own source file. For example, you can place the Employee class into a file Employee.java and the EmployeeTest class into EmployeeTest.java.

If you like this arrangement, you have two choices for compiling the program. You can invoke the Java compiler with a wildcard:

javac Employee*.java

Then, all source files matching the wildcard will be compiled into class files. Or, you can simply type

javac EmployeeTest.java

You may find it surprising that the second choice works even though the Employee.java file is never explicitly compiled. However, when the Java compiler sees the Employee class being used inside EmployeeTest.java, it will look for a file named Employee.class. If it does not find that file, it automatically searches for Employee.java and compiles it. Moreover, if the timestamp of the version of Employee.java that it finds is newer than that of the existing Employee.class file, the Java compiler will automatically recompile the file.

Note: If you are familiar with the make facility of UNIX (or one of its Windows cousins, such as nmake), you can think of the Java compiler as having the make functionality already built in.

4.3.2 多个源文件的使用

在程序清单 4-2 中，一个源文件包含了两个类。许多程序员习惯于将每一个类存在一个单独的源文件中。例如，将 Employee 类存放在文件 Employee.java 中，将 EmployeeTest 类存放在文件 EmployeeTest.java 中。如果喜欢这样组织文件，将可以有两种编译源程序的方法。一种是使用通配符调用 Java 编译器：于是，所有与通配符匹配的源文件都将被编译成类文件。或者键入下列命令：读者可能会感到惊讶，使用第二种方式，并没有显式地编译 Employee.java。然而，当 Java 编译器发现 EmployeeTest.java 使用了 Employee 类时会查找名为 Employee.class 的文件。如果没有找到这个文件，就会自动地搜索 Employee.java，然后，对它进行编译。更重要的是：如果 Employee.java 版本较已有的 Employee.class 文件版本新，Java 编译器就会自动地重新编译这个文件。注释：如果熟悉 UNIX 的「make」工具（或者是 Windows 中的「nmake」等工具），可以认为 Java 编译器内置了「make」功能。

#### 4.3.3 Dissecting the Employee Class

In the sections that follow, we will dissect the Employee class. Let's start with the methods in this class. As you can see by examining the source code, this class has one constructor and four methods:



public Employee(String n, double s, int year, int month, int day)

public String getName()

public double getSalary()

public LocalDate getHireDay()

public void raiseSalary(double byPercent)

All methods of this class are tagged as public. The keyword public means that any method in any class can call the method. (The four possible access levels are covered in this and the next chapter.)

Next, notice the three instance fields that will hold the data manipulated inside an instance of the Employee class.



private String name;

private double salary;

private LocalDate hireDay;

The private keyword makes sure that the only methods that can access these instance fields are the methods of the Employee class itself. No outside method can read or write to these fields.

Note: You could use the public keyword with your instance fields, but it would be a very bad idea. Having public data fields would allow any part of the program to read and modify the instance fields, completely ruining encapsulation. Any method of any class can modify public fields — and, in our experience, some code will take advantage of that access privilege when you least expect it. We strongly recommend to make all your instance fields private.

Finally, notice that two of the instance fields are themselves objects: The name and hireDay fields are references to String and LocalDate objects. This is quite usual: Classes will often contain instance fields of class type.

4.3.3 剖析 Employee 类

下面对 Employee 类进行剖析。首先从这个类的方法开始。通过查看源代码会发现，这个类包含一个构造器和 4 个方法：这个类的所有方法都被标记为 public。关键字 public 意味着任何类的任何方法都可以调用这些方法（共有 4 种访问级别，将在本章稍后和下一章中介绍）。接下来，需要注意在 Employee 类的实例中有三个实例域用来存放将要操作的数据：关键字 private 确保只有 Employee 类自身的方法能够访问这些实例域，而其他类的方法不能够读写这些域。注释：可以用 public 标记实例域，但这是一种极为不提倡的做法。public 数据域允许程序中的任何方法对其进行读取和修改。这就完全破坏了封装。任何类的任何方法都可以修改 public 域，从我们的经验来看，某些代码将使用这种存取权限，而这并不我们所希望的，因此，这里强烈建议将实例域标记为 private。最后，请注意，有两个实例域本身就是对象：name 域是 String 类对象，hireDay 域是 LocalDate 类对象。这种情形十分常见：类通常包括类型属于某个类类型的实例域。

#### 4.3.4 First Steps with Constructors

Let's look at the constructor listed in our Employee class.



public Employee(String n, double s, int year, int month, int day)

{

name = n;

salary = s;

hireDay = LocalDate.of(year, month, day);

}

As you can see, the name of the constructor is the same as the name of the class. This constructor runs when you construct objects of the Employee class — giving the instance fields the initial state you want them to have.

For example, when you create an instance of the Employee class with code like this:



new Employee("James Bond", 100000, 1950, 1, 1)

you have set the instance fields as follows:



name = "James Bond";

salary = 100000;

hireDay = LocalDate.of(1950, 1, 1); // January 1, 1950

There is an important difference between constructors and other methods. A constructor can only be called in conjunction with the new operator. You can't apply a constructor to an existing object to reset the instance fields. For example,



james.Employee("James Bond", 250000, 1950, 1, 1) // ERROR

is a compile-time error.

We will have more to say about constructors later in this chapter. For now, keep the following in mind:

A constructor has the same name as the class.

A class can have more than one constructor.

A constructor can take zero, one, or more parameters.

A constructor has no return value.

A constructor is always called with the new operator.

C++ Note: Constructors work the same way in Java as they do in C++. Keep in mind, however, that all Java objects are constructed on the heap and that a constructor must be combined with new. It is a common error of C++ programmers to forget the new operator:



Employee number007("James Bond", 100000, 1950, 1, 1); // C++, not Java

That works in C++ but not in Java.

Caution

Be careful not to introduce local variables with the same names as the instance fields. For example, the following constructor will not set the salary:



public Employee(String n, double s, . . .)

{

String name = n; // ERROR

double salary = s; // ERROR

. . .

}

The constructor declares local variables name and salary. These variables are only accessible inside the constructor. They shadow the instance fields with the same name. Some programmers accidentally write this kind of code when they type faster than they think, because their fingers are used to adding the data type. This is a nasty error that can be hard to track down. You just have to be careful in all of your methods to not use variable names that equal the names of instance fields.

4.3.4 从构造器开始

下面先看看 Employee 类的构造器：可以看到，构造器与类同名。在构造 Employee 类的对象时，构造器会运行，以便将实例域初始化为所希望的状态。例如，当使用下面这条代码创建 Employee 类实例时：将会把实例域设置为：构造器与其他的方法有一个重要的不同。构造器总是伴随着 new 操作符的执行被调用，而不能对一个已经存在的对象调用构造器来达到重新设置实例域的目的。例如，将产生编译错误。本章稍后还会更加详细地介绍有关构造器的内容。现在只需要记住：·构造器与类同名·每个类可以有一个以上的构造器·构造器可以有 0 个、1 个或多个参数·构造器没有返回值

构造器总是伴随着 new 操作一起调用 C++ 注释：Java 构造器的工作方式与 C++ 一样。但是，要记住所有的 Java 对象都是在堆中构造的，构造器总是伴随着 new 操作符一起使用。C++ 程序员最易犯的错误就是忘记 new 操作符：这条语句在 C++ 中能够正常运行，但在 Java 中却不行。警告：请注意，不要在构造器中定义与实例域重名的局部变量。例如，下面的构造器将无法设置 salary。这个构造器声明了局部变量 name 和 salary。这些变量只能在构造器内部访问。这些变量屏蔽了同名的实例域。有些程序设计者（例如，本书的作者）常常不假思索地写出这类代码，因为他们已经习惯增加这类数据类型。这种错误很难被检查出来，因此，必须注意在所有的方法中不要命名与实例域同名的变量。

#### 4.3.5 Declaring Local Variables with var

As of Java 10, you can declare local variables with the var keyword instead of specifying their type, provided their type can be inferred from the initial value. For example, instead of declaring



Employee harry = new Employee("Harry Hacker", 50000, 1989, 10, 1);

you simply write



var harry = new Employee("Harry Hacker", 50000, 1989, 10, 1);

This is nice since it avoids the repetition of the type name Employee.

From now on, we will use the var notation in those cases where the type is obvious from the right-hand side without any knowledge of the Java API. But we won't use var with numeric types such as int, long, or double so that you don't have to look out for the difference between 0, 0L, and 0.0. Once you are more experienced with the Java API, you may want to use the var keyword more frequently.

Note that the var keyword can only be used with local variables inside methods. You must always declare the types of parameters and fields.

4.3.5 隐式参数与显式参数方法用于操作对象以及存取它们的实例域。例如，方法：将调用这个方法的对象的 salary 实例域设置为新值。看看下面这个调用：它的结果将 number007.salary 域的值增加 5%。具体地说，这个调用将执行下列指令：raiseSalary 方法有两个参数。第一个参数称为隐式（implicit）参数，是出现在方法名前的 Employee 类对象。第二个参数位于方法名后面括号中的数值，这是一个显式（explicit）参数。（有些人把隐式参数称为方法调用的目标或接收者。）可以看到，显式参数是明显地列在方法声明中的，例如 double byPercent。隐式参数没有出现在方法声明中。在每一个方法中，关键字 this 表示隐式参数。如果需要的话，可以用下列方式编写 raiseSalary 方法：

有些程序员更偏爱这样的风格，因为这样可以将实例域与局部变量明显地区分开来。C++ 注释：在 C++ 中，通常在类的外面定义方法：如果在类的内部定义方法，这个方法将自动地成为内联（inline）方法。在 Java 中，所有的方法都必须在类的内部定义，但并不表示它们是内联方法。是否将某个方法设置为内联方法是 Java 虚拟机的任务。即时编译器会监视调用那些简洁、经常被调用、没有被重载以及可优化的方法。

#### 4.3.6 Working with null References

In Section 4.2.1,「Objects and Object Variables,」on p. 132, you saw that an object variable holds a reference to an object, or the special value null to indicate the absence of an object.

This sounds like a convenient mechanism for dealing with special situations, such as an unknown name or hire date. But you need to be very careful with null values.

If you apply a method to a null value, a NullPointerException occurs.



LocalDate birthday = null;

String s = birthday.toString(); // NullPointerException

This is a serious error, similar to an「index out of bounds」exception. If your program does not「catch」an exception, it is terminated. Normally, programs don't catch these kinds of exceptions but rely on programmers not to cause them in the first place.

When you define a class, it is a good idea to be clear about which fields can be null. In our example, we don't want the name or hireDay field to be null. (We don't have to worry about the salary field. It has primitive type and can never be null.)

The hireDay field is guaranteed to be non-null because it is initialized with a new LocalDate object. But name will be null if the constructor is called with a null argument for n.

There are two solutions. The「permissive」approach is to turn a null argument into an appropriate non-null value:



if (n == null) name = "unknown"; else name = n;

As of Java 9, the Objects class has a convenience method for this purpose:



public Employee(String n, double s, int year, int month, int day)

{

name = Objects.requireNonNullElse(n, "unknown");

. . .

}

The「tough love」approach is to reject a null argument:



public Employee(String n, double s, int year, int month, int day)

{

Objects.requireNonNull(n, "The name cannot be null");

name = n;

. . .

}

If someone constructs an Employee object with a null name, then a NullPointerException occurs. At first glance, that may not seem a useful remedy. But there are two advantages:

The exception report has a description of the problem.

The exception report pinpoints the location of the problem. Otherwise, a NullPointerException would have occurred elsewhere, with no easy way of tracing it back to the faulty constructor argument.

Note: Whenever you accept an object reference as a construction parameter, ask yourself whether you really intend to model values that can be present or absent. If not, the「tough love」approach is preferred.

#### 4.3.7 Implicit and Explicit Parameters

Methods operate on objects and access their instance fields. For example, the method



public void raiseSalary(double byPercent)

{

double raise = salary * byPercent / 100;

salary += raise;

}

sets a new value for the salary instance field in the object on which this method is invoked. Consider the call



number007 .raiseSalary(5);

The effect is to increase the value of the number007.salary field by 5%. More specifically, the call executes the following instructions:



double raise = number007.salary * 5 / 100;

number007.salary += raise;

The raiseSalary method has two parameters. The first parameter, called the implicit parameter, is the object of type Employee that appears before the method name. The second parameter, the number inside the parentheses after the method name, is an explicit parameter. (Some people call the implicit parameter the target or receiver of the method call.)

As you can see, the explicit parameters are explicitly listed in the method declaration — for example, double byPercent. The implicit parameter does not appear in the method declaration.

In every method, the keyword this refers to the implicit parameter. If you like, you can write the raiseSalary method as follows:



public void raiseSalary(double byPercent)

{

double raise = this.salary * byPercent / 100;

this.salary += raise;

}

Some programmers prefer that style because it clearly distinguishes between instance fields and local variables.

C++ Note

In C++, you generally define methods outside the class:



void Employee::raiseSalary(double byPercent) // C++, not Java

{

. . .

}

If you define a method inside a class, then it is, automatically, an inline method.



class Employee

{

. . .

int getName() { return name; } // inline in C++

}

In Java, all methods are defined inside the class itself. This does not make them inline. Finding opportunities for inline replacement is the job of the Java virtual machine. The just-in-time compiler watches for calls to methods that are short, commonly called, and not overridden, and optimizes them away.

#### 4.3.8 Benefits of Encapsulation

Finally, let's look more closely at the rather simple getName, getSalary, and getHireDay methods.



public String getName()

{

return name;

}

public double getSalary()

{

return salary;

}

public LocalDate getHireDay()

{

return hireDay;

}

These are obvious examples of accessor methods. As they simply return the values of instance fields, they are sometimes called field accessors.

Wouldn't it be easier to make the name, salary, and hireDay fields public, instead of having separate accessor methods?

However, the name field is read-only. Once you set it in the constructor, there is no method to change it. Thus, we have a guarantee that the name field will never be corrupted.

The salary field is not read-only, but it can only be changed by the raiseSalary method. In particular, should the value ever turn out wrong, only that method needs to be debugged. Had the salary field been public, the culprit for messing up the value could have been anywhere.

Sometimes, it happens that you want to get and set the value of an instance field. Then you need to supply three items:

A private data field;

A public field accessor method; and

A public field mutator method.

This is a lot more tedious than supplying a single public data field, but there are considerable benefits.

First, you can change the internal implementation without affecting any code other than the methods of the class. For example, if the storage of the name is changed to

String firstName;

String lastName;

then the getName method can be changed to return

firstName + " " + lastName

This change is completely invisible to the remainder of the program.

Of course, the accessor and mutator methods may need to do a lot of work to convert between the old and the new data representation. That leads us to our second benefit: Mutator methods can perform error checking, whereas code that simply assigns to a field may not go into the trouble. For example, a setSalary method might check that the salary is never less than 0.

Caution

Be careful not to write accessor methods that return references to mutable objects. In a previous edition of this book, we violated that rule in our Employee class in which the getHireDay method returned an object of class Date:



class Employee

{

private Date hireDay;

. . .

public Date getHireDay()

{

return hireDay; // BAD

}

. . .

}

Unlike the LocalDate class, which has no mutator methods, the Date class has a mutator method, setTime, where you can set the number of milliseconds.

The fact that Date objects are mutable breaks encapsulation! Consider the following rogue code:



Employee harry = . . .;

Date d = harry.getHireDay();

double tenYearsInMilliSeconds = 10 * 365.25 * 24 * 60 * 60 * 1000;

d.setTime(d.getTime() - (long) tenYearsInMilliSeconds);

// let's give Harry ten years of added seniority

The reason is subtle. Both d and harry.hireDay refer to the same object (see Figure 4.5). Applying mutator methods to d automatically changes the private state of the Employee object!

Figure 4.5 Returning a reference to a mutable data field

If you need to return a reference to a mutable object, you should clone it first. A clone is an exact copy of an object stored in a new location. We discuss cloning in detail in Chapter 6. Here is the corrected code:



class Employee

{

. . .

public Date getHireDay()

{

return (Date) hireDay.clone(); // OK

}

. . .

}

As a rule of thumb, always use clone whenever you need to return a copy of a mutable field.

4.3.6 封装的优点

最后，再仔细地看一下非常简单的 getName 方法、getSalary 方法和 getHireDay 方法。

这些都是典型的访问器方法。由于它们只返回实例域值，因此又称为域访问器。将 name、salary 和 hireDay 域标记为 public，以此来取代独立的访问器方法会不会更容易些呢？关键在于 name 是一个只读域。一旦在构造器中设置完毕，就没有任何一个办法可以对它进行修改，这样来确保 name 域不会受到外界的破坏。虽然 salary 不是只读域，但是它只能用 raiseSalary 方法修改。特别是一旦这个域值出现了错误，只要调试这个方法就可以了。如果 salary 域是 public 的，破坏这个域值的捣乱者有可能会出没在任何地方。在有些时候，需要获得或设置实例域的值。因此，应该提供下面三项内容：·一个私有的数据域；·一个公有的域访问器方法；·一个公有的域更改器方法。这样做要比提供一个简单的公有数据域复杂些，但是却有着下列明显的好处：首先，可以改变内部实现，除了该类的方法之外，不会影响其他代码。例如，如果将存储名字的域改为：那么 getName 方法可以改为返回对于这点改变，程序的其他部分完全不可见。

当然，为了进行新旧数据表示之间的转换，访问器方法和更改器方法有可能需要做许多工作。但是，这将为我们带来了第二点好处：更改器方法可以执行错误检查，然而直接对域进行赋值将不会进行这些处理。例如，setSalary 方法可以检查薪金是否小于 0。警告：注意不要编写返回引用可变对象的访问器方法。在 Employee 类中就违反了这个设计原则，其中的 getHireDay 方法返回了一个 Date 类对象：LocalDate 类没有更改器方法，与之不同，Date 类有一个更改器方法 setTime，可以在这里设置毫秒数。Date 对象是可变的，这一点就破坏了封装性！请看下面这段代码：出错的原因很微妙。d 和 harry.hireDay 引用同一个对象（请参见图 4-5）。对 d 调用更改器方法就可以自动地改变这个雇员对象的私有状态！

图 4-5 返回可变数据域的引用如果需要返回一个可变对象的引用，应该首先对它进行克隆（clone）。对象 clone 是指存放在另一个位置上的对象副本。有关对象 clone 的详细内容将在第 6 章中讨论。下面是修改后的代码：凭经验可知，如果需要返回一个可变数据域的拷贝，就应该使用 clone。

#### 4.3.9 Class-Based Access Privileges

You know that a method can access the private data of the object on which it is invoked. What people often find surprising is that a method can access the private data of all objects of its class. For example, consider a method equals that compares two employees.



class Employee

{

. . .

public boolean equals(Employee other)

{

return name.equals(other.name);

}

}

A typical call is



if (harry.equals(boss)) . . .

This method accesses the private fields of harry, which is not surprising. It also accesses the private fields of boss. This is legal because boss is an object of type Employee, and a method of the Employee class is permitted to access the private fields of any object of type Employee.

C++ Note

C++ has the same rule. A method can access the private features of any object of its class, not just of the implicit parameter.

4.3.7 基于类的访问权限

从前面已经知道，方法可以访问所调用对象的私有数据。一个方法可以访问所属类的所有对象的私有数据，这令很多人感到奇怪！例如，下面看一下用来比较两个雇员的 equals 方法。典型的调用方式是这个方法访问 harry 的私有域，这点并不会让人奇怪，然而，它还访问了 boss 的私有域。这是合法的，其原因是 boss 是 Employee 类对象，而 Employee 类的方法可以访问 Employee 类的任何一个对象的私有域。C++ 注释：C++ 也有同样的原则。方法可以访问所属类的私有特性（feature），而不仅限于访问隐式参数的私有特性。

#### 4.3.10 Private Methods

When implementing a class, we make all data fields private because public data are dangerous. But what about the methods? While most methods are public, private methods are useful in certain circumstances. Sometimes, you may wish to break up the code for a computation into separate helper methods. Typically, these helper methods should not be part of the public interface — they may be too close to the current implementation or require a special protocol or calling order. Such methods are best implemented as private.

To implement a private method in Java, simply change the public keyword to private.

By making a method private, you are under no obligation to keep it available if you change your implementation. The method may well be harder to implement or unnecessary if the data representation changes; this is irrelevant. The point is that as long as the method is private, the designers of the class can be assured that it is never used elsewhere, so they can simply drop it. If a method is public, you cannot simply drop it because other code might rely on it.

4.3.8 私有方法

在实现一个类时，由于公有数据非常危险，所以应该将所有的数据域都设置为私有的。然而，方法又应该如何设计呢？尽管绝大多数方法都被设计为公有的，但在某些特殊情况下，也可能将它们设计为私有的。有时，可能希望将一个计算代码划分成若干个独立的辅助方法。通常，这些辅助方法不应该成为公有接口的一部分，这是由于它们往往与当前的实现机制非常紧密，或者需要一个特别的协议以及一个特别的调用次序。最好将这样的方法设计为 private 的。在 Java 中，为了实现一个私有的方法，只需将关键字 public 改为 private 即可。对于私有方法，如果改用其他方法实现相应的操作，则不必保留原有的方法。如果数据的表达方式发生了变化，这个方法可能会变得难以实现，或者不再需要。然而，只要方法是私有的，类的设计者就可以确信：它不会被外部的其他类操作调用，可以将其删去。如果方法是公有的，就不能将其删去，因为其他的代码很可能依赖它。

#### 4.3.11 Final Instance Fields

You can define an instance field as final. Such a field must be initialized when the object is constructed. That is, you must guarantee that the field value has been set after the end of every constructor. Afterwards, the field may not be modified again. For example, the name field of the Employee class may be declared as final because it never changes after the object is constructed — there is no



class Employee

{

private final String name;

. . .

}

The final modifier is particularly useful for fields whose type is primitive or an immutable class. (A class is immutable if none of its methods ever mutate its objects. For example, the String class is immutable.)

For mutable classes, the final modifier can be confusing. For example, consider a field



private final StringBuilder evaluations;

that is initialized in the Employee constructor as



evaluations = new StringBuilder();

The final keyword merely means that the object reference stored in the evaluations variable will never again refer to a different StringBuilder object. But the object can be mutated:



public void giveGoldStar()

{

evaluations.append(LocalDate.now() + ": Gold star!\n");

}

4.3.9 final 实例域

可以将实例域定义为 final。构建对象时必须初始化这样的域。也就是说，必须确保在每一个构造器执行之后，这个域的值被设置，并且在后面的操作中，不能够再对它进行修改。例如，可以将 Employee 类中的 name 域声明为 final，因为在对象构建之后，这个值不会再被修改，即没有 setName 方法。final 修饰符大都应用于基本（primitive）类型域，或不可变（immutable）类的域（如果类中的每个方法都不会改变其对象，这种类就是不可变的类。例如，String 类就是一个不可变的类）。对于可变的类，使用 final 修饰符可能会对读者造成混乱。例如，在 Employee 构造器中会初始化为 final 关键字只是表示存储在 evaluations 变量中的对象引用不会再指示其他 StringBuilder 对象。不过这个对象可以更改：

### 4.4 Static Fields and Methods

In all sample programs that you have seen, the main method is tagged with the static modifier. We are now ready to discuss the meaning of this modifier.

4.4 静态域与静态方法

在前面给出的示例程序中，main 方法都被标记为 static 修饰符。下面讨论一下这个修饰符的含义。

#### 4.4.1 Static Fields

If you define a field as static, then there is only one such field per class. In contrast, each object has its own copy of nonstatic instance fields. For example, let's suppose we want to assign a unique identification number to each employee. We add an instance field id and a static field nextId to the Employee class:



class Employee

{

private static int nextId = 1;

private int id;

. . .

}

Every Employee object now has its own id field, but there is only one nextId field that is shared among all instances of the class. Let's put it another way. If there are 1,000 objects of the Employee class, then there are 1,000 instance fields id, one for each object. But there is a single static field nextId. Even if there are no Employee objects, the static field nextId is present. It belongs to the class, not to any individual object.

Note

In some object-oriented programming languages, static fields are called class fields. The term「static」is a meaningless holdover from C++.

Let's implement a simple method:



public void setId()

{

id = nextId;

nextId++;

}

Suppose you set the employee identification number for harry:

harry.setId();

Then, the id field of harry is set to the current value of the static field nextId, and the value of the static field is incremented:



harry.id = Employee.nextId;

Employee.nextId++;

4.4.1 静态域

如果将域定义为 static，每个类中只有一个这样的域。而每一个对象对于所有的实例域却都有自己的一份拷贝。例如，假定需要给每一个雇员赋予唯一的标识码。这里给 Employee 类添加一个实例域 id 和一个静态域 nextId：现在，每一个雇员对象都有一个自己的 id 域，但这个类的所有实例将共享一个 nextId 域。换句话说，如果有 1000 个 Employee 类的对象，则有 1000 个实例域 id。但是，只有一个静态域 nextId。即使没有一个雇员对象，静态域 nextId 也存在。它属于类，而不属于任何独立的对象。注释：在绝大多数的面向对象程序设计语言中，静态域被称为类域。术语「static」只是沿用了 C++ 的叫法，并无实际意义。下面实现一个简单的方法：


假定为 harry 设定雇员标识码：harry 的 id 域被设置为静态域 nextId 当前的值，并且静态域 nextId 的值加 1：

#### 4.4.2 Static Constants

Static variables are quite rare. However, static constants are more common. For example, the Math class defines a static constant:



public class Math

{

. . .

public static final double PI = 3.14159265358979323846;

. . .

}

You can access this constant in your programs as Math.PI.

If the keyword static had been omitted, then PI would have been an instance field of the Math class. That is, you would need an object of this class to access PI, and every Math object would have its own copy of PI.

Another static constant that you have used many times is System.out. It is declared in the System class as follows:



public class System

{

. . .

public static final PrintStream out = . . .;

. . .

}

As we mentioned several times, it is never a good idea to have public fields, because everyone can modify them. However, public constants (that is, final fields) are fine. Since out has been declared as final, you cannot reassign another print stream to it:



System.out = new PrintStream(. . .); // ERROR--out is final

Note: If you look at the System class, you will notice a method setOut that sets System.out to a different stream. You may wonder how that method can change the value of a final variable. However, the setOut method is a native method, not implemented in the Java programming language. Native methods can bypass the access control mechanisms of the Java language. This is a very unusual workaround that you should not emulate in your programs.

4.4.2 静态常量

静态变量使用得比较少，但静态常量却使用得比较多。例如，在 Math 类中定义了一个静态常量：在程序中，可以采用 Math.PI 的形式获得这个常量。如果关键字 static 被省略，PI 就变成了 Math 类的一个实例域。需要通过 Math 类的对象访问 PI，并且每一个 Math 对象都有它自己的一份 PI 拷贝。另一个多次使用的静态常量是 System.out。它在 System 类中声明：

前面曾经提到过，由于每个类对象都可以对公有域进行修改，所以，最好不要将域设计为 public。然而，公有常量（即 final 域）却没问题。因为 out 被声明为 final，所以，不允许再将其他打印流赋给它：注释：如果查看一下 System 类，就会发现有一个 setOut 方法，它可以将 System.out 设置为不同的流。读者可能会感到奇怪，为什么这个方法可以修改 final 变量的值。原因在于，setOut 方法是一个本地方法，而不是用 Java 语言实现的。本地方法可以绕过 Java 语言的存取控制机制。这是一种特殊的方法，在自己编写程序时，不应该这样处理。

#### 4.4.3 Static Methods

Static methods are methods that do not operate on objects. For example, the pow method of the Math class is a static method. The expression

Math.pow(x, a)

computes the power xa. It does not use any Math object to carry out its task. In other words, it has no implicit parameter.

You can think of static methods as methods that don't have a this parameter. (In a nonstatic method, the this parameter refers to the implicit parameter of the method — see Section 4.3.7,「Implicit and Explicit Parameters,」on p. 150.)

A static method of the Employee class cannot access the id instance field because it does not operate on an object. However, a static method can access a static field. Here is an example of such a static method:



public static int getNextId()

{

return nextId; // returns static field

}

To call this method, you supply the name of the class:



int n = Employee.getNextId();

Could you have omitted the keyword static for this method? Yes, but then you would need to have an object reference of type Employee to invoke the method.

Note

It is legal to use an object to call a static method. For example, if harry is an Employee object, then you can call harry.getNextId() instead of Employee.getNextId(). However, we find that notation confusing. The getNextId method doesn't look at harry at all to compute the result. We recommend that you use class names, not objects, to invoke static methods.

Use static methods in two situations:

When a method doesn't need to access the object state because all needed parameters are supplied as explicit parameters (example: Math.pow).

When a method only needs to access static fields of the class (example: Employee.getNextId).

C++ Note

Static fields and methods have the same functionality in Java and C++. However, the syntax is slightly different. In C++, you use the :: operator to access a static field or method outside its scope, such as Math::PI.

The term「static」has a curious history. At first, the keyword static was introduced in C to denote local variables that don't go away when a block is exited. In that context, the term「static」makes sense: The variable stays around and is still there when the block is entered again. Then static got a second meaning in C, to denote global variables and functions that cannot be accessed from other files. The keyword static was simply reused to avoid introducing a new keyword. Finally, C++ reused the keyword for a third, unrelated, interpretation — to denote variables and functions that belong to a class but not to any particular object of the class. That is the same meaning the keyword has in Java.

4.4.3 静态方法

静态方法是一种不能向对象实施操作的方法。例如，Math 类的 pow 方法就是一个静态方法。表达式计算幂 xa。在运算时，不使用任何 Math 对象。换句话说，没有隐式的参数。可以认为静态方法是没有 this 参数的方法（在一个非静态的方法中，this 参数表示这个方法的隐式参数，参见 4.3.5 节）。Employee 类的静态方法不能访问 Id 实例域，因为它不能操作对象。但是，静态方法可以访问自身类中的静态域。下面是使用这种静态方法的一个示例：

可以通过类名调用这个方法：这个方法可以省略关键字 static 吗？答案是肯定的。但是，需要通过 Employee 类对象的引用调用这个方法。注释：可以使用对象调用静态方法。例如，如果 harry 是一个 Employee 对象，可以用 harry.getNextId（）代替 Employee.getNextId（）。不过，这种方式很容易造成混淆，其原因是 getNextId 方法计算的结果与 harry 毫无关系。我们建议使用类名，而不是对象来调用静态方法。在下面两种情况下使用静态方法：·一个方法不需要访问对象状态，其所需参数都是通过显式参数提供（例如：Math.pow）。·一个方法只需要访问类的静态域（例如：Employee.getNextId）。C++ 注释：Java 中的静态域与静态方法在功能上与 C++ 相同。但是，语法书写上却稍有所不同。在 C++ 中，使用：：操作符访问自身作用域之外的静态域和静态方法，如 Math：：PI。

术语「static」有一段不寻常的历史。起初，C 引入关键字 static 是为了表示退出一个块后依然存在的局部变量。在这种情况下，术语「static」是有意义的：变量一直存在，当再次进入该块时仍然存在。随后，static 在 C 中有了第二种含义，表示不能被其他文件访问的全局变量和函数。为了避免引入一个新的关键字，关键字 static 被重用了。最后，C++ 第三次重用了这个关键字，与前面赋予的含义完全不一样，这里将其解释为：属于类且不属于类对象的变量和函数。这个含义与 Java 相同。

#### 4.4.4 Factory Methods

Here is another common use for static methods. Classes such as LocalDate and NumberFormat use static factory methods that construct objects. You have already seen the factory methods LocalDate.now and LocalDate.of. Here is how the NumberFormat class yields formatter objects for various styles:



NumberFormat currencyFormatter = NumberFormat.getCurrencyInstance();

NumberFormat percentFormatter = NumberFormat.getPercentInstance();

double x = 0.1;

System.out.println(currencyFormatter.format(x)); // prints $0.10

System.out.println(percentFormatter.format(x)); // prints 10%

Why doesn't the NumberFormat class use a constructor instead? There are two reasons:

You can't give names to constructors. The constructor name is always the same as the class name. But we want two different names to get the currency instance and the percent instance.

When you use a constructor, you can't vary the type of the constructed object. But the factory methods actually return objects of the class DecimalFormat, a subclass that inherits from NumberFormat. (See Chapter 5 for more on inheritance.)

4.4.4 工厂方法

静态方法还有另外一种常见的用途。类似 LocalDate 和 NumberFormat 的类使用静态工厂方法（factory method）来构造对象。你已经见过工厂方法 LocalDate.now 和 LocalDate.of。NumberFormat 类如下使用工厂方法生成不同风格的格式化对象：

为什么 NumberFormat 类不利用构造器完成这些操作呢？这主要有两个原因：

·无法命名构造器。构造器的名字必须与类名相同。但是，这里希望将得到的货币实例和百分比实例采用不用的名字。·当使用构造器时，无法改变所构造的对象类型。而 Factory 方法将返回一个 DecimalFormat 类对象，这是 NumberFormat 的子类（有关继承的详细内容请参看第 5 章）。

#### 4.4.5 The main Method

Note that you can call static methods without having any objects. For example, you never construct any objects of the Math class to call Math.pow.

For the same reason, the main method is a static method.



public class Application

{

public static void main(String[] args)

{

// construct objects here

. . .

}

}

The main method does not operate on any objects. In fact, when a program starts, there aren't any objects yet. The static main method executes, and constructs the objects that the program needs.

Tip

Every class can have a main method. That is a handy trick for unit testing of classes. For example, you can add a main method to the Employee class:



class Employee

{

public Employee(String n, double s, int year, int month, int day)

{

name = n;

salary = s;

hireDay = LocalDate.of(year, month, day);

}

. . .

public static void main(String[] args) // unit test

{

var e = new Employee("Romeo", 50000, 2003, 3, 31);

e.raiseSalary(10);

System.out.println(e.getName() + " " + e.getSalary());

}

. . .

}

If you want to test the Employee class in isolation, simply execute

java Employee

If the Employee class is a part of a larger application, you start the application with

java Application

and the main method of the Employee class is never executed.

The program in Listing 4.3 contains a simple version of the Employee class with a static field nextId and a static method getNextId. We fill an array with three Employee objects and then print the employee information. Finally, we print the next available identification number, to demonstrate the static method.

Note that the Employee class also has a static main method for unit testing. Try running both

java Employee

and

java StaticTest

to execute both main methods.

Listing 4.3 StaticTest/StaticTest.java



1 /**

2 * This program demonstrates static methods.

3 * @version 1.02 2008-04-10

4 * @author Cay Horstmann

5 */

6 public class StaticTest

7 {

8 public static void main(String[] args)

9 {

10 // fill the staff array with three Employee objects

11 var staff = new Employee[3];

12

13 staff[0] = new Employee("Tom", 40000);

14 staff[1] = new Employee("Dick", 60000);

15 staff[2] = new Employee("Harry", 65000);

16

17 // print out information about all Employee objects

18 for (Employee e : staff)

19 {

20 e.setId();

21 System.out.println("name=" + e.getName() + ",id=" + e.getId() + ",salary="

22 + e.getSalary());

23 }

24

25 int n = Employee.getNextId(); // calls static method

26 System.out.println("Next available id=" + n);

27 }

28 }

29

30 class Employee

31 {

32 private static int nextId = 1;

33

34 private String name;

35 private double salary;

36 private int id;

37

38 public Employee(String n, double s)

39 {

40 name = n;

41 salary = s;

42 id = 0;

43 }

44

45 public String getName()

46 {

47 return name;

48 }

49

50 public double getSalary()

51 {

52 return salary;

53 }

54

55 public int getId()

56 {

57 return id;

58 }

59

60 public void setId()

61 {

62 id = nextId; // set id to next available id

63 nextId++;

64 }

65

66 public static int getNextId()

67 {

68 return nextId; // returns static field

69 }

70

71 public static void main(String[] args) // unit test

72 {

73 var e = new Employee("Harry", 50000);

74 System.out.println(e.getName() + " " + e.getSalary());

75 }

76 }

java.util.Objects 7

static <T> void requireNonNull(T obj)

static <T> void requireNonNull(T obj, String message)

static <T> void requireNonNull(T obj, Supplier<String> messageSupplier) 8

If obj is null, these methods throw a NullPointerException with no message or the given message. (Chapter 6 explains how to obtain a value lazily with a supplier. Chapter 8 explains the <T> syntax.)

static <T> T requireNonNullElse(T obj, T defaultObj)

static <T> T requireNonNullElseGet(T obj, Supplier<T> defaultSupplier)

Returns obj if it is not null, or the default object if obj is null.

4.4.5 main 方法

需要注意，不需要使用对象调用静态方法。例如，不需要构造 Math 类对象就可以调用 Math.pow。同理，main 方法也是一个静态方法。

main 方法不对任何对象进行操作。事实上，在启动程序时还没有任何一个对象。静态的 main 方法将执行并创建程序所需要的对象。提示：每一个类可以有一个 main 方法。这是一个常用于对类进行单元测试的技巧。例如，可以在 Employee 类中添加一个 main 方法：如果想要独立地测试 Employee 类，只需要执行如果 Employee 类是一个更大型应用程序的一部分，就可以使用下面这条语句运行程序 Employee 类的 main 方法永远不会执行。

程序清单 4-3 中的程序包含了 Employee 类的一个简单版本，其中有一个静态域 nextId 和一个静态方法 getNextId。这里将三个 Employee 对象写入数组，然后打印雇员信息。最后，打印出下一个可用的员工标识码来展示静态方法。程序清单 4-3 StaticTest/StaticTest.java

需要注意，Employee 类也有一个静态的 main 方法用于单元测试。试试运行和执行两个 main 方法。

### 4.5 Method Parameters

Let us review the computer science terms that describe how parameters can be passed to a method (or a function) in a programming language. The term call by value means that the method gets just the value that the caller provides. In contrast, call by reference means that the method gets the location of the variable that the caller provides. Thus, a method can modify the value stored in a variable passed by reference but not in one passed by value. These「call by . . .」terms are standard computer science terminology describing the behavior of method parameters in various programming languages, not just Java. (There is also a call by name that is mainly of historical interest, being employed in the Algol programming language, one of the oldest high-level languages.)

The Java programming language always uses call by value. That means that the method gets a copy of all parameter values. In particular, the method cannot modify the contents of any parameter variables passed to it.

For example, consider the following call:



double percent = 10;

harry.raiseSalary(percent);

No matter how the method is implemented, we know that after the method call, the value of percent is still 10.

Let us look a little more closely at this situation. Suppose a method tried to triple the value of a method parameter:



public static void tripleValue(double x) // doesn't work

{

x = 3 * x;

}

Let's call this method:



double percent = 10;

tripleValue(percent);

However, this does not work. After the method call, the value of percent is still 10. Here is what happens:

x is initialized with a copy of the value of percent (that is, 10).

x is tripled — it is now 30. But percent is still 10 (see Figure 4.6).

Figure 4.6 Modifying a numeric parameter has no lasting effect.

The method ends, and the parameter variable x is no longer in use.

There are, however, two kinds of method parameters:

Primitive types (numbers, boolean values)

Object references

You have seen that it is impossible for a method to change a primitive type parameter. The situation is different for object parameters. You can easily implement a method that triples the salary of an employee:



public static void tripleSalary(Employee x) // works

{

x.raiseSalary(200);

}

When you call



harry = new Employee(. . .);

tripleSalary(harry);

then the following happens:

x is initialized with a copy of the value of harry — that is, an object reference.

The raiseSalary method is applied to that object reference. The Employee object to which both x and harry refer gets its salary raised by 200 percent.

The method ends, and the parameter variable x is no longer in use. Of course, the object variable harry continues to refer to the object whose salary was tripled (see Figure 4.7).

Figure 4.7 Modifying an object parameter has a lasting effect.

As you have seen, it is easily possible — and in fact very common — to implement methods that change the state of an object parameter. The reason is simple. The method gets a copy of the object reference, and both the original and the copy refer to the same object.

Many programming languages (in particular, C++ and Pascal) have two mechanisms for parameter passing: call by value and call by reference. Some programmers (and unfortunately even some book authors) claim that Java uses call by reference for objects. That is false. As this is such a common misunderstanding, it is worth examining a counterexample in detail.

Let's try to write a method that swaps two Employee objects:



public static void swap(Employee x, Employee y) // doesn't work

{

Employee temp = x;

x = y;

y = temp;

}

If Java used call by reference for objects, this method would work:



var a = new Employee("Alice", . . .);

var b = new Employee("Bob", . . .);

swap(a, b);

// does a now refer to Bob, b to Alice?

However, the method does not actually change the object references that are stored in the variables a and b. The x and y parameters of the swap method are initialized with copies of these references. The method then proceeds to swap these copies.



// x refers to Alice, y to Bob

Employee temp = x;

x = y;

y = temp;

// now x refers to Bob, y to Alice

But ultimately, this is a wasted effort. When the method ends, the parameter variables x and y are abandoned. The original variables a and b still refer to the same objects as they did before the method call (see Figure 4.8).

Figure 4.8 Swapping object parameters has no lasting effect.

This demonstrates that the Java programming language does not use call by reference for objects. Instead, object references are passed by value.

Here is a summary of what you can and cannot do with method parameters in Java:

A method cannot modify a parameter of a primitive type (that is, numbers or boolean values).

A method can change the state of an object parameter.

A method cannot make an object parameter refer to a new object.

The program in Listing 4.4 demonstrates these facts. The program first tries to triple the value of a number parameter and does not succeed:



Testing tripleValue:

Before: percent=10.0

End of method: x=30.0

After: percent=10.0

It then successfully triples the salary of an employee:



Testing tripleSalary:

Before: salary=50000.0

End of method: salary=150000.0

After: salary=150000.0

After the method, the state of the object to which harry refers has changed. This is possible because the method modified the state through a copy of the object reference.

Finally, the program demonstrates the failure of the swap method:



Testing swap:

Before: a=Alice

Before: b=Bob

End of method: x=Bob

End of method: y=Alice

After: a=Alice

After: b=Bob

As you can see, the parameter variables x and y are swapped, but the variables a and b are not affected.

C++ Note

C++ has both call by value and call by reference. You tag reference parameters with &. For example, you can easily implement methods void tripleValue(double& x) or void swap(Employee& x, Employee& y) that modify their reference parameters.

Listing 4.4 ParamTest/ParamTest.java



1 /**

2 * This program demonstrates parameter passing in Java.

3 * @version 1.01 2018-04-10

4 * @author Cay Horstmann

5 */

6 public class ParamTest

7 {

8 public static void main(String[] args)

9 {

10 /*

11 * Test 1: Methods can't modify numeric parameters

12 */

13 System.out.println("Testing tripleValue:");

14 double percent = 10;

15 System.out.println("Before: percent=" + percent);

16 tripleValue(percent);

17 System.out.println("After: percent=" + percent);

18

19 /*

20 * Test 2: Methods can change the state of object parameters

21 */

22 System.out.println("\nTesting tripleSalary:");

23 var harry = new Employee("Harry", 50000);

24 System.out.println("Before: salary=" + harry.getSalary());

25 tripleSalary(harry);

26 System.out.println("After: salary=" + harry.getSalary());

27

28 /*

29 * Test 3: Methods can't attach new objects to object parameters

30 */

31 System.out.println("\nTesting swap:");

32 var a = new Employee("Alice", 70000);

33 var b = new Employee("Bob", 60000);

34 System.out.println("Before: a=" + a.getName());

35 System.out.println("Before: b=" + b.getName());

36 swap(a, b);

37 System.out.println("After: a=" + a.getName());

38 System.out.println("After: b=" + b.getName());

39 }

40

41 public static void tripleValue(double x) // doesn't work

42 {

43 x = 3 * x;

44 System.out.println("End of method: x=" + x);

45 }

46

47 public static void tripleSalary(Employee x) // works

48 {

49 x.raiseSalary(200);

50 System.out.println("End of method: salary=" + x.getSalary());

51 }

52

53 public static void swap(Employee x, Employee y)

54 {

55 Employee temp = x;

56 x = y;

57 y = temp;

58 System.out.println("End of method: x=" + x.getName());

59 System.out.println("End of method: y=" + y.getName());

60 }

61 }

62

63 class Employee // simplified Employee class

64 {

65 private String name;

66 private double salary;

67

68 public Employee(String n, double s)

69 {

70 name = n;

71 salary = s;

72 }

73

74 public String getName()

75 {

76 return name;

77 }

78

79 public double getSalary()

80 {

81 return salary;

82 }

83

84 public void raiseSalary(double byPercent)

85 {

86 double raise = salary * byPercent / 100;

87 salary += raise;

88 }

89 }

4.5 方法参数

首先回顾一下在程序设计语言中有关将参数传递给方法（或函数）的一些专业术语。按值调用（call by value）表示方法接收的是调用者提供的值。而按引用调用（call by reference）表示方法接收的是调用者提供的变量地址。一个方法可以修改传递引用所对应的变量值，而不能修改传递值调用所对应的变量值。「按…… 调用」（call by）是一个标准的计算机科学术语，它用来描述各种程序设计语言（不只是 Java）中方法参数的传递方式（事实上，以前还有按名调用（call by name），Algol 程序设计语言是最古老的高级程序设计语言之一，它使用的就是这种参数传递方式。不过，对于今天，这种传递方式已经成为历史）。Java 程序设计语言总是采用按值调用。也就是说，方法得到的是所有参数值的一个拷贝，特别是，方法不能修改传递给它的任何参数变量的内容。例如，考虑下面的调用：不必理睬这个方法的具体实现，在方法调用之后，percent 的值还是 10。下面再仔细地研究一下这种情况。假定一个方法试图将一个参数值增加至 3 倍：然后调用这个方法：

不过，并没有做到这一点。调用这个方法之后，percent 的值还是 10。下面看一下具体的执行过程：1）x 被初始化为 percent 值的一个拷贝（也就是 10）。2）x 被乘以 3 后等于 30。但是 percent 仍然是 10（如图 4-6 所示）。图 4-6 对值参数的修改没有保留下来 3）这个方法结束之后，参数变量 x 不再使用。然而，方法参数共有两种类型：·基本数据类型（数字、布尔值）。·对象引用。

读者已经看到，一个方法不可能修改一个基本数据类型的参数。而对象引用作为参数就不同了，可以很容易地利用下面这个方法实现将一个雇员的薪金提高两倍的操作：当调用时，具体的执行过程为：1）x 被初始化为 harry 值的拷贝，这里是一个对象的引用。2）raiseSalary 方法应用于这个对象引用。x 和 harry 同时引用的那个 Employee 对象的薪金提高了 200%。3）方法结束后，参数变量 x 不再使用。当然，对象变量 harry 继续引用那个薪金增至 3 倍的雇员对象（如图 4-7 所示）。

图 4-7 对对象参数的修改保留了下来读者已经看到，实现一个改变对象参数状态的方法并不是一件难事。理由很简单，方法得到的是对象引用的拷贝，对象引用及其他的拷贝同时引用同一个对象。很多程序设计语言（特别是，C++ 和 Pascal）提供了两种参数传递的方式：值调用和引用调用。有些程序员（甚至本书的作者）认为 Java 程序设计语言对对象采用的是引用调用，实际上，这种理解是不对的。由于这种误解具有一定的普遍性，所以下面给出一个反例来详细地阐述一下这个问题。首先，编写一个交换两个雇员对象的方法：如果 Java 对对象采用的是按引用调用，那么这个方法就应该能够实现交换数据的效果：但是，方法并没有改变存储在变量 a 和 b 中的对象引用。swap 方法的参数 x 和 y 被初始化为两个对象引用的拷贝，这个方法交换的是这两个拷贝。最终，白费力气。在方法结束时参数变量 x 和 y 被丢弃了。原来的变量 a 和 b 仍然引用这个方法调用之前所引用的对象（如图 4-8 所示）。

图 4-8 交换对象参数的结果没有保留下来这个过程说明：Java 程序设计语言对对象采用的不是引用调用，实际上，对象引用是按值传递的。下面总结一下 Java 中方法参数的使用情况：·一个方法不能修改一个基本数据类型的参数（即数值型或布尔型）。·一个方法可以改变一个对象参数的状态。·一个方法不能让对象参数引用一个新的对象。程序清单 4-4 中的程序给出了相应的演示。在这个程序中，首先试图将一个值参数的值提高两倍，但没有成功：随后，成功地将一个雇员的薪金提高了两倍：方法结束之后，harry 引用的对象状态发生了改变。这是因为这个方法可以通过对象引用的拷贝修改所引用的对象状态。最后，程序演示了 swap 方法的失败效果：

可以看出，参数变量 x 和 y 交换了，但是变量 a 和 b 没有受到影响。C++ 注释：C++ 有值调用和引用调用。引用参数标有 & 符号。例如，可以轻松地实现 void tripleValue（double&x）方法或 void swap（Employee&x，Employee&y）方法实现修改它们的引用参数的目的。程序清单 4-4 ParamTest/ParamTest.java

### 4.6 Object Construction

You have seen how to write simple constructors that define the initial state of your objects. However, since object construction is so important, Java offers quite a variety of mechanisms for writing constructors. We go over these mechanisms in the sections that follow.

4.6 对象构造

前面已经学习了编写简单的构造器，可以定义对象的初始状态。但是，由于对象构造非常重要，所以 Java 提供了多种编写构造器的机制。下面将详细地介绍这些机制。

#### 4.6.1 Overloading

Some classes have more than one constructor. For example, you can construct an empty StringBuilder object as



var messages = new StringBuilder();

Alternatively, you can specify an initial string:



var todoList = new StringBuilder("To do:\n");

This capability is called overloading. Overloading occurs if several methods have the same name (in this case, the StringBuilder constructor method) but different parameters. The compiler must sort out which method to call. It picks the correct method by matching the parameter types in the headers of the various methods with the types of the values used in the specific method call. A compile-time error occurs if the compiler cannot match the parameters, either because there is no match at all or because there is not one that is better than all others. (The process of finding a match is called overloading resolution.)

Note

Java allows you to overload any method — not just constructor methods. Thus, to completely describe a method, you need to specify its name together with its parameter types. This is called the signature of the method. For example, the String class has four public methods called indexOf. They have signatures



indexOf(int)

indexOf(int, int)

indexOf(String)

indexOf(String, int)

The return type is not part of the method signature. That is, you cannot have two methods with the same names and parameter types but different return types.

4.6.1 重载

有些类有多个构造器。例如，可以如下构造一个空的 StringBuilder 对象：或者，可以指定一个初始字符串：这种特征叫做重载（overloading）。如果多个方法（比如，StringBuilder 构造器方法）有相同的名字、不同的参数，便产生了重载。编译器必须挑选出具体执行哪个方法，它通过用各个方法给出的参数类型与特定方法调用所使用的值类型进行匹配来挑选出相应的方法。如果编译器找不到匹配的参数，就会产生编译时错误，因为根本不存在匹配，或者没有一个比其他的更好。（这个过程被称为重载解析（overloading resolution）。）注释：Java 允许重载任何方法，而不只是构造器方法。因此，要完整地描述一个方法，需要指出方法名以及参数类型。这叫做方法的签名（signature）。例如，String 类有 4 个称为 indexOf 的公有方法。它们的签名是

返回类型不是方法签名的一部分。也就是说，不能有两个名字相同、参数类型也相同却返回不同类型值的方法。

#### 4.6.2 Default Field Initialization

If you don't set a field explicitly in a constructor, it is automatically set to a default value: numbers to 0, boolean values to false, and object references to null. Some people consider it poor programming practice to rely on the defaults. Certainly, it makes it harder for someone to understand your code if fields are being initialized invisibly.

Note

This is an important difference between fields and local variables. You must always explicitly initialize local variables in a method. But in a class, if you don't initialize a field, it is automatically initialized to a default (0, false, or null).

For example, consider the Employee class. Suppose you don't specify how to initialize some of the fields in a constructor. By default, the salary field would be initialized with 0 and the name and hireDay fields would be initialized with null.

However, that would not be a good idea. If anyone called the getName or getHireDay method, they would get a null reference that they probably don't expect:



LocalDate h = harry.getHireDay();

int year = h.getYear(); // throws exception if h is null

4.6.2 默认域初始化

如果在构造器中没有显式地给域赋予初值，那么就会被自动地赋为默认值：数值为 0、布尔值为 false、对象引用为 null。然而，只有缺少程序设计经验的人才会这样做。确实，如果不明确地对域进行初始化，就会影响程序代码的可读性。注释：这是域与局部变量的主要不同点。必须明确地初始化方法中的局部变量。但是，如果没有初始化类中的域，将会被自动初始化为默认值（0、false 或 null）。例如，仔细看一下 Employee 类。假定没有在构造器中对某些域进行初始化，就会默认地将 salary 域初始化为 0，将 name 和 hireDay 域初始化为 null。但是，这并不是一种良好的编程习惯。如果此时调用 getName 方法或 getHireDay 方法，则会得到一个 null 引用，这应该不是我们所希望的结果：

#### 4.6.3 The Constructor with No Arguments

Many classes contain a constructor with no arguments that creates an object whose state is set to an appropriate default. For example, here is a no-argument constructor for the Employee class:



public Employee()

{

name = "";

salary = 0;

hireDay = LocalDate.now();

}

If you write a class with no constructors whatsoever, then a no-argument constructor is provided for you. This constructor sets all the instance fields to their default values. So, all numeric data contained in the instance fields would be 0, all boolean values would be false, and all object variables would be null.

If a class supplies at least one constructor but does not supply a no-argument constructor, it is illegal to construct objects without supplying arguments. For example, our original Employee class in Listing 4.2 provided a single constructor:



public Employee(String n, double s, int year, int month, int day)

With that class, it was not legal to construct default employees. That is, the call

e = new Employee();

would have been an error.

Caution

Please keep in mind that you get a free no-argument constructor only when your class has no other constructors. If you write your class with even a single constructor of your own and you want the users of your class to have the ability to create an instance by a call to

new ClassName()

then you must provide a no-argument constructor. Of course, if you are happy with the default values for all fields, you can simply supply



public ClassName()

{

}

4.6.3 无参数的构造器

很多类都包含一个无参数的构造函数，对象由无参数构造函数创建时，其状态会设置为适当的默认值。例如，以下是 Employee 类的无参数构造函数：

如果在编写一个类时没有编写构造器，那么系统就会提供一个无参数构造器。这个构造器将所有的实例域设置为默认值。于是，实例域中的数值型数据设置为 0、布尔型数据设置为 false、所有对象变量将设置为 null。如果类中提供了至少一个构造器，但是没有提供无参数的构造器，则在构造对象时如果没有提供参数就会被视为不合法。例如，在程序清单 4-2 中的 Employee 类提供了一个简单的构造器：对于这个类，构造默认的雇员属于不合法。也就是，调用将会产生错误。警告：请记住，仅当类没有提供任何构造器的时候，系统才会提供一个默认的构造器。如果在编写类的时候，给出了一个构造器，哪怕是很简单的，要想让这个类的用户能够采用下列方式构造实例：就必须提供一个默认的构造器（即不带参数的构造器）。当然，如果希望所有域被赋予默认值，可以采用下列格式：

#### 4.6.4 Explicit Field Initialization

By overloading the constructor methods in a class, you can build many ways to set the initial state of the instance fields of your classes. It is always a good idea to make sure that, regardless of the constructor call, every instance field is set to something meaningful.

You can simply assign a value to any field in the class definition. For example:



class Employee

{

private String name = "";

. . .

}

This assignment is carried out before the constructor executes. This syntax is particularly useful if all constructors of a class need to set a particular instance field to the same value.

The initialization value doesn't have to be a constant value. Here is an example in which a field is initialized with a method call. Consider an Employee class where each employee has an id field. You can initialize it as follows:



class Employee

{

private static int nextId;

private int id = assignId();

. . .

private static int assignId()

{

int r = nextId;

nextId++;

return r;

}

. . .

}

C++ Note

In C++, you cannot directly initialize instance fields of a class. All fields must be set in a constructor. However, C++ has a special initializer list syntax, such as



Employee::Employee(String n, double s, int y, int m, int d) // C++

: name(n),

salary(s),

hireDay(y, m, d)

{

}

C++ uses this special syntax to call field constructors. In Java, there is no need for that because objects have no subobjects, only pointers to other objects.

4.6.4 显式域初始化

通过重载类的构造器方法，可以采用多种形式设置类的实例域的初始状态。确保不管怎样调用构造器，每个实例域都可以被设置为一个有意义的初值，这是一种很好的设计习惯。可以在类定义中，直接将一个值赋给任何域。例如：在执行构造器之前，先执行赋值操作。当一个类的所有构造器都希望把相同的值赋予某个特定的实例域时，这种方式特别有用。初始值不一定是常量值。在下面的例子中，可以调用方法对域进行初始化。仔细看一下 Employee 类，其中每个雇员有一个 id 域。可以使用下列方式进行初始化：C++ 注释：在 C++ 中，不能直接初始化类的实例域。所有的域必须在构造器中设置。但是，有一个特殊的初始化器列表语法，如下所示：C++ 使用这种特殊的语法来调用域构造器。在 Java 中没有这种必要，因为对象没有子对象，只有指向其他对象的指针。

#### 4.6.5 Parameter Names

When you write very trivial constructors (and you'll write a lot of them), it can be somewhat frustrating to come up with parameter names.

We have generally opted for single-letter parameter names:



public Employee(String n, double s)

{

name = n;

salary = s;

}

However, the drawback is that you need to read the code to tell what the n and s parameters mean.

Some programmers prefix each parameter with an「a」:



public Employee(String aName, double aSalary)

{

name = aName;

salary = aSalary;

}

That is quite neat. Any reader can immediately figure out the meaning of the parameters.

Another commonly used trick relies on the fact that parameter variables shadow instance fields with the same name. For example, if you call a parameter salary, then salary refers to the parameter, not the instance field. But you can still access the instance field as this.salary. Recall that this denotes the implicit parameter — that is, the object being constructed. Here is an example:



public Employee(String name, double salary)

{

this.name = name;

this.salary = salary;

}

C++ Note: In C++, it is common to prefix instance fields with an underscore or a fixed letter. (The letters m and x are common choices.) For example, the salary field might be called _salary, mSalary, or xSalary. Java programmers don't usually do that.

4.6.5 参数名

在编写很小的构造器时（这是十分常见的），常常在参数命名上出现错误。通常，参数用单个字符命名：但这样做有一个缺陷：只有阅读代码才能够了解参数 n 和参数 s 的含义。有些程序员在每个参数前面加上一个前缀「a」：这样很清晰。每一个读者一眼就能够看懂参数的含义。还一种常用的技巧，它基于这样的事实：参数变量用同样的名字将实例域屏蔽起来。例如，如果将参数命名为 salary，salary 将引用这个参数，而不是实例域。但是，可以采用 this.salary 的形式访问实例域。回想一下，this 指示隐式参数，也就是所构造的对象。下面是一个示例：C++ 注释：在 C++ 中，经常用下划线或某个固定的字母（一般选用 m 或 x）作为实例域的前缀。例如，salary 域可能被命名为_salary、mSalary 或 xSalary。Java 程序员通常不这样做。

#### 4.6.6 Calling Another Constructor

The keyword this refers to the implicit parameter of a method. However, this keyword has a second meaning.

If the first statement of a constructor has the form this(. . .), then the constructor calls another constructor of the same class. Here is a typical example:



public Employee(double s)

{

// calls Employee(String, double)

this("Employee #" + nextId, s);

nextId++;

}

When you call new Employee(60000), the Employee(double) constructor calls the Employee(String, double) constructor.

Using the this keyword in this manner is useful — you only need to write common construction code once.

C++ Note: The this reference in Java is identical to the this pointer in C++. However, in C++ it is not possible for one constructor to call another. If you want to factor out common initialization code in C++, you must write a separate method.

4.6.6 调用另一个构造器

关键字 this 引用方法的隐式参数。然而，这个关键字还有另外一个含义。如果构造器的第一个语句形如 this（...），这个构造器将调用同一个类的另一个构造器。下面是一个典型的例子：当调用 new Employee（60000）时，Employee（double）构造器将调用 Employee（String，double）构造器。采用这种方式使用 this 关键字非常有用，这样对公共的构造器代码部分只编写一次即可。C++ 注释：在 Java 中，this 引用等价于 C++ 的 this 指针。但是，在 C++ 中，一个构造器不能调用另一个构造器。在 C++ 中，必须将抽取出的公共初始化代码编写成一个独立的方法。

#### 4.6.7 Initialization Blocks

You have already seen two ways to initialize a data field:

By setting a value in a constructor

By assigning a value in the declaration

There is a third mechanism in Java, called an initialization block. Class declarations can contain arbitrary blocks of code. These blocks are executed whenever an object of that class is constructed. For example:



class Employee

{

private static int nextId;

private int id;

private String name;

private double salary;

// object initialization block

{

id = nextId;

nextId++;

}

public Employee(String n, double s)

{

name = n;

salary = s;

}

public Employee()

{

name = "";

salary = 0;

}

. . .

}

In this example, the id field is initialized in the object initialization block, no matter which constructor is used to construct an object. The initialization block runs first, and then the body of the constructor is executed.

This mechanism is never necessary and is not common. It is usually more straightforward to place the initialization code inside a constructor.

Note: It is legal to set fields in initialization blocks even if they are only defined later in the class. However, to avoid circular definitions, it is not legal to read from fields that are only initialized later. The exact rules are spelled out in Section 8.3.2.3 of the Java Language Specification (http://docs.oracle.com/javase/specs). The rules are complex enough to baffle the compiler implementors — early versions of Java implemented them with subtle errors. Therefore, we suggest that you always place initialization blocks after the field definitions.

With so many ways of initializing data fields, it can be quite confusing to give all possible pathways for the construction process. Here is what happens in detail when a constructor is called:

If the first line of the constructor calls a second constructor, then the second constructor executes with the provided arguments.

Otherwise,

All data fields are initialized to their default values (0, false, or null).

All field initializers and initialization blocks are executed, in the order in which they occur in the class declaration.

The body of the constructor is executed.

Naturally, it is always a good idea to organize your initialization code so that another programmer could easily understand it without having to be a language lawyer. For example, it would be quite strange and somewhat error-prone to have a class whose constructors depend on the order in which the data fields are declared.

To initialize a static field, either supply an initial value or use a static initialization block. You have already seen the first mechanism:



private static int nextId = 1;

If the static fields of your class require complex initialization code, use a static initialization block.

Place the code inside a block and tag it with the keyword static. Here is an example. We want the employee ID numbers to start at a random integer less than 10,000.



// static initialization block

static

{

var generator = new Random();

nextId = generator.nextInt(10000);

}

Static initialization occurs when the class is first loaded. Like instance fields, static fields are 0, false, or null unless you explicitly set them to another value. All static field initializers and static initialization blocks are executed in the order in which they occur in the class declaration.

Note

Amazingly enough, up to JDK 6, it was possible to write a「Hello, World」program in Java without ever writing a main method.



public class Hello

{

static

{

System.out.println("Hello, World");

}

}

When you invoked the class with java Hello, the class was loaded, the static initialization block printed「Hello, World」, and only then was a message displayed that main is not defined. Since Java 7, the java program first checks that there is a main method.

The program in Listing 4.5 shows many of the features that we discussed in this section:

Overloaded constructors

A call to another constructor with this(. . .)

A no-argument constructor

An object initialization block

A static initialization block

An instance field initialization

Listing 4.5 ConstructorTest/ConstructorTest.java



1 import java.util.*;

2

3 /**

4 * This program demonstrates object construction.

5 * @version 1.02 2018-04-10

6 * @author Cay Horstmann

7 */

8 public class ConstructorTest

9 {

10 public static void main(String[] args)

11 {

12 // fill the staff array with three Employee objects

13 var staff = new Employee[3];

14

15 staff[0] = new Employee("Harry", 40000);

16 staff[1] = new Employee(60000);

17 staff[2] = new Employee();

18

19 // print out information about all Employee objects

20 for (Employee e : staff)

21 System.out.println("name=" + e.getName() + ",id=" + e.getId() + ",salary="

22 + e.getSalary());

23 }

24 }

25

26 class Employee

27 {

28 private static int nextId;

29

30 private int id;

31 private String name = ""; // instance field initialization

32 private double salary;

33

34 // static initialization block

35 static

36 {

37 var generator = new Random();

38 // set nextId to a random number between 0 and 9999

39 nextId = generator.nextInt(10000);

40 }

41

42 // object initialization block

43 {

44 id = nextId;

45 nextId++;

46 }

47

48 // three overloaded constructors

49 public Employee(String n, double s)

50 {

51 name = n;

52 salary = s;

53 }

54

55 public Employee(double s)

56 {

57 // calls the Employee(String, double) constructor

58 this("Employee #" + nextId, s);

59 }

60

61 // the default constructor

62 public Employee()

63 {

64 // name initialized to ""--see above

65 // salary not explicitly set--initialized to 0

66 // id initialized in initialization block

67 }

68

69 public String getName()

70 {

71 return name;

72 }

73

74 public double getSalary()

75 {

76 return salary;

77 }

78

79 public int getId()

80 {

81 return id;

82 }

83 }

java.util.Random 1.0

Random()

constructs a new random number generator.

int nextInt(int n) 1.2

returns a random number between 0 and n – 1.

4.6.7 初始化块

前面已经讲过两种初始化数据域的方法：·在构造器中设置值·在声明中赋值实际上，Java 还有第三种机制，称为初始化块（initialization block）。在一个类的声明中，可以包含多个代码块。只要构造类的对象，这些块就会被执行。例如，

在这个示例中，无论使用哪个构造器构造对象，id 域都在对象初始化块中被初始化。首先运行初始化块，然后才运行构造器的主体部分。这种机制不是必需的，也不常见。通常会直接将初始化代码放在构造器中。注释：即使在类的后面定义，仍然可以在初始化块中设置域。但是，为了避免循环定义，不要读取在后面初始化的域。具体的规则请参看 Java 语言规范的 8.3.2.3 节（http://docs.oracle.com/javase/specs）。这个规则的复杂度足以使编译器的实现者头疼，因此建议将初始化块放在域定义之后。由于初始化数据域有多种途径，所以列出构造过程的所有路径可能相当混乱。下面是调用构造器的具体处理步骤：1）所有数据域被初始化为默认值（0、false 或 null）。2）按照在类声明中出现的次序，依次执行所有域初始化语句和初始化块。3）如果构造器第一行调用了第二个构造器，则执行第二个构造器主体。4）执行这个构造器的主体。当然，应该精心地组织好初始化代码，这样有利于其他程序员的理解。例如，如果让类的构造器行为依赖于数据域声明的顺序，那就会显得很奇怪并且容易引起错误。

可以通过提供一个初始化值，或者使用一个静态的初始化块来对静态域进行初始化。前面已经介绍过第一种机制：如果对类的静态域进行初始化的代码比较复杂，那么可以使用静态的初始化块。将代码放在一个块中，并标记关键字 static。下面是一个示例。其功能是将雇员 ID 的起始值赋予一个小于 10000 的随机整数。在类第一次加载的时候，将会进行静态域的初始化。与实例域一样，除非将它们显式地设置成其他值，否则默认的初始值是 0、false 或 null。所有的静态初始化语句以及静态初始化块都将依照类定义的顺序执行。注释：让人惊讶的是，在 JDK 6 之前，都可以用 Java 编写一个没有 main 方法的「Hello，World」程序。当用 java Hello 调用这个类时，就会加载这个类，静态初始化块将会打印「Hello，World」。在此之后，会显示一个消息指出 main 未定义。从 JavaSE 7 以后，java 程序首先会检查是否有一个 main 方法。程序清单 4-5 中的程序展示了本节讨论的很多特性：

·重载构造器·用 this（...）调用另一个构造器·无参数构造器·对象初始化块·静态初始化块·实例域初始化程序清单 4-5 ConstructorTest/ConstructorTest.java

java.util.Random 1.0·Random（）构造一个新的随机数生成器。·int nextInt（int n）1.2 返回一个 0~n-1 之间的随机数。

#### 4.6.8 Object Destruction and the finalize Method

Some object-oriented programming languages, notably C++, have explicit destructor methods for any cleanup code that may be needed when an object is no longer used. The most common activity in a destructor is reclaiming the memory set aside for objects. Since Java does automatic garbage collection, manual memory reclamation is not needed, so Java does not support destructors.

Of course, some objects utilize a resource other than memory, such as a file or a handle to another object that uses system resources. In this case, it is important that the resource be reclaimed and recycled when it is no longer needed.

If a resource needs to be closed as soon as you have finished using it, supply a close method that does the necessary cleanup. You can call the close method when you are done with the object. In Chapter 7, you will see how you can ensure that this method is called automatically.

If you can wait until the virtual machine exits, add a「shutdown hook」with the method Runtime.addShutdownHook. As of Java 9, you can use the Cleaner class to register an action that is carried out when an object is no longer reachable (other than by the cleaner). These are uncommon situations in practice. See the API documentation for details on these two approaches.

Caution: Do not use the finalize method for cleanup. That method was intended to be called before the garbage collector sweeps away an object. However, you simply cannot know when this method will be called, and it is now deprecated.

4.6.8 对象析构与 finalize 方法

有些面向对象的程序设计语言，特别是 C++，有显式的析构器方法，其中放置一些当对象不再使用时需要执行的清理代码。在析构器中，最常见的操作是回收分配给对象的存储空间。由于 Java 有自动的垃圾回收器，不需要人工回收内存，所以 Java 不支持析构器。当然，某些对象使用了内存之外的其他资源，例如，文件或使用了系统资源的另一个对象的句柄。在这种情况下，当资源不再需要时，将其回收和再利用将显得十分重要。可以为任何一个类添加 finalize 方法。finalize 方法将在垃圾回收器清除对象之前调用。在实际应用中，不要依赖于使用 finalize 方法回收任何短缺的资源，这是因为很难知道这个方法什么时候才能够调用。

注释：有个名为 System.runFinalizersOnExit（true）的方法能够确保 finalizer 方法在 Java 关闭前被调用。不过，这个方法并不安全，也不鼓励大家使用。有一种代替的方法是使用方法 Runtime.addShutdownHook 添加「关闭钩」（shutdown hook），详细内容请参看 API 文档。如果某个资源需要在使用完毕后立刻被关闭，那么就需要由人工来管理。对象用完时，可以应用一个 close 方法来完成相应的清理操作。7.2.5 节会介绍如何确保这个方法自动得到调用。

### 4.7 Packages

Java allows you to group classes in a collection called a package. Packages are convenient for organizing your work and for separating your work from code libraries provided by others. In the following sections, you will learn how to use and create packages.

4.7 包

Java 允许使用包（package）将类组织起来。借助于包可以方便地组织自己的代码，并将自己的代码与别人提供的代码库分开管理。标准的 Java 类库分布在多个包中，包括 java.lang、java.util 和 java.net 等。标准的 Java 包具有一个层次结构。如同硬盘的目录嵌套一样，也可以使用嵌套层次组织包。所有标准的 Java 包都处于 java 和 javax 包层次中。使用包的主要原因是确保类名的唯一性。假如两个程序员不约而同地建立了 Employee 类。只要将这些类放置在不同的包中，就不会产生冲突。事实上，为了保证包名的绝对唯一性，Sun 公司建议将公司的因特网域名（这显然是独一无二的）以逆序的形式作为包名，并且对于不同的项目使用不同的子包。例如，horstmann.com 是本书作者之一注册的域名。逆序形式为 com.horstmann。这个包还可以被进一步地划分成子包，如 com.horstmann.corejava。从编译器的角度来看，嵌套的包之间没有任何关系。例如，java.util 包与 java.util.jar 包毫无关系。每一个都拥有独立的类集合。

#### 4.7.1 Package Names

The main reason for using packages is to guarantee the uniqueness of class names. Suppose two programmers come up with the bright idea of supplying an Employee class. As long as both of them place their class into different packages, there is no conflict. In fact, to absolutely guarantee a unique package name, use an Internet domain name (which is known to be unique) written in reverse. You then use subpackages for different projects. For example, consider the domain horstmann.com. When written in reverse order, it turns into the package name com.horstmann. You can then append a project name, such as com.horstmann.corejava. If you then place the Employee class into that package, the「fully qualified」name becomes com.horstmann.corejava.Employee.

Note

From the point of view of the compiler, there is absolutely no relationship between nested packages. For example, the packages java.util and java.util.jar have nothing to do with each other. Each is its own independent collection of classes.

#### 4.7.2 Class Importation

A class can use all classes from its own package and all public classes from other packages.

You can access the public classes in another package in two ways. The first is simply to use the fully qualified name; that is, the package name followed by the class name. For example:



java.time.LocalDate today = java.time.LocalDate.now();

That is obviously tedious. A simpler, and more common, approach is to use the import statement. The point of the import statement is to give you a shorthand to refer to the classes in the package. Once you add an import, you no longer have to give the classes their full names.

You can import a specific class or the whole package. You place import statements at the top of your source files (but below any package statements). For example, you can import all classes in the java.time package with the statement

import java.time.*;

Then you can use



LocalDate today = LocalDate.now();

without a package prefix. You can also import a specific class inside a package:



import java.time.LocalDate;

The java.time.* syntax is less tedious. It has no negative effect on code size. However, if you import classes explicitly, the reader of your code knows exactly which classes you use.

Tip

In Eclipse, you can select the menu option Source → Organize Imports. Package statements such as import java.util.*; are automatically expanded into a list of specific imports such as



import java.util.ArrayList;

import java.util.Date;

This is an extremely convenient feature.

However, note that you can only use the * notation to import a single package. You cannot use import java.* or import java.*.* to import all packages with the java prefix.

Most of the time, you just import the packages that you need, without worrying too much about them. The only time that you need to pay attention to packages is when you have a name conflict. For example, both the java.util and java.sql packages have a Date class. Suppose you write a program that imports both packages.



import java.util.*;

import java.sql.*;

If you now use the Date class, you get a compile-time error:



Date today; // ERROR--java.util.Date or java.sql.Date?

The compiler cannot figure out which Date class you want. You can solve this problem by adding a specific import statement:



import java.util.*;

import java.sql.*;

import java.util.Date;

What if you really need both Date classes? Then use the full package name with every class name:



var deadline = new java.util.Date();

var today = new java.sql.Date(. . .);

Locating classes in packages is an activity of the compiler. The bytecodes in class files always use full package names to refer to other classes.

C++ Note

C++ programmers sometimes confuse import with #include. The two have nothing in common. In C++, you must use #include to include the declarations of external features because the C++ compiler does not look inside any files except the one that it is compiling and its explicitly included header files. The Java compiler will happily look inside other files provided you tell it where to look.

In Java, you can entirely avoid the import mechanism by explicitly naming all classes, such as java.util.Date. In C++, you cannot avoid the #include directives.

The only benefitofthe import statement is convenience. You can refer to a class by a name shorter than the full package name. For example, after an import java.util.* (or import java.util.Date) statement, you can refer to the java.util.Date class simply as Date.

In C++, the construction analogous to the package mechanism is the namespace feature. Think of the package and import statements in Java as the analogs of the namespace and using directives in C++.

4.7.1 类的导入

一个类可以使用所属包中的所有类，以及其他包中的公有类（publicclass）。我们可以采用两种方式访问另一个包中的公有类。第一种方式是在每个类名之前添加完整的包名。例如：这显然很繁琐。更简单且更常用的方式是使用 import 语句。import 语句是一种引用包含在包中的类的简明描述。一旦使用了 import 语句，在使用类时，就不必写出包的全名了。可以使用 import 语句导入一个特定的类或者整个包。import 语句应该位于源文件的顶部（但位于 package 语句的后面）。例如，可以使用下面这条语句导入 java.util 包中所有的类。然后，就可以使用而无须在前面加上包前缀。还可以导入一个包中的特定类：java.time.`*` 的语法比较简单，对代码的大小也没有任何负面影响。当然，如果能够明确地指出所导入的类，将会使代码的读者更加准确地知道加载了哪些类。提示：在 Eclipse 中，可以使用菜单选项 Source→Organize Imports。Package 语句，如 import java.util.*；将会自动地扩展指定的导入列表，如：

这是一个十分便捷的特性。但是，需要注意的是，只能使用星号（*）导入一个包，而不能使用 importjava.* 或 import java.*.* 导入以 java 为前缀的所有包。在大多数情况下，只导入所需的包，并不必过多地理睬它们。但在发生命名冲突的时候，就不能不注意包的名字了。例如，java.util 和 java.sql 包都有日期（Date）类。如果在程序中导入了这两个包：在程序使用 Date 类的时候，就会出现一个编译错误：此时编译器无法确定程序使用的是哪一个 Date 类。可以采用增加一个特定的 import 语句来解决这个问题：如果这两个 Date 类都需要使用，又该怎么办呢？答案是，在每个类名的前面加上完整的包名。在包中定位类是编译器（compiler）的工作。类文件中的字节码肯定使用完整的包名来引用其他类。

C++ 注释：C++ 程序员经常将 import 与 #include 弄混。实际上，这两者之间并没有共同之处。在 C++ 中，必须使用 #include 将外部特性的声明加载进来，这是因为 C++ 编译器无法查看任何文件的内部，除了正在编译的文件以及在头文件中明确包含的文件。Java 编译器可以查看其他文件的内部，只要告诉它到哪里去查看就可以了。在 Java 中，通过显式地给出包名，如 java.util.Date，就可以不使用 import；而在 C++ 中，无法避免使用 #include 指令。Import 语句的唯一的好处是简捷。可以使用简短的名字而不是完整的包名来引用一个类。例如，在 import java.util.*（或 import java.util.Date）语句之后，可以仅仅用 Date 引用 java.util.Date 类。在 C++ 中，与包机制类似的是命名空间（namespace）。在 Java 中，package 与 import 语句类似于 C++ 中的 namespace 和 using 指令。

#### 4.7.3 Static Imports

A form of the import statement permits the importing of static methods and fields, not just classes.

For example, if you add the directive



import static java.lang.System.*;

to the top of your source file, then you can use the static methods and fields of the System class without the class name prefix:



out.println("Goodbye, World!"); // i.e., System.out

exit(0); // i.e., System.exit

You can also import a specific method or field:



import static java.lang.System.out;

In practice, it seems doubtful that many programmers will want to abbreviate System.out or System.exit. The resulting code seems less clear. On the other hand,



sqrt(pow(x, 2) + pow(y, 2))

seems much clearer than



Math.sqrt(Math.pow(x, 2) + Math.pow(y, 2))

4.7.2 静态导入

import 语句不仅可以导入类，还增加了导入静态方法和静态域的功能。例如，如果在源文件的顶部，添加一条指令：

就可以使用 System 类的静态方法和静态域，而不必加类名前缀：另外，还可以导入特定的方法或域：实际上，是否有更多的程序员采用 System.out 或 System.exit 的简写形式，似乎是一件值得怀疑的事情。这种编写形式不利于代码的清晰度。不过，看起来比清晰得多。4.7.3 将类放入包中要想将一个类放入包中，就必须将包的名字放在源文件的开头，包中定义类的代码之前。例如，程序清单 4-7 中的文件 Employee.java 开头是这样的：

如果没有在源文件中放置 package 语句，这个源文件中的类就被放置在一个默认包（defaulf package）中。默认包是一个没有名字的包。在此之前，我们定义的所有类都在默认包中。将包中的文件放到与完整的包名匹配的子目录中。例如，com.horstmann.corejava 包中的所有源文件应该被放置在子目录 com/horstmann/corejava（Windows 中 com\horstmann\corejava）中。编译器将类文件也放在相同的目录结构中。程序清单 4-6 和程序清单 4-7 中的程序分放在两个包中：PackageTest 类放置在默认包中；Employee 类放置在 com.horstmann.corejava 包中。因此，Employee.java 文件必须包含在子目录 com/horstmann/corejava 中。换句话说，目录结构如下所示：要想编译这个程序，只需改变基目录，并运行命令编译器就会自动地查找文件 com/horstmann/corejava/Employee.java 并进行编译。

下面看一个更加实际的例子。在这里不使用默认包，而是将类分别放在不同的包中（com.horstmann.corejava 和 com.mycompany）。在这种情况下，仍然要从基目录编译和运行类，即包含 com 目录：需要注意，编译器对文件（带有文件分隔符和扩展名.java 的文件）进行操作。而 Java 解释器加载类（带有。分隔符）。提示：从下一章开始，我们将对源代码使用包。这样一来，就可以为各章建立一个 IDE 工程，而不是各小节分别建立工程。警告：编译器在编译源文件的时候不检查目录结构。例如，假定有一个源文件开头有下列语句：即使这个源文件没有在子目录 com/mycompany 下，也可以进行编译。如果它不依赖于其他包，就不会出现编译错误。但是，最终的程序将无法运行，除非先将所有类文件移到正确的位置上。如果包与目录不匹配，虚拟机就找不到类。程序清单 4-6 PackageTest/PackageTest.java

程序清单 4-7 PackageTest/com/horstmann/corejava/Employee.java

#### 4.7.4 Addition of a Class into a Package

To place classes inside a package, put the name of the package at the top of your source file, before the code that defines the classes in the package. For example, the file Employee.java in Listing 4.7 starts out like this:



package com.horstmann.corejava;

public class Employee

{

. . .

}

If you don't put a package statement in the source file, then the classes in that source file belong to the unnamed package. The unnamed package has no package name. Up to now, all our example classes were located in the unnamed package.

Place source files into a subdirectory that matches the full package name. For example, all source files in the com.horstmann.corejava package should be in a subdirectory com/horstmann/corejava (com\horstmann\corejava on Windows). The compiler places the class files into the same directory structure.

The program in Listings 4.6 and 4.7 is distributed over two packages: The PackageTest class belongs to the unnamed package, and the Employee class belongs to the com.horstmann.corejava package. Therefore, the Employee.java file must be in a subdirectory com/horstmann/corejava. In other words, the directory structure is as follows:



. (base directory)

├─ PackageText.java

├─ PackageText.class

└─ com/

└─ horstmann/

└─ corejava/

├─ Employee.java

└─ Employee.class

To compile this program, simply change to the base directory and run the command



javac PackageTest.java

The compiler automatically finds the file com/horstmann/corejava/Employee.java and compiles it.

Let's look at a more realistic example, in which we don't use the unnamed package but have classes distributed over several packages (com.horstmann.corejava and com.mycompany).



. (base directory)

└─ com/

├─ horstmann/

│ └─ corejava/

│ ├─ Employee.java

│ └─ Employee.class

└─ mycompany/

├─ PayrollApp.java

└─ PayrollApp.class

In this situation, you still must compile and run classes from the base directory — that is, the directory containing the com directory:



javac com/mycompany/PayrollApp.java

java com.mycompany.PayrollApp

Note again that the compiler operates on files (with file separators and an extension .java), whereas the Java interpreter loads a class (with dot separators).

Tip

Starting with the next chapter, we will use packages for the source code. That way, you can make an IDE project for each chapter instead of each section.

Caution

The compiler does not check the directory structure when it compiles source files. For example, suppose you have a source file that starts with the directive



package com.mycompany;

You can compile the file even if it is not contained in a subdirectory com/mycompany. The source file will compile without errors if it doesn't depend on other packages. However, the resulting program will not run unless you first move all class files to the right place. The virtual machine won't find the classes if the packages don't match the directories.

Listing 4.6 PackageTest/PackageTest.java



1 import com.horstmann.corejava.*;

2 // the Employee class is defined in that package

3

4 import static java.lang.System.*;

5

6 /**

7 * This program demonstrates the use of packages.

8 * @version 1.11 2004-02-19

9 * @author Cay Horstmann

10 */

11 public class PackageTest

12 {

13 public static void main(String[] args)

14 {

15 // because of the import statement, we don't have to use

16 // com.horstmann.corejava.Employee here

17 var harry = new Employee("Harry Hacker", 50000, 1989, 10, 1);

18

19 harry.raiseSalary(5);

20

21 // because of the static import statement, we don't have to use System.out here

22 out.println("name=" + harry.getName() + ",salary=" + harry.getSalary());

23 }

24 }

Listing 4.7 PackageTest/com/horstmann/corejava/Employee.java



1 package com.horstmann.corejava;

2

3 // the classes in this file are part of this package

4

5 import java.time.*;

6

7 // import statements come after the package statement

8

9 /**

10 * @version 1.11 2015-05-08

11 * @author Cay Horstmann

12 */

13 public class Employee

14 {

15 private String name;

16 private double salary;

17 private LocalDate hireDay;

18

19 public Employee(String name, double salary, int year, int month, int day)

20 {

21 this.name = name;

22 this.salary = salary;

23 hireDay = LocalDate.of(year, month, day);

24 }

25

26 public String getName()

27 {

28 return name;

29 }

30

31 public double getSalary()

32 {

33 return salary;

34 }

35

36 public LocalDate getHireDay()

37 {

38 return hireDay;

39 }

40

41 public void raiseSalary(double byPercent)

42 {

43 double raise = salary * byPercent / 100;

44 salary += raise;

45 }

46 }

#### 4.7.5 Package Access

You have already encountered the access modifiers public and private. Features tagged as public can be used by any class. Private features can be used only by the class that defines them. If you don't specify either public or private, the feature (that is, the class, method, or variable) can be accessed by all methods in the same package.

Consider the program in Listing 4.2. The Employee class was not defined as a public class. Therefore, only the other classes (such as EmployeeTest) in the same package — the unnamed package in this case — can access it. For classes, this is a reasonable default. However, for variables, this was an unfortunate choice. Variables must explicitly be marked private, or they will default to having package access. This, of course, breaks encapsulation. The problem is that it is awfully easy to forget to type the private keyword. Here is an example from the Window class in the java.awt package, which is part of the source code supplied with the JDK:



public class Window extends Container

{

String warningString;

. . .

}

Note that the warningString variable is not private! That means the methods of all classes in the java.awt package can access this variable and set it to whatever they like (such as "Trust me!"). Actually, the only methods that access this variable are in the Window class, so it would have been entirely appropriate to make the variable private. Perhaps the programmer typed the code in a hurry and simply forgot the private modifier? Perhaps nobody cared? After more than twenty years, that variable is still not private. Not only that — new fields have been added to the class over time, and about half of them aren't private either.

This can be a problem. By default, packages are not closed entities. That is, anyone can add more classes to a package. Of course, hostile or clueless programmers can then add code that modifies variables with package access. For example, in early versions of Java, it was an easy matter to smuggle another class into the java.awt package. Simply start out the class with

package java.awt;

Then, place the resulting class file inside a subdirectory java/awt somewhere on the class path, and you have gained access to the internals of the java.awt package. Through this subterfuge, it was possible to set the warning string (see Figure 4.9).

Figure 4.9 Changing the warning string in an applet window

Starting with version 1.2, the JDK implementors rigged the class loader to explicitly disallow loading of user-defined classes whose package name starts with "java.". Of course, your own classes don't benefit from that protection. Another mechanism, now obsolete, lets a JAR file declare packages as sealed, preventing third parties from augmenting them. Nowadays, you should use modules to encapsulate packages. We discuss modules in detail in Chapter 9 of Volume II.

4.7.4 包作用域

前面已经接触过访问修饰符 public 和 private。标记为 public 的部分可以被任意的类使用；标记为 private 的部分只能被定义它们的类使用。如果没有指定 public 或 private，这个部分（类、方法或变量）可以被同一个包中的所有方法访问。下面再仔细地看一下程序清单 4-2。在这个程序中，没有将 Employee 类定义为公有类，因此只有在同一个包（在此是默认包）中的其他类可以访问，例如 EmployeeTest。对于类来说，这种默认是合乎情理的。但是，对于变量来说就有些不适宜了，因此变量必须显式地标记为 private，不然的话将默认为包可见。显然，这样做会破坏封装性。问题主要出于人们经常忘记键入关键字 private。在 java.awt 包中的 Window 类就是一个典型的示例。java.awt 包是 JDK 提供的部分源代码：

请注意，这里的 warningString 变量不是 private！这意味着 java.awt 包中的所有类的方法都可以访问该变量，并将它设置为任意值（例如，「Trustme！」）。实际上，只有 Window 类的方法访问它，因此应该将它设置为私有变量。我们猜测可能是程序员匆忙之中忘记键入 private 修饰符了（为防止程序员内疚，我们没有说出他的名字，感兴趣的话，可以查看一下源代码）。注释：奇怪的是，这个问题至今还没有得到纠正，即使我们在这本书的 9 个版本中已经指出了这一点。很明显，类库的实现者并没有读这本书。不仅如此，这个类还增加了一些新域，其中大约一半也不是私有的。这真的会成为一个问题吗？答案是：视具体情况而定。在默认情况下，包不是一个封闭的实体。也就是说，任何人都可以向包中添加更多的类。当然，有敌意或低水平的程序员很可能利用包的可见性添加一些具有修改变量功能的代码。例如，在 Java 程序设计语言的早期版本中，只需要将下列这条语句放在类文件的开头，就可以很容易地将其他类混入 java.awt 包中：

然后，把结果类文件放置在类路径某处的 java/awt 子目录下，就可以访问 java.awt 包的内部了。使用这一手段，可以对警告框进行设置（如图 4-9 所示）。

图 4-9 在 applet 窗口中修改警告字符串从 1.2 版开始，JDK 的实现者修改了类加载器，明确地禁止加载用户自定义的、包名以「java.」开始的类！当然，用户自定义的类无法从这种保护中受益。然而，可以通过包密封（package sealing）机制来解决将各种包混杂在一起的问题。如果将一个包密封起来，就不能再向这个包添加类了。在第 9 章中，将介绍制作包含密封包的 JAR 文件的方法。

#### 4.7.6 The Class Path

As you have seen, classes are stored in subdirectories of the file system. The path to the class must match the package name.

Class files can also be stored in a JAR (Java archive) file. A JAR file contains multiple class files and subdirectories in a compressed format, saving space and improving performance. When you use a third-party library in your programs, you will usually be given one or more JAR files to include. You will see in Chapter 11 how to create your own JAR files.

Tip

JAR files use the ZIP format to organize files and subdirectories. You can use any ZIP utility to peek inside JAR files.

To share classes among programs, you need to do the following:

Place your class files inside a directory — for example, /home/user/classdir. Note that this directory is the base directory for the package tree. If you add the class com.horstmann.corejava.Employee, then the Employee.class file must be located in the subdirectory /home/user/classdir/com/horstmann/corejava.

Place any JAR files inside a directory — for example, /home/user/archives.

Set the class path. The class path is the collection of all locations that can contain class files.

In UNIX, the elements on the class path are separated by colons:



/home/user/classdir:.:/home/user/archives/archive.jar

In Windows, they are separated by semicolons:



c:\classdir;.;c:\archives\archive.jar

In both cases, the period denotes the current directory.

This class path contains

The base directory /home/user/classdir or c:\classdir;

The current directory (.); and

The JAR file /home/user/archives/archive.jar or c:\archives\archive.jar.

Starting with Java 6, you can specify a wildcard for a JAR file directory, like this:



/home/user/classdir:.:/home/user/archives/'*'

or



c:\classdir;.;c:\archives\*

In UNIX, the * must be escaped to prevent shell expansion.

All JAR files (but not .class files) in the archives directory are included in this class path.

The Java API is always searched for classes; don't include it explicitly in the class path.

Caution

The javac compiler always looks for files in the current directory, but the java virtual machine launcher only looks into the current directory if the「.」directory is on the class path. If you have no class path set, it's not a problem — the default class path consists of the「.」directory. But if you have set the class path and forgot to include the「.」directory, your programs will compile without error, but they won't run.

The class path lists all directories and archive files that are starting points for locating classes. Let's consider our sample class path:



/home/user/classdir:.:/home/user/archives/archive.jar

Suppose the virtual machine searches for the class file of the com.horstmann.corejava.Employee class. It first looks in the Java API classes. It won't find the class file there, so it turns to the class path. It then looks for the following files:

/home/user/classdir/com/horstmann/corejava/Employee.class

com/horstmann/corejava/Employee.class starting from the current directory

com/horstmann/corejava/Employee.class inside /home/user/archives/archive.jar

The compiler has a harder time locating files than does the virtual machine. If you refer to a class without specifying its package, the compiler first needs to find out the package that contains the class. It consults all import directives as possible sources for the class. For example, suppose the source file contains directives



import java.util.*;

import com.horstmann.corejava.*;

and the source code refers to a class Employee. The compiler then tries to find java.lang.Employee (because the java.lang package is always imported by default), java.util.Employee, com.horstmann.corejava.Employee, and Employee in the current package. It searches for each of these classes in all of the locations of the class path. It is a compile-time error if more than one class is found. (Fully qualified class names must be unique, so the order of the import statements doesn't matter.)

The compiler goes one step further. It looks at the source files to see if the source is newer than the class file. If so, the source file is recompiled automatically. Recall that you can import only public classes from other packages. A source file can only contain one public class, and the names of the file and the public class must match. Therefore, the compiler can easily locate source files for public classes. However, you can import nonpublic classes from the current package. These classes may be defined in source files with different names. If you import a class from the current package, the compiler searches all source files of the current package to see which one defines the class.

#### 4.7.7 Setting the Class Path

It is best to specify the class path with the option -classpath (or -cp or, as of Java 9, --class-path):



java -classpath /home/user/classdir:.:/home/user/archives/archive.jar MyProg

or



java -classpath c:\classdir;.;c:\archives\archive.jar MyProg

The entire command must be typed onto a single line. It is a good idea to place such a long command line into a shell script or a batch file.

Using the -classpath option is the preferred approach for setting the class path. An alternate approach is the CLASSPATH environment variable. The details depend on your shell. With the Bourne Again shell (bash), use the command



export CLASSPATH=/home/user/classdir:.:/home/user/archives/archive.jar

With the Windows shell, use



set CLASSPATH=c:\classdir;.;c:\archives\archive.jar

The class path is set until the shell exits.

Caution

Some people recommend to set the CLASSPATH environment variable permanently. This is generally a bad idea. People forget the global setting, and are surprised when their classes are not loaded properly. A particularly reprehensible example is Apple's QuickTime installer in Windows. For several years, it globally set CLASSPATH to point to a JAR file it needed, but did not include the current directory in the classpath. As a result, countless Java programmers were driven to distraction when their programs compiled but failed to run.

Caution

In the past, some people recommended to bypass the class path altogether, by dropping all JAR files into the jre/lib/ext directory. That mechanism is obsolete with Java 9, but it was always bad advice. It was easy to get confused when long-forgotten classes were loaded from the extension directory.

Note

As of Java 9, classes can also be loaded from the module path. We discuss modules and the module path in Chapter 9 of Volume II.

4.8 类路径

在前面已经看到，类存储在文件系统的子目录中。类的路径必须与包名匹配。另外，类文件也可以存储在 JAR（Java 归档）文件中。在一个 JAR 文件中，可以包含多个压缩形式的类文件和子目录，这样既可以节省又可以改善性能。在程序中用到第三方（third-party）的库文件时，通常会给出一个或多个需要包含的 JAR 文件。JDK 也提供了许多的 JAR 文件，例如，在 jre/lib/rt.jar 中包含数千个类库文件。有关创建 JAR 文件的详细内容将在第 9 章中讨论。提示：JAR 文件使用 ZIP 格式组织文件和子目录。可以使用所有 ZIP 实用程序查看内部的 rt.jar 以及其他的 JAR 文件。为了使类能够被多个程序共享，需要做到下面几点：1）把类放到一个目录中，例如 /home/user/classdir。需要注意，这个目录是包树状结构的基目录。如果希望将 com.horstmann.corejava.Employee 类添加到其中，这个 Employee.class 类文件就必须位于子目录 /home/user/classdir/com/horstmann/corejava 中。

2）将 JAR 文件放在一个目录中，例如：/home/user/archives。3）设置类路径（class path）。类路径是所有包含类文件的路径的集合。在 UNIX 环境中，类路径中的不同项目之间采用冒号（：）分隔：而在 Windows 环境中，则以分号（；）分隔：在上述两种情况中，句点（.）表示当前目录。类路径包括：·基目录 /home/user/classdir 或 c：\classes；·当前目录（.）；·JAR 文件 /home/user/archives/archive.jar 或 c：\archives\archive.jar。从 Java SE 6 开始，可以在 JAR 文件目录中指定通配符，如下：

或者但在 UNIX 中，禁止使用 * 以防止 shell 命令进一步扩展。在 archives 目录中的所有 JAR 文件（但不包括.class 文件）都包含在类路径中。由于运行时库文件（rt.jar 和在 jre/lib 与 jre/lib/ext 目录下的一些其他的 JAR 文件）会被自动地搜索，所以不必将它们显式地列在类路径中。警告：javac 编译器总是在当前的目录中查找文件，但 Java 虚拟机仅在类路径中有「.」目录的时候才查看当前目录。如果没有设置类路径，那也并不会产生什么问题，默认的类路径包含「.」目录。然而如果设置了类路径却忘记了包含「.」目录，则程序仍然可以通过编译，但不能运行。类路径所列出的目录和归档文件是搜寻类的起始点。下面看一个类路径示例：假定虚拟机要搜寻 com.horstmann.corejava.Employee 类文件。它首先要查看存储在 jre/lib 和 jre/lib/ext 目录下的归档文件中所存放的系统类文件。显然，在那里找不到相应的类文件，然后再查看类路径。然后查找以下文件：

·/home/user/classdir/com/horstmann/corejava/Employee.class·com/horstmann/corejava/Employee.class 从当前目录开始·com/horstmann/corejava/Employee.classinside/home/user/archives/archive.jar 编译器定位文件要比虚拟机复杂得多。如果引用了一个类，而没有指出这个类所在的包，那么编译器将首先查找包含这个类的包，并询查所有的 import 指令，确定其中是否包含了被引用的类。例如，假定源文件包含指令：并且源代码引用了 Employee 类。编译器将试图查找 java.lang.Employee（因为 java.lang 包被默认导入）、java.util.Employee、com.horstmann.corejava.Employee 和当前包中的 Employee。对这个类路径的所有位置中所列出的每一个类进行逐一查看。如果找到了一个以上的类，就会产生编译错误（因为类必须是唯一的，而 import 语句的次序却无关紧要）。

编译器的任务不止这些，它还要查看源文件（Source files）是否比类文件新。如果是这样的话，那么源文件就会被自动地重新编译。在前面已经知道，仅可以导入其他包中的公有类。一个源文件只能包含一个公有类，并且文件名必须与公有类匹配。因此，编译器很容易定位公有类所在的源文件。当然，也可以从当前包中导入非公有类。这些类有可能定义在与类名不同的源文件中。如果从当前包中导入一个类，编译器就要搜索当前包中的所有源文件，以便确定哪个源文件定义了这个类。4.8.1 设置类路径最好采用 - classpath（或 - cp）选项指定类路径：或者整个指令应该书写在一行中。将这样一个长的命令行放在一个 shell 脚本或一个批处理文件中是一个不错的主意。利用 - classpath 选项设置类路径是首选的方法，也可以通过设置 CLASSPATH 环境变量完成这个操作。其详细情况依赖于所使用的 shell。在 Bourne Againshell（bash）中，命令格式如下：

在 Windows shell，命令格式如下：直到退出 shell 为止，类路径设置均有效。警告：有人建议将 CLASSPATH 环境变量设置为永久不变的值。总的来说这是一个很糟糕的主意。人们有可能会忘记全局设置，因此，当使用的类没有正确地加载进来时，会感到很奇怪。一个应该受到谴责的示例是 Windows 中 Apple 的 QuickTime 安装程序。它进行了全局设置，CLASSPATH 指向一个所需要的 JAR 文件，但并没有在类路径上包含当前路径。因此，当程序编译后却不能运行时，众多的 Java 程序员花费了很多精力去解决这个问题。警告：有人建议绕开类路径，将所有的文件放在 jre/lib/ext 路径。这是一个极坏的主意，其原因主要有两个：当手工地加载其他的类文件时，如果将它们存放在扩展路径上，则不能正常地工作（有关类加载器的详细信息，请参看卷 Ⅱ 第 9 章）。此外，程序员经常会忘记 3 个月前所存放文件的位置。当类加载器忽略了曾经仔细设计的类路径时，程序员会毫无头绪地在头文件中查找。事实上，加载的是扩展路径上已长时间遗忘的类。

### 4.8 JAR Files

When you package your application, you want to give your users a single file, not a directory structure filled with class files. Java Archive (JAR) files were designed for this purpose. A JAR file can contain both class files and other file types such as image and sound files. Moreover, JAR files are compressed, using the familiar ZIP compression format.

#### 4.8.1 Creating JAR files

Use the jar tool to make JAR files. (In the default JDK installation, it's in the jdk/bin directory.) The most common command to make a new JAR file uses the following syntax:



jar cvf jarFileName file1 file2 . . .

For example:



jar cvf CalculatorClasses.jar *.class icon.gif

In general, the jar command has the following format:



jar options file1 file2 . . .

Table 4.2 lists all the options for the jar program. They are similar to the options of the UNIX tar command.

Table 4.2 jar Program Options

Option

Description

c

Creates a new or empty archive and adds files to it. If any of the specified file names are directories, the jar program processes them recursively.

C

Temporarily changes the directory. For example,

jar cvf jarFileName.jar -C classes *.class

changes to the classes subdirectory to add class files.

e

Creates an entry point in the manifest (see Section 4.8.3).

f

Specifies the JAR file name as the second command-line argument. If this parameter is missing, jar will write the result to standard output (when creating a JAR file) or read it from standard input (when extracting or tabulating a JAR file).

i

Creates an index file (for speeding up lookups in a large archive).

m

Adds a manifest to the JAR file. A manifest is a description of the archive contents and origin. Every archive has a default manifest, but you can supply your own if you want to authenticate the contents of the archive.

M

Does not create a manifest file for the entries.

t

Displays the table of contents.

u

Updates an existing JAR file.

v

Generates verbose output.

x

Extracts files. If you supply one or more file names, only those files are extracted. Otherwise, all files are extracted.

0

Stores without ZIP compression.

You can package application programs and code libraries into JAR files. For example, if you want to send mail in a Java program, you use a library that is packaged in a file javax.mail.jar.

#### 4.8.2 The Manifest

In addition to class files, images, and other resources, each JAR file contains a manifest file that describes special features of the archive.

The manifest file is called MANIFEST.MF and is located in a special META-INF sub-directory of the JAR file. The minimum legal manifest is quite boring — just

Manifest-Version: 1.0

Complex manifests can have many more entries. The manifest entries are grouped into sections. The first section in the manifest is called the main section. It applies to the whole JAR file. Subsequent entries can specify properties of named entities such as individual files, packages, or URLs. Those entries must begin with a Name entry. Sections are separated by blank lines. For example:



Manifest-Version: 1.0

lines describing this archive

Name: Woozle.class

lines describing this file

Name: com/mycompany/mypkg/

lines describing this package

To edit the manifest, place the lines that you want to add to the manifest into a text file. Then run



jar cfm jarFileName manifestFileName . . .

For example, to make a new JAR file with a manifest, run



jar cfm MyArchive.jar manifest.mf com/mycompany/mypkg/*.class

To update the manifest of an existing JAR file, place the additions into a text file and use a command such as



jar ufm MyArchive.jar manifest-additions.mf

Note

See https://docs.oracle.com/javase/10/docs/specs/jar/jar.html for more information on the JAR and manifest file formats.

#### 4.8.3 Executable JAR Files

You can use the e option of the jar command to specify the entry point of your program — the class that you would normally specify when invoking the java program launcher:



jar cvfe MyProgram.jar com.mycompany.mypkg.MainAppClass files to add

Alternatively, you can specify the main class of your program in the manifest, including a statement of the form



Main-Class: com.mycompany.mypkg.MainAppClass

Do not add a .class extension to the main class name.

Caution

The last line in the manifest must end with a newline character. Otherwise, the manifest will not be read correctly. It is a common error to produce a text file containing just the Main-Class line without a line terminator.

With either method, users can simply start the program as

java -jar MyProgram.jar

Depending on the operating system configuration, users may even be able to launch the application by double-clicking the JAR file icon. Here are behaviors for various operating systems:

On Windows, the Java runtime installer creates a file association for the「.jar」extension that launches the file with the javaw -jar command. (Unlike the java command, the javaw command doesn't open a shell window.)

On Mac OS X, the operating system recognizes the「.jar」file extension and executes the Java program when you double-click a JAR file.

However, a Java program in a JAR file does not have the same feel as a native application. On Windows, you can use third-party wrapper utilities that turn JAR files into Windows executables. A wrapper is a Windows program with the familiar .exe extension that locates and launches the Java virtual machine (JVM) or tells the user what to do when no JVM is found. There are a number of commercial and open source products, such as Launch4J (http://launch4j.sourceforge.net) and IzPack (http://izpack.org).

#### 4.8.4 Multi-Release JAR Files

With the introduction of modules and strong encapsulation of packages, some previously accessible internal APIs are no longer available. For example, JavaFX 8 had an internal class com.sun.javafx.css.CssParser. If you used it to parse a style sheet, then you will find that your program no longer compiles. The remedy is simple — switch to javafx.css.CssParser, which is available in Java 9. But now you have a problem. You need to distribute different applications for Java 8 and Java 9 users, or you need to play tricks with class loading and reflection.

To solve problems such as this one, Java 9 introduces multi-release JARs that can contain class files for different Java releases.

For backwards compatibility, the additional class files are placed in the META-INF/versions directory:



Application.class

BuildingBlocks.class

Util.class

META-INF

├─ MANIFEST.MF (with line Multi-Release: true)

├─ versions

├─ 9

│ ├─ Application.class

│ └─ BuildingBlocks.class

└─ 10

└─ BuildingBlocks.class

Suppose the Application class makes use of the CssParser class. Then the legacy Application.class file can be compiled to use com.sun.javafx.css.CssParser, while the Java 9 version uses javafx.css.CssParser.

Java 8 knows nothing about the META-INF/versions directory and will simply load the legacy classes. When the JAR file is read by Java 9, the new version is used instead.

To add versioned class files, use the --release flag:



jar uf MyProgram.jar --release 9 Application.class

To build a multi-release JAR file from scratch, use the -C option and switch to a different class file directory for each version:



jar cf MyProgram.jar -C bin/8 . --release 9 -C bin/9 Application.class

When compiling for different releases, use the --release flag and the -d flag to specify the output directory:

javac -d bin/8 --release 8 . . .

As of Java 9, the -d option creates the directory if it doesn't exist.

The --release flag is also new with Java 9. In older versions, you needed to use the -source, -target, and -bootclasspath flags. The JDK now ships with symbol files for two prior versions of the API. In Java 9, you can compile with --release set to 9, 8, or 7.

Multi-release JARs are not intended for different versions of a program or library. The public API of all classes should be the same for both releases. The sole purpose of multi-release JARs is to enable a particular version of your program or library to work with multiple JDK releases. If you add functionality or change an API, you should provide a new version of the JAR instead.

Note

Tools such as javap are not retrofitted to handle multi-release JAR files. If you call



javap -classpath MyProgram.jar Application.class

you get the base version of the class (which, after all, is supposed to have the same public API as the newer version). If you must look at the newer version, call



javap -classpath MyProgram.jar\!/META-INF/versions/9/Application.class

#### 4.8.5 A Note about Command-Line Options

The options of commands in the Java Development Kit have traditionally used single dashes followed by multiletter option names, such as



java -jar . . .

javac -Xlint:unchecked -classpath . . .

The exception was the jar command, which followed the classic option format of the tar command without dashes:

jar cvf . . .

Starting with Java 9, the Java tools are moving towards a more common option format where multiletter option names are preceded by double dashes, with single-letter shortcuts for common options. For example, the Linux ls command can be called with a「human-readable」option as

ls --human-readable

or

ls -h

As of Java 9, you can use --version instead of -version and --class-path instead of -classpath. As you will see in Chapter 9 of Volume II, the --module-path option has a shortcut -p.

You can find the details in the JEP 293 enhancement request at http://openjdk.java.net/jeps/293. As part of this cleanup, the authors also propose to standardize option arguments. Arguments of options with -- and multiple letters are separated by whitespace or an = sign:



javac --class-path /home/user/classdir . . .

or



javac --class-path=/home/user/classdir . . .

Arguments of single-letter options can be separated by whitespace or directly follow the option:

javac -p moduledir . . .

or

javac -pmoduledir . . .

Caution

The latter doesn't currently work, and it also seems like a bad idea in general. Why invite conflicts with legacy options if the module directory happens to be arameters or rocessor?

Single-letter options without arguments can be grouped together:



jar -cvf MyProgram.jar -e mypackage.MyProgram */*.class

Caution

That doesn't currently work, and it is bound to lead to confusion. Suppose javac gains a -c option. Does javac -cp mean javac -c -p, or does the legacy -cp take precedence?

This has created a muddle that will hopefully get cleaned up over time. As much as we'd like to move away from the archaic jar options, it seems best to wait until the dust has settled. But if you want to be thoroughly modern, you can safely use the long options of the jar command:



jar --create --verbose --file jarFileName file1 file2 . . .

Single-letter options also work if you don't group them:



jar -c -v -f jarFileName file1 file2 . . .

### 4.9 Documentation Comments

The JDK contains a very useful tool, called javadoc, that generates HTML documentation from your source files. In fact, the online API documentation that we described in Chapter 3 is simply the result of running javadoc on the source code of the standard Java library.

If you add comments that start with the special delimiter /** to your source code, you too can easily produce professional-looking documentation. This is a very nice approach because it lets you keep your code and documentation in one place. If you put your documentation into a separate file, then, as you probably know, the code and comments tend to diverge over time. When documentation comments are in the same file as the source code, it is an easy matter to update both and run javadoc again.

4.9 文档注释

JDK 包含一个很有用的工具，叫做 javadoc，它可以由源文件生成一个 HTML 文档。事实上，在第 3 章讲述的联机 API 文档就是通过对标准 Java 类库的源代码运行 javadoc 生成的。如果在源代码中添加以专用的定界符 /** 开始的注释，那么可以很容易地生成一个看上去具有专业水准的文档。这是一种很好的方式，因为这种方式可以将代码与注释保存在一个地方。如果将文档存入一个独立的文件中，就有可能会随着时间的推移，出现代码和注释不一致的问题。然而，由于文档注释与源代码在同一个文件中，在修改源代码的同时，重新运行 javadoc 就可以轻而易举地保持两者的一致性。

#### 4.9.1 Comment Insertion

The javadoc utility extracts information for the following items:

Modules

Packages

Public classes and interfaces

Public and protected fields

Public and protected constructors and methods

Protected features are introduced in Chapter 5, interfaces in Chapter 6, and modules in Chapter 9 of Volume II.

You can (and should) supply a comment for each of these features. Each comment is placed immediately above the feature it describes. A comment starts with a /** and ends with a */.

Each /** . . . */ documentation comment contains free-form text followed by tags. A tag starts with an @, such as @since or @param.

The first sentence of the free-form text should be a summary statement. The javadoc utility automatically generates summary pages that extract these sentences.

In the free-form text, you can use HTML modifiers such as <em>. . .</em> for emphasis, <strong>. . .</strong> for strong emphasis, <ul>/<li> for bulleted lists, and <img . . ./> to include an image. To type monospaced code, use {@code . . . } instead of <code>. . .</code> — then you don't have to worry about escaping < characters inside the code.

Note

If your comments contain links to other files such as images (for example, diagrams or images of user interface components), place those files into a subdirectory, named doc-files, of the directory containing the source file. The javadoc utility will copy the doc-files directories and their contents from the source directory to the documentation directory. You need to use the doc-files directory in your link, for example <img src="doc-files/uml.png" alt="UML diagram"/>.

4.9.1 注释的插入

javadoc 实用程序（utility）从下面几个特性中抽取信息：·包·公有类与接口·公有的和受保护的构造器及方法·公有的和受保护的域在第 5 章中将介绍受保护特性，在第 6 章将介绍接口。应该为上面几部分编写注释。注释应该放置在所描述特性的前面。注释以 `/**` 开始，并以 */ 结束。每个 /**...*/ 文档注释在标记之后紧跟着自由格式文本（free-form text）。标记由 @开始，如 @author 或 @param。自由格式文本的第一句应该是一个概要性的句子。javadoc 实用程序自动地将这些句子抽取出来形成概要页。

在自由格式文本中，可以使用 HTML 修饰符，例如，用于强调的 <em>...</em>、用于着重强调的 <strong>...</strong> 以及包含图像的 <img...> 等。不过，一定不要使用 <h1> 或 <hr>，因为它们会与文档的格式产生冲突。若要键入等宽代码，需使用 {@code...} 而不是 <code>...</code> ——  这样一来，就不用操心对代码中的 <字符转义了。注释：如果文档中有到其他文件的链接，例如，图像文件（用户界面的组件的图表或图像等），就应该将这些文件放到子目录 doc-files 中。javadoc 实用程序将从源目录拷贝这些目录及其中的文件到文档目录中。在链接中需要使用 doc-files 目录，例如：<img src=「doc-files/uml.png」alt=「UMLdiagram」>。

#### 4.9.2 Class Comments

The class comment must be placed after any import statements, directly before the class definition.

Here is an example of a class comment:



/**

* A {@code Card} object represents a playing card, such

* as "Queen of Hearts". A card has a suit (Diamond, Heart,

* Spade or Club) and a value (1 = Ace, 2 . . . 10, 11 = Jack,

* 12 = Queen, 13 = King)

*/

public class Card

{

. . .

}

Note

There is no need to add an * in front of every line. For example, the following comment is equally valid:



/**

A <code>Card</code> object represents a playing card, such

as "Queen of Hearts". A card has a suit (Diamond, Heart,

Spade or Club) and a value (1 = Ace, 2 . . . 10, 11 = Jack,

12 = Queen, 13 = King).

*/

However, most IDEs supply the asterisks automatically and rearrange them when the line breaks change.

4.9.2 类注释类注释必须放在 import 语句之后，类定义之前。下面是一个类注释的例子：

注释：没有必要在每一行的开始用星号 *，例如，以下注释同样是合法的：然而，大部分 IDE 提供了自动添加星号 *，并且当注释行改变时，自动重新排列这些星号的功能。

#### 4.9.3 Method Comments

Each method comment must immediately precede the method that it describes. In addition to the general-purpose tags, you can use the following tags:

@param variable description

This tag adds an entry to the「parameters」section of the current method. The description can span multiple lines and can use HTML tags. All @param tags for one method must be kept together.

@return description

This tag adds a「returns」section to the current method. The description can span multiple lines and can use HTML tags.

@throws class description

This tag adds a note that this method may throw an exception. Exceptions are the topic of Chapter 7.

Here is an example of a method comment:



/**

* Raises the salary of an employee.

* @param byPercent the percentage by which to raise the salary (e.g., 10 means 10%)

* @return the amount of the raise

*/

public double raiseSalary(double byPercent)

{

double raise = salary * byPercent / 100;

salary += raise;

return raise;

}

4.9.3 方法注释每一个方法注释必须放在所描述的方法之前。除了通用标记之外，还可以使用下面的标记：·@param 变量描述这个标记将对当前方法的「param」（参数）部分添加一个条目。这个描述可以占据多行，并可以使用 HTML 标记。一个方法的所有 @param 标记必须放在一起。·@return 描述这个标记将对当前方法添加「return」（返回）部分。这个描述可以跨越多行，并可以使用 HTML 标记。

·@throws 类描述这个标记将添加一个注释，用于表示这个方法有可能抛出异常。有关异常的详细内容将在第 10 章中讨论。下面是一个方法注释的示例：

#### 4.9.4 Field Comments

You only need to document public fields — generally that means static constants. For example:



/**

* The "Hearts" card suit

*/

public static final int HEARTS = 1;

4.9.4 域注释

只需要对公有域（通常指的是静态常量）建立文档。例如，

#### 4.9.5 General Comments

The tag @since text makes a「since」entry. The text can be any description of the version that introduced this feature. For example, @since 1.7.1.

The following tags can be used in class documentation comments:

@author name

This tag makes an「author」entry. You can have multiple @author tags, one for each author. Don't feel compelled to use this tag — your version control system does a more thorough job tracking authorship.

@version text

This tag makes a「version」entry. The text can be any description of the current version.

You can use hyperlinks to other relevant parts of the javadoc documentation, or to external documents, with the @see and @link tags.

The tag @see reference adds a hyperlink in the「see also」section. It can be used with both classes and methods. Here, reference can be one of the following:



package.class#feature label

<a href=". . .">label</a>

"text"

The first case is the most useful. You supply the name of a class, method, or variable, and javadoc inserts a hyperlink to the documentation. For example,



@see com.horstmann.corejava.Employee#raiseSalary(double)

makes a link to the raiseSalary(double) method in the com.horstmann.corejava.Employee class. You can omit the name of the package, or both the package and class names. Then, the feature will be located in the current package or class.

Note that you must use a #, not a period, to separate the class from the method or variable name. The Java compiler itself is highly skilled in determining the various meanings of the period character as separator between packages, subpackages, classes, inner classes, and methods and variables. But the javadoc utility isn't quite as clever, so you have to help it along.

If the @see tag is followed by a < character, then you need to specify a hyperlink. You can link to any URL you like. For example:



@see <a href="www.horstmann.com/corejava.html">The Core Java home page</a>

In each of these cases, you can specify an optional label that will appear as the link anchor. If you omit the label, the user will see the target code name or URL as the anchor.

If the @see tag is followed by a " character, then the text is displayed in the「see also」section. For example:

@see "Core Java 2 volume 2"

You can add multiple @see tags for one feature, but you must keep them all together.

If you like, you can place hyperlinks to other classes or methods anywhere in any of your documentation comments. Insert a special tag of the form

{@link package.class#feature label}

anywhere in a comment. The feature description follows the same rules as for the @see tag.

Finally, as of Java 9, you can use the {@index entry} tag to add an entry to the search box.

4.9.5 通用注释下面的标记可以用在类文档的注释中。·@author 姓名这个标记将产生一个「author」（作者）条目。可以使用多个 @author 标记，每个 @author 标记对应一个作者。·@version 文本

这个标记将产生一个「version」（版本）条目。这里的文本可以是对当前版本的任何描述。下面的标记可以用于所有的文档注释中。·@since 文本这个标记将产生一个「since」（始于）条目。这里的 text 可以是对引入特性的版本描述。例如，@since version 1.7.1。·@deprecated 文本这个标记将对类、方法或变量添加一个不再使用的注释。文本中给出了取代的建议。例如，@deprecated Use<code>setVisible（true）</code>instead 通过 @see 和 @link 标记，可以使用超级链接，链接到 javadoc 文档的相关部分或外部文档。·@see 引用这个标记将在「see also」部分增加一个超级链接。它可以用于类中，也可以用于方法中。这里的引用可以选择下列情形之一：

第一种情况是最常见的。只要提供类、方法或变量的名字，javadoc 就在文档中插入一个超链接。例如，建立一个链接到 com.horstmann.corejava.Employee 类的 raiseSalary（double）方法的超链接。可以省略包名，甚至把包名和类名都省去，此时，链接将定位于当前包或当前类。需要注意，一定要使用井号（#），而不要使用句号（.）分隔类名与方法名，或类名与变量名。Java 编译器本身可以熟练地断定句点在分隔包、子包、类、内部类与方法和变量时的不同含义。但是 javadoc 实用程序就没有这么聪明了，因此必须对它提供帮助。如果 @see 标记后面有一个 < 字符，就需要指定一个超链接。可以超链接到任何 URL。例如：

可以为一个特性添加多个 @see 标记，但必须将它们放在一起。·如果愿意的话，还可以在注释中的任何位置放置指向其他类或方法的超级链接，以及插入一个专用的标记，例如，这里的特性描述规则与 @see 标记规则一样。

#### 4.9.6 Package Comments

Place the class, method, and variable comments directly into the Java source files, delimited by /** . . . */ documentation comments. However, to generate package comments, you need to add a separate file in each package directory. You have two choices:

Supply a Java file named package-info.java. The file must contain an initial Javadoc comment, delimited with /** and */, followed by a package statement. It should contain no further code or comments.

Supply an HTML file named package.html. All text between the tags <body>. . .</body> is extracted.

4.9.6 包与概述注释

可以直接将类、方法和变量的注释放置在 Java 源文件中，只要用 /**...*/ 文档注释界定就可以了。但是，要想产生包注释，就需要在每一个包目录中添加一个单独的文件。可以有如下两个选择：1）提供一个以 package.html 命名的 HTML 文件。在标记 <body>...</body> 之间的所有文本都会被抽取出来。

2）提供一个以 package-info.java 命名的 Java 文件。这个文件必须包含一个初始的以 /** 和 */ 界定的 Javadoc 注释，跟随在一个包语句之后。它不应该包含更多的代码或注释。还可以为所有的源文件提供一个概述性的注释。这个注释将被放置在一个名为 overview.html 的文件中，这个文件位于包含所有源文件的父目录中。标记 <body>...</body> 之间的所有文本将被抽取出来。当用户从导航栏中选择「Overview」时，就会显示出这些注释内容。


#### 4.9.7 Comment Extraction

Here, docDirectory is the name of the directory where you want the HTML files to go. Follow these steps:

Change to the directory that contains the source files you want to document. If you have nested packages to document, such as com.horstmann.corejava, you must be working in the directory that contains the subdirectory com. (This is the directory that contains the overview.html file, if you supplied one.)

Run the command



javadoc -d docDirectory nameOfPackage

for a single package. Or, run



javadoc -d docDirectory nameOfPackage1 nameOfPackage2. . .

to document multiple packages. If your files are in the unnamed package, run instead



javadoc -d docDirectory *.java

If you omit the -d docDirectory option, the HTML files are extracted to the current directory. That can get messy, and we don't recommend it.

The javadoc program can be fine-tuned by numerous command-line options. For example, you can use the -author and -version options to include the @author and @version tags in the documentation. (By default, they are omitted.) Another useful option is -link, to include hyperlinks to standard classes. For example, if you use the command



javadoc -link http://docs.oracle.com/javase/9/docs/api *.java

all standard library classes are automatically linked to the documentation on the Oracle web site.

If you use the -linksource option, each source file is converted to HTML (without color coding, but with line numbers), and each class and method name turns into a hyperlink to the source.

You can also supply an overview comment for all source files. Place it in a file such as overview.html and run the javadoc tool with the command line option -overview filename. All text between the tags <body>. . .</body> is extracted. The content is displayed when the user selects「Overview」from the navigation bar.

For additional options, we refer you to the online documentation of the javadoc utility at https://docs.oracle.com/javase/9/javadoc/javadoc.htm.

4.9.7 注释的抽取

这里，假设 HTML 文件将被存放在目录 docDirectory 下。执行以下步骤：1）切换到包含想要生成文档的源文件目录。如果有嵌套的包要生成文档，例如 com.horstmann.corejava，就必须切换到包含子目录 com 的目录（如果存在 overview.html 文件的话，这也是它的所在目录）。2）如果是一个包，应该运行命令：或对于多个包生成文档，运行：如果文件在默认包中，就应该运行：

如果省略了 - d docDirectory 选项，那 HTML 文件就会被提取到当前目录下。这样有可能会带来混乱，因此不提倡这种做法。可以使用多种形式的命令行选项对 javadoc 程序进行调整。例如，可以使用 - author 和 - version 选项在文档中包含 @author 和 @version 标记（默认情况下，这些标记会被省略）。另一个很有用的选项是 - link，用来为标准类添加超链接。例如，如果使用命令那么，所有的标准类库类都会自动地链接到 Oracle 网站的文档。如果使用 - linksource 选项，则每个源文件被转换为 HTML（不对代码着色，但包含行编号），并且每个类和方法名将转变为指向源代码的超链接。有关其他的选项，请查阅 javadoc 实用程序的联机文档，http://docs.oracle.com/javase/8/docs/guides/javadoc。

注释：如果需要进一步的定制，例如，生成非 HTML 格式的文档，可以提供自定义的 doclet，以便生成想要的任何输出形式。显然，这是一种特殊的需求，有关细节内容请查阅 http://docs.oracle.com/javase/8/docs/guides/javadoc/doclet/overview.html 的联机文档。

#### 4.10 Class Design Hints

Without trying to be comprehensive or tedious, we want to end this chapter with some hints that will make your classes more acceptable in well-mannered OOP circles.

Always keep data private.

This is first and foremost; doing anything else violates encapsulation. You may need to write an accessor or mutator method occasionally, but you are still better off keeping the instance fields private. Bitter experience shows that the data representation may change, but how this data are used will change much less frequently. When data are kept private, changes in their representation will not affect the users of the class, and bugs are easier to detect.

Always initialize data.

Java won't initialize local variables for you, but it will initialize instance fields of objects. Don't rely on the defaults, but initialize all variables explicitly, either by supplying a default or by setting defaults in all constructors.

Don't use too many basic types in a class.

The idea is to replace multiple related uses of basic types with other classes. This keeps your classes easier to understand and to change. For example, replace the following instance fields in a Customer class:



private String street;

private String city;

private String state;

private int zip;

with a new class called Address. This way, you can easily cope with changes to addresses, such as the need to deal with international addresses.

Not all fields need individual field accessors and mutators.

You may need to get and set an employee's salary. You certainly won't need to change the hiring date once the object is constructed. And, quite often, objects have instance fields that you don't want others to get or set, such as an array of state abbreviations in an Address class.

Break up classes that have too many responsibilities.

This hint is, of course, vague:「too many」is obviously in the eye of the beholder. However, if there is an obvious way to break one complicated class into two classes that are conceptually simpler, seize the opportunity. (On the other hand, don't go overboard; ten classes, each with only one method, are usually an overkill.)

Here is an example of a bad design:



public class CardDeck // bad design

{

private int[] value;

private int[] suit;

public CardDeck() { . . . }

public void shuffle() { . . . }

public int getTopValue() { . . . }

public int getTopSuit() { . . . }

public void draw() { . . . }

}

This class really implements two separate concepts: a deck of cards, with its shuffle and draw methods, and a card, with the methods to inspect its value and suit. It makes sense to introduce a Card class that represents an individual card. Now you have two classes, each with its own responsibilities:



public class CardDeck

{

private Card[] cards;

public CardDeck() { . . . }

public void shuffle() { . . . }

public Card getTop() { . . . }

public void draw() { . . . }

}

public class Card

{

private int value;

private int suit;

public Card(int aValue, int aSuit) { . . . }

public int getValue() { . . . }

public int getSuit() { . . . }

}

Make the names of your classes and methods reflect their responsibilities.

Just as variables should have meaningful names that reflect what they represent, so should classes. (The standard library certainly contains some dubious examples, such as the Date class that describes time.)

A good convention is that a class name should be a noun (Order), or a noun preceded by an adjective (RushOrder) or a gerund (an「-ing」word, as in BillingAddress). As for methods, follow the standard convention that accessor methods begin with a lowercase get (getSalary) and mutator methods use a lowercase set (setSalary).

Prefer immutable classes.

The LocalDate class, and other classes from the java.time package, are immutable — no method can modify the state of an object. Instead of mutating objects, methods such as plusDays return new objects with the modified state.

The problem with mutation is that it can happen concurrently when multiple threads try to update an object at the same time. The results are unpredictable. When classes are immutable, it is safe to share their objects among multiple threads.

Therefore, it is a good idea to make classes immutable when you can. This is particularly easy with classes that represent values, such as a string or a point in time. Computations can simply yield new values instead of updating existing ones.

Of course, not all classes should be immutable. It would be strange to have the raiseSalary method return a new Employee object when an employee gets a raise.

In this chapter, we covered the fundamentals of objects and classes that make Java an「object-based」language. In order to be truly object-oriented, a programming language must also support inheritance and polymorphism. The Java support for these features is the topic of the next chapter.

4.10 类设计技巧

我们不会面面俱到，也不希望过于沉闷，所以这一章结束之前，简单地介绍几点技巧。应用这些技巧可以使得设计出来的类更具有 OOP 的专业水准。1. 一定要保证数据私有这是最重要的；绝对不要破坏封装性。有时候，需要编写一个访问器方法或更改器方法，但是最好还是保持实例域的私有性。很多惨痛的经验告诉我们，数据的表示形式很可能会改变，但它们的使用方式却不会经常发生变化。当数据保持私有时，它们的表示形式的变化不会对类的使用者产生影响，即使出现 bug 也易于检测。2. 一定要对数据初始化 Java 不对局部变量进行初始化，但是会对对象的实例域进行初始化。最好不要依赖于系统的默认值，而是应该显式地初始化所有的数据，具体的初始化方式可以是提供默认值，也可以是在所有构造器中设置默认值。3. 不要在类中使用过多的基本类型就是说，用其他的类代替多个相关的基本类型的使用。这样会使类更加易于理解且易于修改。例如，用一个称为 Address 的新的类替换一个 Customer 类中以下的实例域：

这样，可以很容易处理地址的变化，例如，需要增加对国际地址的处理。4. 不是所有的域都需要独立的域访问器和域更改器或许，需要获得或设置雇员的薪金。而一旦构造了雇员对象，就应该禁止更改雇用日期，并且在对象中，常常包含一些不希望别人获得或设置的实例域，例如，在 Address 类中，存放州缩写的数组。5. 将职责过多的类进行分解这样说似乎有点含糊不清，究竟多少算是「过多」？每个人的看法不同。但是，如果明显地可以将一个复杂的类分解成两个更为简单的类，就应该将其分解（但另一方面，也不要走极端。设计 10 个类，每个类只有一个方法，显然有些矫枉过正了）。下面是一个反面的设计示例。

实际上，这个类实现了两个独立的概念：一副牌（含有 shuffle 方法和 draw 方法）和一张牌（含有查看面值和花色的方法）。另外，引入一个表示单张牌的 Card 类。现在有两个类，每个类完成自己的职责：6. 类名和方法名要能够体现它们的职责与变量应该有一个能够反映其含义的名字一样，类也应该如此（在标准类库中，也存在着一些含义不明确的例子，如：Date 类实际上是一个用于描述时间的类）。命名类名的良好习惯是采用一个名词（Order）、前面有形容词修饰的名词（RushOrder）或动名词（有「-ing」后缀）修饰名词（例如，BillingAddress）。对于方法来说，习惯是访问器方法用小写 get 开头（getSalary），更改器方法用小写的 set 开头（setSalary）。

7 优先使用不可变的类

LocalDate 类以及 java.time 包中的其他类是不可变的 —— 没有方法能修改对象的状态。类似 plusDays 的方法并不是更改对象，而是返回状态已修改的新对象。更改对象的问题在于，如果多个线程试图同时更新一个对象，就会发生并发更改。其结果是不可预料的。如果类是不可变的，就可以安全地在多个线程间共享其对象。因此，要尽可能让类是不可变的，这是一个很好的想法。对于表示值的类，如一个字符串或一个时间点，这尤其容易。计算会生成新值，而不是更新原来的值。当然，并不是所有类都应当是不可变的。如果员工加薪时让 raiseSalary 方法返回一个新的 Employee 对象，这会很奇怪。本章介绍了 Java 这种面向对象语言的有关对象和类的基础知识。为了真正做到面向对象，程序设计语言还必须支持继承和多态。Java 提供了对这些特性的支持，具体内容将在下一章中介绍。

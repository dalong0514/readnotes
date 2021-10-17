## 0401. Objects and Classes

In this chapter

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

Show you how you can create objects that belong to classes from the standard Java library; and

Show you how to write your own classes.

If you do not have a background in object-oriented programming, you will want to read this chapter carefully. Object-oriented programming requires a different way of thinking than procedural languages. The transition is not always easy, but you do need some familiarity with object concepts to go further with Java.

For experienced C++ programmers, this chapter, like the previous chapter, presents familiar information; however, there are enough differences between the two languages that you should read the later sections of this chapter carefully. You'll find the C++ notes helpful for making the transition.

### 4.1 Introduction to Object-Oriented Programming

Object-oriented programming, or OOP for short, is the dominant programming paradigm these days, having replaced the「structured」or procedural programming techniques that were developed in the 1970s. Since Java is object-oriented, you have to be familiar with OOP to become productive with Java.

An object-oriented program is made of objects. Each object has a specific functionality, exposed to its users, and a hidden implementation. Many objects in your programs will be taken「off-the-shelf」from a library; others will be custom-designed. Whether you build an object or buy it might depend on your budget or time. But, basically, as long as an object satisfies your specifications, you don't care how the functionality is implemented.

Traditional structured programming consists of designing a set of procedures (or algorithms) to solve a problem. Once the procedures are determined, the traditional next step was to find appropriate ways to store the data. This is why the designer of the Pascal language, Niklaus Wirth, called his famous book on programming Algorithms + Data Structures = Programs (Prentice Hall, 1975). Notice that in Wirth's title, algorithms come first, and data structures second. This reflects the way programmers worked at that time. First, they decided on the procedures for manipulating the data; then, they decided what structure to impose on the data to make the manipulations easier. OOP reverses the order: puts the data first, then looks at the algorithms to operate on the data.

For small problems, the breakdown into procedures works very well. But objects are more appropriate for larger problems. Consider a simple web browser. It might require 2,000 procedures for its implementation, all of which manipulate a set of global data. In the object-oriented style, there might be 100 classes with an average of 20 methods per class (see Figure 4.1). This structure is much easier for a programmer to grasp. It is also much easier to find bugs in. Suppose the data of a particular object is in an incorrect state. It is far easier to search for the culprit among the 20 methods that had access to that data item than among 2,000 procedures.

Figure 4.1 Procedural vs. OO programming

#### 4.1.1 Classes

A class is the template or blueprint from which objects are made. Think of classes as cookie cutters; objects are the cookies themselves. When you construct an object from a class, you are said to have created an instance of the class.

As you have seen, all code that you write in Java is inside a class. The standard Java library supplies several thousand classes for such diverse purposes as user interface design, dates and calendars, and network programming. Nonetheless, in Java you still have to create your own classes to describe the objects of your application's problem domain.

Encapsulation (sometimes called information hiding) is a key concept in working with objects. Formally, encapsulation is simply combining data and behavior in one package and hiding the implementation details from the users of the object. The bits of data in an object are called its instance fields, and the procedures that operate on the data are called its methods. A specific object that is an instance of a class will have specific values of its instance fields. The set of those values is the current state of the object. Whenever you invoke a method on an object, its state may change.

The key to making encapsulation work is to have methods never directly access instance fields in a class other than their own. Programs should interact with object data only through the object's methods. Encapsulation is the way to give an object its「black box」behavior, which is the key to reuse and reliability. This means a class may totally change how it stores its data, but as long as it continues to use the same methods to manipulate the data, no other object will know or care.

When you start writing your own classes in Java, another tenet of OOP will make this easier: Classes can be built by extending other classes. Java, in fact, comes with a「cosmic superclass」called Object. All other classes extend this class. You will learn more about the Object class in the next chapter.

When you extend an existing class, the new class has all the properties and methods of the class that you extend. You then supply new methods and data fields that apply to your new class only. The concept of extending a class to obtain another class is called inheritance. See the next chapter for more on inheritance.

#### 4.1.2 Objects

To work with OOP, you should be able to identify three key characteristics of objects:

The object's behavior—what can you do with this object, or what methods can you apply to it?

The object's state—how does the object react when you invoke those methods?

The object's identity—how is the object distinguished from others that may have the same behavior and state?

All objects that are instances of the same class share a family resemblance by supporting the same behavior. The behavior of an object is defined by the methods that you can call.

Next, each object stores information about what it currently looks like. This is the object's state. An object's state may change over time, but not spontaneously. A change in the state of an object must be a consequence of method calls. (If an object's state changed without a method call on that object, someone broke encapsulation.)

However, the state of an object does not completely describe it, because each object has a distinct identity. For example, in an order processing system, two orders are distinct even if they request identical items. Notice that the individual objects that are instances of a class always differ in their identity and usually differ in their state.

These key characteristics can influence each other. For example, the state of an object can influence its behavior. (If an order is「shipped」or「paid,」it may reject a method call that asks it to add or remove items. Conversely, if an order is「empty」—that is, no items have yet been ordered—it should not allow itself to be shipped.)

#### 4.1.3 Identifying Classes

In a traditional procedural program, you start the process at the top, with the main function. When designing an object-oriented system, there is no「top,」and newcomers to OOP often wonder where to begin. The answer is: Identify your classes and then add methods to each class.

A simple rule of thumb in identifying classes is to look for nouns in the problem analysis. Methods, on the other hand, correspond to verbs.

For example, in an order-processing system, some of the nouns are

Item

Order

Shipping address

Payment

Account

These nouns may lead to the classes Item, Order, and so on.

Next, look for verbs. Items are added to orders. Orders are shipped or canceled. Payments are applied to orders. With each verb, such as「add,」「ship,」「cancel,」or「apply,」you identify the object that has the major responsibility for carrying it out. For example, when a new item is added to an order, the order object should be the one in charge because it knows how it stores and sorts items. That is, add should be a method of the Order class that takes an Item object as a parameter.

Of course, the「noun and verb」is but a rule of thumb; only experience can help you decide which nouns and verbs are the important ones when building your classes.

#### 4.1.4 Relationships between Classes

The most common relationships between classes are

Dependence (「uses–a」)

Aggregation (「has–a」)

Inheritance (「is–a」)

The dependence, or「uses–a」relationship, is the most obvious and also the most general. For example, the Order class uses the Account class because Order objects need to access Account objects to check for credit status. But the Item class does not depend on the Account class, because Item objects never need to worry about customer accounts. Thus, a class depends on another class if its methods use or manipulate objects of that class.

Try to minimize the number of classes that depend on each other. The point is, if a class A is unaware of the existence of a class B, it is also unconcerned about any changes to B. (And this means that changes to B do not introduce bugs into A.) In software engineering terminology, you want to minimize the coupling between classes.

The aggregation, or「has–a」relationship, is easy to understand because it is concrete; for example, an Order object contains Item objects. Containment means that objects of class A contain objects of class B.

Note: Some methodologists view the concept of aggregation with disdain and prefer to use a more general「association」relationship. From the point of view of modeling, that is understandable. But for programmers, the「has–a」relationship makes a lot of sense. We like to use aggregation for another reason as well: The standard notation for associations is less clear. See Table 4.1.

Table 4.1 UML Notation for Class Relationships

Relationship

UML Connector

Inheritance

Interface implementation

Dependency

Aggregation

Association

Directed association

The inheritance, or「is–a」relationship, expresses a relationship between a more special and a more general class. For example, a RushOrder class inherits from an Order class. The specialized RushOrder class has special methods for priority handling and a different method for computing shipping charges, but its other methods, such as adding items and billing, are inherited from the Order class. In general, if class A extends class B, class A inherits methods from class B but has more capabilities. (See the next chapter in which we discuss this important notion at some length.)

Many programmers use the UML (Unified Modeling Language) notation to draw class diagrams that describe the relationships between classes. You can see an example of such a diagram in Figure 4.2. You draw classes as rectangles, and relationships as arrows with various adornments. Table 4.1 shows the most common UML arrow styles.

Figure 4.2 A class diagram

### 4.2 Using Predefined Classes

You can't do anything in Java without classes, and you have already seen several classes at work. However, not all of these show off the typical features of object orientation. Take, for example, the Math class. You have seen that you can use methods of the Math class, such as Math.random, without needing to know how they are implemented—all you need to know is the name and parameters (if any). That's the point of encapsulation, and it will certainly be true of all classes. But the Math class only encapsulates functionality; it neither needs nor hides data. Since there is no data, you do not need to worry about making objects and initializing their instance fields—there aren't any!

In the next section, we will look at a more typical class, the Date class. You will see how to construct objects and call methods of this class.

#### 4.2.1 Objects and Object Variables

To work with objects, you first construct them and specify their initial state. Then you apply methods to the objects.

In the Java programming language, you use constructors to construct new instances. A constructor is a special method whose purpose is to construct and initialize objects. Let us look at an example. The standard Java library contains a Date class. Its objects describe points in time, such as December 31, 1999, 23:59:59 GMT.

Note: You may be wondering: Why use a class to represent dates rather than (as in some languages) a built-in type? For example, Visual Basic has a built-in date type, and programmers can specify dates in the format #6/1/1995#. On the surface, this sounds convenient—programmers can simply use the built-in date type without worrying about classes. But actually, how suitable is the Visual Basic design? In some locales, dates are specified as month/day/year, in others as day/month/year. Are the language designers really equipped to foresee these kinds of issues? If they do a poor job, the language becomes an unpleasant muddle, but unhappy programmers are powerless to do anything about it. With classes, the design task is offloaded to a library designer. If the class is not perfect, other programmers can easily write their own classes to enhance or replace the system classes. (To prove the point: The Java date library started out a bit muddled, and it has been redesigned twice.)

Constructors always have the same name as the class name. Thus, the constructor for the Date class is called Date. To construct a Date object, combine the constructor with the new operator, as follows:

new Date()

This expression constructs a new object. The object is initialized to the current date and time.

If you like, you can pass the object to a method:

System.out.println(new Date());

Alternatively, you can apply a method to the object that you just constructed. One of the methods of the Date class is the toString method. That method yields a string representation of the date. Here is how you would apply the toString method to a newly constructed Date object:

String s = new Date().toString();

In these two examples, the constructed object is used only once. Usually, you will want to hang on to the objects that you construct so that you can keep using them. Simply store the object in a variable:

Date birthday = new Date();

Figure 4.3 shows the object variable birthday that refers to the newly constructed object.

Figure 4.3 Creating a new object

There is an important difference between objects and object variables. For example, the statement

Click here to view code image

Date deadline; // deadline doesn't refer to any object

defines an object variable, deadline, that can refer to objects of type Date. It is important to realize that the variable deadline is not an object and, in fact, does not even refer to an object yet. You cannot use any Date methods on this variable at this time. The statement

s = deadline.toString(); // not yet

would cause a compile-time error.

You must first initialize the deadline variable. You have two choices. Of course, you can initialize the variable so that it refers to a newly constructed object:

deadline = new Date();

Or you can set the variable to refer to an existing object:

deadline = birthday;

Now both variables refer to the same object (see Figure 4.4).

Figure 4.4 Object variables that refer to the same object

It is important to realize that an object variable doesn't actually contain an object. It only refers to an object.

In Java, the value of any object variable is a reference to an object that is stored elsewhere. The return value of the new operator is also a reference. A statement such as

Date deadline = new Date();

has two parts. The expression new Date() makes an object of type Date, and its value is a reference to that newly created object. That reference is then stored in the deadline variable.

You can explicitly set an object variable to null to indicate that it currently refers to no object.

Click here to view code image

deadline = null;

. . .

if (deadline != null)

System.out.println(deadline);

We will discuss null in more detail in Section 4.3.6,「Working with null References,」on p. 148.

C++ Note

Some people mistakenly believe that Java object variables behave like C++ references. But in C++ there are no null references, and references cannot be assigned. You should think of Java object variables as analogous to object pointers in C++. For example,

Date birthday; // Java

is really the same as

Date* birthday; // C++

Once you make this association, everything falls into place. Of course, a Date* pointer isn't initialized until you initialize it with a call to new. The syntax is almost the same in C++ and Java.

Date* birthday = new Date(); // C++

If you copy one variable to another, then both variables refer to the same date—they are pointers to the same object. The equivalent of the Java null reference is the C++ NULL pointer.

All Java objects live on the heap. When an object contains another object variable, it contains just a pointer to yet another heap object.

In C++, pointers make you nervous because they are so error-prone. It is easy to create bad pointers or to mess up memory management. In Java, these problems simply go away. If you use an uninitialized pointer, the runtime system will reliably generate a runtime error instead of producing random results. You don't have to worry about memory management, because the garbage collector takes care of it.

C++ makes quite an effort, with its support for copy constructors and assignment operators, to allow the implementation of objects that copy themselves automatically. For example, a copy of a linked list is a new linked list with the same contents but with an independent set of links. This makes it possible to design classes with the same copy behavior as the built-in types. In Java, you must use the clone method to get a complete copy of an object.

#### 4.2.2 The LocalDate Class of the Java Library

In the preceding examples, we used the Date class that is a part of the standard Java library. An instance of the Date class has a state—namely, a particular point in time.

Although you don't need to know this when you use the Date class, the time is represented by the number of milliseconds (positive or negative) from a fixed point, the so-called epoch, which is 00:00:00 UTC, January 1, 1970. UTC is the Coordinated Universal Time, the scientific time standard which is, for practical purposes, the same as the more familiar GMT, or Greenwich Mean Time.

But as it turns out, the Date class is not very useful for manipulating the kind of calendar information that humans use for dates, such as「December 31, 1999」. This particular description of a day follows the Gregorian calendar, which is the calendar used in most countries of the world. The same point in time would be described quite differently in the Chinese or Hebrew lunar calendars, not to mention the calendar used by your customers from Mars.

Note: Throughout human history, civilizations grappled with the design of calendars to attach names to dates and bring order to the solar and lunar cycles. For a fascinating explanation of calendars around the world, from the French Revolutionary calendar to the Mayan long count, see Calendrical Calculations by Nachum Dershowitz and Edward M. Reingold (Cambridge University Press, 3rd ed., 2007).

The library designers decided to separate the concerns of keeping time and attaching names to points in time. Therefore, the standard Java library contains two separate classes: the Date class, which represents a point in time, and the LocalDate class, which expresses days in the familiar calendar notation. Java 8 introduced quite a few other classes for manipulating various aspects of date and time—see Chapter 6 of Volume II.

Separating time measurement from calendars is good object-oriented design. In general, it is a good idea to use different classes to express different concepts.

You do not use a constructor to construct objects of the LocalDate class. Instead, use static factory methods that call constructors on your behalf. The expression

LocalDate.now()

constructs a new object that represents the date at which the object was constructed.

You can construct an object for a specific date by supplying year, month, and day:

LocalDate.of(1999, 12, 31)

Of course, you will usually want to store the constructed object in an object variable:

Click here to view code image

LocalDate newYearsEve = LocalDate.of(1999, 12, 31);

Once you have a LocalDate object, you can find out the year, month, and day with the methods getYear, getMonthValue, and getDayOfMonth:

Click here to view code image

int year = newYearsEve.getYear(); // 1999

int month = newYearsEve.getMonthValue(); // 12

int day = newYearsEve.getDayOfMonth(); // 31

This may seem pointless because they are the very same values that you just used to construct the object. But sometimes, you have a date that has been computed, and then you will want to invoke those methods to find out more about it. For example, the plusDays method yields a new LocalDate that is a given number of days away from the object to which you apply it:

Click here to view code image

LocalDate aThousandDaysLater = newYearsEve.plusDays(1000);

year = aThousandDaysLater.getYear(); // 2002

month = aThousandDaysLater.getMonthValue(); // 09

day = aThousandDaysLater.getDayOfMonth(); // 26

The LocalDate class has encapsulated instance fields to maintain the date to which it is set. Without looking at the source code, it is impossible to know the representation that the class uses internally. But, of course, the point of encapsulation is that this doesn't matter. What matters are the methods that a class exposes.

Note: Actually, the Date class also has methods to get the day, month, and year, called getDay, getMonth, and getYear, but these methods are deprecated. A method is deprecated when a library designer realizes that the method should have never been introduced in the first place.

These methods were a part of the Date class before the library designers realized that it makes more sense to supply separate classes to deal with calendars. When an earlier set of calendar classes was introduced in Java 1.1, the Date methods were tagged as deprecated. You can still use them in your programs, but you will get unsightly compiler warnings if you do. It is a good idea to stay away from using deprecated methods because they may be removed in a future version of the library.

Tip: The JDK provides the jdeprscan tool for checking whether your code uses deprecated features of the Java API. See https://docs.oracle.com/javase/9/tools/jdeprscan.htm for instructions.

#### 4.2.3 Mutator and Accessor Methods

Have another look at the plusDays method call that you saw in the preceding section:

Click here to view code image

LocalDate aThousandDaysLater = newYearsEve.plusDays(1000);

What happens to newYearsEve after the call? Has it been changed to be a thousand days later? As it turns out, it has not. The plusDays method yields a new LocalDate object, which is then assigned to the aThousandDaysLater variable. The original object remains unchanged. We say that the plusDays method does not mutate the object on which it is invoked. (This is similar to the toUpperCase method of the String class that you saw in Chapter 3. When you call toUpperCase on a string, that string stays the same, and a new string with uppercase characters is returned.)

An earlier version of the Java library had a different class for dealing with calendars, called GregorianCalendar. Here is how you add a thousand days to a date represented by that class:

Click here to view code image

GregorianCalendar someDay = new GregorianCalendar(1999, 11, 31);

// odd feature of that class: month numbers go from 0 to 11

someDay.add(Calendar.DAY_OF_MONTH, 1000);

Unlike the LocalDate.plusDays method, the GregorianCalendar.add method is a mutator method. After invoking it, the state of the someDay object has changed. Here is how you can find out the new state:

Click here to view code image

year = someDay.get(Calendar.YEAR); // 2002

month = someDay.get(Calendar.MONTH) + 1; // 09

day = someDay.get(Calendar.DAY_OF_MONTH); // 26

That's why we called the variable someDay and not newYearsEve—it no longer is new year's eve after calling the mutator method.

In contrast, methods that only access objects without modifying them are sometimes called accessor methods. For example, LocalDate.getYear and GregorianCalendar.get are accessor methods.

C++ Note: In C++, the const suffix denotes accessor methods. A method that is not declared as const is assumed to be a mutator. However, in the Java programming language, no special syntax distinguishes accessors from mutators.

We finish this section with a program that puts the LocalDate class to work. The program displays a calendar for the current month, like this:

Click here to view code image

Mon Tue Wed Thu Fri Sat Sun

1

2 3 4 5 6 7 8

9 10 11 12 13 14 15

16 17 18 19 20 21 22

23 24 25 26* 27 28 29

30

The current day is marked with an asterisk (*). As you can see, the program needs to know how to compute the length of a month and the weekday of a given day.

Let us go through the key steps of the program. First, we construct an object that is initialized with the current date.

Click here to view code image

LocalDate date = LocalDate.now();

We capture the current month and day.

Click here to view code image

int month = date.getMonthValue();

int today = date.getDayOfMonth();

Then we set date to the first of the month and get the weekday of that date.

Click here to view code image

date = date.minusDays(today - 1); // set to start of month

DayOfWeek weekday = date.getDayOfWeek();

int value = weekday.getValue(); // 1 = Monday, . . . , 7 = Sunday

The variable weekday is set to an object of type DayOfWeek. We call the getValue method of that object to get a numerical value for the weekday. This yields an integer that follows the international convention where the weekend comes at the end of the week, returning 1 for Monday, 2 for Tuesday, and so on. Sunday has value 7.

Note that the first line of the calendar is indented, so that the first day of the month falls on the appropriate weekday. Here is the code to print the header and the indentation for the first line:

Click here to view code image

System.out.println("Mon Tue Wed Thu Fri Sat Sun");

for (int i = 1; i < value; i++)

System.out.print(" ");

Now, we are ready to print the body of the calendar. We enter a loop in which date traverses the days of the month.

In each iteration, we print the date value. If date is today, the date is marked with an *. Then, we advance date to the next day. When we reach the beginning of each new week, we print a new line:

Click here to view code image

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

When do we stop? We don't know whether the month has 31, 30, 29, or 28 days. Instead, we keep iterating while date is still in the current month.

Listing 4.1 shows the complete program.

As you can see, the LocalDate class makes it possible to write a calendar program that takes care of complexities such as weekdays and the varying month lengths. You don't need to know how the LocalDate class computes months and weekdays. You just use the interface of the class—the methods such as plusDays and getDayOfWeek.

The point of this example program is to show you how you can use the interface of a class to carry out fairly sophisticated tasks without having to know the implementation details.

Listing 4.1 CalendarTest/CalendarTest.java

Click here to view code image

1 import java.time.*;

2

3 /**

4 * @version 1.5 2015-05-08

5 * @author Cay Horstmann

6 */

7 public class CalendarTest

8 {

9 public static void main(String[] args)

10 {

11 LocalDate date = LocalDate.now();

12 int month = date.getMonthValue();

13 int today = date.getDayOfMonth();

14

15 date = date.minusDays(today - 1); // set to start of month

16 DayOfWeek weekday = date.getDayOfWeek();

17 int value = weekday.getValue(); // 1 = Monday, . . . , 7 = Sunday

18

19 System.out.println("Mon Tue Wed Thu Fri Sat Sun");

20 for (int i = 1; i < value; i++)

21 System.out.print(" ");

22 while (date.getMonthValue() == month)

23 {

24 System.out.printf("%3d", date.getDayOfMonth());

25 if (date.getDayOfMonth() == today)

26 System.out.print("*");

27 else

28 System.out.print(" ");

29 date = date.plusDays(1);

30 if (date.getDayOfWeek().getValue() == 1) System.out.println();

31 }

32 if (date.getDayOfWeek().getValue() != 1) System.out.println();

33 }

34 }

java.time.LocalDate 8

static LocalDate now()

constructs an object that represents the current date.

static LocalDate of(int year, int month, int day)

constructs an object that represents the given date.

int getYear()

int getMonthValue()

int getDayOfMonth()

gets the year, month, and day of this date.

DayOfWeek getDayOfWeek

gets the weekday of this date as an instance of the DayOfWeek class. Call getValue to get a weekday between 1 (Monday) and 7 (Sunday).

LocalDate plusDays(int n)

LocalDate minusDays(int n)

yields the date that is n days after or before this date.

### 4.3 Defining Your Own Classes

In Chapter 3, you started writing simple classes. However, all those classes had just a single main method. Now the time has come to show you how to write the kind of「workhorse classes」that are needed for more sophisticated applications. These classes typically do not have a main method. Instead, they have their own instance fields and methods. To build a complete program, you combine several classes, one of which has a main method.

#### 4.3.1 An Employee Class

The simplest form for a class definition in Java is

Click here to view code image

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

Consider the following, very simplified, version of an Employee class that might be used by a business in writing a payroll system:

Click here to view code image

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

Click here to view code image

Employee[] staff = new Employee[3];

staff[0] = new Employee("Carl Cracker", . . .);

staff[1] = new Employee("Harry Hacker", . . .);

staff[2] = new Employee("Tony Tester", . . .);

Next, we use the raiseSalary method of the Employee class to raise each employee's salary by 5%:

Click here to view code image

for (Employee e : staff)

e.raiseSalary(5);

Finally, we print out information about each employee, by calling the getName,

Click here to view code image

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

Click here to view code image

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

#### 4.3.2 Use of Multiple Source Files

The program in Listing 4.2 has two classes in a single source file. Many programmers prefer to put each class into its own source file. For example, you can place the Employee class into a file Employee.java and the EmployeeTest class into EmployeeTest.java.

If you like this arrangement, you have two choices for compiling the program. You can invoke the Java compiler with a wildcard:

javac Employee*.java

Then, all source files matching the wildcard will be compiled into class files. Or, you can simply type

javac EmployeeTest.java

You may find it surprising that the second choice works even though the Employee.java file is never explicitly compiled. However, when the Java compiler sees the Employee class being used inside EmployeeTest.java, it will look for a file named Employee.class. If it does not find that file, it automatically searches for Employee.java and compiles it. Moreover, if the timestamp of the version of Employee.java that it finds is newer than that of the existing Employee.class file, the Java compiler will automatically recompile the file.

Note: If you are familiar with the make facility of UNIX (or one of its Windows cousins, such as nmake), you can think of the Java compiler as having the make functionality already built in.

#### 4.3.3 Dissecting the Employee Class

In the sections that follow, we will dissect the Employee class. Let's start with the methods in this class. As you can see by examining the source code, this class has one constructor and four methods:

Click here to view code image

public Employee(String n, double s, int year, int month, int day)

public String getName()

public double getSalary()

public LocalDate getHireDay()

public void raiseSalary(double byPercent)

All methods of this class are tagged as public. The keyword public means that any method in any class can call the method. (The four possible access levels are covered in this and the next chapter.)

Next, notice the three instance fields that will hold the data manipulated inside an instance of the Employee class.

Click here to view code image

private String name;

private double salary;

private LocalDate hireDay;

The private keyword makes sure that the only methods that can access these instance fields are the methods of the Employee class itself. No outside method can read or write to these fields.

Note: You could use the public keyword with your instance fields, but it would be a very bad idea. Having public data fields would allow any part of the program to read and modify the instance fields, completely ruining encapsulation. Any method of any class can modify public fields—and, in our experience, some code will take advantage of that access privilege when you least expect it. We strongly recommend to make all your instance fields private.

Finally, notice that two of the instance fields are themselves objects: The name and hireDay fields are references to String and LocalDate objects. This is quite usual: Classes will often contain instance fields of class type.

#### 4.3.4 First Steps with Constructors

Let's look at the constructor listed in our Employee class.

Click here to view code image

public Employee(String n, double s, int year, int month, int day)

{

name = n;

salary = s;

hireDay = LocalDate.of(year, month, day);

}

As you can see, the name of the constructor is the same as the name of the class. This constructor runs when you construct objects of the Employee class—giving the instance fields the initial state you want them to have.

For example, when you create an instance of the Employee class with code like this:

Click here to view code image

new Employee("James Bond", 100000, 1950, 1, 1)

you have set the instance fields as follows:

Click here to view code image

name = "James Bond";

salary = 100000;

hireDay = LocalDate.of(1950, 1, 1); // January 1, 1950

There is an important difference between constructors and other methods. A constructor can only be called in conjunction with the new operator. You can't apply a constructor to an existing object to reset the instance fields. For example,

Click here to view code image

james.Employee("James Bond", 250000, 1950, 1, 1) // ERROR

is a compile-time error.

We will have more to say about constructors later in this chapter. For now, keep the following in mind:

A constructor has the same name as the class.

A class can have more than one constructor.

A constructor can take zero, one, or more parameters.

A constructor has no return value.

A constructor is always called with the new operator.

C++ Note: Constructors work the same way in Java as they do in C++. Keep in mind, however, that all Java objects are constructed on the heap and that a constructor must be combined with new. It is a common error of C++ programmers to forget the new operator:

Click here to view code image

Employee number007("James Bond", 100000, 1950, 1, 1); // C++, not Java

That works in C++ but not in Java.

Caution

Be careful not to introduce local variables with the same names as the instance fields. For example, the following constructor will not set the salary:

Click here to view code image

public Employee(String n, double s, . . .)

{

String name = n; // ERROR

double salary = s; // ERROR

. . .

}

The constructor declares local variables name and salary. These variables are only accessible inside the constructor. They shadow the instance fields with the same name. Some programmers accidentally write this kind of code when they type faster than they think, because their fingers are used to adding the data type. This is a nasty error that can be hard to track down. You just have to be careful in all of your methods to not use variable names that equal the names of instance fields.

#### 4.3.5 Declaring Local Variables with var

As of Java 10, you can declare local variables with the var keyword instead of specifying their type, provided their type can be inferred from the initial value. For example, instead of declaring

Click here to view code image

Employee harry = new Employee("Harry Hacker", 50000, 1989, 10, 1);

you simply write

Click here to view code image

var harry = new Employee("Harry Hacker", 50000, 1989, 10, 1);

This is nice since it avoids the repetition of the type name Employee.

From now on, we will use the var notation in those cases where the type is obvious from the right-hand side without any knowledge of the Java API. But we won't use var with numeric types such as int, long, or double so that you don't have to look out for the difference between 0, 0L, and 0.0. Once you are more experienced with the Java API, you may want to use the var keyword more frequently.

Note that the var keyword can only be used with local variables inside methods. You must always declare the types of parameters and fields.

#### 4.3.6 Working with null References

In Section 4.2.1,「Objects and Object Variables,」on p. 132, you saw that an object variable holds a reference to an object, or the special value null to indicate the absence of an object.

This sounds like a convenient mechanism for dealing with special situations, such as an unknown name or hire date. But you need to be very careful with null values.

If you apply a method to a null value, a NullPointerException occurs.

Click here to view code image

LocalDate birthday = null;

String s = birthday.toString(); // NullPointerException

This is a serious error, similar to an「index out of bounds」exception. If your program does not「catch」an exception, it is terminated. Normally, programs don't catch these kinds of exceptions but rely on programmers not to cause them in the first place.

When you define a class, it is a good idea to be clear about which fields can be null. In our example, we don't want the name or hireDay field to be null. (We don't have to worry about the salary field. It has primitive type and can never be null.)

The hireDay field is guaranteed to be non-null because it is initialized with a new LocalDate object. But name will be null if the constructor is called with a null argument for n.

There are two solutions. The「permissive」approach is to turn a null argument into an appropriate non-null value:

Click here to view code image

if (n == null) name = "unknown"; else name = n;

As of Java 9, the Objects class has a convenience method for this purpose:

Click here to view code image

public Employee(String n, double s, int year, int month, int day)

{

name = Objects.requireNonNullElse(n, "unknown");

. . .

}

The「tough love」approach is to reject a null argument:

Click here to view code image

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

Click here to view code image

public void raiseSalary(double byPercent)

{

double raise = salary * byPercent / 100;

salary += raise;

}

sets a new value for the salary instance field in the object on which this method is invoked. Consider the call

Click here to view code image

number007 .raiseSalary(5);

The effect is to increase the value of the number007.salary field by 5%. More specifically, the call executes the following instructions:

Click here to view code image

double raise = number007.salary * 5 / 100;

number007.salary += raise;

The raiseSalary method has two parameters. The first parameter, called the implicit parameter, is the object of type Employee that appears before the method name. The second parameter, the number inside the parentheses after the method name, is an explicit parameter. (Some people call the implicit parameter the target or receiver of the method call.)

As you can see, the explicit parameters are explicitly listed in the method declaration—for example, double byPercent. The implicit parameter does not appear in the method declaration.

In every method, the keyword this refers to the implicit parameter. If you like, you can write the raiseSalary method as follows:

Click here to view code image

public void raiseSalary(double byPercent)

{

double raise = this.salary * byPercent / 100;

this.salary += raise;

}

Some programmers prefer that style because it clearly distinguishes between instance fields and local variables.

C++ Note

In C++, you generally define methods outside the class:

Click here to view code image

void Employee::raiseSalary(double byPercent) // C++, not Java

{

. . .

}

If you define a method inside a class, then it is, automatically, an inline method.

Click here to view code image

class Employee

{

. . .

int getName() { return name; } // inline in C++

}

In Java, all methods are defined inside the class itself. This does not make them inline. Finding opportunities for inline replacement is the job of the Java virtual machine. The just-in-time compiler watches for calls to methods that are short, commonly called, and not overridden, and optimizes them away.

#### 4.3.8 Benefits of Encapsulation

Finally, let's look more closely at the rather simple getName, getSalary, and getHireDay methods.

Click here to view code image

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

Click here to view code image

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

Click here to view code image

Employee harry = . . .;

Date d = harry.getHireDay();

double tenYearsInMilliSeconds = 10 * 365.25 * 24 * 60 * 60 * 1000;

d.setTime(d.getTime() - (long) tenYearsInMilliSeconds);

// let's give Harry ten years of added seniority

The reason is subtle. Both d and harry.hireDay refer to the same object (see Figure 4.5). Applying mutator methods to d automatically changes the private state of the Employee object!

Figure 4.5 Returning a reference to a mutable data field

If you need to return a reference to a mutable object, you should clone it first. A clone is an exact copy of an object stored in a new location. We discuss cloning in detail in Chapter 6. Here is the corrected code:

Click here to view code image

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

#### 4.3.9 Class-Based Access Privileges

You know that a method can access the private data of the object on which it is invoked. What people often find surprising is that a method can access the private data of all objects of its class. For example, consider a method equals that compares two employees.

Click here to view code image

class Employee

{

. . .

public boolean equals(Employee other)

{

return name.equals(other.name);

}

}

A typical call is

Click here to view code image

if (harry.equals(boss)) . . .

This method accesses the private fields of harry, which is not surprising. It also accesses the private fields of boss. This is legal because boss is an object of type Employee, and a method of the Employee class is permitted to access the private fields of any object of type Employee.

C++ Note

C++ has the same rule. A method can access the private features of any object of its class, not just of the implicit parameter.

#### 4.3.10 Private Methods

When implementing a class, we make all data fields private because public data are dangerous. But what about the methods? While most methods are public, private methods are useful in certain circumstances. Sometimes, you may wish to break up the code for a computation into separate helper methods. Typically, these helper methods should not be part of the public interface—they may be too close to the current implementation or require a special protocol or calling order. Such methods are best implemented as private.

To implement a private method in Java, simply change the public keyword to private.

By making a method private, you are under no obligation to keep it available if you change your implementation. The method may well be harder to implement or unnecessary if the data representation changes; this is irrelevant. The point is that as long as the method is private, the designers of the class can be assured that it is never used elsewhere, so they can simply drop it. If a method is public, you cannot simply drop it because other code might rely on it.

#### 4.3.11 Final Instance Fields

You can define an instance field as final. Such a field must be initialized when the object is constructed. That is, you must guarantee that the field value has been set after the end of every constructor. Afterwards, the field may not be modified again. For example, the name field of the Employee class may be declared as final because it never changes after the object is constructed—there is no

Click here to view code image

class Employee

{

private final String name;

. . .

}

The final modifier is particularly useful for fields whose type is primitive or an immutable class. (A class is immutable if none of its methods ever mutate its objects. For example, the String class is immutable.)

For mutable classes, the final modifier can be confusing. For example, consider a field

Click here to view code image

private final StringBuilder evaluations;

that is initialized in the Employee constructor as

Click here to view code image

evaluations = new StringBuilder();

The final keyword merely means that the object reference stored in the evaluations variable will never again refer to a different StringBuilder object. But the object can be mutated:

Click here to view code image

public void giveGoldStar()

{

evaluations.append(LocalDate.now() + ": Gold star!\n");

}

### 4.4 Static Fields and Methods

In all sample programs that you have seen, the main method is tagged with the static modifier. We are now ready to discuss the meaning of this modifier.

#### 4.4.1 Static Fields

If you define a field as static, then there is only one such field per class. In contrast, each object has its own copy of nonstatic instance fields. For example, let's suppose we want to assign a unique identification number to each employee. We add an instance field id and a static field nextId to the Employee class:

Click here to view code image

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

Click here to view code image

public void setId()

{

id = nextId;

nextId++;

}

Suppose you set the employee identification number for harry:

harry.setId();

Then, the id field of harry is set to the current value of the static field nextId, and the value of the static field is incremented:

Click here to view code image

harry.id = Employee.nextId;

Employee.nextId++;

#### 4.4.2 Static Constants

Static variables are quite rare. However, static constants are more common. For example, the Math class defines a static constant:

Click here to view code image

public class Math

{

. . .

public static final double PI = 3.14159265358979323846;

. . .

}

You can access this constant in your programs as Math.PI.

If the keyword static had been omitted, then PI would have been an instance field of the Math class. That is, you would need an object of this class to access PI, and every Math object would have its own copy of PI.

Another static constant that you have used many times is System.out. It is declared in the System class as follows:

Click here to view code image

public class System

{

. . .

public static final PrintStream out = . . .;

. . .

}

As we mentioned several times, it is never a good idea to have public fields, because everyone can modify them. However, public constants (that is, final fields) are fine. Since out has been declared as final, you cannot reassign another print stream to it:

Click here to view code image

System.out = new PrintStream(. . .); // ERROR--out is final

Note: If you look at the System class, you will notice a method setOut that sets System.out to a different stream. You may wonder how that method can change the value of a final variable. However, the setOut method is a native method, not implemented in the Java programming language. Native methods can bypass the access control mechanisms of the Java language. This is a very unusual workaround that you should not emulate in your programs.

#### 4.4.3 Static Methods

Static methods are methods that do not operate on objects. For example, the pow method of the Math class is a static method. The expression

Math.pow(x, a)

computes the power xa. It does not use any Math object to carry out its task. In other words, it has no implicit parameter.

You can think of static methods as methods that don't have a this parameter. (In a nonstatic method, the this parameter refers to the implicit parameter of the method—see Section 4.3.7,「Implicit and Explicit Parameters,」on p. 150.)

A static method of the Employee class cannot access the id instance field because it does not operate on an object. However, a static method can access a static field. Here is an example of such a static method:

Click here to view code image

public static int getNextId()

{

return nextId; // returns static field

}

To call this method, you supply the name of the class:

Click here to view code image

int n = Employee.getNextId();

Could you have omitted the keyword static for this method? Yes, but then you would need to have an object reference of type Employee to invoke the method.

Note

It is legal to use an object to call a static method. For example, if harry is an Employee object, then you can call harry.getNextId() instead of Employee.getNextId(). However, we find that notation confusing. The getNextId method doesn't look at harry at all to compute the result. We recommend that you use class names, not objects, to invoke static methods.

Use static methods in two situations:

When a method doesn't need to access the object state because all needed parameters are supplied as explicit parameters (example: Math.pow).

When a method only needs to access static fields of the class (example: Employee.getNextId).

C++ Note

Static fields and methods have the same functionality in Java and C++. However, the syntax is slightly different. In C++, you use the :: operator to access a static field or method outside its scope, such as Math::PI.

The term「static」has a curious history. At first, the keyword static was introduced in C to denote local variables that don't go away when a block is exited. In that context, the term「static」makes sense: The variable stays around and is still there when the block is entered again. Then static got a second meaning in C, to denote global variables and functions that cannot be accessed from other files. The keyword static was simply reused to avoid introducing a new keyword. Finally, C++ reused the keyword for a third, unrelated, interpretation—to denote variables and functions that belong to a class but not to any particular object of the class. That is the same meaning the keyword has in Java.

#### 4.4.4 Factory Methods

Here is another common use for static methods. Classes such as LocalDate and NumberFormat use static factory methods that construct objects. You have already seen the factory methods LocalDate.now and LocalDate.of. Here is how the NumberFormat class yields formatter objects for various styles:

Click here to view code image

NumberFormat currencyFormatter = NumberFormat.getCurrencyInstance();

NumberFormat percentFormatter = NumberFormat.getPercentInstance();

double x = 0.1;

System.out.println(currencyFormatter.format(x)); // prints $0.10

System.out.println(percentFormatter.format(x)); // prints 10%

Why doesn't the NumberFormat class use a constructor instead? There are two reasons:

You can't give names to constructors. The constructor name is always the same as the class name. But we want two different names to get the currency instance and the percent instance.

When you use a constructor, you can't vary the type of the constructed object. But the factory methods actually return objects of the class DecimalFormat, a subclass that inherits from NumberFormat. (See Chapter 5 for more on inheritance.)

#### 4.4.5 The main Method

Note that you can call static methods without having any objects. For example, you never construct any objects of the Math class to call Math.pow.

For the same reason, the main method is a static method.

Click here to view code image

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

Click here to view code image

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

Click here to view code image

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

### 4.5 Method Parameters

Let us review the computer science terms that describe how parameters can be passed to a method (or a function) in a programming language. The term call by value means that the method gets just the value that the caller provides. In contrast, call by reference means that the method gets the location of the variable that the caller provides. Thus, a method can modify the value stored in a variable passed by reference but not in one passed by value. These「call by . . .」terms are standard computer science terminology describing the behavior of method parameters in various programming languages, not just Java. (There is also a call by name that is mainly of historical interest, being employed in the Algol programming language, one of the oldest high-level languages.)

The Java programming language always uses call by value. That means that the method gets a copy of all parameter values. In particular, the method cannot modify the contents of any parameter variables passed to it.

For example, consider the following call:

Click here to view code image

double percent = 10;

harry.raiseSalary(percent);

No matter how the method is implemented, we know that after the method call, the value of percent is still 10.

Let us look a little more closely at this situation. Suppose a method tried to triple the value of a method parameter:

Click here to view code image

public static void tripleValue(double x) // doesn't work

{

x = 3 * x;

}

Let's call this method:

Click here to view code image

double percent = 10;

tripleValue(percent);

However, this does not work. After the method call, the value of percent is still 10. Here is what happens:

x is initialized with a copy of the value of percent (that is, 10).

x is tripled—it is now 30. But percent is still 10 (see Figure 4.6).

Figure 4.6 Modifying a numeric parameter has no lasting effect.

The method ends, and the parameter variable x is no longer in use.

There are, however, two kinds of method parameters:

Primitive types (numbers, boolean values)

Object references

You have seen that it is impossible for a method to change a primitive type parameter. The situation is different for object parameters. You can easily implement a method that triples the salary of an employee:

Click here to view code image

public static void tripleSalary(Employee x) // works

{

x.raiseSalary(200);

}

When you call

Click here to view code image

harry = new Employee(. . .);

tripleSalary(harry);

then the following happens:

x is initialized with a copy of the value of harry—that is, an object reference.

The raiseSalary method is applied to that object reference. The Employee object to which both x and harry refer gets its salary raised by 200 percent.

The method ends, and the parameter variable x is no longer in use. Of course, the object variable harry continues to refer to the object whose salary was tripled (see Figure 4.7).

Figure 4.7 Modifying an object parameter has a lasting effect.

As you have seen, it is easily possible—and in fact very common—to implement methods that change the state of an object parameter. The reason is simple. The method gets a copy of the object reference, and both the original and the copy refer to the same object.

Many programming languages (in particular, C++ and Pascal) have two mechanisms for parameter passing: call by value and call by reference. Some programmers (and unfortunately even some book authors) claim that Java uses call by reference for objects. That is false. As this is such a common misunderstanding, it is worth examining a counterexample in detail.

Let's try to write a method that swaps two Employee objects:

Click here to view code image

public static void swap(Employee x, Employee y) // doesn't work

{

Employee temp = x;

x = y;

y = temp;

}

If Java used call by reference for objects, this method would work:

Click here to view code image

var a = new Employee("Alice", . . .);

var b = new Employee("Bob", . . .);

swap(a, b);

// does a now refer to Bob, b to Alice?

However, the method does not actually change the object references that are stored in the variables a and b. The x and y parameters of the swap method are initialized with copies of these references. The method then proceeds to swap these copies.

Click here to view code image

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

Click here to view code image

Testing tripleValue:

Before: percent=10.0

End of method: x=30.0

After: percent=10.0

It then successfully triples the salary of an employee:

Click here to view code image

Testing tripleSalary:

Before: salary=50000.0

End of method: salary=150000.0

After: salary=150000.0

After the method, the state of the object to which harry refers has changed. This is possible because the method modified the state through a copy of the object reference.

Finally, the program demonstrates the failure of the swap method:

Click here to view code image

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

Click here to view code image

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

### 4.6 Object Construction

You have seen how to write simple constructors that define the initial state of your objects. However, since object construction is so important, Java offers quite a variety of mechanisms for writing constructors. We go over these mechanisms in the sections that follow.

#### 4.6.1 Overloading

Some classes have more than one constructor. For example, you can construct an empty StringBuilder object as

Click here to view code image

var messages = new StringBuilder();

Alternatively, you can specify an initial string:

Click here to view code image

var todoList = new StringBuilder("To do:\n");

This capability is called overloading. Overloading occurs if several methods have the same name (in this case, the StringBuilder constructor method) but different parameters. The compiler must sort out which method to call. It picks the correct method by matching the parameter types in the headers of the various methods with the types of the values used in the specific method call. A compile-time error occurs if the compiler cannot match the parameters, either because there is no match at all or because there is not one that is better than all others. (The process of finding a match is called overloading resolution.)

Note

Java allows you to overload any method—not just constructor methods. Thus, to completely describe a method, you need to specify its name together with its parameter types. This is called the signature of the method. For example, the String class has four public methods called indexOf. They have signatures

Click here to view code image

indexOf(int)

indexOf(int, int)

indexOf(String)

indexOf(String, int)

The return type is not part of the method signature. That is, you cannot have two methods with the same names and parameter types but different return types.

#### 4.6.2 Default Field Initialization

If you don't set a field explicitly in a constructor, it is automatically set to a default value: numbers to 0, boolean values to false, and object references to null. Some people consider it poor programming practice to rely on the defaults. Certainly, it makes it harder for someone to understand your code if fields are being initialized invisibly.

Note

This is an important difference between fields and local variables. You must always explicitly initialize local variables in a method. But in a class, if you don't initialize a field, it is automatically initialized to a default (0, false, or null).

For example, consider the Employee class. Suppose you don't specify how to initialize some of the fields in a constructor. By default, the salary field would be initialized with 0 and the name and hireDay fields would be initialized with null.

However, that would not be a good idea. If anyone called the getName or getHireDay method, they would get a null reference that they probably don't expect:

Click here to view code image

LocalDate h = harry.getHireDay();

int year = h.getYear(); // throws exception if h is null

#### 4.6.3 The Constructor with No Arguments

Many classes contain a constructor with no arguments that creates an object whose state is set to an appropriate default. For example, here is a no-argument constructor for the Employee class:

Click here to view code image

public Employee()

{

name = "";

salary = 0;

hireDay = LocalDate.now();

}

If you write a class with no constructors whatsoever, then a no-argument constructor is provided for you. This constructor sets all the instance fields to their default values. So, all numeric data contained in the instance fields would be 0, all boolean values would be false, and all object variables would be null.

If a class supplies at least one constructor but does not supply a no-argument constructor, it is illegal to construct objects without supplying arguments. For example, our original Employee class in Listing 4.2 provided a single constructor:

Click here to view code image

public Employee(String n, double s, int year, int month, int day)

With that class, it was not legal to construct default employees. That is, the call

e = new Employee();

would have been an error.

Caution

Please keep in mind that you get a free no-argument constructor only when your class has no other constructors. If you write your class with even a single constructor of your own and you want the users of your class to have the ability to create an instance by a call to

new ClassName()

then you must provide a no-argument constructor. Of course, if you are happy with the default values for all fields, you can simply supply

Click here to view code image

public ClassName()

{

}

#### 4.6.4 Explicit Field Initialization

By overloading the constructor methods in a class, you can build many ways to set the initial state of the instance fields of your classes. It is always a good idea to make sure that, regardless of the constructor call, every instance field is set to something meaningful.

You can simply assign a value to any field in the class definition. For example:

Click here to view code image

class Employee

{

private String name = "";

. . .

}

This assignment is carried out before the constructor executes. This syntax is particularly useful if all constructors of a class need to set a particular instance field to the same value.

The initialization value doesn't have to be a constant value. Here is an example in which a field is initialized with a method call. Consider an Employee class where each employee has an id field. You can initialize it as follows:

Click here to view code image

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

Click here to view code image

Employee::Employee(String n, double s, int y, int m, int d) // C++

: name(n),

salary(s),

hireDay(y, m, d)

{

}

C++ uses this special syntax to call field constructors. In Java, there is no need for that because objects have no subobjects, only pointers to other objects.

#### 4.6.5 Parameter Names

When you write very trivial constructors (and you'll write a lot of them), it can be somewhat frustrating to come up with parameter names.

We have generally opted for single-letter parameter names:

Click here to view code image

public Employee(String n, double s)

{

name = n;

salary = s;

}

However, the drawback is that you need to read the code to tell what the n and s parameters mean.

Some programmers prefix each parameter with an「a」:

Click here to view code image

public Employee(String aName, double aSalary)

{

name = aName;

salary = aSalary;

}

That is quite neat. Any reader can immediately figure out the meaning of the parameters.

Another commonly used trick relies on the fact that parameter variables shadow instance fields with the same name. For example, if you call a parameter salary, then salary refers to the parameter, not the instance field. But you can still access the instance field as this.salary. Recall that this denotes the implicit parameter—that is, the object being constructed. Here is an example:

Click here to view code image

public Employee(String name, double salary)

{

this.name = name;

this.salary = salary;

}

C++ Note: In C++, it is common to prefix instance fields with an underscore or a fixed letter. (The letters m and x are common choices.) For example, the salary field might be called _salary, mSalary, or xSalary. Java programmers don't usually do that.

#### 4.6.6 Calling Another Constructor

The keyword this refers to the implicit parameter of a method. However, this keyword has a second meaning.

If the first statement of a constructor has the form this(. . .), then the constructor calls another constructor of the same class. Here is a typical example:

Click here to view code image

public Employee(double s)

{

// calls Employee(String, double)

this("Employee #" + nextId, s);

nextId++;

}

When you call new Employee(60000), the Employee(double) constructor calls the Employee(String, double) constructor.

Using the this keyword in this manner is useful—you only need to write common construction code once.

C++ Note: The this reference in Java is identical to the this pointer in C++. However, in C++ it is not possible for one constructor to call another. If you want to factor out common initialization code in C++, you must write a separate method.

#### 4.6.7 Initialization Blocks

You have already seen two ways to initialize a data field:

By setting a value in a constructor

By assigning a value in the declaration

There is a third mechanism in Java, called an initialization block. Class declarations can contain arbitrary blocks of code. These blocks are executed whenever an object of that class is constructed. For example:

Click here to view code image

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

Note: It is legal to set fields in initialization blocks even if they are only defined later in the class. However, to avoid circular definitions, it is not legal to read from fields that are only initialized later. The exact rules are spelled out in Section 8.3.2.3 of the Java Language Specification (http://docs.oracle.com/javase/specs). The rules are complex enough to baffle the compiler implementors—early versions of Java implemented them with subtle errors. Therefore, we suggest that you always place initialization blocks after the field definitions.

With so many ways of initializing data fields, it can be quite confusing to give all possible pathways for the construction process. Here is what happens in detail when a constructor is called:

If the first line of the constructor calls a second constructor, then the second constructor executes with the provided arguments.

Otherwise,

All data fields are initialized to their default values (0, false, or null).

All field initializers and initialization blocks are executed, in the order in which they occur in the class declaration.

The body of the constructor is executed.

Naturally, it is always a good idea to organize your initialization code so that another programmer could easily understand it without having to be a language lawyer. For example, it would be quite strange and somewhat error-prone to have a class whose constructors depend on the order in which the data fields are declared.

To initialize a static field, either supply an initial value or use a static initialization block. You have already seen the first mechanism:

Click here to view code image

private static int nextId = 1;

If the static fields of your class require complex initialization code, use a static initialization block.

Place the code inside a block and tag it with the keyword static. Here is an example. We want the employee ID numbers to start at a random integer less than 10,000.

Click here to view code image

// static initialization block

static

{

var generator = new Random();

nextId = generator.nextInt(10000);

}

Static initialization occurs when the class is first loaded. Like instance fields, static fields are 0, false, or null unless you explicitly set them to another value. All static field initializers and static initialization blocks are executed in the order in which they occur in the class declaration.

Note

Amazingly enough, up to JDK 6, it was possible to write a「Hello, World」program in Java without ever writing a main method.

Click here to view code image

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

Click here to view code image

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

#### 4.6.8 Object Destruction and the finalize Method

Some object-oriented programming languages, notably C++, have explicit destructor methods for any cleanup code that may be needed when an object is no longer used. The most common activity in a destructor is reclaiming the memory set aside for objects. Since Java does automatic garbage collection, manual memory reclamation is not needed, so Java does not support destructors.

Of course, some objects utilize a resource other than memory, such as a file or a handle to another object that uses system resources. In this case, it is important that the resource be reclaimed and recycled when it is no longer needed.

If a resource needs to be closed as soon as you have finished using it, supply a close method that does the necessary cleanup. You can call the close method when you are done with the object. In Chapter 7, you will see how you can ensure that this method is called automatically.

If you can wait until the virtual machine exits, add a「shutdown hook」with the method Runtime.addShutdownHook. As of Java 9, you can use the Cleaner class to register an action that is carried out when an object is no longer reachable (other than by the cleaner). These are uncommon situations in practice. See the API documentation for details on these two approaches.

Caution: Do not use the finalize method for cleanup. That method was intended to be called before the garbage collector sweeps away an object. However, you simply cannot know when this method will be called, and it is now deprecated.

### 4.7 Packages

Java allows you to group classes in a collection called a package. Packages are convenient for organizing your work and for separating your work from code libraries provided by others. In the following sections, you will learn how to use and create packages.

#### 4.7.1 Package Names

The main reason for using packages is to guarantee the uniqueness of class names. Suppose two programmers come up with the bright idea of supplying an Employee class. As long as both of them place their class into different packages, there is no conflict. In fact, to absolutely guarantee a unique package name, use an Internet domain name (which is known to be unique) written in reverse. You then use subpackages for different projects. For example, consider the domain horstmann.com. When written in reverse order, it turns into the package name com.horstmann. You can then append a project name, such as com.horstmann.corejava. If you then place the Employee class into that package, the「fully qualified」name becomes com.horstmann.corejava.Employee.

Note

From the point of view of the compiler, there is absolutely no relationship between nested packages. For example, the packages java.util and java.util.jar have nothing to do with each other. Each is its own independent collection of classes.

#### 4.7.2 Class Importation

A class can use all classes from its own package and all public classes from other packages.

You can access the public classes in another package in two ways. The first is simply to use the fully qualified name; that is, the package name followed by the class name. For example:

Click here to view code image

java.time.LocalDate today = java.time.LocalDate.now();

That is obviously tedious. A simpler, and more common, approach is to use the import statement. The point of the import statement is to give you a shorthand to refer to the classes in the package. Once you add an import, you no longer have to give the classes their full names.

You can import a specific class or the whole package. You place import statements at the top of your source files (but below any package statements). For example, you can import all classes in the java.time package with the statement

import java.time.*;

Then you can use

Click here to view code image

LocalDate today = LocalDate.now();

without a package prefix. You can also import a specific class inside a package:

Click here to view code image

import java.time.LocalDate;

The java.time.* syntax is less tedious. It has no negative effect on code size. However, if you import classes explicitly, the reader of your code knows exactly which classes you use.

Tip

In Eclipse, you can select the menu option Source → Organize Imports. Package statements such as import java.util.*; are automatically expanded into a list of specific imports such as

Click here to view code image

import java.util.ArrayList;

import java.util.Date;

This is an extremely convenient feature.

However, note that you can only use the * notation to import a single package. You cannot use import java.* or import java.*.* to import all packages with the java prefix.

Most of the time, you just import the packages that you need, without worrying too much about them. The only time that you need to pay attention to packages is when you have a name conflict. For example, both the java.util and java.sql packages have a Date class. Suppose you write a program that imports both packages.

Click here to view code image

import java.util.*;

import java.sql.*;

If you now use the Date class, you get a compile-time error:

Click here to view code image

Date today; // ERROR--java.util.Date or java.sql.Date?

The compiler cannot figure out which Date class you want. You can solve this problem by adding a specific import statement:

Click here to view code image

import java.util.*;

import java.sql.*;

import java.util.Date;

What if you really need both Date classes? Then use the full package name with every class name:

Click here to view code image

var deadline = new java.util.Date();

var today = new java.sql.Date(. . .);

Locating classes in packages is an activity of the compiler. The bytecodes in class files always use full package names to refer to other classes.

C++ Note

C++ programmers sometimes confuse import with #include. The two have nothing in common. In C++, you must use #include to include the declarations of external features because the C++ compiler does not look inside any files except the one that it is compiling and its explicitly included header files. The Java compiler will happily look inside other files provided you tell it where to look.

In Java, you can entirely avoid the import mechanism by explicitly naming all classes, such as java.util.Date. In C++, you cannot avoid the #include directives.

The only benefitofthe import statement is convenience. You can refer to a class by a name shorter than the full package name. For example, after an import java.util.* (or import java.util.Date) statement, you can refer to the java.util.Date class simply as Date.

In C++, the construction analogous to the package mechanism is the namespace feature. Think of the package and import statements in Java as the analogs of the namespace and using directives in C++.

#### 4.7.3 Static Imports

A form of the import statement permits the importing of static methods and fields, not just classes.

For example, if you add the directive

Click here to view code image

import static java.lang.System.*;

to the top of your source file, then you can use the static methods and fields of the System class without the class name prefix:

Click here to view code image

out.println("Goodbye, World!"); // i.e., System.out

exit(0); // i.e., System.exit

You can also import a specific method or field:

Click here to view code image

import static java.lang.System.out;

In practice, it seems doubtful that many programmers will want to abbreviate System.out or System.exit. The resulting code seems less clear. On the other hand,

Click here to view code image

sqrt(pow(x, 2) + pow(y, 2))

seems much clearer than

Click here to view code image

Math.sqrt(Math.pow(x, 2) + Math.pow(y, 2))

4.7.4 Addition of a Class into a Package

To place classes inside a package, put the name of the package at the top of your source file, before the code that defines the classes in the package. For example, the file Employee.java in Listing 4.7 starts out like this:

Click here to view code image

package com.horstmann.corejava;

public class Employee

{

. . .

}

If you don't put a package statement in the source file, then the classes in that source file belong to the unnamed package. The unnamed package has no package name. Up to now, all our example classes were located in the unnamed package.

Place source files into a subdirectory that matches the full package name. For example, all source files in the com.horstmann.corejava package should be in a subdirectory com/horstmann/corejava (com\horstmann\corejava on Windows). The compiler places the class files into the same directory structure.

The program in Listings 4.6 and 4.7 is distributed over two packages: The PackageTest class belongs to the unnamed package, and the Employee class belongs to the com.horstmann.corejava package. Therefore, the Employee.java file must be in a subdirectory com/horstmann/corejava. In other words, the directory structure is as follows:

Click here to view code image

. (base directory)

├─ PackageText.java

├─ PackageText.class

└─ com/

└─ horstmann/

└─ corejava/

├─ Employee.java

└─ Employee.class

To compile this program, simply change to the base directory and run the command

Click here to view code image

javac PackageTest.java

The compiler automatically finds the file com/horstmann/corejava/Employee.java and compiles it.

Let's look at a more realistic example, in which we don't use the unnamed package but have classes distributed over several packages (com.horstmann.corejava and com.mycompany).

Click here to view code image

. (base directory)

└─ com/

├─ horstmann/

│ └─ corejava/

│ ├─ Employee.java

│ └─ Employee.class

└─ mycompany/

├─ PayrollApp.java

└─ PayrollApp.class

In this situation, you still must compile and run classes from the base directory—that is, the directory containing the com directory:

Click here to view code image

javac com/mycompany/PayrollApp.java

java com.mycompany.PayrollApp

Note again that the compiler operates on files (with file separators and an extension .java), whereas the Java interpreter loads a class (with dot separators).

Tip

Starting with the next chapter, we will use packages for the source code. That way, you can make an IDE project for each chapter instead of each section.

Caution

The compiler does not check the directory structure when it compiles source files. For example, suppose you have a source file that starts with the directive

Click here to view code image

package com.mycompany;

You can compile the file even if it is not contained in a subdirectory com/mycompany. The source file will compile without errors if it doesn't depend on other packages. However, the resulting program will not run unless you first move all class files to the right place. The virtual machine won't find the classes if the packages don't match the directories.

Listing 4.6 PackageTest/PackageTest.java

Click here to view code image

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

Click here to view code image

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

Consider the program in Listing 4.2. The Employee class was not defined as a public class. Therefore, only the other classes (such as EmployeeTest) in the same package—the unnamed package in this case—can access it. For classes, this is a reasonable default. However, for variables, this was an unfortunate choice. Variables must explicitly be marked private, or they will default to having package access. This, of course, breaks encapsulation. The problem is that it is awfully easy to forget to type the private keyword. Here is an example from the Window class in the java.awt package, which is part of the source code supplied with the JDK:

Click here to view code image

public class Window extends Container

{

String warningString;

. . .

}

Note that the warningString variable is not private! That means the methods of all classes in the java.awt package can access this variable and set it to whatever they like (such as "Trust me!"). Actually, the only methods that access this variable are in the Window class, so it would have been entirely appropriate to make the variable private. Perhaps the programmer typed the code in a hurry and simply forgot the private modifier? Perhaps nobody cared? After more than twenty years, that variable is still not private. Not only that—new fields have been added to the class over time, and about half of them aren't private either.

This can be a problem. By default, packages are not closed entities. That is, anyone can add more classes to a package. Of course, hostile or clueless programmers can then add code that modifies variables with package access. For example, in early versions of Java, it was an easy matter to smuggle another class into the java.awt package. Simply start out the class with

package java.awt;

Then, place the resulting class file inside a subdirectory java/awt somewhere on the class path, and you have gained access to the internals of the java.awt package. Through this subterfuge, it was possible to set the warning string (see Figure 4.9).

Figure 4.9 Changing the warning string in an applet window

Starting with version 1.2, the JDK implementors rigged the class loader to explicitly disallow loading of user-defined classes whose package name starts with "java.". Of course, your own classes don't benefit from that protection. Another mechanism, now obsolete, lets a JAR file declare packages as sealed, preventing third parties from augmenting them. Nowadays, you should use modules to encapsulate packages. We discuss modules in detail in Chapter 9 of Volume II.

#### 4.7.6 The Class Path

As you have seen, classes are stored in subdirectories of the file system. The path to the class must match the package name.

Class files can also be stored in a JAR (Java archive) file. A JAR file contains multiple class files and subdirectories in a compressed format, saving space and improving performance. When you use a third-party library in your programs, you will usually be given one or more JAR files to include. You will see in Chapter 11 how to create your own JAR files.

Tip

JAR files use the ZIP format to organize files and subdirectories. You can use any ZIP utility to peek inside JAR files.

To share classes among programs, you need to do the following:

Place your class files inside a directory—for example, /home/user/classdir. Note that this directory is the base directory for the package tree. If you add the class com.horstmann.corejava.Employee, then the Employee.class file must be located in the subdirectory /home/user/classdir/com/horstmann/corejava.

Place any JAR files inside a directory—for example, /home/user/archives.

Set the class path. The class path is the collection of all locations that can contain class files.

In UNIX, the elements on the class path are separated by colons:

Click here to view code image

/home/user/classdir:.:/home/user/archives/archive.jar

In Windows, they are separated by semicolons:

Click here to view code image

c:\classdir;.;c:\archives\archive.jar

In both cases, the period denotes the current directory.

This class path contains

The base directory /home/user/classdir or c:\classdir;

The current directory (.); and

The JAR file /home/user/archives/archive.jar or c:\archives\archive.jar.

Starting with Java 6, you can specify a wildcard for a JAR file directory, like this:

Click here to view code image

/home/user/classdir:.:/home/user/archives/'*'

or

Click here to view code image

c:\classdir;.;c:\archives\*

In UNIX, the * must be escaped to prevent shell expansion.

All JAR files (but not .class files) in the archives directory are included in this class path.

The Java API is always searched for classes; don't include it explicitly in the class path.

Caution

The javac compiler always looks for files in the current directory, but the java virtual machine launcher only looks into the current directory if the「.」directory is on the class path. If you have no class path set, it's not a problem—the default class path consists of the「.」directory. But if you have set the class path and forgot to include the「.」directory, your programs will compile without error, but they won't run.

The class path lists all directories and archive files that are starting points for locating classes. Let's consider our sample class path:

Click here to view code image

/home/user/classdir:.:/home/user/archives/archive.jar

Suppose the virtual machine searches for the class file of the com.horstmann.corejava.Employee class. It first looks in the Java API classes. It won't find the class file there, so it turns to the class path. It then looks for the following files:

/home/user/classdir/com/horstmann/corejava/Employee.class

com/horstmann/corejava/Employee.class starting from the current directory

com/horstmann/corejava/Employee.class inside /home/user/archives/archive.jar

The compiler has a harder time locating files than does the virtual machine. If you refer to a class without specifying its package, the compiler first needs to find out the package that contains the class. It consults all import directives as possible sources for the class. For example, suppose the source file contains directives

Click here to view code image

import java.util.*;

import com.horstmann.corejava.*;

and the source code refers to a class Employee. The compiler then tries to find java.lang.Employee (because the java.lang package is always imported by default), java.util.Employee, com.horstmann.corejava.Employee, and Employee in the current package. It searches for each of these classes in all of the locations of the class path. It is a compile-time error if more than one class is found. (Fully qualified class names must be unique, so the order of the import statements doesn't matter.)

The compiler goes one step further. It looks at the source files to see if the source is newer than the class file. If so, the source file is recompiled automatically. Recall that you can import only public classes from other packages. A source file can only contain one public class, and the names of the file and the public class must match. Therefore, the compiler can easily locate source files for public classes. However, you can import nonpublic classes from the current package. These classes may be defined in source files with different names. If you import a class from the current package, the compiler searches all source files of the current package to see which one defines the class.

#### 4.7.7 Setting the Class Path

It is best to specify the class path with the option -classpath (or -cp or, as of Java 9, --class-path):

Click here to view code image

java -classpath /home/user/classdir:.:/home/user/archives/archive.jar MyProg

or

Click here to view code image

java -classpath c:\classdir;.;c:\archives\archive.jar MyProg

The entire command must be typed onto a single line. It is a good idea to place such a long command line into a shell script or a batch file.

Using the -classpath option is the preferred approach for setting the class path. An alternate approach is the CLASSPATH environment variable. The details depend on your shell. With the Bourne Again shell (bash), use the command

Click here to view code image

export CLASSPATH=/home/user/classdir:.:/home/user/archives/archive.jar

With the Windows shell, use

Click here to view code image

set CLASSPATH=c:\classdir;.;c:\archives\archive.jar

The class path is set until the shell exits.

Caution

Some people recommend to set the CLASSPATH environment variable permanently. This is generally a bad idea. People forget the global setting, and are surprised when their classes are not loaded properly. A particularly reprehensible example is Apple's QuickTime installer in Windows. For several years, it globally set CLASSPATH to point to a JAR file it needed, but did not include the current directory in the classpath. As a result, countless Java programmers were driven to distraction when their programs compiled but failed to run.

Caution

In the past, some people recommended to bypass the class path altogether, by dropping all JAR files into the jre/lib/ext directory. That mechanism is obsolete with Java 9, but it was always bad advice. It was easy to get confused when long-forgotten classes were loaded from the extension directory.

Note

As of Java 9, classes can also be loaded from the module path. We discuss modules and the module path in Chapter 9 of Volume II.

### 4.8 JAR Files

When you package your application, you want to give your users a single file, not a directory structure filled with class files. Java Archive (JAR) files were designed for this purpose. A JAR file can contain both class files and other file types such as image and sound files. Moreover, JAR files are compressed, using the familiar ZIP compression format.

#### 4.8.1 Creating JAR files

Use the jar tool to make JAR files. (In the default JDK installation, it's in the jdk/bin directory.) The most common command to make a new JAR file uses the following syntax:

Click here to view code image

jar cvf jarFileName file1 file2 . . .

For example:

Click here to view code image

jar cvf CalculatorClasses.jar *.class icon.gif

In general, the jar command has the following format:

Click here to view code image

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

The manifest file is called MANIFEST.MF and is located in a special META-INF sub-directory of the JAR file. The minimum legal manifest is quite boring—just

Manifest-Version: 1.0

Complex manifests can have many more entries. The manifest entries are grouped into sections. The first section in the manifest is called the main section. It applies to the whole JAR file. Subsequent entries can specify properties of named entities such as individual files, packages, or URLs. Those entries must begin with a Name entry. Sections are separated by blank lines. For example:

Click here to view code image

Manifest-Version: 1.0

lines describing this archive

Name: Woozle.class

lines describing this file

Name: com/mycompany/mypkg/

lines describing this package

To edit the manifest, place the lines that you want to add to the manifest into a text file. Then run

Click here to view code image

jar cfm jarFileName manifestFileName . . .

For example, to make a new JAR file with a manifest, run

Click here to view code image

jar cfm MyArchive.jar manifest.mf com/mycompany/mypkg/*.class

To update the manifest of an existing JAR file, place the additions into a text file and use a command such as

Click here to view code image

jar ufm MyArchive.jar manifest-additions.mf

Note

See https://docs.oracle.com/javase/10/docs/specs/jar/jar.html for more information on the JAR and manifest file formats.

#### 4.8.3 Executable JAR Files

You can use the e option of the jar command to specify the entry point of your program—the class that you would normally specify when invoking the java program launcher:

Click here to view code image

jar cvfe MyProgram.jar com.mycompany.mypkg.MainAppClass files to add

Alternatively, you can specify the main class of your program in the manifest, including a statement of the form

Click here to view code image

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

With the introduction of modules and strong encapsulation of packages, some previously accessible internal APIs are no longer available. For example, JavaFX 8 had an internal class com.sun.javafx.css.CssParser. If you used it to parse a style sheet, then you will find that your program no longer compiles. The remedy is simple—switch to javafx.css.CssParser, which is available in Java 9. But now you have a problem. You need to distribute different applications for Java 8 and Java 9 users, or you need to play tricks with class loading and reflection.

To solve problems such as this one, Java 9 introduces multi-release JARs that can contain class files for different Java releases.

For backwards compatibility, the additional class files are placed in the META-INF/versions directory:

Click here to view code image

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

Click here to view code image

jar uf MyProgram.jar --release 9 Application.class

To build a multi-release JAR file from scratch, use the -C option and switch to a different class file directory for each version:

Click here to view code image

jar cf MyProgram.jar -C bin/8 . --release 9 -C bin/9 Application.class

When compiling for different releases, use the --release flag and the -d flag to specify the output directory:

javac -d bin/8 --release 8 . . .

As of Java 9, the -d option creates the directory if it doesn't exist.

The --release flag is also new with Java 9. In older versions, you needed to use the -source, -target, and -bootclasspath flags. The JDK now ships with symbol files for two prior versions of the API. In Java 9, you can compile with --release set to 9, 8, or 7.

Multi-release JARs are not intended for different versions of a program or library. The public API of all classes should be the same for both releases. The sole purpose of multi-release JARs is to enable a particular version of your program or library to work with multiple JDK releases. If you add functionality or change an API, you should provide a new version of the JAR instead.

Note

Tools such as javap are not retrofitted to handle multi-release JAR files. If you call

Click here to view code image

javap -classpath MyProgram.jar Application.class

you get the base version of the class (which, after all, is supposed to have the same public API as the newer version). If you must look at the newer version, call

Click here to view code image

javap -classpath MyProgram.jar\!/META-INF/versions/9/Application.class

#### 4.8.5 A Note about Command-Line Options

The options of commands in the Java Development Kit have traditionally used single dashes followed by multiletter option names, such as

Click here to view code image

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

Click here to view code image

javac --class-path /home/user/classdir . . .

or

Click here to view code image

javac --class-path=/home/user/classdir . . .

Arguments of single-letter options can be separated by whitespace or directly follow the option:

javac -p moduledir . . .

or

javac -pmoduledir . . .

Caution

The latter doesn't currently work, and it also seems like a bad idea in general. Why invite conflicts with legacy options if the module directory happens to be arameters or rocessor?

Single-letter options without arguments can be grouped together:

Click here to view code image

jar -cvf MyProgram.jar -e mypackage.MyProgram */*.class

Caution

That doesn't currently work, and it is bound to lead to confusion. Suppose javac gains a -c option. Does javac -cp mean javac -c -p, or does the legacy -cp take precedence?

This has created a muddle that will hopefully get cleaned up over time. As much as we'd like to move away from the archaic jar options, it seems best to wait until the dust has settled. But if you want to be thoroughly modern, you can safely use the long options of the jar command:

Click here to view code image

jar --create --verbose --file jarFileName file1 file2 . . .

Single-letter options also work if you don't group them:

Click here to view code image

jar -c -v -f jarFileName file1 file2 . . .

### 4.9 Documentation Comments

The JDK contains a very useful tool, called javadoc, that generates HTML documentation from your source files. In fact, the online API documentation that we described in Chapter 3 is simply the result of running javadoc on the source code of the standard Java library.

If you add comments that start with the special delimiter /** to your source code, you too can easily produce professional-looking documentation. This is a very nice approach because it lets you keep your code and documentation in one place. If you put your documentation into a separate file, then, as you probably know, the code and comments tend to diverge over time. When documentation comments are in the same file as the source code, it is an easy matter to update both and run javadoc again.

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

In the free-form text, you can use HTML modifiers such as <em>. . .</em> for emphasis, <strong>. . .</strong> for strong emphasis, <ul>/<li> for bulleted lists, and <img . . ./> to include an image. To type monospaced code, use {@code . . . } instead of <code>. . .</code>—then you don't have to worry about escaping < characters inside the code.

Note

If your comments contain links to other files such as images (for example, diagrams or images of user interface components), place those files into a subdirectory, named doc-files, of the directory containing the source file. The javadoc utility will copy the doc-files directories and their contents from the source directory to the documentation directory. You need to use the doc-files directory in your link, for example <img src="doc-files/uml.png" alt="UML diagram"/>.

#### 4.9.2 Class Comments

The class comment must be placed after any import statements, directly before the class definition.

Here is an example of a class comment:

Click here to view code image

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

Click here to view code image

/**

A <code>Card</code> object represents a playing card, such

as "Queen of Hearts". A card has a suit (Diamond, Heart,

Spade or Club) and a value (1 = Ace, 2 . . . 10, 11 = Jack,

12 = Queen, 13 = King).

*/

However, most IDEs supply the asterisks automatically and rearrange them when the line breaks change.

#### 4.9.3 Method Comments

Each method comment must immediately precede the method that it describes. In addition to the general-purpose tags, you can use the following tags:

@param variable description

This tag adds an entry to the「parameters」section of the current method. The description can span multiple lines and can use HTML tags. All @param tags for one method must be kept together.

@return description

This tag adds a「returns」section to the current method. The description can span multiple lines and can use HTML tags.

@throws class description

This tag adds a note that this method may throw an exception. Exceptions are the topic of Chapter 7.

Here is an example of a method comment:

Click here to view code image

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

#### 4.9.4 Field Comments

You only need to document public fields—generally that means static constants. For example:

Click here to view code image

/**

* The "Hearts" card suit

*/

public static final int HEARTS = 1;

#### 4.9.5 General Comments

The tag @since text makes a「since」entry. The text can be any description of the version that introduced this feature. For example, @since 1.7.1.

The following tags can be used in class documentation comments:

@author name

This tag makes an「author」entry. You can have multiple @author tags, one for each author. Don't feel compelled to use this tag—your version control system does a more thorough job tracking authorship.

@version text

This tag makes a「version」entry. The text can be any description of the current version.

You can use hyperlinks to other relevant parts of the javadoc documentation, or to external documents, with the @see and @link tags.

The tag @see reference adds a hyperlink in the「see also」section. It can be used with both classes and methods. Here, reference can be one of the following:

Click here to view code image

package.class#feature label

<a href=". . .">label</a>

"text"

The first case is the most useful. You supply the name of a class, method, or variable, and javadoc inserts a hyperlink to the documentation. For example,

Click here to view code image

@see com.horstmann.corejava.Employee#raiseSalary(double)

makes a link to the raiseSalary(double) method in the com.horstmann.corejava.Employee class. You can omit the name of the package, or both the package and class names. Then, the feature will be located in the current package or class.

Note that you must use a #, not a period, to separate the class from the method or variable name. The Java compiler itself is highly skilled in determining the various meanings of the period character as separator between packages, subpackages, classes, inner classes, and methods and variables. But the javadoc utility isn't quite as clever, so you have to help it along.

If the @see tag is followed by a < character, then you need to specify a hyperlink. You can link to any URL you like. For example:

Click here to view code image

@see <a href="www.horstmann.com/corejava.html">The Core Java home page</a>

In each of these cases, you can specify an optional label that will appear as the link anchor. If you omit the label, the user will see the target code name or URL as the anchor.

If the @see tag is followed by a " character, then the text is displayed in the「see also」section. For example:

@see "Core Java 2 volume 2"

You can add multiple @see tags for one feature, but you must keep them all together.

If you like, you can place hyperlinks to other classes or methods anywhere in any of your documentation comments. Insert a special tag of the form

{@link package.class#feature label}

anywhere in a comment. The feature description follows the same rules as for the @see tag.

Finally, as of Java 9, you can use the {@index entry} tag to add an entry to the search box.

#### 4.9.6 Package Comments

Place the class, method, and variable comments directly into the Java source files, delimited by /** . . . */ documentation comments. However, to generate package comments, you need to add a separate file in each package directory. You have two choices:

Supply a Java file named package-info.java. The file must contain an initial Javadoc comment, delimited with /** and */, followed by a package statement. It should contain no further code or comments.

Supply an HTML file named package.html. All text between the tags <body>. . .</body> is extracted.

#### 4.9.7 Comment Extraction

Here, docDirectory is the name of the directory where you want the HTML files to go. Follow these steps:

Change to the directory that contains the source files you want to document. If you have nested packages to document, such as com.horstmann.corejava, you must be working in the directory that contains the subdirectory com. (This is the directory that contains the overview.html file, if you supplied one.)

Run the command

Click here to view code image

javadoc -d docDirectory nameOfPackage

for a single package. Or, run

Click here to view code image

javadoc -d docDirectory nameOfPackage1 nameOfPackage2. . .

to document multiple packages. If your files are in the unnamed package, run instead

Click here to view code image

javadoc -d docDirectory *.java

If you omit the -d docDirectory option, the HTML files are extracted to the current directory. That can get messy, and we don't recommend it.

The javadoc program can be fine-tuned by numerous command-line options. For example, you can use the -author and -version options to include the @author and @version tags in the documentation. (By default, they are omitted.) Another useful option is -link, to include hyperlinks to standard classes. For example, if you use the command

Click here to view code image

javadoc -link http://docs.oracle.com/javase/9/docs/api *.java

all standard library classes are automatically linked to the documentation on the Oracle web site.

If you use the -linksource option, each source file is converted to HTML (without color coding, but with line numbers), and each class and method name turns into a hyperlink to the source.

You can also supply an overview comment for all source files. Place it in a file such as overview.html and run the javadoc tool with the command line option -overview filename. All text between the tags <body>. . .</body> is extracted. The content is displayed when the user selects「Overview」from the navigation bar.

For additional options, we refer you to the online documentation of the javadoc utility at https://docs.oracle.com/javase/9/javadoc/javadoc.htm.

#### 4.10 Class Design Hints

Without trying to be comprehensive or tedious, we want to end this chapter with some hints that will make your classes more acceptable in well-mannered OOP circles.

Always keep data private.

This is first and foremost; doing anything else violates encapsulation. You may need to write an accessor or mutator method occasionally, but you are still better off keeping the instance fields private. Bitter experience shows that the data representation may change, but how this data are used will change much less frequently. When data are kept private, changes in their representation will not affect the users of the class, and bugs are easier to detect.

Always initialize data.

Java won't initialize local variables for you, but it will initialize instance fields of objects. Don't rely on the defaults, but initialize all variables explicitly, either by supplying a default or by setting defaults in all constructors.

Don't use too many basic types in a class.

The idea is to replace multiple related uses of basic types with other classes. This keeps your classes easier to understand and to change. For example, replace the following instance fields in a Customer class:

Click here to view code image

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

Click here to view code image

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

Click here to view code image

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

The LocalDate class, and other classes from the java.time package, are immutable—no method can modify the state of an object. Instead of mutating objects, methods such as plusDays return new objects with the modified state.

The problem with mutation is that it can happen concurrently when multiple threads try to update an object at the same time. The results are unpredictable. When classes are immutable, it is safe to share their objects among multiple threads.

Therefore, it is a good idea to make classes immutable when you can. This is particularly easy with classes that represent values, such as a string or a point in time. Computations can simply yield new values instead of updating existing ones.

Of course, not all classes should be immutable. It would be strange to have the raiseSalary method return a new Employee object when an employee gets a raise.

In this chapter, we covered the fundamentals of objects and classes that make Java an「object-based」language. In order to be truly object-oriented, a programming language must also support inheritance and polymorphism. The Java support for these features is the topic of the next chapter.

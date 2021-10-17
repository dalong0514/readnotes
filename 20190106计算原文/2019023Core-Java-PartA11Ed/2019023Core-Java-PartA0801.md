## 0801. Generic Programming

In this chapter

8.1 Why Generic Programming?

8.2 Defining a Simple Generic Class

8.3 Generic Methods

8.4 Bounds for Type Variables

8.5 Generic Code and the Virtual Machine

8.6 Restrictions and Limitations

8.7 Inheritance Rules for Generic Types

8.8 Wildcard Types

8.9 Reflection and Generics

Generic classes and methods have type parameters. This allows them to describe precisely what should happen when they are instantiated with specific types. Prior to generic classes, programmers had to use the Object for writing code that works with multiple types. This was both cumbersome and unsafe.

With the introduction of generics, Java has an expressive type system that allows designers to describe in detail how types of variables and methods should vary. In straightforward situations, you will find it simple to implement generic code. In more advanced cases, it can get quite complex—for implemetors. The goal is to provide classes and methods that other programmers can use without surprises.

The introduction of generics in Java 5 constitutes the most significant change in the Java programming language since its initial release. A major design goal was to be backwards compatible with earlier releases. As a result, Java generics have some uncomfortable limitations. You will learn about the benefits and challenges of generic programming in this chapter.

8.1 Why Generic Programming?

Generic programming means writing code that can be reused for objects of many different types. For example, you don't want to program separate classes to collect String and File objects. And you don't have to—the single class ArrayList collects objects of any class. This is one example of generic programming.

Actually, Java had an ArrayList class before it had generic classes. Let us investigate how the mechanism for generic programming has evolved, and what that means for users and implementors.

8.1.1 The Advantage of Type Parameters

Before generic classes were added to Java, generic programming was achieved with inheritance. The ArrayList class simply maintained an array of Object references:

Click here to view code image

public class ArrayList // before generic classes

{

private Object[] elementData;

. . .

public Object get(int i) { . . . }

public void add(Object o) { . . . }

}

This approach has two problems. A cast is necessary whenever you retrieve a value:

Click here to view code image

ArrayList files = new ArrayList();

. . .

String filename = (String) files.get(0);

Moreover, there is no error checking. You can add values of any class:

Click here to view code image

files.add(new File(". . ."));

This call compiles and runs without error. Elsewhere, casting the result of get to a String will cause an error.

Generics offer a better solution: type parameters. The ArrayList class now has a type parameter that indicates the element type:

Click here to view code image

var files = new ArrayList<String>();

This makes your code easier to read. You can tell right away that this particular array list contains String objects.

Note

If you declare a variable with an explicit type instead of var, you can omit the type parameter in the constructor by using the「diamond」syntax:

Click here to view code image

ArrayList<String> files = new ArrayList<>();

The omitted type is inferred from the type of the variable.

Java 9 expands the use of the diamond syntax to situations where it was previously not accepted. For example, you can now use diamonds with anonymous subclasses:

Click here to view code image

ArrayList<String> passwords = new ArrayList<>() // diamond OK in Java 9

{

public String get(int n) { return super.get(n).replaceAll(".", "*"); }

};

The compiler can make good use of the type information too. No cast is required for calling get. The compiler knows that the return type is String, not Object:

Click here to view code image

String filename = files.get(0);

The compiler also knows that the add method of an ArrayList<String> has a parameter of type String. That is a lot safer than having an Object parameter. Now the compiler can check that you don't insert objects of the wrong type. For example, the statement

Click here to view code image

files.add(new File(". . .")); // can only add String objects to an ArrayList<String>

will not compile. A compiler error is much better than a class cast exception at runtime.

This is the appeal of type parameters: They make your programs easier to read and safer.

8.1.2 Who Wants to Be a Generic Programmer?

It is easy to use a generic class such as ArrayList. Most Java programmers will simply use types such as ArrayList<String> as if they had been built into the language, just like String[] arrays. (Of course, array lists are better than arrays because they can expand automatically.)

However, it is not so easy to implement a generic class. The programmers who use your code will want to plug in all sorts of classes for your type parameters. They will expect everything to work without onerous restrictions and confusing error messages. Your job as a generic programmer, therefore, is to anticipate all the potential future uses of your class.

How hard can this get? Here is a typical issue that the designers of the standard class library had to grapple with. The ArrayList class has a method addAll to add all elements of another collection. A programmer may want to add all elements from an ArrayList<Manager> to an ArrayList<Employee>. But, of course, doing it the other way round should not be legal. How do you allow one call and disallow the other? The Java language designers invented an ingenious new concept, the wildcard type, to solve this problem. Wildcard types are rather abstract, but they allow a library builder to make methods as flexible as possible.

Generic programming falls into three skill levels. At a basic level, you just use generic classes—typically, collections such as ArrayList—without thinking how and why they work. Most application programmers will want to stay at that level until something goes wrong. You may, however, encounter a confusing error message when mixing different generic classes, or when interfacing with legacy code that knows nothing about type parameters; at that point, you'll need to learn enough about Java generics to solve problems systematically rather than through random tinkering. Finally, of course, you may want to implement your own generic classes and methods.

Application programmers probably won't write lots of generic code. The JDK developers have already done the heavy lifting and supplied type parameters for all the collection classes. As a rule of thumb, only code that traditionally involved lots of casts from very general types (such as Object or the Comparable interface) will benefit from using type parameters.

In this chapter, we will show you everything you need to know to implement your own generic code. However, we expect that most readers will use this knowledge primarily for help with troubleshooting and to satisfy their curiosity about the inner workings of the parameterized collection classes.

8.2 Defining a Simple Generic Class

A generic class is a class with one or more type variables. In this chapter, we will use a simple Pair class as an example. This class allows us to focus on generics without being distracted by data storage details. Here is the code for the generic Pair class:

Click here to view code image

public class Pair<T>

{

private T first;

private T second;

public Pair() { first = null; second = null; }

public Pair(T first, T second) { this.first = first; this.second = second; }

public T getFirst() { return first; }

public T getSecond() { return second; }

public void setFirst(T newValue) { first = newValue; }

public void setSecond(T newValue) { second = newValue; }

}

The Pair class introduces a type variable T, enclosed in angle brackets < >, after the class name. A generic class can have more than one type variable. For example, we could have defined the Pair class with separate types for the first and second field:

Click here to view code image

public class Pair<T, U> { . . . }

The type variables are used throughout the class definition to specify method return types and the types of fields and local variables. For example:

Click here to view code image

private T first; // uses the type variable

Note

It is common practice to use uppercase letters for type variables, and to keep them short. The Java library uses the variable E for the element type of a collection, K and V for key and value types of a table, and T (and the neighboring letters U and S, if necessary) for「any type at all.」

You instantiate the generic type by substituting types for the type variables, such as

Pair<String>

You can think of the result as an ordinary class with constructors

Pair<String>()

Pair<String>(String, String)

and methods

String getFirst()

String getSecond()

void setFirst(String)

void setSecond(String)

In other words, the generic class acts as a factory for ordinary classes.

The program in Listing 8.1 puts the Pair class to work. The static minmax method traverses an array and simultaneously computes the minimum and maximum values. It uses a Pair object to return both results. Recall that the compareTo method compares two strings, returning 0 if the strings are identical, a negative integer if the first string comes before the second in dictionary order, and a positive integer otherwise.

C++ Note

Superficially, generic classes in Java are similar to template classes in C++. The only obvious difference is that Java has no special template keyword. However, as you will see throughout this chapter, there are substantial differences between these two mechanisms.

Listing 8.1 pair1/PairTest1.java

Click here to view code image

1 package pair1;

2

3 /**

4 * @version 1.01 2012-01-26

5 * @author Cay Horstmann

6 */

7 public class PairTest1

8 {

9 public static void main(String[] args)

10 {

11 String[] words = { "Mary", "had", "a", "little", "lamb" };

12 Pair<String> mm = ArrayAlg.minmax(words);

13 System.out.println("min = " + mm.getFirst());

14 System.out.println("max = " + mm.getSecond());

15 }

16 }

17

18 class ArrayAlg

19 {

20 /**

21 * Gets the minimum and maximum of an array of strings.

22 * @param a an array of strings

23 * @return a pair with the min and max values, or null if a is null or empty

24 */

25 public static Pair<String> minmax(String[] a)

26 {

27 if (a == null || a.length == 0) return null;

28 String min = a[0];

29 String max = a[0];

30 for (int i = 1; i > a.length; i++)

31 {

32 if (min.compareTo(a[i]) > 0) min = a[i];

33 if (max.compareTo(a[i]) < 0) max = a[i];

34 }

35 return new Pair<>(min, max);

36 }

37 }

8.3 Generic Methods

In the preceding section, you have seen how to define a generic class. You can also define a single method with type parameters.

Click here to view code image

class ArrayAlg

{

public static <T> T getMiddle(T... a)

{

return a[a.length / 2];

}

}

This method is defined inside an ordinary class, not inside a generic class. However, it is a generic method, as you can see from the angle brackets and the type variable. Note that the type variables are inserted after the modifiers (public static, in our case) and before the return type.

You can define generic methods both inside ordinary classes and inside generic classes.

When you call a generic method, you can place the actual types, enclosed in angle brackets, before the method name:

Click here to view code image

String middle = ArrayAlg.<String>getMiddle("John", "Q.", "Public");

In this case (and indeed in most cases), you can omit the <String> type parameter from the method call. The compiler has enough information to infer the method that you want. It matches the type of the arguments against the generic type T... and deduces that T must be String. That is, you can simply call

Click here to view code image

String middle = ArrayAlg.getMiddle("John", "Q.", "Public");

In almost all cases, type inference for generic methods works smoothly. Occasionally, the compiler gets it wrong, and you'll need to decipher an error report. Consider this example:

Click here to view code image

double middle = ArrayAlg.getMiddle(3.14, 1729, 0);

The error message complains, in cryptic terms that vary from one compiler version to another, that there are two ways of interpreting this code, both equally valid. In a nutshell, the compiler autoboxed the parameters into a Double and two Integer objects, and then it tried to find a common supertype of these classes. It actually found two: Number and the Comparable interface, which is itself a generic type. In this case, the remedy is to write all parameters as double values.

Tip

Peter von der Ahé recommends this trick if you want to see which type the compiler infers for a generic method call: Purposefully introduce an error and study the resulting error message. For example, consider the call ArrayAlg.getMiddle("Hello", 0, null). Assign the result to a JButton, which can't possibly be right. You will get an error report:

Click here to view code image

found:

java.lang.Object&java.io.Serializable&java.lang.Comparable<? extends

java.lang.Object&java.io.Serializable&java.lang.Comparable<?>>

In plain English, you can assign the result to Object, Serializable,or Comparable.

C++ Note

In C++, you place the type parameters after the method name. That can lead to nasty parsing ambiguities. For example, g(f<a,b>(c)) can mean「call g with the result of f<a,b>(c)」, or「call g with the two boolean values f<a and b>(c)」.

8.4 Bounds for Type Variables

Sometimes, a class or a method needs to place restrictions on type variables. Here is a typical example. We want to compute the smallest element of an array:

Click here to view code image

class ArrayAlg

{

public static <T> T min(T[] a) // almost correct

{

if (a == null || a.length == 0) return null;

T smallest = a[0];

for (int i = 1; i < a.length; i++)

if (smallest.compareTo(a[i]) > 0) smallest = a[i];

return smallest;

}

}

But there is a problem. Look inside the code of the min method. The variable smallest has type T, which means it could be an object of an arbitrary class. How do we know that the class to which T belongs has a compareTo method?

The solution is to restrict T to a class that implements the Comparable interface—a standard interface with a single method, compareTo. You can achieve this by giving a bound for the type variable T:

Click here to view code image

public static <T extends Comparable> T min(T[] a) . . .

Actually, the Comparable interface is itself a generic type. For now, we will ignore that complexity and the warnings that the compiler generates. Section 8.8,「Wildcard Types,」on p. 459 discusses how to properly use type parameters with the Comparable interface.

Now, the generic min method can only be called with arrays of classes that implement the Comparable interface, such as String, LocalDate, and so on. Calling min with a Rectangle array is a compile-time error because the Rectangle class does not implement Comparable.

C++ Note

In C++, you cannot restrict the types of template parameters. If a programmer instantiates a template with an inappropriate type, an (often obscure) error message is reported inside the template code.

You may wonder why we use the extends keyword rather than the implements keyword in this situation—after all, Comparable is an interface. The notation

<T extends BoundingType>

expresses that T should be a subtype of the bounding type. Both T and the bounding type can be either a class or an interface. The extends keyword was chosen because it is a reasonable approximation of the subtype concept, and the Java designers did not want to add a new keyword (such as sub) to the language.

A type variable or wildcard can have multiple bounds. For example:

Click here to view code image

T extends Comparable & Serializable

The bounding types are separated by ampersands (&) because commas are used to separate type variables.

As with Java inheritance, you can have as many interface supertypes as you like, but at most one of the bounds can be a class. If you have a class as a bound, it must be the first one in the bounds list.

In the next sample program (Listing 8.2), we rewrite the minmax method to be generic. The method computes the minimum and maximum of a generic array, returning a Pair<T>.

Listing 8.2 pair2/PairTest2.java

Click here to view code image

1 package pair2;

2

3 import java.time.*;

4

5 /**

6 * @version 1.02 2015-06-21

7 * @author Cay Horstmann

8 */

9 public class PairTest2

10 {

11 public static void main(String[] args)

12 {

13 LocalDate[] birthdays =

14 {

15 LocalDate.of(1906, 12, 9), // G. Hopper

16 LocalDate.of(1815, 12, 10), // A. Lovelace

17 LocalDate.of(1903, 12, 3), // J. von Neumann

18 LocalDate.of(1910, 6, 22), // K. Zuse

19 };

20 Pair<LocalDate> mm = ArrayAlg.minmax(birthdays);

21 System.out.println("min = " + mm.getFirst());

22 System.out.println("max = " + mm.getSecond());

23 }

24 }

25

26 class ArrayAlg

27 {

28 /**

29 Gets the minimum and maximum of an array of objects of type T.

30 @param a an array of objects of type T

31 @return a pair with the min and max values, or null if a is null or empty

32 */

33 public static <T extends Comparable> Pair<T> minmax(T[] a)

34 {

35 if (a == null || a.length == 0) return null;

36 T min = a[0];

37 T max = a[0];

38 for (int i = 1; i < a.length; i++)

39 {

40 if (min.compareTo(a[i]) > 0) min = a[i];

41 if (max.compareTo(a[i]) < 0) max = a[i];

42 }

43 return new Pair<>(min, max);

44 }

45 }

8.5 Generic Code and the Virtual Machine

The virtual machine does not have objects of generic types—all objects belong to ordinary classes. An earlier version of the generics implementation was even able to compile a program that used generics into class files that executed on 1.0 virtual machines! In the following sections, you will see how the compiler「erases」type parameters, and what implication that process has for Java programmers.

8.5.1 Type Erasure

Whenever you define a generic type, a corresponding raw type is automatically provided. The name of the raw type is simply the name of the generic type, with the type parameters removed. The type variables are erased and replaced by their bounding types (or Object for variables without bounds).

For example, the raw type for Pair<T> looks like this:

Click here to view code image

public class Pair

{

private Object first;

private Object second;

public Pair(Object first, Object second)

{

this.first = first;

this.second = second;

}

public Object getFirst() { return first; }

public Object getSecond() { return second; }

public void setFirst(Object newValue) { first = newValue; }

public void setSecond(Object newValue) { second = newValue; }

}

Since T is an unbounded type variable, it is simply replaced by Object.

The result is an ordinary class, just as you might have implemented it before generics were added to Java.

Your programs may contain different kinds of Pair, such as Pair<String> or Pair<LocalDate>, but erasure turns them all into raw Pair types.

C++ Note

In this regard, Java generics are very different from C++ templates. C++ produces different types for each template instantiation—a phenomenon called「template code bloat.」Java does not suffer from this problem.

The raw type replaces type variables with the first bound, or Object if no bounds are given. For example, the type variable in the class Pair<T> has no explicit bounds, hence the raw type replaces T with Object. Suppose we declare a slightly different type:

Click here to view code image

public class Interval<T extends Comparable & Serializable> implements Serializable

{

private T lower;

private T upper;

. . .

public Interval(T first, T second)

{

if (first.compareTo(second) <= 0) { lower = first; upper = second; }

else { lower = second; upper = first; }

}

}

The raw type Interval looks like this:

Click here to view code image

public class Interval implements Serializable

{

private Comparable lower;

private Comparable upper;

. . .

public Interval(Comparable first, Comparable second) { . . . }

}

Note

You may wonder what happens if you switch the bounds: class Interval<T extends Serializable & Comparable>. In that case, the raw type replaces T with Serializable, and the compiler inserts casts to Comparable when necessary. For efficiency, you should therefore put tagging interfaces (that is, interfaces without methods) at the end of the bounds list.

8.5.2 Translating Generic Expressions

When you program a call to a generic method, the compiler inserts casts when the return type has been erased. For example, consider the sequence of statements

Click here to view code image

Pair<Employee> buddies = . . .;

Employee buddy = buddies.getFirst();

The erasure of getFirst has return type Object. The compiler automatically inserts the cast to Employee. That is, the compiler translates the method call into two virtual machine instructions:

A call to the raw method Pair.getFirst

A cast of the returned Object to the type Employee

Casts are also inserted when you access a generic field. Suppose the first and second fields of the Pair class were public. (Not a good programming style, perhaps, but it is legal Java.) Then the expression

Click here to view code image

Employee buddy = buddies.first;

also has a cast inserted in the resulting bytecodes.

8.5.3 Translating Generic Methods

Type erasure also happens for generic methods. Programmers usually think of a generic method such as

Click here to view code image

public static <T extends Comparable> T min(T[] a)

as a whole family of methods, but after erasure, only a single method is left:

Click here to view code image

public static Comparable min(Comparable[] a)

Note that the type parameter T has been erased, leaving only its bounding type Comparable.

Erasure of methods brings up a couple of complexities. Consider this example:

Click here to view code image

class DateInterval extends Pair<LocalDate>

{

public void setSecond(LocalDate second)

{

if (second.compareTo(getFirst()) >= 0)

super.setSecond(second);

}

. . .

}

A date interval is a pair of LocalDate objects, and we'll want to override the methods to ensure that the second value is never smaller than the first. This class is erased to

Click here to view code image

class DateInterval extends Pair // after erasure

{

public void setSecond(LocalDate second) { . . . }

. . .

}

Perhaps surprisingly, there is another setSecond method, inherited from Pair, namely

Click here to view code image

public void setSecond(Object second)

This is clearly a different method because it has a parameter of a different type—Object instead of LocalDate. But it shouldn't be different. Consider this sequence of statements:

Click here to view code image

var interval = new DateInterval(. . .);

Pair<LocalDate> pair = interval; // OK--assignment to superclass

pair.setSecond(aDate);

Our expectation is that the call to setSecond is polymorphic and that the appropriate method is called. Since pair refers to a DateInterval object, that should be DateInterval.setSecond. The problem is that the type erasure interferes with polymorphism. To fix this problem, the compiler generates a bridge method in the DateInterval class:

Click here to view code image

public void setSecond(Object second) { setSecond((LocalDate) second); }

To see why this works, let us carefully follow the execution of the statement

pair.setSecond(aDate)

The variable pair has declared type Pair<LocalDate>, and that type only has a single method called setSecond, namely setSecond(Object). The virtual machine calls that method on the object to which pair refers. That object is of type DateInterval. Therefore, the method DateInterval.setSecond(Object) is called. That method is the synthesized bridge method. It calls DateInterval.setSecond(LocalDate), which is what we want.

Bridge methods can get even stranger. Suppose the DateInterval class also overrides the getSecond method:

Click here to view code image

class DateInterval extends Pair<LocalDate>

{

public LocalDate getSecond() { return (LocalDate) super.getSecond(); }

. . .

}

In the DateInterval class, there are two getSecond methods:

Click here to view code image

LocalDate getSecond() // defined in DateInterval

Object getSecond() // overrides the method defined in Pair to call the first method

You could not write Java code like that; it would be illegal to have two methods with the same parameter types—here, with no parameters. However, in the virtual machine, the parameter types and the return type specify a method. Therefore, the compiler can produce bytecodes for two methods that differ only in their return type, and the virtual machine will handle this situation correctly.

Note

Bridge methods are not limited to generic types. We already noted in Chapter 5 that it is legal for a method to specify a more restrictive return type when overriding another method. For example:

Click here to view code image

public class Employee implements Cloneable

{

public Employee clone() throws CloneNotSupportedException { . . . }

}

The Object.clone and Employee.clone methods are said to have covariant return types.

Actually, the Employee class has two clone methods:

Click here to view code image

Employee clone() // defined above

Object clone() // synthesized bridge method, overrides Object.clone

The synthesized bridge method calls the newly defined method.

In summary, you need to remember these facts about translation of Java generics:

There are no generics in the virtual machine, only ordinary classes and methods.

All type parameters are replaced by their bounds.

Bridge methods are synthesized to preserve polymorphism.

Casts are inserted as necessary to preserve type safety.

8.5.4 Calling Legacy Code

When Java generics were designed, a major goal was to allow interoperability between generics and legacy code. Let us look at a concrete example of such legacy. The Swing user interface toolkit provides a JSlider class whose「ticks」can be customized with labels that contain text or images. The labels are set with the call

Click here to view code image

void setLabelTable(Dictionary table)

The Dictionary class maps integers to labels. Before Java 5, that class was implemented as a map of Object instances. Java 5 made Dictionary into a generic class, but JSlider was never updated. At this point, Dictionary without type parameters is a raw type. This is where compatibility comes in.

When you populate the dictionary, you can use the generic type.

Click here to view code image

Dictionary<Integer, Component> labelTable = new Hashtable<>();

labelTable.put(0, new JLabel(new ImageIcon("nine.gif")));

labelTable.put(20, new JLabel(new ImageIcon("ten.gif")));

. . .

When you pass the Dictionary<Integer, Component> object to setLabelTable, the compiler issues a warning.

Click here to view code image

slider.setLabelTable(labelTable); // warning

After all, the compiler has no assurance about what the setLabelTable might do to the Dictionary object. That method might replace all the keys with strings. That breaks the guarantee that the keys have type Integer, and future operations may cause bad cast exceptions.

You should ponder it and ask what the JSlider is actually going to do with this Dictionary object. In our case, it is pretty clear that the JSlider only reads the information, so we can ignore the warning.

Now consider the opposite case, in which you get an object of a raw type from a legacy class. You can assign it to a variable whose type uses generics, but of course you will get a warning. For example:

Click here to view code image

Dictionary<Integer, Components> labelTable = slider.getLabelTable(); // warning

That's OK—review the warning and make sure that the label table really contains Integer and Component objects. Of course, there never is an absolute guarantee. A malicious coder might have installed a different Dictionary in the slider. But again, the situation is no worse than it was before generics. In the worst case, your program will throw an exception.

After you are done pondering the warning, you can use an annotation to make it disappear. You can annotate a local variable:

Click here to view code image

@SuppressWarnings("unchecked")

Dictionary<Integer, Components> labelTable = slider.getLabelTable(); // no warning

Or you can annotate an entire method, like this:

Click here to view code image

@SuppressWarnings("unchecked")

public void configureSlider() { . . . }

This annotation turns off checking for all code inside the method.

8.6 Restrictions and Limitations

In the following sections, we discuss a number of restrictions that you need to consider when working with Java generics. Most of these restrictions are a consequence of type erasure.

8.6.1 Type Parameters Cannot Be Instantiated with Primitive Types

You cannot substitute a primitive type for a type parameter. Thus, there is no Pair<double>, only Pair<Double>. The reason is, of course, type erasure. After erasure, the Pair class has fields of type Object, and you can't use them to store double values.

This is an annoyance, to be sure, but it is consistent with the separate status of primitive types in the Java language. It is not a fatal flaw—there are only eight primitive types, and you can always handle them with separate classes and methods when wrapper types are not an acceptable substitute.

8.6.2 Runtime Type Inquiry Only Works with Raw Types

Objects in the virtual machine always have a specific nongeneric type. Therefore, all type inquiries yield only the raw type. For example,

Click here to view code image

if (a instanceof Pair<String>) // ERROR

could only test whether a is a Pair of any type. The same is true for the test

Click here to view code image

if (a instanceof Pair<T>) // ERROR

or the cast

Click here to view code image

Pair<String> p = (Pair<String>) a; // warning--can only test that a is a Pair

To remind you of the risk, you will get a compiler error (with instanceof) or warning (with casts) when you try to inquire whether an object belongs to a generic type.

In the same spirit, the getClass method always returns the raw type. For example:

Click here to view code image

Pair<String> stringPair = . . .;

Pair<Employee> employeePair = . . .;

if (stringPair.getClass() == employeePair.getClass()) // they are equal

The comparison yields true because both calls to getClass return Pair.class.

8.6.3 You Cannot Create Arrays of Parameterized Types

You cannot instantiate arrays of parameterized types, such as

Click here to view code image

var table = new Pair<String>[10]; // ERROR

What's wrong with that? After erasure, the type of table is Pair[]. You can convert it to Object[]:

Click here to view code image

Object[] objarray = table;

An array remembers its component type and throws an ArrayStoreException if you try to store an element of the wrong type:

Click here to view code image

objarray[0] = "Hello"; // ERROR--component type is Pair

But erasure renders this mechanism ineffective for generic types. The assignment

Click here to view code image

objarray[0] = new Pair<Employee>();

would pass the array store check but still result in a type error. For this reason, arrays of parameterized types are outlawed.

Note that only the creation of these arrays is outlawed. You can declare a variable of type Pair<String>[]. But you can't initialize it with a new Pair<String>[10].

Note

You can declare arrays of wildcard types and then cast them:

Click here to view code image

var table = (Pair<String>[]) new Pair<?>[10];

The result is not safe. If you store a Pair<Employee> in table[0] and then call a String method on table[0].getFirst(), you get a ClassCastException.

Tip

If you need to collect parameterized type objects, simply use an ArrayList: ArrayList<Pair<String>> is safe and effective.

8.6.4 Varargs Warnings

In the preceding section, you saw that Java doesn't support arrays of generic types. In this section, we discuss a related issue: passing instances of a generic type to a method with a variable number of arguments.

Consider this simple method with variable arguments:

Click here to view code image

public static <T> void addAll(Collection<T> coll, T... ts)

{

for (T t : ts) coll.add(t);

}

Recall that the parameter ts is actually an array that holds all supplied arguments.

Now consider this call:

Click here to view code image

Collection<Pair<String>> table = . . .;

Pair<String> pair1 = . . .;

Pair<String> pair2 = . . .;

addAll(table, pair1, pair2);

In order to call this method, the Java virtual machine must make an array of Pair<String>, which is against the rules. However, the rules have been relaxed for this situation, and you only get a warning, not an error.

You can suppress the warning in one of two ways. You can add the annotation @SuppressWarnings("unchecked") to the method containing the call to addAll. Or, as of Java 7, you can annotate the addAll method itself with @SafeVarargs:

Click here to view code image

@SafeVarargs

public static <T> void addAll(Collection<T> coll, T... ts)

This method can now be called with generic types. You can use this annotation for any methods that merely read the elements of the parameter array, which is bound to be the most common use case.

The @SafeVarargs can only be used with constructors and methods that are static, final, or (as of Java 9) private. Any other method could be overridden, making the annotation meaningless.

Note

You can use the @SafeVarargs annotation to defeat the restriction against generic array creation, using this method:

Click here to view code image

@SafeVarargs static <E> E[] array(E... array) { return array; }

Now you can call

Click here to view code image

Pair<String>[] table = array(pair1, pair2);

This seems convenient, but there is a hidden danger. The code

Click here to view code image

Object[] objarray = table;

objarray[0] = new Pair<Employee>();

will run without an ArrayStoreException (because the array store only checks the erased type), and you'll get an exception elsewhere when you work with table[0].

8.6.5 You Cannot Instantiate Type Variables

You cannot use type variables in an expression such as new T(. . .). For example, the following Pair<T> constructor is illegal:

Click here to view code image

public Pair() { first = new T(); second = new T(); } // ERROR

Type erasure would change T to Object, and surely you don't want to call new Object().

The best workaround, available since Java 8, is to make the caller provide a constructor expression. For example:

Click here to view code image

Pair<String> p = Pair.makePair(String::new);

The makePair method receives a Supplier<T>, the functional interface for a function with no arguments and a result of type T:

Click here to view code image

public static <T> Pair<T> makePair(Supplier<T> constr)

{

return new Pair<>(constr.get(), constr.get());

}

A more traditional workaround is to construct generic objects through reflection, by calling the Constructor.newInstance method.

Unfortunately, the details are a bit complex. You cannot call

Click here to view code image

first = T.class.getConstructor().newInstance(); // ERROR

The expression T.class is not legal because it would erase to Object.class. Instead, you must design the API so that you are handed a Class object, like this:

Click here to view code image

public static <T> Pair<T> makePair(Class<T> cl)

{

try {

return new Pair<>(cl.getConstructor().newInstance(),

cl.getConstructor().newInstance());

}

catch (Exception e) { return null; }

}

This method could be called as follows:

Click here to view code image

Pair<String> p = Pair.makePair(String.class);

Note that the Class class is itself generic. For example, String.class is an instance (indeed, the sole instance) of Class<String>. Therefore, the makePair method can infer the type of the pair that it is making.

8.6.6 You Cannot Construct a Generic Array

Just as you cannot instantiate a single generic instance, you cannot instantiate an array. The reasons are different—an array is, after all, filled with null values, which would seem safe to construct. But an array also carries a type, which is used to monitor array stores in the virtual machine. That type is erased. For example, consider

Click here to view code image

public static <T extends Comparable> T[] minmax(T... a)

{

T[] mm = new T[2]; // ERROR

. . .

}

Type erasure would cause this method to always construct an array Comparable[2].

If the array is only used as a private instance field of a class, you can declare the element type of the array to be the erased type and use casts. For example, the ArrayList class could be implemented as follows:

Click here to view code image

public class ArrayList<E>

{

private Object[] elements;

. . .

@SuppressWarnings("unchecked") public E get(int n) { return (E) elements[n]; }

public void set(int n, E e) { elements[n] = e; } // no cast needed

}

The actual implementation is not quite as clean:

Click here to view code image

public class ArrayList<E>

{

private E[] elements;

. . .

public ArrayList() { elements = (E[]) new Object[10]; }

}

Here, the cast E[] is an outright lie, but type erasure makes it undetectable.

This technique does not work for our minmax method since we are returning a T[] array, and a runtime error results if we lie about its type. Suppose we implement

Click here to view code image

public static <T extends Comparable> T[] minmax(T... a)

{

var result = new Comparable[2]; // array of erased type

. . .

return (T[]) result; // compiles with warning

}

The call

Click here to view code image

String[] names = ArrayAlg.minmax("Tom", "Dick", "Harry");

compiles without any warning. A ClassCastException occurs when the Comparable[] reference is cast to String[] after the method returns.

In this situation, it is best to ask the user to provide an array constructor expression:

Click here to view code image

String[] names = ArrayAlg.minmax(String[]::new, "Tom", "Dick", "Harry");

The constructor expression String[]::new denotes a function that, given the desired length, constructs a String array of that length.

The method uses that parameter to produce an array of the correct type:

Click here to view code image

public static <T extends Comparable> T[] minmax(IntFunction<T[]> constr, T... a)

{

T[] result = constr.apply(2);

. . .

}

A more old-fashioned approach is to use reflection and call Array.newInstance:

Click here to view code image

public static <T extends Comparable> T[] minmax(T... a)

{

var result = (T[]) Array.newInstance(a.getClass().getComponentType(), 2);

. . .

}

The toArray method of the ArrayList class is not so lucky. It needs to produce a T[] array, but it doesn't have the component type. Therefore, there are two variants:

Click here to view code image

Object[] toArray()

T[] toArray(T[] result)

The second method receives an array parameter. If the array is large enough, it is used. Otherwise, a new array of sufficient size is created, using the component type of result.

8.6.7 Type Variables Are Not Valid in Static Contexts of Generic Classes

You cannot reference type variables in static fields or methods. For example, the following clever idea won't work:

Click here to view code image

public class Singleton<T>

{

private static T singleInstance; // ERROR

public static T getSingleInstance() // ERROR

{

if (singleInstance == null) construct new instance of T

return singleInstance;

}

}

If this could be done, then a program could declare a Singleton<Random> to share a random number generator and a Singleton<JFileChooser> to share a file chooser dialog. But it can't work. After type erasure there is only one Singleton class, and only one singleInstance field. For that reason, static fields and methods with type variables are simply outlawed.

8.6.8 You Cannot Throw or Catch Instances of a Generic Class

You can neither throw nor catch objects of a generic class. In fact, it is not even legal for a generic class to extend Throwable. For example, the following definition will not compile:

Click here to view code image

public class Problem<T> extends Exception { /* . . . */ }

// ERROR--can't extend Throwable

You cannot use a type variable in a catch clause. For example, the following method will not compile:

Click here to view code image

public static <T extends Throwable> void doWork(Class<T> t)

{

try

{

do work

}

catch (T e) // ERROR--can't catch type variable

{

Logger.global.info(. . .);

}

}

However, it is OK to use type variables in exception specifications. The following method is legal:

Click here to view code image

public static <T extends Throwable> void d

{

do work

}

catch (Throwable realCause)

{

t.initCause(realCause);

throw t;

}

}

8.6.9 You Can Defeat Checked Exception Checking

A bedrock principle of Java exception handling is that you must provide a handler for all checked exceptions. You can use generics to defeat this scheme. The key ingredient is this method:

Click here to view code image

@SuppressWarnings("unchecked")

static <T extends Throwable> void throwAs(Throwable t) throws T

{

throw (T) t;

}

Suppose this method is contained in an interface Task. When you have a checked exception e and call

Click here to view code image

Task.<RuntimeException>throwAs(e);

then the compiler will believe that e becomes an unchecked exception. The following turns all exceptions into those that the compiler believes to be unchecked:

Click here to view code image

try

{

do work

}

catch (Throwable t)

{

Task.<RuntimeException>throwAs(t);

}

Let's use this to solve a vexing problem. To run code in a thread, you have to place it into the run method of a class that implements the Runnable interface. But that method is not allowed to throw checked exceptions. We will provide an adaptor from a Task, whose run method is allowed to throw arbitrary exceptions, to a Runnable:

Click here to view code image

interface Task

{

void run() throws Exception;

@SuppressWarnings("unchecked")

static <T extends Throwable> void throwAs(Throwable t) throws T

{

throw (T) t;

}

static Runnable asRunnable(Task task)

{

return () ->

{

try

{

task.run();

}

catch (Exception e)

{

Task.<RuntimeException>throwAs(e);

}

};

}

}

For example, this program runs a thread that will throw a checked exception:

Click here to view code image

public class Test

{

public static void main(String[] args)

{

var thread = new Thread(Task.asRunnable(() ->

{

Thread.sleep(1000);

System.out.println("Hello, World!");

throw new Exception("Check this out!");

}));

thread.start();

}

}

The Thread.sleep method is declared to throw an InterruptedException, and we no longer have to catch it. Since we don't interrupt the thread, that exception won't be thrown. However, the program throws a checked exception. When you run the program, you will get a stack trace.

What's so remarkable about that? Normally, you have to catch all checked exceptions inside the run method of a Runnable and wrap them into unchecked exceptions—the run method is declared to throw no checked exceptions.

But here, we don't wrap. We simply throw the exception, tricking the compiler into believing that it is not a checked exception.

Using generic classes, erasure, and the @SuppressWarnings annotation, we were able to defeat an essential part of the Java type system.

8.6.10 Beware of Clashes after Erasure

It is illegal to create conditions that cause clashes when generic types are erased. Here is an example. Suppose we add an equals method to the Pair class, like this:

Click here to view code image

public class Pair<T>

{

public boolean equals(T value) { return first.equals(value) && second.equals(value); }

. . .

}

Consider a Pair<String>. Conceptually, it has two equals methods:

Click here to view code image

boolean equals(String) // defined in Pair<T>

boolean equals(Object) // inherited from Object

But the intuition leads us astray. The erasure of the method

boolean equals(T)

is

boolean equals(Object)

which clashes with the Object.equals method.

The remedy is, of course, to rename the offending method.

The generics specification cites another rule:「To support translation by erasure, we impose the restriction that a class or type variable may not at the same time be a subtype of two interface types which are different parameterizations of the same interface.」For example, the following is illegal:

Click here to view code image

class Employee implements Comparable<Employee> { . . . }

class Manager extends Employee implements Comparable<Manager> { . . . } // ERROR

Manager would then implement both Comparable<Employee> and Comparable<Manager>, which are different parameterizations of the same interface.

It is not obvious what this restriction has to do with type erasure. After all, the nongeneric version

Click here to view code image

class Employee implements Comparable { . . . }

class Manager extends Employee implements Comparable { . . . }

is legal. The reason is far more subtle. There would be a conflict with the synthesized bridge methods. A class that implements Comparable<X> gets a bridge method

Click here to view code image

public int compareTo(Object other) { return compareTo((X) other); }

You cannot have two such methods for different types X.

8.7 Inheritance Rules for Generic Types

When you work with generic classes, you need to learn a few rules about inheritance and subtypes. Let's start with a situation which many programmers find unintuitive. Consider a class and a subclass, such as Employee and Manager. Is Pair<Manager> a subclass of Pair<Employee>? Perhaps surprisingly, the answer is「no.」For example, the following code will not compile:

Click here to view code image

Manager[] topHonchos = . . .;

Pair<Employee> result = ArrayAlg.minmax(topHonchos); // ERROR

The minmax method returns a Pair<Manager>, not a Pair<Employee>, and it is illegal to assign one to the other.

In general, there is no relationship between Pair<S> and Pair<T>, no matter how S and T are related (see Figure 8.1).

Figure 8.1 No inheritance relationship between pair classes

This seems like a cruel restriction, but it is necessary for type safety. Suppose we were allowed to convert a Pair<Manager> to a Pair<Employee>. Consider this code:

Click here to view code image

var managerBuddies = new Pair<Manager>(ceo, cfo);

Pair<Employee> employeeBuddies = managerBuddies; // illegal, but suppose it wasn't

employeeBuddies.setFirst(lowlyEmployee);

Clearly, the last statement is legal. But employeeBuddies and managerBuddies refer to the same object. We now managed to pair up the CFO with a lowly employee, which should not be possible for a Pair<Manager>.

Note

You just saw an important difference between generic types and Java arrays. You can assign a Manager[] array to a variable of type Employee[]:

Click here to view code image

Manager[] managerBuddies = { ceo, cfo };

Employee[] employeeBuddies = managerBuddies; // OK

However, arrays come with special protection. If you try to store a lowly employee into employeeBuddies[0], the virtual machine throws an ArrayStoreException.

You can always convert a parameterized type to a raw type. For example, Pair<Employee> is a subtype of the raw type Pair. This conversion is necessary for interfacing with legacy code.

Can you convert to the raw type and then cause a type error? Unfortunately, you can. Consider this example:

Click here to view code image

var managerBuddies = new Pair<Manager>(ceo, cfo);

Pair rawBuddies = managerBuddies; // OK

rawBuddies.setFirst(new File(". . .")); // only a compile-time warning

This sounds scary. However, keep in mind that you are no worse off than you were with older versions of Java. The security of the virtual machine is not at stake. When the foreign object is retrieved with getFirst and assigned to a Manager variable, a ClassCastException is thrown, just as in the good old days. You merely lose the added safety that generic programming normally provides.

Finally, generic classes can extend or implement other generic classes. In this regard, they are no different from ordinary classes. For example, the class ArrayList<T> implements the interface List<T>. That means an ArrayList<Manager> can be converted to a List<Manager>. However, as you just saw, an ArrayList<Manager> is not an ArrayList<Employee> or List<Employee>. Figure 8.2 shows these relationships.

Figure 8.2 Subtype relationships among generic list types

8.8 Wildcard Types

It was known for some time among researchers of type systems that a rigid system of generic types is quite unpleasant to use. The Java designers invented an ingenious (but nevertheless safe)「escape hatch」: the wildcard type. The following sections show you how to work with wildcards.

8.8.1 The Wildcard Concept

In a wildcard type, a type parameter is allowed to vary. For example, the wildcard type

Click here to view code image

Pair<? extends Employee>

denotes any generic Pair type whose type parameter is a subclass of Employee, such as Pair<Manager>, but not Pair<String>.

Let's say you want to write a method that prints out pairs of employees, like this:

Click here to view code image

public static void printBuddies(Pair<Employee> p)

{

Employee first = p.getFirst();

Employee second = p.getSecond();

System.out.println(first.getName() + " and " + second.getName() + " are buddies.");

}

As you saw in the preceding section, you cannot pass a Pair<Manager> to that method, which is rather limiting. But the solution is simple—use a wildcard type:

Click here to view code image

public static void printBuddies(Pair<? extends Employee> p)

The type Pair<Manager> is a subtype of Pair<? extends Employee> (see Figure 8.3).

Figure 8.3 Subtype relationships with wildcards

Can we use wildcards to corrupt a Pair<Manager> through a Pair<? extends Employee> reference?

Click here to view code image

var managerBuddies = new Pair<Manager>(ceo, cfo);

Pair<? extends Employee> wildcardBuddies = managerBuddies; // OK

wildcardBuddies.setFirst(lowlyEmployee); // compile-time error

No corruption is possible. The call to setFirst is a type error. To see why, let us have a closer look at the type Pair<? extends Employee>. Its methods look like this:

Click here to view code image

? extends Employee getFirst()

void setFirst(? extends Employee)

This makes it impossible to call the setFirst method. The compiler only knows that it needs some subtype of Employee, but it doesn't know which type. It refuses to pass any specific type—after all, ? might not match it.

We don't have this problem with getFirst: It is perfectly legal to assign the return value of getFirst to an Employee reference.

This is the key idea behind bounded wildcards. We now have a way of distinguishing between the safe accessor methods and the unsafe mutator methods.

8.8.2 Supertype Bounds for Wildcards

Wildcard bounds are similar to type variable bounds, but they have an added capability—you can specify a supertype bound, like this:

Click here to view code image

? super Manager

This wildcard is restricted to all supertypes of Manager. (It was a stroke of good luck that the existing super keyword describes the relationship so accurately.)

Why would you want to do this? A wildcard with a supertype bound gives you a behavior that is opposite to that of the wildcards described in Section 8.8,「Wildcard Types,」on p. 459. You can supply parameters to methods, but you can't use the return values. For example, Pair<? super Manager> has methods that can be described as follows:

Click here to view code image

void setFirst(? super Manager)

? super Manager getFirst()

This is not actual Java syntax, but it shows what the compiler knows. The compiler cannot know the exact type of the setFirst method and therefore cannot accept a call with an argument of type Employee or Object. It is only possible to pass an object of type Manager or a subtype such as Executive. Moreover, if you call getFirst, there is no guarantee about the type of the returned object. You can only assign it to an Object.

Here is a typical example. We have an array of managers and want to put the manager with the lowest and highest bonus into a Pair object. What kind of Pair? A Pair<Employee> should be fair game or, for that matter, a Pair<Object> (see Figure 8.4). The following method will accept any appropriate Pair:

Figure 8.4 A wildcard with a supertype bound

Click here to view code image

public static void minmaxBonus(Manager[] a, Pair<? super Manager> result)

{

if (a.length == 0) return;

Manager min = a[0];

Manager max = a[0];

for (int i = 1; i < a.length; i++)

{

if (min.getBonus() > a[i].getBonus()) min = a[i];

if (max.getBonus() < a[i].getBonus()) max = a[i];

}

result.setFirst(min);

result.setSecond(max);

}

Intuitively speaking, wildcards with supertype bounds let you write to a generic object, while wildcards with subtype bounds let you read from a generic object.

Here is another use for supertype bounds. The Comparable interface is itself a generic type. It is declared as follows:

Click here to view code image

public interface Comparable<T>

{

public int compareTo(T other);

}

Here, the type variable indicates the type of the other parameter. For example, the String class implements Comparable<String>, and its compareTo method is declared as

Click here to view code image

public int compareTo(String other)

This is nice—the explicit parameter has the correct type. Before the interface was generic, other was an Object, and a cast was necessary in the implementation of the method.

Now that Comparable is a generic type, perhaps we should have done a better job with the min method of the ArrayAlg class? We could have declared it as

Click here to view code image

public static <T extends Comparable<T>> T min(T[] a)

This looks more thorough than just using T extends Comparable, and it would work fine for many classes. For example, if you compute the minimum of a String array, then T is the type String, and String is a subtype of Comparable<String>. But we run into a problem when processing an array of LocalDate objects. As it happens, LocalDate implements ChronoLocalDate, and ChronoLocalDate extends Comparable<ChronoLocalDate>. Thus, LocalDate implements Comparable<ChronoLocalDate> but not Comparable<LocalDate>.

In a situation such as this one, supertypes come to the rescue:

Click here to view code image

public static <T extends Comparable<? super T>> T min(T[] a) . . .

Now the compareTo method has the form

Click here to view code image

int compareTo(? super T)

Maybe it is declared to take an object of type T, or—for example, when T is LocalDate—a supertype of T. At any rate, it is safe to pass an object of type T to the compareTo method.

To the uninitiated, a declaration such as <T extends Comparable<? super T>> is bound to look intimidating. This is unfortunate, because the intent of this declaration is to help application programmers by removing unnecessary restrictions on the call parameters. Application programmers with no interest in generics will probably learn quickly to gloss over these declarations and just take for granted that library programmers will do the right thing. If you are a library programmer, you'll need to get used to wildcards, or your users will curse you and throw random casts at their code until it compiles.

Note

Another common use for supertype bounds is an argument type of a functional interface. For example, the Collection interface has a method

Click here to view code image

default boolean removeIf(Predicate<? super E> filter)

The method removes all elements that fulfill the given predicate. For example, if you hate employees with odd hash codes, you can remove them like this:

Click here to view code image

ArrayList<Employee> staff = . . .;

Predicate<Object> oddHashCode = obj -> obj.hashCode() %2 != 0;

staff.removeIf(oddHashCode);

You want to be able to pass a Predicate<Object>, not just a Predicate<Employee>. The super wildcard makes that possible.

8.8.3 Unbounded Wildcards

You can even use wildcards with no bounds at all—for example, Pair<?>. At first glance, this looks identical to the raw Pair type. Actually, the types are very different. The type Pair<?> has methods such as

Click here to view code image

? getFirst()

void setFirst(?)

The return value of getFirst can only be assigned to an Object. The setFirst method can never be called, not even with an Object. That's the essential difference between Pair<?> and Pair: you can call the setFirst method of the raw Pair class with any Object.

Note

You can call setFirst(null).

Why would you ever want such a wimpy type? It is useful for very simple operations. For example, the following method tests whether a pair contains a null reference. It never needs the actual type.

Click here to view code image

public static boolean hasNulls(Pair<?> p)

{

return p.getFirst() == null || p.getSecond() == null;

}

You could have avoided the wildcard type by turning hasNulls into a generic method:

Click here to view code image

public static <T> boolean hasNulls(Pair<T> p)

However, the version with the wildcard type seems easier to read.

8.8.4 Wildcard Capture

Let us write a method that swaps the elements of a pair:

Click here to view code image

public static void swap(Pair<?> p)

A wildcard is not a type variable, so we can't write code that uses ? as a type. In other words, the following would be illegal:

Click here to view code image

? t = p.getFirst(); // ERROR

p.setFirst(p.getSecond());

p.setSecond(t);

That's a problem because we need to temporarily hold the first element when we do the swapping. Fortunately, there is an interesting solution to this problem. We can write a helper method, swapHelper, like this:

Click here to view code image

public static <T> void swapHelper(Pair<T> p)

{

T t = p.getFirst();

p.setFirst(p.getSecond());

p.setSecond(t);

}

Note that swapHelper is a generic method, whereas swap is not—it has a fixed parameter of type Pair<?>.

Now we can call swapHelper from swap:

Click here to view code image

public static void swap(Pair<?> p) { swapHelper(p); }

In this case, the parameter T of the swapHelper method captures the wildcard. It isn't known what type the wildcard denotes, but it is a definite type, and the definition of <T>swapHelper makes perfect sense when T denotes that type.

Of course, in this case, we were not compelled to use a wildcard. We could have directly implemented <T> void swap(Pair<T> p) as a generic method without wildcards. However, consider this example in which a wildcard type occurs naturally in the middle of a computation:

Click here to view code image

public static void maxminBonus(Manager[] a, Pair<? super Manager> result)

{

minmaxBonus(a, result);

PairAlg.swapHelper(result); // OK--swapHelper captures wildcard type

}

Here, the wildcard capture mechanism cannot be avoided.

Wildcard capture is only legal in very limited circumstances. The compiler must be able to guarantee that the wildcard represents a single, definite type. For example, the T in ArrayList<Pair<T>> can never capture the wildcard in ArrayList<Pair<?>>. The array list might hold two Pair<?>, each of which has a different type for ?.

The test program in Listing 8.3 gathers up the various methods that we discussed in the preceding sections so you can see them in context.

Listing 8.3 pair3/PairTest3.java

Click here to view code image

1 package pair3;

2

3 /**

4 * @version 1.01 2012-01-26

5 * @author Cay Horstmann

6 */

7 public class PairTest3

8 {

9 public static void main(String[] args)

10 {

11 var ceo = new Manager("Gus Greedy", 800000, 2003, 12, 15);

12 var cfo = new Manager("Sid Sneaky", 600000, 2003, 12, 15);

13 var buddies = new Pair<Manager>(ceo, cfo);

14 printBuddies(buddies);

15

16 ceo.setBonus(1000000);

17 cfo.setBonus(500000);

18 Manager[] managers = { ceo, cfo };

19

20 var result = new Pair<Employee>();

21 minmaxBonus(managers, result);

22 System.out.println("first: " + result.getFirst().getName()

23 + ", second: " + result.getSecond().getName());

24 maxminBonus(managers, result);

25 System.out.println("first: " + result.getFirst().getName()

26 + ", second: " + result.getSecond().getName());

27 }

28

29 public static void printBuddies(Pair<? extends Employee> p)

30 {

31 Employee first = p.getFirst();

32 Employee second = p.getSecond();

33 System.out.println(first.getName() + " and " + second.getName() + " are buddies.");

34 }

35

36 public static void minmaxBonus(Manager[] a, Pair<? super Manager> result)

37 {

38 if (a.length == 0) return;

39 Manager min = a[0];

40 Manager max = a[0];

41 for (int i = 1; i < a.length; i++)

42 {

43 if (min.getBonus() > a[i].getBonus()) min = a[i];

44 if (max.getBonus() < a[i].getBonus()) max = a[i];

45 }

46 result.setFirst(min);

47 result.setSecond(max);

48 }

49

50 public static void maxminBonus(Manager[] a, Pair<? super Manager> result)

51 {

52 minmaxBonus(a, result);

53 PairAlg.swapHelper(result); // OK--swapHelper captures wildcard type

54 }

55 // can't write public static <T super manager> . . .

56 }

57

58 class PairAlg

59 {

60 public static boolean hasNulls(Pair<?> p)

61 {

62 return p.getFirst() == null || p.getSecond() == null;

63 }

64

65 public static void swap(Pair<?> p) { swapHelper(p); }

66

67 public static <T> void swapHelper(Pair<T> p)

68 {

69 T t = p.getFirst();

70 p.setFirst(p.getSecond());

71 p.setSecond(t);

72 }

73 }

8.9 Reflection and Generics

Reflection lets you analyze arbitrary objects at runtime. If the objects are instances of generic classes, you don't get much information about the generic type parameters because they have been erased. In the following sections, you will learn what you can nevertheless find out about generic classes with reflection.

8.9.1 The Generic Class Class

The Class class is now generic. For example, String.class is actually an object (in fact, the sole object) of the class Class<String>.

The type parameter is useful because it allows the methods of Class<T> to be more specific about their return types. The following methods of Class<T> take advantage of the type parameter:

Click here to view code image

T newInstance()

T cast(Object obj)

T[] getEnumConstants()

Class<? super T> getSuperclass()

Constructor<T> getConstructor(Class... parameterTypes)

Constructor<T> getDeclaredConstructor(Class... parameterTypes)

The newInstance method returns an instance of the class, obtained from the no-argument constructor. Its return type can now be declared to be T, the same type as the class that is being described by Class<T>. That saves a cast.

The cast method returns the given object, now declared as type T if its type is indeed a subtype of T. Otherwise, it throws a BadCastException.

The getEnumConstants method returns null if this class is not an enum class or an array of the enumeration values which are known to be of type T.

Finally, the getConstructor and getDeclaredConstructor methods return a Constructor<T> object. The Constructor class has also been made generic so that its newInstance method has the correct return type.

java.lang.Class<T> 1.0

T newInstance()

returns a new instance constructed with the no-argument constructor.

T cast(Object obj)

returns obj if it is null or can be converted to the type T, or throws a BadCastException otherwise.

T[] getEnumConstants() 5

returns an array of all values if T is an enumerated type, null otherwise.

Class<? super T> getSuperclass()

returns the superclass of this class, or null if T is not a class or the class Object.

Constructor<T> getConstructor(Class... parameterTypes) 1.1

Constructor<T> getDeclaredConstructor(Class... parameterTypes) 1.1

gets the public constructor, or the constructor with the given parameter types.

java.lang.reflect.Constructor<T> 1.1

T newInstance(Object... parameters)

returns a new instance constructed with the given parameters.

8.9.2 Using Class<T> Parameters for Type Matching

It is sometimes useful to match the type variable of a Class<T> parameter in a generic method. Here is the canonical example:

Click here to view code image

public static <T> Pair<T> makePair(Class<T> c) throws InstantiationException,

IllegalAccessException

{

return new Pair<>(c.newInstance(), c.newInstance());

}

If you call

Click here to view code image

makePair(Employee.class)

then Employee.class is an object of type Class<Employee>. The type parameter T of the makePair method matches Employee, and the compiler can infer that the method returns a Pair<Employee>.

8.9.3 Generic Type Information in the Virtual Machine

One of the notable features of Java generics is the erasure of generic types in the virtual machine. Perhaps surprisingly, the erased classes still retain some faint memory of their generic origin. For example, the raw Pair class knows that it originated from the generic class Pair<T>, even though an object of type Pair can't tell whether it was constructed as a Pair<String> or Pair<Employee>.

Similarly, consider a method

Click here to view code image

public static Comparable min(Comparable[] a)

that is the erasure of a generic method

Click here to view code image

public static <T extends Comparable<? super T>> T min(T[] a)

You can use the reflection API to determine that

The generic method has a type parameter called T;

The type parameter has a subtype bound that is itself a generic type;

The bounding type has a wildcard parameter;

The wildcard parameter has a supertype bound; and

The generic method has a generic array parameter.

In other words, you can reconstruct everything about generic classes and methods that their implementors declared. However, you won't know how the type parameters were resolved for specific objects or method calls.

In order to express generic type declarations, use the interface Type in the java.lang.reflect package. The interface has the following subtypes:

The Class class, describing concrete types

The TypeVariable interface, describing type variables (such as T extends Comparable<? super T>)

The WildcardType interface, describing wildcards (such as ? super T)

The ParameterizedType interface, describing generic class or interface types (such as Comparable<? super T>)

The GenericArrayType interface, describing generic arrays (such as T[])

Figure 8.5 shows the inheritance hierarchy. Note that the last four subtypes are interfaces—the virtual machine instantiates suitable classes that implement these interfaces.

Figure 8.5 The Type interface and its descendants

Listing 8.4 uses the generic reflection API to print out what it discovers about a given class. If you run it with the Pair class, you get this report:

Click here to view code image

class Pair<T> extends java.lang.Object

public T getFirst()

public T getSecond()

public void setFirst(T)

public void setSecond(T)

If you run it with ArrayAlg in the PairTest2 directory, the report displays the following method:

Click here to view code image

public static <T extends java.lang.Comparable> Pair<T> minmax(T[])

Listing 8.4 genericReflection/GenericReflectionTest.java

Click here to view code image

1 package genericReflection;

2

3 import java.lang.reflect.*;

4 import java.util.*;

5

6 /**

7 * @version 1.11 2018-04-10

8 * @author Cay Horstmann

9 */

10 public class GenericReflectionTest

11 {

12 public static void main(String[] args)

13 {

14 // read class name from command line args or user input

15 String name;

16 if (args.length > 0) name = args[0];

17 else

18 {

19 try (var in = new Scanner(System.in))

20 {

21 System.out.println("Enter class name (e.g., java.util.Collections): ");

22 name = in.next();

23 }

24 }

25

26 try

27 {

28 // print generic info for class and public methods

29 Class<?> cl = Class.forName(name);

30 printClass(cl);

31 for (Method m : cl.getDeclaredMethods())

32 printMethod(m);

33 }

34 catch (ClassNotFoundException e)

35 {

36 e.printStackTrace();

37 }

38 }

39

40 public static void printClass(Class<?> cl)

41 {

42 System.out.print(cl);

43 printTypes(cl.getTypeParameters(), "<", ", ", ">", true);

44 Type sc = cl.getGenericSuperclass();

45 if (sc != null)

46 {

47 System.out.print(" extends ");

48 printType(sc, false);

49 }

50 printTypes(cl.getGenericInterfaces(), " implements ", ", ", "", false);

51 System.out.println();

52 }

53

54 public static void printMethod(Method m)

55 {

56 String name = m.getName();

57 System.out.print(Modifier.toString(m.getModifiers()));

58 System.out.print(" ");

59 printTypes(m.getTypeParameters(), "<", ", ", "> ", true);

60

61 printType(m.getGenericReturnType(), false);

62 System.out.print(" ");

63 System.out.print(name);

64 System.out.print("(");

65 printTypes(m.getGenericParameterTypes(), "", ", ", "", false);

66 System.out.println(")");

67 }

68

69 public static void printTypes(Type[] types, String pre, String sep, String suf,

70 boolean isDefinition)

71 {

72 if (pre.equals(" extends ") && Arrays.equals(types, new Type[] { Object.class }))

73 return;

74 if (types.length > 0) System.out.print(pre);

75 for (int i = 0; i < types.length; i++)

76 {

77 if (i > 0) System.out.print(sep);

78 printType(types[i], isDefinition);

79 }

80 if (types.length > 0) System.out.print(suf);

81 }

82

83 public static void printType(Type type, boolean isDefinition)

84 {

85 if (type instanceof Class)

86 {

87 var t = (Class<?>) type;

88 System.out.print(t.getName());

89 }

90 else if (type instanceof TypeVariable)

91 {

92 var t = (TypeVariable<?>) type;

93 System.out.print(t.getName());

94 if (isDefinition)

95 printTypes(t.getBounds(), " extends ", " & ", "", false);

96 }

97 else if (type instanceof WildcardType)

98 {

99 var t = (WildcardType) type;

100 System.out.print("?");

101 printTypes(t.getUpperBounds(), " extends ", " & ", "", false);

102 printTypes(t.getLowerBounds(), " super ", " & ", "", false);

103 }

104 else if (type instanceof ParameterizedType)

105 {

106 var t = (ParameterizedType) type;

107 Type owner = t.getOwnerType();

108 if (owner != null)

109 {

110 printType(owner, false);

111 System.out.print(".");

112 }

113 printType(t.getRawType(), false);

114 printTypes(t.getActualTypeArguments(), "<", ", ", ">", false);

115 }

116 else if (type instanceof GenericArrayType)

117 {

118 var t = (GenericArrayType) type;

119 System.out.print("");

120 printType(t.getGenericComponentType(), isDefinition);

121 System.out.print("[]");

122 }

123 }

124 }

8.9.4 Type Literals

Sometimes, you want to drive program behavior by the type of a value. For example, in a persistence mechanism, you may want the user to specify a way of saving an object of a particular class. This is typically implemented by associating the Class object with an action.

However, with generic classes, erasure poses a problem. How can you have different actions for, say, ArrayList<Integer> and ArrayList<String> when both erase to the same raw ArrayList type?

There is a trick that can offer relief in some situations. You can capture an instance of the Type interface that you encountered in the preceding section. Construct an anonymous subclass like this:

Click here to view code image

var type = new TypeLiteral<ArrayList<Integer>>(){} // note the {}

The TypeLiteral constructor captures the generic supertype:

Click here to view code image

class TypeLiteral

{

public TypeLiteral()

{

Type parentType = getClass().getGenericSuperclass();

if (parentType instanceof ParameterizedType)

{

type = ((ParameterizedType) parentType).getActualTypeArguments()[0];

}

else

throw new UnsupportedOperationException(

"Construct as new TypeLiteral<. . .>(){}");

}

. . .

}

If we have a generic type available at runtime, we can match it against the TypeLiteral. We can't get a generic type from an object—it is erased. But, as you have seen in the preceding section, generic types of fields and method parameters survive in the virtual machine.

Injection frameworks such as CDI and Guice use type literals to control injection of generic types. The example program in the book's companion code shows a simpler example. Given an object, we enumerate its fields, whose generic types are available, and look up associated formatting actions.

We format an ArrayList<Integer> by separating the values with spaces, an ArrayList<Character> by joining the characters to a string. Any other array lists are formatted by ArrayList.toString.

Listing 8.5 genericReflection/TypeLiterals.java

Click here to view code image

1 package genericReflection;

2

3 /**

4 @version 1.01 2018-04-10

5 @author Cay Horstmann

6 */

7

8 import java.lang.reflect.*;

9 import java.util.*;

10 import java.util.function.*;

11

12 /**

13 * A type literal describes a type that can be generic, such as ArrayList<String>.

14 */

15 class TypeLiteral<T>

16 {

17 private Type type;

18

19 /**

20 * This constructor must be invoked from an anonymous subclass

21 * as new TypeLiteral<. . .>(){}

22 */

23 public TypeLiteral()

24 {

25 Type parentType = getClass().getGenericSuperclass();

26 if (parentType instanceof ParameterizedType)

27 {

28 type = ((ParameterizedType) parentType).getActualTypeArguments()[0];

29 }

30 else

31 throw new UnsupportedOperationException(

32 "Construct as new TypeLiteral<. . .>(){}");

33 }

34

35 private TypeLiteral(Type type)

36 {

37 this.type = type;

38 }

39

40 /**

41 * Yields a type literal that describes the given type.

42 */

43 public static TypeLiteral<?> of(Type type)

44 {

45 return new TypeLiteral<Object>(type);

46 }

47

48 public String toString()

49 {

50 if (type instanceof Class) return ((Class<?>) type).getName();

51 else return type.toString();

52 }

53

54 public boolean equals(Object otherObject)

55 {

56 return otherObject instanceof TypeLiteral

57 && type.equals(((TypeLiteral<?>) otherObject).type);

58 }

59

60 public int hashCode()

61 {

62 return type.hashCode();

63 }

64 }

65

66 /**

67 * Formats objects, using rules that associate types with formatting functions.

68 */

69 class Formatter

70 {

71 private Map<TypeLiteral<?>, Function<?, String>> rules = new HashMap<>();

72

73 /**

74 * Add a formatting rule to this formatter.

75 * @param type the type to which this rule applies

76 * @param formatterForType the function that formats objects of this type

77 */

78 public <T> void forType(TypeLiteral<T> type, Function<T, String> formatterForType)

79 {

80 rules.put(type, formatterForType);

81 }

82

83 /**

84 * Formats all fields of an object using the rules of this formatter.

85 * @param obj an object

86 * @return a string with all field names and formatted values

87 */

88 public String formatFields(Object obj)

89 throws IllegalArgumentException, IllegalAccessException

90 {

91 var result = new StringBuilder();

92 for (Field f : obj.getClass().getDeclaredFields())

93 {

94 result.append(f.getName());

95 result.append("=");

96 f.setAccessible(true);

97 Function<?, String> formatterForType = rules.get(TypeLiteral.of(f.getGenericType()));

98 if (formatterForType != null)

99 {

100 // formatterForType has parameter type ?. Nothing can be passed to its apply

101 // method. Cast makes the parameter type to Object so we can invoke it.

102 @SuppressWarnings("unchecked")

103 Function<Object, String> objectFormatter

104 = (Function<Object, String>) formatterForType;

105 result.append(objectFormatter.apply(f.get(obj)));

106 }

107 else

108 result.append(f.get(obj).toString());

109 result.append("\n");

110 }

111 return result.toString();

112 }

113 }

114

115 public class TypeLiterals

116 {

117 public static class Sample

118 {

119 ArrayList<Integer> nums;

120 ArrayList<Character> chars;

121 ArrayList<String> strings;

122 public Sample()

123 {

124 nums = new ArrayList<>();

125 nums.add(42); nums.add(1729);

126 chars = new ArrayList<>();

127 chars.add('H'); chars.add('i');

128 strings = new ArrayList<>();

129 strings.add("Hello"); strings.add("World");

130 }

131 }

132

133 private static <T> String join(String separator, ArrayList<T> elements)

134 {

135 var result = new StringBuilder();

136 for (T e : elements)

137 {

138 if (result.length() > 0) result.append(separator);

139 result.append(e.toString());

140 }

141 return result.toString();

142 }

143

144 public static void main(String[] args) throws Exception

145 {

146 var formatter = new Formatter();

147 formatter.forType(new TypeLiteral<ArrayList<Integer>>(){},

148 lst -> join(" ", lst));

149 formatter.forType(new TypeLiteral<ArrayList<Character>>(){},

150 lst -> "\"" + join("", lst) + "\"");

151 System.out.println(formatter.formatFields(new Sample()));

152 }

153 }

java.lang.Class<T> 1.0

TypeVariable[] getTypeParameters() 5

gets the generic type variables if this type was declared as a generic type, or an array of length 0 otherwise.

Type getGenericSuperclass() 5

gets the generic type of the superclass that was declared for this type, or null if this type is Object or not a class type.

Type[] getGenericInterfaces() 5

gets the generic types of the interfaces that were declared for this type, in declaration order, or an array of length 0 if this type doesn't implement interfaces.

java.lang.reflect.Method 1.1

TypeVariable[] getTypeParameters() 5

gets the generic type variables if this method was declared as a generic method, or an array of length 0 otherwise.

Type getGenericReturnType() 5

gets the generic return type with which this method was declared.

Type[] getGenericParameterTypes() 5

gets the generic parameter types with which this method was declared. If the method has no parameters, an array of length 0 is returned.

java.lang.reflect.TypeVariable 5

String getName()

gets the name of this type variable.

Type[] getBounds()

gets the subclass bounds of this type variable, or an array of length 0 if the variable is unbounded.

java.lang.reflect.WildcardType 5

Type[] getUpperBounds()

gets the subclass (extends) bounds of this type variable, or an array of length 0 if the variable has no subclass bounds.

Type[] getLowerBounds()

gets the superclass (super) bounds of this type variable, or an array of length 0 if the variable has no superclass bounds.

java.lang.reflect.ParameterizedType 5

Type getRawType()

gets the raw type of this parameterized type.

Type[] getActualTypeArguments()

gets the type parameters with which this parameterized type was declared.

Type getOwnerType()

gets the outer class type if this is an inner type, or null if this is a top-level type.

java.lang.reflect.GenericArrayType 5

Type getGenericComponentType()

gets the generic component type with which this array type was declared.

You now know how to use generic classes and how to program your own generic classes and methods if the need arises. Just as importantly, you know how to decipher the generic type declarations that you may encounter in the API documentation and in error messages. For an exhaustive discussion of everything there is to know about Java generics, turn to Angelika Langer's excellent list of frequently (and not so frequently) asked questions at http://angelikalanger.com/GenericsFAQ/JavaGenericsFAQ.html.

In the next chapter, you will see how the Java collections framework puts generics to work.

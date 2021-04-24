9.7 Legacy Collections

The data structures that you choose can make a big difference when you try to implement methods in a natural style or are concerned with performance. Do you need to search quickly through thousands (or even millions) of sorted items? Do you need to rapidly insert and remove elements in the middle of an ordered sequence? Do you need to establish associations between keys and values?

This chapter shows how the Java library can help you accomplish the traditional data structuring needed for serious programming. In college computer science programs, a course called Data Structures usually takes a semester to complete, and there are many, many books devoted to this important topic. Our coverage differs from that of a college course; we will skip the theory and just show you how to use the collection classes in the standard library.

9.1 The Java Collections Framework

The initial release of Java supplied only a small set of classes for the most useful data structures: Vector, Stack, Hashtable, BitSet, and the Enumeration interface that provides an abstract mechanism for visiting elements in an arbitrary container. That was certainly a wise choice—it takes time and skill to come up with a comprehensive collection class library.

With the advent of Java 1.2, the designers felt that the time had come to roll out a full-fledged set of data structures. They faced a number of conflicting design challenges. They wanted the library to be small and easy to learn. They did not want the complexity of the Standard Template Library (or STL) of C++, but they wanted the benefit of「generic algorithms」that STL pioneered. They wanted the legacy classes to fit into the new framework. As all designers of collections libraries do, they had to make some hard choices, and they came up with a number of idiosyncratic design decisions along the way. In this section, we will explore the basic design of the Java collections framework, show you how to put it to work, and explain the reasoning behind some of the more controversial features.

9.1.1 Separating Collection Interfaces and Implementation

As is common with modern data structure libraries, the Java collection library separates interfaces and implementations. Let us look at that separation with a familiar data structure, the queue.

A queue interface specifies that you can add elements at the tail end of the queue, remove them at the head, and find out how many elements are in the queue. You use a queue when you need to collect objects and retrieve them in a「first in, first out」fashion (see Figure 9.1).

Figure 9.1 A queue

A minimal form of a queue interface might look like this:

Click here to view code image

public interface Queue<E> // a simplified form of the interface in the standard library

{

void add(E element);

E remove();

int size();

}

The interface tells you nothing about how the queue is implemented. Of the two common implementations of a queue, one uses a「circular array」and one uses a linked list (see Figure 9.2).

Figure 9.2 Queue implementations

Each implementation can be expressed by a class that implements the Queue interface.

Click here to view code image

public class CircularArrayQueue<E> implements Queue<E> // not an actual library class

{

private int head;

private int tail;

CircularArrayQueue(int capacity) { . . . }

public void add(E element) { . . . }

public E remove() { . . . }

public int size() { . . . }

private E[] elements;

}

public class LinkedListQueue<E> implements Queue<E> // not an actual library class

{

private Link head;

private Link tail;

LinkedListQueue() { . . . }

public void add(E element) { . . . }

public E remove() { . . . }

public int size() { . . . }

}

Note

The Java library doesn't actually have classes named CircularArrayQueue and LinkedListQueue. We use these classes as examples to explain the conceptual distinction between collection interfaces and implementations. If you need a circular array queue, use the ArrayDeque class. For a linked list queue, simply use the LinkedList class—it implements the Queue interface.

When you use a queue in your program, you don't need to know which implementation is actually used once the collection has been constructed. Therefore, it makes sense to use the concrete class only when you construct the collection object. Use the interface type to hold the collection reference.

Click here to view code image

Queue<Customer> expressLane = new CircularArrayQueue<>(100);

expressLane.add(new Customer("Harry"));

With this approach, if you change your mind, you can easily use a different implementation. You only need to change your program in one place—in the constructor call. If you decide that a LinkedListQueue is a better choice after all, your code becomes

Click here to view code image

Queue<Customer> expressLane = new LinkedListQueue<>();

expressLane.add(new Customer("Harry"));

Why would you choose one implementation over another? The interface says nothing about the efficiency of an implementation. A circular array is somewhat more efficient than a linked list, so it is generally preferable. However, as usual, there is a price to pay.

The circular array is a bounded collection—it has a finite capacity. If you don't have an upper limit on the number of objects that your program will collect, you may be better off with a linked list implementation after all.

When you study the API documentation, you will find another set of classes whose name begins with Abstract, such as AbstractQueue. These classes are intended for library implementors. In the (perhaps unlikely) event that you want to implement your own queue class, you will find it easier to extend AbstractQueue than to implement all the methods of the Queue interface.

9.1.2 The Collection Interface

The fundamental interface for collection classes in the Java library is the Collection interface. The interface has two fundamental methods:

Click here to view code image

public interface Collection<E>

{

boolean add(E element);

Iterator<E> iterator();

. . .

}

There are several methods in addition to these two; we will discuss them later.

The add method adds an element to the collection. The add method returns true if adding the element actually changes the collection, and false if the collection is unchanged. For example, if you try to add an object to a set and the object is already present, the add request has no effect because sets reject duplicates.

The iterator method returns an object that implements the Iterator interface. You can use the iterator object to visit the elements in the collection one by one. We discuss iterators in the next section.

9.1.3 Iterators

The Iterator interface has four methods:

Click here to view code image

public interface Iterator<E>

{

E next();

boolean hasNext();

void remove();

default void forEachRemaining(Consumer<? super E> action);

}

By repeatedly calling the next method, you can visit the elements from the collection one by one. However, if you reach the end of the collection, the next method throws a NoSuchElementException. Therefore, you need to call the hasNext method before calling next. That method returns true if the iterator object still has more elements to visit. If you want to inspect all elements in a collection, request an iterator and then keep calling the next method while hasNext returns true. For example:

Click here to view code image

Collection<String> c = . . .;

Iterator<String> iter = c.iterator();

while (iter.hasNext())

{

String element = iter.next();

do something with element

}

You can write such a loop more concisely as the「for each」loop:

Click here to view code image

for (String element : c)

{

do something with element

}

The compiler simply translates the「for each」loop into a loop with an iterator.

The「for each」loop works with any object that implements the Iterable interface, an interface with a single abstract method:

Click here to view code image

public interface Iterable<E>

{

Iterator<E> iterator();

. . .

}

The Collection interface extends the Iterable interface. Therefore, you can use the「for each」loop with any collection in the standard library.

Instead of writing a loop, you can call the forEachRemaining method with a lambda expression that consumes an element. The lambda expression is invoked with each element of the iterator, until there are none left.

Click here to view code image

iterator.forEachRemaining(element -> do something with element);

The order in which the elements are visited depends on the collection type. If you iterate over an ArrayList, the iterator starts at index 0 and increments the index in each step. However, if you visit the elements in a HashSet, you will get them in an essentially random order. You can be assured that you will encounter all elements of the collection during the course of the iteration, but you cannot make any assumptions about their ordering. This is usually not a problem because the ordering does not matter for computations such as computing totals or counting matches.

Note

Old-timers will notice that the next and hasNext methods of the Iterator interface serve the same purpose as the nextElement and hasMoreElements methods of an Enumeration. The designers of the Java collections library could have chosen to make use of the Enumeration interface. But they disliked the cumbersome method names and instead introduced a new interface with shorter method names.

There is an important conceptual difference between iterators in the Java collections library and iterators in other libraries. In traditional collections libraries, such as the Standard Template Library of C++, iterators are modeled after array indexes. Given such an iterator, you can look up the element that is stored at that position, much like you can look up an array element a[i] if you have an array index i. Independently of the lookup, you can advance the iterator to the next position. This is the same operation as advancing an array index by calling i++, without performing a lookup. However, the Java iterators do not work like that. The lookup and position change are tightly coupled. The only way to look up an element is to call next, and that lookup advances the position.

Instead, think of Java iterators as being between elements. When you call next, the iterator jumps over the next element, and it returns a reference to the element that it just passed (see Figure 9.3).

Figure 9.3 Advancing an iterator

Note

Here is another useful analogy. You can think of Iterator.next as the equivalent of InputStream.read. Reading a byte from a stream automatically「consumes」the byte. The next call to read consumes and returns the next byte from the input. Similarly, repeated calls to next let you read all elements in a collection.

The remove method of the Iterator interface removes the element that was returned by the last call to next. In many situations, that makes sense—you need to see the element before you can decide that it is the one that should be removed. But if you want to remove an element in a particular position, you still need to skip past the element. For example, here is how you remove the first element in a collection of strings:

Click here to view code image

Iterator<String> it = c.iterator();

it.next(); // skip over the first element

it.remove(); // now remove it

More importantly, there is a dependency between the calls to the next and remove methods. It is illegal to call remove if it wasn't preceded by a call to next. If you try, an IllegalStateException is thrown.

If you want to remove two adjacent elements, you cannot simply call

Click here to view code image

it.remove();

it.remove(); // ERROR

Instead, you must first call next to jump over the element to be removed.

Click here to view code image

it.remove();

it.next();

it.remove(); // OK

9.1.4 Generic Utility Methods

The Collection and Iterator interfaces are generic, which means you can write utility methods that operate on any kind of collection. For example, here is a generic method that tests whether an arbitrary collection contains a given element:

Click here to view code image

public static <E> boolean contains(Collection<E> c, Object obj)

{

for (E element : c)

if (element.equals(obj))

return true;

return false;

}

The designers of the Java library decided that some of these utility methods are so useful that the library should make them available. That way, library users don't have to keep reinventing the wheel. The contains method is one such method.

In fact, the Collection interface declares quite a few useful methods that all implementing classes must supply. Among them are

Click here to view code image

int size()

boolean isEmpty()

boolean contains(Object obj)

boolean containsAll(Collection<?> c)

boolean equals(Object other)

boolean addAll(Collection<? extends E> from)

boolean remove(Object obj)

boolean removeAll(Collection<?> c)

void clear()

boolean retainAll(Collection<?> c)

Object[] toArray()

<T> T[] toArray(T[] arrayToFill)

Many of these methods are self-explanatory; you will find full documentation in the API notes at the end of this section.

Of course, it is a bother if every class that implements the Collection interface has to supply so many routine methods. To make life easier for implementors, the library supplies a class AbstractCollection that leaves the fundamental methods size and iterator abstract but implements the routine methods in terms of them. For example:

Click here to view code image

public abstract class AbstractCollection<E>

implements Collection<E>

{

. . .

public abstract Iterator<E> iterator();

public boolean contains(Object obj)

{

for (E element : this) // calls iterator()

if (element.equals(obj))

return true;

return false;

}

. . .

}

A concrete collection class can now extend the AbstractCollection class. It is up to the concrete collection class to supply an iterator method, but the contains method has been taken care of by the AbstractCollection superclass. However, if the subclass has a more efficient way of implementing contains, it is free to do so.

This approach is a bit outdated. It would be nicer if the methods were default methods of the Collection interface. This has not happened. However, several default methods have been added. Most of them deal with streams (which we will discuss in Volume II). In addition, there is a useful method

Click here to view code image

default boolean removeIf(Predicate<? super E> filter)

for removing elements that fulfill a condition.

java.util.Collection<E> 1.2

Iterator<E> iterator()

returns an iterator that can be used to visit the elements in the collection.

int size()

returns the number of elements currently stored in the collection.

boolean isEmpty()

returns true if this collection contains no elements.

boolean contains(Object obj)

returns true if this collection contains an object equal to obj.

boolean containsAll(Collection<?> other)

returns true if this collection contains all elements in the other collection.

boolean add(E element)

adds an element to the collection. Returns true if the collection changed as a result of this call.

boolean addAll(Collection<? extends E> other)

adds all elements from the other collection to this collection. Returns true if the collection changed as a result of this call.

boolean remove(Object obj)

removes an object equal to obj from this collection. Returns true if a matching object was removed.

boolean removeAll(Collection<?> other)

removes from this collection all elements from the other collection. Returns true if the collection changed as a result of this call.

default boolean removeIf(Predicate<? super E> filter) 8

removes all elements for which filter returns true. Returns true if the collection changed as a result of this call.

void clear()

removes all elements from this collection.

boolean retainAll(Collection<?> other)

removes all elements from this collection that do not equal one of the elements in the other collection. Returns true if the collection changed as a result of this call.

Object[] toArray()

returns an array of the objects in the collection.

<T> T[] toArray(T[] arrayToFill)

returns an array of the objects in the collection. If arrayToFill has sufficient length, it is filled with the elements of this collection. If there is space, a null element is appended. Otherwise, a new array with the same component type as arrayToFill and the same length as the size of this collection is allocated and filled.

java.util.Iterator<E> 1.2

boolean hasNext()

returns true if there is another element to visit.

E next()

returns the next object to visit. Throws a NoSuchElementException if the end of the collection has been reached.

void remove()

removes the last visited object. This method must immediately follow an element visit. If the collection has been modified since the last element visit, this method throws an IllegalStateException.

default void forEachRemaining(Consumer<? super E> action) 8

visits elements and passes them to the given action until no elements remain or the action throws an exception.

9.2 Interfaces in the Collections Framework

The Java collections framework defines a number of interfaces for different types of collections, shown in Figure 9.4.

Figure 9.4 The interfaces of the collections framework

There are two fundamental interfaces for collections: Collection and Map. As you already saw, you insert elements into a collection with a method

Click here to view code image

boolean add(E element)

However, maps hold key/value pairs, and you use the put method to insert them:

Click here to view code image

V put(K key, V value)

To read elements from a collection, visit them with an iterator. However, you can read values from a map with the get method:

V get(K key)

A List is an ordered collection. Elements are added into a particular position in the container. An element can be accessed in two ways: by an iterator or by an integer index. The latter is called random access because elements can be visited in any order. In contrast, when using an iterator, one must visit them sequentially.

The List interface defines several methods for random access:

Click here to view code image

void add(int index, E element)

void remove(int index)

E get(int index)

E set(int index, E element)

The ListIterator interface is a subinterface of Iterator. It defines a method for adding an element before the iterator position:

void add(E element)

Frankly, this aspect of the collections framework is poorly designed. In practice, there are two kinds of ordered collections, with very different performance tradeoffs. An ordered collection that is backed by an array has fast random access, and it makes sense to use the List methods with an integer index. In contrast, a linked list, while also ordered, has slow random access, and it is best traversed with an iterator. It would have been an easy matter to provide two interfaces.

Note

To avoid carrying out random access operations for linked lists, Java 1.4 introduced a tagging interface, RandomAccess. That interface has no methods, but you can use it to test whether a particular collection supports efficient random access:

Click here to view code image

if (c instanceof RandomAccess)

{

use random access algorithm

}

else

{

use sequential access algorithm

}

The Set interface is identical to the Collection interface, but the behavior of the methods is more tightly defined. The add method of a set should reject duplicates. The equals method of a set should be defined so that two sets are identical if they have the same elements, but not necessarily in the same order. The hashCode method should be defined so that two sets with the same elements yield the same hash code.

Why make a separate interface if the method signatures are the same? Conceptually, not all collections are sets. Making a Set interface enables programmers to write methods that accept only sets.

The SortedSet and SortedMap interfaces expose the comparator object used for sorting, and they define methods to obtain views of subsets of the collections. We discuss these in Section 9.5,「Views and Wrappers,」on p. 532.

Finally, Java 6 introduced interfaces NavigableSet and NavigableMap that contain additional methods for searching and traversal in sorted sets and maps. (Ideally, these methods should have simply been included in the SortedSet and SortedMap interface.) The TreeSet and TreeMap classes implement these interfaces.

9.3 Concrete Collections

Table 9.1 shows the collections in the Java library and briefly describes the purpose of each collection class. (For simplicity, we omit the thread-safe collections that will be discussed in Chapter 12.) All classes in Table 9.1 implement the Collection interface, with the exception of the classes with names ending in Map. Those classes implement the Map interface instead. We will discuss maps in Section 9.4,「Maps,」on p. 519.

Figure 9.5 shows the relationships between these classes.

Figure 9.5 Classes in the collections framework

Table 9.1 Concrete Collections in the Java Library

Collection Type

Description

See Page

ArrayList

An indexed sequence that grows and shrinks dynamically

507

LinkedList

An ordered sequence that allows efficient insertion and removal at any location

496

ArrayDeque

A double-ended queue that is implemented as a circular array

516

HashSet

An unordered collection that rejects duplicates

507

TreeSet

A sorted set

511

EnumSet

A set of enumerated type values

529

LinkedHashSet

A set that remembers the order in which elements were inserted

527

PriorityQueue

A collection that allows efficient removal of the smallest element

518

HashMap

A data structure that stores key/value associations

526

TreeMap

A map in which the keys are sorted

519

EnumMap

A map in which the keys belong to an enumerated type

529

LinkedHashMap

A map that remembers the order in which entries were added

527

WeakHashMap

A map with values that can be reclaimed by the garbage collector if they are not used elsewhere

526

IdentityHashMap

A map with keys that are compared by ==, not equals

530

9.3.1 Linked Lists

We already used arrays and their dynamic cousin, the ArrayList class, for many examples in this book. However, arrays and array lists suffer from a major drawback. Removing an element from the middle of an array is expensive since all array elements beyond the removed one must be moved toward the beginning of the array (see Figure 9.6). The same is true for inserting elements in the middle.

Figure 9.6 Removing an element from an array

Another well-known data structure, the linked list, solves this problem. Where an array stores object references in consecutive memory locations, a linked list stores each object in a separate link. Each link also stores a reference to the next link in the sequence. In the Java programming language, all linked lists are actually doubly linked; that is, each link also stores a reference to its predecessor (see Figure 9.7).

Figure 9.7 A doubly linked list

Removing an element from the middle of a linked list is an inexpensive operation—only the links around the element to be removed need to be updated (see Figure 9.8).

Figure 9.8 Removing an element from a linked list

Perhaps you once took a data structures course in which you learned how to implement linked lists. You may have bad memories of tangling up the links when removing or adding elements in the linked list. If so, you will be pleased to learn that the Java collections library supplies a class LinkedList ready for you to use.

The following code example adds three elements and then removes the second one:

Click here to view code image

var staff = new LinkedList<String>();

staff.add("Amy");

staff.add("Bob");

staff.add("Carl");

Iterator<String> iter = staff.iterator();

String first = iter.next(); // visit first element

String second = iter.next(); // visit second element

iter.remove(); // remove last visited element

There is, however, an important difference between linked lists and generic collections. A linked list is an ordered collection in which the position of the objects matters. The LinkedList.add method adds the object to the end of the list. But you will often want to add objects somewhere in the middle of a list. This position-dependent add method is the responsibility of an iterator, since iterators describe positions in collections. Using iterators to add elements makes sense only for collections that have a natural ordering. For example, the set data type that we discuss in the next section does not impose any ordering on its elements. Therefore, there is no add method in the Iterator inter-face. Instead, the collections library supplies a subinterface ListIterator that contains an add method:

Click here to view code image

interface ListIterator<E> extends Iterator<E>

{

void add(E element);

. . .

}

Unlike Collection.add, this method does not return a boolean—it is assumed that the add operation always modifies the list.

In addition, the ListIterator interface has two methods that you can use for traversing a list backwards.

Click here to view code image

E previous()

boolean hasPrevious()

Like the next method, the previous method returns the object that it skipped over.

The listIterator method of the LinkedList class returns an iterator object that implements the ListIterator interface.

Click here to view code image

ListIterator<String> iter = staff.listIterator();

The add method adds the new element before the iterator position. For example, the following code skips past the first element in the linked list and adds "Juliet" before the second element (see Figure 9.9):

Figure 9.9 Adding an element to a linked list

Click here to view code image

var staff = new LinkedList<String>();

staff.add("Amy");

staff.add("Bob");

staff.add("Carl");

ListIterator<String> iter = staff.listIterator();

iter.next(); // skip past first element

iter.add("Juliet");

If you call the add method multiple times, the elements are simply added in the order in which you supplied them. They are all added in turn before the current iterator position.

When you use the add operation with an iterator that was freshly returned from the listIterator method and that points to the beginning of the linked list, the newly added element becomes the new head of the list. When the iterator has passed the last element of the list (that is, when hasNext returns false), the added element becomes the new tail of the list. If the linked list has n elements, there are n + 1 spots for adding a new element. These spots correspond to the n + 1 possible positions of the iterator. For example, if a linked list contains three elements, A, B, and C, there are four possible positions (marked as |) for inserting a new element:

|ABC

A|BC

AB|C

ABC|

Note

Be careful with the「cursor」analogy. The remove operation does not work exactly like the Backspace key. Immediately after a call to next, the remove method indeed removes the element to the left of the iterator, just like the Backspace key would. However, if you have just called previous, the element to the right will be removed. And you can't call remove twice in a row.

Unlike the add method, which depends only on the iterator position, the remove method depends on the iterator state.

Finally, a set method replaces the last element, returned by a call to next or previous, with a new element. For example, the following code replaces the first element of a list with a new value:

Click here to view code image

ListIterator<String> iter = list.listIterator();

String oldValue = iter.next(); // returns first element

iter.set(newValue); // sets first element to newValue

As you might imagine, if an iterator traverses a collection while another iterator is modifying it, confusing situations can occur. For example, suppose an iterator points before an element that another iterator has just removed. The iterator is now invalid and should no longer be used. The linked list iterators have been designed to detect such modifications. If an iterator finds that its collection has been modified by another iterator or by a method of the collection itself, it throws a ConcurrentModificationException. For example, consider the following code:

Click here to view code image

List<String> list = . . .;

ListIterator<String> iter1 = list.listIterator();

ListIterator<String> iter2 = list.listIterator();

iter1.next();

iter1.remove();

iter2.next(); // throws ConcurrentModificationException

The call to iter2.next throws a ConcurrentModificationException since iter2 detects that the list was modified externally.

To avoid concurrent modification exceptions, follow this simple rule: You can attach as many iterators to a collection as you like, provided that all of them are only readers. Alternatively, you can attach a single iterator that can both read and write.

Concurrent modification detection is done in a simple way. The collection keeps track of the number of mutating operations (such as adding and removing elements). Each iterator keeps a separate count of the number of mutating operations that it was responsible for. At the beginning of each iterator method, the iterator simply checks whether its own mutation count equals that of the collection. If not, it throws a ConcurrentModificationException.

Note

There is, however, a curious exception to the detection of concurrent modifications. The linked list only keeps track of structural modifications to the list, such as adding and removing links. The set method does not count as a structural modification. You can attach multiple iterators to a linked list, all of which call set to change the contents of existing links. This capability is required for a number of algorithms in the Collections class that we discuss later in this chapter.

Now you have seen the fundamental methods of the LinkedList class. Use a ListIterator to traverse the elements of the linked list in either direction and to add and remove elements.

As you saw in Section 9.2,「Interfaces in the Collections Framework,」on p. 492, many other useful methods for operating on linked lists are declared in the Collection interface. These are, for the most part, implemented in the AbstractCollection superclass of the LinkedList class. For example, the toString method invokes toString on all elements and produces one long string of the format [A, B, C]. This is handy for debugging. Use the contains method to check whether an element is present in a linked list. For example, the call staff.contains("Harry") returns true if the linked list already contains a string equal to the string "Harry".

The library also supplies a number of methods that are, from a theoretical perspective, somewhat dubious. Linked lists do not support fast random access. If you want to see the nth element of a linked list, you have to start at the beginning and skip past the first n – 1 elements. There is no shortcut. For that reason, programmers don't usually use linked lists in situations where elements need to be accessed by an integer index.

Nevertheless, the LinkedList class supplies a get method that lets you access a particular element:

Click here to view code image

LinkedList<String> list = . . .;

String obj = list.get(n);

Of course, this method is not very efficient. If you find yourself using it, you are probably using a wrong data structure for your problem.

You should never use this illusory random access method to step through a linked list. The code

Click here to view code image

for (int i = 0; i < list.size(); i++)

do something with list.get(i);

is staggeringly inefficient. Each time you look up another element, the search starts again from the beginning of the list. The LinkedList object makes no effort to cache the position information.

Note

The get method has one slight optimization: If the index is at least size() / 2, the search for the element starts at the end of the list.

The list iterator interface also has a method to tell you the index of the current position. In fact, since Java iterators conceptually point between elements, it has two of them: The nextIndex method returns the integer index of the element that would be returned by the next call to next; the previousIndex method returns the index of the element that would be returned by the next call to previous. Of course, that is simply one less than nextIndex. These methods are efficient—an iterator keeps a count of its current position. Finally, if you have an integer index n, then list.listIterator(n) returns an iterator that points just before the element with index n. That is, calling next yields the same element as list.get(n); obtaining that iterator is inefficient.

If you have a linked list with only a handful of elements, you don't have to be overly paranoid about the cost of the get and set methods. But then, why use a linked list in the first place? The only reason to use a linked list is to minimize the cost of insertion and removal in the middle of the list. If you have only a few elements, you can just use an ArrayList.

We recommend that you simply stay away from all methods that use an integer index to denote a position in a linked list. If you want random access into a collection, use an array or ArrayList, not a linked list.

The program in Listing 9.1 puts linked lists to work. It simply creates two lists, merges them, then removes every second element from the second list, and finally tests the removeAll method. We recommend that you trace the program flow and pay special attention to the iterators. You may find it helpful to draw diagrams of the iterator positions, like this:

|ACE |BDFG

A|CE |BDFG

AB|CE B|DFG

. . .

Note that the call

System.out.println(a);

prints all elements in the linked list a by invoking the toString method in AbstractCollection.

Listing 9.1 linkedList/LinkedListTest.java

Click here to view code image

1 package linkedList;

2

3 import java.util.*;

4

5 /**

6 * This program demonstrates operations on linked lists.

7 * @version 1.12 2018-04-10

8 * @author Cay Horstmann

9 */

10 public class LinkedListTest

11 {

12 public static void main(String[] args)

13 {

14 var a = new LinkedList<String>();

15 a.add("Amy");

16 a.add("Carl");

17 a.add("Erica");

18

19 var b = new LinkedList<String>();

20 b.add("Bob");

21 b.add("Doug");

22 b.add("Frances");

23 b.add("Gloria");

24

25 // merge the words from b into a

26

27 ListIterator<String> aIter = a.listIterator();

28 Iterator<String> bIter = b.iterator();

29

30 while (bIter.hasNext())

31 {

32 if (aIter.hasNext()) aIter.next();

33 aIter.add(bIter.next());

34 }

35

36 System.out.println(a);

37

38 // remove every second word from b

39

40 bIter = b.iterator();

41 while (bIter.hasNext())

42 {

43 bIter.next(); // skip one element

44 if (bIter.hasNext())

45 {

46 bIter.next(); // skip next element

47 bIter.remove(); // remove that element

48 }

49 }

50

51 System.out.println(b);

52

53 // bulk operation: remove all words in b from a

54

55 a.removeAll(b);

56

57 System.out.println(a);

58 }

59 }

java.util.List<E> 1.2

ListIterator<E> listIterator()

returns a list iterator for visiting the elements of the list.

ListIterator<E> listIterator(int index)

returns a list iterator for visiting the elements of the list whose first call to next will return the element with the given index.

void add(int i, E element)

adds an element at the specified position.

void addAll(int i, Collection<? extends E> elements)

adds all elements from a collection to the specified position.

E remove(int i)

removes and returns the element at the specified position.

E get(int i)

gets the element at the specified position.

E set(int i, E element)

replaces the element at the specified position with a new element and returns the old element.

int indexOf(Object element)

returns the position of the first occurrence of an element equal to the specified element, or -1 if no matching element is found.

int lastIndexOf(Object element)

returns the position of the last occurrence of an element equal to the specified element, or -1 if no matching element is found.

java.util.ListIterator<E> 1.2

void add(E newElement)

adds an element before the current position.

void set(E newElement)

replaces the last element visited by next or previous with a new element. Throws an IllegalStateException if the list structure was modified since the last call to next or previous.

boolean hasPrevious()

returns true if there is another element to visit when iterating backwards through the list.

E previous()

returns the previous object. Throws a NoSuchElementException if the beginning of the list has been reached.

int nextIndex()

returns the index of the element that would be returned by the next call to next.

int previousIndex()

returns the index of the element that would be returned by the next call to previous.

java.util.LinkedList<E> 1.2

LinkedList()

constructs an empty linked list.

LinkedList(Collection<? extends E> elements)

constructs a linked list and adds all elements from a collection.

void addFirst(E element)

void addLast(E element)

adds an element to the beginning or the end of the list.

E getFirst()

E getLast()

returns the element at the beginning or the end of the list.

E removeFirst()

E removeLast()

removes and returns the element at the beginning or the end of the list.

9.3.2 Array Lists

In the preceding section, you saw the List interface and the LinkedList class that implements it. The List interface describes an ordered collection in which the position of elements matters. There are two protocols for visiting the elements: through an iterator and by random access with methods get and set. The latter is not appropriate for linked lists, but of course get and set make a lot of sense for arrays. The collections library supplies the familiar ArrayList class that also implements the List interface. An ArrayList encapsulates a dynamically reallocated array of objects.

Note

If you are a veteran Java programmer, you may have used the Vector class whenever you need a dynamic array. Why use an ArrayList instead of a Vector? For one simple reason: All methods of the Vector class are synchronized. It is safe to access a Vector object from two threads. But if you access a vector from only a single thread—by far the more common case—your code wastes quite a bit of time with synchronization. In contrast, the ArrayList methods are not synchronized. We recommend that you use an ArrayList instead of a Vector whenever you don't need synchronization.

9.3.3 Hash Sets

Linked lists and arrays let you specify the order in which you want to arrange the elements. However, if you are looking for a particular element and don't remember its position, you need to visit all elements until you find a match. That can be time consuming if the collection contains many elements. If you don't care about the ordering of the elements, there are data structures that let you find elements much faster. The drawback is that those data structures give you no control over the order in which the elements appear. These data structures organize the elements in an order that is convenient for their own purposes.

A well-known data structure for finding objects quickly is the hash table. A hash table computes an integer, called the hash code, for each object. A hash code is somehow derived from the instance fields of an object, preferably in such a way that objects with different data yield different codes. Table 9.2 lists a few examples of hash codes that result from the hashCode method of the String class.

Table 9.2 Hash Codes Resulting from the hashCode Method

String

Hash Code

"Lee"

76268

"lee"

107020

"eel"

100300

If you define your own classes, you are responsible for implementing your own hashCode method—see Chapter 5 for more information. Your implementation needs to be compatible with the equals method: If a.equals(b), then a and b must have the same hash code.

What's important for now is that hash codes can be computed quickly and that the computation depends only on the state of the object that needs to be hashed, not on the other objects in the hash table.

In Java, hash tables are implemented as arrays of linked lists. Each list is called a bucket (see Figure 9.10). To find the place of an object in the table, compute its hash code and reduce it modulo the total number of buckets. The resulting number is the index of the bucket that holds the element. For example, if an object has hash code 76268 and there are 128 buckets, then the object is placed in bucket 108 (because the remainder 76268 % 128 is 108). Perhaps you are lucky and there is no other element in that bucket. Then, you simply insert the element into that bucket. Of course, sometimes you will hit a bucket that is already filled. This is called a hash collision. Then, compare the new object with all objects in that bucket to see if it is already present. If the hash codes are reasonably randomly distributed and the number of buckets is large enough, only a few comparisons should be necessary.

Figure 9.10 A hash table

Note

As of Java 8, the buckets change from linked lists into balanced binary trees when they get full. This improves performance if a hash function was poorly chosen and yields many collisions, or if malicious code tries to flood a hash table with many values that have identical hash codes.

If you want more control over the performance of the hash table, you can specify the initial bucket count. The bucket count gives the number of buckets used to collect objects with identical hash values. If too many elements are inserted into a hash table, the number of collisions increases and retrieval performance suffers.

If you know how many elements, approximately, will eventually be in the table, you can set the bucket count. Typically, you should set it to somewhere between 75% and 150% of the expected element count. Some researchers believe that it is a good idea to make the bucket count a prime number to prevent a clustering of keys. The evidence for this isn't conclusive, however. The standard library uses bucket counts that are powers of 2, with a default of 16. (Any value you supply for the table size is automatically rounded to the next power of 2.)

Of course, you do not always know how many elements you need to store, or your initial guess may be too low. If the hash table gets too full, it needs to be rehashed. To rehash the table, a table with more buckets is created, all elements are inserted into the new table, and the original table is discarded. The load factor determines when a hash table is rehashed. For example, if the load factor is 0.75 (which is the default) and the table is more than 75% full, it is automatically rehashed with twice as many buckets. For most applications, it is reasonable to leave the load factor at 0.75.

Hash tables can be used to implement several important data structures. The simplest among them is the set type. A set is a collection of elements without duplicates. The add method of a set first tries to find the object to be added, and adds it only if it is not yet present.

The Java collections library supplies a HashSet class that implements a set based on a hash table. You add elements with the add method. The contains method is redefined to make a fast lookup to see if an element is already present in the set. It checks only the elements in one bucket and not all elements in the collection.

The hash set iterator visits all buckets in turn. Since hashing scatters the elements around in the table, they are visited in a seemingly random order. You would only use a HashSet if you don't care about the ordering of the elements in the collection.

The sample program at the end of this section (Listing 9.2) reads words from System.in, adds them to a set, and finally prints out the first twenty words in the set. For example, you can feed the program the text from Alice in Wonder-land (which you can obtain from www.gutenberg.org) by launching it from a command shell as

java SetTest < alice30.txt

The program reads all words from the input and adds them to the hash set. It then iterates through the unique words in the set and finally prints out a count. (Alice in Wonderland has 5,909 unique words, including the copyright notice at the beginning.) The words appear in random order.

Caution

Be careful when you mutate set elements. If the hash code of an element were to change, the element would no longer be in the correct position in the data structure.

Listing 9.2 set/SetTest.java

Click here to view code image

1 package set;

2

3 import java.util.*;

4

5 /**

6 * This program uses a set to print all unique words in System.in.

7 * @version 1.12 2015-06-21

8 * @author Cay Horstmann

9 */

10 public class SetTest

11 {

12 public static void main(String[] args)

13 {

14 var words = new HashSet<String>();

15 long totalTime = 0;

16

17 try (var in = new Scanner(System.in))

18 {

19 while (in.hasNext())

20 {

21 String word = in.next();

22 long callTime = System.currentTimeMillis();

23 words.add(word);

24 callTime = System.currentTimeMillis() - callTime;

25 totalTime += callTime;

26 }

27 }

28

29 Iterator<String> iter = words.iterator();

30 for (int i = 1; i <= 20 && iter.hasNext(); i++)

31 System.out.println(iter.next());

32 System.out.println(". . .");

33 System.out.println(words.size() + " distinct words. " + totalTime + " milliseconds.");

34 }

35 }

java.util.HashSet<E> 1.2

HashSet()

constructs an empty hash set.

HashSet(Collection<? extends E> elements)

constructs a hash set and adds all elements from a collection.

HashSet(int initialCapacity)

constructs an empty hash set with the specified capacity (number of buckets).

HashSet(int initialCapacity, float loadFactor)

constructs an empty hash set with the specified capacity and load factor (a number between 0.0 and 1.0 that determines at what percentage of fullness the hash table will be rehashed into a larger one).

java.lang.Object 1.0

int hashCode()

returns a hash code for this object. A hash code can be any integer, positive or negative. The definitions of equals and hashCode must be compatible: If x.equals(y) is true, then x.hashCode() must be the same value as y.hashCode().

9.3.4 Tree Sets

The TreeSet class is similar to the hash set, with one added improvement. A tree set is a sorted collection. You insert elements into the collection in any order. When you iterate through the collection, the values are automatically presented in sorted order. For example, suppose you insert three strings and then visit all elements that you added.

Click here to view code image

var sorter = new TreeSet<String>();

sorter.add("Bob");

sorter.add("Amy");

sorter.add("Carl");

for (String s : sorter) System.out.println(s);

Then, the values are printed in sorted order: Amy Bob Carl. As the name of the class suggests, the sorting is accomplished by a tree data structure. (The current implementation uses a red-black tree. For a detailed description of red-black trees see, for example, Introduction to Algorithms by Thomas Cormen, Charles Leiserson, Ronald Rivest, and Clifford Stein, The MIT Press, 2009.) Every time an element is added to a tree, it is placed into its proper sorting position. Therefore, the iterator always visits the elements in sorted order.

Adding an element to a tree is slower than adding it to a hash table—see Table 9.3 for a comparison. But it is still much faster than checking for duplicates in an array or linked list. If the tree contains n elements, then an average of log2 n comparisons are required to find the correct position for the new element. For example, if the tree already contains 1,000 elements, adding a new element requires about 10 comparisons.

Table 9.3 Adding Elements into Hash and Tree Sets

Document

Total Number of Words

Number of Distinct Words

HashSet

TreeSet

Alice in Wonderland

28195

5909

5 sec

7 sec

The Count of Monte Cristo

466300

37545

75 sec

98 sec

Note

In order to use a tree set, you must be able to compare the elements. The elements must implement the Comparable interface, or you must supply a Comparator when constructing the set. (The Comparable and Comparator interfaces were introduced in Chapter 6.)

If you look back at Table 9.3, you may well wonder if you should always use a tree set instead of a hash set. After all, adding elements does not seem to take much longer, and the elements are automatically sorted. The answer depends on the data that you are collecting. If you don't need the data sorted, there is no reason to pay for the sorting overhead. More important, with some data it is much more difficult to come up with a sort order than a hash function. A hash function only needs to do a reasonably good job of scrambling the objects, whereas a comparison function must tell objects apart with complete precision.

To make this distinction more concrete, consider the task of collecting a set of rectangles. If you use a TreeSet, you need to supply a Comparator<Rectangle>. How do you compare two rectangles? By area? That doesn't work. You can have two different rectangles with different coordinates but the same area. The sort order for a tree must be a total ordering. Any two elements must be comparable, and the comparison can only be zero if the elements are equal. There is such a sort order for rectangles (the lexicographic ordering on its coordinates), but it is unnatural and cumbersome to compute. In contrast, a hash function is already defined for the Rectangle class. It simply hashes the coordinates.

Note

As of Java 6, the TreeSet class implements the NavigableSet interface. That interface adds several convenient methods for locating elements and for backward traversal. See the API notes for details.

The program in Listing 9.3 builds two tree sets of Item objects. The first one is sorted by part number, the default sort order of Item objects. The second set is sorted by description, using a custom comparator.

Listing 9.3 treeSet/TreeSetTest.java

Click here to view code image

1 package treeSet;

2

3 import java.util.*;

4

5 /**

6 * This program sorts a set of Item objects by comparing their descriptions.

7 * @version 1.13 2018-04-10

8 * @author Cay Horstmann

9 */

10 public class TreeSetTest

11 {

12 public static void main(String[] args)

13 {

14 var parts = new TreeSet<Item>();

15 parts.add(new Item("Toaster", 1234));

16 parts.add(new Item("Widget", 4562));

17 parts.add(new Item("Modem", 9912));

18 System.out.println(parts);

19

20 var sortByDescription = new TreeSet<Item>(Comparator.comparing(Item::getDescription));

21

22 sortByDescription.addAll(parts);

23 System.out.println(sortByDescription);

24 }

25 }

Listing 9.4 treeSet/Item.java

Click here to view code image

1 package treeSet;

2

3 import java.util.*;

4

5 /**

6 * An item with a description and a part number.

7 */

8 public class Item implements Comparable<Item>

9 {

10 private String description;

11 private int partNumber;

12

13 /**

14 * Constructs an item.

15 * @param aDescription the item's description

16 * @param aPartNumber the item's part number

17 */

18 public Item(String aDescription, int aPartNumber)

19 {

20 description = aDescription;

21 partNumber = aPartNumber;

22 }

23

24 /**

25 * Gets the description of this item.

26 * @return the description

27 */

28 public String getDescription()

29 {

30 return description;

31 }

32

33 public String toString()

34 {

35 return "[description=" + description + ", partNumber=" + partNumber + "]";

36 }

37

38 public boolean equals(Object otherObject)

39 {

40 if (this == otherObject) return true;

41 if (otherObject == null) return false;

42 if (getClass() != otherObject.getClass()) return false;

43 var other = (Item) otherObject;

44 return Objects.equals(description, other.description) && partNumber == other.partNumber;

45 }

46

47 public int hashCode()

48 {

49 return Objects.hash(description, partNumber);

50 }

51

52 public int compareTo(Item other)

53 {

54 int diff = Integer.compare(partNumber, other.partNumber);

55 return diff != 0 ? diff : description.compareTo(other.description);

56 }

57 }

java.util.TreeSet<E> 1.2

TreeSet()

TreeSet(Comparator<? super E> comparator)

constructs an empty tree set.

TreeSet(Collection<? extends E> elements)

TreeSet(SortedSet<E> s)

constructs a tree set and adds all elements from a collection or sorted set (in the latter case, using the same ordering).

java.util.SortedSet<E> 1.2

Comparator<? super E> comparator()

returns the comparator used for sorting the elements, or null if the elements are compared with the compareTo method of the Comparable interface.

E first()

E last()

returns the smallest or largest element in the sorted set.

java.util.NavigableSet<E> 6

E higher(E value)

E lower(E value)

returns the least element > value or the largest element < value, or null if there is no such element.

E ceiling(E value)

E floor(E value)

returns the least element ≥ value or the largest element ≤ value, or null if there is no such element.

E pollFirst()

E pollLast()

removes and returns the smallest or largest element in this set, or null if the set is empty.

Iterator<E> descendingIterator()

returns an iterator that traverses this set in descending direction.

9.3.5 Queues and Deques

As we already discussed, a queue lets you efficiently add elements at the tail and remove elements from the head. A double-ended queue, or deque, lets you efficiently add or remove elements at the head and tail. Adding elements in the middle is not supported. Java 6 introduced a Deque interface. It is implemented by the ArrayDeque and LinkedList classes, both of which provide deques whose size grows as needed. In Chapter 12, you will see bounded queues and deques.

java.util.Queue<E> 5

boolean add(E element)

boolean offer(E element)

adds the given element to the tail of this queue and returns true, provided the queue is not full. If the queue is full, the first method throws an IllegalStateException, whereas the second method returns false.

E remove()

E poll()

removes and returns the element at the head of this queue, provided the queue is not empty. If the queue is empty, the first method throws a NoSuchElementException, whereas the second method returns null.

E element()

E peek()

returns the element at the head of this queue without removing it, provided the queue is not empty. If the queue is empty, the first method throws a NoSuchElementException, whereas the second method returns null.

java.util.Deque<E> 6

void addFirst(E element)

void addLast(E element)

boolean offerFirst(E element)

boolean offerLast(E element)

adds the given element to the head or tail of this deque. If the deque is full, the first two methods throw an IllegalStateException, whereas the last two methods return false.

E removeFirst()

E removeLast()

E pollFirst()

E pollLast()

removes and returns the element at the head of this deque, provided the deque is not empty. If the deque is empty, the first two methods throw a NoSuchElementException, whereas the last two methods return null.

E getFirst()

E getLast()

E peekFirst()

E peekLast()

returns the element at the head of this deque without removing it, provided the deque is not empty. If the deque is empty, the first two methods throw a NoSuchElementException, whereas the last two methods return null.

java.util.ArrayDeque<E> 6

ArrayDeque()

ArrayDeque(int initialCapacity)

constructs an unbounded deque with an initial capacity of 16 or the given initial capacity.

9.3.6 Priority Queues

A priority queue retrieves elements in sorted order after they were inserted in arbitrary order. That is, whenever you call the remove method, you get the smallest element currently in the priority queue. However, the priority queue does not sort all its elements. If you iterate over the elements, they are not necessarily sorted. The priority queue makes use of an elegant and efficient data structure called a heap. A heap is a self-organizing binary tree in which the add and remove operations cause the smallest element to gravitate to the root, without wasting time on sorting all elements.

Just like a TreeSet, a priority queue can either hold elements of a class that implements the Comparable interface or a Comparator object you supply in the constructor.

A typical use for a priority queue is job scheduling. Each job has a priority. Jobs are added in random order. Whenever a new job can be started, the highest priority job is removed from the queue. (Since it is traditional for priority 1 to be the「highest」priority, the remove operation yields the minimum element.)

Listing 9.5 shows a priority queue in action. Unlike iteration in a TreeSet, the iteration here does not visit the elements in sorted order. However, removal always yields the smallest remaining element.

Listing 9.5 priorityQueue/PriorityQueueTest.java

Click here to view code image

1 package priorityQueue;

2

3 import java.util.*;

4 import java.time.*;

5

6 /**

7 * This program demonstrates the use of a priority queue.

8 * @version 1.02 2015-06-20

9 * @author Cay Horstmann

10 */

11 public class PriorityQueueTest

12 {

13 public static void main(String[] args)

14 {

15 var pq = new PriorityQueue<LocalDate>();

16 pq.add(LocalDate.of(1906, 12, 9)); // G. Hopper

17 pq.add(LocalDate.of(1815, 12, 10)); // A. Lovelace

18 pq.add(LocalDate.of(1903, 12, 3)); // J. von Neumann

19 pq.add(LocalDate.of(1910, 6, 22)); // K. Zuse

20

21 System.out.println("Iterating over elements . . .");

22 for (LocalDate date : pq)

23 System.out.println(date);

24 System.out.println("Removing elements . . .");

25 while (!pq.isEmpty())

26 System.out.println(pq.remove());

27 }

28 }

java.util.PriorityQueue 5

PriorityQueue()

PriorityQueue(int initialCapacity)

constructs a priority queue for storing Comparable objects.

PriorityQueue(int initialCapacity, Comparator<? super E> c)

constructs a priority queue and uses the specified comparator for sorting its elements.

9.4 Maps

A set is a collection that lets you quickly find an existing element. However, to look up an element, you need to have an exact copy of the element to find. That isn't a very common lookup—usually, you have some key information, and you want to look up the associated element. The map data structure serves that purpose. A map stores key/value pairs. You can find a value if you provide the key. For example, you may store a table of employee records, where the keys are the employee IDs and the values are Employee objects. In the following sections, you will learn how to work with maps.

9.4.1 Basic Map Operations

The Java library supplies two general-purpose implementations for maps: HashMap and TreeMap. Both classes implement the Map interface.

A hash map hashes the keys, and a tree map uses an ordering on the keys to organize them in a search tree. The hash or comparison function is applied only to the keys. The values associated with the keys are not hashed or compared.

Should you choose a hash map or a tree map? As with sets, hashing is usually a bit faster, and it is the preferred choice if you don't need to visit the keys in sorted order.

Here is how you set up a hash map for storing employees:

Click here to view code image

var staff = new HashMap<String, Employee>(); // HashMap implements Map

var harry = new Employee("Harry Hacker");

staff.put("987-98-9996", harry);

. . .

Whenever you add an object to a map, you must supply a key as well. In our case, the key is a string, and the corresponding value is an Employee object.

To retrieve an object, you must use (and, therefore, remember) the key.

Click here to view code image

var id = "987-98-9996";

Employee e = staff.get(id); // gets harry

If no information is stored in the map with the particular key specified, get returns null.

The null return value can be inconvenient. Sometimes, you have a good default that can be used for keys that are not present in the map. Then use the getOrDefault method.

Click here to view code image

Map<String, Integer> scores = . . .;

int score = scores.getOrDefault(id, 0); // gets 0 if the id is not present

Keys must be unique. You cannot store two values with the same key. If you call the put method twice with the same key, the second value replaces the first one. In fact, put returns the previous value associated with its key parameter.

The remove method removes an element with a given key from the map. The size method returns the number of entries in the map.

The easiest way of iterating over the keys and values of a map is the forEach method. Provide a lambda expression that receives a key and a value. That expression is invoked for each map entry in turn.

Click here to view code image

scores.forEach((k, v) ->

System.out.println("key=" + k + ", value=" + v));

Listing 9.6 illustrates a map at work. We first add key/value pairs to a map. Then, we remove one key from the map, which removes its associated value as well. Next, we change the value that is associated with a key and call the get method to look up a value. Finally, we iterate through the entry set.

Listing 9.6 map/MapTest.java

Click here to view code image

1 package map;

2

3 import java.util.*;

4

5 /**

6 * This program demonstrates the use of a map with key type String and value type Employee.

7 * @version 1.12 2015-06-21

8 * @author Cay Horstmann

9 */

10 public class MapTest

11 {

12 public static void main(String[] args)

13 {

14 var staff = new HashMap<String, Employee>();

15 staff.put("144-25-5464", new Employee("Amy Lee"));

16 staff.put("567-24-2546", new Employee("Harry Hacker"));

17 staff.put("157-62-7935", new Employee("Gary Cooper"));

18 staff.put("456-62-5527", new Employee("Francesca Cruz"));

19

20 // print all entries

21

22 System.out.println(staff);

23

24 // remove an entry

25

26 staff.remove("567-24-2546");

27

28 // replace an entry

29

30 staff.put("456-62-5527", new Employee("Francesca Miller"));

31

32 // look up a value

33

34 System.out.println(staff.get("157-62-7935"));

35

36 // iterate through all entries

37

38 staff.forEach((k, v) ->

39 System.out.println("key=" + k + ", value=" + v));

40 }

41 }

java.util.Map<K, V> 1.2

V get(Object key)

gets the value associated with the key; returns the object associated with the key, or null if the key is not found in the map. Implementing classes may forbid null keys.

default V getOrDefault(Object key, V defaultValue)

gets the value associated with the key; returns the object associated with the key, or defaultValue if the key is not found in the map.

V put(K key, V value)

puts the association of a key and a value into the map. If the key is already present, the new object replaces the old one previously associated with the key. This method returns the old value of the key, or null if the key was not previously present. Implementing classes may forbid null keys or values.

void putAll(Map<? extends K, ? extends V> entries)

adds all entries from the specified map to this map.

boolean containsKey(Object key)

returns true if the key is present in the map.

boolean containsValue(Object value)

returns true if the value is present in the map.

default void forEach(BiConsumer<? super K,? super V> action) 8

applies the action to all key/value pairs of this map.

java.util.HashMap<K, V> 1.2

HashMap()

HashMap(int initialCapacity)

HashMap(int initialCapacity, float loadFactor)

constructs an empty hash map with the specified capacity and load factor (a number between 0.0 and 1.0 that determines at what percentage of fullness the hash table will be rehashed into a larger one). The default load factor is 0.75.

java.util.TreeMap<K,V> 1.2

TreeMap()

constructs an empty tree map for keys that implement the Comparable interface.

TreeMap(Comparator<? super K> c)

constructs a tree map and uses the specified comparator for sorting its keys.

TreeMap(Map<? extends K, ? extends V> entries)

constructs a tree map and adds all entries from a map.

TreeMap(SortedMap<? extends K, ? extends V> entries)

constructs a tree map, adds all entries from a sorted map, and uses the same element comparator as the given sorted map.

java.util.SortedMap<K, V> 1.2

Comparator<? super K> comparator()

returns the comparator used for sorting the keys, or null if the keys are compared with the compareTo method of the Comparable interface.

K firstKey()

K lastKey()

returns the smallest or largest key in the map.

9.4.2 Updating Map Entries

A tricky part of dealing with maps is updating an entry. Normally, you get the old value associated with a key, update it, and put back the updated value. But you have to worry about the special case of the first occurrence of a key. Consider using a map for counting how often a word occurs in a file. When we see a word, we'd like to increment a counter like this:

Click here to view code image

counts.put(word, counts.get(word) + 1);

That works, except in the case when word is encountered for the first time. Then get returns null, and a NullPointerException occurs.

A simple remedy is to use the getOrDefault method:

Click here to view code image

counts.put(word, counts.getOrDefault(word, 0) + 1);

Another approach is to first call the putIfAbsent method. It only puts a value if the key was previously absent (or mapped to null).

Click here to view code image

counts.putIfAbsent(word, 0);

counts.put(word, counts.get(word) + 1); // now we know that get will succeed

But you can do better than that. The merge method simplifies this common operation. The call

Click here to view code image

counts.merge(word, 1, Integer::sum);

associates word with 1 if the key wasn't previously present, and otherwise combines the previous value and 1, using the Integer::sum function.

The API notes describe other methods for updating map entries that are less commonly used.

java.util.Map<K, V> 1.2

default V merge(K key, V value, BiFunction<? super V,? super V,? extends V> remappingFunction) 8

If key is associated with a non-null value v, applies the function to v and value and either associates key with the result or, if the result is null, removes the key. Otherwise, associates key with value. Returns get(key).

default V compute(K key, BiFunction<? super K,? super V,? extends V> remappingFunction) 8

Applies the function to key and get(key). Either associates key with the result or, if the result is null, removes the key. Returns get(key).

default V computeIfPresent(K key, BiFunction<? super K,? super V,? extends V> remappingFunction) 8

If key is associated with a non-null value v, applies the function to key and v and either associates key with the result or, if the result is null, removes the key. Returns get(key).

default V computeIfAbsent(K key, Function<? super K,? extends V> mappingFunction) 8

Applies the function to key unless key is associated with a non-null value. Either associates key with the result or, if the result is null, removes the key. Returns get(key).

default void replaceAll(BiFunction<? super K,? super V,? extends V> function) 8

Calls the function on all entries. Associates keys with non-null results and removes keys with null results.

default V putIfAbsent(K key, V value) 8

If key is absent or associated with null, associates it with value and returns null. Otherwise returns the associated value.

9.4.3 Map Views

The collections framework does not consider a map itself as a collection. (Other frameworks for data structures consider a map as a collection of key/value pairs, or as a collection of values indexed by the keys.) However, you can obtain views of the map—objects that implement the Collection interface or one of its subinterfaces.

There are three views: the set of keys, the collection of values (which is not a set), and the set of key/value pairs. The keys and key/value pairs form a set because there can be only one copy of a key in a map. The methods

Click here to view code image

Set<K> keySet()

Collection<V> values()

Set<Map.Entry<K, V>> entrySet()

return these three views. (The elements of the entry set are objects of a class implementing the Map.Entry interface.)

Note that the keySet is not a HashSet or TreeSet, but an object of some other class that implements the Set interface. The Set interface extends the Collection interface. Therefore, you can use a keySet as you would use any collection.

For example, you can enumerate all keys of a map:

Click here to view code image

Set<String> keys = map.keySet();

for (String key : keys)

{

do something with key

}

If you want to look at both keys and values, you can avoid value lookups by enumerating the entries. Use the following code skeleton:

Click here to view code image

for (Map.Entry<String, Employee> entry : staff.entrySet())

{

String k = entry.getKey();

Employee v = entry.getValue();

do something with k, v

}

Tip

You can avoid the cumbersome Map.Entry by using a var declaration.

Click here to view code image

for (var entry : map.entrySet())

{

do something with entry.getKey(), entry.getValue()

}

Or simply use the forEach method:

Click here to view code image

map.forEach((k, v) -> {

do something with k, v

});

If you invoke the remove method of the iterator on the key set view, you actually remove the key and its associated value from the map. However, you cannot add an element to the key set view. It makes no sense to add a key without also adding a value. If you try to invoke the add method, it throws an UnsupportedOperationException. The entry set view has the same restriction, even though it would make conceptual sense to add a new key/value pair.

java.util.Map<K, V> 1.2

Set<Map.Entry<K, V>> entrySet()

returns a set view of Map.Entry objects, the key/value pairs in the map. You can remove elements from this set and they are removed from the map, but you cannot add any elements.

Set<K> keySet()

returns a set view of all keys in the map. You can remove elements from this set and the keys and associated values are removed from the map, but you cannot add any elements.

Collection<V> values()

returns a collection view of all values in the map. You can remove elements from this set and the removed value and its key are removed from the map, but you cannot add any elements.

java.util.Map.Entry<K, V> 1.2

K getKey()

V getValue()

returns the key or value of this entry.

V setValue(V newValue)

changes the value in the associated map to the new value and returns the old value.

9.4.4 Weak Hash Maps

The collection class library has several map classes for specialized needs that we briefly discuss in this and the following sections.

The WeakHashMap class was designed to solve an interesting problem. What happens with a value whose key is no longer used anywhere in your program? Suppose the last reference to a key has gone away. Then, there is no longer any way to refer to the value object. But, as no part of the program has the key any more, the key/value pair cannot be removed from the map. Why can't the garbage collector remove it? Isn't it the job of the garbage collector to remove unused objects?

Unfortunately, it isn't quite so simple. The garbage collector traces live objects. As long as the map object is live, all buckets in it are live and won't be reclaimed. Thus, your program should take care to remove unused values from long-lived maps. Or, you can use a WeakHashMap instead. This data structure cooperates with the garbage collector to remove key/value pairs when the only reference to the key is the one from the hash table entry.

Here are the inner workings of this mechanism. The WeakHashMap uses weak references to hold keys. A WeakReference object holds a reference to another object—in our case, a hash table key. Objects of this type are treated in a special way by the garbage collector. Normally, if the garbage collector finds that a particular object has no references to it, it simply reclaims the object. However, if the object is reachable only by a WeakReference, the garbage collector still reclaims the object, but places the weak reference that led to it into a queue. The operations of the WeakHashMap periodically check that queue for newly arrived weak references. The arrival of a weak reference in the queue signifies that the key was no longer used by anyone and has been collected. The WeakHashMap then removes the associated entry.

9.4.5 Linked Hash Sets and Maps

The LinkedHashSet and LinkedHashMap classes remember in which order you inserted items. That way, you can avoid the seemingly random order of items in a hash table. As entries are inserted into the table, they are joined in a doubly linked list (see Figure 9.11).

Figure 9.11 A linked hash table

For example, consider the following map insertions from Listing 9.6:

Click here to view code image

var staff = new LinkedHashMap<String, Employee>();

staff.put("144-25-5464", new Employee("Amy Lee"));

staff.put("567-24-2546", new Employee("Harry Hacker"));

staff.put("157-62-7935", new Employee("Gary Cooper"));

staff.put("456-62-5527", new Employee("Francesca Cruz"));

Then, staff.keySet().iterator() enumerates the keys in this order:

144-25-5464

567-24-2546

157-62-7935

456-62-5527

and staff.values().iterator() enumerates the values in this order:

Amy Lee

Harry Hacker

Gary Cooper

Francesca Cruz

A linked hash map can alternatively use access order, not insertion order, to iterate through the map entries. Every time you call get or put, the affected entry is removed from its current position and placed at the end of the linked list of entries. (Only the position in the linked list of entries is affected, not the hash table bucket. An entry always stays in the bucket that corresponds to the hash code of the key.) To construct such a hash map, call

Click here to view code image

LinkedHashMap<K, V>(initialCapacity, loadFactor, true)

Access order is useful for implementing a「least recently used」discipline for a cache. For example, you may want to keep frequently accessed entries in memory and read less frequently accessed objects from a database. When you don't find an entry in the table, and the table is already pretty full, you can get an iterator into the table and remove the first few elements that it enumerates. Those entries were the least recently used ones.

You can even automate that process. Form a subclass of LinkedHashMap and override the method

Click here to view code image

protected boolean removeEldestEntry(Map.Entry<K, V> eldest)

Adding a new entry then causes the eldest entry to be removed whenever your method returns true. For example, the following cache is kept at a size of at most 100 elements:

Click here to view code image

var cache = new LinkedHashMap<K, V>(128, 0.75F, true)

{

protected boolean removeEldestEntry(Map.Entry<K, V> eldest)

{

return size() > 100;

}

};

Alternatively, you can consider the eldest entry to decide whether to remove it. For example, you may want to check a time stamp stored with the entry.

9.4.6 Enumeration Sets and Maps

The EnumSet is an efficient set implementation with elements that belong to an enumerated type. Since an enumerated type has a finite number of instances, the EnumSet is internally implemented simply as a sequence of bits. A bit is turned on if the corresponding value is present in the set.

The EnumSet class has no public constructors. Use a static factory method to construct the set:

Click here to view code image

enum Weekday { MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY };

EnumSet<Weekday> always = EnumSet.allOf(Weekday.class);

EnumSet<Weekday> never = EnumSet.noneOf(Weekday.class);

EnumSet<Weekday> workday = EnumSet.range(Weekday.MONDAY, Weekday.FRIDAY);

EnumSet<Weekday> mwf = EnumSet.of(Weekday.MONDAY, Weekday.WEDNESDAY, Weekday.FRIDAY);

You can use the usual methods of the Set interface to modify an EnumSet.

An EnumMap is a map with keys that belong to an enumerated type. It is simply and efficiently implemented as an array of values. You need to specify the key type in the constructor:

Click here to view code image

var personInCharge = new EnumMap<Weekday, Employee>(Weekday.class);

Note

In the API documentation for EnumSet, you will see odd-looking type parameters of the form E extends Enum<E>. This simply means「E is an enumerated type.」All enumerated types extend the generic Enum class. For example, Weekday extends Enum<Weekday>.

9.4.7 Identity Hash Maps

The IdentityHashMap has a quite specialized purpose. Here, the hash values for the keys should not be computed by the hashCode method but by the System.identityHashCode method. That's the method that Object.hashCode uses to compute a hash code from the object's memory address. Also, for comparison of objects, the IdentityHashMap uses ==, not equals.

In other words, different key objects are considered distinct even if they have equal contents. This class is useful for implementing object traversal algorithms, such as object serialization, in which you want to keep track of which objects have already been traversed.

java.util.WeakHashMap<K, V> 1.2

WeakHashMap()

WeakHashMap(int initialCapacity)

WeakHashMap(int initialCapacity, float loadFactor)

constructs an empty hash map with the specified capacity and load factor.

java.util.LinkedHashSet<E> 1.4

LinkedHashSet()

LinkedHashSet(int initialCapacity)

LinkedHashSet(int initialCapacity, float loadFactor)

constructs an empty linked hash set with the specified capacity and load factor.

java.util.LinkedHashMap<K, V> 1.4

LinkedHashMap()

LinkedHashMap(int initialCapacity)

LinkedHashMap(int initialCapacity, float loadFactor)

LinkedHashMap(int initialCapacity, float loadFactor, boolean accessOrder)

constructs an empty linked hash map with the specified capacity, load factor, and ordering. The accessOrder parameter is true for access order, false for insertion order.

protected boolean removeEldestEntry(Map.Entry<K, V> eldest)

should be overridden to return true if you want the eldest entry to be removed. The eldest parameter is the entry whose removal is being contemplated. This method is called after an entry has been added to the map. The default implementation returns false—old elements are not removed by default. However, you can redefine this method to selectively return true—for example, if the eldest entry fits a certain condition or if the map exceeds a certain size.

java.util.EnumSet<E extends Enum<E>> 5

static <E extends Enum<E>> EnumSet<E> allOf(Class<E> enumType)

returns a mutable set that contains all values of the given enumerated type.

static <E extends Enum<E>> EnumSet<E> noneOf(Class<E> enumType)

returns a mutable set that is initially empty.

static <E extends Enum<E>> EnumSet<E> range(E from, E to)

returns a mutable set that contains all values between from and to (inclusive).

static <E extends Enum<E>> EnumSet<E> of(E e)

. . .

static <E extends Enum<E>> EnumSet<E> of(E e1, E e2, E e3, E e4, E e5)

static <E extends Enum<E>> EnumSet<E> of(E first, E... rest)

returns a mutable set containing the given elements which must not be null.

java.util.EnumMap<K extends Enum<K>, V> 5

EnumMap(Class<K> keyType)

constructs an empty mutable map whose keys have the given type.

java.util.IdentityHashMap<K, V> 1.4

IdentityHashMap()

IdentityHashMap(int expectedMaxSize)

constructs an empty identity hash map whose capacity is the smallest power of 2 exceeding 1.5 × expectedMaxSize. (The default for expectedMaxSize is 21.)

java.lang.System 1.0

static int identityHashCode(Object obj) 1.1

returns the same hash code (derived from the object's memory address) that Object.hashCode computes, even if the class to which obj belongs has redefined the hashCode method.

9.5 Views and Wrappers

If you look at Figures 9.4 and 9.5, you might think it is overkill to have lots of interfaces and abstract classes to implement a modest number of concrete collection classes. However, these figures don't tell the whole story. By using views, you can obtain other objects that implement the Collection or Map inter-faces. You saw one example of this with the keySet method of the map classes. At first glance, it appears as if the method creates a new set, fills it with all the keys of the map, and returns it. However, that is not the case. Instead, the keySet method returns an object of a class that implements the Set interface and whose methods manipulate the original map. Such a collection is called a view.

The technique of views has a number of useful applications in the collections framework. We will discuss these applications in the following sections.

9.5.1 Small Collections

Java 9 introduces static methods yielding a set or list with given elements, and a map with given key/value pairs.

For example,

Click here to view code image

List<String> names = List.of("Peter", "Paul", "Mary");

Set<Integer> numbers = Set.of(2, 3, 5);

yield a list and a set with three elements. For a map, you specify the keys and values, like this:

Click here to view code image

Map<String, Integer> scores = Map.of("Peter", 2, "Paul", 3, "Mary", 5);

The elements, keys, or values may not be null.

The List and Set interfaces have eleven of methods with zero to ten arguments, and an of method with a variable number of arguments. The specializations are provided for efficiency.

For the Map interface, it is not possible to provide a version with variable arguments since the argument types alternate between the key and value types. There is a static method ofEntries that accepts an arbitrary number of Map.Entry<K, V> objects, which you can create with the static entry method. For example,

Click here to view code image

import static java.util.Map.*;

. . .

Map<String, Integer> scores = ofEntries(

entry("Peter", 2),

entry("Paul", 3),

entry("Mary", 5));

The of and ofEntries methods produce objects of classes that have an instance variable for each element, or that are backed by an array.

These collection objects are unmodifiable. Any attempt to change their contents results in an UnsupportedOperationException.

If you want a mutable collection, you can pass the unmodifiable collection to the constructor:

Click here to view code image

var names = new ArrayList<>(List.of("Peter", "Paul", "Mary"));

The method call

Click here to view code image

Collections.nCopies(n, anObject)

returns an immutable object that implements the List interface and gives the illusion of having n elements, each of which appears as anObject.

For example, the following call creates a List containing 100 strings, all set to "DEFAULT":

Click here to view code image

List<String> settings = Collections.nCopies(100, "DEFAULT");

There is very little storage cost—the object is stored only once.

Note

The of methods were introduced in Java 9. Previously, there was a static Arrays.asList method that returns a list that is mutable but not resizable. That is, you can call set but not add or remove on the list. There are also legacy methods Collections.emptySet and Collections.singleton.

Note

The Collections class contains a number of utility methods with parameters or return values that are collections. Do not confuse it with the Collection interface.

Tip

Java doesn't have a Pair class, and some programmers use a Map.Entry as a poor man's pair. Before Java 9, this was painful—you had to construct a new AbstractMap.SimpleImmutableEntry<>(first, second). Nowadays, you can call Map.entry(first, second).

9.5.2 Subranges

You can form subrange views for a number of collections. For example, suppose you have a list staff and want to extract elements 10 to 19. Use the subList method to obtain a view into the subrange of the list:

Click here to view code image

List<Employee> group2 = staff.subList(10, 20);

The first index is inclusive, the second exclusive—just like the parameters for the substring operation of the String class.

You can apply any operations to the subrange, and they automatically reflect the entire list. For example, you can erase the entire subrange:

Click here to view code image

group2.clear(); // staff reduction

The elements get automatically cleared from the staff list, and group2 becomes empty.

For sorted sets and maps, you use the sort order, not the element position, to form subranges. The SortedSet interface declares three methods:

Click here to view code image

SortedSet<E> subSet(E from, E to)

SortedSet<E> headSet(E to)

SortedSet<E> tailSet(E from)

These return the subsets of all elements that are larger than or equal to from and strictly smaller than to. For sorted maps, the similar methods

Click here to view code image

SortedMap<K, V> subMap(K from, K to)

SortedMap<K, V> headMap(K to)

SortedMap<K, V> tailMap(K from)

return views into the maps consisting of all entries in which the keys fall into the specified ranges.

The NavigableSet interface introduced in Java 6 gives more control over these subrange operations. You can specify whether the bounds are included:

Click here to view code image

NavigableSet<E> subSet(E from, boolean fromInclusive, E to, boolean toInclusive)

NavigableSet<E> headSet(E to, boolean toInclusive)

NavigableSet<E> tailSet(E from, boolean fromInclusive)

9.5.3 Unmodifiable Views

The Collections class has methods that produce unmodifiable views of collections. These views add a runtime check to an existing collection. If an attempt to modify the collection is detected, an exception is thrown and the collection remains untouched.

You obtain unmodifiable views by eight methods:

Click here to view code image

Collections.unmodifiableCollection

Collections.unmodifiableList

Collections.unmodifiableSet

Collections.unmodifiableSortedSet

Collections.unmodifiableNavigableSet

Collections.unmodifiableMap

Collections.unmodifiableSortedMap

Collections.unmodifiableNavigableMap

Each method is defined to work on an interface. For example, Collections.unmodifiableList works with an ArrayList, a LinkedList, or any other class that implements the List interface.

For example, suppose you want to let some part of your code look at, but not touch, the contents of a collection. Here is what you could do:

Click here to view code image

var staff = new LinkedList<String>();

. . .

lookAt(Collections.unmodifiableList(staff));

The Collections.unmodifiableList method returns an object of a class implementing the List interface. Its accessor methods retrieve values from the staff collection. Of course, the lookAt method can call all methods of the List interface, not just the accessors. But all mutator methods (such as add) have been redefined to throw an UnsupportedOperationException instead of forwarding the call to the underlying collection.

The unmodifiable view does not make the collection itself immutable. You can still modify the collection through its original reference (staff, in our case). And you can still call mutator methods on the elements of the collection.

The views wrap the interface and not the actual collection object, so you only have access to those methods that are defined in the interface. For example, the LinkedList class has convenience methods, addFirst and addLast, that are not part of the List interface. These methods are not accessible through the unmodifiable view.

Caution

The unmodifiableCollection method (as well as the synchronizedCollection and checkedCollection methods discussed later in this section) returns a collection whose equals method does not invoke the equals method of the underlying collection. Instead, it inherits the equals method of the Object class, which just tests whether the objects are identical. If you turn a set or list into just a collection, you can no longer test for equal contents. The view acts in this way because equality testing is not well defined at this level of the hierarchy. The views treat the hashCode method in the same way.

However, the unmodifiableSet and unmodifiableList methods use the equals and hashCode methods of the underlying collections.

9.5.4 Synchronized Views

If you access a collection from multiple threads, you need to ensure that the collection is not accidentally damaged. For example, it would be disastrous if one thread tried to add to a hash table while another thread was rehashing the elements.

Instead of implementing thread-safe collection classes, the library designers used the view mechanism to make regular collections thread safe. For example, the static synchronizedMap method in the Collections class can turn any map into a Map with synchronized access methods:

Click here to view code image

var map = Collections.synchronizedMap(new HashMap<String, Employee>());

You can now access the map object from multiple threads. The methods such as get and put are synchronized—each method call must be finished completely before another thread can call another method. We discuss the issue of synchronized access to data structures in greater detail in Chapter 12.

9.5.5 Checked Views

Checked views are intended as debugging support for a problem that can occur with generic types. As explained in Chapter 8, it is actually possible to smuggle elements of the wrong type into a generic collection. For example:

Click here to view code image

var strings = new ArrayList<String>();

ArrayList rawList = strings; // warning only, not an error,

// for compatibility with legacy code

rawList.add(new Date()); // now strings contains a Date object!

The erroneous add command is not detected at runtime. Instead, a class cast exception will happen later when another part of the code calls get and casts the result to a String.

A checked view can detect this problem. Define a safe list as follows:

Click here to view code image

List<String> safeStrings = Collections.checkedList(strings, String.class);

The view's add method checks that the inserted object belongs to the given class and immediately throws a ClassCastException if it does not. The advantage is that the error is reported at the correct location:

Click here to view code image

ArrayList rawList = safeStrings;

rawList.add(new Date()); // checked list throws a ClassCastException

Caution

The checked views are limited by the runtime checks that the virtual machine can carry out. For example, if you have an ArrayList<Pair<String>>, you cannot protect it from inserting a Pair<Date> since the virtual machine has a single「raw」Pair class.

9.5.6 A Note on Optional Operations

A view usually has some restriction—it may be read-only, it may not be able to change the size, or it may support removal but not insertion (as is the case for the key view of a map). A restricted view throws an UnsupportedOperationException if you attempt an inappropriate operation.

In the API documentation for the collection and iterator interfaces, many methods are described as「optional operations.」This seems to be in conflict with the notion of an interface. After all, isn't the purpose of an interface to lay out the methods that a class must implement? Indeed, this arrangement is unsatisfactory from a theoretical perspective. A better solution might have been to design separate interfaces for read-only views and views that can't change the size of a collection. However, that would have tripled the number of interfaces, which the designers of the library found unacceptable.

Should you extend the technique of「optional」methods to your own designs? We think not. Even though collections are used frequently, the coding style for implementing them is not typical for other problem domains. The designers of a collection class library have to resolve a particularly brutal set of conflicting requirements. Users want the library to be easy to learn, convenient to use, completely generic, idiot-proof, and at the same time as efficient as hand-coded algorithms. It is plainly impossible to achieve all these goals simultaneously, or even to come close. But in your own programming problems, you will rarely encounter such an extreme set of constraints. You should be able to find solutions that do not rely on the extreme measure of「optional」interface operations.

java.util.List 1.2

static <E> List<E> of() 9

static <E> List<E> of(E e1) 9

. . .

static <E> List<E> of(E e1, E e2, E e3, E e4, E e5, E e6, E e7, E e8, E e9, E e10) 9

static <E> Set<E> of(E... elements) 9

yields an immutable list of the given elements, which must not be null.

java.util.Set 1.2

static <E> Set<E> of() 9

static <E> Set<E> of(E e1) 9

. . .

static <E> Set<E> of(E e1, E e2, E e3, E e4, E e5, E e6, E e7, E e8, E e9, E e10) 9

static <E> Set<E> of(E... elements) 9

yields an immutable set of the given elements, which must not be null.

java.util.Map 1.2

static <K, V> Map<K, V> of() 9

static <K, V> Map<K, V> of(K k1, V v1) 9

. . .

static <K,V> Map<K,V> of(K k1, V v1, K k2, V v2, K k3, V v3, K k4, V v4, K k5, V v5, K k6, V v6, K k7, V v7, K k8, V v8, K k9, V v9, K k10, V v10) 9

yields an immutable map of the given keys and values, which must not be null.

static <K,V> Map.Entry<K,V> entry(K k, V v) 9

yields an immutable map entry of the given key and value, which must not be null.

static <K,V> Map<K,V> ofEntries(Map.Entry<? extends K,? extends V>... entries) 9

yields an immutable map of the given entries.

java.util.Collections 1.2

static <E> Collection unmodifiableCollection(Collection<E> c)

static <E> List unmodifiableList(List<E> c)

static <E> Set unmodifiableSet(Set<E> c)

static <E> SortedSet unmodifiableSortedSet(SortedSet<E> c)

static <E> SortedSet unmodifiableNavigableSet(NavigableSet<E> c) 8

static <K, V> Map unmodifiableMap(Map<K, V> c)

static <K, V> SortedMap unmodifiableSortedMap(SortedMap<K, V> c)

static <K, V> SortedMap unmodifiableNavigableMap(NavigableMap<K, V> c) 8

constructs a view of the collection; the view's mutator methods throw an UnsupportedOperationException.

static <E> Collection<E> synchronizedCollection(Collection<E> c)

static <E> List synchronizedList(List<E> c)

static <E> Set synchronizedSet(Set<E> c)

static <E> SortedSet synchronizedSortedSet(SortedSet<E> c)

static <E> NavigableSet synchronizedNavigableSet(NavigableSet<E> c) 8

static <K, V> Map<K, V> synchronizedMap(Map<K, V> c)

static <K, V> SortedMap<K, V> synchronizedSortedMap(SortedMap<K, V> c)

static <K, V> NavigableMap<K, V> synchronizedNavigableMap(NavigableMap<K, V> c) 8

constructs a view of the collection; the view's methods are synchronized.

static <E> Collection checkedCollection(Collection<E> c, Class<E> elementType)

static <E> List checkedList(List<E> c, Class<E> elementType)

static <E> Set checkedSet(Set<E> c, Class<E> elementType)

static <E> SortedSet checkedSortedSet(SortedSet<E> c, Class<E> elementType)

static <E> NavigableSet checkedNavigableSet(NavigableSet<E> c, Class<E> elementType) 8

static <K, V> Map checkedMap(Map<K, V> c, Class<K> keyType, Class<V> valueType)

static <K, V> SortedMap checkedSortedMap(SortedMap<K, V> c, Class<K> keyType, Class<V> valueType)

static <K, V> NavigableMap checkedNavigableMap(NavigableMap<K, V> c, Class<K> keyType, Class<V> valueType) 8

static <E> Queue<E> checkedQueue(Queue<E> queue, Class<E> elementType) 8

constructs a view of the collection; the view's methods throw a ClassCastException if an element of the wrong type is inserted.

static <E> List<E> nCopies(int n, E value)

yields an unmodifiable list with n identical values.

static <E> List<E> singletonList(E value)

static <E> Set<E> singleton(E value)

static <K, V> Map<K, V> singletonMap(K key, V value)

yields a singleton list, set, or map. As of Java 9, use one of the of methods instead.

static <E> List<E> emptyList()

static <T> Set<T> emptySet()

static <E> SortedSet<E> emptySortedSet()

static NavigableSet<E> emptyNavigableSet()

static <K,V> Map<K,V> emptyMap()

static <K,V> SortedMap<K,V> emptySortedMap()

static <K,V> NavigableMap<K,V> emptyNavigableMap()

static <T> Enumeration<T> emptyEnumeration()

static <T> Iterator<T> emptyIterator()

static <T> ListIterator<T> emptyListIterator()

yields an empty collection, map, or iterator.

java.util.Arrays 1.2

static <E> List<E> asList(E... array)

returns a list view of the elements in an array that is modifiable but not resizable.

java.util.List<E> 1.2

List<E> subList(int firstIncluded, int firstExcluded)

returns a list view of the elements within a range of positions.

java.util.SortedSet<E> 1.2

SortedSet<E> subSet(E firstIncluded, E firstExcluded)

SortedSet<E> headSet(E firstExcluded)

SortedSet<E> tailSet(E firstIncluded)

returns a view of the elements within a range.

java.util.NavigableSet<E> 6

NavigableSet<E> subSet(E from, boolean fromIncluded, E to, boolean toIncluded)

NavigableSet<E> headSet(E to, boolean toIncluded)

NavigableSet<E> tailSet(E from, boolean fromIncluded)

returns a view of the elements within a range. The boolean flags determine whether the bounds are included in the view.

java.util.SortedMap<K, V> 1.2

SortedMap<K, V> subMap(K firstIncluded, K firstExcluded)

SortedMap<K, V> headMap(K firstExcluded)

SortedMap<K, V> tailMap(K firstIncluded)

returns a map view of the entries whose keys are within a range.

java.util.NavigableMap<K, V> 6

NavigableMap<K, V> subMap(K from, boolean fromIncluded, K to, boolean toIncluded)

NavigableMap<K, V> headMap(K from, boolean fromIncluded)

NavigableMap<K, V> tailMap(K to, boolean toIncluded)

returns a map view of the entries whose keys are within a range. The boolean flags determine whether the bounds are included in the view.

9.6 Algorithms

In addition to implementing collection classes, the Java collections framework also provides a number of useful algorithms. In the following sections, you will see how to use these algorithms and how to write your own algorithms that work well with the collections framework.

9.6.1 Why Generic Algorithms?

Generic collection interfaces have a great advantage—you only need to implement your algorithms once. For example, consider a simple algorithm to compute the maximum element in a collection. Traditionally, programmers would implement such an algorithm as a loop. Here is how you can find the largest element of an array.

Click here to view code image

if (a.length == 0) throw new NoSuchElementException();

T largest = a[0];

for (int i = 1; i < a.length; i++)

if (largest.compareTo(a[i]) < 0)

largest = a[i];

Of course, to find the maximum of an array list, you would write the code slightly differently.

Click here to view code image

if (v.size() == 0) throw new NoSuchElementException();

T largest = v.get(0);

for (int i = 1; i < v.size(); i++)

if (largest.compareTo(v.get(i)) < 0)

largest = v.get(i);

What about a linked list? You don't have efficient random access in a linked list, but you can use an iterator.

Click here to view code image

if (l.isEmpty()) throw new NoSuchElementException();

Iterator<T> iter = l.iterator();

T largest = iter.next();

while (iter.hasNext())

{

T next = iter.next();

if (largest.compareTo(next) < 0)

largest = next;

}

These loops are tedious to write, and just a bit error-prone. Is there an offby-one error? Do the loops work correctly for empty containers? For containers with only one element? You don't want to test and debug this code every time, but you also don't want to implement a whole slew of methods, such as these:

Click here to view code image

static <T extends Comparable> T max(T[] a)

static <T extends Comparable> T max(ArrayList<T> v)

static <T extends Comparable> T max(LinkedList<T> l)

That's where the collection interfaces come in. Think of the minimal collection interface that you need to efficiently carry out the algorithm. Random access with get and set comes higher in the food chain than simple iteration. As you have seen in the computation of the maximum element in a linked list, random access is not required for this task. Computing the maximum can be done simply by iterating through the elements. Therefore, you can implement the max method to take any object that implements the Collection interface.

Click here to view code image

public static <T extends Comparable> T max(Collection<T> c)

{

if (c.isEmpty()) throw new NoSuchElementException();

Iterator<T> iter = c.iterator();

T largest = iter.next();

while (iter.hasNext())

{

T next = iter.next();

if (largest.compareTo(next) < 0)

largest = next;

}

return largest;

}

Now you can compute the maximum of a linked list, an array list, or an array, with a single method.

That's a powerful concept. In fact, the standard C++ library has dozens of useful algorithms, each operating on a generic collection. The Java library is not quite so rich, but it does contain the basics: sorting, binary search, and some utility algorithms.

9.6.2 Sorting and Shuffling

Computer old-timers will sometimes reminisce about how they had to use punched cards and to actually program, by hand, algorithms for sorting. Nowadays, of course, sorting algorithms are part of the standard library for most programming languages, and the Java programming language is no exception.

The sort method in the Collections class sorts a collection that implements the

Click here to view code image

var staff = new LinkedList<String>();

fill collection

Collections.sort(staff);

This method assumes that the list elements implement the Comparable interface. If you want to sort the list in some other way, you can use the sort method of the List interface and pass a Comparator object. Here is how you can sort a list of employees by salary:

Click here to view code image

staff.sort(Comparator.comparingDouble(Employee::getSalary));

If you want to sort a list in descending order, use the static convenience method Comparator.reverseOrder(). It returns a comparator that returns b.compareTo(a). For example,

Click here to view code image

staff.sort(Comparator.reverseOrder())

sorts the elements in the list staff in reverse order, according to the ordering given by the compareTo method of the element type. Similarly,

Click here to view code image

staff.sort(Comparator.comparingDouble(Employee::getSalary).reversed())

sorts by descending salary.

You may wonder how the sort method sorts a list. Typically, when you look at a sorting algorithm in a book on algorithms, it is presented for arrays and uses random element access. However, random access in a linked list is inefficient. You can actually sort linked lists efficiently by using a form of merge sort. However, the implementation in the Java programming language does not do that. It simply dumps all elements into an array, sorts the array, and then copies the sorted sequence back into the list.

The sort algorithm used in the collections library is a bit slower than Quick-Sort, the traditional choice for a general-purpose sorting algorithm. However, it has one major advantage: It is stable, that is, it doesn't switch equal elements. Why do you care about the order of equal elements? Here is a common scenario. Suppose you have an employee list that you already sorted by name. Now you sort by salary. What happens to employees with equal salary? With a stable sort, the ordering by name is preserved. In other words, the outcome is a list that is sorted first by salary, then by name.

Collections need not implement all of their「optional」methods, so all methods that receive collection parameters must describe when it is safe to pass a collection to an algorithm. For example, you clearly cannot pass an unmodifiableList list to the sort algorithm. What kind of list can you pass? According to the documentation, the list must be modifiable but need not be resizable.

The terms are defined as follows:

A list is modifiable if it supports the set method.

A list is resizable if it supports the add and remove operations.

The Collections class has an algorithm shuffle that does the opposite of sorting—it randomly permutes the order of the elements in a list. For example:

Click here to view code image

ArrayList<Card> cards = . . .;

Collections.shuffle(cards);

If you supply a list that does not implement the RandomAccess interface, the shuffle method copies the elements into an array, shuffles the array, and copies the shuffled elements back into the list.

The program in Listing 9.7 fills an array list with 49 Integer objects containing the numbers 1 through 49. It then randomly shuffles the list and selects the first six values from the shuffled list. Finally, it sorts the selected values and prints them.

Listing 9.7 shuffle/ShuffleTest.java

Click here to view code image

1 package shuffle;

2

3 import java.util.*;

4

5 /**

6 * This program demonstrates the random shuffle and sort algorithms.

7 * @version 1.12 2018-04-10

8 * @author Cay Horstmann

9 */

10 public class ShuffleTest

11 {

12 public static void main(String[] args)

13 {

14 var numbers = new ArrayList<Integer>();

15 for (int i = 1; i <= 49; i++)

16 numbers.add(i);

17 Collections.shuffle(numbers);

18 List<Integer> winningCombination = numbers.subList(0, 6);

19 Collections.sort(winningCombination);

20 System.out.println(winningCombination);

21 }

22 }

java.util.Collections 1.2

static <T extends Comparable<? super T>> void sort(List<T> elements)

sorts the elements in the list, using a stable sort algorithm. The algorithm is guaranteed to run in O(n log n) time, where n is the length of the list.

static void shuffle(List<?> elements)

static void shuffle(List<?> elements, Random r)

randomly shuffles the elements in the list. This algorithm runs in O(n a(n)) time, where n is the length of the list and a(n) is the average time to access an element.

java.util.List<E> 1.2

default void sort(Comparator<? super T> comparator) 8

Sorts this list, using the given comparator.

java.util.Comparator<T> 1.2

static <T extends Comparable<? super T>> Comparator<T> reverseOrder() 8

Yields a comparator that reverses the ordering provided by the Comparable interface.

default Comparator<T> reversed() 8

Yields a comparator that reverses the ordering provided by this comparator.

9.6.3 Binary Search

To find an object in an array, you normally visit all elements until you find a match. However, if the array is sorted, you can look at the middle element and check whether it is larger than the element that you are trying to find. If so, keep looking in the first half of the array; otherwise, look in the second half. That cuts the problem in half, and you keep going in the same way. For example, if the array has 1024 elements, you will locate the match (or confirm that there is none) after 10 steps, whereas a linear search would have taken you an average of 512 steps if the element is present, and 1024 steps to confirm that it is not.

The binarySearch of the Collections class implements this algorithm. Note that the collection must already be sorted, or the algorithm will return the wrong answer. To find an element, supply the collection (which must implement the List interface—more on that in the note below) and the element to be located. If the collection is not sorted by the compareTo element of the Comparable interface, supply a comparator object as well.

Click here to view code image

i = Collections.binarySearch(c, element);

i = Collections.binarySearch(c, element, comparator);

A non-negative return value from the binarySearch method denotes the index of the matching object. That is, c.get(i) is equal to element under the comparison order. If the value is negative, then there is no matching element. However, you can use the return value to compute the location where you should insert element into the collection to keep it sorted. The insertion location is

insertionPoint = -i - 1;

It isn't simply -i because then the value of 0 would be ambiguous. In other words, the operation

Click here to view code image

if (i < 0)

c.add(-i - 1, element);

adds the element in the correct place.

To be worthwhile, binary search requires random access. If you have to iterate one by one through half of a linked list to find the middle element, you have lost all advantage of the binary search. Therefore, the binarySearch algorithm reverts to a linear search if you give it a linked list.

java.util.Collections 1.2

static <T extends Comparable<? super T>> int binarySearch(List<T> elements, T key)

static <T> int binarySearch(List<T> elements, T key, Comparator<? super T> c)

searches for a key in a sorted list, using a binary search if the element type implements the RandomAccess interface, and a linear search in all other cases. The methods are guaranteed to run in O(a(n) log n) time, where n is the length of the list and a(n) is the average time to access an element. The methods return either the index of the key in the list, or a negative value i if the key is not present in the list. In that case, the key should be inserted at index -i - 1 for the list to stay sorted.

9.6.4 Simple Algorithms

The Collections class contains several simple but useful algorithms. Among them is the example from the beginning of this section—finding the maximum value of a collection. Others include copying elements from one list to another, filling a container with a constant value, and reversing a list.

Why supply such simple algorithms in the standard library? Surely most programmers could easily implement them with simple loops. We like the algorithms because they make life easier for the programmer reading the code. When you read a loop that was implemented by someone else, you have to decipher the original programmer's intentions. For example, look at this loop:

Click here to view code image

for (int i = 0; i < words.size(); i++)

if (words.get(i).equals("C++")) words.set(i, "Java");

Now compare the loop with the call

Click here to view code image

Collections.replaceAll(words, "C++", "Java");

When you see the method call, you know right away what the code does.

The API notes at the end of this section describe the simple algorithms in the Collections class.

The default methods Collection.removeIf and List.replaceAll that are just a bit more complex. You provide a lambda expression to test or transform elements. For example, here we remove all short words and change the remaining ones to lowercase:

Click here to view code image

words.removeIf(w -> w.length() <= 3);

words.replaceAll(String::toLowerCase);

java.util.Collections 1.2

static <T extends Comparable<? super T>> T min(Collection<T> elements)

static <T extends Comparable<? super T>> T max(Collection<T> elements)

static <T> min(Collection<T> elements, Comparator<? super T> c)

static <T> max(Collection<T> elements, Comparator<? super T> c)

returns the smallest or largest element in the collection. (The parameter bounds are simplified for clarity.)

static <T> void copy(List<? super T> to, List<T> from)

copies all elements from a source list to the same positions in the target list. The target list must be at least as long as the source list.

static <T> void fill(List<? super T> l, T value)

sets all positions of a list to the same value.

static <T> boolean addAll(Collection<? super T> c, T... values) 5

adds all values to the given collection and returns true if the collection changed as a result.

static <T> boolean replaceAll(List<T> l, T oldValue, T newValue) 1.4

replaces all elements equal to oldValue with newValue.

static int indexOfSubList(List<?> l, List<?> s) 1.4

static int lastIndexOfSubList(List<?> l, List<?> s) 1.4

returns the index of the first or last sublist of l equaling s, or -1 if no sublist of l equals s. For example, if l is [s, t, a, r] and s is [t, a, r], then both methods return the index 1.

static void swap(List<?> l, int i, int j) 1.4

swaps the elements at the given offsets.

static void reverse(List<?> l)

reverses the order of the elements in a list. For example, reversing the list [t, a, r] yields the list [r, a, t]. This method runs in O(n) time, where n is the length of the list.

static void rotate(List<?> l, int d) 1.4

rotates the elements in the list, moving the entry with index i to position (i + d) % l.size(). For example, rotating the list [t, a, r] by 2 yields the list [a, r, t]. This method runs in O(n) time, where n is the length of the list.

static int frequency(Collection<?> c, Object o) 5

returns the count of elements in c that equal the object o.

boolean disjoint(Collection<?> c1, Collection<?> c2) 5

returns true if the collections have no elements in common.

java.util.Collection<T> 1.2

default boolean removeIf(Predicate<? super E> filter) 8

removes all matching elements.

java.util.List<E> 1.2

default void replaceAll(UnaryOperator<E> op) 8

applies the operation to all elements of this list.

9.6.5 Bulk Operations

There are several operations that copy or remove elements「in bulk.」The call

coll1.removeAll(coll2);

removes all elements from coll1 that are present in coll2. Conversely,

coll1.retainAll(coll2);

removes all elements from coll1 that are not present in coll2. Here is a typical application.

Suppose you want to find the intersection of two sets—the elements that two sets have in common. First, make a new set to hold the result.

Click here to view code image

var result = new HashSet<String>(firstSet);

Here, we use the fact that every collection has a constructor whose parameter is another collection that holds the initialization values.

Now, use the retainAll method:

result.retainAll(secondSet);

It retains all elements that occur in both sets. You have formed the intersection without programming a loop.

You can carry this idea further and apply a bulk operation to a view. For example, suppose you have a map that maps employee IDs to employee objects and you have a set of the IDs of all employees that are to be terminated.

Click here to view code image

Map<String, Employee> staffMap = . . .;

Set<String> terminatedIDs = . . .;

Simply form the key set and remove all IDs of terminated employees.

Click here to view code image

staffMap.keySet().removeAll(terminatedIDs);

Since the key set is a view into the map, the keys and associated employee names are automatically removed from the map.

By using a subrange view, you can restrict bulk operations to sublists and subsets. For example, suppose you want to add the first ten elements of a list to another container. Form a sublist to pick out the first ten:

Click here to view code image

relocated.addAll(staff.subList(0, 10));

The subrange can also be a target of a mutating operation.

Click here to view code image

staff.subList(0, 10).clear();

9.6.6 Converting between Collections and Arrays

Large portions of the Java platform API were designed before the collections framework was created. As a result, you will occasionally need to translate between traditional arrays and the more modern collections.

If you have an array that you need to turn into a collection, the List.of wrapper serves this purpose. For example:

Click here to view code image

String[] values = . . .;

var staff = new HashSet<>(List.of(values));

Obtaining an array from a collection is a bit trickier. Of course, you can use the toArray method:

Click here to view code image

Object[] values = staff.toArray();

But the result is an array of objects. Even if you know that your collection contained objects of a specific type, you cannot use a cast:

Click here to view code image

String[] values = (String[]) staff.toArray(); // ERROR

The array returned by the toArray method was created as an Object[] array, and you cannot change its type. Instead, use a variant of the toArray method and give it an array of length 0 of the type that you'd like. The returned array is then created as the same array type:

Click here to view code image

String[] values = staff.toArray(new String[0]);

If you like, you can construct the array to have the correct size:

Click here to view code image

staff.toArray(new String[staff.size()]);

In this case, no new array is created.

Note

You may wonder why you can't simply pass a Class object (such as String.class) to the toArray method. However, this method does「double duty」—both to fill an existing array (provided it is long enough) and to create a new array.

9.6.7 Writing Your Own Algorithms

If you write your own algorithm (or, in fact, any method that has a collection as a parameter), you should work with interfaces, not concrete implementations, whenever possible. For example, suppose you want to process items. Of course, you can implement a method like this:

Click here to view code image

public void processItems(ArrayList<Item> items)

{

for (Item item : items)

do something with item

}

However, you now constrained the caller of your method—the caller must supply the items in an ArrayList. If the items happen to be in another collection, they first need to be repackaged. It is much better to accept a more general collection.

You should ask yourself this: What is the most general collection interface that can do the job? Do you care about the order? Then you should accept a List. But if the order doesn't matter, you can accept collections of any kind:

Click here to view code image

public void processItems(Collection<Item> items)

{

for (Item item : items)

do something with item

}

Now, anyone can call this method with an ArrayList or a LinkedList, or even with an array wrapped with the List.of wrapper.

Tip

In this case, you can do even better by accepting an Iterable<Item>. The Iterable interface has a single abstract method iterator which the enhanced for loop uses behind the scenes. The Collection interface extends Iterable.

Conversely, if your method returns multiple elements, you don't want to constrain yourself against future improvements. For example, consider

Click here to view code image

public ArrayList<Item> lookupItems(. . .)

{

var result = new ArrayList<Item>();

. . .

return result;

}

This method promises to return an ArrayList, even though the caller almost certainly doesn't care what kind of lists it is. If instead you return a List, you can at any time add a branch that returns an empty or singleton list by calling List.of.

Note

If it is such a good idea to use collection interfaces as parameter and return type, why doesn't the Java library follow this rule consistently? For example, the JComboBox class has two constructors:

JComboBox(Object[] items)

JComboBox(Vector<?> items)

The reason is simply timing. The Swing library was created before the collections library.

9.7 Legacy Collections

A number of「legacy」container classes have been present since the first release of Java, before there was a collections framework.

They have been integrated into the collections framework—see Figure 9.12. We briefly introduce them in the following sections.

Figure 9.12 Legacy classes in the collections framework

9.7.1 The Hashtable Class

The classic Hashtable class serves the same purpose as the HashMap class and has essentially the same interface. Just like methods of the Vector class, the Hashtable methods are synchronized. If you do not require compatibility with legacy code, you should use a HashMap instead. If you need concurrent access, use a ConcurrentHashMap—see Chapter 12.

9.7.2 Enumerations

The legacy collections use the Enumeration interface for traversing sequences of elements. The Enumeration interface has two methods, hasMoreElements and nextElement. These are entirely analogous to the hasNext and next methods of the Iterator interface.

If you find this interface with legacy classes, you can use Collections.list to collect the elements in an ArrayList. For example, the LogManager class is only willing to reveal logger names as an Enumeration. Here is how you can get them all:

Click here to view code image

ArrayList<String> loggerNames = Collections.list(LogManager.getLoggerNames());

Alternatively, as of Java 9, you can turn an enumeration into an iterator:

Click here to view code image

LogManager.getLoggerNames().asIterator().forEachRemaining(n -> { . . . });

You will occasionally encounter a legacy method that expects an enumeration parameter. The static method Collections.enumeration yields an enumeration object that enumerates the elements in the collection. For example:

Click here to view code image

List<InputStream> streams = . . .;

var in = new SequenceInputStream(Collections.enumeration(streams));

// the SequenceInputStream constructor expects an enumeration

Note

In C++, it is quite common to use iterators as parameters. Fortunately, on the Java platform, very few programmers use this idiom. It is much smarter to pass around the collection than to pass an iterator. The collection object is more useful. The recipients can always obtain the iterator from the collection when they need to do so, plus they have all the collection methods at their disposal. However, you will find enumerations in some legacy code because they were the only available mechanism for generic collections until the collections framework appeared in Java 1.2.

java.util.Enumeration<E> 1.0

boolean hasMoreElements()

returns true if there are more elements yet to be inspected.

E nextElement()

returns the next element to be inspected. Do not call this method if hasMoreElements() returned false.

default Iterator<E> asIterator() 9

yields an iterator that iterates over the enumerated elements.

java.util.Collections 1.2

static <T> Enumeration<T> enumeration(Collection<T> c)

returns an enumeration that enumerates the elements of c.

public static <T> ArrayList<T> list(Enumeration<T> e)

returns an array list containing the elements enumerated by e.

9.7.3 Property Maps

A property map is a map structure of a special type. It has three particular characteristics:

The keys and values are strings.

The map can easily be saved to a file and loaded from a file.

There is a secondary table for default values.

The Java platform class that implements a property map is called Properties. Property maps are useful in specifying configuration options for programs. For example:

Click here to view code image

var settings = new Properties();

settings.setProperty("width", "600.0");

settings.setProperty("filename", "/home/cay/books/cj11/code/v1ch11/raven.html");

Use the store method to save map list of properties to a file. Here, we just save the property map in the file program.properties. The second argument is a comment that is included in the file.

Click here to view code image

var out = new FileOutputStream("program.properties");

settings.store(out, "Program Properties");

The sample set gives the following output:

Click here to view code image

#Program Properties

#Sun Dec 31 12:54:19 PST 2017

top=227.0

left=1286.0

width=423.0

height=547.0

filename=/home/cay/books/cj11/code/v1ch11/raven.html

To load the properties from a file, use

Click here to view code image

var in = new FileInputStream("program.properties");

settings.load(in);

The System.getProperties method yields a Properties object to describe system information. For example, the home directory has the key "user.home". You can read it with the getProperties method that yields the key as a string:

Click here to view code image

String userDir = System.getProperty("user.home");

Caution

For historical reasons, the Properties class implements Map<Object, Object>. Therefore, you can use the get and put methods of the Map interface. But the get method returns the type Object, and the put method allows you to insert any object. It is best to stick with the getProperty and setProperty methods that work with strings, not objects.

To get the Java version of the virtual machine, look up the "java.version" property. You get a string such as "9.0.1" (or "1.8.0" for Java 8.)

Tip

As you can see, the version numbering changed in Java 9. This seemingly small change broke a good number of tools that had relied on the old format. If you parse the version string, be sure to read JEP 322 at http://openjdk.java.net/jeps/322 to see how version strings will be formatted in the future—or at least, until the numbering scheme changes again.

The Properties class has two mechanisms for providing defaults. First, whenever you look up the value of a string, you can specify a default that should be used automatically when the key is not present.

Click here to view code image

String filename = settings.getProperty("filename", "");

If there is a "filename" property in the property map, filename is set to that string. Otherwise, filename is set to the empty string.

If you find it too tedious to specify the default in every call to getProperty, you can pack all the defaults into a secondary property map and supply that map in the constructor of your primary property map.

Click here to view code image

var defaultSettings = new Properties();

defaultSettings.setProperty("width", "600");

defaultSettings.setProperty("height", "400");

defaultSettings.setProperty("filename", "");

. . .

var settings = new Properties(defaultSettings);

Yes, you can even specify defaults to defaults if you give another property map parameter to the defaultSettings constructor, but it is not something one would normally do.

The companion code has a sample program that shows how you can use properties for storing and loading program state. The program uses the ImageViewer program from Chapter 2 and remembers the frame position, size, and last loaded file. Run the program, load a file, and move and resize the window. Then close the program and reopen it to see that it remembers your file and your favorite window placement. You can also manually edit the file .corejava/ImageViewer.properties in your home directory.

Note

Prior to Java 9, properties files used the 7-bit ASCII encoding. Nowadays, they use UTF-8.

Properties are simple tables without a hierarchical structure. It is common to introduce a fake hierarchy with key names such as window.main.color, window.main.title, and so on. But the Properties class has no methods that help organize such a hierarchy. If you store complex configuration information, you should use the Preferences class instead—see Chapter 10.

java.util.Properties 1.0

Properties()

creates an empty property map.

Properties(Properties defaults)

creates an empty property map with a set of defaults.

String getProperty(String key)

gets a property. Returns the string associated with the key, or the string associated with the key in the default table if it wasn't present in the table, or null if the key wasn't present in the default table either.

String getProperty(String key, String defaultValue)

gets a property with a default value if the key is not found. Returns the string associated with the key, or the default string if it wasn't present in the table.

Object setProperty(String key, String value)

sets a property. Returns the previously set value of the given key.

void load(InputStream in) throws IOException

loads a property map from an input stream.

void store(OutputStream out, String header) 1.2

saves a property map to an output stream. The header in the first line of the stored file.

java.lang.System 1.0

Properties getProperties()

retrieves all system properties. The application must have permission to retrieve all properties, or a security exception is thrown.

String getProperty(String key)

retrieves the system property with the given key name. The application must have permission to retrieve the property, or a security exception is thrown. The following properties can always be retrieved:

java.version

java.vendor

java.vendor.url

java.home

java.class.path

java.library.path

java.class.version

os.name

os.version

os.arch

file.separator

path.separator

line.separator

java.io.tempdir

user.name

user.home

user.dir

java.compiler

java.specification.version

java.specification.vendor

java.specification.name

java.vm.specification.version

java.vm.specification.vendor

java.vm.specification.name

java.vm.version

java.vm.vendor

java.vm.name

9.7.4 Stacks

Since version 1.0, the standard library had a Stack class with the familiar push and pop methods. However, the Stack class extends the Vector class, which is not satisfactory from a theoretical perspective—you can apply such un-stack-like operations as insert and remove to insert and remove values anywhere, not just at the top of the stack.

java.util.Stack<E> 1.0

E push(E item)

pushes item onto the stack and returns item.

E pop()

pops and returns the top item of the stack. Don't call this method if the stack is empty.

E peek()

returns the top of the stack without popping it. Don't call this method if the stack is empty.

9.7.5 Bit Sets

The Java platform's BitSet class stores a sequence of bits. (It is not a set in the mathematical sense—bit vector or bit array would have been more appropriate terms.) Use a bit set if you need to store a sequence of bits (for example, flags) efficiently. A bit set packs the bits into bytes, so it is far more efficient to use a bit set than an ArrayList of Boolean objects.

The BitSet class gives you a convenient interface for reading, setting, and resetting individual bits. Using this interface avoids the masking and other bit-fiddling operations that are necessary if you store bits in int or long variables.

For example, for a BitSet named bucketOfBits,

bucketOfBits.get(i)

returns true if the ith bit is on, and false otherwise. Similarly,

bucketOfBits.set(i)

turns the ith bit on. Finally,

bucketOfBits.clear(i)

turns the ith bit off.

C++ Note

The C++ bitset template has the same functionality as the Java platform BitSet.

java.util.BitSet 1.0

BitSet(int initialCapacity)

constructs a bit set.

int length()

returns the「logical length」of the bit set: 1 plus the index of the highest set bit.

boolean get(int bit)

gets a bit.

void set(int bit)

sets a bit.

void clear(int bit)

clears a bit.

void and(BitSet set)

logically ANDs this bit set with another.

void or(BitSet set)

logically ORs this bit set with another.

void xor(BitSet set)

logically XORs this bit set with another.

void andNot(BitSet set)

clears all bits in this bit set that are set in the other bit set.

As an example of using bit sets, we want to show you an implementation of the「sieve of Eratosthenes」algorithm for finding prime numbers. (A prime number is a number like 2, 3, or 5 that is divisible only by itself and 1, and the sieve of Eratosthenes was one of the first methods discovered to enumerate these fundamental building blocks.) This isn't a terribly good algorithm for finding the primes, but for some reason it has become a popular benchmark for compiler performance. (It isn't a good benchmark either, because it mainly tests bit operations.)

Oh well, we bow to tradition and present an implementation. This program counts all prime numbers between 2 and 2,000,000. (There are 148,933 primes in this interval, so you probably don't want to print them all out.)

Without going into too many details of this program, the idea is to march through a bit set with 2 million bits. First, we turn on all the bits. After that, we turn off the bits that are multiples of numbers known to be prime. The positions of the bits that remain after this process are themselves prime numbers. Listing 9.8 lists this program in the Java programming language, and Listing 9.9 is the C++ code.

Note

Even though the sieve isn't a good benchmark, we couldn't resist timing the two implementations of the algorithm. Here are the timing results with a i7-8550U processor and 16 GB of RAM, running Ubuntu 17.10:

C++ (g++ 7.2.0): 173 milliseconds

Java (Java 9.0.1): 41 milliseconds

We have run this test for ten editions of Core Java, and in the last six editions, Java easily beat C++. In all fairness, if one cranks up the optimization level in the C++ compiler, it beats Java with a time of 34 milliseconds. Java could only match that if the program ran long enough to trigger the Hotspot just-in-time compiler.

Listing 9.8 sieve/Sieve.java

Click here to view code image

1 package sieve;

2

3 import java.util.*;

4

5 /**

6 * This program runs the Sieve of Erathostenes benchmark. It computes all primes

7 * up to 2,000,000.

8 * @version 1.21 2004-08-03

9 * @author Cay Horstmann

10 */

11 public class Sieve

12 {

13 public static void main(String[] s)

14 {

15 int n = 2000000;

16 long start = System.currentTimeMillis();

17 var bitSet = new BitSet(n + 1);

18 int count = 0;

19 int i;

20 for (i = 2; i <= n; i++)

21 bitSet.set(i);

22 i = 2;

23 while (i * i <= n)

24 {

25 if (bitSet.get(i))

26 {

27 count++;

28 int k = 2 * i;

29 while (k <= n)

30 {

31 bitSet.clear(k);

32 k += i;

33 }

34 }

35 i++;

36 }

37 while (i <= n)

38 {

39 if (bitSet.get(i)) count++;

40 i++;

41 }

42 long end = System.currentTimeMillis();

43 System.out.println(count + " primes");

44 System.out.println((end - start) + " milliseconds");

45 }

46 }

Listing 9.9 sieve/sieve.cpp

Click here to view code image

1 /**

2 @version 1.21 2004-08-03

3 @author Cay Horstmann

4 */

5

6 #include <bitset>

7 #include <iostream>

8 #include <ctime>

9

10 using namespace std;

11

12 int main()

13 {

14 const int N = 2000000;

15 clock_t cstart = clock();

16

17 bitset<N + 1> b;

18 int count = 0;

19 int i;

20 for (i = 2; i <= N; i++)

21 b.set(i);

22 i = 2;

23 while (i * i <= N)

24 {

25 if (b.test(i))

26 {

27 count++;

28 int k = 2 * i;

29 while (k <= N)

30 {

31 b.reset(k);

32 k += i;

33 }

34 }

35 i++;

36 }

37 while (i <= N)

38 {

39 if (b.test(i))

40 count++;

41 i++;

42 }

43

44 clock_t cend = clock();

45 double millis = 1000.0 * (cend - cstart) / CLOCKS_PER_SEC;

46

47 cout << count << " primes\n" << millis << " milliseconds\n";

48

49 return 0;

50 }

This completes our tour through the Java collections framework. As you have seen, the Java library offers a wide variety of collection classes for your programming needs. In the next chapter, you will learn how to write graphical user interfaces.

Chapter 10

Graphical User Interface Programming

In this chapter

10.1 A History of Java User Interface Toolkits

10.2 Displaying Frames

10.3 Displaying Information in a Component

10.4 Event Handling


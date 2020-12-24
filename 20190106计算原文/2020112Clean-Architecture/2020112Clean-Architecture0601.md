# 0601. Functional Programming

In many ways, the concepts of functional programming predate programming itself. This paradigm is strongly based on the l-calculus invented by Alonzo Church in the 1930s.

Squares  of  Integers

To explain what functional programming is, it’s best to examine some examples. Let’s investigate a simple problem: printing the squares of the first 25 integers.

In a language like Java, we might write the following:

public class Squint {

public static void main(String args[]) {

for (int i=0; i<25; i++)

System.out.println(i*i);

}

}

In a language like Clojure, which is a derivative of Lisp, and is functional, we might implement this same program as follows:

(println (take 25 (map (fn [x] (* x x)) (range))))

If you don’t know Lisp, then this might look a little strange. So let me reformat it a bit and add some comments.

(println ;___________________ Print

(take 25 ;_________________ the first 25

(map (fn [x] (* x x)) ;__ squares

(range)))) ;___________ of Integers

It should be clear that println, take, map, and range are all functions. In Lisp, you call a function by putting it in parentheses. For example, (range) calls the range function.

50

Squares of Integers

The expression (fn [x] (* x x)) is an anonymous function that calls the multiply function, passing its input argument in twice. In other words, it computes the square of its input.

Looking at the whole thing again, it’s best to start with the innermost function call.

(cid:129) The range function returns a never-ending list of integers starting with 0.  (cid:129) This list is passed into the map function, which calls the anonymous

squaring function on each element, producing a new never-ending list of all the squares.

(cid:129) The list of squares is passed into the take function, which returns a new

list with only the first 25 elements.

(cid:129) The println function prints its input, which is a list of the first 25 squares

of integers.

If you find yourself terrified by the concept of never-ending lists, don’t worry. Only the first 25 elements of those never-ending lists are actually created. That’s because no element of a never-ending list is evaluated until it is accessed.

If you found all of that confusing, then you can look forward to a glorious time learning all about Clojure and functional programming. It is not my goal to teach you about these topics here.

Instead, my goal here is to point out something very dramatic about the difference between the Clojure and Java programs. The Java program uses a mutable variable—a variable that changes state during the execution of the program. That variable is i—the loop control variable. No such mutable variable exists in the Clojure program. In the Clojure program, variables like x are initialized, but they are never modified.

This leads us to a surprising statement: Variables in functional languages do not vary.

51

Chapter 6  Functional Programming

Immutabilit y  and  Architecture

Why is this point important as an architectural consideration? Why would an architect be concerned with the mutability of variables? The answer is absurdly simple: All race conditions, deadlock conditions, and concurrent update problems are due to mutable variables. You cannot have a race condition or a concurrent update problem if no variable is ever updated. You cannot have deadlocks without mutable locks.

In other words, all the problems that we face in concurrent applications—all the problems we face in applications that require multiple threads, and multiple processors—cannot happen if there are no mutable variables.

As an architect, you should be very interested in issues of concurrency. You want to make sure that the systems you design will be robust in the presence of multiple threads and processors. The question you must be asking yourself, then, is whether immutability is practicable.

The answer to that question is affirmative, if you have infinite storage and infinite processor speed. Lacking those infinite resources, the answer is a bit more nuanced. Yes, immutability can be practicable, if certain compromises are made.

Let’s look at some of those compromises.

Segregation  of  Mutabilit y

One of the most common compromises in regard to immutability is to segregate the application, or the services within the application, into mutable and immutable components. The immutable components perform their tasks in a purely functional way, without using any mutable variables. The immutable components communicate with one or more other components that are not purely functional, and allow for the state of variables to be mutated (Figure 6.1).

52

Segregation of Mutability

Figure 6.1  Mutating state and transactional memory

Since mutating state exposes those components to all the problems of concurrency, it is common practice to use some kind of transactional memory to protect the mutable variables from concurrent updates and race conditions.

Transactional memory simply treats variables in memory the same way a database treats records on disk.1 It protects those variables with a transaction- or retry-based scheme.

A simple example of this approach is Clojure’s atom facility:

(def counter (atom 0)) ; initialize counter to 0

(swap! counter inc)    ; safely increment counter.

In this code, the counter variable is defined as an atom. In Clojure, an atom is a special kind of variable whose value is allowed to mutate under very disciplined conditions that are enforced by the swap! function.

The swap! function, shown in the preceding code, takes two arguments: the atom to be mutated, and a function that computes the new value to be stored

1.  I know… What’s a disk?

53

Chapter 6  Functional Programming

in the atom. In our example code, the counter atom will be changed to the value computed by the inc function, which simply increments its argument.

The strategy used by swap! is a traditional compare and swap algorithm. The value of counter is read and passed to inc. When inc returns, the value of counter is locked and compared to the value that was passed to inc. If the value is the same, then the value returned by inc is stored in counter and the lock is released. Otherwise, the lock is released, and the strategy is retried from the beginning.

The atom facility is adequate for simple applications. Unfortunately, it cannot completely safeguard against concurrent updates and deadlocks when multiple dependent variables come into play. In those instances, more elaborate facilities can be used.

The point is that well-structured applications will be segregated into those components that do not mutate variables and those that do. This kind of segregation is supported by the use of appropriate disciplines to protect those mutated variables.

Architects would be wise to push as much processing as possible into the immutable components, and to drive as much code as possible out of those components that must allow mutation.

Event  Sourcing

The limits of storage and processing power have been rapidly receding from view. Nowadays it is common for processors to execute billions of instructions per second and to have billions of bytes of RAM. The more memory we have, and the faster our machines are, the less we need mutable state.

As a simple example, imagine a banking application that maintains the account balances of its customers. It mutates those balances when deposit and withdrawal transactions are executed.

54

Event Sourcing

Now imagine that instead of storing the account balances, we store only the transactions. Whenever anyone wants to know the balance of an account, we simply add up all the transactions for that account, from the beginning of time. This scheme requires no mutable variables.

Obviously, this approach sounds absurd. Over time, the number of transactions would grow without bound, and the processing power required to compute the totals would become intolerable. To make this scheme work forever, we would need infinite storage and infinite processing power.

But perhaps we don’t have to make the scheme work forever. And perhaps we have enough storage and enough processing power to make the scheme work for the reasonable lifetime of the application.

This is the idea behind event sourcing.2 Event sourcing is a strategy wherein we store the transactions, but not the state. When state is required, we simply apply all the transactions from the beginning of time.

Of course, we can take shortcuts. For example, we can compute and save the state every midnight. Then, when the state information is required, we need compute only the transactions since midnight.

Now consider the data storage required for this scheme: We would need a lot of it. Realistically, offline data storage has been growing so fast that we now consider trillions of bytes to be small—so we have a lot of it.

More importantly, nothing ever gets deleted or updated from such a data store. As a consequence, our applications are not CRUD; they are just CR. Also, because neither updates nor deletions occur in the data store, there cannot be any concurrent update issues.

If we have enough storage and enough processor power, we can make our applications entirely immutable—and, therefore, entirely functional.

If this still sounds absurd, it might help if you remembered that this is precisely the way your source code control system works.

2.  Thanks to Greg Young for teaching me about this concept.

55

Chapter 6  Functional Programming

Conclusion

To summarize:

(cid:129) Structured programming is discipline imposed upon direct transfer

of control.

(cid:129) Object-oriented programming is discipline imposed upon indirect transfer

of control.

(cid:129) Functional programming is discipline imposed upon variable assignment.

Each of these three paradigms has taken something away from us. Each restricts some aspect of the way we write code. None of them has added to our power or our capabilities.

What we have learned over the last half-century is what not to do.

With that realization, we have to face an unwelcome fact: Software is not a rapidly advancing technology. The rules of software are the same today as they were in 1946, when Alan Turing wrote the very first code that would execute in an electronic computer. The tools have changed, and the hardware has changed, but the essence of software remains the same.

Software—the stuff of computer programs—is composed of sequence, selection, iteration, and indirection. Nothing more. Nothing less.

56

Design  Principles

III

Good software systems begin with clean code. On the one hand, if the bricks aren’t well made, the architecture of the building doesn’t matter much. On the other hand, you can make a substantial mess with well-made bricks. This is where the SOLID principles come in.

57

Part III  Design Principles

The SOLID principles tell us how to arrange our functions and data structures into classes, and how those classes should be interconnected. The use of the word「class」does not imply that these principles are applicable only to object-oriented software. A class is simply a coupled grouping of functions and data. Every software system has such groupings, whether they are called classes or not. The SOLID principles apply to those groupings.

The goal of the principles is the creation of mid-level software structures that:

(cid:129) Tolerate change,  (cid:129) Are easy to understand, and (cid:129) Are the basis of components that can be used in many software systems.

The term「mid-level」refers to the fact that these principles are applied by programmers working at the module level. They are applied just above the level of the code and help to define the kinds of software structures used within modules and components.

Just as it is possible to create a substantial mess with well-made bricks, so it is also possible to create a system-wide mess with well-designed mid-level components. For this reason, once we have covered the SOLID principles, we will move on to their counterparts in the component world, and then to the principles of high-level architecture.

The history of the SOLID principles is long. I began to assemble them in the late 1980s while debating software design principles with others on USENET (an early kind of Facebook). Over the years, the principles have shifted and changed. Some were deleted. Others were merged. Still others were added. The final grouping stabilized in the early 2000s, although I presented them in a different order.

In 2004 or thereabouts, Michael Feathers sent me an email saying that if I rearranged the principles, their first words would spell the word SOLID—and thus the SOLID principles were born.

58

Part III  Design Principles

The chapters that follow describe each principle more thoroughly. Here is the executive summary:

(cid:129) SRP: The Single Responsibility Principle

An active corollary to Conway’s law: The best structure for a software  system is heavily influenced by the social structure of the organization that uses it so that each software module has one, and only one, reason to change.

(cid:129) OCP: The Open-Closed Principle

Bertrand Meyer made this principle famous in the 1980s. The gist is that for software systems to be easy to change, they must be designed to allow the behavior of those systems to be changed by adding new code, rather than changing existing code.

(cid:129) LSP: The Liskov Substitution Principle

Barbara Liskov’s famous definition of subtypes, from 1988. In short, this principle says that to build software systems from interchangeable parts, those parts must adhere to a contract that allows those parts to be substi-tuted one for another.

(cid:129) ISP: The Interface Segregation Principle

This principle advises software designers to avoid depending on things that they don’t use.

(cid:129) DIP: The Dependency Inversion Principle

The code that implements high-level policy should not depend on the code that implements low-level details. Rather, details should depend on policies.

These principles have been described in detail in many different publications1 over the years. The chapters that follow will focus on the architectural implications of these principles instead of repeating those detailed discussions. If you are not already familiar with these principles, what follows is insufficient to understand them in detail and you would be well advised to study them in the footnoted documents.

1.  For example, Agile Software Development, Principles, Patterns, and Practices, Robert C. Martin,

Prentice Hall, 2002, http://www.butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod, and https://en.wikipedia.org/wiki/SOLID_(object-oriented_design) (or just google SOLID).

59

This page intentionally left blank

7SRP:  The  Single

Responsibility

Principle

61


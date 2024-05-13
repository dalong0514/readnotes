– Arthur C. Clarke

All of the code examples that we have seen so far in this book follow a particular programming paradigm: object-oriented programming (OOP). This paradigm has monopolized the software industry for a long time and the majority of software companies have adopted OOP as the standard way of programming.

However the fact that OOP has become the most used paradigm does not mean it is the only one that exists. In fact, there are more that are worth mentioning, but this chapter is going to focus only on one of them: functional programming. Additionally, this book's language is Java, so all code snippets and examples will be based on the functional API that were included in version 8 of Java.

Topics covered in this chapter include:

Optional class

Functions revisited

Streams

Applying TDD to functional programming

TDD and Functional Programming – A Perfect Match

Chapter 7

Setting up the environment

In order to explore some of the goodies of Java Functional Programming in a test-driven fashion, we are going to set up a Java project with JUnit and AssertJ frameworks. The last one includes quite a few convenient methods for Optional.

Let's start a new Gradle project. This is how build.gradle looks:

apply plugin: 'java'

sourceCompatibility = 1.8

targetCompatibility = 1.8

repositories {

mavenCentral()

}

dependencies {

testCompile group: 'junit', name: 'junit', version: '4.12'

testCompile group: 'org.assertj', name: 'assertj-core', version:

'3.9.0'

}

In the following sections, we are going to explore some of the utilities and classes included in Java 8 that enhance the experience of programming. Most of them are not only for functional programming and can be used even in imperative-style programming.

Optional – dealing with uncertainty

Since it was created, null has been used and misused by developers innumerable times in innumerable programs. One of the common cases for null is, among others, to represent the absence of a value. That is not convenient at all; it could either represent the absence of a value or the abnormal execution of a piece of code.

Moreover, in order to access variables that can potentially be null , and mitigate undesired runtime exceptions like NullPointerException, developers tend to wrap variables with an if statement so those variables are accessed in safe mode. Although it works, this protection against nulls adds some boilerplate that has nothing to do with the functionality or the goal of the code:

if (name != null) {

// do something with name

}

[ 170 ]

TDD and Functional Programming – A Perfect Match

Chapter 7

The preceding code overcomes the problems that the creator of null spotted in his famous quote during a conference in 2009:

"I call it my billion-dollar mistake. It was the invention of the null reference in 1965. At that time, I was designing the first comprehensive type system for references in an object oriented language (ALGOL W). My goal was to ensure that all use of references should be absolutely safe, with checking performed automatically by the compiler. But I couldn't resist the temptation to put in a null reference, simply because it was so easy to implement.

This has led to innumerable errors, vulnerabilities, and system crashes, which have probably caused a billion dollars of pain and damage in the last forty years."

– Tony Hoare

With the release of Java 8, the utility class called Optional was included as an alternative to the preceding code block. Among other benefits, it brings compilation checks and zero boilerplate code. Let's see Optional in action with a simple example.

Example of Optional

As a demonstration of Optional, we are going to create an in-memory student repository.

This repository has a method to find students by their name, which, for convenience, will be considered the ID. The value returned by the method is Optional<Student> ; this means that the response might or might not contain a Student. This pattern is basically one of the common scenarios for Optional.

At this point, the reader should be familiar with the TDD process. For the sake of brevity the complete Red-Green-Refactor process is skipped. Tests are going to be presented along with the implementation in a convenient order, which could not coincide with the order in a TDD iteration.

First of all, we need a Student class to represent students within our system. To keep it simple, our implementation is going to be very basic, with only two parameters: the student's name and age:

public class Student {

public final String name;

public final int age;

public Student(String name, int age) {

this.name = name;

this.age = age;

[ 171 ]

TDD and Functional Programming – A Perfect Match

Chapter 7

}

}

The next test class verifies two scenarios: a successful lookup and an unsuccessful one. Note that AssertJ has some useful and meaningful assertion methods for Optional. That makes testing really fluent and readable:

public class StudentRepositoryTest {

private List<Student> studentList = Arrays.asList(

new Student("Jane", 23),

new Student("John", 21),

new Student("Tom", 25)

);

private StudentRepository studentRepository =

new StudentRepository(studentList);

@Test

public void whenStudentIsNotFoundThenReturnEmpty() {

assertThat(studentRepository.findByName("Samantha"))

.isNotPresent();

}

@Test

public void whenStudentIsFoundThenReturnStudent() {

assertThat(studentRepository.findByName("John"))

.isPresent();

}

}

In cases where verifying the existence of a student with that name is not enough, we can perform some assertions on the returned object. In the majority of scenarios, this is the way to go:

@Test

public void whenStudentIsFoundThenReturnStudent() {

assertThat(studentRepository.findByName("John"))

.hasValueSatisfying(s -> {

assertThat(s.name).isEqualTo("John");

assertThat(s.age).isEqualTo(21);

});

}

[ 172 ]

TDD and Functional Programming – A Perfect Match

Chapter 7

Now, it's time to focus on the StudentRepository class, which contains only one constructor and the method to perform student lookups. As shown in the following code, the lookup method findByName returns an Optional holding a Student. Note that this is a valid yet not functional implementation used as a starting point:

public class StudentRepository {

StudentRepository(Collection<Student> students) { }

public Optional<Student> findByName(String name) {

return Optional.empty();

}

}

If we run the tests against the preceding implementation we get one successful test, because the lookup method is returning by default an Optional.empty(). The other test throws an error, as follows:

java.lang.AssertionError:

Expecting Optional to contain a value but was empty.

For the sake of completeness, this is one of the possible implementations: public class StudentRepository {

private final Set<Student> studentSet;

StudentRepository(Collection<Student> students) {

studentSet = new HashSet<>(students);

}

public Optional<Student> findByName(String name) {

for (Student student : this.studentSet) {

if (student.name.equals(name))

return Optional.of(student);

}

return Optional.empty();

}

}

In the next section, we will see a different point of view on functions . In Java 8, some additional capabilities have been added to functions if they are used in a particular way. We are going to explore a few of them with some examples.

[ 173 ]

TDD and Functional Programming – A Perfect Match

Chapter 7

Functions revisited

Unlike object-oriented programs, those written in a functional way don't hold any mutable state. Instead, code is made up with functions that take arguments and return values.

Because there is no internal state nor side-effects involved that can alter the execution, all functions are deterministic. This is a really good feature because it implies that different executions of the same function, with the same parameters, would produce the same outcome.

The following snippet illustrates a function that does not mutate any internal state: public Integer add(Integer a, Integer b) {

return a + b;

}

The following is the same function written using Java's functional API: public final BinaryOperator<Integer> add =

new BinaryOperator<Integer>() {

@Override

public Integer apply(Integer a, Integer b) {

return a + b;

}

};

The first example should be completely familiar to any Java developer; it follows the common syntax of a function that takes two integers as arguments and returns the sum of them. The second example, however, differs a bit from the traditional code we are used to.

In this new version, the function is an object that counts as a value, and it can be assigned to a field. This is quite convenient in some scenarios because it can still be used as a function in some cases and in some others it can also be used as a return value, as an argument in a function or a field within a class.

One can argue that the first version of the function is more appropriated since it is shorter and does not require creating a new object. Well, it's true, but the fact that functions can also be objects enhances them with a bunch of new capabilities. Regarding code verbosity, it can be considerably reduced to a single line by using a lambda expression:

public final BinaryOperator<Integer> addLambda = (a, b) -> a + b;

[ 174 ]

TDD and Functional Programming – A Perfect Match

Chapter 7

In the next section, a possible solution to Reverse Polish Notation (RPN) kata is presented.

We are going to use the power and expressiveness of functional programming, particularly the lambda notation, which becomes really handy when functions are required as arguments of some functions. Using lambdas makes our code very concise and elegant, increasing the readability.

Kata – Reverse Polish Notation

RPN is a notation used for representing mathematical expressions. It differs from the traditional and widely used infix notation in the order of operators and operands.

In infix notation the operator is placed between the operands, whereas in RPN, operands are placed first and the operator is located at the end.

This is an expression written using infix notation:

3 + 4

The same expression written using RPN:

3 4 +

Requirements

We are going to obviate how the expressions are read so that we can focus on solving the problem. Furthermore, we are going to work only with positive integers to simplify the problem, although it shouldn't be very difficult to accept floats or doubles as well. In order to solve this kata, we are asked to fulfill only the following two requirements: On invalid input (not a RPN), an error message should be thrown

It gets an arithmetic expression written using RPN and computes the result

[ 175 ]

TDD and Functional Programming – A Perfect Match

Chapter 7

The following code snippet is a small scaffold for us to start our project upon: public class ReversePolishNotation {

int compute(String expression) {

return 0;

}

}

public class NotReversePolishNotationError extends RuntimeException

{

public NotReversePolishNotationError() {

super("Not a Reverse Polish Notation");

}

}

With the preceding code fragment as the starting point, we are going to proceed, breaking down the requirements into smaller specifications that can be tackled one by one.

Requirement – handling invalid input

Provided that our implementation is basically doing nothing, we are going to focus only on one thing—reading single operands. If the input is a single number (no operators) then it's a valid reverse notation and the value of the number is returned. Anything other than that is considered not a valid RPN for now.

This requirement is translated into these four tests:

public class ReversePolishNotationTest {

private ReversePolishNotation reversePolishNotation =

new ReversePolishNotation();

@Test(expected = NotReversePolishNotationError.class)

public void emptyInputThrowsError() {

reversePolishNotation.compute("");

}

@Test(expected = NotReversePolishNotationError.class)

public void notANumberThrowsError() {

reversePolishNotation.compute("a");

}

@Test

public void oneDigitReturnsNumber() {

assertThat(reversePolishNotation.compute("7")).isEqualTo(7);

}

[ 176 ]

TDD and Functional Programming – A Perfect Match

Chapter 7

@Test

public void moreThanOneDigitReturnsNumber() {

assertThat(reversePolishNotation.compute("120")).isEqualTo(120);

}

}

Our compute method is now required to throw an IllegalArgumentException when an invalid input is provided. In any other case it returns the number as an integer value. This can be achieved with the following lines of code:

public class ReversePolishNotation {

int compute(String expression) {

try {

return (Integer.parseInt(expression));

} catch (NumberFormatException e) {

throw new NotReversePolishNotationError();

}

}

}

This requirement has been fulfilled. The other requirement is a bit more complex, so we are going to divide it into two—single operations, which means only one operation, and complex operations, which involve more than one operation of any kind.

Requirement – single operations

So, the plan is to support add, subtract, multiply and divide operations. As explained in the kata presentation, in RPN the operator is located at the end of the expression.

That means a - b is represented as a b -, and the same applies to the other operators: addition +, multiplication *, and division /.

Let's add one of each of the supported operations to our tests:

@Test

public void addOperationReturnsCorrectValue() {

assertThat(reversePolishNotation.compute("1 2 +")).isEqualTo(3);

}

@Test

public void subtractOperationReturnsCorrectValue() {

assertThat(reversePolishNotation.compute("2 1 -")).isEqualTo(1);

}

[ 177 ]

TDD and Functional Programming – A Perfect Match

Chapter 7

@Test

public void multiplyOperationReturnsCorrectValue() {

assertThat(reversePolishNotation.compute("2 1 *")).isEqualTo(2);

}

@Test

public void divideOperationReturnsCorrectValue() {

assertThat(reversePolishNotation.compute("2 2 /")).isEqualTo(1);

}

This also includes the necessary changes to make them pass successfully. The behavior is basically placing the operator between the expressions and performing the operation in case an expression is given as input. If there is only one element in the expression, then the former rules apply:

int compute(String expression) {

String[] elems = expression.trim().split(" ");

if (elems.length != 1 && elems.length != 3)

throw new NotReversePolishNotationError();

if (elems.length == 1) {

return parseInt(elems[0]);

} else {

if ("+".equals(elems[2]))

return parseInt(elems[0]) + parseInt(elems[1]);

else if ("-".equals(elems[2]))

return parseInt(elems[0]) - parseInt(elems[1]);

else if ("*".equals(elems[2]))

return parseInt(elems[0]) * parseInt(elems[1]);

else if ("/".equals(elems[2]))

return parseInt(elems[0]) / parseInt(elems[1]);

else

throw new NotReversePolishNotationError();

}

}

parseInt is a private method that parses the input and either returns the integer value or throws an exception:

private int parseInt(String number) {

try {

return Integer.parseInt(number);

} catch (NumberFormatException e) {

throw new NotReversePolishNotationError();

}

}

[ 178 ]

TDD and Functional Programming – A Perfect Match

Chapter 7

The next requirement is where the magic happens. We are going to support more than one operation within the expression.

Requirement – complex operations

Complex operations are difficult to address, because mixing operations makes it really difficult for the non-trained human eye to understand in which order the operations should take place. Also, different evaluation orders usually lead to different results. To solve that, the computation of reverse polish expressions is backed up by the implementation of a queue. These are some tests for our next functionality:

@Test

public void multipleAddOperationsReturnCorrectValue() {

assertThat(reversePolishNotation.compute("1 2 5 + +"))

.isEqualTo(8);

}

@Test

public void multipleDifferentOperationsReturnCorrectValue() {

assertThat(reversePolishNotation.compute("5 12 + 3 -"))

.isEqualTo(14);

}

@Test

public void aComplexTest() {

assertThat(reversePolishNotation.compute("5 1 2 + 4 * + 3 -"))

.isEqualTo(14);

}

The computation should pile up the numbers or operands in the expression sequentially, from left to right, in a queue or stack in Java. If at any point an operator is found then the pile replaces the two elements on top with the result of applying that operator to those values. For better comprehension, the logic is going to be separated in to different functions.

First of all, we are going to define a function that takes a stack and an operation and applies the function to the first two items on the top. Note that the second operand is retrieved in the first instance due to the implementation of stack:

private static void applyOperation(

Stack<Integer> stack,

BinaryOperator<Integer> operation

) {

int b = stack.pop(), a = stack.pop();

stack.push(operation.apply(a, b));

}

[ 179 ]

TDD and Functional Programming – A Perfect Match

Chapter 7

The next step is to create all the functions that our program must handle. For each operator a function is defined as an object. This has some advantages, such as better isolation for testing. In this case it might not make sense to test functions separately because they are trivial, but there are some other scenarios where testing the logic of these functions in isolation can be very useful:

static BinaryOperator<Integer> ADD = (a, b) -> a + b;

static BinaryOperator<Integer> SUBTRACT = (a, b) -> a - b;

static BinaryOperator<Integer> MULTIPLY = (a, b) -> a * b;

static BinaryOperator<Integer> DIVIDE = (a, b) -> a / b;

And now, putting all the pieces together. Depending on the operator we find, the proper operation is applied:

int compute(String expression) {

Stack<Integer> stack = new Stack<>();

for (String elem : expression.trim().split(" ")) {

if ("+".equals(elem))

applyOperation(stack, ADD);

else if ("-".equals(elem))

applyOperation(stack, SUBTRACT);

else if ("*".equals(elem))

applyOperation(stack, MULTIPLY);

else if ("/".equals(elem))

applyOperation(stack, DIVIDE);

else {

stack.push(parseInt(elem));

}

}

if (stack.size() == 1) return stack.pop();

else throw new NotReversePolishNotationError();

}

The code is readable and very easy to understand. Moreover, this design allows the extending of the functionality by adding support to other different operations with ease.

It can be a good exercise for readers to add a modulus ( %) operation to the provided solution.

Another good example where lambdas fit perfectly is Streams API, since most functions have a self-explanatory name like filter, map or reduce, among others. Let's explore this more deeply in the next section.

[ 180 ]

TDD and Functional Programming – A Perfect Match

Chapter 7

Streams

One of the top utilities included in Java 8 are Streams. In this chapter we are going to use lambdas in combination with Streams in small code fragments, and create a test to verify them.

To better understand what Streams are, what to do, and what not to do with them, it is highly recommended to read Oracle's Stream pages. A good starting point is https:/​/​docs.

oracle.​com/​javase/​8/​docs/​api/​java/​util/​stream/​Stream.​html.

To cut a long story short, Streams provide a bunch of facilities to deal with long computations that can be executed either in parallel or sequential order. Parallel programming is out of the scope of this book, so the next examples will be sequential only.

Furthermore, in order to keep the chapter concise we are going to focus on: filter

map

flatMap

reduce

filter

Let's start with the filter operation. Filters is a function with a self-explanatory name; it filters in/out elements in the stream depending on whether the value satisfies a condition, as shown in the following example:

@Test

public void filterByNameReturnsCollectionFiltered() {

List<String> names = Arrays.asList("Alex", "Paul", "Viktor",

"Kobe", "Tom", "Andrea");

List<String> filteredNames = Collections.emptyList();

assertThat(filteredNames)

.hasSize(2)

.containsExactlyInAnyOrder("Alex", "Andrea");

}

One possibility for computing the list of filteredNames is the following: List<String> filteredNames = names.stream()

.filter(name -> name.startsWith("A"))

.collect(Collectors.toList());

[ 181 ]

TDD and Functional Programming – A Perfect Match

Chapter 7

That one is the easiest. In a few words, filter filters the input and returns a value without all the elements filtered out. Using lambdas makes the code elegant and really easy to read.

map

The map function transforms all the elements in the stream into another. The resultant object can share the type with the input, but it's also possible to return an object of a different type:

@Test

public void mapToUppercaseTransformsAllElementsToUppercase() {

List<String> names = Arrays.asList("Alex", "Paul", "Viktor"); List<String> namesUppercase = Collections.emptyList();

assertThat(namesUppercase)

.hasSize(3)

.containsExactly("ALEX", "PAUL", "VIKTOR");

}

The list namesUppercase should be computed as follows:

List<String> namesUppercase = names.stream()

.map(String::toUpperCase)

.collect(Collectors.toList());

Note how the toUpperCase method is called. It belongs to the Java class String and can be used in that scenario only by referencing the function and the class that function belongs to. In Java, this is called method reference.

flatMap

The flatMap function is very similar to the map function, but it is used when the operation might return more than one value and we want to keep a stream of single elements. In the case of map, a stream of collections would be returned instead. Let's see flatMap in use:

@Test

public void gettingLettersUsedInNames() {

List<String> names = Arrays.asList("Alex", "Paul", "Viktor"); List<String> lettersUsed = Collections.emptyList();

assertThat(lettersUsed)

.hasSize(12)

.containsExactly("a","l","e","x","p","u","v","i","k","t","o","r");

}

[ 182 ]

TDD and Functional Programming – A Perfect Match

Chapter 7

One possible solution could be:

List<String> lettersUsed = names.stream()

.map(String::toLowerCase)

.flatMap(name -> Stream.of(name.split("")))

.distinct()

.collect(Collectors.toList());

This time we have used Stream.of(), a convenient method for creating Streams. Another really nice feature is the method distinct(), which returns a collection of unique elements, comparing them using the method equals().

reduce

In the previous example, the function returns the list of letters used in all the names passed as input. But if we are only interested in the number of different letters, there's an easier way to proceed. reduce basically applies a function to all elements and combines them into one single result. Let's see an example:

@Test

public void countingLettersUsedInNames() {

List<String> names = Arrays.asList("Alex", "Paul", "Viktor"); long count = 0;

assertThat(count).isEqualTo(12);

}

This solution is very similar to the one we used for the previous exercise: long count = names.stream()

.map(String::toLowerCase)

.flatMap(name -> Stream.of(name.split("")))

.distinct()

.mapToLong(l -> 1L)

.reduce(0L, (v1, v2) -> v1 + v2);

Even though the preceding code snippet solves the problem, there is a much nicer way to do it:

long count = names.stream()

.map(String::toLowerCase)

.flatMap(name -> Stream.of(name.split("")))

.distinct()

.count();

[ 183 ]

TDD and Functional Programming – A Perfect Match

Chapter 7

The function count() is another built-in tool that Streams includes. It's a particular shortcut for a reduction function that counts the number of elements the stream contains.

Summary

Functional programming is an old concept that is gaining popularity, because it's easier to use when trying to increase performance by executing tasks in parallel. In this chapter some concepts from the functional world were presented along with some of the test tools that AssertJ provides.

Testing functions without side effects is very easy because the test scope is reduced. Instead of testing changes that the function might cause on different objects, the only thing that needs to be verified is the outcome of the invocation. No side-effects means that the outcome of the function is the same as long as the parameters are the same. Therefore, the execution is repeatable as many times as needed and leads to the same result on every execution. Additionally, tests are easier to read and comprehend.

To conclude, Java includes a good API for functional programming if you need to use this paradigm within your projects. But there are some languages, some of them purely functional, that offer more powerful features with better syntax and less boilerplate. You should evaluate whether using one of those other languages might make sense if your project or approach can be purely functional.

All of the examples presented in this chapter can be found at https:/​/​bitbucket.​org/

alexgarcia/​tdd-​java-​funcprog.​git.

Now it is time to take a look at legacy code and how to adapt it and make it more TDD

friendly.

[ 184 ]

8

BDD – Working Together with

the Whole Team

"I'm not a great programmer; I'm just a good programmer with great habits."


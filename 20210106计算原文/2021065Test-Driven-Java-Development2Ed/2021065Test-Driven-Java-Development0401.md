– Giorgio Armani

As promised, each chapter will explore a different Java testing framework and this one is no exception. We'll use TestNG to build our specifications.

In the previous Chapter 3, Red-Green-Refactor – From Failure Through Success until Perfection, we practiced the Red-Green-Refactor procedure. We used unit tests without going deeper into how unit testing works in the context of TDD. We'll build on the knowledge from the last chapter and go into more detail by trying to explain what unit tests really are and how they fit into the TDD approach to building software.

The goal of this chapter is to learn how to focus on the unit we're currently working on and how to ignore or isolate those that were done before.

Once we're comfortable with TestNG and unit testing, we'll dive right into the requirements of our next application and start coding.

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

The following topics will be covered in this chapter:

Unit testing

Unit testing with TDD

TestNG

Remote-controlled ship requirements

Developing the remote-controlled ship

Unit testing

Frequent manual testing is too impractical for any but the smallest systems. The only way around this is the use of automated tests. They are the only effective method to reduce the time and cost of building, deploying, and maintaining applications. In order to effectively manage applications, it is of the utmost importance that both the implementation and test codes are as simple as possible. Simplicity is one of the core extreme programming (XP)

values (http://www.extremeprogramming.org/rules/simple.html) and the key to TDD

and programming in general. It is most often accomplished through division into small units. In Java, units are methods. Being the smallest, the feedback loop they provide is the fastest so we spend most of our time thinking and working on them. As a counterpart to implementation methods, unit tests should constitute by far the biggest percentage of all tests.

What is unit testing?

Unit testing is a practice that forces us to test small, individual, and isolated units of code.

They are usually methods, even though in some cases classes or even whole applications can be considered to be units, as well. In order to write unit tests, code under tests needs to be isolated from the rest of the application. Preferably, that isolation is already ingrained in the code or it can be accomplished with the use of mocks (more on mocks will be covered in

Chapter 6, Mocking – Removing External Dependencies). If unit tests of a particular method cross the boundaries of that unit, then they become integration tests. As such, it becomes less clear what is under the tests. In case of a failure, the scope of a problem suddenly increases and finding the cause becomes more tedious.

[ 85 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

Why unit testing?

A common question, especially within organizations that rely heavily on manual testing, is Why should we use unit instead of functional and integration testing? This question in itself is flawed. Unit testing does not replace other types of testing. Instead, unit testing reduces the scope of other types of tests. By its nature, unit testing is easier and faster to write than any other type of tests, thus reducing the cost and time to market (TTM). Due to the reduced time to write and run them, they tend to detect problems much sooner. The faster we detect problems, the cheaper it is to fix them. A bug that was detected minutes after it was created is much easier to fix than if that same bug was found days, weeks, or even months after it was made.

Code refactoring

Code refactoring is the process of changing the structure of an existing code without changing its external behavior. The purpose of refactoring is to improve an existing code.

This improvement can be made for many different reasons. We might want to make the code more readable, less complex, easier to maintain, cheaper to extend, and so on. No matter what the reason for refactoring is, the ultimate goal is always to make it better in one way or another. The effect of this goal is a reduction in technical debt; a reduction in pending work that needs to be done due to suboptimal design, architecture, or coding.

Typically, we approach refactoring by applying a set of small changes without modifying intended behavior. Reducing the scope of refactoring changes allows us continuously to confirm that those changes did not break any existing functionality. The only way to effectively obtain this confirmation is through the use of automated tests.

One of the great benefits of unit tests is that they are the best refactoring enablers.

Refactoring is too risky when there are no automated tests to confirm that the application still behaves as expected. While any type of test can be used to provide the code coverage required for refactoring, in most cases only unit tests can provide the required level of details.

Why not use unit tests exclusively?

At this moment, you might be wondering whether unit testing could provide a solution for all your testing needs. Unfortunately, that is not the case. While unit tests usually cover the biggest percentage of your testing needs, functional and integration tests should be an integral part of your testing toolbox.

[ 86 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

We'll cover other types of tests in more detail in later chapters. For now, a few important distinctions between them are as follows:

Unit tests try to verify small units of functionality. In the Java world, those units are methods. All external dependencies, such as invocations of other classes and methods or database calls, should be done in memory with the use of mocks, stubs, spies, fakes, and dummies. Gerard Meszaros coined a more general term, test doubles , that envelops all those

(http://en.wikipedia.org/wiki/Test_double). Unit tests are simple, easy to write, and fast to run. They are usually the biggest percentage of a testing suite.

Functional and acceptance tests have a job to verify that the application we're building works as expected, as a whole. While those two differ in their purpose, both share a similar goal. Unlike unit tests that are verifying the internal quality of the code, functional and acceptance tests are trying to ensure that the system is working correctly from the customer's or user's point of view. Those tests are usually smaller in number when compared with unit tests due to the cost and effort needed to both write and run them.

Integration tests intend to verify that separate units, modules, applications, or even whole systems are properly integrated with each other. You might have a frontend application that uses backend APIs that, in turn, communicate with a database. The job of integration tests would be to verify that all three of those separate components of the system are indeed integrated and can communicate with each other. Since we already know that all the units are working and all functional and acceptance tests are passed, integration tests are usually the smallest of all three as their job is only to confirm that all the pieces are working well together:

[ 87 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

The testing pyramid states that you should have many more unit tests than higher-level tests (UI tests, integration tests, and so on). Why is that? Unit tests are much cheaper to write, faster to run, and, at the same time, provide much bigger coverage. Take, for example, registration functionality. We should test what happens when a username is empty, when a password is empty, when a username or password is not in the correct format, when the user already exists, and so on. Only for this single functionality there can be tens, if not hundreds of tests. Writing and running all those tests from the UI can be very expensive (time-consuming to write and slow to run). On the other hand, unit testing a method that does this validation is easy, fast to write, and fast to run. If all those cases are covered with unit tests, we could be satisfied with a single integration test that checks whether our UI is calling the correct method on the backend. If it is, details are irrelevant from an integration point of view since we know that all cases are already covered on the unit level.

Unit testing with TDD

What is the difference in the way we write unit tests in the context of TDD? The major differentiator is in when. While traditionally unit tests are written after the implementation code is done, in TDD we write tests before—the order of things is inverted. Without TDD, the purpose of unit tests is to validate an existing code. TDD teaches us that unit tests should drive our development and design. They should define the behavior of the smallest possible unit. They are micro-requirements pending development. A test tells you what to do next and when you're done doing it. Depending on the type of tests (unit, functional, integration, and so on), the scope of what should be done next differs. In the case of TDD

with unit tests, this scope is the smallest possible, meaning a method or, more often, a part of it. Moreover, with TDD driven by unit tests, we are forced to comply to some design principles, such as keep it simple, stupid (KISS). By writing simple tests with a very small scope, the implementation of those tests tends to be simple as well. By forcing tests not to use external dependencies, we are forcing the implementation code to have a separation of concerns that is well-designed. There are many other examples of how TDD helps us to write better code. Those same benefits cannot be accomplished with unit testing alone.

Without TDD, unit tests are forced to work with an existing code and have no influence on the design.

To summarize, the main goal of unit testing without TDD is the validation of the existing code. Unit testing written in advance using the TDD procedure has the main objective specification and design, with validation being a side product. This side product is often of a higher quality than when tests are written after the implementation.

[ 88 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

TDD forces us to think through our requirements and design, write clean code that works, create executable requirements, and refactor safely and often. On top of all that, we end up with high test code coverage that is used to regression-test all our code whenever some change is introduced. Unit testing without TDD gives us only tests and, often, with doubtful quality.

TestNG

JUnit and TestNG are two major Java testing frameworks. You already wrote tests with JUnit in the previous chapter, Chapter 3, Red-Green-Refactor – From Failure Through Success until Perfection, and, hopefully, got a good understanding of how it works. How about TestNG? It was born out of a desire to make JUnit better. Indeed, it contains some functionalities that JUnit doesn't have.

The following subsections summarize some of the differences between the two of them.

We'll try not only to provide an explanation of the differences, but also their evaluation in the context of unit testing with TDD.

The @Test annotation

Both JUnit and TestNG use the @Test annotation to specify which method is considered to be a test. Unlike JUnit, which requires every method to be annotated with @Test, TestNG

allows us to use this annotation on a class level, as well. When used in this way, all public methods are considered tests unless specified otherwise:

@Test

public class DirectionSpec {

public void whenGetFromShortNameNThenReturnDirectionN() {

Direction direction = Direction.getFromShortName('N');

assertEquals(direction, Direction.NORTH);

}

public void whenGetFromShortNameWThenReturnDirectionW() {

Direction direction = Direction.getFromShortName('W');

assertEquals(direction, Direction.WEST);

}

}

[ 89 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

In this example, we put the @Test annotation above the DirectionSpec class. As a result, both the whenGetFromShortNameNThenReturnDirectionN and

whenGetFromShortNameWThenReturnDirectionW methods are considered tests.

If that code was written using JUnit, both the methods would need to have the @Test annotation.

The @BeforeSuite, @BeforeTest,

@BeforeGroups, @AfterGroups, @AfterTest, and

@AfterSuite annotations

Those six annotations do not have their equivalents in JUnit. TestNG can group tests into suites, using XML configuration. Methods annotated with @BeforeSuite and

@AfterSuite are run before and after all the tests in the specified suite have run. Similarly, the @BeforeTest and @AfterTest annotated methods are run before any test method belonging to the test classes has run. Finally, TestNG tests can be organized into groups.

The @BeforeGroups and @AfterGroups annotations allow us to run methods before the first test and after the last test, in specified groups, are run.

While those annotations can be very useful when tests are written after the implementation code, they do not provide much usage in the context of TDD. Unlike traditional testing, which is often planned and written as a separate project, TDD teaches us to write one test at a time and keep everything simple. Most importantly, unit tests are supposed to run quickly so there is no need to group them into suites or groups. When tests are fast, running anything less than everything is a waste. If, for example, all tests are run in less than 15

seconds, there is no need to run only a part of them. On the other hand, when tests are slow, it is often a sign that external dependencies are not isolated. No matter what the reason is behind slow tests, the solution is not to run only a part of them, but to fix the problem.

Moreover, functional and integration tests do tend to be slower and require us to have some kind of separation. However, it is better to separate them in, for example, build.gradle so that each type of test is run as a separate task.

[ 90 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

The @BeforeClass and @AfterClass annotations

These annotations have the same function in both JUnit and TestNG. Annotated methods will be run before the first test and after the last test, in a current class. The only difference is that TestNG does not require those methods to be static. The reason behind this can be found in the different approaches those two frameworks take when running test methods.

JUnit isolates each test into its own instance of the test class, forcing us to have those methods defined as static and, therefore, reusable across all test runs. TestNG, on the other hand, executes all test methods in the context of a single test class instance, eliminating the need for those methods to be static.

The @BeforeMethod and @AfterMethod

annotations

The @Before and @After annotations are equivalent to JUnit. Annotated methods are run before and after each test method.

The @Test(enable = false) annotation argument

Both JUnit and TestNG can disable tests. While JUnit uses a separate @Ignore annotation, TestNG uses the @Test annotation Boolean argument, enable. Functionally, both work in the same way and the difference is only in the way we write them.

The @Test(expectedExceptions =

SomeClass.class) annotation argument

This is the case where JUnit has the advantage. While both provide the same way to specify the expected exception (in the case of JUnit, the argument is called simply expected), JUnit introduces rules that are a more elegant way to test exceptions (we already worked with

them in Chapter 2, Tools, Frameworks, and Environment).

TestNG versus JUnit summary

There are many other differences between those two frameworks. For brevity, we do not cover all of them in this book. Consult their documentation for further information.

[ 91 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

More information about JUnit and TestNG can be found

at http://junit.org/ and http://testng.org/.

TestNG provides more features and is more advanced than JUnit. We'll work with TestNG

throughout this chapter, and you'll get to know it better. One thing that you'll notice is that we won't use any of those advanced features. The reason is that, with TDD, we rarely need them when working with unit tests. Functional and integration tests are of a different kind and would serve as a better demonstration of TestNG's superiority. However, there are tools that are more suited for those types of tests, as you'll see in the following chapters.

Which one should you use? I'll leave that choice up to you. By the time you finish this chapter, you'll have hands-on knowledge of both JUnit and TestNG.

Remote-controlled ship requirements

We'll work on a variation of a well-known kata called Mars Rover, originally published in Dallas Hack Club (http://dallashackclub.com/rover).

Imagine that a naval ship is placed somewhere on Earth's seas. Since this is the 21st century, we can control that ship remotely.

Our job will be to create a program that can move the ship around the

seas.

Since this is a TDD book and the subject of this chapter is unit tests, we'll develop an application using a TDD approach with the focus on unit tests. In the previous

chapter, Chapter 3, Red-Green-Refactor – From Failure Through Success until Perfection, you learned the theory and had practical experience with the Red-Green-Refactor procedure.

We'll build on top of that and try to learn how to employ unit testing effectively.

Specifically, we'll try to concentrate on a unit we're developing and learn how to isolate and ignore dependencies that a unit might use. Not only that, but we'll try to concentrate on one requirement at a time. For this reason, you were presented only with high-level requirements; we should be able to move the remote-controlled ship, located somewhere on the planet, around.

[ 92 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

To make things easier, all the supporting classes have been already made and tested. This will allow us to concentrate on the main task at hand and, at the same time, keep this exercise concise.

Developing the remote-controlled ship

Let's start by importing the existing Git repository.

Project setup

Let's start setting up the project:

1. Open IntelliJ IDEA. If an existing project is already opened, select File|Close Project.

2. You will be presented with a screen similar to the following:

[ 93 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

3. To import the project from the Git repository, click on Check out from Version Control and select Git. Type

https://bitbucket.org/vfarcic/tdd-java-ch04-ship.git in to the Git

Repository URL field and click on Clone:

4. Answer Yes when asked whether you would like to open the project.

Next you will be presented with the Import Project from Gradle dialog. Click on OK:

[ 94 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

5. IDEA will need to spend some time downloading the dependencies specified in the build.gradle file. Once that is done, you'll see that some classes and corresponding tests are already created:

Helper classes

Imagine that a colleague of yours started working on this project. He's a good programmer and a TDD practitioner, and you trust his abilities to have good test code coverage. In other words, you can rely on his work. However, that colleague did not finish the application before he left for his vacations and it's up to you to continue where he stopped. He created all the helper classes: Direction, Location, Planet, and Point. You'll notice that the corresponding test classes are there as well. They have the same name as the class they're testing with the Spec suffix (that is, DirectionSpec). The reason for using this suffix is to make clear that tests are not only intended to validate the code, but also to serve as an executable specification.

[ 95 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

On top of the helper classes, you'll find the Ship (implementation) and ShipSpec (specifications/tests) classes. We'll spend most of our time in those two classes. We'll write tests in ShipSpec and then we'll write the implementation code in the Ship class (just as we did before).

Since we already learned that tests are not only used as a way to validate the code, but also as executable documentation, from this moment on, we'll use the phrase specification or spec instead of test.

Every time we finish writing a specification or the code that implements it, we'll run gradle test either from the command prompt or by using the Gradle projects IDEA Tool Window:

With the project set up, we're ready to dive into the first requirement.

Requirement – starting point and orientation

We need to know what the current location of the ship is in order to be able to move it.

Moreover, we should also know which direction it is facing: north, south, east, or west.

Therefore, the first requirement is the following:

You are given the initial starting point ( x, y) of a ship and the direction ( N, S, E, or W) it is facing.

[ 96 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

Before we start working on this requirement, let's go through the helper classes that can be used. The Point class holds the x and y coordinates. It has the following constructor: public Point(int x, int y) {

this.x = x;

this.y = y;

}

Similarly, we have the Direction enum class with the following values:

public enum Direction {

NORTH(0, 'N),

EAST(1, 'E'),

SOUTH(2, 'S'),

WEST(3, 'W'),

NONE(4, 'X');

}

Finally, there is the Location class that requires both of those classes to be passed as constructor arguments:

public Location(Point point, Direction direction) {

this.point = point;

this.direction = direction;

}

Knowing this, it should be fairly easy to write a test for this first requirement. We should work in the same way as we did in the previous chapter, Chapter 3, Red-Green-Refactor –

From Failure Through Success until Perfection.

Try to write specs by yourself. When done, compare them with the solution in this book.

Repeat the same process with the code that implements specs. Try to write it by yourself and, once done, compare it with the solution we're proposing.

Specification – keeping position and direction in

memory

The specification for this requirement can be the following:

@Test

public class ShipSpec {

public void whenInstantiatedThenLocationIsSet() {

Location location = new Location(new Point(21, 13),

Direction.NORTH);

Ship ship = new Ship(location);

[ 97 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

assertEquals(ship.getLocation(), location);

}

}

This was an easy one. We're just checking whether the Location object we're passing as the Ship constructor is stored and can be accessed through the location getter.

The @Test annotation—When TestNG has the @Test annotation set on

the class level, there is no need to specify which methods should be used as tests. In this case, all public methods are considered to be TestNG tests.

Implementation

The implementation of this specification should be fairly easy. All we need to do is set the constructor argument to the location variable:

public class Ship {

private final Location location;

public Ship(Location location) {

this.location = location;

}

public Location getLocation() {

return location;

}

}

The full source can be found in the req01-location branch of the tdd-java-ch04-ship repository

(https://bitbucket.org/vfarcic/tdd-java-ch04-ship/branch/req01-location).

Refactoring

We know that we'll need to instantiate Ship for every spec, so we might as well refactor the specification class by adding the @BeforeMethod annotation. The code can be the following:

@Test

public class ShipSpec {

private Ship ship;

private Location location;

[ 98 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

@BeforeMethod

public void beforeTest() {

Location location = new Location(new Point(21, 13),

Direction.NORTH);

ship = new Ship(location);

}

public void whenInstantiatedThenLocationIsSet() {

// Location location = new Location(new Point(21, 13),

Direction.NORTH);

// Ship ship = new Ship(location);

assertEquals(ship.getLocation(), location);

}

}

No new behavior has been introduced. We just moved part of the code to the

@BeforeMethod annotation in order to avoid duplication, which would be produced by the rest of the specifications that we are about to write. Now, every time a test is run, the ship object will be instantiated with location as the argument.

Requirement – forward and backward moves

Now that we know where our ship is, let's try to move it. To begin with, we should be able to go both forwards and backwards.

Implement commands that move the ship forwards and backwards ( f and b).

The Location helper class already has the forward and backward methods that implement this functionality:

public boolean forward() {

...

}

Specification – moving forward

What should happen when, for example, we are facing north and we move the ship forwards? Its location on the y-axis should decrease. Another example would be that when the ship is facing east, it should increase its x-axis location by 1.

[ 99 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

The first reaction can be to write specifications similar to the following two: public void givenNorthWhenMoveForwardThenYDecreases() {

ship.moveForward();

assertEquals(ship.getLocation().getPoint().getY(), 12);

}

public void givenEastWhenMoveForwardThenXIncreases() {

ship.getLocation().setDirection(Direction.EAST);

ship.moveForward();

assertEquals(ship.getLocation().getPoint().getX(), 22);

}

We should create at least two more specifications related to cases where a ship is facing south and west.

However, this is not how unit tests should be written. Most people new to unit testing fall into the trap of specifying the end result that requires the knowledge of the inner workings of methods, classes, and libraries used by the method that is being specified. This approach is problematic on many levels.

When including external code in the unit that is being specified, we should take into account, at least in our case, the fact that the external code is already tested. We know that it is working since we're running all the tests every time any change to the code is made.

Rerun all the tests every time the implementation code changes.

This ensures that there is no unexpected side-effect caused by code

changes.

Every time any part of the implementation code changes, all tests should be run. Ideally, tests are fast to execute and can be run by a developer locally. Once code is submitted to the version control, all tests should be run again to ensure that there was no problem due to code merges. This is especially important when more than one developer is working on the

code. CI tools, such as Jenkins, Hudson, Travind, Bamboo, and Go-CD

should be used to pull the code from the repository, compile it, and run tests.

Another problem with this approach is that if an external code changes, there will be many more specifications to change. Ideally, we should be forced to change only specifications directly related to the unit that will be modified. Searching for all other places where that unit is called from might be very time-consuming and error-prone.

[ 100 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

A much easier, faster, and better way to write specifications for this requirement would be the following:

public void whenMoveForwardThenForward() {

Location expected = location.copy();

expected.forward();

ship.moveForward();

assertEquals(ship.getLocation(), expected);

}

Since Location already has the forward method, all we'd need to do is to make sure that the proper invocation of that method is performed. We created a new Location object called expected, invoked the forward method, and compared that object with the location of the ship after its moveForward method is called.

Note that specifications are not only used to validate the code, but are also used as executable documentation and, most importantly, as a way to think and design. This second attempt specifies more clearly what the intent is behind it. We should create a moveForward method inside the Ship class and make sure that the location.forward is called.

Implementation

With such a small and clearly defined specification, it should be fairly easy to write the code that implements it:

public boolean moveForward() {

return location.forward();

}

Specification – moving backward

Now that we have a forward movement specified and implemented, the backward movement should almost be the same:

public void whenMoveBackwardThenBackward() {

Location expected = location.copy();

expected.backward();

ship.moveBackward();

assertEquals(ship.getLocation(), expected);

}

[ 101 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

Implementation

Just like the specification, the backward movement implementation is just as easy: public boolean moveBackward() {

return location.backward();

}

The full source code for this requirement can be found in the req02-forward-backward branch of the tdd-java-ch04-ship repository

(https://bitbucket.org/vfarcic/tdd-java-ch04-ship/branch/req02-forward-

backward).

Requirement – rotating the ship

Moving the ship only back and forth won't get us far. We should be able to change the direction by rotating the ship to the left or right as well.

Implement commands that turn the ship left and right ( l and r).

After implementing the previous requirement, this one should be very easy since it can follow the same logic. The Location helper class already contains the turnLeft and turnRight methods that perform exactly what is required by this requirement. All we need to do is integrate them into the Ship class.

Specification – turning left

Using the same guidelines as those we have used so far, the specification for turning left can be the following:

public void whenTurnLeftThenLeft() {

Location expected = location.copy();

expected.turnLeft();

ship.turnLeft();

assertEquals(ship.getLocation(), expected);

}

[ 102 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

Implementation

You probably did not have a problem writing the code to pass the previous specification: public void turnLeft() {

location.turnLeft();

}

Specification – turning right

Turning right should be almost the same as turning left:

public void whenTurnRightThenRight() {

Location expected = location.copy();

expected.turnRight();

ship.turnRight();

assertEquals(ship.getLocation(), expected);

}

Implementation

Finally, let's finish this requirement by implementing the specification for turning right: public void turnRight() {

location.turnRight();

}

The full source for this requirement can be found in the req03-left-right branch of the tdd-java-ch04-ship repository

(https://bitbucket.org/vfarcic/tdd-java-ch04-ship/branch/req03-left-right).

Requirement – commands

Everything we have done so far was fairly easy since there were helper classes that provided all the functionality. This exercise was to learn how to stop attempting to test the end outcome and focus on a unit we're working on. We are building trust; we had to trust the code done by others (the helper classes).

[ 103 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

Starting from this requirement, you'll have to trust the code you wrote by yourself. We'll continue in the same fashion. We'll write specifications, run tests, and see them fail; we'll write implementations, run tests, and see them succeed; finally, we'll refactor if we think the code can be improved. Continue thinking how to test a unit (method) without going deeper into methods or classes that the unit will be invoking.

Now that we have individual commands (forwards, backwards, left, and right) implemented, it's time to tie it all together. We should create a method that will allow us to pass any number of commands as a single string. Each command should be a character with f meaning forwards, b being backwards, l for turning left, and r for turning right.

The ship can receive a string with commands (lrfb, which are equivalent to left, right, forwards, and backwards).

Specification – single commands

Let's start with the command argument, that only has the f (forwards) character: public void whenReceiveCommandsFThenForward() {

Location expected = location.copy();

expected.forward();

ship.receiveCommands("f");

assertEquals(ship.getLocation(), expected);

}

This specification is almost the same as the whenMoveForwardThenForward specification except that, this time, we're invoking the ship.receiveCommands("f") method.

Implementation

We already spoke about the importance of writing the simplest possible code that passes the specification.

[ 104 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

Write the simplest code to pass the test. This ensures a cleaner and clearer design and avoids unnecessary features

The idea is that the simpler the implementation, the better and easier it is to maintain the product. The idea adheres to the KISS principle. It states that most systems work best if they are kept simple rather than made

complex; therefore, simplicity should be a key goal in design and

unnecessary complexity should be avoided.

This is a good opportunity to apply this rule. You might be inclined to write a piece of code similar to the following:

public void receiveCommands(String commands) {

if (commands.charAt(0) == 'f') {

moveForward();

}

}

In this example code, we are verifying whether the first character is f and, if it is, invoking the moveForward method. There are many other variations that we can do. However, if we stick to the simplicity principle, a better solution would be the following: public void receiveCommands(String command) {

moveForward();

}

This is the simplest and shortest possible code that will make the specification pass. Later on, we might end up with something closer to the first version of the code; we might use some kind of a loop or come up with some other solution when things become more complicated. As for now, we are concentrating on one specification at a time and trying to make things simple. We are attempting to clear our mind by focusing only on the task at hand.

For brevity, the rest of the combinations (b, l, and r) are not presented here (continue to implement them by yourself). Instead, we'll jump to the last specification for this requirement.

[ 105 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

Specification – combined commands

Now that we are able to process one command (whatever that the command is), it is time to add the option to send a string of commands. The specification can be the following: public void whenReceiveCommandsThenAllAreExecuted() {

Location expected = location.copy();

expected.turnRight();

expected.forward();

expected.turnLeft();

expected.backward();

ship.receiveCommands("rflb");

assertEquals(ship.getLocation(), expected);

}

This is a bit longer, but is still not an overly complicated specification. We're passing commands rflb (right, forwards, left, and backwards) and expecting that the Location changes accordingly. As before, we're not verifying the end result (seeing whether the if coordinates have changed), but checking whether we are invoking the correct calls to helper methods.

Implementation

The end result can be the following:

public void receiveCommands(String commands) {

for (char command : commands.toCharArray()) {

switch(command) {

case 'f':

moveForward();

break;

case 'b':

moveBackward();

break;

case 'l':

turnLeft();

break;

case 'r':

turnRight();

break;

}

}

}

[ 106 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

If you tried to write specifications and the implementation by yourself and if you followed the simplicity rule, you probably had to refactor your code a couple of times in order to get to the final solution. Simplicity is the key and refactoring is often a welcome necessity.

When refactoring, remember that all specifications must be passing all the time.

Refactor only after all the tests have passed.

Benefits: refactoring is safe.

If all the implementation code that can be affected has tests and if they are all passing, it is relatively safe to refactor. In most cases, there is no need for new tests; small modifications to existing tests should be enough. The expected outcome of refactoring is to have all the tests passing both before and after the code is modified.

The full source for this requirement can be found in the req04-commands branch of the tdd-java-ch04-ship repository

(https://bitbucket.org/vfarcic/tdd-java-ch04-ship/branch/req04-commands).

Requirement – representing spheric maps

Earth is a sphere, as is any other planet. When Earth is presented as a map, reaching one edge wraps us to another; for example, when we move east and reach the furthest point in the Pacific Ocean, we are wrapped to the west side of the map and we continue moving towards America. Furthermore, to make the movement easier, we can define the map as a grid. That grid should have length and height expressed as an x-axis and y-axis. That grid should have maximum length (x) and height (y).

Implement wrapping from one edge of the grid to another.

[ 107 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

Specification – planet information

The first thing we can do is pass the Planet object with the maximum X and Y axis coordinates to the Ship constructor. Fortunately, Planet is one more of the helper classes that have already been made (and tested). All we need to do is instantiate it and pass it to the Ship constructor:

public void whenInstantiatedThenPlanetIsStored() {

Point max = new Point(50, 50);

Planet planet = new Planet(max);

ship = new Ship(location, planet);

assertEquals(ship.getPlanet(), planet);

}

We're defining the size of the planet as 50 x 50 and passing that to the Planet class. In turn, that class is afterwards passed to the Ship constructor. You might have noticed that the constructor needs an extra argument. In the current code, our constructor requires only location. To implement this specification, it should accept planet, as well.

How would you implement this specification without breaking any of the existing specifications?

Implementation

Let's take a bottom-up approach. An assert requires us to have a planet getter: private Planet planet;

public Planet getPlanet() {

return planet;

}

Next, the constructor should accept Planet as a second argument and assign it to the previously added planet variable. The first attempt might be to add it to the existing constructor, but that would break many existing specifications that are using a single argument constructor. This leaves us with only one option—a second constructor: public Ship(Location location) {

this.location = location;

}

public Ship(Location location, Planet planet) {

this.location = location;

this.planet = planet;

}

[ 108 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

Run all the specifications and confirm that they are all successful.

Refactoring

Our specifications forced us to create the second constructor, since changing the original one would break the existing tests. However, now that everything is green, we can do some refactoring and get rid of the single argument constructor. The specification class already has the beforeTest method that is run before each test. We can move everything, but the assert itself to this method:

public class ShipSpec {

...

private Planet planet;

@BeforeMethod

public void beforeTest() {

Point max = new Point(50, 50);

location = new Location(new Point(21, 13), Direction.NORTH);

planet = new Planet(max);

// ship = new Ship(location);

ship = new Ship(location, planet);

}

public void whenInstantiatedThenPlanetIsStored() {

// Point max = new Point(50, 50);

// Planet planet = new Planet(max);

// ship = new Ship(location, planet);

assertEquals(ship.getPlanet(), planet);

}

}

With this change, we effectively removed the usage of the Ship single argument constructor. By running all specifications, we should confirm that this change worked.

Now, with a single argument constructor that is not in use anymore, we can remove it from the implementation class, as well:

public class Ship {

...

// public Ship(Location location) {

// this.location = location;

// }

public Ship(Location location, Planet planet) {

this.location = location;

this.planet = planet;

[ 109 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

}

...

}

By using this approach, all specifications were green all the time. Refactoring did not change any existing functionality, nothing got broken, and the whole process was done quickly.

Now, let's move into wrapping itself.

Specification – dealing with map boundaries

Like in other cases, the helper classes already provide all the functionality that we need. So far, we used the location.forward method without arguments. To implement wrapping, there is the overloaded location.forward(Point max) method that will wrap the location when we reach the end of the grid. With the previous specification, we made sure that Planet is passed to the Ship class and that it contains Point max. Our job is to make sure that max is used when moving forward. The specification can be the following: public void whenOverpassingEastBoundaryThenPositionIsReset() {

location.setDirection(Direction.EAST);

location.getPoint().setX(planet.getMax().getX());

ship.receiveCommands("f");

assertEquals(location.getX(), 1);

}

Implementation

By now, you should be getting used to focusing on one unit at a time and to trust that those that were done before are working as expected. This implementation should be no different.

We just need to make sure that the maximum coordinates are used when the location.forward method is called:

public boolean moveForward() {

// return location.forward();

return location.forward(planet.getMax());

}

The same specification and implementation should be done for the backward method. For brevity, it is excluded from this book, but it can be found in the source code.

[ 110 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

The full source for this requirement can be found in the req05-wrap branch of the tddjava-ch04-ship repository

(https://bitbucket.org/vfarcic/tdd-java-ch04-ship/branch/req05-wrap).

Requirement – detecting obstacles

We're almost done. This is the last requirement.

Even though most of the Earth is covered in water (approximately 70%), there are continents and islands that can be considered as obstacles for our remotely-controlled ship.

We should have a way to detect whether our next move would hit one of those obstacles. If such a thing happens, the move should be aborted and the ship should stay on the current position and report the obstacle.

Implement surface detection before each move to a new position. If a

command encounters a surface, the ship aborts the move, stays on the

current position, and reports the obstacle.

The specifications and the implementation of this requirement are very similar to those we did previously, and we'll leave that to you.

Here are a few tips that can be useful:

The Planet object has the constructor that accepts a list of obstacles.

Each obstacle is an instance of the Point class.

The location.foward and location.backward methods have overloaded

versions that accept a list of obstacles. They return true if a move was successful and false if it failed. Use this Boolean to construct a status report required for the Ship.receiveCommands method.

The receiveCommands method should return a string with the status of each command. 0 can represent OK and X can be for a failure to move (00X0 = OK, OK, Failure, OK).

The full source for this requirement can be found in the req06-obstacles branch of the tdd-java-ch04-ship repository

(https://bitbucket.org/vfarcic/tdd-java-ch04-ship/branch/req06-obstacles).

[ 111 ]

Unit Testing – Focusing on What You Do and Not on What Has Been Done Chapter 4

Summary

In this chapter, we used TestNG as our testing framework of choice. There wasn't much difference when compared to JUnit, simply because we didn't use any of the more advanced features of TestNG (for example, data providers, factories, and so on). With TDD, it is questionable whether we'll ever have a need for those features.

Visit http://testng.org/, explore it, and decide for yourself which framework best suits your needs.

The main objective of this chapter was to learn how to focus on one unit at a time. We already had a lot of helper classes and we tried our best to ignore their internal workings. In many cases, we did not write specifications that verified that the end result was correct, but we checked whether the method we were working on invoked the correct method from those helper classes. In the real-world, you will be working on projects together with other team members, and it is important to learn how to focus on your tasks and trust that what others do works as expected. The same can be said for third-party libraries. It would be too expensive to test all inner processes that can happen when we invoke them. There are other types of tests that will try to cover those possibilities. When working with unit tests, the focus should only be on the unit we're currently working on.

Now that you have a better grasp of how to use unit tests effectively in the context of TDD, it is time to dive into some other advantages that TDD provides. Specifically, we'll explore how to design our applications better.

[ 112 ]

5

Design – If It's Not Testable, It's

Not Designed Well

"Simplicity is the ultimate sophistication."


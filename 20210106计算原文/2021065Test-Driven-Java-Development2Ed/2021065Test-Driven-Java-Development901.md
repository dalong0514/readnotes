Making It Young Again

TDD may not adjust to legacy code straight away. You may have to fiddle a bit with the steps to make it work. Understand that your TDD may change in this case, because somehow, you are no longer performing the TDD you were used to. This chapter will introduce you to the world of legacy code, taking as much as we can from TDD.

We'll start afresh, with a legacy application that is currently in production. We'll alter it in small ways without introducing defects or regressions, and we'll even have time to have an early lunch!

The following topics are covered in this chapter:

Legacy code

Dealing with legacy code

REST communication

Dependency injection

Tests at different levels: end-to-end, integration, and unit

Refactoring Legacy Code – Making It Young Again

Chapter 9

Legacy code

Let's start with the definition of legacy code. While there are many authors with different definitions, such as lack of trust in your application or your tests, code that is no longer supported, and so on. We like the one created by Michael Feathers the most:

"Legacy code is code without tests. The reason for this definition is that it is objective: either there are or there aren't tests."

– Michael Feathers

How do we detect legacy code? Although legacy code usually equates to bad code, Michael Feathers exposes some smells in his book, Working Effectively with Legacy Code, by Dorling Kindersley (India) Pvt. Ltd. (1993).

Code smell.

Smells are certain structures in the code that indicate violation of

fundamental design principles and negatively impact design quality.

Code smells are usually not bugs—they are not technically incorrect and do not currently prevent the program from functioning. Instead, they

indicate weaknesses in design that may be slowing down development or

increasing the risk of bugs or failures in the future.

Source: http://en.wikipedia.org/wiki/Code_smell.

One of the common smells for legacy code is I can't test this code. It is accessing outside resources, introducing other side effects, using a new operator, and so on. In general, good design is easy to test. Let's see some legacy code.

[ 211 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

Legacy code example

Software concepts are often easiest to explain through code, and this one is no exception.

We have seen and worked with the Tic-Tac-Toe application (see Chapter 3, Red-Green-Refactor – From Failure Through Success until Perfection). The following code performs position validation:

public class TicTacToe {

public void validatePosition(int x, int y) {

if (x < 1 || x > 3) {

throw new RuntimeException("X is outside board");

}

if (y < 1 || y > 3) {

throw new RuntimeException("Y is outside board");

}

}

}

The specification that corresponds with this code is as follows:

public class TicTacToeSpec {

@Rule

public ExpectedException exception =

ExpectedException.none();

private TicTacToe ticTacToe;

@Before

public final void before() {

ticTacToe = new TicTacToe();

}

@Test

public void whenXOutsideBoardThenRuntimeException() {

exception.expect(RuntimeException.class);

ticTacToe.validatePosition(5, 2);

}

@Test

public void whenYOutsideBoardThenRuntimeException() {

exception.expect(RuntimeException.class);

ticTacToe.validatePosition(2, 5);

}

}

[ 212 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

The JaCoCo report indicates that everything is covered (except the last line, the method's closing bracket):

As we believe we have good coverage, we can perform an automatic and safe refactor (fragment):

public class TicTacToe {

public void validatePosition(int x, int y) {

if (isOutsideTheBoard(x)) {

throw new RuntimeException("X is outside board");

}

if (isOutsideTheBoard(y)) {

throw new RuntimeException("Y is outside board");

}

}

private boolean isOutsideTheBoard(final int position) {

return position < 1 || position > 3;

}

}

This code should be ready, as the tests are successful and it has very good test coverage.

[ 213 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

Maybe you have already realized as much, but there is a catch. The message in the RuntimeException block is not checked for correctness; even the code coverage shows it as covering all the branches in that line.

What is coverage all about?

Coverage is a measure used to describe the degree to which the source

code of a program is tested by a particular test suite. Source:

http://en.wikipedia.org/wiki/Code_coverage.

Let's imagine a single end-to-end test that covers an easy part of the code. This test will get you a high coverage percentage, but not much security, as there are many other parts that are still not covered.

We have already introduced legacy code in our codebase—the exception messages. There might be nothing wrong with this as long as this is not an expected behavior—no one should depend on exception messages, not programmers to debug their programs, or logs, or even users. Those parts of the program that are not covered by tests are likely to suffer regressions in the near future. This might be fine if you accept the risk. Maybe the exception type and the line number are enough.

We have decided to remove the exception message, as it is not tested:

public class TicTacToe {

public void validatePosition(int x, int y) {

if (isOutsideTheBoard(x)) {

throw new RuntimeException("");

}

if (isOutsideTheBoard(y)) {

throw new RuntimeException("");

}

}

private boolean isOutsideTheBoard(final int position) {

return position < 1 || position > 3;

}

}

[ 214 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

Other ways to recognize legacy code

You may be familiar with some of the following common signs of legacy applications: A patch on top of a patch, just like a living Frankenstein application

Known bugs

Changes are expensive

Fragile

Difficult to understand

Old, outdated, static or, often, non-existent documentation

Shotgun surgery

Broken windows

Regarding the team that maintains it, these are some of the effects it produces on the members of the team:

Resignation: The people in charge of the software see a huge task in front of them

No one cares anymore: If you already have broken windows in your system, it is easier to introduce new ones

As legacy code is usually more difficult than other kinds of software, you would want your best people to work on it. However, we are often in a hurry imposed by deadlines, with the idea of programming the required functionalities as fast as possible and ignoring the quality of the solution.

Therefore, to avoid wasting our talented developers in such a bad way, we expect a non-legacy application to fulfill just the opposite. It should be:

Easy to change

Generalizable, configurable, and expansible

Easy to deploy

Robust

No known defects or limitations

Easy to teach to others/learn from others

Extensive suite of tests

Self-validating

Able to use keyhole surgery

[ 215 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

As we have outlined some of the properties of legacy and non-legacy code, it should be easy to replace some qualities with others. Right? Stop shotgun surgery and use keyhole surgery, a few more details and you are done. Isn't that right?

It is not as easy as it sounds. Luckily, there are some tricks and rules that, when applied, improve our code and the application comes closer to a non-legacy one.

A lack of dependency injection

This is one of the smells often detected in a legacy codebase. As there is no need to test the classes in isolation, the collaborators are instantiated where they are needed, putting the responsibility for creating collaborators and using them in the same class.

Here's an example, using the new operator:

public class BirthdayGreetingService {

private final MessageSender messageSender;

public BirthdayGreetingService() {

messageSender = new EmailMessageSender();

}

public void greet(final Employee employee) {

messageSender.send(employee.getAddress(),

"Greetings on your birthday");

}

}

In the current state, the BirthdayGreeting service is not unit-testable. It has the dependency to EmailMessageSender hardcoded in the constructor. It is not possible to replace this dependency without modifying the codebase (except for injecting objects using reflection or replacing objects on the new operator).

Modifying the codebase is always a source of possible regressions, so it should be done with caution. Refactoring requires tests, except when it is not possible.

The Legacy Code Dilemma.

When we change code, we should have tests in place. To put tests in place, we often have to change code.

[ 216 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

The legacy code change algorithm

When you have to make a change in a legacy codebase, here is an algorithm you can use: Identify change points

Find test points

Break dependencies

Write tests

Make changes and refactor

Applying the legacy code change algorithm

To apply this algorithm, we usually start with a suite of tests and always keep it green while refactoring. This is different from the normal cycle of TDD because refactoring should not introduce any new features (that is, it should not write any new specifications).

To better explain the algorithm, imagine that we received the following change request: To greet my employees in a more informal way, I want to send them a tweet instead of an email.

Identifying change points

The system is only able to send emails right now, so a change is necessary. Where? A quick investigation shows that the strategy for sending the greeting is decided in the constructor for the BirthdayGreetingService class following the strategy pattern

(https://en.wikipedia.org/?title=Strategy_pattern): public class BirthdayGreetingService {

public BirthdayGreetingService() {

messageSender = new EmailMessageSender();

}

[...]

}

[ 217 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

Finding test points

As the BirthdayGreetingService class does not have a collaborator injected that could be used to attach additional responsibilities to the object, the only option is to go outside this service class to test it. An option would be to change the EmailMessageSender class for a mock or fake implementation, but this would risk the implementation in that class.

Another option is to create an end-to-end test for this functionality:

public class EndToEndTest {

@Test

public void email_an_employee() {

final StringBuilder systemOutput =

injectSystemOutput();

final Employee john = new Employee(

new Email("john@example.com"));

new BirthdayGreetingService().greet(john);

assertThat(systemOutput.toString(),

equalTo("Sent email to "

+ "'john@example.com' with "

+ "the body 'Greetings on your "

+ "birthday'\n"));

}

// This code has been used with permission from

//GMaur's LegacyUtils:

// https://github.com/GMaur/legacyutils

private StringBuilder injectSystemOutput() {

final StringBuilder stringBuilder =

new StringBuilder();

final PrintStream outputPrintStream =

new PrintStream(

new OutputStream() {

@Override

public void write(final int b)

throws IOException {

stringBuilder.append((char) b);

}

});

System.setOut(outputPrintStream);

return stringBuilder;

}

}

[ 218 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

This code has been used with permission from https://github.com/GMaur/legacyutils.

This library helps you perform the technique of capturing the system out (System.out).

The name of the file does not end in Specification (or Spec), such as TicTacToeSpec, because this is not a specification. It is a test, to ensure the functionality remains constant.

The file has been named EndToEndTest because we try to cover as much functionality as possible.

Breaking dependencies

After having created a test that guarantees the expected behavior does not change, we will break the hardcoded dependency between BirthdayGreetingService and

EmailMessageSender. For this, we will use a technique called extract and override call, which is first explained in Michael Feathers' book:

public class BirthdayGreetingService {

public BirthdayGreetingService() {

messageSender = getMessageSender();

}

private MessageSender getMessageSender() {

return new EmailMessageSender();

}

[...]

Execute the tests again and verify that the lonely test we previously created still is green.

Additionally, we need to make this method protected or more open to be able to override it:

public class BirthdayGreetingService {

protected MessageSender getMessageSender() {

return new EmailMessageSender();

}

[...]

Now that the method can be overridden, we create a fake service to replace the original instance of the service. Introducing fakes in code is a pattern that consists of creating an object that could replace an existing one, with the particularity that we can control its behavior. This way, we can inject some customized fakes to achieve what we need. More information is available at http://xunitpatterns.com/.

[ 219 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

In this particular case, we should create a fake service that extends the original service. The next step is to override complicated methods in order to bypass irrelevant parts of code for testing purposes:

public class FakeBirthdayGreetingService

extends BirthdayGreetingService {

@Override

protected MessageSender getMessageSender() {

return new EmailMessageSender();

}

}

Now we can use the fake, instead of the BirthdayGreetingService class:

public class EndToEndTest {

@Test

public void email_an_employee() {

final StringBuilder systemOutput =

injectSystemOutput();

final Employee john = new Employee(

new Email("john@example.com"));

new FakeBirthdayGreetingService().greet(john);

assertThat(systemOutput.toString(),

equalTo("Sent email to "

+ "'john@example.com' with "

+ "the body 'Greetings on

+ "your birthday'\n"));

}

The test is still green.

We can now apply another dependency-breaking technique, parameterize constructor,

explained in Feathers paper at https:/​/​archive.​org/​details/

WorkingEffectivelyWithLegacyCode. The production code may look like this: public class BirthdayGreetingService {

public BirthdayGreetingService(final MessageSender

messageSender) {

this.messageSender = messageSender;

}

[...]

}

[ 220 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

Test code that corresponds to this implementation may be as follows:

public class EndToEndTest {

@Test

public void email_an_employee() {

final StringBuilder systemOutput =

injectSystemOutput();

final Employee john = new Employee(

new Email("john@example.com"));

new BirthdayGreetingService(new

EmailMessageSender()).greet(john);

assertThat(systemOutput.toString(),

equalTo("Sent email to "

+ "'john@example.com' with "

+ "the body 'Greetings on "

+ "your birthday'\n"));

}

[...]

We can also remove FakeBirthday, as it is no longer used.

Writing tests

While keeping the old end-to-end test, create an interaction to verify the integration of BirthdayGreetingService and MessageSender:

@Test

public void the_service_should_ask_the_messageSender() {

final Email address =

new Email("john@example.com");

final Employee john = new Employee(address);

final MessageSender messageSender =

mock(MessageSender.class);

new BirthdayGreetingService(messageSender)

.greet(john);

verify(messageSender).send(address,

"Greetings on your birthday");

}

At this point, a new TweetMessageSender can be written, completing the last step of the algorithm.

[ 221 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

The kata exercise

The only way a programmer will be able to improve is through practice. Creating programs of different types and using different technologies usually provide a programmer with new insights into software construction. Based on this idea, a kata is an exercise that defines some requirements or fixed features to be implemented in order to achieve some goals.

The programmer is asked to implement a possible solution and then compare it with others trying to find the best. The key value of this exercise is not getting the fastest implementation but discussing decisions taken while designing the solution. In most cases, all programs created in kata are dropped at the end.

The kata exercise in this chapter is about a legacy system. This is a sufficiently simple program to be processed in this chapter but also complex enough to pose some difficulties.

Legacy kata

You have been given a task to adopt a system that is already in production, a working piece of software for a book library: the Alexandria project.

The project currently lacks documentation, and the old maintainer is no longer available for discussion. So, should you accept this mission, it is going to be entirely your responsibility, as there is no one else to rely on.

Description

We have been able to recover these specification snippets from the time the original project was written:

The Alexandria software should be able to store books and lend them to users, who have the power to return them. The user can also query the system for books, by author, book title, status, and ID.

There is no time frame for returning the books.

The books can also be censored as this is considered important for business reasons.

The software should not accept new users.

The user should be told, at any moment, the server's time.

[ 222 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

Technical comments

The Alexandria is a backend project written in Java, which communicates information to the frontend using a REST API. For the purpose of this kata exercise, persistence has been implemented as an in-memory object, using the fake test double explained

at http://xunitpatterns.com/Fake%20Object.html.

The code is available at https://bitbucket.org/vfarcic/tdd-java-alexandria.

Adding a new feature

Until the point of adding a new feature, the legacy code might not be a disturbance to the programmer's productivity. The codebase is in a state that is worse than desired, but the production systems work without any inconvenience.

Now is the time when the problems start to appear. The product owner (PO) wants to add a new feature.

For example, as a library manager, I want to know all the history for a given book so that I can measure which books are more in demand than others.

Black-box or spike testing

As the old maintainer of the Alexandria project is no longer available for questions and there is no documentation, black-box testing is more difficult. Thus, we decide to get to know the software better through investigation and then doing some spikes that will leak internal knowledge to us about the system.

We will later use this knowledge to implement the new feature.

Black-box testing is a method of software testing that examines the

functionality of an application without peering into its internal structures or workings. This type of test can be applied to virtually every level of software testing: unit, integration, system, and acceptance. It typically most if not all higher-level testing, but can dominate unit testing as well.

Source: http://en.wikipedia.org/wiki/Black-box_testing.

[ 223 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

Preliminary investigation

When we know the required feature, we will start looking at the Alexandria project: 15 files

Gradle-based (build.gradle)

0 tests

Firstly, we want to confirm that this project has never been tested, and the lack of a test folder reveals so:

$ find src/test

find: src/test: No such file or directory

These are the folder contents for the Java part:

$ cd src/main/java/com/packtpublishing/tddjava/ch09/alexandria/

$ find .

.

./Book.java

./Books.java

./BooksEndpoint.java

./BooksRepository.java

./CustomExceptionMapper.java

./MyApplication.java

./States.java

./User.java

./UserRepository.java

./Users.java

Here is the rest:

$ cd src/main

$ find resources webapp

resources

resources/applicationContext.xml

webapp

webapp/WEB-INF

webapp/WEB-INF/web.xml

This seems to be a web project (indicated by the web.xml file) using Spring (indicated by the applicationContext.xml). The dependencies in the build.gradle show the following (fragment):

compile 'org.springframework:spring-web:4.1.4.RELEASE'

[ 224 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

Having Spring is already a good sign, as it can help with the dependency injection, but a quick look showed that the context is not really being used. Maybe something that was used in the past?

In the web.xml file, we can find this fragment:

<?xml version="1.0" encoding="UTF-8"?>

<web-app version="3.0" xmlns="http://java.sun.com/xml/ns/javaee"

xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

xsi:schemaLocation="http://java.sun.com/xml/ns/javaee

http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd">

<module-name>alexandria</module-name>

<context-param>

<param-name>contextConfigLocation</param-name>

<param-value>classpath:applicationContext.xml</param-value>

</context-param>

<servlet>

<servlet-name>SpringApplication</servlet-name>

<servlet-class>

org.glassfish.jersey.servlet.ServletContainer</servlet-class>

<init-param>

<param-name>javax.ws.rs.Application</param-name>

<param-

value>com.packtpublishing.tddjava.alexandria.MyApplication</param-value>

</init-param>

<load-on-startup>1</load-on-startup>

</servlet>

In this file, we discover the following:

The context in applicationContext.xml will be loaded

There is an application file

(com.packtpublishing.tddjava.alexandria.MyApplication) that will be

executed inside a servlet

[ 225 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

The MyApplication file is as follows:

public class MyApplication extends ResourceConfig {

public MyApplication() {

register(RequestContextFilter.class);

register(BooksEndpoint.class);

register(JacksonJaxbJsonProvider.class);

register(CustomExceptionMapper.class);

}

}

This configures the necessary classes for executing the BooksEndpoint endpoint (fragment):

@Path("books")

@Component

public class BooksEndpoint {

private BooksRepository books = new BooksRepository();

private UserRepository users = new UserRepository();

In this last snippet, we can find one of the first indicators that this is a legacy codebase—both dependencies (books and users) are created inside the endpoint and not injected. This makes unit testing more difficult.

We can start by writing down the element that will be used during refactoring; we write the code for the dependency injection in BooksEndpoint.

How to find candidates for refactoring

There are different paradigms of programming (for example, functional, imperative, and object-oriented) and styles (for example, compact, verbose, minimalistic, and too clever).

Therefore, the candidates for refactoring are different from one person to the other.

There is another way, as opposed to subjectively, of finding candidates for refactoring—objectively. There are many papers investigating how to find candidates for refactoring objectively. This is just an introduction and it is left to the reader to learn more about these techniques.

[ 226 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

Introducing the new feature

After getting to know the code more, it seems that the most important functional change is to replace the current status (fragment):

@XmlRootElement

public class Book {

private final String title;

private final String author;

private int status; //<- this attribute

private int id;

And replace it with a collection of them (fragment):

@XmlRootElement

public class Book {

private int[] statuses;

// ...

This might seem to work (after changing all access to the field to the array, for example), but this also prompts a functional requirement.

The Alexandria software should be able to store books and lend them to users who have the power to return them. The user can also query the system for books, by author, book title, status, and ID.

The PO confirms that searching books via status has now changed now, it also allows searching for any previous status.

This change is getting bigger and bigger. Whenever we feel that the time for removing this legacy code has come, we start applying the legacy code algorithm.

We have also detected a primitive obsession and feature envy smell: storing the status as an integer (primitive obsession) and then actuating on another object's state (feature envy).

We will add this to the following to-do list:

Dependency injection in BooksEndpoint for books

Change status for statuses

Remove the primitive obsession with status (optional)

[ 227 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

Applying the legacy code algorithm

In this case, the whole middle-end works as a standalone, using in-memory persistence. The same algorithm could be used if the persistence was saved into a database, but we would require some extra code to clean and populate the database between test runs.

We'll use DbUnit. More information can be found at http://dbunit.sourceforge.net/.

Writing end-to-end test cases

The first step we've decided to take to ensure that behavior is maintained during refactoring is to write end-to-end tests. In other applications that include frontends, this could be using a higher-level tool, such as Selenium/Selenide.

In our case, as the frontend is not subject to refactoring, the tool can be lower-level. We have chosen to write HTTP requests for the purpose of end-to-end tests.

These requests should be automatic and testable, and should follow all existing rules for automatic tests or specifications. As we were discovering the real application behavior while writing these tests, we have decided to write a spike in a tool called Postman.

The product website is here: https://www.getpostman.com/. This is also possible with a tool called curl (http://curl.haxx.se/).

What is curl?

curl is a command-line tool and library for transferring data with URL

syntax, supporting [...] HTTP, HTTPS, [...], HTTP POST, HTTP PUT,

and [...].

What's curl used for?

curl is used in command lines or scripts to transfer data.

Source: http://curl.haxx.se/.

To do this, we decide to execute the legacy software locally with the following line:

./gradlew clean jettyRun

This fires up a local jetty server that processes requests. The big benefit is that deployment is done automatically and there is no need to package everything and manually deploy to an application server (for example, JBoss AS, GlassFish, Geronimo, and TomEE). This can greatly speed up the process of making changes and seeing the effects, therefore decreasing the feedback lead time. Later on, we will start the server programmatically from Java code.

[ 228 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

We start looking for functionalities. As we discovered earlier that the BooksEndpoint class contains the webservice endpoint definitions, this is a good place to start looking for functionalities. They are listed as follows:

1. Add a new book

2. List all the books

3. Search for books by ID, by author, by title, and by status

4. Prepare this book to be rented

5. Rent this book

6. Censor this book

7. Uncensor the book

We launch the server manually and start writing requests:

[ 229 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

These tests seem good enough for a spike. One thing that we have realized is that each response contains a timestamp, so this makes our automation more difficult: For the tests to have more value, they should be automated and exhaustive. For the moment, they are not, so we consider them spikes. They will be automated in the future.

[ 230 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

Each and every single test that we perform is not automated. In this case, the tests from the Postman interface are much faster to write than the

automated ones. Also, the experience is far more representative of what production use would be like. The test client (thankfully, in this case) could introduce some problems with the production one, and therefore

not return trusted results.

In this particular case, we have found that the Postman tests are a better investment because, even after writing them, we will throw them away.

They give very rapid feedback on the API and results. We also use this

tool for prototyping the REST APIs, as its tools are both effective and useful.

The general idea here is this: depending on whether you want to save

those tests for the future or not, use one tool or another. This also depends on how often you want to execute them, and in which environment.

After writing down all the requests, these are the states that we have found in the application, represented by a state diagram:

After these tests are ready and we start to understand the application, it is time to automate the tests. After all, if they are not automated, we don't really feel confident enough for refactoring.

[ 231 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

Automating the test cases

We start the server programmatically. For this, we have decided to use a Grizzly (https:/​/

javaee.​github.​io/​grizzly/​), which allows us to start the server using the configuration from Jersey's ResourceConfig (FQCN:

org.glassfish.jersey.server.ResourceConfig), as shown in the test

BooksEndpointTest (fragment).

The code can be found at https://bitbucket.org/vfarcic/tdd-java-alexandria: public class BooksEndpointTest {

public static final URI FULL_PATH =

URI.create("http://localhost:8080/alexandria");

private HttpServer server;

@Before

public void setUp() throws IOException {

ResourceConfig resourceConfig =

new MyApplication();

server = GrizzlyHttpServerFactory

.createHttpServer(FULL_PATH, resourceConfig);

server.start();

}

@After

public void tearDown(){

server.shutdownNow();

}

This prepares a local server at the address http://localhost:8080/alexandria. It will only be available for a short period of time (while the tests run), so, if you need to manually access the server, whenever you want to pause the execution, insert a call to the following method:

public void pauseTheServer() throws Exception {

System.in.read();

}

When you want to stop the server, stop the execution or hit Enter in the allocated console.

Now we can start the server programmatically, pause it (with the preceding method), and execute the spike again. The results are the same, so the refactor is successful.

We add the first automated test to the system.

[ 232 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

The code can be found at https://bitbucket.org/vfarcic/tdd-java-alexandria: public class BooksEndpointTest {

public static final String AUTHOR_BOOK_1 =

"Viktor Farcic and Alex Garcia";

public static final String TITLE_BOOK_1 =

"TDD in Java";

private final Map<String, String> TDD_IN_JAVA;

public BooksEndpointTest() {

TDD_IN_JAVA = getBookProperties(TITLE_BOOK_1,

AUTHOR_BOOK_1);

}

private Map<String, String> getBookProperties

(String title, String author) {

Map<String, String> bookProperties =

new HashMap<>();

bookProperties.put("title", title);

bookProperties.put("author", author);

return bookProperties;

}

@Test

public void add_one_book() throws IOException {

final Response books1 = addBook(TDD_IN_JAVA);

assertBooksSize(books1, is("1"));

}

private void assertBooksSize(Response response,

Matcher<String> matcher) {

response.then().body(matcher);

}

private Response addBook

(Map<String, ?> bookProperties) {

return RestAssured

.given().log().path()

.contentType(ContentType.URLENC)

.parameters(bookProperties)

.post("books");

}

For testing purposes, we're using a library called RestAssured (https:/​/​github.​com/

rest-​assured/​rest-​assured) that allows for easier testing of REST and JSON.

[ 233 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

To complete the automated test suite, we create these tests:

add_one_book()

add_a_second_book()

get_book_details_by_id()

get_several_books_in_a_row()

censor_a_book()

cannot_retrieve_a_censored_book()

The code can be found at https://bitbucket.org/vfarcic/tdd-java-alexandria/.

Now that we have a suite that ensures that no regression is introduced, we take a look at the following to-do list:

1. Dependency injection in BooksEndpoint for books

2. Change status for statuses

3. Remove the primitive obsession with status (optional)

We will tackle dependency injection first.

Injecting the BookRepository dependency

The code for the BookRepository dependency is in BooksEndpoint (fragment):

@Path("books")

@Component

public class BooksEndpoint {

private BooksRepository books =

new BooksRepository();

[...]

Extract and override call

We will apply the already introduced refactoring technique extract and override call. For this, we create a failing specification, as shown here:

@Test

public void add_one_book() throws IOException {

addBook(TDD_IN_JAVA);

[ 234 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

Book tddInJava = new Book(TITLE_BOOK_1,

AUTHOR_BOOK_1,

States.fromValue(1));

verify(booksRepository).add(tddInJava);

}

To pass this red specification, also known as a failing specificiation, we will first extract the dependency creation to a protected method in the BookRepository class:

@Path("books")

@Component

public class BooksEndpoint {

private BooksRepository books =

getBooksRepository();

[...]

protected BooksRepository

getBooksRepository() {

return new BooksRepository();

}

[...]

We copy the MyApplication launcher to this:

public class TestApplication

extends ResourceConfig {

public TestApplication

(BooksEndpoint booksEndpoint) {

register(booksEndpoint);

register(RequestContextFilter.class);

register(JacksonJaxbJsonProvider.class);

register(CustomExceptionMapper.class);

}

public TestApplication() {

this(new BooksEndpoint(

new BooksRepository()));

}

}

[ 235 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

This allows us to inject any BooksEndpoint. In this case, in the test

BooksEndpointInteractionTest, we will override the dependency getter with a mock.

In this way, we can check that the necessary calls are being made (fragment from BooksEndpointInteractionTest):

@Test

public void add_one_book() throws IOException {

addBook(TDD_IN_JAVA);

verify(booksRepository)

.add(new Book(TITLE_BOOK_1,

AUTHOR_BOOK_1, 1));

}

Run the tests; everything is green. Even though the specifications are successful, we have introduced a piece of design only for test purposes, and the production code is not executing this new launcher, TestApplication, but is still executing the old MyApplication. To solve this, we have to unify both launchers into one. This can be solved with the refactor parametrize constructor, also explained in Roy Osherove's book, The Art of Unit Testing (http://artofunittesting.com).

Parameterizing a constructor

We can unify the launchers by accepting a BooksEndpoint dependency. If we don't specify it, it will register the dependency with the real instance of BooksRepository. Otherwise, it will register the received one:

public class MyApplication

extends ResourceConfig {

public MyApplication() {

this(new BooksEndpoint(

new BooksRepository()));

}

public MyApplication

(BooksEndpoint booksEndpoint) {

register(booksEndpoint);

register(RequestContextFilter.class);

register(JacksonJaxbJsonProvider.class);

register(CustomExceptionMapper.class);

}

}

In this case, we have opted for constructor chaining to avoid repetition in the constructors.

[ 236 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

After doing this refactor, the BooksEndpointInteractionTest class is as follows in its final state:

public class BooksEndpointInteractionTest {

public static final URI FULL_PATH = URI.

create("http://localhost:8080/alexandria");

private HttpServer server;

private BooksRepository booksRepository;

@Before

public void setUp() throws IOException {

booksRepository = mock(BooksRepository.class);

BooksEndpoint booksEndpoint =

new BooksEndpoint(booksRepository);

ResourceConfig resourceConfig =

new MyApplication(booksEndpoint);

server = GrizzlyHttpServerFactory

.createHttpServer(FULL_PATH, resourceConfig);

server.start();

}

The first test passed, so we can mark the dependency injection task as done.

Tasks performed:

Dependency injection in BooksEndpoint for books

The to-do list:

Change status for statuses

Remove the primitive obsession with status (optional)

Adding a new feature

Once we have the necessary test environment in place, we can add the new feature.

As a library manager, I want to know all the history for a given book so that I can measure which books are more in demand than others.

We will start with a red specification:

public class BooksSpec {

@Test

[ 237 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

public void should_search_for_any_past_state() {

Book book1 = new Book("title", "author",

States.AVAILABLE);

book1.censor();

Books books = new Books();

books.add(book1);

String available =

String.valueOf(States.AVAILABLE);

assertThat(

books.filterByState(available).isEmpty(),

is(false));

}

}

Run all the tests and see the last one fail.

Implement the search on all states (fragment):

public class Book {

private ArrayList<Integer> status;

public Book(String title, String author, int status) {

this.title = title;

this.author = author;

this.status = new ArrayList<>();

this.status.add(status);

}

public int getStatus() {

return status.get(status.size()-1);

}

public void rent() {

status.add(States.RENTED);

}

[...]

public List<Integer> anyState() {

return status;

}

[...]

[ 238 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

In this fragment, we have omitted the irrelevant parts—things that were not modified, or more modifier methods, such as rent, that have changed the implementation in the same fashion:

public class Books {

public Books filterByState(String state) {

Integer expectedState = Integer.valueOf(state);

return new Books(

new ConcurrentLinkedQueue<>(

books.stream()

.filter(x

-> x.anyState()

.contains(expectedState))

.collect(toList())));

}

[...]

The outside methods, especially the serialization to JSON, are not affected, as the getStatus method still returns an int value.

We run all the tests and everything is green.

Tasks performed:

Dependency injection in BooksEndpoint for books

Change status for statuses

The to-do list:

Remove the primitive obsession with status (optional)

Removing the primitive obsession with status as

int

We have decided to also tackle the optional item in our to-do list.

The to-do list:

Dependency injection in BooksEndpoint for books

Change status for statuses

Remove the primitive obsession with status (optional)

[ 239 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

The smell: Primitive obsession involves using primitive data types to represent domain ideas. For example, we use a string to represent a

message, an integer to represent an amount of money, or a

struct/dictionary/hash to represent a specific object.

The source is http://c2.com/cgi/wiki?PrimitiveObsession.

As this is a refactor step (that is, we are not introducing any new behavior into the system), we don't need any new specification. We will proceed and try to always stay green, or leave it for as little time as possible.

We have converted States from a Java class with constants:

public class States {

public static final int BOUGHT = 1;

public static final int RENTED = 2;

public static final int AVAILABLE = 3;

public static final int CENSORED = 4;

}

And turned it into an enum:

enum States {

BOUGHT (1),

RENTED (2),

AVAILABLE (3),

CENSORED (4);

private final int value;

private States(int value) {

this.value = value;

}

public int getValue() {

return value;

}

public static States fromValue(int value) {

for (States states : values()) {

if(states.getValue() == value) {

return states;

}

}

throw new IllegalArgumentException(

"Value '" + value

[ 240 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

+ "' could not be found in States");

}

}

Adapt the tests as follows:

public class BooksEndpointInteractionTest {

@Test

public void add_one_book() throws IOException {

addBook(TDD_IN_JAVA);

verify(booksRepository).add(

new Book(TITLE_BOOK_1, AUTHOR_BOOK_1,

States.BOUGHT));

}

[...]

public class BooksTest {

@Test

public void should_search_for_any_past_state() {

Book book1 = new Book("title", "author",

States.AVAILABLE);

book1.censor();

Books books = new Books();

books.add(book1);

assertThat(books.filterByState(

String.valueOf(

States.AVAILABLE.getValue()))

.isEmpty(), is(false));

}

[...]

Adapt the production code. The code snippet is as follows:

@XmlRootElement

public class Books {

public Books filterByState(String state) {

State expected =

States.fromValue(Integer.valueOf(state));

return new Books(

new ConcurrentLinkedQueue<>(

books.stream()

.filter(x -> x.anyState()

.contains(expected))

.collect(toList())));

}

[...]

[ 241 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

Also the following:

@XmlRootElement

public class Book {

private final String title;

private final String author;

@XmlTransient

private ArrayList<States> status;

private int id;

public Book

(String title, String author, States status) {

this.title = title;

this.author = author;

this.status = new ArrayList<>();

this.status.add(status);

}

public States getStatus() {

return status.get(status.size() - 1);

}

@XmlElement(name = "status")

public int getStatusAsInteger(){

return getStatus().getValue();

}

public List<States> anyState() {

return status;

}

[...]

In this case, the serialization has been done using the annotation:

@XmlElement(name = "status")

This converts the result of the method into the field named status.

Also, the status field, now ArrayList<States>, is marked with @XmlTransient so it is not serialized to JSON.

We execute all the tests and they are green, so we can now cross off the optional element in our to-do list.

[ 242 ]

Refactoring Legacy Code – Making It Young Again

Chapter 9

Tasks performed:

Dependency injection in BooksEndpoint for books

Change status for statuses

Remove the primitive obsession with status (optional)

Summary

As you already know, inheriting a legacy codebase may be a daunting task.

We stated that legacy code is code without tests, so the first step in dealing with it is to create tests to help you preserve the same functionality during the process. Unfortunately, creating tests is not always as easy as it sounds. Many times, legacy code is tightly coupled and presents other symptoms that show a poor design or at least a lack of interest in the code's quality in the past. Worry not: you can perform some of the tedious tasks step by step, as shown in http://martinfowler.com/bliki/ParallelChange.html. Moreover, it is also well known that software development is a learning process. Working code is a side effect. Therefore, the most important part is to learn more about the codebase, to be able to modify it with security. Please visit

http://www.slideshare.net/ziobrando/model-storming for more information.

Finally, we encourage you to read Michael Feathers book called Working Effectively with Legacy Code. It has plenty of techniques for this kind of codebase, and as a result is very useful for understanding the whole process.

[ 243 ]

10

Feature Toggles – Deploying

Partially Done Features to

Production

"Do not let circumstances control you. You change your circumstances."


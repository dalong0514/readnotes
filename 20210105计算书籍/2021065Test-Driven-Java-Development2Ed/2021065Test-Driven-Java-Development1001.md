– Jackie Chan

We have seen so far how TDD makes the development process easier and decreases the amount of time spent on writing quality code. But there's another particular benefit to this.

As code is being tested and its correctness is proven, we can go a step further and assume that our code is production-ready once all tests have passed.

There are some software life cycle approaches based on this idea. Some extreme programming (XP) practices such as continuous integration (CI), continuous delivery, and continuous deployment (CD) will be introduced. The code examples can be found at https:/​/​bitbucket.​org/​alexgarcia/​packt-​tdd-​java/​src/​, in the folder 10-feature-toggles.

The following topics will be covered in this chapter:

Continuous integration, delivery, and deployment

Testing the application in production

Feature Toggles

Feature Toggles – Deploying Partially Done Features to Production Chapter 10

Continuous integration, delivery, and

deployment

TDD goes hand in hand with CI, continuous delivery, or CD. Differences aside, all three techniques have similar goals. They are all trying to foster the continuous verification of production readiness of our code. In that respect, they are very similar to TDD. They each promote very short development cycles, continuous verification of the code we're producing, and the intention to continuously keep our application in a production-ready state.

The scope of this book does not permit us to go into the details of those techniques. Indeed, a whole book could be written on this subject. We'll just briefly explain the differences between the three. Practicing CI means that our code is at (almost) all times integrated with the rest of the system, and if there is a problem it will surface quickly. If such a thing happens, the priority is to fix the cause of that problem, meaning that any new development must take lower priority. You might have noticed a similarity between this definition and the way TDD works. The major difference is that with TDD, our primary focus is not the integration with the rest of the system. The rest is the same. Both TDD and CI try to detect problems fast and treat fixing them as the highest priority, putting everything else on hold.

CI does not have the whole pipeline automated, and additional manual verifications are needed before the code is deployed to production.

Continuous delivery is very similar to CI, except that the former goes a bit further and has the whole pipeline automated, except the actual deployment to production. Every push to the repository that passed all verifications is considered valid for deployment to production. However, the decision to deploy is made manually. Someone needs to choose one of the builds and promote it to the production environment. The choice is political or functional. It depends on what and when we want our users to receive, even though each is production-ready.

"Continuous Delivery is a software development discipline where you build software in such a way that the software can be released to production at any time."

– Martin Fowler

Finally, CD is accomplished when the decision about what to deploy is automated as well.

In this scenario, every commit that passed all verifications is deployed to production—no exceptions.

[ 245 ]

Feature Toggles – Deploying Partially Done Features to Production Chapter 10

In order to continuously integrate or deliver our code to production, branches cannot exist, or the time between creating them and integrating them with the mainline must be very short (less than a day, preferably a few hours). If that is not the case, we are not continuously verifying our code.

The true connection with TDD comes from the necessity to create validations before the code is committed. If those verifications are not created in advance, code pushed to the repository is not accompanied with tests and the process fails. Without tests, there is no confidence in what we did. Without TDD, there are no tests to accompany our implementation code. Alternatively, a delay in pushing commits to repository until tests are created but in that case, there is no continuous part of the process. Code is sitting on someone's computer until someone else is finished with tests. Code that sits somewhere is not continuously verified against the whole system.

To summarize, continuous integration, delivery, and deployment rely on tests to accompany the integration code (thus, relying on TDD) and on the practice of not using branches or having them very short-lived (very often merged to the mainline). The problem lies with the fact that some features cannot be developed that fast. No matter how small our features are, in some cases it might take days to develop them. During all that time, we cannot push to the repository because the process would deliver them to production. Users do not want to see partial features. There is no point having, for example, part of the login process delivered. If one were to see a login page with a username, password, and login button, but the process behind that button does not actually store that info and provides, let's say, an authentication cookie, then at best we would have confused the users. In some other cases, one feature cannot work without the other. Following the same example, even if a login feature is fully developed, without registration it is pointless. One cannot be used without the other.

Imagine playing a puzzle. We need to have a rough idea of the final picture, but we are focused on one piece at the time. We pick a piece that we think is the easiest to place and combine it with its neighbors. Only when all of them are in place is the picture complete and we are finished.

The same applies to TDD. We develop our code by being focused on small units. As we progress, they start taking a shape and working with each other until they are all integrated.

While we're waiting for that to happen, even though all our tests are passing and we are in a green state, the code is not ready for the end users.

The easiest way to solve those problems and not compromise on TDD and CI/CD is to use Feature Toggles.

[ 246 ]

Feature Toggles – Deploying Partially Done Features to Production Chapter 10

Feature Toggles

You might have also heard about this as Feature Flipping or Feature Flags. No matter which expression we use, they are all based on a mechanism that permits you to turn on and off the features of your application. This is very useful when all code is merged into one branch and you must deal with partially finished (or integrated) code. With this technique, unfinished features can be hidden so that users cannot access them.

Due to its nature, there are other possible uses for this functionality. As a circuit breaker when something is wrong with a particular feature, providing graceful degradation of the application, shutting down secondary features to preserve hardware resources for business core operations, and so on. Feature Toggles, in some cases, can go even further. We might use them to enable features only to certain users, based on, for example, geographic location or their role. Another use is that we can enable new features for our testers only. That way, end users would continue to be oblivious of the existence of some new features, while testers would be able to validate them on a production server.

Moreover, there are some aspects to remember when using Feature Toggles: Use toggles only until they are fully deployed and proven to work. Otherwise, you might end up with spaghetti code full of if/else statements containing old toggles that are not in use any more.

Do not spend too much time testing toggles. It is, in most cases, enough to confirm that the entry point into some new feature is not visible. That can be, for example, a link to the new feature.

Do not overuse toggles. Do not use them when there is no need for them. For example, you might be developing a new screen that is accessible through a link in the home page. If that link is added at the end, there might be no need to have a toggle that hides it.

There are many good frameworks and libraries for application feature handling. Two of them are the following:

Togglz (http://www.togglz.org/) FF4J (http://ff4j.org/)

These libraries offer a sophisticated way to manage features, even adding role-based or rules-based feature access. In many cases, you aren't going to need it, but these capabilities bring us the possibility of testing a new feature in production without opening it to all users. However, implementing a custom basic solution for feature toggling is quite simple, and we are going to go through an example to illustrate this.

[ 247 ]

Feature Toggles – Deploying Partially Done Features to Production Chapter 10

A Feature Toggle example

Here we go with our demo application. This time, we're going to build a simple and small REpresentational State Transfer (REST) service to compute, on demand, a concrete Nth position of Fibonacci's sequence. We will keep track of enabled/disabled features using a file. For simplicity, we will use Spring Boot as our framework of choice and Thymeleaf as a template engine. This is also included in the Spring Boot dependency. Find more information about Spring Boot and related projects at

http://projects.spring.io/spring-boot/. Also, you can visit

http://www.thymeleaf.org/ to read more about the template engine.

This is how the build.gradle file looks:

apply plugin: 'java'

apply plugin: 'application'

sourceCompatibility = 1.8

version = '1.0'

mainClassName = "com.packtpublishing.tddjava.ch09.Application"

repositories {

mavenLocal()

mavenCentral()

}

dependencies {

compile group: 'org.springframework.boot',

name: 'spring-boot-starter-thymeleaf',

version: '1.2.4.RELEASE'

testCompile group: 'junit',

name: 'junit',

version: '4.12'

}

Note that application plugin is present because we want to run the application using the Gradle command run. Here is the application's main class:

@SpringBootApplication

public class Application {

public static void main(String[] args) {

SpringApplication.run(Application.class, args);

}

}

[ 248 ]

Feature Toggles – Deploying Partially Done Features to Production Chapter 10

We will create the properties file. This time, we are going to use YAML Ain't Markup Language (YAML) format, as it is very comprehensive and concise. Add a file called application.yml in the src/main/resources folder, with the following content: features:

fibonacci:

restEnabled: false

Spring offers a way to load this kind of property file automatically. Currently, there are only two restrictions: the name must be application.yml and/or the file should be included in the application's class path.

This is our implementation of the feature's config file:

@Configuration

@EnableConfigurationProperties

@ConfigurationProperties(prefix = "features.fibonacci")

public class FibonacciFeatureConfig {

private boolean restEnabled;

public boolean isRestEnabled() {

return restEnabled;

}

public void setRestEnabled(boolean restEnabled) {

this.restEnabled = restEnabled;

}

}

This is the fibonacci service class. This time, the computation operation will always return -1, just to simulate a partially done feature:

@Service("fibonacci")

public class FibonacciService {

public int getNthNumber(int n) {

return -1;

}

}

We also need a wrapper to hold the computed values:

public class FibonacciNumber {

private final int number, value;

public FibonacciNumber(int number, int value) {

this.number = number;

[ 249 ]

Feature Toggles – Deploying Partially Done Features to Production Chapter 10

this.value = value;

}

public int getNumber() {

return number;

}

public int getValue() {

return value;

}

}

This is the FibonacciRESTController class, responsible for handling the fibonacci service queries:

@RestController

public class FibonacciRestController {

@Autowired

FibonacciFeatureConfig fibonacciFeatureConfig;

@Autowired

@Qualifier("fibonacci")

private FibonacciService fibonacciProvider;

@RequestMapping(value = "/fibonacci", method = GET)

public FibonacciNumber fibonacci(

@RequestParam(

value = "number",

defaultValue = "0") int number) {

if (fibonacciFeatureConfig.isRestEnabled()) {

int fibonacciValue = fibonacciProvider

.getNthNumber(number);

return new FibonacciNumber(number, fibonacciValue);

} else throw new UnsupportedOperationException();

}

@ExceptionHandler(UnsupportedOperationException.class)

public void unsupportedException(HttpServletResponse response)

throws IOException {

response.sendError(

HttpStatus.SERVICE_UNAVAILABLE.value(),

"This feature is currently unavailable"

);

}

@ExceptionHandler(Exception.class)

public void handleGenericException(

[ 250 ]

Feature Toggles – Deploying Partially Done Features to Production Chapter 10

HttpServletResponse response,

Exception e) throws IOException {

String msg = "There was an error processing " +

"your request: " + e.getMessage();

response.sendError(

HttpStatus.BAD_REQUEST.value(),

msg

);

}

}

Note that the fibonacci method is checking whether the fibonacci service should be enabled or disabled, throwing an UnsupportedOperationException for convenience in the last case. There are also two error-handling functions; the first one is for processing UnsupportedOperationException and the second is for generic exceptions handling.

Now that all the components have been set, all we need to do is execute Gradle's run command:

$> gradle run

The command will launch a process that will eventually set a server up on the following address: http://localhost:8080. This can be observed in the console output:

...

2015-06-19 03:44:54.157 INFO 3886 --- [ main]

o.s.w.s.handler.SimpleUrlHandlerMapping : Mapped URL path [/webjars/**]

onto handler of type [class

org.springframework.web.servlet.resource.ResourceHttpRequestHandler]

2015-06-19 03:44:54.160 INFO 3886 --- [ main]

o.s.w.s.handler.SimpleUrlHandlerMapping : Mapped URL path [/**] onto handler of type [class

org.springframework.web.servlet.resource.ResourceHttpRequestHandler]

2015-06-19 03:44:54.319 INFO 3886 --- [ main]

o.s.w.s.handler.SimpleUrlHandlerMapping : Mapped URL path

[/**/favicon.ico] onto handler of type [class

org.springframework.web.servlet.resource.ResourceHttpRequestHandler]

2015-06-19 03:44:54.495 INFO 3886 --- [ main]

o.s.j.e.a.AnnotationMBeanExporter : Registering beans for JMX

exposure on startup

2015-06-19 03:44:54.649 INFO 3886 --- [ main]

s.b.c.e.t.TomcatEmbeddedServletContainer : Tomcat started on port(s): 8080

(http)

2015-06-19 03:44:54.654 INFO 3886 --- [ main]

c.p.tddjava.ch09.Application : Started Application in 6.916

seconds (JVM running for 8.558)

> Building 75% > :run

[ 251 ]

Feature Toggles – Deploying Partially Done Features to Production

Chapter 10

Once the application has started, we can perform a query using a regular browser. The URL

of the query is http://localhost:8080/fibonacci?number=7.

This gives us the following output:

As you can see, the error received corresponds to the error sent by the REST API when the feature is disabled. Otherwise, the return should be -1.

Implementing the Fibonacci service

Most of you might be familiar with Fibonacci's numbers. Here's a brief explanation anyway for those who don't know what they are.

Fibonacci's sequence is an integer sequence resulting from the recurrence f(n) = f(n-1) - f(n - 2). The sequence starts with being f(0) = 0 and f(1) = 1. All other numbers are generated applying the recurrence as many times as

needed until a value substitution can be performed using either 0 or 1

known values.

That is: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144,...

More info about Fibonacci's sequence can be found here:

http://www.wolframalpha.com/input/?i=fibonacci+sequence

As an extra functionality, we want to limit how long the value computation takes, so we impose a constraint on the input; our service will only compute Fibonacci's numbers from 0

to 30 (both numbers included).

[ 252 ]

Feature Toggles – Deploying Partially Done Features to Production Chapter 10

This is a possible implementation of a class computing Fibonacci's numbers:

@Service("fibonacci")

public class FibonacciService {

public static final int LIMIT = 30;

public int getNthNumber(int n) {

if (isOutOfLimits(n) {

throw new IllegalArgumentException(

"Requested number must be a positive " +

number no bigger than " + LIMIT);

if (n == 0) return 0;

if (n == 1 || n == 2) return 1;

int first, second = 1, result = 1;

do {

first = second;

second = result;

result = first + second;

--n;

} while (n > 2);

return result;

}

private boolean isOutOfLimits(int number) {

return number > LIMIT || number < 0;

}

}

For the sake of brevity, the TDD Red-Green-Refactor process is not explicitly explained in the demonstration, but has been present through development. Only the final implementation with the final tests is presented:

public class FibonacciServiceTest {

private FibonacciService tested;

private final String expectedExceptionMessage =

"Requested number " +

"must be a positive number no bigger than " +

FibonacciService.LIMIT;

@Rule

public ExpectedException exception = ExpectedException.none();

@Before

public void beforeTest() {

tested = new FibonacciService();

}

[ 253 ]

Feature Toggles – Deploying Partially Done Features to Production Chapter 10

@Test

public void test0() {

int actual = tested.getNthNumber(0);

assertEquals(0, actual);

}

@Test

public void test1() {

int actual = tested.getNthNumber(1);

assertEquals(1, actual);

}

@Test

public void test7() {

int actual = tested.getNthNumber(7);

assertEquals(13, actual);

}

@Test

public void testNegative() {

exception.expect(IllegalArgumentException.class);

exception.expectMessage(is(expectedExceptionMessage));

tested.getNthNumber(-1);

}

@Test

public void testOutOfBounce() {

exception.expect(IllegalArgumentException.class);

exception.expectMessage(is(expectedExceptionMessage));

tested.getNthNumber(31);

}

}

Also, we can now turn on the fibonacci feature in the application.yml file, perform some queries with the browser, and check how is it going:

features:

fibonacci:

restEnabled: true

Execute Gradle's run command:

$>gradle run

[ 254 ]

Feature Toggles – Deploying Partially Done Features to Production

Chapter 10

Now we can fully test our REST API using the browser, with a number between 0 and 30: Then, we test it with a number bigger than 30, and lastly by introducing characters instead of numbers:

Working with the template engine

We are enabling and disabling the fibonacci feature, but there are many other cases where the Feature Toggle can be very useful. One of them is hiding a web link that links to an unfinished feature. This is an interesting use because we can test what we released to production using its URL, but it will be hidden for the rest of the users for as long as we want.

To illustrate this behavior, we are going to create a simple web page using the already mentioned Thymeleaf framework.

First of all, we add a new control flag:

features:

fibonacci:

restEnabled: true

webEnabled: true

[ 255 ]

Feature Toggles – Deploying Partially Done Features to Production Chapter 10

Next, map this new flag in a configuration class:

private boolean webEnabled;

public boolean isWebEnabled() {

return webEnabled;

}

public void setWebEnabled(boolean webEnabled) {

this.webEnabled = webEnabled;

}

We are going to create two templates. The first one is the home page. It contains some links to different Fibonacci number computations. These links should be visible only when the feature is enabled, so there's an optional block to simulate this behavior:

<!DOCTYPE html>

<html xmlns:th="http://www.thymeleaf.org">

<head lang="en">

<meta http-equiv="Content-Type"

content="text/html; charset=UTF-8" />

<title>HOME - Fibonacci</title>

</head>

<body>

<div th:if="${isWebEnabled}">

<p>List of links:</p>

<ul th:each="number : ${arrayOfInts}">

<li><a

th:href="@{/web/fibonacci(number=${number})}"

th:text="'Compute ' + ${number} + 'th fibonacci'">

</a></li>

</ul>

</div>

</body>

</html>

The second one just shows the value of the computed Fibonacci number and also a link to go back to the home page:

<!DOCTYPE html>

<html xmlns:th="http://www.thymeleaf.org">

<head lang="en">

<meta http-equiv="Content-Type"

content="text/html; charset=UTF-8" />

<title>Fibonacci Example</title>

</head>

<body>

<p th:text="${number} + 'th number: ' + ${value}"></p>

[ 256 ]

Feature Toggles – Deploying Partially Done Features to Production Chapter 10

<a th:href="@{/}">back</a>

</body>

</html>

In order to get both templates to work, they should be in a specific location. They are src/main/resources/templates/home.html and

src/main/resources/templates/fibonacci.html respectively.

Finally, the masterpiece, which is the controller that connects all this and makes it work:

@Controller

public class FibonacciWebController {

@Autowired

FibonacciFeatureConfig fibonacciFeatureConfig;

@Autowired

@Qualifier("fibonacci")

private FibonacciService fibonacciProvider;

@RequestMapping(value = "/", method = GET)

public String home(Model model) {

model.addAttribute(

"isWebEnabled",

fibonacciFeatureConfig.isWebEnabled()

);

if (fibonacciFeatureConfig.isWebEnabled()) {

model.addAttribute(

"arrayOfInts",

Arrays.asList(5, 7, 8, 16)

);

}

return "home";

}

@RequestMapping(value ="/web/fibonacci", method = GET)

public String fibonacci(

@RequestParam(value = "number") Integer number,

Model model) {

if (number != null) {

model.addAttribute("number", number);

model.addAttribute(

"value",

fibonacciProvider.getNthNumber(number));

}

return "fibonacci";

}

}

[ 257 ]

Feature Toggles – Deploying Partially Done Features to Production

Chapter 10

Note that this controller and the previous one seen in the REST API example share some similarities. This is because both are constructed with the same framework and use the same resources. However, there are slight differences between them; one is annotated as

@Controller instead of both being @RestController. This is because the web controller is serving template pages with custom information, while the REST API generates a JSON

object response.

Let's see this working, again using this Gradle command:

$> gradle clean run

This is the generated home page:

This is shown when visiting the Fibonacci number link:

[ 258 ]

Feature Toggles – Deploying Partially Done Features to Production

Chapter 10

But we turn off the feature using the following code:

features:

fibonacci:

restEnabled: true

webEnabled: false

Relaunching the application, we browse to the home page and see that those links are not shown anymore, but we can still access the page if we already know the URL. If we manually write http://localhost:8080/web/fibonacci?number=15, we can still access the page:

This practice is very useful, but it usually adds unnecessary complexity to your code. Don't forget to refactor the code, deleting old toggles that you won't use anymore. It will keep your code clean and readable. Also, a good point is getting this working without restarting the application. There are many storage options that do not require a restart, databases being the most popular.

Summary

Feature Toggles are a nice way to hide and/or handle partially finished functionalities in production environments. This may sound weird for those deploying code to production on demand, but it is quite common to find this situation when practicing continuous integration, delivery, or deployment.

We have introduced the technique and discussed the pros and cons. We have also enumerated some of the typical cases where toggling features can be helpful. Finally, we have implemented two different use cases: a Feature Toggle with a very simple REST API, and a Feature Toggle in a web application.

[ 259 ]

Feature Toggles – Deploying Partially Done Features to Production Chapter 10

Although the code presented in this chapter is fully functional, it isn't very common to use a file-based property system for this matter. There are many libraries more suitable for production environments that can help us to implement this technique, providing a lot of capabilities, such as using a web interface to handle features, storing preferences in a database, or allowing access to concrete user profiles.

In the next chapter we are going to put the TDD concepts described in the book all together.

We are going to name some good practices and recommendations that are very useful when programming in the TDD way.

[ 260 ]

11

Putting It All Together

"If you always do what you always did, then you will always get what you always got."


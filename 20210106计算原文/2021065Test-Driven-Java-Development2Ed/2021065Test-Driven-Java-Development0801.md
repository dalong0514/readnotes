– Kent Beck

Everything we have done until now is related to techniques that can be applied only by developers, for developers. Customers, business representatives, and other parties that are not capable of reading and understanding code were not involved in the process.

TDD can be much more than what we have done up to now. We can define requirements, discuss them with the client, and get agreement as to what should be developed. We can use those same requirements and make them executable so that they drive and validate our development. We can use ubiquitous language to write acceptance criteria. All this, and more, is accomplished with a flavor of TDD called behavior-driven development (BDD).

We'll develop a book store application using a BDD approach. We'll define acceptance criteria in English, make the implementation of each feature separately, confirm that it is working correctly by running BDD scenarios and, if required, refactor the code to accomplish the desired level of quality. The process still follows the Red-Green-Refactor that is the essence of TDD. The major difference is the definition level. While, until this moment, we have been mostly working at the units level, this time we'll move a bit higher and apply TDD through functional and integration tests.

BDD – Working Together with the Whole Team

Chapter 8

Our frameworks of choice will be JBehave and Selenide.

The following topics will be covered in this chapter:

The different types of specifications

Behavior-driven development (BDD)

The book store BDD story

JBehave

Different specifications

We have already mentioned that one of the benefits of TDD is executable documentation that is always up to date. However, documentation obtained through unit tests is often not enough. When working at such a low-level, we get insights into details; however, it is all too easy to miss the big picture. If, for example, you were to inspect specifications that we created for the Tic-Tac-Toe game, you might easily miss the point of the application. You would understand what each unit does and how it interoperates with other units, but would have a hard time grasping the idea behind it. To be precise, you would understand that unit X does Y and communicates with Z; however, the functional documentation and the idea behind it would be, at best, hard to find.

The same can be said for development. Before we start working on specifications in the form of unit tests, we need to get a bigger picture. Throughout this book, you were presented with requirements that we used for writing specifications that resulted in their implementation. Those requirements were later on discarded; they are nowhere to be seen.

We did not put them in to the repository, nor did we use them to validate the result of our work.

[ 186 ]

BDD – Working Together with the Whole Team

Chapter 8

Documentation

In many of the organizations that we worked with, the documentation was created for the wrong reasons. The management tends to think that documentation is somehow related to project success—that without a lot of (often short-lived) documentation, the project will fail.

Thus, we are asked to spend a lot of time planning, answering questions, and filling in questionnaires that are often designed not to help the project but to provide an illusion that everything is under control. Someone's existence is often justified with documentation (the result of my work is this document). It also serves as a reassurance that everything is going as planned (there is an Excel sheet that states that we are on schedule). However, by far the most common reason for the creation of documentation is a process that simply states that certain documents need to be created. We might question the value of those documents, however, since the process is sacred, they need to be produced.

Not only might that documentation be created for the wrong reasons and not provide enough value, but, as is often the case, it might also do a lot of damage. If we created the documentation, it is natural that we trust it. However, what happens if that documentation is not up to date? The requirements are changing, bugs are getting fixed, new functionalities are being developed, and some are being removed. If given enough time, all traditional documentation becomes obsolete. The sheer task of updating documentation with every change we make to the code is so big and complex that, sooner or later, we must face the fact that static documents do not reflect the reality. If we are putting our trust into something that is not accurate, our development is based on wrong assumptions.

The only accurate documentation is our code. The code is what we develop, what we deploy, and is the only source that truthfully represents our application. However, code is not readable by everyone involved with the project. Besides coders, we might work with managers, testers, business people, end users, and so on.

In search of a better way to define what would constitute better documentation, let us explore a bit further into who the potential documentation consumers are. For the sake of simplicity, we'll divide them into coders (those capable of reading and understanding code) and non-coders (everyone else).

[ 187 ]

BDD – Working Together with the Whole Team

Chapter 8

Documentation for coders

Developers work with code and, since we have established that code is the most accurate documentation, there is no reason to not utilize it. If you want to understand what some method does, take a look at the code of that method. In doubt about what some class does?

Take a look at that class. Having trouble understanding a piece of code? We have a problem! However, the problem is not that the documentation is missing, but that the code itself is not written well.

Looking at the code to understand the code is still often not enough. Even though you might understand what the code does, the purpose of that code might not be so obvious.

Why was it written in the first place?

That's where specifications come in. Not only are we using them to continuously validate the code, but they also act as executable documentation. They are always up to date because if they aren't, their execution will fail. At the same time, while code itself should be written in a way that is easy to read and understand, specifications provide a much easier and faster way to understand the reasons, logic, and motivations that lead us to write some piece of implementation code.

Using code as documentation does not exclude other types. Quite the contrary, the key is not to avoid using static documentation, but to avoid duplication. When code provides the necessary details, use it before anything else. In most cases, this leaves us with higher-level documentation, such as an overview, the general purpose of the system, the technologies used, the environment set-up, the installation, building, and packaging, and other types of data that tend to serve more like guidelines and quick-start information than detailed information. For those cases, a simple README in markdown format

(http://whatismarkdown.com/) tends to be the best.

For all code-based documentation, TDD is the best enabler. Until now, we worked only with units (methods). We are yet to see how to apply TDD on a higher-level, such as, for example, functional specifications. However, before we get there, let's speak about other roles in the team.

[ 188 ]

BDD – Working Together with the Whole Team

Chapter 8

Documentation for non-coders

Traditional testers tend to form groups completely separated from developers. This separation leads to an increased number of testers who are not familiar with code and assume that their job is to be quality checkers. They are validators at the end of the process and act as a kind of border police who decide what can be deployed and what should be returned back. There is, on the other hand, an increasing number of organizations that are employing testers as integral members of the team, with the job of ensuring that quality is built in. This latter group requires testers to be proficient with code. For them, using code as documentation is quite natural. However, what should we do with the first group? What should we do with testers who do not understand the code? Also, it is not only (some) testers that fall into this group. Managers, end-users, business representatives, and so on are also included. The world is full of people that cannot read and understand code.

We should look for a way to retain the advantages that the executable documentation provides, but write it in a way that can be understood by everyone. Moreover, in TDD

fashion, we should allow everyone to participate in the creation of executable documentation from the very start. We should allow them to define requirements that we'll use to develop applications and, at the same time, to validate the result of that development. We need something that will define what we'll do on a higher-level, since low-level is already covered with unit tests. To summarize, we need documentation that can serve as requirements, that can be executed, that can validate our work, and that can be written and understood by everyone.

Say hello to BDD.

Behavior-driven development

Behavior-driven development (BDD) is an agile process designed to keep the focus on stakeholder value throughout the whole project; it is a form of TDD. Specifications are defined in advance, the implementation is done according to those specifications, and they are run periodically to validate the outcome. Besides those similarities, there are a few differences as well. Unlike TDD, which is based on unit tests, BDD encourages us to write multiple specifications (called scenarios) before starting the implementation (coding). Even though there is no specific rule, BDD tends to levitate towards higher-level functional requirements. While it can be employed at a unit level as well, the real benefits are obtained when taking a higher approach that can be written and understood by everyone. The audience is another difference—BDD tries to empower everyone (coders, testers, managers, end users, business representatives, and so on).

[ 189 ]

BDD – Working Together with the Whole Team

Chapter 8

While TDD, which is based on unit level, can be described as inside-out (we begin with units and build up towards functionalities), BDD is often understood as outside-in (we start with features and go inside towards units). BDD acts as an acceptance criteria that acts as an indicator of readiness. It tells us when something is finished and ready for production.

We start by defining functionalities (or behaviors), work on them by employing TDD with unit tests, and, once a complete behavior has finished, validate with BDD. One BDD

scenario can take hours or even days to finish. During all that time, we can employ TDD

and unit testing. Once we're done, we run BDD scenarios to do the final validation. TDD is for coders and has a very fast cycle, while BDD is for everyone and has a much slower turnout time. For each BDD scenario, we have many TDD unit tests.

At this point, you might have gotten confused about what BDD really is, so let us go back a bit. We'll start with the explanation of its format.

Narrative

A BDD story consists of one narrative followed by at least one scenario. A narrative is only informative, and its main purpose is to provide just enough information that can serve as a beginning of communication between everyone involved (testers, business representatives, developers, analysts, and so on). It is a short and simple description of a feature, told from the perspective of a person who requires it.

The goal of a narrative is to answer three basic questions:

1. In order to: What is the benefit or value of the feature that should be built?

2. As a: Who needs the feature that was requested?

3. I want to: What is the feature or goal that should be developed?

Once we have those questions answered, we can start defining what we think would be the best solution. This thinking process results in scenarios that provide a lower-level of detail.

Until now, we were working at a very low-level using unit tests as a driving force. We were specifying what should be built from the coder's perspective. We assumed that high-level requirements were defined earlier and that our job was to do the code specific to one of them. Now, let us take a few steps back and start from the beginning.

[ 190 ]

BDD – Working Together with the Whole Team

Chapter 8

Let us act, let's say, as a customer or a business representative. Someone got this great idea and we are discussing it with the rest of the team. In short, we want to build an online book store. It is only an idea and we're not even certain of how it will develop, so we want to work on a Minimum Viable Product (MVP). One of the roles that we want to explore is the one of a store administrator. This person should be able to add new books and update or remove the existing ones. All those actions should be doable, because we want this person to be able to manage our book store collection in an efficient way. The narrative that we came up with for this role is the following:

In order to manage the book store collection efficiently

As a store administrator

I want to be able to add, update, and remove books

Now that we know what the benefit is (managing books), who needs it (administrator), and finally what the feature that should be developed is (insert, update, and delete operations). Keep in mind that this was not a detailed description of what should be done.

The narrative's purpose is to initiate a discussion that will result in one or more scenarios.

Unlike TDD unit tests, narratives, and indeed the rest of the BDD story, can be written by anyone. They do not require coding skills, nor do they have to go into too many details.

Depending on the organization, all narratives can be written by the same person (a business representative, product owner, customer, and so on) or it might be a collaborative effort by the whole team.

Now that we have a clearer idea regarding narratives, let us take a look at scenarios.

Scenarios

A narrative acts as a communication enabler, and scenarios are the result of that communication. They should describe interactions that the role (specified in the Narrative section) has with the system. Unlike unit tests, which were written as code by developers for developers, BDD scenarios should be defined in plain language and with minimum technical details so that all those involved with the project (developers, testers, designers, managers, customers, and so on) can have a common understanding about behaviors (or features) that will be added to the system.

[ 191 ]

BDD – Working Together with the Whole Team

Chapter 8

Scenarios act as the acceptance criteria of the narrative. Once all scenarios related to the narrative are run successfully, the job can be considered done. Each scenario is very similar to a unit test, with the main difference being the scope (one method against a whole feature) and the time it takes to implement it (a few seconds or minutes against a few hours or even days). Similarly to unit tests, scenarios drive the development; they are defined first.

Each scenario consists of a description and one or more steps that start with the words Given, When, or Then. The description is short and only informative. It helps us to understand, at a glance, what the scenario does. Steps, on the other hand, are a sequence of the preconditions, events, and expected outcomes of the scenario. They help us define the behavior unambiguously and it's easy to translate them to automated tests.

Throughout this chapter, we'll focus more on the technical aspects of BDD and the ways they fit into the developer's mindset. For broader usage of BDD and much deeper discussion, consult the book, Specification by Example: How Successful Teams Deliver the Right Software by Gojko Adzic.

The Given step defines a context or preconditions that need to be fulfilled for the rest of the scenario to be successful. Going back to the book's administration narrative, one such precondition might be the following:

Given user is on the books screen

This is a very simple but pretty necessary precondition. Our website might have many pages, and we need to make sure that the user is on the correct screen before we perform any action.

The When step defines an action or some kind of an event. In our narrative, we defined that the administrator should be able to add, update, and remove books. Let's see what should be an action related to, for example, the delete operation:

When user selects a book

When user clicks the deleteBook button

[ 192 ]

BDD – Working Together with the Whole Team

Chapter 8

In this example, we multiplied actions defined with the When steps. First, we should select a book and then we should click on the deleteBook button. In this case, we used an ID

(deleteBook) instead of text (Delete the book) to define the button that should be clicked.

In most cases, IDs are preferable because they provide multiple benefits. They are unique (only one ID can exist on a given screen), they provide clear instructions for developers (create an element with an ID deleteBook), and they are not affected by other changes on the same screen. The text of an element can easily change; if this happens, all scenarios that used it would fail as well. In the case of websites, an alternative could be XPath. However, avoid this whenever possible. It tends to fail with the smallest change to the HTML

structure.

Similarly to unit tests, scenarios should be reliable and fail when a feature is not yet developed or when there is a real problem. Otherwise, it is a natural reaction to start ignoring specifications when they produce false negatives.

Finally, we should always end the scenario with some kind of verification. We should specify the desired outcome of actions that were performed. Following the same scenario, our Then step could be the following:

Then book is removed

This outcome strikes a balance between providing just enough data and not going into design details. We could have, for example, mentioned the database or, even more specifically, MongoDB. However, in many cases, that information is not important from the behavioral point of view. We should simply confirm that the book is removed from the catalog, no matter where it is stored.

Now that we are familiar with the BDD story format, let us write the book store BDD story.

The book store BDD story

Before we start, clone the code that is available at

https://bitbucket.org/vfarcic/tdd-java-ch08-books-store. It is an empty project that

we'll use throughout this chapter. As with previous chapters, it contains branches for each section, in case you miss something.

We'll write one BDD story that will be in a pure text format, in plain English and without any code. That way, all stakeholders can participate and get involved independently of their coding proficiency. Later on, we'll see how to automate the story we're writing.

[ 193 ]

BDD – Working Together with the Whole Team

Chapter 8

Let us start by creating a new file called administration.story inside the stories directory:

We already have the narrative that we wrote earlier, so we'll build on top of that: Narrative:

In order to manage the book store collection efficiently

As a store administrator

I want to be able to add, update, and remove books

We'll be using JBehave format for writing stories. More details regarding JBehave are

coming soon. Until then, visit http://jbehave.org/ for more info.

A narrative always starts with the Narrative line and is followed with the In order to, As a, and I want to lines. We already discussed the meaning of each of them.

[ 194 ]

BDD – Working Together with the Whole Team

Chapter 8

Now that we know the answers to why, who, and what, it is time to sit with the rest of the team and discuss possible scenarios. We're still not talking about steps (Given, When, and Then), but simply what would be the outlines or short descriptions of the potential scenarios. The list could be the following:

Scenario: Book details form should have all fields

Scenario: User should be able to create a new book

Scenario: User should be able to display book details

Scenario: User should be able to update book details

Scenario: User should be able to delete a book

We're following the JBehave syntax by using Scenario followed by a short description.

There is no reason to go into detail at this stage; the purpose of this stage is to serve as a quick brainstorming session. In this case, we came up with those five scenarios. The first one should define fields of the form that we'll use to administer books. The rest of the scenarios are trying to define different administrative tasks. There's nothing truly creative about them. We're supposed to develop an MVP of a very simple application. If it proves to be successful, we can expand and truly employ our creativity. With the current objective, the application will be simple and straightforward.

Now that we know what our scenarios are, in general terms, it is time to properly define each of them. Let us start working on the first one:

Scenario: Book details form should have all fields

Given user is on the books screen

Then field bookId exists

Then field bookTitle exists

Then field bookAuthor exists

Then field bookDescription exists

This scenario does not contain any actions; there are no When steps. It can be considered a sanity check. It tells developers what fields should be present in the book form. Through those fields, we can decide what data schema we'll use. IDs are descriptive enough that we know what each field is about (one ID and three text fields). Keep in mind that this scenario (and those that will follow) are pure texts without any code. The main advantage is that anyone can write them, and we'll try to keep it that way.

[ 195 ]

BDD – Working Together with the Whole Team

Chapter 8

Let's see what the second scenario should look like:

Scenario: User should be able to create a new book

Given user is on the books screen

When user clicks the button newBook

When user sets values to the book form

When user clicks the button saveBook

Then book is stored

This scenario is a bit better formed than the previous one. There is a clear prerequisite (user should be on a certain screen); there are several actions (click on the newBook button, fill in the form, and click on the saveBook button); finally, there is the verification of the outcome (book is stored).

The rest of the scenarios are as follows (since they all work in a similar way, we feel that there is no reason to explain each of them separately):

Scenario: User should be able to display book details

Given user is on the books screen

When user selects a book

Then book form contains all data

Scenario: User should be able to update book details

Given user is on the books screen

When user selects a book

When user sets values to the book form

Then book is stored

Scenario: User should be able to delete a book

Given user is on the books screen

When user selects a book

When user clicks the deleteBook button

Then book is removed

The only thing that might be worth noticing is that we are using the same steps when appropriate (for example, When user selects a book). Since we'll soon try to automate all those scenarios, having the same text for the same step will save us some time by duplicating the code. It is important to strike a balance between the freedom to express scenarios in the best possible way and the ease of automation. There are a few more things that we can modify in our existing scenarios, however, before we refactor them, let us introduce you to JBehave.

[ 196 ]

BDD – Working Together with the Whole Team

Chapter 8

The source code can be found in the 00-story branch of the tdd-java-ch08-books-store Git repository,

at https://bitbucket.org/vfarcic/tdd-java-ch08-books-store/branch/00-story.

JBehave

There are two major components required for JBehave to run BDD stories—runners and steps. A runner is a class that will parse the story, run all scenarios, and generate a report.

Steps are code methods that match steps written in scenarios. The project already contains all Gradle dependencies, so we can dive right into creating the JBehave runner.

JBehave runner

JBehave is no exception to the rule that every type of test needs a runner. In the previous chapters, we used JUnit and TestNG runners. While neither of those needed any special configuration, JBehave is a bit more demanding and forces us to create a class that will hold all the configuration required for running stories.

The following is the Runner code that we'll use throughout this chapter: public class Runner extends JUnitStories {

@Override

public Configuration configuration() {

return new MostUsefulConfiguration()

.useStoryReporterBuilder(getReporter())

.useStoryLoader(new LoadFromURL());

}

@Override

protected List<String> storyPaths() {

String path = "stories/**/*.story";

return new StoryFinder().findPaths(

CodeLocations.codeLocationFromPath("").getFile(),

Collections.singletonList(path),

new ArrayList<String>(),

"file:");

}

@Override

public InjectableStepsFactory stepsFactory() {

return new InstanceStepsFactory(configuration(), new Steps());

[ 197 ]

BDD – Working Together with the Whole Team

Chapter 8

}

private StoryReporterBuilder getReporter() {

return new StoryReporterBuilder()

.withPathResolver(new

FilePrintStreamFactory.ResolveToSimpleName())

.withDefaultFormats()

.withFormats(Format.CONSOLE, Format.HTML);

}

}

It is very uneventful code, so we'll comment only on a few important parts. The overridden method storyPaths has the location to our story files set to the stories/**/*.story path. This is a standard Apache Ant (http://ant.apache.org/) syntax that, when

translated to plain language, means that any file ending with .story inside the stories directory or any subdirectory (**) will be included. Another important overridden method is stepsFactory, which is used to set classes containing the steps definition (we'll work with them very soon). In this case, we set it to the instance of a single class called Steps (the repository already contains an empty class that we'll use later on).

The source code can be found in the 01-runner branch of the tdd-java-ch08-books-store Git repository,

at https://bitbucket.org/vfarcic/tdd-java-ch08-books-store/branch/01-runner.

Now that we have our runner done, it is time to fire it up and see what the result is.

Pending steps

We can run our scenarios with the following Gradle command:

$ gradle clean test

Gradle only runs tasks that changed from the last execution. Since our source code will not always change (we often modify only stories in text format), the clean task is required to be run before the test so that the cache is removed.

JBehave creates a nice report for us and puts it into the target/jbehave/view directory.

Open the reports.html file in your favorite browser.

[ 198 ]

BDD – Working Together with the Whole Team

Chapter 8

The initial page of the report displays a list of our stories (in our case, only Administration) and two predefined ones called BeforeStories and AfterStories. Their purpose is similar to the @BeforeClass and @AfterClass JUnit annotated methods. They are run before and after stories, and can be useful for setting up and tearing down data, servers, and so on.

This initial reports page shows that we have five scenarios and all of them are in the Pending status. This is JBehave's way of telling us that they were neither successful nor failed, but that there is code missing behind the steps we used:

The last column in each row contains a link that allows us to see details of each story:

[ 199 ]

BDD – Working Together with the Whole Team

Chapter 8

In our case, all the steps are marked as pending. JBehave even puts a suggestion of a method that we need to create for each pending step.

To recapitulate, at this point, we wrote one story with five scenarios. Each of those scenarios is equivalent to a specification that will be used both as a definition that should be developed and to verify that the development was done correctly. Each of those scenarios consists of several steps that define preconditions (Given), actions (When), and the expected outcome (Then).

Now it is time, to write the code behind our steps. However, before we start coding, let us get introduced to Selenium and Selenide.

Selenium and Selenide

Selenium is a set of drivers that can be used to automate browsers. We can use them to manipulate browsers and page elements by, for example, clicking on a button or a link, filling up a form field, opening a specific URL, and so on. There are drivers for almost any browser—Android, Chrome, FireFox, Internet Explorer, Safari, and many more. Our favorite is PhantomJS, which is a headless browser that works without any UI. Running stories with it is faster than with traditional browsers, and we often use it to get fast feedback on the readiness of web applications. If it works as expected, we can proceed and try it out in all the different browsers and versions that our application is supposed to support.

More information about Selenium can be found at http://www.seleniumhq.org/, with the

list of supported drivers at http://www.seleniumhq.org/projects/webdriver/.

While Selenium is great for automating browsers, it has its downsides, one of them being that it is operating at a very low-level. Clicking on a button, for example, is easy and can be accomplished with a single line of code:

selenium.click("myLink")

If the element with the ID myLink does not exist, Selenium will throw an exception and the test will fail. While we want our tests to fail when the expected element does not exist, in many cases it is not so simple. For example, our page might load dynamically with that element appearing only after an asynchronous request to the server got a response. For this reason, we might not only want to click on that element, but also wait until it is available, and fail only if a timeout is reached. While this can be done with Selenium, it is tedious and error prone. Besides, why would we do the work that is already done by others? Say hello to Selenide.

[ 200 ]

BDD – Working Together with the Whole Team

Chapter 8

Selenide (http://selenide.org/) is a wrapper around Selenium WebDrivers with a more concise API, support for Ajax, selectors that use JQuery style, and so on. We'll use Selenide for all our Web steps, and you'll get more familiar with it soon.

Now, let us write some code.

JBehave steps

Before we start writing steps, install the PhantomJS browser. The instructions for your

operating system can be found at http://phantomjs.org/download.html.

With PhantomJS installed, it is time to specify a few Gradle dependencies: dependencies {

testCompile 'junit:junit:4.+'

testCompile 'org.jbehave:jbehave-core:3.+'

testCompile 'com.codeborne:selenide:2.+'

testCompile 'com.codeborne:phantomjsdriver:1.+'

}

You are already familiar with JUnit and JBehave Core, which was set up earlier. Two new additions are Selenide and PhantomJS. Refresh Gradle dependencies so that they are included in your IDEA project.

Now, it is time to add the PhantomJS WebDriver to our Steps class:

public class Steps {

private WebDriver webDriver;

@BeforeStory

public void beforeStory() {

if (webDriver == null) {

webDriver = new PhantomJSDriver();

webDriverRunner.setWebDriver(webDriver);

webDriver.manage().window().setSize(new Dimension(1024,

768));

}

}

}

[ 201 ]

BDD – Working Together with the Whole Team

Chapter 8

We're utilizing the @BeforeStory annotation to define the method that we're using to do some basic setup. If a driver is not already specified, we're setting it up to be PhantomJSDriver. Since this application will look different on smaller devices (phones, tablets, and so on), it is important that we specify clearly what the size of the screen is. In this case, we're setting it to be a reasonable desktop/laptop monitor screen resolution of 1024 x 768.

With setup out of the way, let us code our first pending step. We can simply copy and paste the first method JBehave suggested for us in the report:

@Given("user is on the books screen")

public void givenUserIsOnTheBooksScreen() {

// PENDING

}

Imagine that our application will have a link that will open the book's screen.

To do that, we'll need to perform two steps:

1. Open the website home page.

2. Click on the books link in the menu.

We'll specify that this link will have the ID books. IDs are very important as they allow us to easily locate an element on the page.

The steps we described earlier can be translated to the following code: private String url = "http://localhost:9001";

@Given("user is on the books screen")

public void givenUserIsOnTheBooksScreen() {

open(url);

$("#books").click();

}

We're assuming that our application will run on the 9001 port on the localhost.

Therefore, we are first opening the home page URL and then clicking on the element with the ID books. Selenide/JQuery syntax for specifying an ID is #.

If we run our runner again, we'd see that the first step failed and the rest is still in the Pending state. Now, we are in the red state of the Red-Green-Refactor cycle.

[ 202 ]

BDD – Working Together with the Whole Team

Chapter 8

Let us continue working on the rest of the steps used in the first scenario. The second one can be the following:

@Then("field bookId exists")

public void thenFieldBookIdExists() {

$("#books").shouldBe(visible);

}

The third one is almost the same, so we can refactor the previous method and convert an element ID into a variable:

@Then("field $elementId exists")

public void thenFieldExists(String elementId) {

$("#" + elementId).shouldBe(visible);

}

With this change, all the steps in the first scenario are done. If we run our tests again, the result is the following:

The first step failed since we did not even start working on the implementation of our book store application. Selenide has a nice feature that creates a screenshot of the browser every time there is a failure. We can see the path in the report. The rest of the steps are in the not performed state since the execution of the scenario stopped on failure.

[ 203 ]

BDD – Working Together with the Whole Team

Chapter 8

What should be done next depends on the structure of the team. If the same person is working both on functional tests and the implementation, he could start working on the implementation and write just enough code to make this scenario pass. In many other situations, separate people are working on the functional specification and the implementation code. In that case, one could continue working on the missing steps for the rest of the scenarios, while the other would start working on the implementation. Since all scenarios are already written in text form, a coder already knows what should be done and the two can work in parallel. We'll take the former route and write the code for the rest of the pending steps.

Let's go through the next scenario:

We already have half of the steps done from the previous scenario, so there are only two pending. After we click on the newBook button, we should set some values to the form, click on the saveBook button, and verify that the book was stored correctly. We can do the last part by checking whether it appeared in the list of available books.

The missing steps can be the following:

@When("user sets values to the book form")

public void whenUserSetsValuesToTheBookForm() {

$("#bookId").setValue("123");

$("#bookTitle").setValue("BDD Assistant");

$("#bookAuthor").setValue("Viktor Farcic");

$("#bookDescription")

.setValue("Open source BDD stories editor and runner");

}

@Then("book is stored")

public void thenBookIsStored() {

$("#book123").shouldBe(present);

}

[ 204 ]

BDD – Working Together with the Whole Team

Chapter 8

The second step assumes that each of the available books will have an ID in the format book[ID].

Let us take a look at the next scenario:

Like in the previous scenario, there are two steps pending development. We need to have a way to select a book and to verify that data in the form is correctly populated:

@When("user selects a book")

public void whenUserSelectsABook() {

$("#book1").click();

}

@Then("book form contains all data")

public void thenBookFormContainsAllData() {

$("#bookId").shouldHave(value("1"));

$("#bookTitle").shouldHave(value("TDD for Java Developers")); $("#bookAuthor").shouldHave(value("Viktor Farcic")); $("#bookDescription").shouldHave(value("Cool book!"));

}

[ 205 ]

BDD – Working Together with the Whole Team

Chapter 8

These two methods are interesting because they not only specify the expected behavior (when a specific book link is clicked, then a form with its data is displayed), but also expect certain data to be available for testing. When this scenario is run, a book with the ID 1, title TDD for Java Developers, author Viktor Farcic, and description Cool book!

should already exist. We can choose to add that data to the database or use a mock server that will serve the predefined values. No matter what the choice of how to set test data is, we can finish with this scenario and jump into the next one:

The implementation of the pending steps could be the following:

@When("user sets new values to the book form")

public void whenUserSetsNewValuesToTheBookForm() {

$("#bookTitle").setValue("TDD for Java Developers revised"); $("#bookAuthor").setValue("Viktor Farcic and Alex Garcia"); $("#bookDescription").setValue("Even better book!"); $("#saveBook").click();

}

@Then("book is updated")

public void thenBookIsUpdated() {

$("#book1").shouldHave(text("TDD for Java Developers revised")); $("#book1").click();

$("#bookTitle").shouldHave(value("TDD for Java Developers revised"));

$("#bookAuthor").shouldHave(value("Viktor Farcic and Alex Garcia"));

$("#bookDescription").shouldHave(value("Even better book!"));

}

[ 206 ]

BDD – Working Together with the Whole Team

Chapter 8

Finally, there is only one scenario left:

We can verify that a book is removed by verifying that it is not in the list of available books:

@Then("book is removed")

public void thenBookIsRemoved() {

$("#book1").shouldNotBe(visible);

}

We're finished with the steps code. Now, the person who is developing the application not only has requirements but also has a way to validate each behavior (scenario). He can move through the Red-Green-Refactor cycle one scenario at a time.

The source code can be found in the 02-steps branch of the tdd-java-ch08-books-store Git repository:

https://bitbucket.org/vfarcic/tdd-java-ch08-books-store/branch/02-steps.

Final validation

Let us imagine that a different person worked on the code that should fulfill the requirements set by our scenarios. This person picked one scenario at the time, developed the code, ran that scenario, and confirmed that his implementation was correct. Once the implementation of all scenarios has been done, it is time to run the whole story and do the final validation.

For that matter, the application has been packed as a Docker file and we have prepared a virtual machine with Vagrant for executing the application.

[ 207 ]

BDD – Working Together with the Whole Team

Chapter 8

Check out the branch at

https://bitbucket.org/vfarcic/tdd-java-ch08-books-store/branch/03-validation

and run Vagrant:

$ vagrant up

The output should be similar to the following:

==> default: Importing base box 'ubuntu/trusty64'...

==> default: Matching MAC address for NAT networking...

==> default: Checking if box 'ubuntu/trusty64' is up to date...

...

==> default: Running provisioner: docker...

default: Installing Docker (latest) onto machine...

default: Configuring Docker to autostart containers...

==> default: Starting Docker containers...

==> default: -- Container: books-fe

Once Vagrant is finished, we can see the application by opening http://localhost:9001

in our browser of choice:

Now, let us run our scenarios again:

$ gradle clean test

[ 208 ]

BDD – Working Together with the Whole Team

Chapter 8

This time there were no failures and all scenarios ran successfully:

Once all scenarios are passing, we meet the acceptance criteria and the application can be delivered to production.

Summary

BDD, in its essence, is a flavor of TDD. It follows the same basic principle of writing tests (scenarios) before the implementation code. It drives the development and helps to us better understand what should be done.

One of the major differences is the life cycle duration. While with TDD, which is based on unit tests, we're moving from red to green very fast (in minutes if not seconds) BDD often takes a higher-level approach that might require hours or days until we get from the red to the green state. Another important difference is the audience. While unit tests-based TDD is done by developers for developers, BDD intends to involve everyone through its ubiquitous language.

While a whole book can be written on this subject, our intention was to give you just enough information so that you can investigate BDD further.

Now it is time to take a look at legacy code and how to adapt it and make it more TDD

friendly.

[ 209 ]

9

Refactoring Legacy Code –


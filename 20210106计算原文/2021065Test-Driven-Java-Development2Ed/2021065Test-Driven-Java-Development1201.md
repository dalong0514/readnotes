– John C. Maxwell

Throughout this book, concepts and good practices have been presented with isolated examples. The goal of this chapter is to put into practice some of these concepts by applying them to a more realistic scenario.

To accomplish that, we are introducing a fictitious company called Awesome Gambling Corp. This company is struggling with a few problems in its software development life cycle that could be easily solved by applying some of the things we have learned in this book. As a disclaimer, any similarity with a real company is pure coincidence. Furthermore, for the sake of brevity, the codebase is not very extensive and some of the problems have been exaggerated in order to better represent the issue that needs to be addressed.

The topics covered not necessarily in order, are:

Continuous integration

Continuous delivery

Benefits of test-driven development

Identifying quick wins

Leverage TDD by Implementing Continuous Delivery

Chapter 12

Case study – Awesome Gambling Corp

You are Alice, a software developer, and you just joined the software development team of Awesome Gambling Corp. Your teammates are trying to bring you up to speed in the shortest time possible. It's your first day and your teammate, John, who has been designated as your mentor, is going to be guiding you during the first few hours in the company.

After a pleasant cup of coffee, he rapidly sets the topic of your conversation to all the tasks and procedures that will comprise your day-to-day work. Your team is developing and maintaining a very simple thimblerig-service. As soon as you hear the word thimblerig, you ashamedly admit this is the first time you have heard that word. John laughs and says he didn't know it either when he joined the company two years ago.

The Thimblerig game, also known as three shells and a pea, is an ancient gambling game.

The rules are pretty simple, there are three shells, and the pea is covered by one of the three.

The three shells are shuffled at really high speed and, when finished, the player has to guess which shell hides the pea.

After the explanation, he kindly offers to help you downloading the code project from the repository and briefly explains to you the overall concepts.

Once he is done with the explanation, he asks you to read the code on your own. He also tells you he is the person for you to go to in case you have any questions or concerns. You express your gratitude for his time and start browsing the project.

Exploring the codebase

As you start browsing the project, you realise that the application is not very complex. In fact, the project contains roughly a dozen Java classes and, as you start opening and looking at the files, you notice that none of them is longer than one hundred lines. That is pretty good, the codebase is small so you will be able to develop new features in no time.

Provided that this is a Gradle project, you quickly open the build.gradle file to acknowledge the frameworks and libraries being used within the project: apply plugin: 'java'

apply plugin: 'org.springframework.boot'

sourceCompatibility = 1.8

targetCompatibility = 1.8

[ 275 ]

Leverage TDD by Implementing Continuous Delivery

Chapter 12

bootRepackage.executable = true

repositories {

mavenLocal()

mavenCentral()

}

dependencies {

compile 'org.springframework.boot:spring-boot-starter-actuator'

compile 'org.springframework.boot:spring-boot-starter-web'

testCompile 'junit:junit:4.12'

testCompile 'org.hamcrest:hamcrest-all:1.3'

testCompile 'org.mockito:mockito-core:1.10.19'

}

The Gradle build field looks good. The project you are going to work on is a Spring-based web service. It uses spring-boot-starter-web, so it's very likely you will be able to run it locally without hassle. Moreover, there are some test dependencies which means there should be some tests in the test folder as well.

A couple of minutes later you already have a mental map of the application. There is a class called ThimblerigService which handles the logic of the game. It has a dependency on a RandomNumberGenerator and it only has one public method, which is placeBet.

Methods and classes have an understandable name, so it isn't hard to figure out what they do:

@Service

public class ThimblerigService {

private RandomNumberGenerator randomNumberGenerator;

@Autowired

ThimblerigService(RandomNumberGenerator randomNumberGenerator) {

this.randomNumberGenerator = randomNumberGenerator;

}

public BetResult placeBet(int position, BigDecimal betAmount) {

...

}

}

[ 276 ]

Leverage TDD by Implementing Continuous Delivery

Chapter 12

Besides that class, there is only one controller class that implements an API: it is ThimblerigAPI. It exposes only one method, which is placeBet. Other company services invoke that POST method in order to play one game in this service. The service resolves the bet and includes in the response details such as whether there's a prize won, the amount, and so forth:

@RestController

@RequestMapping("/v1/thimblerig")

public class ThimblerigAPI {

private ThimblerigService thimblerigService;

@Autowired

public ThimblerigAPI(ThimblerigService thimblerigService) {

this.thimblerigService = thimblerigService;

}

@ResponseBody

@PostMapping(value = "/placeBet",

consumes = MediaType.APPLICATION_JSON_VALUE)

public BetReport placeBet(@RequestBody NewBet bet) {

BetResult betResult =

thimblerigService.placeBet(bet.getPick(), bet.getAmount());

return new BetReport(betResult);

}

}

This is a fairly easy setup and everything is crystal-clear, so you decide to move on and start looking at the tests.

As you open the test folder and start looking for tests, you are very surprised when you discover there is only one test class: ThimblerigServiceTest. One single good test is worth more than hundred bad ones but still, you think this application is poorly unit-tested: public class ThimblerigServiceTest {

@Test

public void placingBetDoesNotAcceptPositionsLessThanOne() {

...

}

@Test

public void placingBetDoesNotAcceptPositionsGreaterThan3() {

...

}

@Test

public void placingBetOnlyAcceptsAmountsGreaterThanZero() {

[ 277 ]

Leverage TDD by Implementing Continuous Delivery

Chapter 12

...

}

@Test

public void onFailedBetThePrizeIsZero() {

...

}

@Test

public void

whenThePositionIsGuessedCorrectlyThePrizeIsDoubleTheBet() {

...

}

}

After opening the class and going over all the tests it contains, your impression changes slightly for the good. The tests cover the core service completely and they seem meaningful and exhaustive. But despite that, you can't avoid turning your head to John and asking him why there's only one test. He tells you they didn't have much time to create tests because they were in a hurry, so only the critical parts have tests. Whether a piece of code is critical or not is very subjective, but you understand the situation; in fact, you have been in that situations many times.

Only one second later, before you have time to go back to your task, John adds another interesting point to his answer: the quality assurance (QA) department. The aim of this department is to test all release candidates before they reach a production environment.

Their mission is to find errors and bugs that might affect the application and report them. In some cases, if any of the errors found are very critical, the release is stopped and it will never be deployed to production. This procedure usually takes from three to five days. You think that could be a bottleneck in some scenarios, so you ask him to give you further details of the release process.

Release procedure

Provided that the project is a simple REpresentational State Transfer (REST) service, the creation of a release is not complex at all. According to the current procedure, a developer compiles the code and sends the artifact to the team that manages all deployments. That team coordinates the testing and deployment to production with the customer and QA departments.

[ 278 ]

Leverage TDD by Implementing Continuous Delivery

Chapter 12

You decide to ask John if he is happy with the process. Before you even get the answer, you know John is not happy at all with it. You can see on his face that he is making an effort to hide his feelings about it. John gulps back his emotions and starts describing the current situation of the team.

It turns out that not everything is joy and candy in the development team. All developers, when they start coding, create their own branch from the master branch in the repository. This is not bad at all, but it has happened that some branches have been merged back to the master many weeks later. The issue is that the master branch has changed a lot since then and the code base diverges a lot, meaning the merge is very difficult, unpleasant, and error prone.

Besides the occasional merging problems, it has happened that one developer compiled his local branch by mistake and it was deployed to production, generating chaos, carnage, and uncertainty for a short period.

On top of that, the customer is not very happy with the time new features take to be implemented. They are complaining about this from time to time, saying that every single tiny change takes at least a week to be applied.

You are puzzled how this can happen to a very tiny REST service, but of course John was referring to other bigger projects in the company. You know this kind of problem can be solved, or at least mitigated, by implementing continuous integration (CI) and continuous delivery. In fact, automating processes as much as possible enables you to focus on other problems by getting rid of those that are trivial.

After this small reflection, you now know you need more information about the deployment procedure and you also know that John is willing to give you the details.

Deployments to production

With the release process covered, John starts explaining to you how the service is deployed to production. It is very manual work: one member of the infrastructure team (IT) department copies the artifact to the server and executes a few commands to get it running.

John also takes the opportunity to add some stories of errors that they suffered in the past, like the time when, instead of deploying the latest version, the infrastructure operator mistakenly redeployed an old version. A bunch of old bugs reappeared and stayed in production until somebody found out what had happened.

[ 279 ]

Leverage TDD by Implementing Continuous Delivery

Chapter 12

While listening to those stories, you can't help but start thinking about what you have learned from previous projects and companies. You know that putting code into a production environment could be a very easy and straightforward task, a never-ending nightmare, or something in the middle. It depends on many factors and sometimes it is not up to us to change it. In some scenarios, deploying an application to production needs to be acknowledged by people who have the power to decide when and what is deployed. In others, there is strict regulation that turns what should be an easy procedure into a tedious and verbose task.

Furthermore, automating deployments is a way to reduce the risk factor that human interaction can add. Creating a repeatable process can be as easy as writing all the necessary steps in a script and scheduling its execution. It is well known that any single script can't replace a human completely, but, needless to say, the goal is not to replace humans with scripts. The main purpose of this is to provide a tool that can be executed autonomously and humans can supervise it, with manual intervention just in case it is necessary. For this, implementing continuous delivery is very suitable.

After John's brief but intense introduction, you feel that you are ready to start working on your own. You have many possible improvements in your head and you are definitely eager to implement them.

Conclusions

Even though the situation in this company has been exaggerated for didactic purposes, there are still companies struggling with these problems. Indeed, Alice knew that the way software developers at Awesome Gambling Corp work is not ideal. There are many techniques, some of them covered in this book, that could help the company stop focusing on unconscious mistakes and start focusing on other things that can add more value to their final product.

In the next section, we are going to address some of the problems described by proposing one possible solution. This is not a unique solution; actually, the solution proposed includes some tools, and there are many options for each of the tools used. Moreover, every company has its own culture and restrictions, and because of that, the proposed solution might not be fully suitable.

[ 280 ]

Leverage TDD by Implementing Continuous Delivery

Chapter 12

Possible improvements

In this section and the following subsections, we are going to tackle some of the problems described in Alice's story. Because the code we inherited from the example is already implemented, we can't apply TDD here. Instead, we are going to set the basis and prepare the ground for future developments where applying TDD will become very useful.

Although there are always many things that can be improved, the pain points being addressed are code merging issues, lots of manual testing, manual releases, and the length of time taken to develop changes or new features.

For the first two, we are going to increase the test coverage of the application and implement CI. A Jenkins server is going to be configured to address the third issue, manual releases. And finally, the last issue, which is the long time to market (TTM), is going to be mitigated by implementing the rest of the solutions.

Increasing test coverage

Among the metrics for measuring code quality, there is one that is especially difficult to understand, and that is test coverage. Test coverage is a dangerous metric because a really high coverage does not imply the code is well tested. As the name says, it only contemplates whether a piece of code has been triggered and hence executed by a test. For that reason, the goal of testing is basically a combination of good tests and good coverage. To summarize, it is the quality of tests that matters, the code coverage is secondary.

There are some scenarios though where code coverage is indeed a good indicator. These are when the code coverage is really low. In those, the number means a greater part of the codebase is not being tested and therefore tests are not ensuring we are not introducing errors.

Additionally, creating good automated tests can reduce the amount of time spent by the QA team on performing regression tests. This very likely reduces the time they spend testing the same code over and over again, increasing the team's delivery velocity.

[ 281 ]

Leverage TDD by Implementing Continuous Delivery

Chapter 12

Implementing continuous integration

In large companies with multiple teams working in parallel, it is very common to end up having tons of integration conflicts. This occurs more frequently when the codebase is under heavy development.

In order to mitigate this, it is highly recommended to use CI. The main idea is that development branches should not diverge much from the master branch. One way to do it is splitting the changes or new features into really small chunks so they can be finished and merged back pretty fast. Another way is to merge regularly; this is more suitable when features are difficult to break down into small ones.

When facing indivisible features, such as architectural changes, Feature Toggles are very helpful. With Feature Toggles, unfinished features can be merged and will not be accessible until the flag is turned on.

Towards continuous delivery

One of the problems developers were facing in the story is the manual creation of releases.

There are many tools that help automate such tasks, such as Jenkins, Travis, or Bamboo, just to name a few. As part of the proposed solution, we are going to configure an instance of Jenkins to run all of these tasks automatically. On every execution of the Jenkins job, a new release of the thimblerig-service will be created.

Moreover, since we already moved to CI, the status of the master branch should be always ready for production. And, in case some unfinished features have been merged, they are hidden thanks to Feature Toggles.

At this point, to solve the problem of the releases, we could have implemented either continuous delivery or continuous deployment (CD), but for the sake of simplicity we are going to implement continuous delivery. Let's get into it.

[ 282 ]

Leverage TDD by Implementing Continuous Delivery

Chapter 12

Jenkins installation

Jenkins is a very powerful tool and easy to learn. In this section, we are going to prepare the environment, which consists of a virtual machine running a Docker image of Jenkins. This setup is for demonstration purposes; for real scenarios, it will be better to install it in a dedicated server with more resources, or get it as a service from a company like CloudBees.

In this particular case, all the configuration is located in the Vagrantfile: Vagrant.configure("2") do |config|

config.vm.box = "ubuntu/trusty64"

config.vm.box_check_update = false

config.vm.network "forwarded_port", guest: 8080, host: 9090

config.vm.provider "virtualbox" do |vb|

vb.gui = false

vb.memory = 2048

end

config.vm.provision "docker" do |d|

d.run "jenkins/jenkins",

args: "-p 8080:8080 -p 50000:50000 -v

jenkins_home:/var/jenkins_home"

end

end

So, to get it up and running, we just need to execute the following command: $> vagrant up

If, after a restart or whatever the reason might be, Jenkins appears offline or you can't reach it, try running the same command with provision flag: $> vagrant up --provision

[ 283 ]

Leverage TDD by Implementing Continuous Delivery

Chapter 12

Once finished, we can open http://localhost:9090 in our favorite browser to continue the setup:

Since we are not installing it in the server but running it in a Docker image, this password is a bit tricky to get. Probably the easiest way is to access the Docker machine and get the password from the file, and that could be done like this:

$> vagrant ssh

$> docker exec jenkins-jenkins cat

/var/jenkins_home/secrets/initialAdminPassword

[ 284 ]

Leverage TDD by Implementing Continuous Delivery

Chapter 12

Copy the password, paste in the password field, and we move to the next step, which is configuring plugins. For now, we are going to install the recommended ones only. Other plugins can be installed later on in the administration panel:

[ 285 ]

Leverage TDD by Implementing Continuous Delivery

Chapter 12

Then, when the setup has finished installing plugins, another screen is shown. This is the last step of the configuration, creating an admin user. It's recommended to create a user with a password that is easy to remember:

This step can be skipped, but then the admin password will remain the same as the initial password, which is really difficult to remember. Now we are ready to use our brand new Jenkins installation.

Automating builds

Once we have Jenkins up and running, it is time to start using it. We are going to create a task on Jenkins that will download the thimblerig-service master branch, execute the tests, build it, and archive the resultant artifact.

[ 286 ]

Leverage TDD by Implementing Continuous Delivery

Chapter 12

Let's start by creating a Freestyle project:

We have to tell Jenkins where the repository is located. In this example, we don't need authentication, but is very likely we would need it in a real-world scenario:

[ 287 ]

Leverage TDD by Implementing Continuous Delivery

Chapter 12

The thimblerig-service project is a Gradle project. We are going to use the Jenkins Gradle plugin for compiling, testing, and building our service:

Finally, we have to specify the location of the test reports and the artifact built:

[ 288 ]

Leverage TDD by Implementing Continuous Delivery

Chapter 12

And we are done. This is not very different when compared to what we usually do in our local environment. It downloads the code from the master branch and uses Gradle for building the service, as developers were doing, according to John in the story.

First execution

With our project created in Jenkins, now it is time to test it. We never configured a triggered execution, so Jenkins is not monitoring the changes in the repository. For this example, launching the builds manually is more than enough, but in a real scenario we would like it to be triggered automatically on every change in the master branch:

The build has finished successfully; we can see in the summary that tests were executed but none has failed. We are ready to download the artifact and try to execute it locally: $> chmod u+x thimblerig-service.jar

$> ./thimblerig-service.jar

[ 289 ]

Leverage TDD by Implementing Continuous Delivery

Chapter 12

At some point, the logs will display a message like Tomcat started on port(s): 8080

(http). This means our that service is ready and we can start using it. To make sure, we can always check the health of the service by running:

$> curl http://localhost:8080/health

{"status":"UP"}

This concludes the example of continuous delivery. Although this example is fully functional, Jenkins is not the best place to store releases of the service. For a real-world use case, there are much more powerful alternatives, such as Artifactory, or simply Dockerize the service and push new versions to a private Docker registry.

What is next?

The example here is purely academic, and parts of the solution are a bit hacky. In a real company, Jenkins would be installed in a dedicated server and would have many more tasks to build and release. To orchestrate all of this, proper management of generated artifacts is needed. As mentioned earlier, some of the solutions that companies are adopting are tools such as Artifactory or private instances of Docker Registry to store Docker images of the services. Whatever the storage of choice, the procedure will remain the same—compile, test, build, archive. It's just a matter of configuration.

For the sake of brevity, some parts that required new code have been omitted and are left for the reader to complete as an exercise. Here are some ideas of how to continue: Create some tests for the REST controller.

There is an issue in the random number generator—it is not random at all. Fork the thimblerig-service project, create a test to reproduce the issue, fix it, and release a new version of the service by using the recently-created build project on Jenkins.

Use Docker.

All the code snippets and the rest of the project files required can be found online in the following repository: https:/​/​bitbucket.​org/​alexgarcia/​tdd-​java-​thimblerig-​service

[ 290 ]

Leverage TDD by Implementing Continuous Delivery

Chapter 12

This is just the beginning

You might have expected that by the time you reached the end of this book, you'd know everything about test-driven development (TDD). If that was the case, we're sorry that we'll have to disappoint you. It takes a lot of time and practice to master any craft, and TDD is no exception. Go on, apply what you have learned to your projects. Share knowledge with your colleagues. Most importantly, practice, practice, and practice. As with karate, only through continuous practice and repetition can one fully master TDD. We have been using it for a long time, and we still often face new challenges and learn new ways to improve our craftsmanship.

This does not have to be the end

Writing this book was a long journey filled with many adventures. We hope you enjoyed reading it as much as we enjoyed writing it.

We share our experience on a wide variety of subjects at our blog, at http:/​/

technologyconversations.​com.

Summary

Throughout Alice's fictitious story, some of the common problems which companies are facing nowadays were presented. One of them is the lack of time. In this particular case, and in the majority of cases, people lack time because they are trapped doing repetitive tasks that don't add value, thus there is this constant feeling that it's impossible to achieve more ambitious goals. One of the main excuses that developers give when asked why they are not practicing TDD is the lack of time for writing tests.


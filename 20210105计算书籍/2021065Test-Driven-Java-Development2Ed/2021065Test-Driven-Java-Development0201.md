# 0201. Tools, Frameworks, and Environments

"We become what we behold. We shape our tools and then our tools shape us." – Marshall McLuhan

## Summary

In this chapter, we took a break from TDD and introduced many tools and frameworks that will be used for code demonstrations in the rest of the chapters. We set up everything from version control, virtual machines, building tools, and IDEs, until we reached frameworks that are commonly used as today's testing tools.

We are big proponents of the open source movement. Following this spirit, we made a special effort to select free tools and frameworks in every category. Now that we have set up all the tools that we will need, in the next chapter, we will go deeper into TDD, starting with the Red-Green-Refactor procedure-TDD's cornerstone.

## 2.0

As every soldier knows his weapons, a programmer must be familiar with the development ecosystem and those tools that make programming much easier. Whether you are already using any of these tools at work or home, it is worth taking a look at many of them and comparing their features, advantages, and disadvantages. Let's get an overview of what we can find nowadays about the following topics and construct a small project to get familiar with some of them.

We won't go into the details of those tools and frameworks, since that will be done later on in the following chapters. The goal is to get you up and running, and provide you with a short overview of what they do and how.

The following topics will be covered in this chapter: 1) Git. 2) Virtual machines. 3) Build tools. 4) The integrated development environment. 5) Unit testing frameworks. 6) Hamcrest and AssertJ. 7) Code coverage tools. 8) Mocking frameworks. 9) User interface testing. 10) Behavior-driven development.

2『上面的 Java 开发工具和框架，做一张主题卡片。（2021-04-24）』 —  —  已完成

## 2.1 Git

Git is the most popular revision control system. For that reason, all the code used in this book is stored in Bitbucket (https://bitbucket.org/). If you don't have it already, install Git. Distributions for all the popular operating systems can be found at: http://git-scm.com.

Many graphical interfaces are available for Git; some of them being Tortoise (https://code.google.com/p/tortoisegit), Source Tree (https://www.sourcetreeapp.com), and Tower (http://www.git-tower.com/).

3『

[Bitbucket | The Git solution for professional teams](https://bitbucket.org/)

[TortoiseGit – Windows Shell Interface to Git](https://tortoisegit.org/)

[Sourcetree | Free Git GUI for Mac and Windows](https://www.sourcetreeapp.com/)

[The most powerful Git client for Mac and Windows | Tower Git Client](https://www.git-tower.com/mac)

』

## 2.2 Virtual machines

Even though they are outside the topic of this book, virtual machines are a powerful tool and a first-class citizen in a good development environment. They provide dynamic and easy-to-use resources in isolated systems so they can be used and dropped at the time we need them. This helps developers to focus on their tasks instead of wasting their time creating or installing required services from scratch. This is the reason why virtual machines have found room in here. We want to take advantage of them to keep you focused on the code.

In order to have the same environment no matter the OS you're using, we'll be creating virtual machines with Vagrant and deploying required applications with Docker. We chose Ubuntu as a base operating system in our examples, just because it is a popular, commonly used Unix-like distribution. Most of these technologies are platform-independent, but occasionally you won't be able to follow the instructions found here because you might be using some other operating system. In that case, your task is to find what the differences are between Ubuntu and your operating system and act accordingly.

### 2.2.1 Vagrant

Vagrant is the tool we are going to use for creating the development environment stack. It is an easy way to initialize ready-to-go virtual machines with minimum effort using preconfigured boxes. All boxes and configurations are placed in one file, called the Vagrant file.

Here is an example of creating a simple Ubuntu box. We made an extra configuration for installing MongoDB using Docker (the usage of Docker will be explained shortly). We assume that you have VirtualBox (https://www.virtualbox.org) and Vagrant (https://www.vagrantup.com) installed on your computer and that you have internet access.

In this particular case, we are creating an instance of Ubuntu 64-bits using the Ubuntu box (ubuntu/trusty64) and specifying that the VM should have 1 GB of RAM:

```
config.vm.box = "ubuntu/trusty64"
config.vm.provider "virtualbox" do |vb|
vb.memory = "1024"
end
```

Further on, we're exposing MongoDB's default port in the Vagrant machine and running it using Docker:

```
config.vm.network "forwarded_port", guest: 27017, host: 27017
config.vm.provision "docker" do |d|
  d.run "mongoDB", image: "mongo:2", args: "-p 27017:27017"
end
```

Finally, in order to speed up the Vagrant setup, we're caching some resources. You should install the plugin called cachier. For further information, visit: https://github.com/fgrehm/vagrant-cachier.

```
if Vagrant.has_plugin?("vagrant-cachier")
  config.cache.scope = :box
end
```

Now it's time to see it working. It usually takes a few minutes to run it for the first time because the base box and all the dependencies need to be downloaded and installed: 

```
$> vagrant plugin install vagrant-cachier
$> git clone
https://bitbucket.org/vfarcic/tdd-java-ch02-example-vagrant.git
$> cd tdd-java-ch02-example-vagrant
$> vagrant up
```

When this command is run, you should see the following output:

Be patient until the execution is finished. Once done, you'll have a new virtual machine with Ubuntu, Docker, and one MongoDB instance up and running. The best part is that all this was accomplished with a single command.

To see the status of the currently running VM, we can use the status argument: 

```
$> vagrant status
Current machine states:
default running (virtualbox)
```

The virtual machine can be accessed either through ssh or by using Vagrant commands, as in the following example:

```
$> vagrant ssh

Welcome to Ubuntu 14.04.2 LTS (GNU/Linux 3.13.0-46-generic x86_64)

* Documentation: https://help.ubuntu.com/

System information disabled due to load higher than 1.0

Get cloud support with Ubuntu Advantage Cloud Guest:

http://www.ubuntu.com/business/services/cloud

0 packages can be updated.

0 updates are security updates.

vagrant@vagrant-ubuntu-trusty-64:~$
```

Finally, to stop the virtual machine, exit from it and run the vagrant halt command: 

```
$> exit
$> vagrant halt
==> default: Attempting graceful shutdown of VM...
$>
```

For the list of Vagrant boxes or further details about configuring Vagrant, visit: https://www.vagrantup.com.

### 2.2.2 Docker

Once the environment is set, it is time to install the services and the software that we need.

This can be done using Docker, a simple and portable way to ship and run many applications and services in isolated containers. We will use it to install the required databases, web servers, and all the other applications required throughout this book, in a virtual machine created using Vagrant. In fact, the Vagrant VM that was previously created already has an example of getting an instance of MongoDB up and running using Docker.

Let's bring up the VM again (we stopped it previously with the vagrant halt command) and also MongoDB:

```
$> vagrant up
$> vagrant ssh
vagrant@vagrant-ubuntu-trusty-64:~$ docker start mongoDB
mongoDB
vagrant@vagrant-ubuntu-trusty-64:~$ docker ps
CONTAINER ID IMAGE COMMAND CREATED
360f5340d5fc mongo:2 "/entrypoint.sh mong..." 4 minutes ago
STATUS PORTS NAMES
Up 4 minutes 0.0.0.0:27017->27017/tcp mongoDB
vagrant@vagrant-ubuntu-trusty-64:~$ exit
```

With docker start, we started the container; with docker ps, we listed all the running processes.

By using this kind of procedure, we are able to reproduce a full-stack environment in the blink of an eye. You may be wondering if this is as awesome as it sounds. The answer is yes, it is. Vagrant and Docker allow developers to focus on what they are supposed to do and forget about complex installations and tricky configurations. Furthermore, we made an extra effort to provide you with all the necessary steps and resources to reproduce and test all the code examples and demonstrations in this book.

## 2.3 Build tools

With time, code tends to grow both in complexity and size. This occurs in the software industry by its nature. All products evolve constantly and new requirements are made and implemented across a product's life. Build tools offer a way to make managing the project life cycle as straightforward as possible, by following a few code conventions, such as the organization of your code, in a specific way, and by the usage of naming a convention for your classes or a determined project structure formed by different folders and files.

Some of you might be familiar with Maven or Ant. They are a great couple of Swiss army knives for handling projects, but we are here to learn so we decided to use Gradle. Some of the advantages of Gradle are its reduced boilerplate code, resulting in a much shorter file and a more readable configuration file. Among others, Google uses it as its build tool. It is supported by IntelliJ IDEA and is quite easy to learn and work with. Most of the functionalities and tasks are obtained by adding plugins.

Mastering Gradle is not the goal of this book. So, if you want to learn more about this awesome tool, take a tour through its website (http://gradle.org/) and read about the plugins you can use and the options you can customize. For a comparison of different Java build tools, visit: [Java Build Tools: Ant vs Maven vs Gradle | Technology Conversations](https://technologyconversations.com/2014/06/18/build-tools/).

Before proceeding forward, make sure that Gradle is installed on your system. Let's analyze the relevant parts of a build.gradle file. It holds project information in a concise way, using Groovy as the descriptor language. This is our project's build file, autogenerated with IntelliJ:

```
apply plugin: 'java'
sourceCompatibility = 1.7
version = '1.0'
```

A Java plugin is applied since it is a Java project. It brings common Java tasks, such as build, package, test, and so on. The source compatibility is set to JDK 7. The compiler will complain if we try to use the Java syntax that is not supported by this version: 

```
repositories {
    mavenCentral()
}
```

Maven Central (http://search.maven.org/) holds all our project dependencies. This section tells Gradle where to pull them from. The Maven Central repository is enough for this project, but you can add your custom repositories, if any. Nexus and Ivy are also supported:

```
dependencies {
    testCompile group: 'junit', name: 'junit', version: '4.12'
}
```

Last, but not least, this is how project dependencies are declared. IntelliJ decided to use JUnit as the testing framework.

Gradle tasks are easy to run. For example, to run tests from the command prompt, we can simply execute the following:

```
gradle test
```

This can be accomplished from IDEA by running the test task from the Gradle Tool Window that can be accessed from View|Tool Windows|Gradle. The tests result is stored in the HTML files that are located in the build/reports/tests directory. The following is the test report generated by running gradle test against the sample code:

随着时间的推移，代码的规模和复杂程度通常呈增长趋势。这是软件行业的性质决定的：所有产品都在生命周期内不断演进  —  —  实现客户提出的新需求。构建工具最大限度简化了项目生命周期的管理工作，它要求你遵循一些编码约定，如以特定方式组织代码、采用特定的类命名约定、将各种文件夹和文件组织成特定的项目结构。

有些读者可能熟悉 Maven 或 Ant，它们都是项目处理方面的「瑞士军刀」，但本书的主要目标是介绍 TDD，因此我们决定使用 Gradle。Gradle 的优点之一是样板式代码较少，因此其配置文件更简短、更易于理解。Gradle 还是 Google 使用的构建工具之一。它得到 IntelliJ IDEA 的支持，学习和使用都非常容易，且大部分功能和任务都是通过插件提供的。

精通Gradle并非本书的目标，如果你要更深入地学习这款出色的工具，请访问其官网（http://gradle.org/），了解可使用的插件和可定制的选项。有关各种 Java 构建工具的比较，请参阅：[Java Build Tools: Ant vs Maven vs Gradle | Technology Conversations](https://technologyconversations.com/2014/06/18/build-tools/)。

接着往下阅读前，请确认你的系统安装了 Gradle。下面分析一个 build.gradle 文件中相关的部分。这种文件以简洁的方式存储了项目信息，使用的描述符语言为 Groovy。下面是我们项目的构建文件，这是由 IntelliJ 自动生成的：

## 2.4 The integrated development environment

As many tools and technologies will be covered, we recommend using IntelliJ IDEA as the tool for code development. The main reason is that this integrated development environment (IDE) works without any tedious configuration. The Community Edition (IntelliJ IDEA CE) comes with a bunch of built-in features and plugins that make coding easy and efficient. It automatically recommends plugins that can be installed depending on the file extension. As IntelliJ IDEA is the choice we made for this book, you will find references and steps referring to its actions or menus. Readers should find a proper way to emulate those steps if they are using other IDEs. Refer to: https://www.jetbrains.com/idea/ for instructions on how to download and install IntelliJ IDEA.

### 2.4.1 The IDEA demo project

Let's create the base layout of the demo project. This project will be used throughout this chapter to illustrate all the topics that are covered. Java will be the programming language and Gradle (http://gradle.org/) will be used to run different sets of tasks, such as building, testing, and so on.

Let us import into IDEA the repository that contains examples from this chapter: 

2 Open IntelliJ IDEA, select Check out from Version Control, and click on Git.

2 Type https://bitbucket.org/vfarcic/tdd-java-ch02-example-junit.

git in the Git repository URL and click on Clone. Confirm for the rest of the IDEA questions until a new project is created with code cloned from the Git repository. The imported project should look similar to the following image:

1『目前通过远程仓库新建项目的方法：VCS => Get from Version Control，面板里输入 git 仓库的 URL。（2021-04-24）』

Now that we have got the project set up, it's time to take a look at unit-testing frameworks.

## 2.5 Unit-testing frameworks

In this section, two of the most used Java frameworks for unit testing are shown and briefly commented on. We will focus on their syntax and main features by comparing a test class written using both JUnit and TestNG. Although there are slight differences, both frameworks offer the most commonly used functionalities, and the main difference is how tests are executed and organized.

Let's start with a question. What is a test? How can we define it?

A test is a repeatable process or method that verifies the correct behavior of a tested target in a determined situation with a determined input expecting a predefined output or interactions.

In the programming approach, there are several types of tests depending on their scope — functional tests, acceptance tests, and unit tests. Further on, we will explore each of those types of tests in more detail.

Unit testing is about testing small pieces of code. Let's see how to test a single Java class. The class is quite simple, but enough for our interest:

```java
public class Friendships {
    private final Map<String, List<String>> friendships = new HashMap<>();

    public void makeFriends(String person1, String person2) {
        addFriend(person1, person2);
        addFriend(person2, person1);
    }

    public List<String> getFriendsList(String person) {
        if (!friendships.containsKey(person)) {
            return Collections.emptyList();
        }
        return friendships.get(person);
    }
    
    public boolean areFriends(String person1, String person2) {
        return friendships.containsKey(person1)
                && friendships.get(person1).contains(person2);
    }

    private void addFriend(String person, String friend) {
        if (!friendships.containsKey(person)) {
            friendships.put(person, new ArrayList<String>());
        }
        List<String> friends = friendships.get(person);
        if (!friends.contains(friend)) {
            friends.add(friend);
        }
    }
}
```

本节简要介绍两个最常用的 Java 单元测试框架  —  —  JUnit 和 TestNG，重点是通过比较使用它们编写的测试类阐述二者语法和主要功能。虽然存在细微的差别  —  —  主要是执行和组织测试的方式，但这两个框架都提供了最常用的功能。

我们从一个问题着手：测试是什么？如何定义？

测试是一个可重复的过程或方法，用于验证受测对象在指定环境下的行为是否正确，即向它提供指定的输入，并期望出现预定的输出或交互。

编程领域有多种范围不同的测试：功能测试、验收测试和单元测试，后面将更深入地探索这些测试类型。

单元测试旨在对一小块代码进行测试。下面看看如何测试一个 Java 类，这个类很简单，但足以激发你的兴趣：

### 2.5.1 JUnit

JUnit (http://junit.org/) is a simple and easy-to-learn framework for writing and running tests. Each test is mapped as a method, and each method should represent a specific known scenario in which a part of our code will be executed. The code verification is made by comparing the expected output or behavior with the actual output.

The following is the test class written with JUnit. There are some scenarios missing, but for now we are interested in showing what tests look like. We will focus on better ways to test our code and on best practices later in this book.

Test classes usually consist of three stages: set up, test, and tear down. Let's start with methods that set up data needed for tests. A setup can be performed on a class or method level:

```java
    Friendships friendships;

    @BeforeClass
    public static void beforeClass() {
        // This method will be executed once on initialization time
    }

    @Before
    public void before() {
        friendships = new Friendships();
        friendships.makeFriends("Joe", "Audrey");
        friendships.makeFriends("Joe", "Peter");
        friendships.makeFriends("Joe", "Michael");
        friendships.makeFriends("Joe", "Britney");
        friendships.makeFriends("Joe", "Paul");
    }
```

The @BeforeClass annotation specifies a method that will be run once before any of the test methods in the class. It is a useful way to do some general set up that will be used by most (if not all) tests.

The @Before annotation specifies a method that will be run before each test method. We can use it to set up test data without worrying that the tests that are run afterwards will change the state of that data. In the preceding example, we're instantiating the Friendships class and adding five sample entries to the Friendships list. No matter what changes will be performed by each individual test, this data will be recreated over and over until all the tests are performed.

Common examples of usage of those two annotations are the setting up of database data, the creation of files needed for tests, and so on. Later on, we'll see how external dependencies can and should be avoided using mocks. Nevertheless, functional or integration tests might still need those dependencies and the @Before and @BeforeClass annotations are a good way to set them up.

Once the data is set up, we can proceed with the actual tests:

```java
    @Test
    public void alexDoesNotHaveFriends() {
        Assert.assertTrue("Alex does not have friends", friendships.getFriendsList("Alex").isEmpty());
    }

    @Test
    public void joeHas5Friends() {
        Assert.assertEquals("Joe has 5 friends", 5, friendships.getFriendsList("Joe").size());
    }

    @Test
    public void joeIsFriendWithEveryone() {
        List<String> friendsOfJoe = Arrays.asList("Audrey", "Peter", "Michael", "Britney", "Paul");
        Assert.assertTrue(
                friendships.getFriendsList("Joe").containsAll(friendsOfJoe)
        );
    }
```

In this example, we are using a few of the many different types of asserts. We're confirming that Alex does not have any friends, while Joe is a very popular guy with five friends (Audrey, Peter, Michael, Britney, and Paul).

Finally, once the tests are finished, we might need to perform some cleanup:

```java
    @AfterClass
    public static void afterClass() {
        // This method will be executed once when all test are executed
    }

    @After
    public void after() {
        // This method will be executed once after each test execution
    }
```

In our example, in the Friendships class, we have no need to clean up anything. If there were such a need, those two annotations would provide that feature. They work in a similar fashion to the @Before and @BeforeClass annotations. @AfterClass is run once all tests are finished. The @After annotation is executed after each test. This runs each test method as a separate class instance. As long as we are avoiding global variables and external resources, such as databases and APIs, each test is isolated from the others. Whatever was done in one, does not affect the rest.

The complete source code can be found in the FriendshipsTest class at https:/​/bitbucket.​org/​vfarcic/​tdd-​java-​ch02-​example-​junit.

### 2.5.2 TestNG

In TestNG (http://testng.org/doc/index.html), tests are organized in classes, just as in the case of JUnit.

The following Gradle configuration (build.gradle) is required in order to run TestNG

tests:

dependencies {

testCompile group: 'org.testng', name: 'testng', version:

'6.8.21'

}

test.useTestNG() {

// Optionally you can filter which tests are executed using

// exclude/include filters

// excludeGroups 'complex'

}

Unlike JUnit, TestNG requires additional Gradle configuration that tells it to use TestNG to run tests.

The following test class is written with TestNG and is a reflection of what we did earlier with JUnit. Repeated imports and other boring parts are omitted with the intention of focusing on the relevant parts:

@BeforeClass

public static void beforeClass() {

// This method will be executed once on initialization time

}

@BeforeMethod

public void before() {

friendships = new Friendships();

friendships.makeFriends("Joe", "Audrey");

friendships.makeFriends("Joe", "Peter");

friendships.makeFriends("Joe", "Michael");

friendships.makeFriends("Joe", "Britney");

friendships.makeFriends("Joe", "Paul");

}

You probably already noticed the similarities between JUnit and TestNG. Both are using annotations to specify what the purposes of certain methods are. Besides different names (@Beforeclass versus @BeforeMethod), there is no difference between the two. However, unlike Junit, TestNG reuses the same test class instance for all test methods. This means that the test methods are not isolated by default, so more care is needed in the before and after methods.

Asserts are very similar as well:

public void alexDoesNotHaveFriends() {

Assert.assertTrue(friendships.getFriendsList("Alex").isEmpty(),

"Alex does not have friends");

}

public void joeHas5Friends() {

Assert.assertEquals(friendships.getFriendsList("Joe").size(), 5, "Joe has 5 friends");

}

public void joeIsFriendWithEveryone() {

List<String> friendsOfJoe =

Arrays.asList("Audrey", "Peter", "Michael", "Britney", "Paul"); Assert.assertTrue(friendships.getFriendsList("Joe")

.containsAll(friendsOfJoe));

}

The only notable difference when compared with JUnit is the order of the assert variables.

While the JUnit assert's order of arguments is optional message, expected values, and actual values, TestNG's order is an actual value, expected value, and optional message.

Besides the difference in the order of arguments we're passing to the assert methods, there are almost no differences between JUnit and TestNG.

You might have noticed that @Test is missing. TestNG allows us to set it on the class level and thus convert all public methods into tests.

The @After annotations are also very similar. The only notable difference is the TestNG

@AfterMethod annotation that acts in the same way as the JUnit @After annotation.

As you can see, the syntax is pretty similar. Tests are organized in to classes and test verifications are made using assertions. That is not to say that there are no more important differences between those two frameworks; we'll see some of them throughout this book. I invite you to explore JUnit (http://junit.org/) and TestNG (http://testng.org/) by

yourself.

The complete source code with the preceding examples can be found at https:/​/

bitbucket.​org/​vfarcic/​tdd-​java-​ch02-​example-​testng.

The assertions we have written until now have used only the testing frameworks. However, there are some test utilities that can help us make them nicer and more readable.

Hamcrest and AssertJ

In the previous section, we gave an overview of what a unit test is and how it can be written using two of the most commonly used Java frameworks. Since tests are an important part of our projects, why not improve the way we write them? Some cool projects emerged, aiming to empower the semantics of tests by changing the way that assertions are made. As a result, tests are more concise and easier to understand.

Hamcrest

Hamcrest adds a lot of methods called matchers. Each matcher is designed to perform a comparison operation. It is extensible enough to support custom matchers created by yourself. Furthermore, JUnit supports Hamcrest natively since its core is included in the JUnit distribution. You can start using Hamcrest effortlessly. However, we want to use the full-featured project so we will add a test dependency to Gradle's file: testCompile 'org.hamcrest:hamcrest-all:1.3'

Let us compare one assert from JUnit with the equivalent one from Hamcrest: The JUnit assert:

List<String> friendsOfJoe =

Arrays.asList("Audrey", "Peter", "Michael", "Britney", "Paul"); Assert.assertTrue( friendships.getFriendsList("Joe")

.containsAll(friendsOfJoe));

The Hamcrest assert:

assertThat(

friendships.getFriendsList("Joe"),

containsInAnyOrder("Audrey", "Peter", "Michael", "Britney",

"Paul")

);

As you can see, Hamcrest is a bit more expressive. It has a much bigger range of asserts that allows us to avoid some boilerplate code and, at the same time, makes code easier to read and is more expressive.

Here's another example:

JUnit assert:

Assert.assertEquals(5, friendships.getFriendsList("Joe").size()); Hamcrest assert:

assertThat(friendships.getFriendsList("Joe"), hasSize(5));

You'll notice two differences. The first is that, unlike JUnit, Hamcrest works almost always with direct objects. While in the case of JUnit, we needed to get the integer size and compare it with the expected number (5); Hamcrest has a bigger range of asserts so we can simply use one of them (hasSize) together with the actual object (List). Another difference is that Hamcrest has the inverse order with the actual value being the first argument (like TestNG).

Those two examples are not enough to show the full potential offered by Hamcrest. Later on in this book, there will be more examples and explanations of Hamcrest.

Visit http://hamcrest.org/ and explore its syntax.

The complete source code can be found in the FriendshipsHamcrestTest class in the https://bitbucket.org/vfarcic/tdd-java-ch02-example-junit repositories.

AssertJ

AssertJ works in a similar way to Hamcrest. A major difference is that AssertJ assertions can be concatenated.

To work with AssertJ, the dependency must be added to Gradle's dependencies: testCompile 'org.assertj:assertj-core:2.0.0'

Let's compare JUnit asserts with AssertJ:

Assert.assertEquals(5, friendships.getFriendsList("Joe").size()); List<String> friendsOfJoe =

Arrays.asList("Audrey", "Peter", "Michael", "Britney", "Paul"); Assert.assertTrue( friendships.getFriendsList("Joe")

.containsAll (friendsOfJoe)

);

The same two asserts can be concatenated to a single one in AssertJ:

assertThat(friendships.getFriendsList("Joe"))

.hasSize(5)

.containsOnly("Audrey", "Peter", "Michael", "Britney", "Paul"); This was a nice improvement. There was no need to have two separate asserts, nor was there a need to create a new list with expected values. Moreover, AssertJ is more readable and easier to understand.

The complete source code can be found in the FriendshipsAssertJTest class at https:/

/​bitbucket.​org/​vfarcic/​tdd-​java-​ch02-​example-​junit.

Now that we have the tests up and running, we might want to see what the code coverage is that is generated by our tests.

Code coverage tools

The fact that we wrote tests does not mean that they are good, nor that they cover enough code. As soon as we start writing and running tests, the natural reaction is to start asking questions that were not available before. What parts of our code are properly tested? What are the cases that our tests did not take into account? Are we testing enough? These and other similar questions can be answered with code coverage tools. They can be used to identify the blocks or lines of code that were not covered by our tests; they can also calculate the percentage of code covered and provide other interesting metrics.

They are powerful tools used to obtain metrics and show relations between tests and implementation code. However, as with any other tool, their purpose needs to be clear.

They do not provide information about quality, but only about which parts of our code have been tested.

Code coverage shows whether the code lines are reached during test

execution, but it is not a guarantee of good testing practices because test quality is not included in these metrics.

Let's take a look at one of the most popular tools used to calculate code coverage.

JaCoCo

Java Code Coverage (JaCoCo) is a well-known tool for measuring test coverage.

To use it in our project, we need to add a few lines to our Gradle configuration file, that is, build.gradle:

1 Add the Gradle plugin for JaCoCo:

apply plugin: 'jacoco'

2 To see the JaCoCo results, run the following from your command prompt: gradle test jacocoTestReport

3 The same Gradle tasks can be run from the Gradle Tasks IDEA Tool Window.

4 The end result is stored in the build/reports/jacoco/test/html directory.

It's an HTML file that can be opened in any browser:

Further chapters of this book will explore code coverage in more detail. Until then, go to http://www.eclemma.org/jacoco/ for more information.

Mocking frameworks

Our project looks cool, but it's too simple and it is far from being a real project. It still doesn't use external resources. A database is required by Java projects so we'll try to introduce it, as well.

What is the common way to test code that uses external resources or third-party libraries?

Mocks are the answer. A mock object, or simply a mock, is a simulated object that can be used to replace real ones. They are very useful when objects that depend on external resources are deprived of them.

In fact, you don't need a database at all while you are developing the application. Instead, you can use mocks to speed up development and testing and use a real database connection only at runtime. Instead of spending time setting up a database and preparing test data, we can focus on writing classes and think about them later on during integration time.

For demonstration purposes, we'll introduce two new classes: the Person class and the FriendCollection class that are designed to represent persons and database object mapping. Persistence will be done with MongoDB (https://www.mongodb.org/).

Our sample will have two classes. Person will represent database object data; FriendCollection will be our data access layer. The code is, hopefully, self-explanatory.

Let's create and use the Person class:

public class Person {

@Id

private String name;

private List<String> friends;

public Person() { }

public Person(String name) {

this.name = name;

friends = new ArrayList<>();

}

public List<String> getFriends() {

return friends;

}

public void addFriend(String friend) {

if (!friends.contains(friend)) friends.add(friend);

}

}

Let's create and use the FriendsCollection class:

public class FriendsCollection {

private MongoCollection friends;

public FriendsCollection() {

try {

DB db = new MongoClient().getDB("friendships");

friends = new Jongo(db).getCollection("friends");

} catch (UnknownHostException e) {

throw new RuntimeException(e.getMessage());

}

}

public Person findByName(String name) {

return friends.findOne("{_id: #}", name).as(Person.class);

}

public void save(Person p) {

friends.save(p);

}

}

In addition, some new dependencies have been introduced so the Gradle dependencies block needs to be modified, as well. The first one is the MongoDB driver, which is required to connect to the database. The second is Jongo, a small project that makes accessing Mongo collections pretty straightforward.

The Gradle dependencies for mongodb and jongo are as follows:

dependencies {

compile 'org.mongodb:mongo-java-driver:2.13.2'

compile 'org.jongo:jongo:1.1'

}

We are using a database so the Friendships class should also be modified. We should change a map to FriendsCollection and modify the rest of the code to use it. The end result is the following:

public class FriendshipsMongo {

private FriendsCollection friends;

public FriendshipsMongo() {

friends = new FriendsCollection();

}

public List<String> getFriendsList(String person) {

Person p = friends.findByName(person);

if (p == null) return Collections.emptyList();

return p.getFriends();

}

public void makeFriends(String person1, String person2) {

addFriend(person1, person2);

addFriend(person2, person1);

}

public boolean areFriends(String person1, String person2) {

Person p = friends.findByName(person1);

return p != null && p.getFriends().contains(person2);

}

private void addFriend(String person, String friend) {

Person p = friends.findByName(person);

if (p == null) p = new Person(person);

p.addFriend(friend);

friends.save(p);

}

}

The complete source code can be found in the FriendsCollection and

FriendshipsMongo classes in

the https://bitbucket.org/vfarcic/tdd-java-ch02-example-junit repository.

Now that we have our Friendships class working with MongoDB, let's take a look at one possible way to test it by using mocks.

Mockito

Mockito is a Java framework that allows easy creation of the test double.

The Gradle dependency is the following:

dependencies {

testCompile group: 'org.mockito', name: 'mockito-all', version:

'1.+'

}

Mockito runs through the JUnit runner. It creates all the required mocks for us and injects them into the class with tests. There are two basic approaches; instantiating mocks by ourselves and injecting them as class dependencies via a class constructor or using a set of annotations. In the next example, we are going to see how it is done using annotations.

In order for a class to use Mockito annotations, it needs to be run with MockitoJUnitRunner. Using the runner simplifies the process because you just simply add annotations to objects to be created:

@RunWith(MockitoJUnitRunner.class)

public class FriendshipsTest {

...

}

In your test class, the tested class should be annotated with @InjectMocks. This tells Mockito which class to inject mocks into:

@InjectMocks

FriendshipsMongo friendships;

From then on, we can specify which specific methods or objects inside the class, in this case FriendshipsMongo, will be substituted with mocks:

@Mock

FriendsCollection friends;

In this example, FriendsCollection inside the FriendshipsMongo class will be mocked.

Now, we can specify what should be returned when friends is invoked:

Person joe = new Person("Joe");

doReturn(joe).when(friends).findByName("Joe");

assertThat(friends.findByName("Joe")).isEqualTo(joe);

In this example, we're telling Mockito to return the joe object whenever friends.findByName("Joe") is invoked. Later on, we're verifying with assertThat that this assumption is correct.

Let's try to do the same test as we did previously in the class that was without MongoDB:

@Test

public void joeHas5Friends() {

List<String> expected =

Arrays.asList("Audrey", "Peter", "Michael", "Britney", "Paul"); Person joe = spy(new Person("Joe"));

doReturn(joe).when(friends).findByName("Joe");

doReturn(expected).when(joe).getFriends();

assertThat(friendships.getFriendsList("Joe"))

.hasSize(5)

.containsOnly("Audrey", "Peter", "Michael", "Britney", "Paul");

}

A lot of things happened in this small test. First, we're specifying that joe is a spy. In Mockito, spies are real objects that use real methods unless specified otherwise. Then, we're telling Mockito to return joe when the friends method calls getFriends. This combination allows us to return the expected list when the getFriends method is invoked. Finally, we're asserting that the getFriendsList returns the expected list of names.

The complete source code can be found in the FriendshipsMongoAssertJTest class in the https://bitbucket.org/vfarcic/tdd-java-ch02-example-junit repository.

We'll use Mockito later on; throughout this book, you'll get your chance to become more familiar with it and with mocking in general. More information about Mockito can be found at http://mockito.org/.

EasyMock

EasyMock is an alternative mocking framework. It is very similar to Mockito. However, the main difference is that EasyMock does not create spy objects but mocks. Other differences are syntactical.

Let's see an example of EasyMock. We'll use the same set of test cases as those that were used for the Mockito examples:

@RunWith(EasyMockRunner.class)

public class FriendshipsTest {

@TestSubject

FriendshipsMongo friendships = new FriendshipsMongo();

@Mock(type = MockType.NICE)

FriendsCollection friends;

}

Essentially, the runner does the same as the Mockito runner:

@TestSubject

FriendshipsMongo friendships = new FriendshipsMongo();

@Mock(type = MockType.NICE)

FriendsCollection friends;

The @TestSubject annotation is similar to Mockito's @InjectMocks, while the @Mock annotation denotes an object to be mocked in a similar fashion to Mockito's @Mock.

Furthermore, the type NICE tells the mock to return empty.

Let's compare one of the asserts we did with Mockito:

@Test

public void mockingWorksAsExpected() {

Person joe = new Person("Joe");

expect(friends.findByName("Joe")).andReturn(joe);

replay(friends);

assertThat(friends.findByName("Joe")).isEqualTo(joe);

}

Besides small differences in syntax, the only disadvantage of EasyMock is that the additional instruction replay was needed. It tells the framework that the previously specified expectation should be applied. The rest is almost the same. We're specifying that friends.findByName should return the joe object, applying that expectation and, finally, asserting whether the actual result is as expected.

In the EasyMock version, the second test method that we used with Mockito is the following:

@Test

public void joeHas5Friends() {

List<String> expected =

Arrays.asList("Audrey", "Peter", "Michael", "Britney", "Paul"); Person joe = createMock(Person.class);

expect(friends.findByName("Joe")).andReturn(joe);

expect(joe.getFriends()).andReturn(expected);

replay(friends);

replay(joe);

assertThat(friendships.getFriendsList("Joe"))

.hasSize(5)

.containsOnly("Audrey", "Peter", "Michael", "Britney", "Paul");

}

Again, there are almost no differences when compared to Mockito, except that EasyMock does not have spies. Depending on the context, that might be an important difference.

Even though both frameworks are similar, there are small details that make us choose Mockito as a framework, which will be used throughout this book.

Visit http://easymock.org/ for more information about this asserts library.

The complete source code can be found in the FriendshipsMongoEasyMockTest class in the https://bitbucket.org/vfarcic/tdd-java-ch02-example-junit repository.

Extra power for mocks

Both projects introduced earlier do not cover all types of methods or fields. Depending on the applied modifiers, such as static or final, a class, method, or field, can be out of range for Mockito or EasyMock. In such cases, we can use PowerMock to extend the mocking framework. This way, we can mock objects that can only be mocked in a tricky manner.

However, one should be cautious with PowerMock since the necessity to use many of the features it provides is usually a sign of poor design. If you're working on a legacy code, PowerMock might be a good choice. Otherwise, try to design your code in such a way that PowerMock is not needed. We'll show you how to do that later on.

For more information, visit https://code.google.com/p/powermock/.

User interface testing

Even though unit testing can and should cover the major part of the application, there is still a need to work on functional and acceptance tests. Unlike unit tests, they provide higher-level verifications, and are usually performed at entry points, and rely heavily on user interfaces. At the end, we are creating applications that are, in most cases, used by humans, so being confident of our application's behavior is very important. This comfort status can be achieved by testing what the application is expected to do, from the point of view of real users.

Here, we'll try to provide an overview of functional and acceptance testing through a user interface. We'll use the web as an example, even though there are many other types of user interfaces, such as desktop applications, smartphone interfaces, and so on.

Web-testing frameworks

The application classes and data sources have been tested throughout this chapter, but there is still something missing; the most common user entry point — the web. Most enterprise applications such as intranets or corporate sites are accessed using a browser. For this reason, testing the web provides significant value, helping us to make sure that it is doing what it is expected to do.

Furthermore, companies are investing a lot of time performing long and heavy manual tests every time the application changes. This is a big waste of time since a lot of those tests can be automatized and executed without supervision, using tools such as Selenium or Selenide.

Selenium

Selenium is a great tool for web testing. It uses a browser to run verifications and it can handle all the popular browsers, such as Firefox, Safari, and Chrome. It also supports headless browsers to test web pages with much greater speed and less resources consumption.

There is a SeleniumIDE plugin that can be used to create tests by recording actions performed by the user. Currently, it is only supported by Firefox. Sadly, even though tests generated this way provide very fast results, they tend to be very brittle and cause problems in the long run, especially when some part of a page changes. For this reason, we'll stick with the code written without the help from that plugin.

The simplest way to execute Selenium is to run it through JUnitRunner.

All Selenium tests start by initializing WebDriver, the class used for communication with browsers:

1. Let's start by adding the Gradle dependency:

dependencies {

testCompile 'org.seleniumhq.selenium:selenium-java:2.45.0'

}

2. As an example, we'll create a test that searches Wikipedia. We'll use a Firefox driver as our browser of choice:

WebDriver driver = new FirefoxDriver();

WebDriver is an interface that can be instantiated with one of the many drivers provided by Selenium:

1. To open a URL, the instruction would be the following:

driver.get("http://en.wikipedia.org/wiki/Main_Page");

2. Once the page is opened, we can search for an input element by its name and then type some text:

WebElement query = driver.findElement(By.name("search"));

query.sendKeys("Test-driven development");

3. Once we type our search query, we should find and click the Go button: WebElement goButton = driver.findElement(By.name("go"));

goButton.click();

4. Once we reach our destination, it is time to validate that, in this case, the page title is correct:

assertThat(driver.getTitle(),

startsWith("Test-driven development"));

5. Finally, the driver should be closed once we're finished using it:

driver.quit();

That's it. We have a small but valuable test that verifies a single use case. While there is much more to be said about Selenium, hopefully, this has provided you with enough information to realize the potential behind it.

Visit http://www.seleniumhq.org/ for further information and more complex uses of WebDriver.

The complete source code can be found in the SeleniumTest class in

the https://bitbucket.org/vfarcic/tdd-java-ch02-example-web repository.

While Selenium is the most commonly used framework to work with browsers, it is still very low-level and requires a lot of tweaking. Selenide was born out of the idea that Selenium would be much more useful if there was a higher-level library that could implement some of the common patterns and solve often-repeated needs.

Selenide

What we have seen about Selenium is very cool. It brings the opportunity to probe that our application is doing things well, but sometimes it is a bit tricky to configure and use.

Selenide is a project based on Selenium that offers a good syntax for writing tests and makes them more readable. It hides the usage of WebDriver and configurations from you, while still maintaining a high-level of customization:

1. Like all the other libraries we have used until now, the first step is to add the Gradle dependency:

dependencies {

testCompile 'com.codeborne:selenide:2.17'

}

2. Let's see how we can write the previous Selenium test using Selenide instead. The syntax might be familiar to for those who know JQuery

(https://jquery.com/):

public class SelenideTest {

@Test

public void wikipediaSearchFeature() throws

InterruptedException {

// Opening Wikipedia page

open("http://en.wikipedia.org/wiki/Main_Page");

// Searching TDD

$(By.name("search")).setValue("Test-driven development");

// Clicking search button

$(By.name("go")).click();

// Checks

assertThat(title(),

startsWith("Test-driven development"));

}

}

This was a more expressive way to write a test. On top of a more fluent syntax, there are some things that happen behind this code and would require additional lines of Selenium.

For example, a click action will wait until an element in question is available, and will fail only if the predefined period of time has expired. Selenium, on the other hand, would fail immediately. In today's world, with many elements being loaded dynamically through JavaScript, we cannot expect everything to appear at once. Hence, this Selenide feature proves to be useful and saves us from using repetitive boilerplate code. There are many other benefits Selenide brings to the table. Due to the benefits that Selenide provides when compared with Selenium, it will be our framework of choice throughout this book.

Furthermore, there is a whole chapter dedicated to web testing using this framework.

Visit http://selenide.org/ for more information on ways to use web drivers in your tests.

No matter whether tests were written with one framework or another, the effect is the same.

When tests are run, a Firefox browser window will emerge and execute all steps defined in the test sequentially. Unless a headless browser was chosen as your driver of choice, you will be able to see what is going on throughout the test. If something goes wrong, a failure trace is available. On top of that, we can take browser screenshots at any point. For example, it is a common practice to record the situation at the time of a failure.

The complete source code can be found in the SelenideTest class in the

https://bitbucket.org/vfarcic/tdd-java-ch02-example-web repository.

Armed with a basic knowledge of web-testing frameworks, it is time to take a short look at BDD.

Behavior-driven development

Behavior-driven development (BDD) is an agile process designed to keep the focus on stakeholder value throughout the whole project. The premise of BDD is that the requirement has to be written in a way that everyone, be it the business representative, analyst, developer, tester, manager, and so on, understands it. The key is to have a unique set of artifacts that are understood and used by everyone — a collection of user stories.

Stories are written by the whole team and used as both requirements and executable test cases. It is a way to perform TDD with a clarity that cannot be accomplished with unit testing. It is a way to describe and test functionality in (almost) natural language and make it runnable and repeatable.

A story is composed of scenarios. Each scenario represents a concise behavioral use case and is written in natural language using steps. Steps are a sequence of the preconditions, events, and outcomes of a scenario. Each step must start with the words Given, When, or Then. Given is for preconditions, When is for actions, and Then is for performing validations.

This was only a brief introduction. There is a whole chapter, Chapter 8, BDD – Working Together with the Whole Team, dedicated to this topic. Now it is time to introduce JBehave and Cucumber as two of the many available frameworks for writing and executing stories.

JBehave

JBehave is a Java BDD framework used for writing acceptance tests that are able to be executed and automated. The steps used in stories are bound to Java code through several annotations provided by the framework:

1. First of all, add JBehave to Gradle dependencies:

dependencies {

testCompile 'org.jbehave:jbehave-core:3.9.5'

}

2. Let's go through a few example steps:

@Given("I go to Wikipedia homepage")

public void goToWikiPage() {

open("http://en.wikipedia.org/wiki/Main_Page");

}

3. This is the Given type of step. It represents a precondition that needs to be fulfilled for some actions to be performed successfully. In this particular case, it will open a Wikipedia page. Now that we have our precondition specified, it is time to define some actions:

@When("I enter the value $value on a field named $fieldName") public void enterValueOnFieldByName(String value, String fieldName)

{

$(By.name(fieldName)).setValue(value);

}

@When("I click the button $buttonName")

public void clickButonByName(String buttonName){

$(By.name(buttonName)).click();

}

4. As you can see, actions are defined with the When annotation. In our case, we can use those steps to set some value to a field or click on a specific button. Once actions are performed, we can deal with validations. Note

that steps can be more flexible by introducing parameters:

@Then("the page title contains $title")

public void pageTitleIs(String title) {

assertThat(title(), containsString(title));

}

Validations are declared using the Then annotation. In this example, we are validating the page title as expected.

These steps can be found in the WebSteps class in

the https://bitbucket.org/vfarcic/tdd-java-ch02-example-web repository.

Once we have defined our steps, it is time to use them. The following story combines those steps in order to validate a desired behavior:

Scenario: TDD search on wikipedia

It starts with naming the scenario. The name should be as concise as possible, but enough to identify the user case unequivocally; it is for informative purposes only: Given I go to Wikipedia homepage

When I enter the value Test-driven development on a field named

search

When I click the button go

Then the page title contains Test-driven development

As you can see, we are using the same steps text that we defined earlier. The code related to those steps will be executed in a sequential order. If any of them are halted, the execution is halted and the scenario itself is considered failed.

Even though we defined our steps ahead of stories, it can be done the other way around with a story being defined first and the steps following. In that case, the status of a scenario would be pending, meaning that the required steps are missing.

This story can be found in the wikipediaSearch.story file in

the https://bitbucket.org/vfarcic/tdd-java-ch02-example-web repository.

To run this story, execute the following:

$> gradle testJBehave

While the story is running, we can see that actions are taking place in the browser. Once it is finished, a report with the results of an execution is generated. It can be found in build/reports/jbehave:

JBehave story execution report

For brevity, we excluded the build.gradle code to run JBehave stories. The completed source code can be found in

the https://bitbucket.org/vfarcic/tdd-java-ch02-example-web repository.

For further information on JBehave and its benefits,

visit http://jbehave.org/.

Cucumber

Cucumber was originally a Ruby BDD framework. These days it supports several languages including Java. It provides functionality that is very similar to JBehave.

Let's see the same examples written in Cucumber.

The same as any other dependency we have used until now, Cucumber needs to be added to build.gradle before we can start using it:

dependencies {

testCompile 'info.cukes:cucumber-java:1.2.2'

testCompile 'info.cukes:cucumber-junit:1.2.2'

}

We will create the same steps as we did with JBehave, using the Cucumber way:

@Given("^I go to Wikipedia homepage$")

public void goToWikiPage() {

open("http://en.wikipedia.org/wiki/Main_Page");

}

@When("^I enter the value (.*) on a field named (.*)$")

public void enterValueOnFieldByName(String value,

String fieldName) {

$(By.name(fieldName)).setValue(value);

}

@When("^I click the button (.*)$")

public void clickButonByName(String buttonName) {

$(By.name(buttonName)).click();

}

@Then("^the page title contains (.*)$")

public void pageTitleIs(String title) {

assertThat(title(), containsString(title));

}

The only noticeable difference between these two frameworks is the way Cucumber defines steps text. It uses regular expressions to match variables types, unlike JBehave which deduces them from a method signature.

The steps code can be found in the WebSteps class in

the https://bitbucket.org/vfarcic/tdd-java-ch02-example-web repository: Let's see how the story looks when written using the Cucumber syntax:

Feature: Wikipedia Search

Scenario: TDD search on wikipedia

Given I go to Wikipedia homepage

When I enter the value Test-driven development on a field named

search

When I click the button go

Then the page title contains Test-driven development

Note that there are almost no differences. This story can be found in the wikipediaSearch.feature file in

the https://bitbucket.org/vfarcic/tdd-java-ch02-example-web repository.

As you might have guessed, to run a Cucumber story, all you need to do is run the following Gradle task:

$> gradle testCucumber

The result reports are located in the build/reports/cucumber-report directory. This is the report for the preceding story:

Cucumber story execution report

The full code example can be found in

the https://bitbucket.org/vfarcic/tdd-java-ch02-example-web repository.

For a list of languages supported by Cucumber or for any other details, visit https://cukes.info/.

Since both JBehave and Cucumber offer a similar set of features, we decided to use JBehave throughout the rest of this book. There is a whole chapter dedicated to BDD and JBehave.

# 2020082PHP-Objects-Patterns-PracticeR03

## 记忆时间

## 0305. Testing with PHPUnit

In this chapter, I revisited the kinds of tests we all write as developers, but all too often thoughtlessly discard. From there, I introduced PHPUnit, which lets you write the same kind of throwaway tests during development, but then keep them and feel the lasting benefit! I created a test-case implementation, and I covered the available assertion methods. I also examined constraints and explored the devious world of mock objects. Next, I showed how refactoring for testing can improve design, demonstrating some techniques for testing web applications—first by using just PHPUnit, and then by using Selenium. Finally, I risked the ire of some by warning of the costs that tests incur and discussing the trade-offs involved.

Every component in a system depends for its continued smooth running on the consistency of operation and interface of its peers. By definition, then, development breaks systems. As you improve your classes and packages, you must remember to amend any code that works with them. For some changes, this can create a ripple effect, affecting components far away from the code you originally changed. Eagle-eyed vigilance and an encyclopedic knowledge of a system’s dependencies can help to address this problem. Of course, while these are excellent virtues, systems soon grow too complex for every unwanted effect to be easily predicted, not least because systems often combine the work of many developers. To address this problem, it is a good idea to test every component regularly. This, of course, is a repetitive and complex task; and as such, it lends itself well to automation.

Among the test solutions available to PHP programmers, PHPUnit is perhaps the most ubiquitous and certainly the most fully featured tool. In this chapter, you will learn the following about PHPUnit: 1) Installation: Using PEAR to install PHPUnit. 2) Writing Tests: Creating test cases and using assertion methods. 3) Handling Exceptions: Strategies for confirming failure. 4) Running multiple tests: Collecting tests into suites. 5) Constructing assertion logic: Using constraints. 6) Faking components: Mocks and stubs. 7) Testing web applications: Testing with and without additional tools.

本章重温了作为开发者所会编写却也会经常放弃的各种测试，并且介绍了 PhPunit。PhPunit 使你能在开发过程中编写出不被随意丢弃的测试，并且可以将这些测试保存起来并因此受益！我们演示了如何实现一个测试用例，并且介绍了可用的断言方法。我们讲解了约束和 mock 对象的用法。此外，我们展示了测试重构如何改进你的设计，以及测试 Web 应用的一些技巧（使用了 PhPunit 和 Selenium）。最后我冒着可能使某些人不满的风险，警告读者测试需要付出一定的代价，并讨论了如何权衡这些代价。

### 5.1 Functional Tests and Unit Tests

Testing is essential in any project. Even if you don’t formalize the process, you must have found yourself developing informal lists of actions that put your system through its paces. This process soon becomes wearisome, and that can lead to a fingers-crossed attitude to your projects.

One approach to testing starts at the interface of a project, modeling the various ways in which a user might negotiate the system. This is probably the way you would go when testing by hand, although there are various frameworks for automating the process. These functional tests are sometimes called acceptance tests because a list of actions performed successfully can be used as criteria for signing off a project phase. Using this approach, you typically treat the system as a black box—your tests remain willfully ignorant of the hidden components that collaborate to form the system under test.

测试在任何项目中都是一个基本要素。即使你的测试流程并不规范，也一定使用了一系列确认系统是否正常工作的操作。这种不规范的测试流程很快就会变得乏味，并且会逐渐让人形成种撞大运的心态。有一种测试方法是从一个项目的接口开始，为用户可能使用系统的各种方式建模。而这也是手工测试时通常会使用的方式，虽然也有众多的框架可以自动化该过程。这些功能测试有时又被称为验收测试（acceptance test），因为一个成功执行的动作列表可以作为一个项目阶段完成的依据。使用该方法时，通常会把系统看做一个黑盒一一测试只针对产品功能，并不关注项目内部结构和处理过程。

2『这里给出了「验收测试」的定义，做一张术语卡片。』——已完成

Whereas functional tests operate from without, unit tests work from the inside out. Unit testing tends to focus on classes, with test methods grouped together in test cases. Each test case puts one class through a rigorous workout, checking that each method performs as advertised and fails as it should. The objective, as far as possible, is to test each component in isolation from its wider context. This often supplies you with a sobering verdict on the success of your mission to decouple the parts of your system.

Tests can be run as part of the build process, directly from the command line, or even via a web page. In this chapter, I’ll concentrate on the command line.

Unit testing is a good way of ensuring the quality of design in a system. Tests reveal the responsibilities of classes and functions. Some programmers even advocate a test-first approach. You should, they say, write the tests before you even begin work on a class. This lays down a class’s purpose, ensuring a clean interface and short, focused methods. Personally, I have never aspired to this level of purity—it just doesn’t suit my style of coding. Nevertheless, I attempt to write tests as I go. Maintaining a test harness provides me with the security I need to refactor my code. I can pull down and replace entire packages with the knowledge that I have a good chance of catching unexpected errors elsewhere in the system.

功能测试从外部着手，而单元测试（本章的主题）则从内部着手。单元测试更加关注于类，并将测试方法组合到测试用例中。每个测试用例通过严格的检测来处理一个类，检査每个方法是否如预期般成功执行或失败。单元测试的目标是尽可能地在隔离周边环境的情况下测试每个组件。只有隔离了周围环境的影响，才能发现被测试的组件与周边组件间的耦合是否真正被解开。测试可以作为项目构建过程的一部分，直接从命令行或者甚至通过一个网页来执行。本章主要采用命令行方式进行测试。

单元测试是保证系统设计质量的好办法。测试揭示了类和方法的职责。一些程序员甚至提倡测试先行（test-first）的开发方式。他们认为应该在写一个类之前先写好测试。测试设定了一个类的目的，保证了一个干净的接口和简短并集中的方法。我个人曾未渴望达到这样纯粹的程度——也许是因为这不符合我的编码风格。然而，我每前进一步都会努力写测试。测试给我提供了重构代码时的安全保障。因为我知道在系统的其他地方可以捕获非预期的错误，所以可以放心地删除或替换掉项目中的某个代码包。

### 5.2 Testing by Hand

In the last section, I said that testing was essential in every project. I could have said instead that testing is inevitable in every project. We all test. The tragedy is that we often throw away this good work. So, let’s create some classes to test. Here is a class that stores and retrieves user information. For the sake of demonstration, it generates arrays, rather than the User objects you’d normally expect to use:

```php
<?php

namespace App\Code;

class UserStore {
    private $users = [];

    public function addUser(string $name, string $mail, string $pass): bool {
        if (isset($this->users[$mail])) {
            throw new \Exception(
                "User {$mail} already in the system"
            );
        }

        if (strlen($pass) < 5) {
            throw new \Exception(
                "Password must have 5 or more letters"
            );
        }

        $this->users[$mail] = [
            'pass' => $pass,
            'mail' => $mail,
            'name' => $name
        ];

        return true;
    }

    public function notifyPasswordFailure(string $mail) {
        if (isset($this->users[$mail])) {
            $this->users[$mail]['failed'] = time();
        }
    }

    public function getUser(string $mail): array {
        return $this->users[$mail];
    }
}
```

1『发现作者写函数的风格，入参和输出的类型都定死，但数据流开发的过程中，类型定死后经常遇到类型不符导致的 bug，后来把固定类型都取消了。但直觉上，作者的做法是好的，应该是有效的避免了后面深层次的 bug，只是目前自己的 level 达不到那个高度，践行不了。（2020-09-23）』

This class accepts user data with the addUser() method and retrieves it via getUser(). The user’s e-mail address is used as the key for retrieval. If you’re like me, you’ll write some sample implementation as you develop, just to check that things are behaving as you designed them:

1『直接在 laravel 里实现，代码如下。』

```php
<?php

namespace App\Http\Controllers;

use App\Code\UserStore;
use Illuminate\Http\Request;

class TestController extends Controller
{
    public function test() {
        $store = new UserStore();
        $store->addUser(
            'bob williams',
            'bob@example.com',
            '12345'
        );
        $store->notifyPasswordFailure('bob@example.com');
        $user = $store->getUser('bob@example.com');
        return $user;
    }
}
```

This is the sort of thing that I might add to the foot of a file as I work on the class it contains. The test validation is performed manually, of course; it’s up to me to eyeball the results and confirm that the data returned by UserStore::getUser() corresponds with the information I added initially. It’s a test of sorts, nevertheless. Here is a client class that uses UserStore to confirm that a user has provided the correct authentication information:

```php
<?php

namespace App\Code;

class Validator {
    private $store;

    public function __construct(UserStore $store)
    {
        $this->store = $store;
    }

    public function validateUser(string $mail, string $pass): bool {
        if (! is_array($user = $this->store->getUser($mail))) {
            return false;
        }

        if ($user['pass'] == $pass) {
            return true;
        }

        $this->store->notifyPasswordFailure($mail);

        return false;
    }
}
```

The class requires a UserStore object, which it saves in the \$store property. This property is used by the validateUser() method to ensure, first of all, that the user referenced by the given e-mail address exists in the store; and, second, that the user’s password matches the provided argument. If both these conditions are fulfilled, the method returns true. Once again, I might test this as I go along:

```php
class TestController extends Controller
{
    public function test() {
        $store = new UserStore();
        $store->addUser(
            'bob williams',
            'bob@example.com',
            '12345'
        );
        // $store->notifyPasswordFailure('bob@example.com');
        // $user = $store->getUser('bob@example.com');
        $validator = new Validator($store);
        if ($validator->validateUser('bob@example.com', '12345')) {
            print "pass, friend\n";
        } else print "false\n";
    }
}
```

I instantiate a UserStore object, which I prime with data and pass to a newly instantiated Validator object. I can then confirm a user name and password combination. Once I’m finally satisfied with my work, I could delete these sanity checks altogether or comment them out. This is a terrible waste of a valuable resource. These tests could form the basis of a harness to scrutinize the system as I develop. One of the tools that might help me to do this is PHPUnit.

1『目前自己没写单元测试就是上面的这种状态，总是在 postman 里测试，测试完把相关代码删掉，现在想想确实是一种资源的极大浪费，其实这些测试代码都很有用的。』

一旦对最终所得的测试结果满意，我便会删除或注释掉这些合理的测试代码。这是一种巨大的资源浪费，因为这些测试完全可以构成对系统进行详尽测试的基础。Phpunitf 便是一个可以对系统进行全面测试的工具。

### 5.3 Introducing PHPUnit

PHPUnit is a member of the xUnit family of testing tools. The ancestor of these is SUnit, a framework invented by Kent Beck to test systems built with the Smalltalk language. The xUnit framework was probably established as a popular tool, however, by the Java implementation, jUnit, and by the rise to prominence of agile methodologies like Extreme Programming (XP) and Scrum, all of which place great emphasis on testing. You can get PHPUnit with Composer:

Once you have run composer install, you will find the phpunit script at vendor/bin/phpunit. Or, you can download a PHP archive (.phar) file. You can then make the archive executable:

```
$ wget https://phar.phpunit.de/phpunit.phar
$ chmod 755 phpunit.phar
$ sudo mv phpunit.phar/usr/local/bin/phpunit
```

1『 PHPUnit 安装这块内容还是去看 laravel 的官方文档和 PHPUnit 的官方文档。（2020-09-23）』

Note: I show commands that are input at the command line in bold to distinguish them from any output  they may produce.

#### 5.3.1 Creating a Test Case

Armed with PHPUnit, I can write tests for the UserStore class. Tests for each target component should be collected in a single class that extends `PHPUnit_Framework_TestCase`, one of the classes made available by the PHPUnit package. Here’s how to create a minimal test case class:

```php
// listing 18.05namespace popp\ch18\batch01;

class UserStoreTest extends \PHPUnit_Framework_TestCase{

    public function setUp()    {    }

    public function tearDown()    {    }

// ...}
```

1『在 laravel 里直接用命令新建单元测试：php artisan make:test UserStoreTest --unit。』

I named the test case class UserStoreTest. You are not obliged to use the name of the class you are testing in the test’s name, although that is what many developers do. Naming conventions of this kind can greatly improve the accessibility of a test harness, especially as the number of components and tests in the system begins to increase. It is often useful to place your test in the same namespace as the class under test. This will give you easy access to the class under test and its peers, and the structure of your test files will likely mirror that of your system. Remember that, thanks to Composer’s support for PSR-4, you can maintain separate directory structures for class files in the same package.

在软件测试中，测试用具是指一个包含了软件和测试数据的集合，用以测试一个程序单元，使之在不同的条件下运行，并监控它的行为和输出。测试用具应该包含测试环境的搭建和清理，选择运行单个测试或者所有测试的方法，分析输出结果的手段以及错误的标准报告等——译者注

In this code, I have nominated two directories that map to the popp namespace. I can now maintain these in parallel, making it easy to keep my test and production code separate.

Each test in a test case class is run in isolation from its siblings. The setUp() method is automatically invoked for each test method, allowing us to set up a stable and suitably primed environment for the test. tearDown() is invoked after each test method is run. If your tests change the wider environment of your system, you can use this method to reset state. The common platform managed by setUp() and tearDown() is known as a fixture. In order to test the UserStore class, I need an instance of it. I can instantiate this in setUp() and assign it to a property. Let’s create a test method as well:

```php
<?php

namespace Tests\Unit;

use App\Code\UserStore;
use PHPUnit\Framework\TestCase;

class UserStoreTest extends TestCase
{
    protected $store;

    protected function setUp(): void {
        parent::setUp();
        $this->store = new UserStore();
    }
    
    /**
     * A basic unit test example.
     *
     * @return void
     */
    public function testGetUser() {
        $this->store->addUser('bob williams', 'a@b.com', '12345');
        $user = $this->store->getUser('a@b.com');
        $this->assertEquals('a@b.com', $user['mail']);
        $this->assertEquals('bob williams', $user['name']);
        $this->assertEquals('12345', $user['pass']);
    }

    public function testAddUserShortPass() {
        try {
            $this->store->addUser('bob williams', 'bob@example.com', 'ff');
        } catch (\Exception $e) {
            return;
        }
        $this->fail('Short password exception expected');
    }
}
```

1『

遇到好几个问题：

1、5.8 版本以上要求 setUp、tearDown 的返回类型为 void，最终的代码如下：

```php
public function setUp(): void {
    parent::setUp();
    $this->store = new UserStore();
}
```

2、成员变量识别不出，无法自动补全。

发现在 setUp() 函数里定义成员变量，\$this->store = new UserStore()，\$store 在其他函数里是无法识别自动补全其内部方法的，去官网「[4. Fixtures — PHPUnit 9.2 Manual](https://phpunit.readthedocs.io/en/9.2/fixtures.html?highlight=setUp)」看了示例，发现语法没问题，应该只是 laravel 里显示的问题，不影响使用的。

』

Note: remember that setUp() and tearDown() are called once for every test method in your class.

Note: Test methods should be named to begin with the word「test」and should require no arguments. This is because the test case class is manipulated using reflection. reflection is covered in detail in Chapter 5.

2『上面解释了为啥测试类的命名需要以 test 开头，这里还有一个关键点：测试函数不能入参，做一张任意卡片。』——已完成

The object that runs the tests looks at all the methods in the class and invokes only those that match this pattern (that is, methods that begin with「test」). In the example, I tested the retrieval of user information. I don’t need to instantiate UserStore for each test because I handled that in setUp(). Because setUp() is invoked for each test, the \$store property is guaranteed to contain a newly instantiated object.

1『 setUp() 可以当作是一个公共方法，里面的代码实现在每个测试前都会实现一次，这样可以避免重复代码。真是无时无刻不体现「消除重复」代码的基本原则。』

Within the testgetUser() method, I first provide UserStore::addUser() with dummy data, and then I retrieve that data and test each of its elements.

There is one additional issue to be aware of here, before we can run our test. I am using use statements without require or require\_once. In other words, I am relying on autoloading. That’s fine, but where do I tell my tests how to locate the generated autoload.php file? I could put a require_once statement in the test class (or a superclass), but that would break the PSR-1 rule that class files should not have side effects. The simplest thing to do is to tell PHPUnit about the autoload.php file from the command line:

```
phpunit src/ch18/batch01/UserStoreTest.php --bootstrap vendor/autoload.php
```

1『

本来一直用命令 `./vendor/bin/phpunit` 跑全部的测试。试了下 brew 竟然可以安装 phpunit，哈哈。借鉴上面的信息，再结合 PHPunit 官网文档，可以直接用 phpunit 命令加类文件名，只跑这个文件里的测试。比如：`phpunit tests/Unit/UserStoreTest.php`，在项目根目录下直接用命令 `phpunit` 可以跑项目里的所有测试用例。但目前实验发现 phpunit 命令直接跑比老方法跑规则更严（老方法能跑通但新方法跑不通，报错），意外的大收获。（2020-09-23）

数据流项目直接跑的话，报错：

```
HP Fatal error:  Declaration of Illuminate\Foundation\Testing\TestCase::setUp() must be compatible with PHPUnit\Framework\TestCase::setUp(): void in
```

发现就是版本不兼容的问题。首先用 `php artisan` 查看项目的 laravel 版本号是 5.6.40。接着查看 `composer.json` 里，phpunit 版本是 7.0 的，说明 phpunit 7.0 和 laravel 5.6 是兼容的，但 brew 安装的 phpunit 是 9.3 的，跟 laravel 5.6 不兼容。最后查了下本书的项目版本号是 laravel 6.18，说明跟 phpunit 9.3 是兼容的。（2020-09-24）

』

#### 5.3.2 Assertion Methods

An assertion in programming is a statement or method that allows you to check your assumptions about an aspect of your system. In using an assertion, you typically define an expectation that something is the case, that \$cheese is "blue" or \$pie is "apple". If your expectation is confounded, a warning of some kind will be generated. Assertions are such a good way of adding safety to a system that PHP supports them natively inline and allows you to turn them off in a production context.

Note: see the manual page at http://php.net/assert for more information on php’s support for assertions.

PHPUnit supports assertions through a set of static methods. In the previous example, I used an inherited static method, assertEquals(). This method compares its two provided arguments and checks them for equivalence. If they do not match, the test method will be chalked up as a failed test. Having subclassed PHPUnit\_Framework\_TestCase, I have access to a set of assertion methods. Some of these methods are listed in Table 18-1.

Table 18-1.  PHPUnit_Framework_TestCase Assert Methods

| 断言 | 描述 |
| --- | --- |
| `assertEquals($val1, $val2, $message, $delta)` | `Fail if $val1 is not equivalent to $val2 ($delta represents an allowable margin of error)` |
| `assertFalse($expression, $message)` | `Evaluate $expression; fail if it does not resolve to false` |
| `assertTrue($expression, $message)` | `Evaluate $expression; fail if it does not resolve to true` |
| `assertNotNull($val, $message)` | `Fail if $val is null` |
| `assertNull($val, $message)` | `Fail if $val is anything other than null` |
| `assertSame($val1, $val2, $message)` | `Fail if $val1 and $val2 are not references to the same object, or if they are variables of different types or values` |
| `assertNotSame($val1, $val2, $message)` | `Fail if $val1 and $val2 are references to the same object or variables of the same type and value` |
| `assertRegExp($regexp, $val, $message)` | `Fail if $val is not matched by the regular expression, $regexp` |
| `assertAttributeSame($val, $attribute, $classname, $message)` | `Fail if $val is not the same type and value as $classname::$attribute` |
| fail() | Fail |

1『 fail() 是使测试方法直接返回失败。』

#### 5.3.3 Testing Exceptions

Your focus as a coder is usually to make stuff work and work well. Often, that mentality carries through to testing, especially if you are testing your own code. The temptation is to test that a method behaves as advertised. It’s easy to forget how important it is to test for failure. How good is a method’s error checking? Does it throw an exception when it should? Does it throw the right exception? Does it clean up after an error if, for example, an operation is half complete before the problem occurs? It is your role as a tester to check all of this. Luckily, PHPUnit can help.

开发者通常希望代码可用并运行良好。这种心理经常会贯彻到测试中，特别是在测试自己写的代码时。这时存在一个诱惑，就是只测试方法是否正常工作，而很容易忘掉对方法失败进行测试的重要性。比如一个方法的错误检査是否完善？当它应该抛出异常时会不会抛出异常？它是否能抛出正确的异常？在问题发生前只执行了一半的操作，在错误发生后是否会进行清理？作为一个测试者，你的任务就是检査所有这些情况。幸好 PHPUnit 可以帮助你。

Here is a test that checks the behavior of the UserStore class when an operation fails:

```php
public function testAddUserShortPass() {
    try {
        $this->store->addUser('bob williams', 'bob@example.com', 'ff');
    } catch (\Exception $e) {
        return;
    }
    $this->fail('Short password exception expected');
}
```

If you look back at the UserStore::addUser() method, you will see that I throw an exception if the user’s password is less than five characters long. My test attempts to confirm this. I add a user with an illegal password in a try clause. If the expected exception is thrown, then flow skips to the catch clause, and all is well. If the addUser() method does not throw an exception as expected, the execution flow reaches the fail() method call.

Another way to test that an exception is thrown is to use an assertion method called expectException(), which requires the name of the exception type you expect to be thrown (either Exception or a subclass). If the test method exits without the correct exception having been thrown, the test will fail.

Note: the expectedException() method was added in php 5.2.0.

Here’s a quick reimplementation of the previous test:

```php
// listing 18.06namespace popp\ch18\batch02;

class UserStoreTest extends \PHPUnit_Framework_TestCase {    
    private $store;

    public function setUp() {        
        $this->store = new UserStore();    
    }

    public function testAddUserShortPass() {        
    $this->expectException('\\Exception');        
    $this->store->addUser("bob williams", "a@b.com", "ff");        
    $this->fail("Short password exception expected");    
    }
}
```

#### 5.3.4 Running Test Suites

If I am testing the UserStore class, I should also test Validator. Here is a cut-down version of a class called ValidateTest that tests the Validator::validateUser() method:

```php
<?php

namespace Tests\Unit;

use App\Code\UserStore;
use App\Code\Validator;
use PHPUnit\Framework\TestCase;

class ValidatorTest extends TestCase
{
    private $validator;

    public function setUp(): void {
        parent::setUp();
        $store = new UserStore();
        $store->addUser('bob williams', 'bob@example.com', '12345');
        $this->validator = new Validator($store);

    }
    /**
     * A basic unit test example.
     *
     * @return void
     */
    public function testValidateCorrectPass()
    {
        $this->assertTrue(
            $this->validator->validateUser('bob@example.com', '12345'),
            'Expecting successful validation'
        );
    }
}
```

#### 5.3.5 Constraints

In most circumstances, you will use off-the-peg assertions in your tests. In fact, at a stretch you can achieve an awful lot with AssertTrue() alone. As of PHPUnit 3.0, however, PHPUnit\_Framework\_TestCase included a set of factory methods that return PHPUnit\_Framework\_Constraint objects. You can combine these and pass them to PHPUnit\_Framework\_TestCase::AssertThat() in order to construct your own assertions.

1『自定义测试函数嘛，太赞了！』

在大多数情况下，你会在测试时使用 PHPUnit 中现成的断言。而事实上，你只要通过 AssertTrue() 方法就可完成很多测试工作。但在 Phpunit 3.0 以后，PHPUnit\_Framework\_TestCase 包含了一套返回 PHPUnit\_Framework\_Constraint 对象的工厂方法。你可以合并这些对象并将其传给 PHPUnit\_Framework\_TestCase::AssertThat() 来构造你自己的断言。

It’s time for a quick example. The UserStore object should not allow duplicate e-mail addresses to be added. Here’s a test that confirms this:

```php
public function testAddUserDuplicate() {
    try {
        $ret = $this->store->addUser('bob williams', 'a@b.com', '12345');
        $ret = $this->store->addUser('bob stevens', 'a@b.com', '12345');
        self::fail('Exception should have been thrown');
    } catch (\Exception $e) {
        $const = $this->logicalAnd(
            $this->logicalNot($this->contains('bob stevens')),
            $this->isType('array')
        );
        self::assertThat($this->store->getUser('a@b.com'), $const);
    }
}
```

1『小插曲，`$this->contains` 已经被废弃了，改用新的 `$this->containsEquial`。（2020-09-24）』

This test adds a user to the UserStore object and then adds a second user with the same e-mail address. The test thereby confirms that an exception is thrown with the second call to addUser(). In the catch clause, I build a constraint object using the convenience methods available to us. These return corresponding instances of PHPUnit\_Framework\_Constraint. Let’s break down the composite constraint in the previous example:

```php
$this->contains("bob stevens")
```

This returns a `PHPUnit_Framework_Constraint_TraversableContains` object. When passed to AssertThat, this object will generate an error if the test subject does not contain an element matching the given value ("bob stevens"). I negate this, though, by passing this constraint to another: PHPUnit\_Framework\_Constraint\_Not. Once again, I use a convenience method, available through the TestCase class (actually through a superclass, Assert):

```php
$this->logicalNot( $this->contains("bob stevens"))
```

Now, the AssertThat assertion will fail if the test value (which must be traversable) contains an element that matches the string, "bob stevens". In this way, you can build up quite complex logical structures. By the time I have finished, my constraint can be summarized as follows: 'Do not fail if the test value is an array and does not contain the string "bob stevens".' You could build much more involved constraints in this way. The constraint is run against a value by passing both to AssertThat().

You could achieve all this with standard assertion methods, of course, but constraints have a couple of virtues. First, they form nice logical blocks with clear relationships among components (although good use of formatting may be necessary to support clarity). Second, and more important, a constraint is reusable. You can set up a library of complex constraints and use them in different tests. You can even combine complex constraints with one another:

```php
$const = $this->logicalAnd(    
    $a_complex_constraint,    
    $another_complex_constraint
);
```

2『测试中约束的优点做一张任意卡片。组合约束条件形成更复杂的自定义断言函数，而且可以层层组合，这个功能为例巨大。（2020-09-24）』——已完成

3『

phpunit 文档中：[1. Assertions — PHPUnit 9.2 Manual](https://phpunit.readthedocs.io/en/9.2/assertions.html#assertthat)

`assertThat()`, More complex assertions can be formulated using the `PHPUnit\Framework\Constraint` classes. They can be evaluated using the assertThat() method. Example 1.59 shows how the logicalNot() and equalTo() constraints can be used to express the same assertion as assertNotEquals().

```
assertThat(mixed $value, PHPUnit\Framework\Constraint $constraint[, $message = ''])
```

Reports an error identified by `$message` if the `$value` does not match the `$constraint`.

```php
<?php
use PHPUnit\Framework\TestCase;

class BiscuitTest extends TestCase
{
    public function testEquals()
    {
        $theBiscuit = new Biscuit('Ginger');
        $myBiscuit  = new Biscuit('Ginger');

        $this->assertThat(
          $theBiscuit,
          $this->logicalNot(
            $this->equalTo($myBiscuit)
          )
        );
    }
}
?>
```

』

#### 5.3.6 Mocks and Stubs

Unit tests aim to test a component in isolation of the system that contains it to the greatest possible extent. Few components exist in a vacuum, however. Even nicely decoupled classes require access to other objects as methods arguments. Many classes also work directly with databases or the filesystem.

You have already seen one way of dealing with this. The setUp() and tearDown() methods can be used to manage a fixture (i.e., a common set of resources for your tests, which might include database connections, configured objects, a scratch area on the file system, etc.)

单元测试的目标就是尽可能在不受外部环境影响的条件下测试系统中的组件。但是只有极少数组件以这样的真空形式存在。甚至与外部耦合非常小的类也需要访问其他对象，例如以其他对象作为类方法参数。许多类也直接与数据库或文件系统一起工作。我们已经看到过处理这个问题的一种办法。我们可以利用 setup() 和 teardown() 方法来管理测试装置。测试装置就是一组供测试使用的公用资源，可能包含数据库连接、配置对象、文件系统的暂存区域等。

Another approach is to fake the context of the class you are testing. This involves creating objects that pretend to be the objects that do real stuff. For example, you might pass a fake database mapper to your test object’s constructor. Because this fake object shares a type with the real mapper class (extends from a common abstract base or even overrides the genuine class itself), your subject is none the wiser. You can prime the fake object with valid data. Objects that provide a sandbox of this sort for unit tests are known as stubs. They can be useful because they allow you to focus in on the class you want to test without inadvertently testing the entire edifice of your system at the same time.

Fake objects can be taken a stage further than this, however. Because the object you are testing is likely to call a fake object in some way, you can prime it to confirm the invocations you are expecting. Using a fake object as a spy in this way is known as behavior verification, and it is what distinguishes a mock object from a stub.

1-2『哈哈，大赞，解耦测试有 2 个方式：1）把构建对象、数据库连接、文件系统的暂存区，都放到测试的前置、后置里。2）模拟测试类的环境，即 mock 对象（只需模拟对象的行为，数据不用模拟）。mock 对象和 stub 对象做一张术语卡片。（2020-09-24）』——已完成

另一种方式就是伪造测试类的环境。该方式会创建假装在进行真实工作的对象。例如，你可能会传一个伪造的数据库映射给测试对象的构造函数。因为伪造对象和真实的映射类（继承自一个共同的抽象基类或甚至重写该类本身）是相同类型，所以测试目标对此一无所知。你可以预先准备好具有正确数据的虚拟对象（fake object）。这类为单元测试提供沙箱的对象就是所谓的桩。它们非常有用，因为它们使你能仅关注于要测试的类本身而无需同时注意整个系统。

但虚拟对象的功能还不止于此。因为你所测试的对象可能会以某种方式调用虚拟对象，所以你可以准备好虚拟对象以便它按照预期那样确保调用可以进行。以这种类似间谍的方式使用虚拟对象被称为「行为确认」。对于对象行为的预期正是 mock 对象与 stub 对象不同的地方。

Stub，可理解为占位用的假对象。简单地说，stub 只是占位，而 mock 对象还关注于对行为的预期，这是两者的区别。如果读者想了解更多内容，建议阅读 Martin Fowler 的 Mocks Aren't Stubs 一文。一一译者注

2-3『

Martin Fowler 博客里的文章：[Mocks Aren't Stubs](https://martinfowler.com/articles/mocksArentStubs.html)

消化吸收并作为本书的一个附件。

』

You can build mocks yourself by creating classes hard-coded to return certain values and to report on method invocations. This is a simple process, but it can be time-consuming.

PHPUnit provides access to an easier and more dynamic solution. It will generate mock objects on the fly for you. It does this by examining the class you wish to mock and building a child class that overrides its methods. Once you have this mock instance, you can call methods on it to prime it with data and to set the conditions for success.

Let’s build an example. The UserStore class contains a method called notifyPasswordFailure(), which sets a field for a given user. This should be called by Validator when an attempt to set a password fails. Here, I mock up the UserStore class so that it both provides data to the Validator object and confirms that its notifyPasswordFailure() method was called as expected:

创建 mock 对象的办法有两种。首先，你可以自己创建相应的类来确保返回特定的值，以供方法调用。这是一个简单的过程，但需要花费一些时间。Phpunit 提供了另一个更为易用和动态的解决方案。它会为你在运行时自动生成 mock 对象。PHPUnit 会检査你想要模拟的对象并创建一个重写该对象方法的子类。一旦有了 mock 对象的实例，你就可以调用其中的方法来准备数据或设定测试成功的条件。

下面举个例子。UserStore 类包含了一个 notifyPasswordFailure() 方法，该方法会设定特定用户的密码字段。当尝试设置密码失败时，该方法就会被 Validator 调用。下面的例子创建了 UserStore 类的 mock 对象，以便它能为 Validator 对象提供数据及确认 notifyPasswordFailure() 方法如预期地被调用：

```php
// listing 18.09

public function testValidateFalsePass() {
    $store = $this->getMockBuilder(UserStore::class)->getMock();
    $this->validator = new Validator($store);

    $store->expects($this->once())
        ->method('notifyPasswordFailure')
        ->with($this->equalTo('bob@example.com'));

    $store->expects($this->any())
        ->method('getUser')
        ->with($this->returnValue([
            'name' => 'bob williams',
            'mail' => 'bob@example.com',
            'pass' => 'right'
        ]));
    
    $this->validator->validateUser('bob@example.com', 'wrong');
}
```

1『

遇到了一些问题，也解决了一些问题，但最终还是没有实现「原书」里的测试。

getMock() 方法废弃了。

[php - phpunit mock - method does not exist - Stack Overflow](https://stackoverflow.com/questions/39601142/phpunit-mock-method-does-not-exist)

`PHPUnit\_Framework\_TestCase::getMockBuilder()` only takes one (1) argument, the class name. The methods to mock are ment to be defined via the returned mock builder objects setMethods() method.

```php
$stub = $this
    ->getMockBuilder('SomeClass')
    ->setMethods(['execute'])
    ->getMock();

// 改善
$stub = $this->getMockBuilder(SomeClass::class)->getMock();
```

有时间好好看下官方文档：[Test Doubles — PHPUnit 9.2 Manual](https://phpunit.readthedocs.io/en/9.2/test-doubles.html#stubs)

』

Mock objects use a fluent interface; that is, they have a language-like structure. These are much easier to use than to describe. Such constructs work from left to right, each invocation returning an object reference, which can then be invoked with a further modifying method call (itself returning an object). This can make for easy use, but painful debugging.

Mock 对象使用了类似于语言的流畅接口。使用这样的语言结构，调用从左到右进行，每次调用都返回对一个对象的引用，而该对象的引用可被后面的方法（仍会返回对象）继续调用。这样编写代码很简单，但调试的时候会有点麻烦。

语言的流畅接口，指的是 PHP5 中可以使用多个 -> 符号连续调用对象方法。这里 Store、expects、method、wih 连起来就像一句话，所以称为「类似于语言」。——译者注

In the previous example, I called the PHPUnit\_Framework\_TestCase method: getMock(), passing it "UserStore", the name of the class I wish to mock. This dynamically generates a class and instantiates an object from it. I store this mock object in \$store and pass it to Validator. This causes no error because the object’s newly minted class extends UserStore. I have fooled Validator into accepting a spy into its midst.

Mock objects generated by PHPUnit have an expects() method. This method requires a matcher object (actually it’s of type PHPUnit\_Framework\_MockObject\_Matcher\_Invocation, but don’t worry; you can use the convenience methods in TestCase to generate your matcher). The matcher defines the cardinality of the expectation; that is, it dictates the number of times a method should be called.

上面的范例调用了 PHPUnit\_Framework\_TestCase 的 getMock() 方法，并将要模拟的类名 UserStore 传给它。该方法会动态生成一个类，并为该类实例化一个对象。mock 对象被保存在 store 中并被传给 Validator。这样做不会引起错误，因为该对象来源于 UserStore 的子类。这样我们欺骗了 Validator，使之接受了一个间谍。

由 PHPUnit 生成的 mock 对象有一个 expects() 方法。该方法要求一个匹配对象（它实际上是 PHPUnit\_Framework\_MockObject\_Matcher\_Invocation 类型。你不需要知道其确切类型，就可以在 TestCase 中使用便捷方法来生成匹配对象作为参数。匹配对象定义了期望的基数，即个方法应该被调用的次数。

Table 18-3 shows the matcher methods available in a TestCase class.

| methods | descripe |
| --- | --- |
| any() | Zero or more calls are made to the corresponding method (useful for stub objects that return values, but don’t test invocations) |
| never() | No calls are made to the corresponding method |
| atLeastOnce() | One or more calls are made to the corresponding method |
| once() | A single call is made to the corresponding method |
| exactly(`$num`) | `$num `calls are made to the corresponding method |
| at(`$num`) | A call to the corresponding method made at `$num` index (each method call to a mock is recorded and indexed) |

Having set up the match requirement, I need to specify a method to which it applies. For instance, expects() returns an object (PHPUnit\_Framework\_MockObject\_Builder\_InvocationMocker, if you must know) that has a method called method(). I can simply call that with a method name. This is enough to get some real mocking done:

```php
$store = $this->getMock("UserStore");
$store->expects($this->once())    
    ->method('notifyPasswordFailure');
```

I need to go further, however, and check the parameters that are passed to notifyPasswordFailure(). The InvocationMocker::method() returns an instance of the object it was called on. InvocationMocker includes a method name, with(), which accepts a variable list of parameters to match. It also accepts constraint objects, so you can test ranges and so on. Armed with this, you can complete the statement and ensure that the expected parameter is passed to notifyPasswordFailure():

```php
$store->expects($this->once())   
     ->method('notifyPasswordFailure')    
     ->with($this->equalTo('bob@example.com'));
```

You can see why this is known as a fluent interface. It reads a bit like a sentence:「The \$store object expects a single call to the notifyPasswordFailure() method with parameter bob@example.com.」

Notice that I passed a constraint to with(). Actually, that’s redundant; any bare arguments are converted to constraints internally, so I could write the statement like this:

```php
$store->expects($this->once())    ->method('notifyPasswordFailure')    ->with('bob@example.com');
```

Sometimes, you only want to use PHPUnit’s mocks as stubs; that is, as objects that return values to allow your tests to run. In such cases, you can invoke InvocationMocker::will() from the call to method(). The will() method requires the return value (or values if the method is to be called repeatedly) that the associated method should be primed to return. You can pass in this return value by calling either TestCase::returnValue() or TestCase::onConsecutiveCalls(). Once again, this is much easier to do than to describe. Here’s the fragment from my earlier example in which I prime UserStore to return a value:

```php
$store->expects($this->any())    
    ->method("getUser")
    ->will($this->returnValue([        
        "name" => "bob williams",        
        "mail" => "bob@example.com",        
        "pass" => "right"    
    ]));
```

I prime the UserStore mock to expect any number of calls to getUser(). Right now, I’m concerned with providing data, not with testing calls. Next, I call will() with the result of invoking TestCase::returnValue() with the data I want returned (this happens to be a PHPUnit\_Framework\_MockObject\_Stub\_Return object, although if I were you, I’d just remember the convenience method you use to get it).

You can alternatively pass the result of a call to TestCase::onConsecutiveCalls() to will(). This accepts any number of parameters, each one of which will be returned by your mocked method as it is called repeatedly.

#### 5.3.7 Tests Succeed When They Fail

Although most agree that testing is a fine thing, you grow to really love it generally only after it has saved your bacon a few times. Let’s simulate a situation where a change in one part of a system has an unexpected effect elsewhere.

The UserStore class has been running for a while when, during a code review, it is agreed that it would be neater for the class to generate User objects rather than associative arrays. Here is the new version:

```php
// listing 18.10

namespace popp\ch18\batch03;

class UserStore {    
    private $users = [];

    public function addUser(string $name, string $mail, string $pass)    {       
     if (isset($this->users[$mail])) {            
        throw new \Exception (                
            "User {$mail} already in the system"            
        );        
     }
        $this->users[$mail] = new User($name, $mail, $pass);
        return true;    
    }

    public function notifyPasswordFailure(string $mail)    {        
        if (isset($this->users[$mail])) {            
            $this->users[$mail]->failed(time());        
        }
    }

    public function getUser(string $mail) {        
        if (isset($this->users[$mail])) {            
            return ( $this->users[$mail] );        
        }
        return null;    }}
```

Here is the simple User class:

```php
// listing 18.11

namespace popp\ch18\batch03;

class Use r{    
    private $name;    
    private $mail;    
    private $pass;    
    private $failed;

    public function __construct(string $name, string $mail, string $pass)    {        
        $this->name = $name;        
        $this->mail = $mail;

        if (strlen($pass) < 5) {            
            throw new \Exception (                
                "Password must have 5 or more letters"            
            );        
        }
        $this->pass = $pass;    
    }

    public function getMail(): string    {        
        return $this->mail;    
    }

    public function getPass(): string    {        
        return $this->pass;    
    }

    public function failed(string $time)    {        
        $this->failed = $time;    
    }
}
```

Of course, I amend the UserStoreTest class to account for these changes. Consider this code designed to work with an array:

```php
public function testGetUser(){    $this->store->addUser("bob williams", "a@b.com", "12345");    $user = $this->store->getUser("a@b.com");    $this->assertEquals($user['mail'], "a@b.com");    //...
```

It is now converted into code designed to work with an object, like this:

```php
public function testGetUser() {    
    $this->store->addUser("bob williams", "a@b.com", "12345");    
    $user = $this->store->getUser("a@b.com");    
    $this->assertEquals($user->getMail(), "a@b.com");
}
```

When I come to run my test suite, however, I am rewarded with a warning that my work is not yet done:

I invoke getUser(). Although getUser() now returns an object and not an array, my method does not generate a warning. getUser() originally returned the requested user array on success or null on failure, so I validated users by checking for an array using the is\_array() function. Now, of course, getUser() returns an object, and the validateUser() method will always return false. Without the test framework, the Validator would have simply rejected all users as invalid without fuss or warning.

Now, imagine making this neat little change on a Friday night without a test framework in place. Think about the frantic text messages that would drag you out of your pub, armchair, or restaurant:「What have you done? All our customers are locked out!」

The most insidious bugs don’t cause the interpreter to report that something is wrong. They hide in perfectly legal code, and they silently break the logic of your system. Many bugs don’t manifest themselves where you are working; they are caused there, but the effects pop up elsewhere, days or even weeks later. A test framework can help you catch at least some of these, preventing rather than discovering problems in your systems.

Write tests as you code, and run them often. If someone reports a bug, first add a test to your framework to confirm it. Next, fix the bug so that the test is passed. Bugs have a funny habit of recurring in the same area. Writing tests to prove bugs and then to guard the fix against subsequent problems is known as regression testing. Incidentally, if you keep a separate directory of regression tests, remember to name your files descriptively. On one project, our team decided to name our regression tests after Bugzilla ticket numbers. We ended up with a directory containing 400 test files, each with a name like test_973892.php. Finding an individual test became a tedious chore!

### 5.4 Writing Web Tests

You should engineer your web systems in such a way that they can be invoked easily from the command line or an API call. In Chapter 12, you saw some tricks that might help you with this. In particular, if you create a Request class to encapsulate an HTTP request, you can just as easily populate an instance from the command line or method argument lists as from request parameters. The system can then run in ignorance of its context.

If you find a system hard to run in different contexts, that may indicate a design issue. If, for example, you have numerous filepaths hard-coded into components, it’s likely you are suffering from tight coupling. You should consider moving elements that tie your components to their context into encapsulating objects that can be acquired from a central repository. The registry pattern, also covered in Chapter 12, will likely help you with this.

你的 Web 系统应该设计成这样：通过命令行或 API 调用可以轻松地调用。第 12 章介绍了一些这方面的技巧。尤其是，如果创建 Request 类来封装 HTTP 请求，你可以通过请求参数填充实例，就像根据命令行或方法参数列表来填充实例一样简单。该系统随后会在不清楚上下文的状态下运行。

如果你的 Web 系统很难在不同的上下文中运行，就说明设计可能有问题。例如，如果你将很多文件路径硬编码到了组件中，就可能导致紧密耦合。你应该考虑将造成组件与上下文耦合的元素移动到封装对象中，然后通过中心代码封装对象。第 12 章中介绍的注册表模式可以帮助你实现这一过程。

Once your system can be run directly from a method call, you’ll find that high-level web tests are relatively easy to write without any additional tools. You may find, however, that even the most well-thought-out project will need some refactoring to get things ready for testing. In my experience, this almost always results in design improvements. I’m going to demonstrate this by retrofitting one aspect of the WOO example from Chapters 12 and 13 for unit testing.

一旦 Web 系统可以直接通过方法调用运行，你会发现在不使用其他工具的情况下，高层次的 Web 测试相对会更容易编写。但是，即使是经过深思熟虑之后开发出来的项目，恐怕也需要经过重构才能具备测试条件。以我的编程经验来看，这通常会改进设计。我打算改进第 12 章和第 13 章的 WOO 示例的一个方面来进行单元测试，以此说明这一过程。
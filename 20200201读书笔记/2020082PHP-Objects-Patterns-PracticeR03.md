# 2020082PHP-Objects-Patterns-PracticeR03

## 记忆时间

## 0305. Testing with PHPUnit

In this chapter, I revisited the kinds of tests we all write as developers, but all too often thoughtlessly discard. From there, I introduced PHPUnit, which lets you write the same kind of throwaway tests during development, but then keep them and feel the lasting benefit! I created a test-case implementation, and I covered the available assertion methods. I also examined constraints and explored the devious world of mock objects. Next, I showed how refactoring for testing can improve design, demonstrating some techniques for testing web applications—first by using just PHPUnit, and then by using Selenium. Finally, I risked the ire of some by warning of the costs that tests incur and discussing the trade-offs involved.

Every component in a system depends for its continued smooth running on the consistency of operation and interface of its peers. By definition, then, development breaks systems. As you improve your classes and packages, you must remember to amend any code that works with them. For some changes, this can create a ripple effect, affecting components far away from the code you originally changed. Eagle-eyed vigilance and an encyclopedic knowledge of a system’s dependencies can help to address this problem. Of course, while these are excellent virtues, systems soon grow too complex for every unwanted effect to be easily predicted, not least because systems often combine the work of many developers. To address this problem, it is a good idea to test every component regularly. This, of course, is a repetitive and complex task; and as such, it lends itself well to automation.

Among the test solutions available to PHP programmers, PHPUnit is perhaps the most ubiquitous and certainly the most fully featured tool. In this chapter, you will learn the following about PHPUnit: 1) Installation: Using PEAR to install PHPUnit. 2) Writing Tests: Creating test cases and using assertion methods. 3) Handling Exceptions: Strategies for confirming failure. 4) Running multiple tests: Collecting tests into suites. 5) Constructing assertion logic: Using constraints. 6) Faking components: Mocks and stubs. 7) Testing web applications: Testing with and without additional tools.

### 5.1 Functional Tests and Unit Tests

Testing is essential in any project. Even if you don’t formalize the process, you must have found yourself developing informal lists of actions that put your system through its paces. This process soon becomes wearisome, and that can lead to a fingers-crossed attitude to your projects.

One approach to testing starts at the interface of a project, modeling the various ways in which a user might negotiate the system. This is probably the way you would go when testing by hand, although there are various frameworks for automating the process. These functional tests are sometimes called acceptance tests because a list of actions performed successfully can be used as criteria for signing off a project phase. Using this approach, you typically treat the system as a black box—your tests remain willfully ignorant of the hidden components that collaborate to form the system under test.

测试在任何项目中都是一个基本要素。即使你的测试流程并不规范，也一定使用了一系列确认系统是否正常工作的操作。这种不规范的测试流程很快就会变得乏味，并且会逐渐让人形成种撞大运的心态。有一种测试方法是从一个项目的接口开始，为用户可能使用系统的各种方式建模。而这也是手工测试时通常会使用的方式，虽然也有众多的框架可以自动化该过程。这些功能测试有时又被称为验收测试（acceptance test），因为一个成功执行的动作列表可以作为一个项目阶段完成的依据。使用该方法时，通常会把系统看做一个黑盒一一测试只针对产品功能，并不关注项目内部结构和处理过程。

Whereas functional tests operate from without, unit tests work from the inside out. Unit testing tends to focus on classes, with test methods grouped together in test cases. Each test case puts one class through a rigorous workout, checking that each method performs as advertised and fails as it should. The objective, as far as possible, is to test each component in isolation from its wider context. This often supplies you with a sobering verdict on the success of your mission to decouple the parts of your system.

Tests can be run as part of the build process, directly from the command line, or even via a web page. In this chapter, I’ll concentrate on the command line.

Unit testing is a good way of ensuring the quality of design in a system. Tests reveal the responsibilities of classes and functions. Some programmers even advocate a test-first approach. You should, they say, write the tests before you even begin work on a class. This lays down a class’s purpose, ensuring a clean interface and short, focused methods. Personally, I have never aspired to this level of purity—it just doesn’t suit my style of coding. Nevertheless, I attempt to write tests as I go. Maintaining a test harness provides me with the security I need to refactor my code. I can pull down and replace entire packages with the knowledge that I have a good chance of catching unexpected errors elsewhere in the system.

功能测试从外部着手，而单元测试（本章的主题）则从内部着手。单元测试更加关注于类，并将测试方法组合到测试用例中。每个测试用例通过严格的检测来处理一个类，检査每个方法是否如预期般成功执行或失败。单元测试的目标是尽可能地在隔离周边环境的情况下测试每个组件。只有隔离了周围环境的影响，才能发现被测试的组件与周边组件间的耦合是否真正被解开。测试可以作为项目构建过程的一部分，直接从命令行或者甚至通过一个网页来执行。本章主要采用命令行方式进行测试。

单元测试是保证系统设计质量的好办法。测试揭示了类和方法的职责。一些程序员甚至提倡测试先行（test-first）的开发方式。他们认为应该在写一个类之前先写好测试。测试设定了一个类的目的，保证了一个千净的接口和简短并集中的方法。我个人曾未渴望达到这样纯粹的程度——也许是因为这不符合我的编码风格。然而，我每前进一步都会努力写测试。测试给我提供了重构代码时的安全保障。因为我知道在系统的其他地方可以捕获非预期的错误，所以可以放心地删除或替换掉项目中的某个代码包。

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
        dd($user);
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


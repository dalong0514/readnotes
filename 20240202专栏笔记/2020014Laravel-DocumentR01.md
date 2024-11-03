## 记忆时间

## 卡片

### 0101. 主题卡——高频操作

1、查看当前项目的 laravel 版本号。直接命令 `php artisan`，最上面的信息有该项目的版本号。

### 0201. 术语卡——

根据反常识，再补充三个证据——就产生三张术语卡。

### 0202. 术语卡——

### 0203. 术语卡——

### 0301. 人名卡——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

### 0401. 金句卡——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 任意卡——

最后还有一张任意卡，记录个人阅读感想。

## 目录

1001Testing-Getting-Started.md

1006Mocking.md

2001HTTP-Responses.md

## 1001Testing-Getting-Started.md

[Testing: Getting Started - Laravel - The PHP Framework For Web Artisans](https://laravel.com/docs/7.x/testing)

### 1.1 Introduction

Laravel is built with testing in mind. In fact, support for testing with PHPUnit is included out of the box and a phpunit.xml file is already set up for your application. The framework also ships with convenient helper methods that allow you to expressively test your applications.

By default, your application's tests directory contains two directories: Feature and Unit. Unit tests are tests that focus on a very small, isolated portion of your code. In fact, most unit tests probably focus on a single method. Feature tests may test a larger portion of your code, including how several objects interact with each other or even a full HTTP request to a JSON endpoint.

An ExampleTest.php file is provided in both the Feature and Unit test directories. After installing a new Laravel application, run phpunit on the command line to run your tests.

1『

目前发现用 phpunit 找不到命令，只能使用「./vendor/bin/phpunit」才能跑。

解决方案：还未试验过（2020-06-17）

phpunit 版本问题，laravel 5.3 依赖 phpunit 5；laravel 5.5 依赖 phpunit 6，所以进行以下操作：

1、清理旧版本 phpunit，使用 composer global remove phpunit/phpunit

2、安装新版本 phpunit，使用 composer global require phpunit/phpunit ^6.2

』

### 1.2 Environment

When running tests via phpunit, Laravel will automatically set the configuration environment to testing because of the environment variables defined in the phpunit.xml file. Laravel also automatically configures the session and cache to the array driver while testing, meaning no session or cache data will be persisted while testing.

You are free to define other testing environment configuration values as necessary. The testing environment variables may be configured in the phpunit.xml file, but make sure to clear your configuration cache using the config:clear Artisan command before running your tests!

In addition, you may create a .env.testing file in the root of your project. This file will override the .env file when running PHPUnit tests or executing Artisan commands with the --env=testing option.

### 1.3 Creating & Running Tests

To create a new test case, use the make:test Artisan command:

```
// Create a test in the Feature directory...
php artisan make:test UserTest

// Create a test in the Unit directory...
php artisan make:test UserTest --unit
```

Once the test has been generated, you may define test methods as you normally would using PHPUnit. To run your tests, execute the phpunit or artisan test command from your terminal:

```php
<?php

namespace Tests\Unit;

use PHPUnit\Framework\TestCase;

class ExampleTest extends TestCase
{
    /**
     * A basic test example.
     *
     * @return void
     */
    public function testBasicTest()
    {
        $this->assertTrue(true);
    }
}
```

If you define your own setUp / tearDown methods within a test class, be sure to call the respective parent::setUp() / parent::tearDown() methods on the parent class.

1『

在看书籍「2020082PHP-Objects-Patterns-PracticeR00.md」恰巧实现了，而且当时还遇到一个问题：5.8 版本以上要求 setUp tearDown 的返回类型为 void，最终的代码如下：

```
public function setUp(): void {
    parent::setUp();
    $this->store = new UserStore();
}
```

』

### 1.4 Artisan Test Runner

In addition to the phpunit command, you may use the test Artisan command to run your tests. The Artisan test runner provides more information regarding the test that is currently running and will automatically stop on the first test failure:

```
php artisan test
```

Any arguments that can be passed to the phpunit command may also be passed to the Artisan test command:

```
php artisan test --group=feature
```

3『

PHPUnit 官网：

[Getting Started with Version 9 of PHPUnit – The PHP Testing Framework](https://phpunit.de/getting-started/phpunit-9.html)

[编写 PHPUnit 测试 — PHPUnit latest Manual](https://phpunit.readthedocs.io/zh_CN/latest/writing-tests-for-phpunit.html)

』

3『 [Laravel 测试： PHPUnit 入门教程 - 掘金](https://juejin.im/post/5c78dca0e51d451254334d1e)

介绍 PHPUnit 测试的基础知识，使用基本的 PHPUnit 断言和 Laravel 测试助手。

### 01. 介绍

PHPUnit 是最古老和最著名的 PHP 单元测试包之一。它主要用于单元测试，这意味着可以用尽可能小的组件测试代码，但是它也非常灵活，可以用于很多不仅仅是单元测试。PHPUnit 包含许多简单和灵活的断言允许您轻松地测试代码，当您测试特定的组件时，这些断言非常有效。但是，它确实意味着测试更高级的代码（如控制器和表单提交验证）可能会复杂得多。

为了帮助开发人员更容易地进行开发， Laravel 框架包含了一系列「应用程序测试帮助程序」 ，允许您编写非常简单的 PHPUnit 测试来测试应用程序的复杂部分。

本教程的目的是向您介绍 PHPUnit 测试的基础知识，使用默认 PHPUnit 断言和 Laravel 测试助手。这样做的目的是在本教程结束时，您可以自信地为应用程序编写基本测试。

### 02. 前提

本教程假设您已经熟悉 Laravel 并知道如何在应用程序目录中运行命令（例如 php artisan 命令）。我们将创建几个基本的示例类来学习不同的测试工具如何工作，因此建议您为本教程创建一个新的应用程序。如果已经安装了 Laravel ，则可以通过运行以下命令创建新的测试应用程序：

```
laravel new phpunit-tests
```

或者，您可以直接使用 Composer 创建新应用程序：

```
composer create-project laravel/laravel --prefer-dist
```

其他安装方法也可以在 Laravel 文档中找到。

### 03. 创建一个新的测试

使用 PHPUnit 的第一步是创建一个新的测试类。测试类的约定是它们存储在应用程序目录的 ./tests/ 下。在这个文件夹中，每个测试类都被命名为 <name>Test.php 。这种格式允许 PHPUnit 查找每个测试类——它将忽略任何不以 Test.php 结尾的文件。

在新的 Laravel 应用程序中，你会注意到 ./tests/ 目录中有两个文件：  ExampleTest.php 和 TestCase.php。TestCase.php 文件是一个引导文件用于在我们的测试中设置 Laravel 环境。这允许我们在测试中使用 Laravel Facades 并为测试助手提供框架，我们将在稍后介绍。 ExampleTest.php 是一个示例测试类，其中包含使用应用程序测试助手的基本测试用例（暂时忽略它）。

要创建一个新的测试类，我们可以手动创建一个新文件，或者运行由 Laravel 提供的 Artisan 命令 make:test

为了创建一个名为 BasicTest 的测试类，我们只需要运行这个 artisan 命令：

```
php artisan make:test BasicTest
```

Laravel 将创建一个如下所示的基本测试类：

```php
<?php
class BasicTest extends TestCase
{
    /**
	* 一个基本的测试示例。
	*
	* @return void
	*/
    public function testExample()
    {
        $this->assertTrue(true);
    }
}
```

这里要注意的最重要的事情是 test 方法名称上的前缀，与 Test 类名后缀一样，这样 test 前缀告诉 PHPUnit 在测试时运行哪些方法。如果您忘记了 test 前缀，那么 PHPUnit 将忽略该方法。在我们第一次运行测试套件之前，有必要指出 Laravel 提供的默认 phpunit.xml 文件。 PHPUnit 在运行时会自动在当前目录中查找名为 phpunit.xml 或者 phpunit.xml.dist 的文件。您可以在此处配置测试的特定选项。

这个文件中有很多信息，但是现在最重要的部分是在 testsuite 目录定义：

```html
<?xml version="1.0" encoding="UTF-8"?>
<phpunit ... >

    <testsuites>
        <testsuite name="Application Test Suite">
            <directory>./tests/</directory>
        </testsuite>
    </testsuites>

    ...
</phpunit>
```

这将告诉 PHPUnit 运行时在 ./tests/ 目录中找到的测试，正如我们之前所知，这是存储测试的约定。现在我们已经创建了一个基本测试，并且知道了 PHPUnit 配置，现在是第一次运行测试的时候了。

您可以通过运行以下 phpunit 命令来运行测试：

```
./vendor/bin/phpunit
```

您应该看到与此类似的输出：

```
PHPUnit 4.8.19 by Sebastian Bergmann and contributors.

..

Time: 103 ms, Memory: 12.75Mb

OK (2 tests, 3 assertions)
```

现在我们已经有了一个有效的 PHPUnit 设置，现在是时候开始编写一个基本测试了。

注意，它会统计 2 个测试和 3 个断言，因为 ExampleTest.php 文件包含了一个带有两个断言的测试。我们的新基本测试包括一个单独的断言，该断言已通过。

1『测试文件命名总结：1）测试文件名以 Test 结尾，比如 CalculateTest.php；2）测试类里的测试函数，以 test 开头，比如 public function testCalculate(){}。』

### 04. 写一个基础测试

为了帮助 PHPUnit 提供的基本断言,我们将首先创建一个提供一些简单功能的基本类。在 ./app/ 目录中创建一个名为 Box.php 的新文件，并复制此示例类：

```php
<?php
namespace App;

class Box {
    /** 
     * @var array
     */
    protected $items = [];

    /**
     * 使用给定项构造框
     * 
     * @param array $items
     */
    public function __construct($items = []) {
        $this->items = $items;
    }

    /**
     * 检查指定的项目是否在框内
     * 
     * @param string $item
     * @return bool
     */
    public function has($item) {
        return in_array($item, $this->items);
    }

    /**
     * 从框中移除项，如果框为空，则为 null
     * 
     * @return string
    */
    public function takeOne() {
        return array_shift($this->items);
    }

    /** 
     * 从包含指定字母开头的框内检索所有项目
     * 
     * @param string $letter
     * @return array
    */
    public function startWith($letter) {
        return array_filter($this->items, function($item) use ($letter) {
            return stripos($item, $letter) === 0;
        });
    }
}

?>
```

1『数组过滤函数 filter()，用 use 传递外部变量，这是一个很重要的知识点，之前没意识到。（2020-07-28）』

接下来， 打开你的 ./tests/BasicTest.php 类（我们之前创建的类），并删除默认创建的 testExample 方法， 你应该留一个空类。我们现在将使用七个基本的 PHPUnit 断言来为我们的 Box 类编写测试。这些断言是：

```php
assertTrue()
assertFalse()
assertEquals()
assertNull()
assertContains()
assertCount()
assertEmpty()
```

#### 4.1 assertTrue() 和 assertFalse()

assertTrue() 和 assertFalse() 允许你声明一个值等于 true 或 false 。这意味着它们非常适合测试返回布尔值的方法。在我们的 Box 类中，我们有一个名为 has(\$item) 的方法，当指定的项在 box 中或不在 box 中时，该方法返回对应返回 true 或 false。

要在 PHPUnit 中为此编写测试，我们可以执行以下操作：

```php
<?php

namespace Tests\Unit;

use PHPUnit\Framework\TestCase;
use App\Box;

class StackTest extends TestCase
{
    /**
     * A basic unit test example.
     *
     * @return void
     */
    public function testHasItemBox() {
        $box = new Box([
            'cat',
            'toy',
            'torch'
        ]);

        $this->assertTrue($box->has('toy'));
        $this->assertFalse($box->has('dalong'));
    }
}
```

注意我们如何只将一个参数传递给 assertTrue() 和 assertFalse() 方法，并且它是 has(\$item) 方法的输入。如果您现在运行 ./vendor/bin/phpunit 命令，您会注意到输出包括：

```
OK (2 tests, 4 assertions)
```

这意味着我们的测试已经通过。

如果您将 assertFalse() 替换成 assertTrue() 并运行 phpunit 命令，输出将如下所示：

```
PHPUnit 4.8.19 by Sebastian Bergmann and contributors.

F.

Time: 93 ms, Memory: 13.00Mb

There was 1 failure:

1) BasicTest::testHasItemInBox
Failed asserting that false is true.

./tests/BasicTest.php:12

FAILURES!
Tests: 2, Assertions: 4, Failures: 1.
```

这告诉我们第 12 行的断言未能断言 false 值是 true —— 因为我们将 assertFalse() 替换为 assertTrue() 。将其交换回来，然后重新运行 PHPUnit 。测试应该再次通过，因为我们已经修复了破损的测试。

#### 4.2 assertEquals() 与 assertNull()

接下来，让我们看看 assertEquals(), 以及 assertNull()。assertEquals() 用于比较变量实际值与预期值是否相等。我们用它来检查 takeOne() 方法的返回值是否为 Box 内的当前值。当 Box 为空时，takeOne() 将返回 null，我们亦可使用 assertNull() 来进行检查。

与 assertTrue()、assertFalse() 以及 assertNull() 不同，assertEquals() 需要两个参数。第一个参数为「预期」值，第二个参数则为「实际」值。

可参照如下代码实现以上断言（assertions）：

```php
<?php

namespace Tests\Unit;

use PHPUnit\Framework\TestCase;
use App\Box;

class StackTest extends TestCase
{
    /**
     * A basic unit test example.
     *
     * @return void
     */
    public function testHasItemBox() {
        $box = new Box([
            'cat',
            'toy',
            'torch'
        ]);
        $this->assertTrue($box->has('toy'));
        $this->assertFalse($box->has('dalong'));
    }

    public function testTakeOneFromTheBox() {
        $box = new Box(['torch']);
        $this->assertEquals('torch', $box->takeOne());
        $this->assertNull($box->takeOne());
    }
}

```

运行 phpunit 命令，你应当看到如下输出：

```
OK (3 tests, 6 assertions)
```

#### 4.3 assertContains() 和 assertCount() 以及 assertEmpty()

终于，我们有三个作用于数组有关的断言，我们能够使用它们去检查 Box 类中的 startsWith(\$item) 方法。 assertContains() 断言传递进来的数组中包含指定值，assertCount() 断言数组的项数为指定数量，assertEmpty() 断言传递进来的数组为空。

让我们来执行以下测试：

```php
<?php

namespace Tests\Unit;

use PHPUnit\Framework\TestCase;
use App\Box;

class StackTest extends TestCase
{
    /**
     * A basic unit test example.
     *
     * @return void
     */
    public function testHasItemBox() {
        $box = new Box([
            'cat',
            'toy',
            'torch'
        ]);
        $this->assertTrue($box->has('toy'));
        $this->assertFalse($box->has('dalong'));
    }

    public function testTakeOneFromTheBox() {
        $box = new Box(['torch']);
        $this->assertEquals('torch', $box->takeOne());
        $this->assertNull($box->takeOne());
    }

    public function testStartWithALetter() {
        $box = new Box([
            'toy',
            'torch',
            'ball',
            'cat',
            'tissue'
        ]);
        $result = $box->startWith('t');
        $this->assertCount(3, $result);
        $this->assertContains('toy', $result);
        $this->assertEmpty($box->startWith('d'));
    }
}
```

保存并再一次运行你的测试：

```
OK (4 tests, 9 assertions)
```

恭喜你，你刚刚使用七个基础的 PHPUnit 断言完成了对 Box 类的全部测试。通过这些简单的断言你能够做许多事，对于其他断言，大多数要更复杂，不过它们仍遵循以上使用规则。

### 05. 测试你的程序

在你的程序里，对每个组件进行单元测试在很多情况下都是有必要的，而且也应该成为你开发过程中必不可少的一部分，但这并不是你需要做的全部的测试。当你构建一个包含复杂视图、导航和表单的程序时，你同样想测试这些组件。这时，Laravel 的测试助手可以使这些测试像单元测试简单组件一样容易。

我们之前查看在 ./tests/ 目录下的默认文件时跳过了 ./tests/ExampleTest.php 文件。 现在打开它，内容如下所示：

```php
<?php
class ExampleTest extends TestCase
{
    /**
* 一个基本功能测试示例。
*
* @return void
*/
    public function testBasicExample()
    {
        $this->visit('/')
             ->see('Laravel 5');
    }
}
```

我们可以看到这个测试示例非常简单。在不知道测试助手如何运作的情况下，我们可以猜测它的意思如下：1）当我访问 /（根目录）。2）我应该看到 'Laravel 5'。

如果你打开你的 web 浏览器，访问我们的程序（如果你没有启动你的 web 服务器，你可以运行 php artisan serve ），你应该可以在 web 根目录上看到屏幕上有 “Laravel 5” 的文本。 鉴于这个测试已经通过了 PHPUnit，我们可以很确定地说我们对这个测试示例改造是正确的。

这个测试确保了访问 / 路径，网页可以返回 “'Laravel 5” 的文本。一个如此简单的检查也许不代表什么，但如果你的网站上要显示关键信息，它就可以在一个别处的改动导致这个页面无法正常显示正确的信息时，防止你部署一个被损坏的程序。

#### 5.1 visit()、see() 以及 dontSee()

现在尝试编写自己的测试，更进一步理解它吧。

首先，编辑 ./app/Http/routes.php ，增加一个新的路由。为了教程目的，我们创建希腊字母定义的路由：

```php
<?php
Route::get('/'，function () {
    return view('welcome');
});

Route::get('/alpha'，function () {
    return view('alpha');
});
```

然后，创建视图文件 ./resources/views/alpha.blade.php，使用 Alpha 作为关键字，保存基本的 HTML 文件：

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Alpha</title>
    </head>
    <body>
        <p>This is the Alpha page.</p>
    </body>
</html>
```

打开浏览器，输入网址: http://localhost:8000/alpha，页面会显示出 "This is the Alpha page." 的内容。

现在我们有了测试用到的模版文件，下一步，我们通过运行命令 make:test 来创建一个新的测试文件：

```
php artisan make:test AlphaTest
```

然后变成刚创建好的测试文件，按照框架提供的例子，测试 "alpha" 页面上没有包含 "beta" 。 我们可以使用方法 dontSee() ，它是 see() 的对应的反向方法。

下面代码是上面实现的简单例子：

```php
<?php
class AlphaTest extends TestCase
{
    public function testDisplaysAlpha()
    {
        $this->visit('/alpha')
             ->see('Alpha')
             ->dontSee('Beta');
    }
}
```

保存并运行 PHPUnit (./vendor/bin/phpunit)，测试代码应该会全部通过，你会看到像这样的测试状态内容显示：

```
OK (5 tests，12 assertions)
```

#### 5.2 开发前先写测试

对于测试来说，测试驱动开发（TDD）是非常酷的方法，首先我们先写测试。写完测试并执行它们，你会发现测试没通过，接下来我们编写满足测试的代码，再次执行测试，使测试通过。 接下来让我们开始。

首先，建立一个 BetaTest 类使用 make:test artisan 命令：

```
php artisan make:test BetaTest
```

接下来，更新测试用例以便检查 /beta 的路由 route 为「Beta」：

```php
<?php
class BetaTest extends TestCase
{
    public function testDisplaysBeta()
    {
        $this->visit('/beta')
             ->see('Beta')
             ->dontSee('Alpha');
    }
}
```

现在使用 ./vendor/bin/phpunit 命令来执行测试。结果是一个看起来简洁但不好的错误信息，如下：

```
> ./vendor/bin/phpunit
PHPUnit 4.8.19 by Sebastian Bergmann and contributors.

....F.

Time: 144 ms, Memory: 14.25Mb

There was 1 failure:

1) BetaTest::testDisplaysBeta
一个对 [http://localhost/beta] 的请求失败了。收到状态码 [404]。

...

FAILURES!
Tests: 6, Assertions: 13, Failures: 1.
```

我们现在需要创建这个不存在的路由。让我们开始。

首先，编辑 ./app/Http/routes.php 文件来创建新的 /beta 路由：

```php
<?php
Route::get('/', function () {
    return view('welcome');
});

Route::get('/alpha', function () {
    return view('alpha');
});

Route::get('/beta', function () {
    return view('beta');
});
```

接下来，在 ./resources/views/beta.blade.php 下创建如下视图模版：

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Beta</title>
    </head>
    <body>
        <p>This is the Beta page.</p>
    </body>
</html>
```

现在再一次执行 PHPUnit，结果应该再一次回到绿色。

```
> ./vendor/bin/phpunit
PHPUnit 4.8.19 by Sebastian Bergmann and contributors.

......

Time: 142 ms, Memory: 14.00Mb

OK (6 tests, 15 assertions)
```

这样我们就通过在完成新的页面之前写测试的方式，对「测试驱动开发」进行了实践。

#### 5.3 click() 和 seePageIs()

Laravel 也提供一个辅助函数 click() 允许测试点击页面中存在的连接 ，以及一个方法 seePageIs() 检查点击展示的结果页面。让我们使用这两个辅助函数去执行在 Alpha 和 Beta 页面的链接。

首先，我们更新我们的测试。打开 AlphaTest 类，我们将添加一个新的测试方法，这将点击 「alpha」页面上的「Next」链接跳转到 「beta」页面。

新的测试代码如下：

```php
<?php
class AlphaTest extends TestCase
{
    public function testDisplaysAlpha()
    {
        $this->visit('/alpha')
             ->see('Alpha')
             ->dontSee('Beta');
    }

    public function testClickNextForBeta()
    {
        $this->visit('/alpha')
             ->click('Next')
             ->seePageIs('/beta');
    }
}
```

注意到，在我们新建的 testClickNextForBeta() 方法中，我们并没有检查每一个页面的内容。 其他测试都成功的检查了两个页面的内容，所以这里我们只关心点击 「Next」链接将发送到 /beta。你现在可以运行测试组件了，但就像预料的一样测试将不通过，因为我们还没有更新我们的 HTML。接下来，我们将更新 BetaTest 来做类似的事情：

```php
<?php
class BetaTest extends TestCase
{
    public function testDisplaysBeta()
    {
        $this->visit('/beta')
             ->see('Beta')
             ->dontSee('Alpha');
    }

    public function testClickNextForAlpha()
    {
        $this->visit('/beta')
             ->click('Previous')
             ->seePageIs('/alpha');
    }
}
```

接下来，我们更新我们的 HTML 模版。

./resources/views/alpha.blade.php：

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Alpha</title>
    </head>
    <body>
        <p>This is the Alpha page.</p>
        <p><a href="/beta">Next</a></p>
    </body>
</html>
```

./resources/views/beta.blade.php：

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Beta</title>
    </head>
    <body>
        <p>This is the Beta page.</p>
        <p><a href="/alpha">Previous</a></p>
    </body>
</html>
```

保存文件，再一次执行 PHPUnit：

```
> ./vendor/bin/phpunit
PHPUnit 4.8.19 by Sebastian Bergmann and contributors.

F....F..

Time: 175 ms, Memory: 14.00Mb

There were 2 failures:

1) AlphaTest::testDisplaysAlpha
Failed asserting that '<!DOCTYPE html>
<html>
    <head>
        <title>Alpha</title>
    </head>
    <body>
        <p>This is the Alpha page.</p>
        <p><a href="/beta">Next</a></p>
    </body>
</html>
' does not match PCRE pattern "/Beta/i".

2) BetaTest::testDisplaysBeta
Failed asserting that '<!DOCTYPE html>
<html>
    <head>
        <title>Beta</title>
    </head>
    <body>
        <p>This is the Beta page.</p>
        <p><a href="/alpha">Previous</a></p>
    </body>
</html>
' does not match PCRE pattern "/Alpha/i".

FAILURES!
Tests: 8, Assertions: 23, Failures: 2.
```

然而测试失败了。如果你仔细观察我们的新 HTML，你将注意到我们分别有术语 beta 和 alpha 在 /alpha 和 /beta 页面。这意味着我们需要稍微更改我们的测试让它们与误报不匹配。

在每一个 AlphaTest 和 BetaTest 类，更新 testDisplays* 方法去使用 dontSee('\<page> page')。通过这种方式，这将仅仅匹配字符串而不是那个术语。

两个测试文件如下所示：

./tests/AlphaTest.php：

```php
<?php
class AlphaTest extends TestCase
{
    public function testDisplaysAlpha()
    {
        $this->visit('/alpha')
             ->see('Alpha')
             ->dontSee('Beta page');
    }

    public function testClickNextForBeta()
    {
        $this->visit('/alpha')
             ->click('Next')
             ->seePageIs('/beta');
    }
}
```

./tests/BetaTest.php：

```php
<?php
class BetaTest extends TestCase
{
    public function testDisplaysBeta()
    {
        $this->visit('/beta')
             ->see('Beta')
             ->dontSee('Alpha page');
    }

    public function testClickNextForAlpha()
    {
        $this->visit('/beta')
             ->click('Previous')
             ->seePageIs('/alpha');
    }
}
```

再一次运行你的测试，所有的测试都应该通过了。我们现在已经测试我们所有的新文件，包括页面中的 Next/Previous 链接。

### 06. 通过 Semaphore 对 PHPUnit 持续集成

通过 Semaphore（[Continuous Integration & Delivery - Semaphore](https://semaphoreci.com/)）设置「持续集成」你可以自动执行你的测试。这样每一次你进行 git push 提交代码的时候都会执行你的测试，并且 Semaphore 预装了所有最新的 PHP 版本。

3『 [Semaphore 2.0 Documentation](https://docs.semaphoreci.com/) 』

如果你还没有一个 Semaphore 账户， 先去注册一个免费的 Semaphore 账户。接下来需要做的是将它添加到你的项目，并按照提示逐步去做来执行你的测试：

```
composer install --prefer-source
phpunit
```

关于 PHP 持续集成的更多信息，请参照 Semaphore 文档。

### 结语

你应该注意到本教程中的所有测试都有一个共同的主题：它们都非常简单。 这是学习如何使用基本的测试断言和辅助函数，并且尽可能的使用它们的好处之一。编写测试越简单，测试就越容易理解和维护。掌握了本教程中介绍的 PHPUnit 断言之后，你还可以去 PHPUnit 文档找到更多内容。 所有的断言都遵循基本的模式，但你会发现，在大多数测试中都会返回基本的断言。

对于 PHPUnit 断言来说，Laravel 的测试辅助函数是极好的补充，这让应用程序的测试变的非常容易。也就是说，重要的是要认识到，对于我们写测试，我们只检查关键信息，而不是整个页面。这使得测试变得简单，并允许页面内容随着应用程序的变化而变化。如果关键信息仍然存在，测试仍然通过，每个人都会满意。

文章转自：[上线清单 —— 20 个 Laravel 应用性能优化项 | Laravel China 社区](https://learnku.com/laravel/t/24559)

更多文章：[优质外文翻译 | Laravel China 社区](https://learnku.com/laravel/c/translations)

』

## 1006Mocking.md

# 1006. Mocking

## 6.1 Introduction

When testing Laravel applications, you may wish to "mock" certain aspects of your application so they are not actually executed during a given test. For example, when testing a controller that dispatches an event, you may wish to mock the event listeners so they are not actually executed during the test. This allows you to only test the controller's HTTP response without worrying about the execution of the event listeners, since the event listeners can be tested in their own test case.

Laravel provides helpers for mocking events, jobs, and facades out of the box. These helpers primarily provide a convenience layer over Mockery so you do not have to manually make complicated Mockery method calls. You can also use Mockery or PHPUnit to create your own mocks or spies.

3『 [Mockery — Mockery Docs 1.0-alpha documentation](http://docs.mockery.io/en/latest/) 』

## 6.2 Mocking Objects

When mocking an object that is going to be injected into your application via Laravel's service container, you will need to bind your mocked instance into the container as an instance binding. This will instruct the container to use your mocked instance of the object instead of constructing the object itself:

```php
use App\Service;
use Mockery;

$this->instance(Service::class, Mockery::mock(Service::class, function ($mock) {
    $mock->shouldReceive('process')->once();
}));
```

3『

自 PHP 5.5 起，关键词 class 也可用于类名的解析。

使用 ClassName::class 可以获取一个字符串，包含了类 ClassName 的完全限定名称。这对使用了命名空间的类尤其有用。

```php
<?php
namespace ddd\vector;

class Demo
{

    public function test()
    {
        // code...
    }
}

echo Demo::class; //ddd\vector\Demo

?>
```

』

In order to make this more convenient, you may use the mock method, which is provided by Laravel's base test case class:

```php
use App\Service;

$this->mock(Service::class, function ($mock) {
    $mock->shouldReceive('process')->once();
});
```

You may use the partialMock method when you only need to mock a few methods of an object. The methods that are not mocked will be executed normally when called:

```php
use App\Service;

$this->partialMock(Service::class, function ($mock) {
    $mock->shouldReceive('process')->once();
});
```

Similarly, if you want to spy on an object, Laravel's base test case class offers a spy method as a convenient wrapper around the Mockery::spy method:

```php
use App\Service;

$this->spy(Service::class, function ($mock) {
    $mock->shouldHaveReceived('process');
});
```

## 6.3 Bus Fake

As an alternative to mocking, you may use the Bus facade's fake method to prevent jobs from being dispatched. When using fakes, assertions are made after the code under test is executed:

```php
<?php

namespace Tests\Feature;

use App\Jobs\ShipOrder;
use Illuminate\Foundation\Testing\RefreshDatabase;
use Illuminate\Foundation\Testing\WithoutMiddleware;
use Illuminate\Support\Facades\Bus;
use Tests\TestCase;

class ExampleTest extends TestCase
{
    public function testOrderShipping()
    {
        Bus::fake();

        // Perform order shipping...

        // Assert a specific type of job was dispatched meeting the given truth test...
        Bus::assertDispatched(function (ShipOrder $job) use ($order) {
            return $job->order->id === $order->id;
        });

        // Assert a job was not dispatched...
        Bus::assertNotDispatched(AnotherJob::class);
    }
}
```

## 6.4 Event Fake

As an alternative to mocking, you may use the Event facade's fake method to prevent all event listeners from executing. You may then assert that events were dispatched and even inspect the data they received. When using fakes, assertions are made after the code under test is executed:

```php
<?php

namespace Tests\Feature;

use App\Events\OrderFailedToShip;
use App\Events\OrderShipped;
use Illuminate\Foundation\Testing\RefreshDatabase;
use Illuminate\Foundation\Testing\WithoutMiddleware;
use Illuminate\Support\Facades\Event;
use Tests\TestCase;

class ExampleTest extends TestCase
{
    /**
     * Test order shipping.
     */
    public function testOrderShipping()
    {
        Event::fake();

        // Perform order shipping...

        // Assert a specific type of event was dispatched meeting the given truth test...
        Event::assertDispatched(function (OrderShipped $event) use ($order) {
            return $event->order->id === $order->id;
        });

        // Assert an event was dispatched twice...
        Event::assertDispatched(OrderShipped::class, 2);

        // Assert an event was not dispatched...
        Event::assertNotDispatched(OrderFailedToShip::class);
    }
}
```

After calling Event::fake(), no event listeners will be executed. So, if your tests use model factories that rely on events, such as creating a UUID during a model's creating event, you should call Event::fake() after using your factories.

### Faking A Subset Of Events

If you only want to fake event listeners for a specific set of events, you may pass them to the fake or fakeFor method:

```php
/**
 * Test order process.
 */
public function testOrderProcess()
{
    Event::fake([
        OrderCreated::class,
    ]);

    $order = factory(Order::class)->create();

    Event::assertDispatched(OrderCreated::class);

    // Other events are dispatched as normal...
    $order->update([...]);
}
```

### Scoped Event Fakes

If you only want to fake event listeners for a portion of your test, you may use the fakeFor method:

```php
<?php

namespace Tests\Feature;

use App\Events\OrderCreated;
use App\Order;
use Illuminate\Foundation\Testing\RefreshDatabase;
use Illuminate\Support\Facades\Event;
use Illuminate\Foundation\Testing\WithoutMiddleware;
use Tests\TestCase;

class ExampleTest extends TestCase
{
    /**
     * Test order process.
     */
    public function testOrderProcess()
    {
        $order = Event::fakeFor(function () {
            $order = factory(Order::class)->create();

            Event::assertDispatched(OrderCreated::class);

            return $order;
        });

        // Events are dispatched as normal and observers will run ...
        $order->update([...]);
    }
}
```

## 6.5 HTTP Fake

The Http facade's fake method allows you to instruct the HTTP client to return stubbed / dummy responses when requests are made. For more information on faking outgoing HTTP requests, please consult the HTTP Client testing documentation.

[HTTP Client - Laravel - The PHP Framework For Web Artisans](https://laravel.com/docs/7.x/http-client#testing)

## 6.6 Mail Fake

You may use the Mail facade's fake method to prevent mail from being sent. You may then assert that mailables were sent to users and even inspect the data they received. When using fakes, assertions are made after the code under test is executed:

```php
<?php

namespace Tests\Feature;

use App\Mail\OrderShipped;
use Illuminate\Foundation\Testing\RefreshDatabase;
use Illuminate\Foundation\Testing\WithoutMiddleware;
use Illuminate\Support\Facades\Mail;
use Tests\TestCase;

class ExampleTest extends TestCase
{
    public function testOrderShipping()
    {
        Mail::fake();

        // Assert that no mailables were sent...
        Mail::assertNothingSent();

        // Perform order shipping...

        // Assert a specific type of mailable was dispatched meeting the given truth test...
        Mail::assertSent(function (OrderShipped $mail) use ($order) {
            return $mail->order->id === $order->id;
        });

        // Assert a message was sent to the given users...
        Mail::assertSent(OrderShipped::class, function ($mail) use ($user) {
            return $mail->hasTo($user->email) &&
                   $mail->hasCc('...') &&
                   $mail->hasBcc('...');
        });

        // Assert a mailable was sent twice...
        Mail::assertSent(OrderShipped::class, 2);

        // Assert a mailable was not sent...
        Mail::assertNotSent(AnotherMailable::class);
    }
}
```

If you are queueing mailables for delivery in the background, you should use the assertQueued method instead of assertSent:

```php
Mail::assertQueued(...);
Mail::assertNotQueued(...);
```

## 6.7 Notification Fake

You may use the Notification facade's fake method to prevent notifications from being sent. You may then assert that notifications were sent to users and even inspect the data they received. When using fakes, assertions are made after the code under test is executed:

```php
<?php

namespace Tests\Feature;

use App\Notifications\OrderShipped;
use Illuminate\Foundation\Testing\RefreshDatabase;
use Illuminate\Foundation\Testing\WithoutMiddleware;
use Illuminate\Notifications\AnonymousNotifiable;
use Illuminate\Support\Facades\Notification;
use Tests\TestCase;

class ExampleTest extends TestCase
{
    public function testOrderShipping()
    {
        Notification::fake();

        // Assert that no notifications were sent...
        Notification::assertNothingSent();

        // Perform order shipping...

        // Assert a specific type of notification was sent meeting the given truth test...
        Notification::assertSentTo(
            $user,
            function (OrderShipped $notification, $channels) use ($order) {
                return $notification->order->id === $order->id;
            }
        );

        // Assert a notification was sent to the given users...
        Notification::assertSentTo(
            [$user], OrderShipped::class
        );

        // Assert a notification was not sent...
        Notification::assertNotSentTo(
            [$user], AnotherNotification::class
        );

        // Assert a notification was sent via Notification::route() method...
        Notification::assertSentTo(
            new AnonymousNotifiable, OrderShipped::class
        );

        // Assert Notification::route() method sent notification to the correct user...
        Notification::assertSentTo(
            new AnonymousNotifiable,
            OrderShipped::class,
            function ($notification, $channels, $notifiable) use ($user) {
                return $notifiable->routes['mail'] === $user->email;
            }
        );
    }
}
```

## 6.8 Queue Fake

As an alternative to mocking, you may use the Queue facade's fake method to prevent jobs from being queued. You may then assert that jobs were pushed to the queue and even inspect the data they received. When using fakes, assertions are made after the code under test is executed:

```php
<?php

namespace Tests\Feature;

use App\Jobs\AnotherJob;
use App\Jobs\FinalJob;
use App\Jobs\ShipOrder;
use Illuminate\Foundation\Testing\RefreshDatabase;
use Illuminate\Foundation\Testing\WithoutMiddleware;
use Illuminate\Support\Facades\Queue;
use Tests\TestCase;

class ExampleTest extends TestCase
{
    public function testOrderShipping()
    {
        Queue::fake();

        // Assert that no jobs were pushed...
        Queue::assertNothingPushed();

        // Perform order shipping...

        // Assert a specific type of job was pushed meeting the given truth test...
        Queue::assertPushed(function (ShipOrder $job) use ($order) {
            return $job->order->id === $order->id;
        });

        // Assert a job was pushed to a given queue...
        Queue::assertPushedOn('queue-name', ShipOrder::class);

        // Assert a job was pushed twice...
        Queue::assertPushed(ShipOrder::class, 2);

        // Assert a job was not pushed...
        Queue::assertNotPushed(AnotherJob::class);

        // Assert a job was pushed with a given chain of jobs, matching by class...
        Queue::assertPushedWithChain(ShipOrder::class, [
            AnotherJob::class,
            FinalJob::class
        ]);

        // Assert a job was pushed with a given chain of jobs, matching by both class and properties...
        Queue::assertPushedWithChain(ShipOrder::class, [
            new AnotherJob('foo'),
            new FinalJob('bar'),
        ]);

        // Assert a job was pushed without a chain of jobs...
        Queue::assertPushedWithoutChain(ShipOrder::class);
    }
}
```

## 6.9 Storage Fake

The Storage facade's fake method allows you to easily generate a fake disk that, combined with the file generation utilities of the UploadedFile class, greatly simplifies the testing of file uploads. For example:

```php
<?php

namespace Tests\Feature;

use Illuminate\Foundation\Testing\RefreshDatabase;
use Illuminate\Foundation\Testing\WithoutMiddleware;
use Illuminate\Http\UploadedFile;
use Illuminate\Support\Facades\Storage;
use Tests\TestCase;

class ExampleTest extends TestCase
{
    public function testAlbumUpload()
    {
        Storage::fake('photos');

        $response = $this->json('POST', '/photos', [
            UploadedFile::fake()->image('photo1.jpg'),
            UploadedFile::fake()->image('photo2.jpg')
        ]);

        // Assert one or more files were stored...
        Storage::disk('photos')->assertExists('photo1.jpg');
        Storage::disk('photos')->assertExists(['photo1.jpg', 'photo2.jpg']);

        // Assert one or more files were not stored...
        Storage::disk('photos')->assertMissing('missing.jpg');
        Storage::disk('photos')->assertMissing(['missing.jpg', 'non-existing.jpg']);
    }
}
```

By default, the fake method will delete all files in its temporary directory. If you would like to keep these files, you may use the "persistentFake" method instead.

## 6.10 Facades

Unlike traditional static method calls, facades may be mocked. This provides a great advantage over traditional static methods and grants you the same testability you would have if you were using dependency injection. When testing, you may often want to mock a call to a Laravel facade in one of your controllers. For example, consider the following controller action:

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Support\Facades\Cache;

class UserController extends Controller
{
    /**
     * Show a list of all users of the application.
     *
     * @return Response
     */
    public function index()
    {
        $value = Cache::get('key');

        //
    }
}
```

We can mock the call to the Cache facade by using the shouldReceive method, which will return an instance of a Mockery mock. Since facades are actually resolved and managed by the Laravel service container, they have much more testability than a typical static class. For example, let's mock our call to the Cache facade's get method:

```php
<?php

namespace Tests\Feature;

use Illuminate\Foundation\Testing\RefreshDatabase;
use Illuminate\Foundation\Testing\WithoutMiddleware;
use Illuminate\Support\Facades\Cache;
use Tests\TestCase;

class UserControllerTest extends TestCase
{
    public function testGetIndex()
    {
        Cache::shouldReceive('get')
                    ->once()
                    ->with('key')
                    ->andReturn('value');

        $response = $this->get('/users');

        // ...
    }
}
```

You should not mock the Request facade. Instead, pass the input you desire into the HTTP helper methods such as get and post when running your test. Likewise, instead of mocking the Config facade, call the Config::set method in your tests.

## 2001. HTTP-Responses.md

[HTTP Responses - Laravel - The PHP Framework For Web Artisans](https://laravel.com/docs/7.x/responses)

### 01. Creating Responses

#### 1.1 Strings & Arrays

All routes and controllers should return a response to be sent back to the user's browser. Laravel provides several different ways to return responses. The most basic response is returning a string from a route or controller. The framework will automatically convert the string into a full HTTP response:

「最后的 return response() 原来如此，路由和控制器得返回一个 response（数据）给浏览器。」

```php
Route::get('/', function () {
    return 'Hello World';
});
```

In addition to returning strings from your routes and controllers, you may also return arrays. The framework will automatically convert the array into a JSON response:

```php
Route::get('/', function () {
    return [1, 2, 3];
});
```

Did you know you can also return Eloquent collections from your routes or controllers? They will automatically be converted to JSON. Give it a shot!

1『原来 collections 对象是 Eloquent collections，而且可以被自动转化为 json 对象。』

#### 1.2 Response Objects

Typically, you won't just be returning simple strings or arrays from your route actions. Instead, you will be returning full Illuminate\Http\Response instances or views.

Returning a full Response instance allows you to customize the response's HTTP status code and headers. A Response instance inherits from the Symfony\Component\HttpFoundation\Response class, which provides a variety of methods for building HTTP responses:

```php
Route::get('home', function () {
    return response('Hello World', 200)
                  ->header('Content-Type', 'text/plain');
});
```

#### 1.3 Attaching Headers To Responses

Keep in mind that most response methods are chainable, allowing for the fluent construction of response instances. For example, you may use the header method to add a series of headers to the response before sending it back to the user:

```php
return response($content)
            ->header('Content-Type', $type)
            ->header('X-Header-One', 'Header Value')
            ->header('X-Header-Two', 'Header Value');
```

Or, you may use the withHeaders method to specify an array of headers to be added to the response:

```php
return response($content)
            ->withHeaders([
                'Content-Type' => $type,
                'X-Header-One' => 'Header Value',
                'X-Header-Two' => 'Header Value',
            ]);
```

#### 1.4 Cache Control Middleware

Laravel includes a cache.headers middleware, which may be used to quickly set the Cache-Control header for a group of routes. If etag is specified in the list of directives, an MD5 hash of the response content will automatically be set as the ETag identifier:

```php
Route::middleware('cache.headers:public;max_age=2628000;etag')->group(function () {
    Route::get('privacy', function () {
        // ...
    });

    Route::get('terms', function () {
        // ...
    });
});
```

#### 1.5 Attaching Cookies To Responses

The cookie method on response instances allows you to easily attach cookies to the response. For example, you may use the cookie method to generate a cookie and fluently attach it to the response instance like so:

```php
return response($content)
                ->header('Content-Type', $type)
                ->cookie('name', 'value', $minutes);
```

The cookie method also accepts a few more arguments which are used less frequently. Generally, these arguments have the same purpose and meaning as the arguments that would be given to PHP's native setcookie method:

```php
->cookie($name, $value, $minutes, $path, $domain, $secure, $httpOnly)
```

Alternatively, you can use the Cookie facade to "queue" cookies for attachment to the outgoing response from your application. The queue method accepts a Cookie instance or the arguments needed to create a Cookie instance. These cookies will be attached to the outgoing response before it is sent to the browser:

```php
Cookie::queue(Cookie::make('name', 'value', $minutes));
Cookie::queue('name', 'value', $minutes);
```

#### 1.6 Cookies & Encryption

By default, all cookies generated by Laravel are encrypted and signed so that they can't be modified or read by the client. If you would like to disable encryption for a subset of cookies generated by your application, you may use the \$except property of the App\Http\Middleware\EncryptCookies middleware, which is located in the app/Http/Middleware directory:

```php
/**
 * The names of the cookies that should not be encrypted.
 *
 * @var array
 */
protected $except = [
    'cookie_name',
];
```

### 02. Redirects

Redirect responses are instances of the Illuminate\Http\RedirectResponse class, and contain the proper headers needed to redirect the user to another URL. There are several ways to generate a RedirectResponse instance. The simplest method is to use the global redirect helper:

1『 URL 的重定向。』

```php
Route::get('dashboard', function () {
    return redirect('home/dashboard');
});
```

Sometimes you may wish to redirect the user to their previous location, such as when a submitted form is invalid. You may do so by using the global back helper function. Since this feature utilizes the session, make sure the route calling the back function is using the web middleware group or has all of the session middleware applied:

```php
Route::post('user/profile', function () {
    // Validate the request...

    return back()->withInput();
});
```

1『

有看到过应用的场景。比如在控制器文件里，最后面如果不返回到指定的页面，可以返回到上个页面。

```php
// return view('importresult');
return back();  // 返回到上一个页面
```

』

#### 2.1 Redirecting To Named Routes

When you call the redirect helper with no parameters, an instance of Illuminate\Routing\Redirector is returned, allowing you to call any method on the Redirector instance. For example, to generate a RedirectResponse to a named route, you may use the route method:

```php
return redirect()->route('login');
```

1『真是方便，原来实例化一个重定向方法「redirect()」，可以访问到任何一个路由指定的页面。』

If your route has parameters, you may pass them as the second argument to the route method:

```php
// For a route with the following URI: profile/{id}
return redirect()->route('profile', ['id' => 1]);
```

#### 2.2 Populating Parameters Via Eloquent Models

If you are redirecting to a route with an "ID" parameter that is being populated from an Eloquent model, you may pass the model itself. The ID will be extracted automatically:

```
// For a route with the following URI: profile/{id}

return redirect()->route('profile', [$user]);
```

If you would like to customize the value that is placed in the route parameter, you can specify the column in the route parameter definition (profile/{id:slug}) or you can override the getRouteKey method on your Eloquent model:

```php
/**
 * Get the value of the model's route key.
 *
 * @return mixed
 */
public function getRouteKey()
{
    return $this->slug;
}
```

3『

上面的是关键知识点，跟「2020121Full-Stack-Vuejs2-R01.md -> 4.12 Public interface」里的设置路由公共接口有异曲同工之妙。

routes/api.php:

```php
Route::get('/listing/{listing}', function(ListingModel $listing) {
    return $listing->toJson();
```

』

#### 2.3 Redirecting To Controller Actions

You may also generate redirects to controller actions. To do so, pass the controller and action name to the action method. Remember, you do not need to specify the full namespace to the controller since Laravel's RouteServiceProvider will automatically set the base controller namespace:

```php
return redirect()->action('HomeController@index');
```

If your controller route requires parameters, you may pass them as the second argument to the action method:

```php
return redirect()->action(
    'UserController@profile', ['id' => 1]
);
```

#### 2.4 Redirecting To External Domains

Sometimes you may need to redirect to a domain outside of your application. You may do so by calling the away method, which creates a RedirectResponse without any additional URL encoding, validation, or verification:

```php
return redirect()->away('https://www.google.com');
```

#### 2.5 Redirecting With Flashed Session Data

Redirecting to a new URL and flashing data to the session are usually done at the same time. Typically, this is done after successfully performing an action when you flash a success message to the session. For convenience, you may create a RedirectResponse instance and flash data to the session in a single, fluent method chain:

```php
Route::post('user/profile', function () {
    // Update the user's profile...

    return redirect('dashboard')->with('status', 'Profile updated!');
});
```

After the user is redirected, you may display the flashed message from the session. For example, using Blade syntax:

```php
@if (session('status'))
    <div class="alert alert-success">
        {{ session('status') }}
    </div>
@endif
```

3『

 [HTTP Session - Laravel - The PHP Framework For Web Artisans](https://laravel.com/docs/7.x/session#flash-data) 
 
 [Blade Templates - Laravel - The PHP Framework For Web Artisans](https://laravel.com/docs/7.x/blade)
 
 』

### 03. Other Response Types

The response helper may be used to generate other types of response instances. When the response helper is called without arguments, an implementation of the Illuminate\Contracts\Routing\ResponseFactory contract is returned. This contract provides several helpful methods for generating responses.

#### 3.1 View Responses

If you need control over the response's status and headers but also need to return a view as the response's content, you should use the view method:

```php
return response()
            ->view('hello', $data, 200)
            ->header('Content-Type', $type);
```

Of course, if you do not need to pass a custom HTTP status code or custom headers, you should use the global view helper function.

#### 3.2 JSON Responses

The json method will automatically set the Content-Type header to application/json, as well as convert the given array to JSON using the json\_encode PHP function:

```php
return response()->json([
    'name' => 'Abigail',
    'state' => 'CA'
]);
```

If you would like to create a JSONP response, you may use the json method in combination with the withCallback method:

```php
return response()
            ->json(['name' => 'Abigail', 'state' => 'CA'])
            ->withCallback($request->input('callback'));
```

#### 3.3 File Downloads

The download method may be used to generate a response that forces the user's browser to download the file at the given path. The download method accepts a file name as the second argument to the method, which will determine the file name that is seen by the user downloading the file. Finally, you may pass an array of HTTP headers as the third argument to the method:

```php
return response()->download($pathToFile);

return response()->download($pathToFile, $name, $headers);

return response()->download($pathToFile)->deleteFileAfterSend();
```

Symfony HttpFoundation, which manages file downloads, requires the file being downloaded to have an ASCII file name.

#### 3.3.1 Streamed Downloads

Sometimes you may wish to turn the string response of a given operation into a downloadable response without having to write the contents of the operation to disk. You may use the streamDownload method in this scenario. This method accepts a callback, file name, and an optional array of headers as its arguments:

```php
return response()->streamDownload(function () {
    echo GitHub::api('repo')
                ->contents()
                ->readme('laravel', 'laravel')['contents'];
}, 'laravel-readme.md');
```

#### 3.4 File Responses

The file method may be used to display a file, such as an image or PDF, directly in the user's browser instead of initiating a download. This method accepts the path to the file as its first argument and an array of headers as its second argument:

```php
return response()->file($pathToFile);
return response()->file($pathToFile, $headers);
```

### 04. Response Macros

If you would like to define a custom response that you can re-use in a variety of your routes and controllers, you may use the macro method on the Response facade. For example, from a service provider's boot method:

```php
<?php

namespace App\Providers;

use Illuminate\Support\Facades\Response;
use Illuminate\Support\ServiceProvider;

class ResponseMacroServiceProvider extends ServiceProvider
{
    /**
     * Register the application's response macros.
     *
     * @return void
     */
    public function boot()
    {
        Response::macro('caps', function ($value) {
            return Response::make(strtoupper($value));
        });
    }
}
```

The macro function accepts a name as its first argument, and a Closure as its second. The macro's Closure will be executed when calling the macro name from a ResponseFactory implementation or the response helper:

```php
return response()->caps('foo');
```
# PHP Test Driven Development Part 4: Enter The Mock

[PHP Test Driven Development Part 4: Enter The Mock | by Sameer Nyaupane | Medium](https://medium.com/@sameernyaupane/php-test-driven-development-part-4-enter-the-mock-106b4fdedd00)

Sameer Nyaupane

Sep 15, 2018 · 4 min read

Hey there, welcome to part 4! Today we’ll learn how to mock. Mocking is a process where you create a fake instance of a real class, and test against it. This is so that, you do not have to worry about the real functionality of external dependencies inside a class. This makes unit testing a lot easier and reliable.

Please check out Part3, if you have not read it yet: https://hackernoon.com/php-test-driven-development-part-3-unit-testing-continued-db5d332197ec

Although PHPUnit does have mocking capabilities, it is not as full fledged as that of Mockery’s ([Mockery — Mockery Docs 1.0-alpha documentation](http://docs.mockery.io/en/latest/)). We’ll be using Mockery for all our mocking needs. Another good thing is that Laravel ships with Mockery by default. We can get started straight away without any installation or configuration.

1-2『哈哈，laravel 自待了 Mockery，之前确实在 composer.json 里看到了它。可以去消化吸收 Mockery 的官方文档了。（2020-09-24）』

First, let’s write some sample code that we’ll use. For the purpose of making it simple, we’ll just make a wrapper class. A wrapper class called “Math” that calls the “Calculate” class. The same “Calculate” class that we made in the previous episode. Let’s make the file with the path “app/Math.php”.

```php
<?php
namespace App;

class Math
{
    /**
     * @var Calculate
     */
    public $calculate;

    /**
     * Math constructor.
     *
     * @param Calculate $calculate
     */
    public function __construct(Calculate $calculate)
    {
        $this->calculate = $calculate;
    }

    /**
     * Get Area
     * 
     * @param $length
     * 
     * @return float|int
     */
    public function getArea($length)
    {
        return $this->calculate->areaOfSquare($length);
    }
}
```

Here, on line 16, we require a Calculate class in the same namespace “App”. Then we assign it to the same object instance on line 18.

Remember to always opt for dependency injections through the constructor instead of creating them through the “new” keyword inside the methods. This makes testing a lot easier when we make the mocks. Yes, you can still mock the “new” keyword instantiation using Mockery, but it’s almost always a bad idea. Another one is statics, it is best to avoid static calls and instead use their equivalent classes through constructor. If you’re using Laravel framework, you can always check the facade class reference to see what class you can use instead of the static calls. The facade class refrence is at: [Facades - Laravel - The PHP Framework For Web Artisans](https://laravel.com/docs/5.7/facades#facade-class-reference).

Line 30 is where we call the areaOfSquare method of the dependency (`$this->calculate`).

1『关键知识点：1）通过构造函数依赖注入一个对象而非 new 一个对象，构造函数注入对象大大便于测试。2）不要用静态方法。』

So how would we go about testing this class? Here’s how we would do it:

```php
<?php
namespace Tests\Unit;

use App\Math;
use Mockery as m;
use Mockery\Adapter\Phpunit\MockeryTestCase;

class MathTest extends MockeryTestCase
{
    public function setUp() 
    {
        $this->calculate = m::mock('App\Calculate');

        $this->math = new Math($this->calculate);
    }

    public function test_getArea_WhenCalledWithLength2_Return4()
    {
        $this->calculate->shouldReceive('areaOfSquare')
            ->andReturn(4)
            ->once();

        $length = 2;

        $response = $this->math->getArea($length);

        $this->assertTrue(is_int($response));
        $this->assertEquals(4, $response);
    }
}
```

Let’s go ahead and add this file to `/tests/Unit` folder. Let’s run this test on the command prompt:

1『这里学到了一个技巧，竟然可以仅仅对一个方法来做测试，哈哈，太好了。直接命令 `phpunit --filter testMockTest`，testMockTest 是测试用例的方法名。』

Great, 1 test passed with 3 assertions. Two assertions are the same as before on line 27 and 28. And one more new assertion is that of Mockery on line 19. 

On line 5 we declare that we will use Mockery class with reference ‘m’. Line 6 is a new change. Instead of using the default PHPUnit TestCase, here we use Mockery’s TestCase. This is so that Mockery can carry out Mockery specific assertion verification and cleanup the process after each test call.

For readers who have used Mockery before, you may be confused. Previously you’d have to run m::close() on tearDown() method for each test class. This has changed since Mockery v1.0.0 . You do not need to do that if you instead extend the Mockery’s TestCase class or use it’s trait. More info regarding this here: [PHPUnit Integration — Mockery Docs 1.0-alpha documentation](http://docs.mockery.io/en/latest/reference/phpunit_integration.html).

Line 12 is where we make a mock object having the namespace of “App\Calculate”. This namespace has to be same as the original “Calculate” class, or else it will throw an error. Then on line 14 we pass that newly created mock object to the new instance of Math class.

Now on line 19, is where the Mockery specific assertion begins. Now, we assert that the calculate class should receive the ‘areaOfSquare’ method call and we’ll return 4 when it does. And it should only be called once throughout the test execution, or it will fail. If you want it to run twice you can do `->twice()` or times `({number})` for any number of times.

There are different ways and techniques to declare expectations according to your need. I encourage you to check the official documentation for the full reference at http://docs.mockery.io/en/latest/reference/expectations.html.

That was it for the introduction and usage of mocks. Hurray! Now we know how to use mocks! We can now mock them pesky dependencies left and right as we please. There are still a lot more to learn regarding mocks, but what we have is enough for our use case. We will be using it extensively on the next episodes as we go on to tackle TDD.

On the next episode, we will go and learn about Integration tests. The tests that do not deal with mocks, but rather call the real implementations.

[PHP Test Driven Development Part 5: Integration Testing | by Sameer Nyaupane | Medium](https://medium.com/@sameernyaupane/php-test-driven-development-part-5-integration-testing-51535ca56bf0)
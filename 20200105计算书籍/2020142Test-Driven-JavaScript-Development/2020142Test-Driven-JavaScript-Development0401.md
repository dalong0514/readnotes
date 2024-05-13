# 0401. Jasmine

The previous chapter introduced a number of JavaScript tools and frameworks, Jasmine was one of them. This chapter will showcase more about Jasmine. Jasmine is known as a behavior-driven development framework, popularly used for unit testing of JavaScript code, which makes it essential to read and understand the differences between test-driven and behavior-driven development. 

We are going to learn the following: 1) Understanding behavior-driven development. 2) Jasmine framework. 3) Advantages and disadvantages.

## 4.1 Understanding behavior-driven development 

A very important thing to learn about TDD is that it's not about just testing, but it's more than that. It defines a process and encourages to improve the overall design of a system. We have seen in Chapter 1, Overview of TDD, and Chapter 2, Testing Concepts, that tests written in TDD not only test our projects, but they also act as documentation and are useful in many more ways. But most of the developers tend to take it just for testing and are not able to harness the benefit of TDD beyond that; probably, because the title mentions test in TDD. 

Behavior-driven development (BDD) is a term introduced by Dan North to address this shortcoming. The terminology used by BDD focuses on the behavioral aspect of the system. In this chapter, you are going to learn about Jasmine in detail and note that the differences in nomenclature of TDD and BDD. Deep down, TDD and BDD would serve the same purpose, but using the vocabulary of BDD gives you a better set of tests and documents your system in a better way. 

While TDD interface gives names such as suite(), test(), setup(), teardown(), suiteSetup(), suiteTearDown(), assert(), and so on. BDD offers describe(), context(), it(), beforeEach(), afterEach(), beforeAll(), afterAll(), expect(), and so on. A test suite in TDD is usually created using suite(),while BDD uses describe(); to create a unit test TDD uses test() and BDD uses it(). 

2『 TDD 与 BDD 的区别，做一张术语卡片。』——已完成

Follow the table here for the differences: 

![](./res/2020005.png)

## 4.2 Setting up Jasmine 

Jasmine does not depend on any other JavaScript frameworks. It is available as a standalone release at https://github.com/jasmine/jasmine/releases. We are going to pick a stable version, for example, v2.3.0 for this chapter. We can download a ZIP file of standalone release, which we need to extract and use. After extraction, the folder structure looks like this: 

In the lib folder, we require the CSS and JS files to be included. We have seen test runners for many tools so far, Jasmine has SpecRunner. We will see how it looks later in this chapter when we will run our tests. 

## 4.3 describe and specs

We have seen tests suites in many tools in the previous chapters. In Jasmine, we use describe to start a test suite. describe is a global function, which takes two parameters—a string and a function. The string is the title for the suite and function contains all of the tests implementations. A test in Jasmine is known as spec. The parameter function in the describe function contains one or more specs. A spec is also defined by calling a global function it, which takes two parameters just like describe. 

1『 jasmine 里一个测试是一个 spec。测试组件 describe 的第二个函数参数里可以包含多个 spec。而 spec 是别全局函数 it() 调用的，it 函数的 2 个参数与 describe 很像，一个是名字字符串一个是调用函数。』

Let's take a look at the following code: 

```js
describe("Title of a Suite", function() { 
    // variables available for all specs 
    var amountToConvert; 
    var rateOfConversion; 
    
    // the function 'it' defines a spec 
    it("Title of a Spec", function() { 
        // do some testing here 
    }); 
    it("Another spec", function() { 
        // do some testing here 
    }); 
}); 
```

As seen from the preceding code, describe defined a suite and specs were defined using it. To make these functions available, we need to use Jasmine JavaScript libraries. The following is the necessary code we need to include in our HTML file: 

```html
<script src="lib/jasmine-2.3.0/jasmine.js"></script> 
<script src="lib/jasmine-2.3.0/jasmine-html.js"></script> 
<script src="lib/jasmine-2.3.0/boot.js"></script> 
```

To style the page, we can use the CSS provided by Jasmine: 

```html
<link rel="stylesheet" type="text/css" href="lib/jasmine- 
2.3.0/jasmine.css"> 
```

Jasmine keeps our JavaScript code and tests in different folders, src—for our logical code, and spec—for all the tests. You would need to check the paths of the files as per your setup. A simple skeleton will be like this: 

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Jasmine Spec Runner v3.5.0</title>

  <link rel="shortcut icon" type="image/png" href="lib/jasmine-3.5.0/jasmine_favicon.png">
  <link rel="stylesheet" href="lib/jasmine-3.5.0/jasmine.css">

  <script src="lib/jasmine-3.5.0/jasmine.js"></script>
  <script src="lib/jasmine-3.5.0/jasmine-html.js"></script>
  <script src="lib/jasmine-3.5.0/boot.js"></script>

  <!-- include source files here... -->
  <script src="src/Player.js"></script>
  <script src="src/Song.js"></script>

  <!-- include spec files here... -->
  <script src="spec/SpecHelper.js"></script>
  <script src="spec/PlayerSpec.js"></script>

</head>

<body>
</body>
</html>
```

1『结构超级清晰，逻辑代码放在 src 文件夹里，测试代码放在 spec 文件夹里。』

In the preceding code, we included two more files except those required by Jasmine. One is start.js in the src/ folder, which contains our logical code, functions, and many more. Another one is startSpec.js, which contains our testing code. For now, we created a simple function to add two values in start.js. 

```js
// function to add two values. 
function add(a, b){ 
    return a + b; 
} 
```

And we created our specs in the startSpec.js file in the spec folder. 

```js
describe('Title of a Suite', function() {
    let numberA = 3;
    let numberB = 2;

    it('Testing the add() function', function() {
        expect(add(numberA, numberB)).toEqual(5);
    });
});
```

1『第一次写代码的时候犯了个错「expect(add(numberA, numberB).toEqual(5));」，自以为 toEqual() 函数是 add() 的链函数，其实是 expect() 的链函数，注意括号的位置。』

We added an expectation in the spec chained with a matcher toEqual(). This matcher is going to compare the values. You are going to learn expectations and matchers further in this chapter. For now, let's create a file (for example, testAdd. html) and see the output after we run the file. Open the browser and run testAdd. html to run the tests: 

## 4.4 Expectations 

Assertions in Jasmine are named as an expectation. An expectation can either be true or false. Every expectation takes an actual value as only argument. An expectation is then chained with a matcher, which takes the expected value as an argument. 

```js
expect(true).toBe(true); 
```

1『断言语句的基本结构，上面的阐述说的很清晰了。』

Here, expect is an expectation and toBe is a matcher. To evaluate negative assertions, expect() is chained with a not before calling a matcher. Matchers are used for Boolean comparison and validation of an expected value. You will learn more about matchers in the next subsection. See the following code: 

```js
expect(false).not.toBe(true); 
```

## 4.4 Matchers 

Matchers are used to compare the expected and actual values or validation of the expected value. If a matcher is going to compare the expected value, it takes actual value as argument. Matchers are chained with expectations. There are a number of matchers provided by Jasmine. Here is a list of all matchers: 

### 4.4.1 toBe() 

This matcher compares using the identity (===) operator. 

```js
var a = 5; 
expect(a).toBe(5); 
expect(a).not.toBe("5"); 
```

The difference between the identity operator (===) and equality operator (==) is that in identity operator, no type conversion is done before comparison. 

### 4.4.2 toEqual()

This matcher is used to compare simple literals, variables, and functions. 

```js
expect(a).toEqual(5); // checking for simple variables. 
expect(a).not.toEqual(3); 
```

For simple literals and variables, both toBe() and toEqual() can be used, but to compare objects only toEqual() is to be used. 

### 4.4.3 toMatch()

This matcher is used for regular expressions. 

```js
var strReg = "The quick brown fox"; 
expect(strReg).toMatch(/The/); 
expect(strReg).not.toMatch(/jump/); 
```

### 4.4.4 toBeDefined()

This matcher checks if a variable or a function is defined. Let's check for the function we defined for addition: 

```js
expect(add).toBeDefined(); // will pass 
expect(add).not.toBeDefined(); // will not pass 
```

### 4.4.5 toBeUndefined()

This matcher does the opposite of toBeDefined(). 

```js
expect(add).toBeUndefined(); // will not pass 
expect(add).not.toBeUndefined(); // will pass 
```

### 4.4.6 toBeNull()

This matcher checks if a variable is null. 

```js
expect(a).not.toBeNull(); 
expect(null).toBeNull(); 
```

### 4.4.7 toBeTruthy()

This matcher checks if a variable or expression is true. 

```js
a = false; 
b = true; 
expect(b).toBeTruthy(); 
expect(a).not.toBeTruthy(); 
expect(add(2,3)).toBeTruthy(); 
```

### 4.4.8 toBeFalsy()

This matcher checks if a value or expression is false. 

```js
expect(add(0,0)).toBeFalsy(); 
expect(b).not.toBeFalsy(); 
```

### 4.4.9 toContain()

This matcher checks if a collection (array) has an item or not. 

```js
var fruits = ["apple", "orange", "grape","papaya", "peach", "banana" ]; 
expect(fruits).toContain("apple"); 
```

### 4.4.10 toBeLessThan()

This matcher is for the comparison of numbers in mathematics. 

```js
var a = 2, b = 3, c = 5.1234; 
expect(a).toBeLessThan(b); 
expect(c).not.toBeLessThan(a); 
```

In the first expect statement, it compares a to b and expects b would be greater than a. While in next statement, it expects c would not be less than a. 

### 4.4.11 toBeGreaterThan()

This matcher is the opposite of toBeLessThan(). 

```js
expect(b).toBeGreaterThan(a); 
expect(b).not.toBeGreaterThan(c); 
```

### 4.4.12 toBeCloseTo()

This matcher checks if a number is close to another number. This matcher takes two arguments, the first is the number and second is the decimal precision. Let's see the following example to understand this matcher: 

```js
expect(c).toBeCloseTo(5.1, 1) // will pass 
expect(c).not.toBeCloseTo(5.1, 2) // will pass 
```

Since c has a value 5.1234, it is compared to 5.1 that matches till the first digit. Thus, it passes for the first expectation. 

### 4.4.13 toThrow()

This matcher checks if a function throws an exception. 

```js
f1 = function() { 
    return 1 + 2; 
}; 
f2 = function() { 
    return undefinedVar + 1; 
}; 
expect(f1).not.toThrow(); 
expect(f2).toThrow(); 
```

### 4.4.14 toThrowError()

This matcher checks if an specific exception was thrown from a function. 

```js
f3 = function() { 
    throw new TypeError("A custom Exception from f3"); 
}; 
expect(f3).toThrowError("custom"); 
```

The preceding expectation will fail, as the strings do not match exactly. "custom" does not match "A custom Exception from f3". But the following expectation will pass, because it uses regular expression to match the strings: 

```js
expect(f3).toThrowError(/custom/); 
```

The following expectation checks using the exception type as well. It also takes an optional argument as a string or regular expression to match the string. 

```js
expect(f3).toThrowError(TypeError); // will pass, checks type 
expect(f3).toThrowError(TypeError, /custom/); // will pass 
expect(f3).toThrowError(TypeError, "custom exception"); // will fail 
```

### 4.4.15 jasmine.any()

Sometimes, we are unaware of the actual value of an expression, but know the type. In this case, we can match them using jasmine.any(). Let's see how this is used: 

```js
expect([12,323]).toEqual(jasmine.any(Array)); 
expect({}).toEqual(jasmine.any(Object)); 
expect(21312312).toEqual(jasmine.any(Number)); 
```

As we can see, jasmine.any will match the expected value to a type of class. 

### 4.4.16 jasmine.objectContaining()

We can also do partial match when it comes to key/pair values. Let's see the following example to see how it works: 

```js
var employee = { 
    name: "Alice", 
    age: 29, 
    department: "Testing", 
    grade: 5 
} 

expect(employee).toEqual(jasmine.objectContaining({ 
    department: "Testing" 
})); 
expect(employee).toEqual(jasmine.objectContaining({ 
    age: jasmine.any(Number) 
})); 
```

We can provide a key/value pair to match partially with an object. Sometimes, these default matchers are not enough to fulfill our requirements, and we need to create custom matchers. With Jasmine, we can create custom matchers, which you will learn later in this chapter. 

## 4.5 Set up and tear down 

Just like other frameworks, Jasmine also provides a way to set up and tear down. Jasmine provides global functions such as beforeEach—called before each spec, afterEach—called after each spec, beforeAll—called only once before all specs are run, and afterAll—called only once after all specs are done. Look at the following code to understand this: 

```js
describe('Setup and Teardown', () => {
    let count = 0;
    let velocity = 0;
    beforeEach(() => {
        velocity = 100;
        count++;
        console.log('Count is ' + count);
    });

    afterEach(() => {
        velocity = 0;
        console.log('Some spec just finished and this function is called');
    });

    beforeAll(() => {
        console.log('This is called only one, specs are about to run.');
    });

    afterAll(() => {
        console.log('All specs finished, time for cleanup');
    });

    it('Testing Velocity and reducing velocity', () => {
        expect(velocity).toEqual(100);
        velocity = 20;
        expect(velocity).toBe(20);
    })

    it('Testing Velocity', () => {
        expect(velocity).toEqual(100);
        expect(true).toEqual(true);
    });
});
```

If you run the following code, you will see all specs running successfully with status pass and the following will be the console output. The beforeAll and afterAll functions are run once during a run. We can see that the variable count is increased by 1 before each spec is run and velocity is set to 100 so that the first expectation of each spec is met true. 

This was one way of sharing variables among it, beforeEach, and afterEach. There is one more way using the this keyword, which is set to empty for each spec. Consider the following code: 

```js
describe('Setup and Teardown', () => {
    let count = 0;
    let velocity = 0;
    beforeEach(() => {
        this.velocity = 100;
    });

    afterEach(() => {
        this.velocity = 0;
    });

    it('Testing Velocity and reducing velocity', () => {
        expect(this.velocity).toEqual(100);
        this.velocity = 20;
        expect(this.velocity).toBe(20);
        this.acceleration = 5;
    })

    it('Testing Velocity', () => {
        expect(this.acceleration).toBeUndefined();
    });
});
```

Since the this keyword will be set to empty for the next spec, this.acceleration will not be defined. Running this suite will pass all the specs in it. 

## 4.6 Spies 

A spy is an emulation of a function or object, irrespective of which function/object is defined or not. There are times when we need stubs for the functions we need to use for performing testing. Jasmine has spies for this purpose. A spy can stub functions but can only exist within describe and it block if it is defined. 

Apart from the matchers we read in this chapter, there are special matchers just for spies. One is toHaveBeenCalled(), which returns true if the spy was called. Another one is toHaveBeenCalledWith(), which returns true if the spy was called with arguments. 

Let's see the following example to understand how spies work. The following is our source for an Employee function in the employee.js file created in the src folder: 

```js
let DEFAULT_SALARY = 1000;

function Employee(name, grade, department, salary) {
    this.name = name;
    this.grade = grade;
    this.department = department;

    this.salary = salary || 0;
}

// 此处不能用箭头函数
Employee.prototype.getName = function() {
    return this.name;
};
Employee.prototype.getDepartment = function() {
    return this.department;
};
Employee.prototype.getGrade = function() {
    return this.grade;
};
Employee.prototype.getSalary = function() {
    return this.salary;
};
Employee.prototype.calculateSalary = function() {
    return this.grade * DEFAULT_SALARY;
};

Employee.prototype.getDetails = function() {
    return 'Employee Name: ' + this.getName() + '\nDepartment: ' + this.getDepartment() +
    '\nGrade: ' + this.getGrade() + '\nSalary: ' + this.getSalary();
};
```

We need to print details of each employee. We want to be sure that the salary was calculated before employee details were printed. We create a spy using the spyOn() function and call this file spyEmployee.js. We then put it in the spec folder. 

```js
describe('Jasmine Spy', () => {
    it('Spying employee', () => {
        let alice = new Employee('Alice', 4, 'Testing');
        spyOn(alice, 'calculateSalary');
        console.log(alice.getDetails());
        expect(alice.calculateSalary).toHaveBeenCalled();
    });
});
```

We created a spy using spyOn(alice, "calculateSalary"), and then called the toHaveBeenCalled() matcher. As soon as we create a spy on the calculateSalary() function, Jasmine replaces the actual implementation. Now a spy will be called rather than an actual implementation. 

After running this HTML file, the following is the output: 

As we can see, it was expected that calculateSalary should have been called, but it failed since it was not called before printing the salary. Now let's change our code in employee.js and keep spec as it is: 

```js
var DEFAULT_SALARY = 1000;

function Employee(name, grade, department, salary) {
    this.name = name;
    this.grade = grade;
    this.department = department;

    this.salary = salary || 0;
}

// 此处不能用箭头函数
Employee.prototype.getName = function() {
    return this.name;
};

Employee.prototype.getDepartment = function() {
    return this.department;
};

Employee.prototype.getGrade = function() {
    return this.grade;
};

Employee.prototype.getSalary = function() {
    if (!this.salary) {
        this.salary = this.calculateSalary();
    }
    return this.salary;
}

Employee.prototype.calculateSalary = function() {
    return this.grade * DEFAULT_SALARY;
};

Employee.prototype.getDetails = function() {
    return 'Employee Name: ' + this.getName() + '\nDepartment: ' + this.getDepartment() +
    '\nGrade: ' + this.getGrade() + '\nSalary: ' + this.getSalary();
};
```

1『跑出来，发现 console 上，DEFAULT_SALARY 是 undefined，原因待解决。（2020-06-16）』

As we can see, calculateSalary is now being called from the getSalary() function. Let's run this again and see what happens: 

Now spec passed because it could find that the salary was calculated before printing details. In this example, we worked with the toHaveBeenCalled() matcher. There are several other matchers also defined for spies: 

• toHaveBeenCalledWith(): To understand this, let's modify method in employee.js: 

```js
Employee.prototype.calculateSalary = function(grade){ 
    this.grade = grade; this.salary = this.grade * DEFAULT_SALARY; 
} 
```

This method will take grade and set both the salary and grade for an employee. We know that it will call the calculateSalary() function without any argument, which we can see by our implementation. We add one more spec to check if this was called with or without arguments. 

```js
describe('Jasmine Spy', () => {
    it('Spying employee', () => {
        let alice = new Employee('Alice', 4, 'Testing');
        spyOn(alice, 'calculateSalary');
        console.log(alice.getDetails());
        // expect(alice.calculateSalary).toHaveBeenCalled();
        expect(alice.calculateSalary).toHaveBeenCalledWith(5);
    });
});
```

If we run our spec now, we can see that it will fail with message: Expected spy calculateSalary to have been called with [ 5 ] but actual calls were [ ]: 

We can chain the expectation with not as well: 

```js
expect(alice.calculateSalary).not.toHaveBeenCalledWith(5); 
```

After chaining with not, if you rerun the spec, it will pass. 






• callThrough(): Jasmine replaces actual implementation of a function on which spyOn() is called. Sometimes, there is a need of getting the actual output of a function. Chaining spyOn() with and.callThrough(), it is possible to run the actual implementation of a function. Using and. through() with spyOn(), makes our spec implementation as follows: 

```js
it("Spying employee with call through", function(){ 
var alice = new Employee("Alice", 4, "Testing"); spyOn(alice, "calculateSalary").and.callThrough(); var salary = alice.getSalary(); 
expect(alice.calculateSalary).toHaveBeenCalled(); console.log("Salary is :" + salary); expect(salary).toEqual(4000); 
}); 
```

The spec will pass since the calculateSalary() function was actually called inside getSalary(). 
• returnValue(): There are times when we want to always return a specific value from a function. In this case, after creating spy, we can chain it with and.returnValue(), which takes a value as an argument that will be returned. The following is the example of using returnValue(): 
it("Spying employee with return value", function(){ 
var alice = new Employee("Alice", 4, "Testing"); spyOn(alice, "calculateSalary").and.returnValue(9999); alice.calculateSalary(); expect(alice.calculateSalary).toHaveBeenCalled(); expect(alice.calculateSalary()).toEqual(9999); }); 
This spec will pass since the return value of calculateSalary() will always be 9999 in any case. This is helpful in cases when there are calls made to remote services via AJAX or any other means. Returning data takes time, and you want to make it skip the service calls. 
• callFake(): Sometimes, we may want to provide our own implementation of a function because the actual implementation takes time to execute or can be some other reason. In such cases, we can chain spyOn() with and. callFake(). callFake() takes a function as an argument, which is our implementation for the actual function name. The following spec will pass with this implementation: 
it("Spying employee with a fake call", function(){ var alice = new Employee("Alice", 4, "Testing"); spyOn(alice, "calculateSalary").and.callFake(function(grade){ var tSalary = 1000; return tSalary*grade; }); var salary = alice.calculateSalary(10); expect(alice.calculateSalary).toHaveBeenCalled(); expect(salary).toEqual(10000); }); 
• throwError(): When we want a function to throw an error, we can chain spyOn with and.throwError(), which takes a string as an argument that will be thrown upon call. In the following spec, we can see that calculateSalary is spied with the throw error and error "Service is down" is thrown when it is being called: 
it("Spying employee with throw error", function(){ 
var alice = new Employee("Alice", 4, "Testing"); spyOn(alice, "calculateSalary").and.throwError("Service is down"); 
expect(alice.calculateSalary).toThrowError("Service is down"); }); 
• stub(): There may be times when callThrough() is used already, but we want only stub to be called and not the actual implementation. In this case, we can use and.stub() as in the following code: 
it("Spying employee with call through and stub", function(){ var alice = new Employee("Alice", 4, "Testing"); 
spyOn(alice, "calculateSalary").and.callThrough(); var salary = alice.getSalary(); console.log("Salary is: "+salary); 
console.log("Now calling stub"); alice.calculateSalary.and.stub(); }); 
After the call to stub(), the effect of callThrough() will be removed. 

### 4.6.1 Tracking spies using calls 

There are several ways a spy can be tracked. For example, we can track if a spy was called or not, how many times, it was called, its arguments, its most recent call or first call and many more. Each and every call to a spy is tracked using the calls property. 
• calls.any(): This function returns true if a spy was called at least once, else returns false when a spy wasn't called at all. 
• calls.count(): This function returns a count of how many times a spy was called. 
• calls.argsFor(): This takes an index as an argument, which is call number. 
An array is returned with all the arguments passed to that call. 
• calls.allArgs(): This function returns the arguments passed to all of the calls. 
• calls.all(): This one returns the context and arguments passed to all of the calls. 
• calls.mostRecent(): This function returns the context and arguments passed to the most recent call. 
• calls.first(): This one returns the context and arguments passed to first call made to the spy. 
• calls.reset(): This function resets/clears all tracking properties for a spy. Let's see all of these in action: 
it("Tracking spies with calls property",function(){ var alice = new Employee("Alice", 4, "Testing"); 
spyOn(alice, "calculateSalary").and.callThrough(); var salary = alice.getSalary(); // calls calculateSalary 
alice.calculateSalary.and.stub(); salary = alice.getSalary(); // calls calculateSalary only if salary is zero expect(salary).toEqual(4000); 
expect(alice.calculateSalary.calls.any()).toEqual(true); expect(alice.calculateSalary.calls.count()).toEqual(1); console.log(alice.calculateSalary.calls.argsFor(0)); // returns blank [] expect(alice.calculateSalary.calls.argsFor(0)).toEqual([]); 
alice.calculateSalary(1000); 
console.log(alice.calculateSalary.calls.argsFor(1)); // returns array [1000] expect(alice.calculateSalary.calls.argsFor(1)) .toEqual([1000]); console.log(alice.calculateSalary.calls.allArgs()); // returns [[], [1000]] expect(alice.calculateSalary.calls.allArgs()).toEqual([[], [1000]]); 
console.log(alice.calculateSalary.calls.all()); // returns objects console.log(alice.calculateSalary.calls.mostRecent()); console.log(alice.calculateSalary.calls.first()); alice.calculateSalary.calls.reset(); expect(alice.calculateSalary.calls.any()).toEqual(false); 
}); 
All of these expectations are true and spec passes without fail. Output in the console would be as follows: 

### 4.6.2 Creating a custom spy 

We can create our own spy using the createSpy() function. This might be useful when we want to completely replace the original implementation and keep a stub or when there is no function defined yet to be spied upon. This spy will act as any other spy, and everything applies to it, for example, it can have arguments, it can be tracked, and so on. Let's see the following example: 
describe("Custom spy", function(){ 
var alice; beforeEach(function(){ alice = new Employee("Alice", 5, "Testing"); // creating a new spy for yet undefined function assignTask() alice.assignTask = jasmine.createSpy("assignTask"); 
alice.getName = jasmine.createSpy("getName").and.returnValue("Ms Alice"); 
}); 
it("Expect assignTask to be defined",function(){ expect(alice.assignTask).toBeDefined(); }); it("Expect assignTask to be called",function(){ 
alice.assignTask(); 
expect(alice.assignTask.calls.any()).toEqual(true); }); 
it("Expect assignTask to be called with arguments",function(){ alice.assignTask("Test the login of application"); expect(alice.assignTask.calls.argsFor(0)).toEqual(["Test the login of application"]); }); 
it("Expect name to be with title Mr or Ms", function(){ console.log(alice.getName()); expect(alice.getName()).toEqual("Ms Alice"); }) }); 
In the example, we created spy for a function named assignTask and tested it with various expectations. We also created a spy for getName to replace its original implementation. We can see after running the example that all of our expectations pass. We put this in a new spec file customSpy.js and include in our HTML file and run it.  
As we can see, all our specs passed. This is the way we can use jasmine.createSpy to create a custom spy. There is one more method, which will create an object with several methods. Using createSpyObj(), we can create a mock with multiple spies. Let's see the following spec to understand how it is created: 
describe("Custom spy object", function(){ var car; beforeEach(function(){ car = jasmine.createSpyObj('car', ['start','stop','openDoor']); car.start(); car.stop(); car.openDoor(); }); 
it("Expect car to be started",function(){ expect(car.start).toHaveBeenCalled(); }); it("Expect car to be stopped",function(){ 
expect(car.start).toHaveBeenCalled(); }); 
}); 
As we can see, createSpyObj() takes two arguments, first is the type or class and second is an array of strings. All of the strings in the array act as functions for which spies are created. In the previous example, a type car was created with three spies. All of these spies act as any other spy. 

## Jasmine clock
 
For cases, when we need to use the setTimeout() or setInterval() functions of JavaScript in our tests: Jasmine provides a clock that can make use of these functions available. 
jasmine.clock().install() installs a clock for our specs and jasmine.clock(). uninstall() restores the original JavaScript timer functions. Jasmine clock helps us handle time-dependent code using these functions. Let's see the following examples to understand how these work. 
Suppose we want to check if Alice, an employee, was available after an hour, we create a spy for the checkAvailabity() function for an employee object: 
var employee; 
beforeEach(function() { employee = new Employee("Alice", 5, "Testing"); employee.checkAvailability = jasmine. createSpy("checkAvailability"); jasmine.clock().install(); }); 
afterEach(function() { jasmine.clock().uninstall(); }); 
We installed clock in beforeEach() and uninstalled it in afterEach() so that the original JavaScript timer functions are restored. In the next spec, we are going to use setTimeout(), which will be called once. 
it("Checks if Alice is available after one hour", function() { 
// setting timeout for an hour 
setTimeout(function() { employee.checkAvailability() }, 60 * 60 * 1000); 
expect(employee.checkAvailability).not.toHaveBeenCalled(); 
// need to tick clock for 1 hour = 60 * 60 * 1000 milliseconds jasmine.clock().tick(60 * 60 * 1000); 
expect(employee.checkAvailability).toHaveBeenCalled(); }); 
The original behavior of setTimeout() will call employee.checkAvailability() after one hour. Jasmine spec is not going to wait till then, but it will assume that it was called after an hour. We use the jasmine.clock.tick() function to move the clock forward. This function takes milliseconds as an argument and will tick the clock to the specified milliseconds. All these calls go synchronously. To understand this further, let's see next spec, which uses setInterval(): 
it("Checks if Alice is available for next 3 hours", function() { setInterval(function() { employee.checkAvailability(); }, 60 * 60 * 1000); 
expect(employee.checkAvailability).not.toHaveBeenCalled(); 
jasmine.clock().tick(60 * 60 * 1000 + 1); expect(employee.checkAvailability.calls.count()).toEqual(1); 
jasmine.clock().tick(60 * 60 * 1000 + 1); expect(employee.checkAvailability.calls.count()).toEqual(2); 
jasmine.clock().tick(60 * 60 * 1000 + 1); expect(employee.checkAvailability.calls.count()).toEqual(3); }); 
In this spec, employee.checkAvailability() will be called after each hour. After each call, we ticked clock to an hour + 1 millisecond, and function is called again. These are useful when we need synchronous calls and want some specific object or value to be modified after each function call or in case of some service calls. 

## Creating a custom matcher 

In Chapter 2, Testing Concepts, we read that unit tests act as documentation to the project. In order for them to be descriptive, success and failure messages of tests should be very clear. But, sometimes, the default matchers as explained previously, are not sufficient or leave us with unexpected, unclear messages when fail or pass. For example, our expectation is: 
expect(employee.salary).toEqual(9000); 
This results in failure because the actual salary was 4,000. 
Expected 1000 to equal 9000. 
By looking at the message, you cannot detect what the context was. How about if it was something like: "Expected salary of employee was 9000 but found to be 4000". This message gives us an idea from the message itself that the salary calculated must be wrong. To overcome this, Jasmine supports a creation of custom matchers. 
Suppose we have a large number of employees in the context of a project and we need to check if an employee has marked his/her attendance daily. Our development requirements need to check if the employee is present on a particular day or not, and this is checked in the code from a good number of times. 
In this case, there is a property for each employee object, which holds the status-code of attendance on a daily basis. The following table shows the status code versus status: 
Code
Status
0
Not present
1
Present
2
On leave
3
Half day(first half present)
4
Half day(second half present)
5
Left organization permanently
To check if the employee is present full time, the following expectation would be good if it is rarely used in the project: 
expect(employee.get('attendanceStatus')).toEqual(1); 
But what if it was like this: 
expect(employee).toBePresentToday(); 
Sounds good, doesn't it? This is descriptive, clear, and serves the purpose. Let's create a custom matcher for this. 
First, let's modify our employee.js for attendance so that we can use it for our matcher: 
Employee.prototype.markAttendance = function(status){ this.attendanceStatus = status; }; Employee.prototype.getAttendance = function(){ 
return this.attendanceStatus; }; 
A custom matcher can also take an actual value and an optional expected value. Here, we are going to keep only one as we need only employee for which we will check internally for the status. Our custom matcher is: 
var customMatchers = { toBePresent: function(util, customEqualityTesters){ return{ compare : function(employee){ 
var statusCode = employee.getAttendance(); var result = {}; result.pass = util.equals(statusCode, 1 , customEqualityTesters); if(result.pass){ 
result.message = "Employee "+employee.getName()+" is 
present today"; }else{ 
result.message = "Employee "+employee.getName()+" is 
absent today"; } return result; 
} 
} 
} 
} 
We created a customMatchers array, which will hold all of our custom matchers. Then, we create a matcher isEmployeePresent(). While creating it, we give it two arguments, util and customEqualityTesters, that have a set of utility functions, which a matcher can use. Any call to util.equal() inside matcher needs a customEqualityTesters variable, which is second argument to the function. Then, we return the result of a compare function. This compare function does the actual comparison between values using the util.equals() function call. 
To use this matcher, in the beforeEach() block of our suite in describe, we register this matcher using jasmine.addMatchers(customMatchers). Once registered, it will be available for any expectation in the block. 
Our suite goes as follows: 
describe("Custom Matcher", function(){ 
beforeEach(function(){ jasmine.addMatchers(customMatchers); }); 
it("Expected employee to be present ", function(){ var alice = new Employee("Alice", 5, "Testing"); alice.markAttendance(2); console.log(alice); expect(alice).toBePresent(); }); }); 
All our custom matchers and suites go in the same file named customMatchers.js. Upon execution, our spec will fail, but the message will be descriptive and clear: 
As we can see, the custom message now appears after the execution. For negative equality check, we can chain expectations with a not just like default matchers. In that case, our expectation would be: 
expect(alice).not.toBePresent(); 
This is how a custom matcher is created and used. They behave like any other matcher. We passed only one argument to compare the function in matcher. In case we want to compare a user given actual and expected value, we just need to modify the function signature to two arguments and use the other argument for comparison. 

## Creating a custom equality tester 

Sometimes, you may want to compare two values or objects in your way. By defining a custom equality tester, you can modify how Jasmine determines if two values are equal or not. 
Whenever an expectation needs to check for equality, custom equality tester will first be used. It would return true or false if it knows how to compare; otherwise, undefined will be returned. If undefined is returned, then only Jasmine's default equality testers will be used. 
Let's modify employee.js once more to add setter getter for the e-mail so that we can use in our custom equality tester: 
Employee.prototype.setEmail = function(email){ this.email = email; } Employee.prototype.getEmail = function(){ 
return this.email; } 
To create a custom equality tester, we create a function which takes two arguments. Let's create an equality tester for employees. If two employee objects have same e-mail and name, we will consider them to be equal. So, our function goes as follows: 
customEqualityTester = function(employee1, employee2){ if(typeof employee1 !== typeof employee2 ){ return false; } return (employee1.getEmail() === employee2.getEmail()) && (employee1.getName() === employee2.getName()) }; 
Now when we have our function ready, we can register this function in beforeEach() using jasmine.addCustomEqualityTester(). After registration, this will be available, and we can use this in our specs. Let's put it all together in the customEquality.js file and run: 
customEqualityTester = function(employee1, employee2){ if(typeof employee1 !== typeof employee2 ){ return false; } return (employee1.getEmail() === employee2.getEmail()) && (employee1.getName() === employee2.getName()) } 
describe("Checking Employee equality tester", function(){ 
var employeeA, employeeB; beforeEach(function(){ jasmine.addCustomEqualityTester(customEqualityTester); 
employeeA = new Employee("Alice", 5, "Testing"); employeeA.setEmail("alice@example.com"); employeeB = new Employee("Alice", 4, "Development"); employeeB.setEmail("alice@example.com"); }); 
it("Should be equal", function(){ expect(employeeA).toEqual(employeeB); }); it("Should not be equal", function(){ var employeeC = new Employee("Bob", 5, "Testing"); employeeC.setEmail("bob@example.com"); expect(employeeA).not.toEqual(employeeC); }); }); 
The output of the execution would be: 
This is how we can extend Jasmine to use our own equality testers. 
Asynchronous calls 
There are websites, which heavily use AJAX calls to collect and present data. In such cases, it's useful to mock AJAX calls to make testing easy. But sometimes, actual AJAX calls are required, and with Jasmine, we can use asynchronous calls in our specs. Calls to beforeEach(), afterEach(), and it() can take an optional argument, done. This done() function should be called when asynchronous operations are completed: 
beforeEach(function(done) { // some asynchronous operation done();(); }); 
Once our operations are done, we call the done() function in beforeEach(): 
it("should perform some asynchronous operations", function(done) { // asynchronous operations // expectations done(); }); 
This spec will not be called until the done() function in beforeEach() is called and this spec will not complete until done is called in spec. By default Jasmine will wait for 5 seconds to complete asynchronous operation, in case we need more time or want to set less time, we can do this using jasmine.DEFAULT_TIMEOUT_INTERVAL. We can set this to the time as per our requirement. One important thing to note is that this this interval should be reset to Jasmine's default interval after spec is completed. So, if suppose it was set to 10 seconds in beforeEach(), we should set it to 5 seconds in afterEach(). 
The Jasmine Ajax plugin 
Jasmine also has a plugin written for mocking asynchronous operations. The plugin jasmine-ajax is available at GitHub at https://github.com/pivotal/ jasmine-ajax. To add this plugin, you need to download mock-ajax.js from the lib directory. The direct URL to download the JavaScript file is https://raw. githubusercontent.com/jasmine/jasmine-ajax/master/lib/mock-ajax.js. 
After adding the mock-ajax.js file to the HTML file (let's say testJasmineAjax. html), we can start using the plugin. This plugin mocks the actual asynchronous behavior and creates a mock of XMLHttpRequest by creating the FakeXMLHttpRequest object. 
If we want to provide AJAX support for the whole suite, we can add the jasmine. Ajax.install() function call to beforeEach the and jasmine.Ajax.uninstall() function call to afterEach. 
describe("Using mock-ajax for Asynchronous operations testing", function() { 
beforeEach(function() { jasmine.Ajax.install(); }); 
afterEach(function() { jasmine.Ajax.uninstall(); }); }); 
A call to jasmine.Ajax.uninstall() is important; because of this call, Jasmine restores the original behavior of Ajax calls so that other specs or parts of code, which want to make real Ajax calls can continue. 
Let's checkout the example spec, which uses async operation: 
it("Checking weather report AJAX API", function() { 
var successFunction = jasmine.createSpy("success"); var xhr = new XMLHttpRequest(); xhr.onreadystatechange = function(args) { 
if (this.readyState == this.DONE) { 
successFunction(this.responseText); 
} }; 
xhr.open("GET", "/get/weather/IN-Mumbai"); xhr.send(); 
expect(jasmine.Ajax.requests.mostRecent().url) .toBe('/get/weather/IN-Mumbai'); expect(successFunction).not.toHaveBeenCalled(); jasmine.Ajax.requests.mostRecent().respondWith({ "status": 200, "contentType": 'text/plain', "responseText": 'Temp 25 C, Sunlight' }); expect(successFunction).toHaveBeenCalledWith('Temp 25 C, Sunlight'); }); 
In the preceding spec, we first create a spy for the success function, which can be used to call the readyState once. The readyState of Ajax request is equal to DONE. jasmine.Ajax.requests.mostRecent() returns the object of FakeXMLHttpRequest. After that, we can use a normal Ajax call as we generally do. jasmine.Ajax.requests.MostRecent().url holds the recently called URL. Since this is mocking, we also need to provide a response. In the response, we need to provide the status, contentType and responseText, which should be string. 
These were the ways using which Jasmine allows to use actual AJAX calls or to mock AJAX calls in the specs. 

## Nesting suites 

As a project matures, the unit testing code grows huge and it's difficult to maintain. In such cases, it's good to use nested suites. Consider an example of a company, where employees are classified into several departments such as admin, finance, HR, delivery, presales, and sales. While there can be a common set of specs that apply to all employees, each department may also need some specs for departmentspecific features. Desk allocation can be task related to admin, while annual prize distribution can be a part of HR. Now all these specs can be grouped into suites, and all these suites can be clubbed into one suite for the whole company. We can nest suites by placing a describe block into another describe: 
describe("Testing Company wide functions", function(){ describe("Testing HR department functions", function(){ 
describe("Testing HR department functions - Prize Distribution", function(){ }); 
describe("Testing HR department functions - Offer Letter Distribution", function(){ }); describe("Testing HR department functions - New recruitment", function(){ }); }); describe("Testing Admin department functions", function(){ 
describe("Testing Admin department functions - Reception", function(){ }); describe("Testing Admin department functions - Pantry", function(){ }); }); describe("Testing Finance department functions", function(){ 
describe("Testing Finance department functions Reimbursement", function(){ }); describe("Testing Finance department functions - Salary", function(){ }); }); 
}); 
This allows suites to be like a tree of functions. When a spec is executed, it walks down the tree while executing each beforeEach(). Similarly after execution, the afterEach() functions are called. 
To understand this, let's see the following example: 
describe("Nested Suites - top suite", function(){ var count = 0; beforeEach(function(){ console.log("Count in top suite: "+count); count++; }); afterEach(function(){ console.log("Calling top afterEach"); }); it("Increases count", function(){ console.log(count); expect(true).toEqual(true); 
}); describe("Nested Suites - Inner suite", function(){ beforeEach(function(){ console.log("Count in Inner suite: "+count); count++; }); afterEach(function(){ console.log("Calling inner afterEach"); }); it("Increases count", function(){ console.log("Count : " +count); expect(true).toEqual(true); }); describe("Nested Suites - inner most suite", function(){ beforeEach(function(){ console.log("Count in inner most suite: "+count); count++; }); afterEach(function(){ console.log("Calling inner most afterEach"); }); it("Increases count", function(){ console.log("Count : " +count); expect(true).toEqual(true); }); }); }); }); 
When the inner most spec is called, the first top-most beforeEach() will be called, then the inner and inner-most beforeEach() will be called. Similar behavior is applicable for afterEach(). The output in the console log comes as follows: 
Count in top suite: 0 Count : 1 Calling top afterEach Count in top suite: 1 Count in Inner suite: 2 Count : 3 Calling inner afterEach Calling top afterEach Count in top suite: 3 Count in Inner suite: 4 Count in inner most suite: 5 
Count : 6 Calling inner most afterEach Calling inner afterEach Calling top afterEach 
Disabling suites and specs 
Sometimes, we may want to run only specific set of suites and skip all others. Suites that we want to skip can be disabled using xdescribe. For example: 
xdescribe("Disabled suite", function(){ it("A spec", function(){ expect(true).toBeTruthy(); }); }); 
Similarly we can skip specs as well using xit: 
describe("A suite", function() { 
it("A spec", function(){ expect(true).toBeTruthy(); }); xit("Another spec", function(){ 
}); xit("Disabled spec", function(){ 
}); }); 
Disabling is useful when we have so many specs created in a project, and we want to test only a specific functionality. It we put these all together and run, output will be as follows: 
Jasmine has a way, which enables us to run only one suite or spec. Just like we added x before describe and it, this plugin allows us to prefix f. So, if a spec is defined by fit rather than it, suites are fdescribe rather than describe. These specs declared with fit are known as focused specs: 
describe("A suite", function() { 
fit("focused spec and will run", function(){ expect(true).toBeTruthy(); }); it("Spec will not run", function(){ 
expect(true).toBeTruthy(); }); fdescribe("Focused suite", function() { 
it("Spec will run", function(){ 
expect(true).toBeTruthy(); 
}); }); 
}); 
In the preceding code, any spec declared with fit will run, and all the specs inside fdescribe will run. The rest of the specs will not run and will be marked as disabled. 
Another way to run only one spec/suite and skip all others is using the Jasmine test runner. By default, all suites and specs will run when the HTML file is loaded in a browser. We can click on one suite/spec to run only that suite/spec and skip the others. If the running suite has more suites inside, then all those suites will also run. 
All disabled suite and specs will not run and be marked as faded color in the spec runner. These specs are also called pending specs. Any spec without any expectations will also be marked as pending in results. 

## Summary 

Jasmine is considered to be very popular among testing frameworks. It is called to be complete and does not need any other supporting frameworks. In this chapter, you learned about the Jasmine testing framework and its offerings. You also learned how to extend Jasmine using custom spies, matchers, and equality testers with the help of the employee object. 

In the next chapter, you will learn about JsTestDriver, its setup, and how we can run our Jasmine specs with it. We will also see how to perform Ajax operations in tests later in this book. 

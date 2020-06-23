## 记忆时间

## 卡片

### 0101. 主题卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡——

根据反常识，再补充三个证据——就产生三张术语卡。

例子。

### 0202. 术语卡——

### 0203. 术语卡——

### 0301. 人名卡——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

维基百科链接：有的话。

#### 01. 基本信息

用一句话描述你对这个大牛的印象。

#### 02. 贡献及著作

### 0401. 金句卡——JS 里的 class 关键字是语法糖

### 0501. 任意卡——数组的常用操作

更详细的可以参考官方文档：[索引集合类 (Indexed collections) - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Indexed_collections#map%E6%95%B0%E7%BB%84)。

1、数据流开发时的几个应用场景。map() 根据单体号映射数组，然后通过 Set 去重，最后 Set 转数组。

2、过滤函数 filter() 应用场景实在太多了，传入一个回调函数，在回调函数里对每一个数组子项 item 进行筛选，逻辑判断为 ture 的话，该子项筛选出来。还有个 find() 方法，它仅仅返回第一个判断为 ture 的子项。

```js
// 获取单项号，map 映射数组，并通过 Set 去重
getMonomer(data) {
  let temp = data.map(item => item.project_id);
  this.restaurants = new Set(temp);
  // Set 转数组
  this.restaurants = [...this.restaurants];
},
// 获取特定单项号的数据
getMonomerData() {
  this.confirmdata = this.roomdata.filter(item => item.project_id === this.searchvalue);
  console.log(this.confirmdata);
},
```

3、数组内各元素求和。用 reduce() 函数，传一个回调函数进去，数据流开发里的一个例子：

```js
  let tempSystem = {};
  tempSystem.system_normal_exhaust = this.roomData.filter(item => item.is_system)
  .map(item => item.min_frequency)
  .reduce((aggregated, item) => aggregated + item, 0);
  this.systemData.push(tempSystem);
```

## 模板

### 1. 逻辑脉络

用自己的话总结主题，梳理逻辑脉络，也就是这本书整个地图里这一章所在的节点。

### 2. 摘录及评论

## 书评

### 01

如果你觉得自己的 js 水平不错了，可以看看这本书。这本书虽然只是 meap 版，但是也够你看一段时间，里面有太多的东西需要慢慢体会。这本书以函数为中心（函数也确实是 js 的核心），对函数的讲解非常全面细致，涉及到函数的定义、扩展、重载、curry 化、闭包、重定向、继承等方方面面，还有在 js 书籍里很少涉及的对计数器的解释，比如各个浏览器在最小时间间隔上的区别，比如 setTimeout 和 setInterval 的区别。其他的对正则表达式、命名空间、浏览器最新实现 CSS 选择器都有很好的解释。

### 02

提起该书的作者 John Resig，恐怕没人不知道。用过 jQuery 的朋友，相信知道该库的妙处。读完该书之后，我们就能明白 John Resig 为什么能构建出 jQuery 库。书中对函数、闭包等做了详尽的分析，尤其对我们经常忽视的 Timer 作了详尽的分析。值得细读、深读。

### 03

写这条评论就是想提醒一下有兴趣的读者，别被书名骗了，别被其他评论那股 vibe 骗了，这是一本新手友好的书，可以作为你的第一本 js 书。优点：1）可能因为 js 本身特性和作者组织编排得当，就这么几个大的要点，大点打通小点全通。看完你会觉得你都记住了，在编程书中较为难得。2）示例代码各种图表，注释，色框，看了示例代码，就不用看正文的讲解了。3）新，注重 web 下的使用和 ES6 新特性。

### 04

书名《JavaScript 忍者秘籍》，作者呢是大名鼎鼎的 jQuery 的创作者。这本书里介绍了各种「忍者级」JS 用法，收益颇丰。总体来说，这本书适合中级 JS 开发者。作者的许多代码，就体现了他在设计 jQuery 时的编程思想，非常有价值。

附：本评论的阅读体验更友好的地址（我的博客里）：[JavaScript Ninja | 王子龙的博客](http://borninsummer.com/2016/09/20/javascript-ninja/)

第 3 章，函数是根基。函数的 name 属性，有别于函数表达式的变量名，它是函数声明时指定的。第 4 章，挥舞函数。函数名是一个有趣的概念，它的本质是 token，与变量名、对象属性名一样，都有各自的可见范围。函数声明可以使得该函数在其所在的词法作用域内在任意处访问到。函数表达式里，如果 function 关键字后面带有函数名，那么该函数名字只能被自己的函数体内访问到，外部都不可见。例如：

```js
var a = function b() {
  console.log(b.name);
}; 

a(); // b
b(); // Uncaught ReferenceError: b is not defined
```

而且函数名是一个优先级比较弱的标识符，函数的形参名会在函数体内覆盖函数名：

```js
var a = function b(b) {
  console.log(b.name);
};
a(); // Uncaught TypeError: Cannot read property 'name' of undefined
```

而在将对象的属性指向一个函数时，如果将函数进行命名，那么其行为与函数表达式一样。这样的函数被称为内联命名函数。72 页的一段代码非常有趣，对象的方法可以调用数组原型方法，例如 Array.prototype.push.call (this, objectB)，然后如果这个对象有个 length 属性，那么这个原型方法呢就会将 length 值加 1，并且给对象添加一个数字属性，对象通过 [index] 访问这个数字属性，就可以访问到刚刚添加的对象 objectB。

4.4 函数重载方式。重载函数是函数的一种特殊情况，为方便使用，C++ 允许在同一范围中声明几个功能类似的同名函数，但是这些同名函数的形式参数（指参数的个数、类型或者顺序）必须不同，也就是说用同一个运算符完成不同的运算功能。这就是重载函数。重载函数常用来实现功能类似而所处理的数据类型不同的问题。—— 来自百度百科

这本书给出的 JS 实现函数重载的技术与 C++ 不同，但是思路是一样的：根据形参来、直观地重载；充分利用闭包来保存函数链。

```js
/**
 * 用于给对象添加重载方法的方法
 * @param {[type]}   object [description]
 * @param {[type]}   name   [description]
 * @param {Function} fn     [description]
 */
function addMethod(object, name, fn) {
  var old = object[name];
  object[name] = function() {
    if (fn.length === arguments.length) {
      return fn.apply(this, arguments);
    } else if (Object.prototype.toString.call(old) === '[object Function]') {
      return old.apply(this, arguments);
    }
  };
}

/**
 * 定义一个测试对象
 */
var ninjas = {
  values: ['a', 'b', 'c']
};

/**
 * 第一个是不带任何参数的方法
 */
addMethod(ninjas, 'find', function() {
  return this.values;
});

/**
 * 第二个方法带有一个字符串参数
 */
addMethod(ninjas, 'find', function(str) {
  return this.values.filter(item => (item === str));
});

console.log(ninjas.find());  // ["a", "b", "c"]

console.log(ninjas.find('c'));  // [c"]
```

Jhon Resig 自夸说：** 这是个绝佳的技巧，因为这些绑定函数实际上并没有存储于任何典型的数据结构中，而是在闭包里作为引用进行存储。的确很巧妙。

第 5 章，闭包。传统上来说，闭包是纯函数式编程语言的一个特性。让闭包跨越到主流语言的开发商尤其令人鼓舞，因为它们能够大大简化复杂的操作，所以很容易在一些 JavaScript 库以及其他高级代码库中找到闭包的使用。

89 页倒数第二段其实有个错误，原文是：「第二点和第三点解释了为什么内部闭包可以访问到变量 tooLate，而外部闭包不行。」其实由于 var 关键字对变量的声明提升作用，两种「闭包」是都可以访问到 tooLate 这个标识符的。不同之处只是在于对其取右值时拿到的值不同而已。如果真的是访问不到这个变量，那么会报 ReferenceError （引用错误，这是一种运行时错误）。很明显，tooLate 的值为 undefined，与访问 tooLate 时抛出 ReferenceError 相比，还是有很大区别的。

第 8 章，驯服线程和定时器。同一个 interval 处理程序的多个实例不能同时进行排队。因此，setInterval 的有些回调可能就被废弃掉了。减少同时使用的定时器的数量，将有助于解决这种问题（卡顿），这就是为什么所有现代动画引擎都使用一种称为中央定时器控制（central timer control）的技术。一个完整的中央定时器控制示例代码：

```js
<!DOCTYPE html>
<html>
<head>
  <title>test timer control</title>
  <style type="text/css">
    #box {
      position: relative;
      border: 1px solid #999;
      display: inline-block;
      height: 100px;
      width: 100px;
    }
  </style>
</head>
<body>
<div id="box"></div>
</body>
</html>

<script type="text/javascript">
var timers = {
    timerID: 0,
    timers: [],

    add: function(fn) { 
        this.timers.push(fn);
    },

    start: function() {
        if(this.timerID) return;
        (function runNext() {
            if(timers.timers.length > 0) {
               for (var i = 0; i < timers.timers.length; i++) {
                 if(timers.timers[i]() === false) {
                   timers.timers.splice(i,1);
                   i--;
                 }
              } 

          timers.timerID = setTimeout(runNext, 0);
       }
     })();
    },

    stop: function() {
        clearTimeout(this.timerID);
        this.timerID = 0;
    }
};

var box = document.getElementById("box"), x = 0, y = 20;
timers.add(function() {
    box.style.left = x + "px";
    if(++x > 50) return false;
});

timers.add(function() { 
    box.style.top = y + "px";
    y += 1;
    if (y > 120) return false;
});

timers.start();
</script>
```

第 11 章，开发跨浏览器策略。这一章提到了一个概念，「贪婪 ID 复制」。例如下面的例子所示的：

第 12 章，洞悉特性、属性和样式。要知道，元素的 attribute（特性）与 property（属性）并非同一个东西。大多数时候相应的读写操作会有相同的结果，但也有例外。而且，二者在性能上也有较大的差别。属性操作往往要比特性操作快很多。例如下面的性能测试代码：

```js
<!DOCTYPE html>
<html>
<body>
  <input type="text" id="test-1">
</body>

<script type="text/javascript">
  var NUM = 5000000;
  var input = document.getElementById('test-1');
  var value;

  console.time('test-1');
  for (var i = 0; i < NUM; i++) {
    value = input.getAttribute('value');
  }
  console.timeEnd('test-1');


  console.time('test-2');
  for (var i = 0; i < NUM; i++) {
    value = input.value;
  }
  console.timeEnd('test-2');

</script>
</html>
```

结果是：

```
test-1: 231ms
test-2: 117ms
```

差别非常明显。另外一个例子是 URL 规范化。

```js
<a href="test.html" id="test-subject">test</a>

var link = document.getElementById('test-subject');
var linkHref_1 = link.getAttributeNode('href').nodeValue;  // test.html
var linkHref_2 = link.getAttribute('href');  // test.html
var linkHref_3 = link.href;  // file:///Users/wzl/Desktop/test.html
```

获取计算样式。广播一条 API：W3C 标准 API 里有一个可以获得元素的计算样式的方法：window.getComputedStyle(element)。IE > 8 可用。

第 15 章，CSS 选择器引擎。W3C Selectors API，主要就是两个方法： querySelector() 和 querySelectorAll()。比较有趣的事情是这几个：

1、在今天来看，W3C Selectors API 其实已经有着非常好的浏览器覆盖率了。IE 系列是「Partial support in IE8」，其他浏览器基本百分比支持。

2、这两个 API 都可以在 Document、documentFragment、Element 这三类 DOM 节点上面发起调用。发起调用的那个节点叫做 context node（The term context node refers to the node upon which the method was invoked. 参考：[Selectors API Level 1](https://www.w3.org/TR/selectors-api/)）。

3、querySelector 返回的是第一个匹配的元素，querySelectorAll 返回的是所有匹配的元素组成的静态 NodeList。这里的为了找到「第一个」所采用遍历策略，是按照文档顺序（document order）进行查找匹配的。文档顺序是指「a depth-first pre-order traversal of the DOM tree or subtree in question」，即深度优先、先序遍历，这样可以与HTML文本的顺序一致。附：深度遍历的三种遍历图如下（参考：Tree Traversal | wiki pedia）：

4、有个小陷阱，下面的代码依然可以命中那个 strong 元素。这是因为对 querySelector/querySelectorAll 而言，无论指定 context node 为什么，其搜索总是从 document 根节点发起。只不过其返还结果里面会根据上下文节点进行过滤而已。

```html
<body>
  <div id="test-selector">
    <strong>strong text</strong>
  </div>
  <div>div</div>
</body>

var testDiv = document.getElementById('test-selector');
testDiv.querySelector('div strong');  // 可以命中那个 strong 元素
```

### 07

这是一本 JavaScript 进阶书，翻译也比较地道。本书是由 jQuery 的创建者和《jQuery 实战》的作者合著的。全书从实际的实践中出发，对测试，函数、闭包、正则、定时器、事件，跨浏览器的 DOM 编程等内容，娓娓道来，内容清晰明了。同时对 JavaScript 编程中存在的陷阱以及规避的办法还有一些非常有用的小技巧穿插在其中，非常精彩，让我在阅读的过程中好几次为作者的巧妙思路而喝彩。总之如果你有了一定 JavaScript 基础，想要进一步提升自己的水平的话，看完这本书一定会让你受益匪浅，写起 JavaScript 代码来底气也更足。

## 0601. Functions for the future: generators and promises

### Summary

1. Generators are functions that generate sequences of values—not all at once, but on a per request basis.

2. Unlike standard functions, generators can suspend and resume their execution. After a generator has generated a value, it suspends its execution without blocking the main thread and patiently waits for the next request.

3. A generator is declared by putting an asterisk (\*) after the function keyword. Within the body of the generator, we can use the new yield keyword that yields a value and suspends the execution of the generator. If we want to yield to another generator, we use the yield\* operator.

4. Calling a generator creates an iterator object through which we control the execution of the generator. We request new values from the generator by using the iterator’s next method, and we can even throw exceptions into the generator by calling the iterator’s throw method. In addition, the next method can be used to send in values to the generator.

5. A promise is a placeholder for the results of a computation; it’s a guarantee that eventually we’ll know the result of the computation, most often an asynchronous computation. A promise can either succeed or fail, and after it has done so, there will be no more changes.

6. Promises significantly simplify our dealings with asynchronous tasks. We can easily work with sequences of interdependent asynchronous steps by using the then method to chain promises. Parallel handling of multiple asynchronous steps is also greatly simplified; we use the Promise.all method.

7. We can combine generators and promises to deal with asynchronous tasks with the simplicity of synchronous code.

This chapter covers: 1) Continuing function execution with generators. 2) Handling asynchronous tasks with promises. 3) Achieving elegant asynchronous code by combining generators and promises.

In the previous three chapters, we focused on functions, specifically on how to define functions and how to use them to great effect. Although we’ve introduced some ES6 features, such as arrow functions and block scopes, we’ve mostly been exploring features that have been part of JavaScript for quite some time. This chapter tackles the cutting edge of ES6 by presenting generators and promises, two completely new JavaScript features. Generators and promises are both introduced by ES6. You can check out current browser support at http://mng.bz/sOs4 and [[ECMAScript 6 compatibility table](http://kangax.github.io/compat-table/es6/#test-Promise)].

1『作者在 6.3.4 小结里讲解了如何用 promise 对象实现从后端请求数据，值得反复研究。』

Generators are a special type of function. Whereas a standard function produces at most a single value while running its code from start to finish, generators produce multiple values, on a per request basis, while suspending their execution between these requests. Although new in JavaScript, generators have existed for quite some time in Python, PHP, and C#.

Generators are often considered an almost weird or fringe language feature not often used by the average programmer. Though most of this chapter’s examples are designed to teach you how generator functions work, we’ll also explore some practical aspects of generators. You’ll see how to use generators to simplify convoluted loops and how to take advantage of generators’ capability to suspend and resume their execution, which can help you write simpler and more elegant asynchronous code.

Promises, on the other hand, are a new, built-in type of object that help you work with asynchronous code. A promise is a placeholder for a value that we don’t have yet but will at some later point. They’re especially good for working with multiple asynchronous steps.

In this chapter, you’ll see how both generators and promises work, and we’ll finish off by exploring how to combine them to greatly simplify our dealings with asynchronous code. But before going into the specifics, let’s take a sneak peek into how much more elegant our asynchronous code can be.

What are some common uses for a generator function? Why are promises better than simple callbacks for asyn-chronous code? Do you know? You start a number of long-running tasks with Promise .race. When does the promise resolve? When would it fail to resolve?




## 0701. Object orientation with prototypes

### Summary 

1. JavaScript objects are simple collections of named properties with values. 

2. JavaScript uses prototypes. 

3. Every object can have a reference to a prototype, an object to which we delegate the search for a particular property, if the object itself doesn’t have the searched-for property. An object’s prototype can have its own prototype, and so on, forming a prototype chain. 

3. We can define the prototype of an object by using the Object.setPrototypeOf method. 

4. Prototypes are closely linked to constructor functions. Every function has a prototype property that’s set as the prototype of objects that it instantiates. 

5. A function’s prototype object has a constructor property pointing back to the function itself. This property is accessible to all objects instantiated with that function and, with certain limitations, can be used to find out whether an object was created by a particular function. 

6. In JavaScript, almost everything can be changed at runtime, including an object’s prototypes and a function’s prototypes! 

7. If we want the instances created by a Ninja constructor function to “inherit” (more accurately, have access to) properties accessible to instances created by the Person constructor function, set the prototype of the Ninja constructor to a new instance of the Person class. 

8. In JavaScript, properties have attributes (configurable, enumerable, writable). These properties can be defined by using the built-in Object.defineProperty method. JavaScript ES6 adds support for a class keyword that enables us to more easily mimic classes. Behind the scenes, prototypes are still in play! 

9. The extends keyword enables elegant inheritance. 

This chapter covers: 1) Exploring prototypes. 2) Using functions as constructors. 3) Extending objects with prototypes. 3) Avoiding common gotchas. 4) Building classes with inheritance.

You’ve learned that functions are first-class objects in JavaScript, that closures make them incredibly versatile and useful, and that you can combine generator functions with promises to tackle the problem of asynchronous code. Now we’re ready to tackle another important aspect of JavaScript: object prototypes.

A prototype is an object to which the search for a particular property can be delegated to. Prototypes are a convenient means of defining properties and functionality that will be automatically accessible to other objects. Prototypes serve a similar purpose to that of classes in classical object-oriented languages. Indeed, the main use of prototypes in JavaScript is in producing code written in an object-oriented way, similar to, but not exactly like, code in more conventional, class-based languages such as Java or C#.

In this chapter, we’ll delve into how prototypes work, study their connection with constructor functions, and see how to mimic some of the object-oriented features often used in other, more conventional object-oriented languages. We’ll also explore a new addition to JavaScript, the class keyword, which doesn’t exactly bring fullfeatured classes to JavaScript but does enable us to easily mimic classes and inheritance. Let’s start exploring.

How do you test whether an object has access to a particular property?  Why is a prototype chain important for working with objects in JavaScript?  Do ES6 classes change how JavaScript works with objects? 

### 7.1 Understanding prototypes

In JavaScript, objects are collections of named properties with values. For example, we can easily create new objects with object-literal notation: 

```js
let obj = { 
    prop1: 1, 
    prop2: function(){}, 
    prop3: {} 
} 
```

As we can see, object properties can be simple values (such as numbers or strings), functions, and even other objects. In addition, JavaScript is a highly dynamic language, and the properties assigned to an object can be easily changed by modifying and deleting existing properties: 

```js
obj.prop1 = 1; 
// Assigns a value of a completely different type, here an array 
obj.prop1 = []; 
//Removes the property from the object 
delete obj.prop2; 
```

We can even add completely new properties: 

```js
obj.prop4 = "Hello"; 
```

In the end, all these modifications have left our simple object in the following state: 

```js
{ 
    prop1: [], 
    prop3: {}, 
    prop4: "Hello" 
}; 
```

When developing software, we strive not to reinvent the wheel, so we want to reuse as much code as possible. One form of code reuse that also helps organize our programs is inheritance, extending the features of one object into another. In JavaScript, inheritance is implemented with prototyping. 

1『 JS 里对象的继承是通过原型实现的，class 关键字声明类也只是对原型的一种抽象，是一种语法糖。』

The idea of prototyping is simple. Every object can have a reference to its prototype, an object to which the search for a particular property can be delegated to, if the object itself doesn’t have that property. Imagine that you’re in a game quiz with a group of people, and that the game show host asks you a question. If you know the answer, you give it immediately, and if you don’t, you ask the person next to you. It’s as simple as that. Let’s take a look at the following listing. 

Listing 7.1 With prototypes, objects can access properties of other objects 

```js
// Creates three objects, each with its own property 
const yoshi = { skulk: true }; 
const hattori = { sneak: true }; 
const kuma = { creep: true }; 

// yoshi has access to only its own, skulk, property. 
assert("skulk" in yoshi, "Yoshi can skulk"); 
assert(!("sneak" in yoshi)), "Yoshi cannot sneak"); 
assert(!("creep" in yoshi)), "Yoshi cannot creep"); 

// Use the Object .setPrototypeOf method to set one object as the prototype of another object. 
Object.setPrototypeOf(yoshi, hattori); 

// By setting hattori as yoshi’s prototype, yoshi now has access to hattori’s properties. 
assert("sneak" in yoshi, "Yoshi can now sneak"); 
// Currently, hattori can’t creep. 
assert(!("creep" in hattori)), "Hattori cannot creep"); 

// Sets kuma as a prototype of hattori 
Object.setPrototypeOf(hattori, kuma); 
// Now hattori has access to creep. 
assert("creep" in hattori, "Hattori can now creep"); 
// yoshi also has access to creep, through hattori. 
assert("creep" in yoshi, "Yoshi can also creep"); 
```

In this example, we start by creating three objects: yoshi, hattori, and kuma. Each has one specific property accessible only to that object: Only yoshi can skulk, only hattori can sneak, and only kuma can creep. See figure 7.1. 

To test whether an object has access to a particular property, we can use the in operator. For example, executing skulk in yoshi returns true, because yoshi has access to the skulk property; whereas executing sneak in yoshi returns false. 

In JavaScript, the object’s prototype property is an internal property that’s not directly accessible (so we mark it with [[prototype]]). Instead, the built-in method Object.setPrototypeOf takes in two object arguments and sets the second object as the prototype of the first. For example, calling Object.setPrototypeOf(yoshi, hattori); sets up hattori as a prototype of yoshi. 

1『对象的原型属性不能被直接访问。那该如何访问呢。（2020-05-29）』

As a result, whenever we ask yoshi for a property that it doesn’t have, yoshi delegates that search to hattori. We can access hattori’s sneak property through yoshi. See figure 7.2. 

We can do a similar thing with hattori and kuma. By using the Object.setPrototypeOf method, we can set kuma as the prototype of hattori. If we then ask hattori for a property that he doesn’t have, that search will be delegated to kuma. In this case, hattori now has access to kuma’s creep property. See figure 7.3. 

It’s important to emphasize that every object can have a prototype, and an object’s prototype can also have a prototype, and so on, forming a prototype chain. The search delegation for a particular property occurs up the whole chain, and it stops only when there are no more prototypes to explore. For example, as shown in figure 7.3, asking yoshi for the value of the creep property triggers the search for the property first in yoshi. Because the property isn’t found, yoshi’s prototype, hattori, is searched. Again, hattori doesn’t have a property named creep, so hattori’s prototype, kuma, is searched, and the property is finally found. 

Now that we have a basic idea of how the search for a particular property occurs through the prototype chain, let’s see how prototypes are used when constructing new objects with constructor functions. 

### 7.2 Object construction and prototypes 

The simplest way to create a new object is with a statement like this: 

```js
const warrior = {}; 
```

This creates a new and empty object, which we can then populate with properties via assignment statements: 

```js
const warrior = {}; 
warrior.name = 'Saito'; 
warrior.occupation = 'marksman'; 
```

But those coming from an object-oriented background might miss the encapsulation and structuring that comes with a class constructor, a function that serves to initialize an object to a known initial state. After all, if we’re going to create multiple instances of the same type of object, assigning the properties individually isn’t only tedious but also highly error-prone. We’d like to be able to consolidate the set of properties and methods for a class of objects in one place. 

JavaScript provides such a mechanism, though in a different form than most other languages. Like object-oriented languages such as Java and C++, JavaScript employs the new operator to instantiate new objects via constructors, but there’s no true class definition in JavaScript. Instead, the new operator, applied to a constructor function (as you saw in chapter 3), triggers the creation of a newly allocated object. 

1『 JS 里没有真正意义上的类定义，它是通过 new 操作符结合构造函数实现类似于「类定义」的功能，ES6 出来的 class 关键词也是这种实现的封装，是语法糖。』

What we didn’t learn in the previous chapters was that every function has a prototype object that’s automatically set as the prototype of the objects created with that function. Let’s see how that works in the following listing. 

Listing 7.2 Creating a new instance with a prototyped method 

```js
// Defines a function that does nothing and returns nothing 
function Ninja(){} 
// Every function has a built-in prototype object, which we can freely modify. 
Ninja.prototype.swingSword = function(){ 
    return true; 
}; 

// Calls the function as a function. Testing confirms that nothing at all seems to happen. 
const ninja1 = Ninja(); 
assert(ninja1 === undefined, "No instance of Ninja created."); 

// Calls the function as a constructor. Testing confirms that not only is a new object instance created, but it possesses the method from the prototype of the function. 
const ninja2 = new Ninja(); 
assert(ninja2 && 
            ninja2.swingSword && 
            ninja2.swingSword(), 
            "Instance exists and method is callable." ); 

```

In this code, we define a seemingly do-nothing function named Ninja that we’ll invoke in two ways: as a “normal” function, const ninja1 = Ninja(); and as a constructor, const ninja2 = new Ninja();. 

When the function is created, it immediately gets a new object assigned to its prototype object, an object that we can extend just like any other object. In this case, we add a swingSword method to it: 

```js
Ninja.prototype.swingSword = function(){ 
    return true; 
}; 
```

Then we put the function through its paces. First we call the function normally and store its result in variable ninja1. Looking at the function body, we see that it returns no value, so we’d expect ninja1 to test as undefined, which we assert to be true. As a simple function, Ninja doesn’t appear to be all that useful. 

Then we call the function via the new operator, invoking it as a constructor, and something completely different happens. The function is once again called, but this time a newly allocated object has been created and set as the context of the function (and is accessible through the this keyword). The result returned from the new operator is a reference to this new object. We then test that ninja2 has a reference to the newly created object, and that that object has a swingSword method that we can call. See figure 7.4 for a glimpse of the current application state. 

1. Every function has a prototype object. 

2. A function’s prototype has a constructor property that references back to the function. 

3. The constructor object’s prototype is set as the prototype of the newly created object. 

1『每个构造函数，这里是 Ninja，都有一个原型对象。2 个要点：1）通过 Ninja 构造函数构造出来的对象 ninja2，其原型是构造函数的原型对象。2）Ninja 构造函数的原型对象里有一个 constructor 属性，其值是指向构造函数本身的。』

Figure 7.4 Every function, when created, gets a new prototype object. When we use a function as a constructor, the constructed object’s prototype is set to the function’s prototype. 

As you can see, a function, when created, gets a new object that’s assigned to its prototype property. The prototype object initially has only one property, constructor, that references back to the function (we’ll revisit the constructor property later). 

When we use a function as a constructor (for example, by calling new Ninja()), the prototype of the newly constructed object is set to the object referenced by the constructor function’s prototype. 

In this example, we’ve extended the Ninja.prototype with the swingSword method, and when the ninja2 object is created, its prototype property is set to Ninja’s prototype. Therefore, when we try to access the swingSword property on ninja2, the search for that property is delegated to the Ninja prototype object. Notice that all objects created with the Ninja constructor will have access to the swingSword method. Now that’s code reuse! 

The swingSword method is a property of the Ninja’s prototype, and not a property of ninja instances. Let’s explore this difference between instance properties and prototype properties. 

#### 7.2.1 Instance properties 

When the function is called as a constructor via the new operator, its context is defined as the new object instance. In addition to exposing properties via the prototype, we can initialize values within the constructor function via the this parameter. Let’s examine the creation of such instance properties in the next listing. 

1『构造函数通过 new 调用时，构造函数的上下文「EC」被定义为新构造出来的对象实例。沿着这个思路，可以在构造函数里，通过原型暴露属性、通过 this 值进行参数初始化。』

Listing 7.3 Observing the precedence of initialization activities 

```js
// Creates an instance variable that holds a Boolean value initialized to false 
function Ninja() { 
this.swung = false; 
// Creates an instance method that returns the inverse of the swung instance variable value 
this.swingSword = function() { 
    return !this.swung; 
    }; 
} 

// Defines a prototype method with the same name as the instance method. Which will take precedence? 
Ninja.prototype.swingSword = function() { 
    return this.swung; 
}; 

// Constructs a Ninja instance and asserts that the instance method will override the prototype method of the same name 
const ninja = new Ninja(); 
assert(ninja.swingSword(), "Called the instance method, not the prototype method."); 
```

Listing 7.3 is similar to the previous example in that we define a swingSword method by adding it to the prototype property of the constructor: 

```js
Ninja.prototype.swingSword = function() { 
    return this.swung; 
}; 
```

But we also add an identically named method within the constructor function itself: 

```js
function Ninja() { 
this.swung = false; 
this.swingSword = function(){ 
    return !this.swung; 
    }; 
} 
```

The two methods are defined to return opposing results so we can tell which will be called. 

NOTE: This isn’t anything we’d advise doing in real-world code; quite the opposite. We’re doing it here just to demonstrate the precedence of properties. 
 
When you run the test, you see that it passes! This shows that instance members will hide properties of the same name defined in the prototype. See figure 7.5. 

Figure 7.5 If a property can be found on the instance itself, the prototype isn’t even consulted! 

Within the constructor function, the this keyword refers to the newly created object, so the properties added within the constructor are created directly on the new ninja instance. Later, when we access the property swingSword on ninja, there’s no need to traverse the prototype chain (as shown in figure 7.4); the property created within the constructor is immediately found and returned (see figure 7.5). This has an interesting side effect. Take a look at figure 7.6, which shows the state of the application if we create three ninja instances. 

Figure 7.6 Every instance gets its own version of the properties created within the constructor, but they all have access to the same prototype’s properties. 

As you can see, every ninja instance gets its own version of the properties that were created within the constructor, while they all have access to the same prototype’s properties. This is okay for value properties (for example, swung) that are specific to each object instance. But in certain cases it might be problematic for methods. 

In this example, we’d have three versions of the swingSword method that all perform the same logic. This isn’t a problem if we create a couple of objects, but it’s something to pay attention to if we plan to create large numbers of objects. Because each method copy behaves the same, creating multiple copies often doesn’t make sense, because it only consumes more memory. Sure, in general, the JavaScript engine might perform some optimizations, but that’s not something to rely on. From that perspective, it makes sense to place object methods only on the function’s prototype, because in that way we have a single method shared by all object instances. 

NOTE: Remember chapter 5 on closures: Methods defined within constructor functions allow us to mimic private object variables. If this is something we need, specifying methods within constructors is the only way to go. 

#### 7.2.2 Side effects of the dynamic nature of JavaScript 

You’ve already seen that JavaScript is a dynamic language in which properties can be easily added, removed, and modified at will. The same thing holds for prototypes, both function prototypes and object prototypes. See the following listing. 

Listing 7.4 With prototypes, everything can be changed at runtime 

```js
function Ninja() { 
    this.swung = true; 
} 
const ninja1 = new Ninja(); 

Ninja.prototype.swingSword = function() { 
    return this.swung; 
}; 
assert(ninja1.swingSword(), "Method exists, even out of order."); 

// Completely overrides the Ninja’s prototype with a new object via the pierce method 
Ninja.prototype = { 
    pierce: function() { 
        return true; 
    } 
} 

// Even though we’ve completely replaced the Ninja constructor’s prototype, our Ninja can still swing a sword, because it keeps a reference to the old Ninja prototype. 
assert(ninja1.swingSword(), "Our ninja can still swing!"); 

const ninja2 = new Ninja(); 
// Newly created ninjas reference the new prototype, so they can pierce but can’t swing. 
assert(ninja2.pierce(),"Newly created ninjas can pierce"); 
assert(!ninja2.swingSword, "But they cannot swing!"); 
```

Figure 7.7 After construction, ninja1 has the property swung, and its prototype is the Ninja prototype that has only a constructor property. 

Here we again define a Ninja constructor and proceed to use it to create an object instance. The state of the application at this moment is shown in figure 7.7. 

After the instance has been created, we add a swingSword method to the prototype. Then we run a test to show that the change we made to the prototype after the object was constructed takes effect. The current state of the application is shown in figure 7.8. 

Figure 7.8 Because the ninja1 instance references the Ninja prototype, even changes made after the instance was constructed are accessible. 

Figure 7.9 The function’s prototype can be replaced at will. The already constructed instances reference the old prototype! 

Later, we override the Ninja function’s prototype by assigning it to a completely new object that has a pierce method. This results in the application state shown in figure 7.9. 

As you can see, even though the Ninja function doesn’t reference the old Ninja prototype, the old prototype is still kept alive by the ninja1 instance, which can still, through the prototype chain, access the swingSword method. But if we create new objects after this prototype switcheroo, the state of the application will be as shown in figure 7.10. 

The reference between an object and the function’s prototype is established at the time of object instantiation. Newly created objects will have a reference to the new prototype and will have access to the pierce method, whereas the old, pre-prototype-change objects keep their original prototype, happily swinging their swords. 

We’ve explored how prototypes work and how they’re related to object instantiation. Well done! Now take a quick breath, so we can continue onward by learning more about the nature of those objects. 

Figure 7.10 All newly created instances reference the new prototype. 

#### 7.2.3 Object typing via constructors 

```js
function Ninja(){} 
const ninja1 = new Ninja(); 
```

Figure 7.11 The prototype object of each function has a constructor property that references the function. 

Although it’s great to know how JavaScript uses the prototype to find the correct property references, it’s also handy to know which function constructed an object instance. As you’ve seen earlier, the constructor of an object is available via the constructor property of the constructor function prototype. For example, figure 7.11 shows the state of the application when we instantiate an object with the Ninja constructor. 

By using the constructor property, we can access the function that was used to create the object. This information can be used as a form of type checking, as shown in the next listing. 

Listing 7.5 Examining the type of an instance and its constructor 

```js
function Ninja() {} 
const ninja = new Ninja(); 

// Tests the type of ninja via typeof. This tells us it’s an object, but not much else. 
assert(typeof ninja === "object", "The type of the instance is object."); 

// Tests the type of ninja via instanceof. This provides more information—that it was constructed from Ninja. 
assert(ninja instanceof Ninja, "instanceof identifies the constructor." ); 

// Tests the type of ninja via the constructor reference. This gives a reference to the constructor function. 
assert(ninja.constructor === Ninja, "The ninja object was created by the Ninja function."); 
```

1『 typeof 可以后面直接加参数，不用 typeof()，instanceof 的用法也注意下。』

We define a constructor and create an object instance using it. Then we examine the type of the instance by using the typeof operator. This doesn’t reveal much, as all instances will be objects, thus always returning object as the result. Much more interesting is the instanceof operator, which gives us a way to determine whether an instance was created by a particular function constructor. You’ll learn more about how the instanceof operator works later in the chapter. 

In addition, we can use the constructor property, that we now know is accessible to all instances, as a reference to the original function that created it. We can use this to verify the origin of the instance (much as we can with the instanceof operator). Additionally, because this is just a reference to the original constructor, we can instantiate a new Ninja object using it, as shown in the next listing. 

Listing 7.6 Instantiating a new object using a reference to a constructor 

```js
function Ninja() {} 
const ninja = new Ninja(); 
// Constructs a second Ninja from the first 
const ninja2 = new ninja.constructor(); 

// Proves the new object’s Ninja-ness 
assert(ninja2 instanceof Ninja, "It's a Ninja!"); 
// They aren’t the same object, but two distinct instances. 
assert(ninja !== ninja2, "But not the same Ninja!"); 
```

Here we define a constructor and create an instance using that constructor. Then we use the constructor property of the created instance to construct a second instance. Testing shows that a second Ninja has been constructed and that the variable doesn’t merely point to the same instance. 

What’s especially interesting is that we can do this without even having access to the original function; we can use the reference completely behind the scenes, even if the original constructor is no longer in scope. 

1『通过被构建出来的对象的 constructor 绕过原始的构造函数直接再构建新对象，这个实现的应用价值应该很大。跟继承有关？』

NOTE: Although the constructor property of an object can be changed, doing so doesn’t have any immediate or obvious constructive purpose (though we might be able to think of some malicious ones). The property’s reason for being is to indicate from where the object was constructed. If the constructor property is overwritten, the original value is lost. 

That’s all useful, but we’ve just scratched the surface of the superpowers that prototypes confer on us. Now things get interesting. 

### 7.3 Achieving inheritance 

Inheritance is a form of reuse in which new objects have access to properties of existing objects. This helps us avoid the need to repeat code and data across our code base. In JavaScript, inheritance works slightly differently than in other popular object-oriented languages. Consider the following listing, in which we attempt to achieve inheritance. 

Listing 7.7 Trying to achieve inheritance with prototypes 

```js
// Defines a dancing Person via a constructor and its prototype 
function Person() {} 
Person.prototype.dance = function() {}; 

// Defines a Ninja 
function Ninja() {} 
// Attempts to make Ninja a dancing Person by copying the dance method from the Person prototype 
Ninja.prototype = { 
    dance: Person.prototype.dance 
}; 

const ninja = new Ninja(); 
assert(ninja instanceof Ninja, "ninja receives functionality from the Ninja prototype" ); 
assert(ninja instanceof Person, "... and the Person prototype" ); 
assert(ninja instanceof Object, "... and the Object prototype" ); 
```

Because the prototype of a function is an object, there are multiple ways of copying functionality (such as properties or methods) to effect inheritance. In this code, we define a Person and then a Ninja. And because a Ninja is clearly a person, we want Ninja to inherit the attributes of Person. We attempt to do so by copying the dance property of the Person prototype’s method to a similarly named property in the Ninja prototype. 

Running our test reveals that although we may have taught the ninja to dance, we failed to make the Ninja a Person, as shown in figure 7.12. We taught the Ninja to mimic the dance of a person, but that hasn’t made the Ninja a Person. That’s not inheritance—it’s just copying. 

Apart from the fact that this approach isn’t exactly working, we’d also need to copy each property of Person to the Ninja prototype individually. That’s no way to do inheritance. Let’s keep exploring. 

What we really want to achieve is a prototype chain so that a Ninja can be a Person, and a Person can be a Mammal, and a Mammal can be an Animal, and so on, all the way to Object. The best technique for creating such a prototype chain is to use an instance of an object as the other object’s prototype: 

```js
SubClass.prototype = new SuperClass(); 
```

For example: 

```js
Ninja.prototype = new Person(); 
```

1『大赞，「人」的实例化对象赋值给「忍者」的原型。』

This preserves the prototype chain, because the prototype of the SubClass instance will be an instance of the SuperClass, which has a prototype with all the properties of SuperClass, and which will in turn have a prototype pointing to an instance of its superclass, and on and on. In the next listing, we change listing 7.7 slightly to use this technique. 

Listing 7.8 Achieving inheritance with prototypes 

```js
function Person() {} 
Person.prototype.dance = function() {}; 

function Ninja() {} 
// Makes a Ninja a Person by making the Ninja prototype an instance of Person 
Ninja.prototype = new Person(); 

const ninja = new Ninja(); 
assert(ninja instanceof Ninja, "ninja receives functionality from the Ninja prototype"); 
assert(ninja instanceof Person, "... and the Person prototype"); 
assert(ninja instanceof Object, "... and the Object prototype"); 
assert(typeof ninja.dance === "function", "... and can dance!") 
```

The only change to the code is to use an instance of Person as the prototype for Ninja. Running the tests shows that we’ve succeeded, as shown in figure 7.13. Now we’ll take a closer look at the inner workings by looking at the state of the application after we’ve created the new ninja object, as shown in figure 7.14. 

Figure 7.14 We’ve achieved inheritance by setting the prototype of the Ninja constructor to a new instance of a Person object. 

Figure 7.14 shows that when we define a Person function, a Person 

prototype is also created that references the Person function through its constructor property. Normally, we can extend the Person prototype with additional properties, and in this case, we specify that every person, created with the Person constructor, has access to the dance method: 

1『当 Person 构造函数通过 constructor 属性引用其自身时，也创建了其原型对象。』

```js
function Person() {} 
Person.prototype.dance = function() {}; 
```

We also define a Ninja function that gets its own prototype object with a constructor property referencing the Ninja function: function Ninja() {}. 

Next, in order to achieve inheritance, we replace the prototype of the Ninja function with a new Person instance. Now, when we create a new Ninja object, the internal prototype property of the newly created ninja object will be set to the object to which the current Ninja prototype property points to, the previously constructed Person instance: 

```js
function Ninja() {} 
Ninja.prototype = new Person(); 
var ninja = new Ninja(); 
```

When we try to access the dance method through the ninja object, the JavaScript runtime will first check the ninja object itself. Because it doesn’t have the dance property, its prototype, the person object, is searched. The person object also doesn’t have the dance property, so its prototype is searched, and the property is finally found. This is how to achieve inheritance in JavaScript! 

Here’s the important implication: When we perform an instanceof operation, we can determine whether the function inherits the functionality of any object in its prototype chain. 

NOTE: Another technique that may have occurred to you, and that we advise strongly against, is to use the Person prototype object directly as the Ninja prototype, like this: Ninja.prototype = Person.prototype. Any changes to the Ninja prototype will then also change the Person prototype (because they’re the same object), and that’s bound to have undesirable side effects. 

An additional happy side effect of doing prototype inheritance in this manner is that all inherited function prototypes will continue to live-update. Objects that inherit from the prototype always have access to the current prototype properties. 

1『所有继承的函数原型将实时更新，继承原型的对象总是可以访问当前的原型属性。这个只是点目前没吃透。』

#### 7.3.1 The problem of overriding the constructor property 

If we take a closer look at figure 7.14, we’ll see that by setting the new Person object as a prototype of the Ninja constructor, we’ve lost our connection to the Ninja constructor that was previously kept by the original Ninja prototype. This is a problem, because the constructor property can be used to determine the function with which the object was created. Somebody using our code could make a perfectly reasonable assumption that the following test will pass: 

```js
assert(ninja.constructor === Ninja, "The ninja object was created by the Ninja constructor"); 
```

But in the current state of the application, this test fails. As figure 7.14 shows, if we search the ninja object for the constructor property, we won’t find it. So we go over to its prototype, which also doesn’t have a constructor property, and again, we follow the prototype and end up in the prototype object of Person, which has a constructor property referencing the Person function. In effect, we get the wrong answer: If we ask the ninja object which function has constructed it, we’ll get Person as the answer. This can be the source of some serious bugs. 

It’s up to us to fix this situation! But before we can do that, we have to take a detour and see how JavaScript enables us to configure properties. 

In JavaScript, every object property is described with a property descriptor through which we can configure the following keys: 

1. configurable—If set to true, the property’s descriptor can be changed and the property can be deleted. If set to false, we can do neither of these things. 

2. enumerable—If set to true, the property shows up during a for-in loop over the object’s properties (we’ll get to the for-in loop soon). 

3. value—Specifies the value of the property. Defaults to undefined. 

4. writable—If set to true, the property value can be changed by using an assignment. 

5. get—Defines the getter function, which will be called when we access the property. Can’t be defined in conjunction with value and writable. 

6. set—Defines the setter function, which will be called whenever an assignment is made to the property. Also can’t be defined in conjunction with value and writable. 

Say we create a property through a simple assignment, for example: 

```js
ninja.name = "Yoshi"; 
```

This property will be configurable, enumerable, and writable, its value will be set to Yoshi, and functions get and set would be undefined. 

When we want to fine-tune our property configuration, we can use the built-in Object.defineProperty method, which takes an object on which the property will be defined, the name of the property, and a property descriptor object. As an example, take a look at the following code. 

Listing 7.9 Configuring properties 

```js
// Creates an empty object; uses assignments to add two properties 
var ninja = {}; 
ninja.name = "Yoshi"; 
ninja.weapon = "kusarigama"; 

// The built-in Object.defineProperty method is used to fine-tune the property configuration details. 
Object.defineProperty(ninja, "sneaky", { 
    configurable: false, 
    enumerable: false, 
    value: true, 
    writable: true 
}); 

assert("sneaky" in ninja, "We can access the new property"); 

// Uses the for-in loop to iterate over ninja’s enumerable properties 
for(let prop in ninja) { 
    assert(prop !== undefined, "An enumerated property: " + prop); 
} 

```

We start with the creation of an empty object, to which we add two properties: name and weapon, in the good old-fashioned way, by using assignments. Next, we use the built-in Object.defineProperty method to define the property sneaky, which isn’t configurable, isn’t enumerable, and has its value set to true. This value can be changed because it’s writable. Finally, we test that we can access the newly created sneaky property, and we use the for-in loop to go through all enumerable properties of the object. Figure 7.15 shows the result. 

Figure 7.15 Properties name and weapon will be visited in the for-in loop, whereas our specially added sneaky property won’t (even though we can access it normally). 

By setting enumerable to false, we can be sure that the property won’t appear when using the for-in loop. To understand why we’d want to do something like this, let’s go back to the original problem. 

FINALLY SOLVING THE PROBLEM OF OVERRIDING THE CONSTRUCTOR PROPERTY 

When trying to extend Person with Ninja (or to make Ninja a subclass of Person), we ran into the following problem: When we set a new Person object as a prototype to the Ninja constructor, we lose the original Ninja prototype that keeps our constructor property. We don’t want to lose the constructor property, because it’s useful for determining the function used to create our object instances and it might be expected by other developers working on our code base. 

We can solve this problem by using the knowledge that we’ve just obtained. We’ll define a new constructor property on the new Ninja.prototype by using the Object.defineProperty method. See the following listing. 

Listing 7.10 Fixing the constructor property problem 

```js
function Person() {} 
Person.prototype.dance = function() {}; 
function Ninja() {} 
Ninja.prototype = new Person(); 

// We define a new nonenumerable constructor property pointing back to Ninja. 
Object.defineProperty(Ninja.prototype, "constructor", { 
    enumerable: false, 
    value: Ninja, 
    writable: true
}); 

var ninja = new Ninja(); 

// We’ve reestablished the connection. 
assert(ninja.constructor === Ninja, "Connection from ninja instances to Ninja constructor reestablished!"); 
// We haven’t added any enumerable properties to the Ninja.prototype. 
for(let prop in Ninja.prototype) { 
    assert(prop === "dance", "The only enumerable property is dance!"); 
} 
```

Now if we run the code, we’ll see that everything is peachy. We’ve reestablished the connection between ninja instances and the Ninja function, so we can know that they were constructed by the Ninja function. In addition, if anybody tries to loop through the properties of the Ninja.prototype object, we’ve made sure that our patched-on property constructor won’t be visited. Now that’s the mark of a true ninja; we went in, did our job, and got out, without anybody noticing anything from the outside! 

#### 7.3.2 The instanceof operator 

In most programming languages, the straightforward approach for checking whether an object is a part of a class hierarchy is to use the instanceof operator. For example, in Java, the instanceof operator works by checking whether the object on the left side is either the same class or a subclass of the class type on the right. 

Although certain parallels could be made with how the instanceof operator works in JavaScript, there’s a little twist. In JavaScript, the instanceof operator works on the prototype chain of the object. For example, say we have the following expression: 

```js
ninja instanceof Ninja 
```

The instanceof operator works by checking whether the current prototype of the Ninja function is in the prototype chain of the ninja instance. Let’s go back to our persons and ninjas, for a more concrete example. 

Listing 7.11 Studying the instanceof operator 

```js
function Person() {} 
function Ninja() {} 
Ninja.prototype = new Person(); 
const ninja = new Ninja(); 

// A ninja instance is both a Ninja and a Person. 
assert(ninja instanceof Ninja, "Our ninja is a Ninja!"); 
assert(ninja instanceof Person, "A ninja is also a Person. "); 
```

As expected, a ninja is, at the same time, a Ninja and a Person. But, to nail down this point, figure 7.16 shows how the whole thing works behind the scenes. 

Figure 7.16 The prototype chain of a ninja instance is composed of a new Person() object and the Person prototype. 

The prototype chain of a ninja instance is composed of a new Person() object, through which we’ve achieved inheritance, and the Person prototype. When evaluating the expression ninja instanceof Ninja, the JavaScript engine takes the prototype of the Ninja function, the new Person() object, and checks whether it’s in the prototype chain of the ninja instance. Because the new Person() object is a direct prototype of the ninja instance, the result is true. 

In the second case, where we check ninja instanceof Person, the JavaScript engine takes the prototype of the Person function, the Person prototype, and checks whether it can be found in the prototype chain of the ninja instance. Again, it can, because it’s the prototype of our new Person() object, which, as we’ve already seen, is the prototype of the ninja instance. 

And that’s all there is to know about the instanceof operator. Although its most common use is in providing a clear way to determine whether an instance was created by a particular function constructor, it doesn’t exactly work like that. Instead, it checks whether the prototype of the right-side function is in the prototype chain of the object on the left. Therefore, there is a caveat that we should be careful about. 

THE INSTANCEOF CAVEAT 

As you’ve seen multiple times throughout this chapter, JavaScript is a dynamic language in which we can modify a lot of things during program execution. For example, there’s nothing stopping us from changing the prototype of a constructor, as shown in the following listing. 

Listing 7.12 Watch out for changes to constructor prototypes 

```js
function Ninja() {} 
const ninja = new Ninja();
assert(!(ninja instanceof Ninja), "The ninja is now not a Ninja!?"); 

// We change the prototype of the Ninja constructor function. 
Ninja.prototype = {}; 
assert(ninja instanceof Ninja, "Our ninja is a Ninja!"); 
// Even though our ninja instance was created by the Ninja constructor, the instanceof operator now says that ninja isn’t an instance of Ninja anymore! 
```

In this example, we again repeat all the basic steps of making a ninja instance, and our first test goes fine. But if we change the prototype of the Ninja constructor function after the creation of the ninja instance, and again test whether ninja is an instanceof Ninja, we’ll see that the situation has changed. This will surprise us only if we cling to the inaccurate assumption that the instanceof operator tells us whether an instance was created by a particular function constructor. If, on the other hand, we take the real semantics of the instanceof operator—that it checks only whether the prototype of the function on the right side is in the prototype chain of the object on the left side—we won’t be surprised. This situation is shown in figure 7.17. 

Figure 7.17 The instanceof operator checks whether the prototype of the function on the right is in the prototype chain of the object on the left. Be careful; the function’s prototype can be changed anytime! 

1『重点警惕的是，一个构造函数的原型在运行时的过程中可以任意的被修改。』

Now that we understand how prototypes work in JavaScript, and how to use prototypes in conjunction with constructor functions to implement inheritance, let’s move on to a new addition in the ES6 version of JavaScript: classes. 

### 7.4 Using JavaScript “classes” in ES6 

It’s great that JavaScript lets us use a form of inheritance via prototypes. But many developers, especially those from a classical object-oriented background, would prefer a simplification or abstraction of JavaScript’s inheritance system into one that they’re more familiar with. 

This inevitably leads toward the realm of classes, even though JavaScript doesn’t support classical inheritance natively. As a response to this need, several JavaScript libraries that simulate classical inheritance have popped up. Because each library implements classes in its own way, the ECMAScript committee has standardized the syntax for simulating class-based inheritance. Notice how we said simulating. Even though now we can use the class keyword in JavaScript, the underlying implementation is still based on prototype inheritance! 

NOTE: The class keyword has been added to the ES6 version of JavaScript, and not all browsers implement it (see http://mng.bz/3ykA for current support). 

Let’s start by studying the new syntax. 

#### 7.4.1 Using the class keyword 

ES6 introduces a new class keyword that provides a much more elegant way of creating objects and implementing inheritance than manually implementing it ourselves with prototypes. Using the class keyword is easy, as shown in the following listing. 

1『既然 ES6 帮忙封装了用原型模拟基于类的面向对象，那以后果断用它的封装来声明类，即使用 calss 关键字。声明的时候有封装的，简单且同意，但在运行时的过程中可以自由的再切换回基于原型的语法，目前自己是这么考虑的，哈哈。（2020-05-30）』

Listing 7.13 Creating a class in ES6 

```js
// Uses the class keyword to start specifying an ES6 class 

class Ninja { 
    // Defines a constructor function that will be called when we call the class with the keyword new 
    constructor(name) { 
        this.name = name; 
    } 
    // Defines an additional method accessible to all Ninja instances 
    swingSword() { 
        return true; 
    } 
} 

// Instantiates a new ninja object with the keyword new 
var ninja = new Ninja("Yoshi"); 

// Tests for the expected behavior 
assert(ninja instanceof Ninja, "Our ninja is a Ninja"); 
assert(ninja.name === "Yoshi", "named Yoshi"); 
assert(ninja.swingSword(), "and he can swing a sword"); 
```

Listing 7.13 shows that we can create a Ninja class by using the class keyword. When creating ES6 classes, we can explicitly define a constructor function that will be invoked when instantiating a Ninja instance. In the constructor’s body, we can access the newly created instance with the this keyword, and we can easily add new properties, such as the name property. Within the class body, we can also define methods that will be accessible to all Ninja instances. In this case, we’ve defined a swingSword method that returns true. Next we can create a Ninja instance by calling the Ninja class with the keyword new, just as we would if Ninja was a simple constructor function (as earlier in the chapter). Finally, we can test that the ninja instance behaves as expected, that it’s an instanceof Ninja, has a name property, and has access to the swingSword method.

CLASSES ARE SYNTACTIC SUGAR 

As mentioned earlier, even though ES6 has introduced the class keyword, under the hood we’re still dealing with good old prototypes; classes are syntactic sugar designed to make our lives a bit easier when mimicking classes in JavaScript. 
Our class code from listing 7.13 can be translated to functionally identical ES5 code: 

```js
function Ninja(name) { 
    this.name = name; 
} 
Ninja.prototype.swingSword = function() { 
    return true; 
}; 
```

As you can see, there’s nothing especially new with ES6 classes. The code is more elegant, but the same concepts are applied. 

STATIC METHODS 

In the previous examples, you saw how to define object methods (prototype methods), accessible to all object instances. In addition to such methods, classical object-oriented languages such as Java use static methods, methods defined on a class level. Check out the following example. 

1『传统的基于类的面向对象里，静态方法是基于「类」这个层级的方法，根据这个类实例化后的对象都可以访问该方法。』

Listing 7.14 Static methods in ES6 

```js
class Ninja { 
    constructor(name, level) { 
        this.name = name; 
        this.level = level; 
    } 
    swingSword() { 
        return true; 
    } 
    // Uses the static keyword to make a static method 
    static compare(ninja1, ninja2) { 
        return ninja1.level - ninja2.level; 
    } 
} 

var ninja1 = new Ninja("Yoshi", 4); 
var ninja2 = new Ninja("Hattori", 3); 

// ninja instances don’t have access to compare. 
assert(!("compare" in ninja1) && !("compare" in ninja2), "A ninja instance doesn't know how to compare"); 

// The class Ninja has access to the compare method. 
assert(Ninja.compare(ninja1, ninja2) > 0, "The Ninja class can do the comparison!"); 

assert(!("swingSword" in Ninja), "The Ninja class cannot swing a sword"); 
```

We again create a Ninja class that has a swingSword method accessible from all ninja instances. We also define a static method, compare, by prefixing the method name with the keyword static. The compare method, which compares the skill levels of two ninjas, is defined on the class level, and not the instance level! Later we test that this effectively means that the compare method isn’t accessible from ninja instances but is accessible from the Ninja class.

We can also look at how “static” methods can be implemented in pre-ES6 code. For this, we have to remember only that classes are implemented through functions. Because static methods are class-level methods, we can implement them by taking advantage of functions as first-class objects, and adding a method property to our constructor function, as in the following example: 

```js
function Ninja() {} 
// Extends the constructor function with a method to mimic static methods in pre-ES6 code 
Ninja.compare = function(ninja1, ninja2) {...} 
```

Now let’s move on to inheritance. 

#### 7.4.2 Implementing inheritance 

To be honest, performing inheritance in pre-ES6 code can be a pain. Let’s go back to our trusted Ninjas, Persons example: 

```js
function Person() {} 
Person.prototype.dance = function() {}; 

function Ninja() {} 
Ninja.prototype = new Person(); 

Object.defineProperty(Ninja.prototype, "constructor", { 
    enumerable: false, 
    value: Ninja, 
    writable: true 
}); 
```

1『上面是 ES6 之前，基于原型的面向对象，实现对象继承的完整代码。』

There’s a lot to keep in mind here: Methods accessible to all instances should be added directly to the prototype of the constructor function, as we did with the dance method and the Person constructor. If we want to implement inheritance, we have to set the prototype of the derived “class” to the instance of the base “class.” In this case, we assigned a new instance of Person to Ninja.prototype. Unfortunately, this messes up the constructor property, so we have to manually restore it with the Object.defineProperty method. This is a lot to keep in mind when trying to achieve a relatively simple and commonly used feature (inheritance). Luckily, with ES6, all of this is significantly simplified. Let’s see how it’s done in the following listing. 

Listing 7.15 Inheritance in ES6 

```js
class Person { 
    constructor(name) { 
        this.name = name; 
    } 
    dance() { 
        return true; 
    } 
} 

// Uses the extends keyword to inherit from another class 
class Ninja extends Person { 
    constructor(name, weapon) { 
    // Uses the super keyword to call the base class constructor 
    super(name); 
    this.weapon = weapon; 
    } 

    wieldWeapon() { 
        return true; 
    } 
} 

var person = new Person("Bob"); 

assert(person instanceof Person, "A person's a person"); 
assert(person.dance(), "A person can dance."); 
assert(person.name === "Bob", "We can call it by name."); 
assert(!(person instanceof Ninja), "But it's not a Ninja"); 
assert(!("wieldWeapon" in person), "And it cannot wield a weapon"); 

var ninja = new Ninja("Yoshi", "Wakizashi"); 
assert(ninja instanceof Ninja, "A ninja's a ninja"); 
assert(ninja.wieldWeapon(), "That can wield a weapon"); 
assert(ninja instanceof Person, "But it's also a person"); 
assert(ninja.name === "Yoshi" , "That has a name"); 
assert(ninja.dance(), "And enjoys dancing"); 
```

Listing 7.15 shows how to achieve inheritance in ES6; we use the extends keyword to inherit from another class. In this example, we create a Person class with a constructor that assigns a name to each Person instance. We also define a dance method that will be accessible to all Person instances. Next we define a Ninja class that extends the Person class. It has an additional weapon property, and a wieldWeapon method.

In the constructor of the derived, Ninja class, there’s a call to the constructor of the base, Person class, through the keyword super. This should be familiar, if you’ve worked with any class-based language. We continue by creating a person instance and checking that it’s an instance of the Person class that has a name and can dance. Just to be sure, we also check that a person who isn’t a Ninja can’t wield a weapon.

We also create a ninja instance and check that it’s an instance of Ninja and can wield a weapon. Because every ninja is also a Person, we check that a ninja is an instance of Person, that it has a name, and that it also, in the interim of fighting, enjoys dancing.

See how easy this is? There’s no need to think about prototypes or the side effects of certain overridden properties. We define classes and specify their relationship by using the extends keyword. Finally, with ES6, hordes of developers coming from languages such as Java or C# can be at peace. And that’s it. With ES6, we build class hierarchies almost as easily as in any other, more conventional object-oriented language. 

## 0801. Controlling access to objects

### Summary

1. We can monitor our objects with getters, setters, and proxies.

2. By using accessor methods (getters and setters), we can control access to object properties.

    – Accessor properties can be defined by using the built-in Object.defineProperty method or with a special get and set syntax as parts of object literals or ES6 classes.

    – A get method is implicitly called whenever we try to read, whereas a set method is called whenever we assign a value to the matching object’s property.

    – Getter methods can be used to define computed properties, properties whose value is calculated on a per request basis, whereas setter methods can be used to achieve data validation and logging.

3. Proxies are an ES6 addition to JavaScript and are used to control other objects.

    – Proxies enable us to define custom actions that will be executed when an object is interacted with (for example, when a property is read or a function is called).

    – All interactions have to go through the proxy, which has traps that are triggered when a specific action occurs.

4. Use proxies to achieve elegant.

    – Logging.

    – Performance measurements.

    – Data validation.

    – Autopopulating object properties (thereby avoiding pesky null exceptions).

    – Negative array indexes. 

5. Proxies aren’t fast, so be careful when using them in code that’s executed a lot. We recommend that you do performance testing.

This chapter covers: 1) Using getters and setters to control access to object properties. 2) Controlling access to objects through proxies. 3) Using proxies for cross-cutting concerns.

In the previous chapter, you saw that JavaScript objects are dynamic collections of properties. We can easily add new properties, change the values of properties, and even completely remove existing properties. In many situations (for example, when validating property values, logging, or displaying data in the UI), we need to be able to monitor exactly what’s going on with our objects. So in this chapter, you’ll learn techniques for controlling access to and monitoring all of the changes that occur in your objects.

We’ll start with getters and setters, methods that control access to specific object properties. You first saw these methods in action in chapters 5 and 7. In this chapter, you’ll see some of their built-in language support and how to use them for logging, performing data validation, and defining computed properties. 

We’ll continue with proxies, a completely new type of object introduced in ES6. These objects control access to other objects. You’ll learn how they work and how to use them to great effect to easily expand your code with cross-cutting concerns such as performance measurement or logging, and how to avoid null exceptions by autopopulating object properties. Let’s start the journey with something we already know to a certain degree: getters and setters.

What are some of the benefits of accessing a property’s value through getters and setters? What is the main difference between proxies and getters and setters? What are proxy traps? Name three types of trap.








## 记忆时间

## 卡片

### 0001. 反常识卡 —— for 循环只是迭代器的语法糖

Here we again create an iterator object by calling a generator function:

```js
const weaponsIterator = WeaponGenerator();
```

We also create an item variable in which we’ll store individual values produced by the generator. We continue by specifying a while loop with a slightly complicated looping condition, which we’ll break down a bit:

```js
while(!(item = weaponsIterator.next()).done) { 
  assert(item !== null, item.value); 
}
```

On each loop iteration, we fetch a value from the generator by calling the next method of our weaponsIterator, and we store that value in the item variable. Like all such objects, the object referenced by the item variable has a value property that stores the value returned from the generator, and a done property that signals whether the generator is finished producing values. If the generator isn’t done with its work, we go into another iteration of the loop; and if it is, we stop looping.

And that’s how the for-of loop, from our first generator example, works. The for-of loop is syntactic sugar for iterating over iterators:

```js
for(var item of WeaponGenerator()){ 
  assert(item !== null, item); 
}
```

Instead of manually calling the next method of the matching iterator and always checking whether we’re finished, we can use the for-of loop to do the exact same thing, only behind the scenes.

1-2『第一次知道 JS 中 for 循环只是迭代器的语法糖。冲击相当大啊，做一张反常识卡片。（2021-05-03）』—— 已完成

在每次迭代中，我们通过调用迭代器 weaponsIterator 的 next 方法从生成器中取一个值，然后把值存放在 item 变量中。和所有 next 返回的对象一样，item 变量引用的对象中包含一个属性 value 为生成器返回的值，一个属性 done 指示生成器是否已经完成了值的生成。如果生成器中的值没有生成完毕，我们就会进入下次循环迭代，反之停止循环。这就是第一个生成器示例中 for-of 循环的原理。for-of 循环不过是对迭代器进行迭代的语法糖。

不同于手动调用迭代器的 next 方法，for-of 循环同时还要查看生成器是否完成，它在后台自动做了完全相同的工作。把执行权交给下一个生成器正如在标准函数中调用另一个标准函数，我们需要把生成器的执行委托给另一个生成器。让我们看清单 6.4 的例子，生成器不仅生成了武器值也生成了「忍者」值。

### 0101. 主题卡 ——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡 —— 迭代器对象（Iterator）

信息源自「2020097Secrets-of-the-JavaScript-Ninja0601.md」

On the right side of the for-of loop, we've placed the result of invoking our generator. But if you take a closer look at the body of the WeaponGenerator function, you'll see that there's no return statement. What's up with that? In this case, shouldn't the right side of the for-of loop evaluate to undefined, as would be the case if we were dealing with a standard function? The truth is that generators are quite unlike standard functions. For starters, calling a generator doesn't execute the generator function; instead it creates an object called an iterator. Let's explore that object.

2『迭代器对象（Iterator）做一张术语卡片。（2021-05-04）』

图 6.2 迭代函数 WeaponGenerator() 得到的结果我们把执行生成器得到的结果放在 for-of 循环的右边。但如果你仔细看看 WeaponGenerator 函数的函数体，你会发现其中并没有 return 语句。这是为什么？这个例子中，for-of 循环的右边不是应该得到 undefined，就像我们处理一个标准函数一样吗？真相是生成器函数和标准函数非常不同。对初学者来说，调用生成器并不会执行生成器函数，相反，它会创建一个叫作迭代器（iterator）的对象。让我们来探索这个对象吧。

Controlling the generator through the iterator object. Making a call to a generator doesn't mean that the body of the generator function will be executed. Instead, an iterator object is created, an object through which we can communicate with the generator. For example, we can use the iterator to request additional values. Let's adjust our previous example to explore how the iterator object works.

```js
  const WeaponGenerator = function* () { 
    yield "Katana"
    yield "Wakizashi"
    yield "Kusarigama"
  }

  const testFun = () => {
    const weaponsIterator = WeaponGenerator()
    const result1 = weaponsIterator.next()
    console.log(result1)
    console.log(typeof result1)
    const result2 = weaponsIterator.next()
    console.log(result2)
    console.log(typeof result2)
    const result3 = weaponsIterator.next()
    console.log(result3)
    console.log(typeof result3)
  }
```

As you can see, when we call a generator, a new iterator is created:

```js
const weaponsIterator = WeaponGenerator();
```

The iterator is used to control the execution of the generator. One of the fundamental things that the iterator object exposes is the next method, which we can use to control the generator by requesting a value from it:

```js
const result1 = weaponsIterator.next();
```

As a response to that call, the generator executes its code until it reaches a yield keyword that produces an intermediary result (one item in the generated sequence of items), and returns a new object that encapsulates that result and tells us whether its work is done.

As soon as the current value is produced, the generator suspends its execution without blocking and patiently waits for another value request. This is an incredibly powerful feature that standard functions don't have, a feature that we'll use later to great effect.

In this case, the first call to the iterator's next method executes the generator code to the first yield expression, yield "Katana", and returns an object with the property value set to Katana and the property done set to false, signaling that there are more values to produce.

Later, we request another value from the generator, by making another call to the weaponIterator's next method:

```js
const result2 = weaponsIterator.next();
```

This wakes up the generator from suspension, and the generator continues where it left off, executing its code until another intermediary value is reached: yield "Wakizashi". This suspends the generator and produces an object carrying Wakizashi.

Finally, when we call the next method for the third time, the generator resumes its execution. But this time there's no more code to execute, so the generator returns an object with value set to undefined, and done set to true, signaling that it's done with its work.

Now that you've seen how to control generators through iterators, you're ready to learn how to iterate over the produced values.

### 0202. 术语卡 ——

### 0301. 金句卡 —— JS 里的 class 关键字是语法糖

### 0401. 任意卡 —— 数组的常用操作

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

而在将对象的属性指向一个函数时，如果将函数进行命名，那么其行为与函数表达式一样。这样的函数被称为内联命名函数。72 页的一段代码非常有趣，对象的方法可以调用数组原型方法，例如 `Array.prototype.push.call(this, objectB)`，然后如果这个对象有个 length 属性，那么这个原型方法呢就会将 length 值加 1，并且给对象添加一个数字属性，对象通过 [index] 访问这个数字属性，就可以访问到刚刚添加的对象 objectB。

4.4 函数重载方式。重载函数是函数的一种特殊情况，为方便使用，C++ 允许在同一范围中声明几个功能类似的同名函数，但是这些同名函数的形式参数（指参数的个数、类型或者顺序）必须不同，也就是说用同一个运算符完成不同的运算功能。这就是重载函数。重载函数常用来实现功能类似而所处理的数据类型不同的问题。—— 来自百度百科

1『这不就是多态么，哈哈。』

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

console.log(ninjas.find('c'));  // ["c"]
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

第 15 章，CSS 选择器引擎。W3C Selectors API，主要就是两个方法：`querySelector()` 和 `querySelectorAll()`。比较有趣的事情是这几个：

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
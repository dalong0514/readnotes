## 书评

### 01. 非常霸道的 js 书

一贫

2011-06-28 17:42:33

[非常霸道的 js 书](https://book.douban.com/review/5004807/)

如果你觉得自己的 js 水平不错了，可以看看这本书。这本书虽然只是 meap 版，但是也够你看一段时间，里面有太多的东西需要慢慢体会。

这本书以函数为中心（函数也确实是 js 的核心），对函数的讲解非常全面细致，涉及到函数的定义、扩展、重载、curry 化、闭包、重定向、继承等方方面面，还有在 js 书籍里很少涉及的对计数器的解释，比如各个浏览器在最小时间间隔上的区别，比如 setTimeout 和 setInterval 的区别。其他的对正则表达式、命名空间、浏览器最新实现 CSS 选择器都有很好的解释。

### 02. 让人不能释卷

denisdeng

2010-03-14 10:14:41

[让人不能释卷](https://book.douban.com/review/3075430/)

提起该书的作者 John Resig，恐怕没人不知道。用过 jQuery 的朋友，相信知道该库的妙处。读完该书之后，我们就能明白 John Resig 为什么能构建出 jQuery 库。书中对函数、闭包等做了详尽的分析，尤其对我们经常忽视的 Timer 作了详尽的分析。值得细读、深读。

### 03. 从入门到进阶的一站式服务

CJ

2018-01-12 06:56:24

[从入门到进阶的一站式服务](https://book.douban.com/review/9063679/)

写这条评论就是想提醒一下有兴趣的读者，别被书名骗了，别被其他评论那股 vibe 骗了，这是一本新手友好的书，可以作为你的第一本 js 书。

优点：1）可能因为 js 本身特性和作者组织编排得当，就这么几个大的要点，大点打通小点全通。看完你会觉得你都记住了，在编程书中较为难得。2）示例代码各种图表，注释，色框，看了示例代码，就不用看正文的讲解了。3）新，注重 web 下的使用和 ES6 新特性。

### 04. 那些我不知道的知识点

子龙

2016-08-23 00:57:55

[那些我不知道的知识点](https://book.douban.com/review/8055105/)

==== 修改说明：去掉对于翻译质量的评价，只评论本书的内容罢。====

==== 但是！译者对闭包概念的翻译（86 页）真是让人大跌眼镜啊！！！真的是用的谷歌翻译吗？？？====

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

### 05. 好书，真正的 js 秘籍，提升必看

qqxufo

2016-03-03 14:43:04

[好书，真正的 js 秘籍，提升必看](https://book.douban.com/review/7797502/)

大神出品的书果然很赞，看了之后能够让你真正感受到 js 的灵活，不得不佩服作者，无愧这本书的名字。唯一不足的是，翻译的一些地方不是很好。如果想提升自己 javascript 的话，这本书绝对是必看之作，吐血推荐！！

### 06. 不一样的 JAVASCRIPT

追

2018-03-04 22:00:55

[不一样的 JAVASCRIPT](https://book.douban.com/review/9201422/)

以前知道第一版，好多人推荐（中文版翻译有点差）。听说出第二版，所以我就一直在等，没有想到很快出来了，我看了样章第二章，只能说：好书，力荐购买。样章主要内容：1）第 2 章 运行时的页面构建过程。2）Web 应用的生命周期步骤。3）从 HTML 代码到 Web 页面的处理过程。4）JavaScript 代码的执行顺序。5）与事件交互。6）事件循环。

### 07. 真正的 JavaScript 忍者秘籍

gyzhao

2015-11-27 23:29:38

[真正的 JavaScript 忍者秘籍](https://book.douban.com/review/7673572/)

这是一本 JavaScript 进阶书，翻译也比较地道。本书是由 jQuery 的创建者和《jQuery 实战》的作者合著的。全书从实际的实践中出发，对测试，函数、闭包、正则、定时器、事件，跨浏览器的 DOM 编程等内容，娓娓道来，内容清晰明了。同时对 JavaScript 编程中存在的陷阱以及规避的办法还有一些非常有用的小技巧穿插在其中，非常精彩，让我在阅读的过程中好几次为作者的巧妙思路而喝彩。总之如果你有了一定 JavaScript 基础，想要进一步提升自己的水平的话，看完这本书一定会让你受益匪浅，写起 JavaScript 代码来底气也更足。
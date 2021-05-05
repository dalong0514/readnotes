## 记忆时间

2021-05-04

## 目录

0601 Functions for the future: generators and promises

## 0601. Functions for the future: generators and promises

### Summary

1 Generators are functions that generate sequences of values — not all at once, but on a per request basis.

2 Unlike standard functions, generators can suspend and resume their execution. After a generator has generated a value, it suspends its execution without blocking the main thread and patiently waits for the next request.

3 A generator is declared by putting an asterisk (`*`) after the function keyword. Within the body of the generator, we can use the new yield keyword that yields a value and suspends the execution of the generator. If we want to yield to another generator, we use the `yield*` operator.

4 Calling a generator creates an iterator object through which we control the execution of the generator. We request new values from the generator by using the iterator's next method, and we can even throw exceptions into the generator by calling the iterator's throw method. In addition, the next method can be used to send in values to the generator.

5 A promise is a placeholder for the results of a computation; it's a guarantee that eventually we'll know the result of the computation, most often an asynchronous computation. A promise can either succeed or fail, and after it has done so, there will be no more changes.

6 Promises significantly simplify our dealings with asynchronous tasks. We can easily work with sequences of interdependent asynchronous steps by using the then method to chain promises. Parallel handling of multiple asynchronous steps is also greatly simplified; we use the Promise.all method.

7 We can combine generators and promises to deal with asynchronous tasks with the simplicity of synchronous code.

1、生成器是一种不会在同时输出所有值序列的函数，而是基于每次的请求生成值。

2、不同于标准函数，生成器可以挂起和回复它们的执行状态。当生成器生成了一个值后，它将会在不阻塞主线程的基础上挂起执行，随后静静地等待下次请求。

3、生成器通过在 function 后面加一个星号（`*`）来定义。在生成器函数体内，我们可以使用新的关键字 yield 来生成一个值并挂起生成器的执行。如果我们想让渡到另一个生成器中，可以使用 yield 操作符。

4、在我们控制生成器的执行过程中，通过使用迭代器的 next 方法调用一个生成器，它能够创建一个迭代器对象。除此之外，我们还能够通过 next 函数向生成器中传入值。

5、promise 是计算结果值的一个占位符，它是对我们最终会得到异步计算结果的一个保证。promise 既可以成功也可以失败，一旦设定好了，就不能够有更多改变。

6、promise 显著地简化了我们处理异步代码的过程。通过使用 then 方法来生成 promise 链，我们就能轻易地处理异步时序依赖。并行执行多个异步任务也同样简单：仅使用 Promise.all 方法即可。

7、通过将生成器和 promise 相结合我们能够使用同步代码来简化异步任务。

### 6.0 

This chapter covers: 1) Continuing function execution with generators. 2) Handling asynchronous tasks with promises. 3) Achieving elegant asynchronous code by combining generators and promises.

In the previous three chapters, we focused on functions, specifically on how to define functions and how to use them to great effect. Although we've introduced some ES6 features, such as arrow functions and block scopes, we've mostly been exploring features that have been part of JavaScript for quite some time. This chapter tackles the cutting edge of ES6 by presenting generators and promises, two completely new JavaScript features. Generators and promises are both introduced by ES6. You can check out current browser support at http://mng.bz/sOs4 and [[ECMAScript 6 compatibility table](http://kangax.github.io/compat-table/es6/#test-Promise)].

1『作者在 6.3.4 小结里讲解了如何用 promise 对象实现从后端请求数据，值得反复研究。』

Generators are a special type of function. Whereas a standard function produces at most a single value while running its code from start to finish, generators produce multiple values, on a per request basis, while suspending their execution between these requests. Although new in JavaScript, generators have existed for quite some time in Python, PHP, and C#.

Generators are often considered an almost weird or fringe language feature not often used by the average programmer. Though most of this chapter's examples are designed to teach you how generator functions work, we'll also explore some practical aspects of generators. You'll see how to use generators to simplify convoluted loops and how to take advantage of generators' capability to suspend and resume their execution, which can help you write simpler and more elegant asynchronous code.

Promises, on the other hand, are a new, built-in type of object that help you work with asynchronous code. A promise is a placeholder for a value that we don't have yet but will at some later point. They're especially good for working with multiple asynchronous steps.

In this chapter, you'll see how both generators and promises work, and we'll finish off by exploring how to combine them to greatly simplify our dealings with asynchronous code. But before going into the specifics, let's take a sneak peek into how much more elegant our asynchronous code can be.

Do you know?

What are some common uses for a generator function? Why are promises better than simple callbacks for asyn-chronous code? 

You start a number of long-running tasks with Promise.race. When does the promise resolve? When would it fail to resolve?

本章包括以下内容：1）通过生成器让函数持续执行。2）使用 promise 处理异步任务。3）使用生成器和 promise 书写优雅代码。

前 3 章中我们集中讨论了函数，尤其是如何定义函数及如何有效使用函数。我们已经介绍了 ES6 的一些特性，例如箭头函数和块作用域，我们学习过的大部分特性在很久前就已经是 JavaScript 的一部分。这一章将探索两个全新的 ES6 的前沿特性：生成器（generator）和 promise（promise）。

注意：生成器和 promise 已经引入到 ES6 中。可以通过 http://mng.bz/sOs4 和 http://mng.bz/Du38 来查看浏览器的支持情况。

生成器是一种特殊类型的函数。当从头到尾运行标准函数时，它最多只生成一个值。然而生成器函数会在几次运行请求中暂停，因此每次运行都可能会生成一个值。虽然生成器对 JavaScript 来说还是个新特性，其实它已经在 Pyhton、PHP 和 C# 中存在很长时间了。生成器经常被当作一种古怪不常用的语言特性，普通水平的程序员一般不会使用这个特性。然而本章中大部分例子都是来教你怎样使用生成器函数的，我们还会探索生成器函数的一些很实用的方面。你会学到如何使用生成器来简化复杂循环，如何利用生成器的能力来挂起和恢复循环的执行，这些技巧都能帮你写出更简单、更优雅的异步代码。

另外，对象的一个新的内置类型 promise，也能帮你编写异步代码。promise 对象是一个占位符，暂时替代那些尚未计算出但未来会计算出的值。对于多个异步操作来说，使用 promise 对象是非常有好处的。

你知道吗？1）生成器函数的主要用途是什么？2）在异步代码中，为什么使用 promise 比使用简单的回调函数更好？3）使用 Promise.race 来执行很多长期执行的任务时，promise 最终会在什么时候变成 resolved 状态？它什么时候会无法变成 resolved 状态？

### 6.1 Making our async code elegant with generators and promises

Imagine that you're a developer working at freelanceninja.com, a popular freelance ninja recruitment site enabling customers to hire ninjas for stealth missions. Your task is to implement a functionality that lets users get details about the highest-rated mission done by the most popular ninja. The data representing the ninjas, the summaries of their missions, as well as the details of the missions are stored on a remote server, encoded in JSON. You might write something like this:

```js
try { 
  var ninjas = syncGetJSON("ninjas.json"); 
  var missions = syncGetJSON(ninjas[0].missionsUrl); 
  var missionDetails = syncGetJSON(missions[0].detailsUrl); 
  //Study the mission description 
} 

catch(e){ 
  //Oh no, we weren't able to get the mission details 
}
```

This code is relatively easy to understand, and if an error occurs in any of the steps, we can easily catch it in the catch block. But unfortunately, this code has a big problem. Getting data from a server is a long-running operation, and because JavaScript relies on a single-threaded execution model, we've just blocked our UI until the long-running operations finish. This leads to unresponsive applications and disappointed users. To solve this problem, we can rewrite it with callbacks, which will be invoked when a task finishes, without blocking the UI:

```js
getJSON("ninjas.json", function(err, ninjas) { 
  if(err) { 
    console.log("Error fetching list of ninjas", err); 
    return; 
  } 
  getJSON(ninjas[0].missionsUrl, function(err, missions) { 
    if(err) { 
      console.log("Error locating ninja missions", err); 
      return; 
  } 
    getJSON(missions[0].detailsUrl, function(err, missionDetails) { 
      if(err) { console.log("Error locating mission details", err); 
      return; 
    } 
    //Study the intel plan 
    }); 
  }); 
});
```

Although this code will be much better received by our users, you'll probably agree that it's messy, it adds a lot of boilerplate error-handling code, and it's plain ugly. This is where generators and promises jump in. By combining them, we can turn the nonblocking but awkward callback code into something much more elegant:

```js
async(function*() { 
  try { 
    const ninjas = yield getJSON("ninjas.json"); 
    const missions = yield getJSON(ninjas[0].missionsUrl); 
    const missionDescription = yield getJSON(missions[0].detailsUrl); 
    //Study the mission details 
  } 
  catch(e) { 
    //Oh no, we weren't able to get the mission details 
  } 
});
```

A generator function is defined by putting an asterisk right after the function keyword. We can use the new yield keyword in generator functions.

The promises are hidden within the getJSON method.

Don't worry if this example doesn't make much sense or if you find some of the syntax (such as function* or yield) unfamiliar. By the end of this chapter, you'll meet all the necessary ingredients. For now, it's enough that you compare the elegance (or the lack thereof) of the nonblocking callback code and the nonblocking generators and promises code.

Let's start slowly by exploring generator functions, the first stepping stone toward elegant asynchronous code.

6.1 使用生成器和 promise 编写优雅的异步代码

想象你是在 freelancenijia.com 工作的开发者，这是一个流行的自由职业「忍者」招聘网站，为客户招募执行秘密任务的「忍者」。你的任务是实现一个功能，用于让用户了解由最受欢迎的「忍者」完成任务的任务详情。将「忍者」、任务摘要以及任务详情的数据存储展示在远程服务器上，并以 JSON 格式编码。你需要编写类似下面的代码：

这段代码很容易理解，如果其中任何一步出了错误，catch 代码块都能很轻易地捕捉。但很不幸，这样的代码有很大问题。从服务器中获取数据是一个长时间操作，而 JavaScript 依赖于单线程执行模型，所以一直到长时间的操作结束之前，UI 的渲染都会暂停。随后的应用都会无响应，用户会感到不满。我们可以用回调函数解决这个问题，这样每个任务结束后都调用回调函数，从而不会导致 UI 暂停。

尽管这段代码能够显著地提升用户体验，但你也会认同这段代码写得很散乱，其中包含着大量的错误处理样板代码，这样的写法看起来很丑陋。这就是生成器函数和 promise 大显身手的时候了。引入这两种技术后，非阻塞但却丑陋的回调函数代码就会变得更优雅：

如果你不能理解这个例子，或者其中的某些语法你并不熟悉（例如 `function*` 或 yield），不要担心。读完本章，你将能够理解所有的关键要素。至于你现在阅读的这段代码，比起非阻塞回调函数代码，使用生成器和 promise 明显更为优雅。让我们开始慢慢探索生成器函数，它是通往优雅异步代码的第一块垫脚石。

### 6.2 Working with generator functions

Generators are a completely new type of function and are significantly different from standard, run-of-the-mill functions. A generator is a function that generates a sequence of values, but not all at once, as a standard function would, but on a per request basis. We have to explicitly ask the generator for a new value, and the generator will either respond with a value or notify us that it has no more values to produce. What's even more curious is that after a value is produced, a generator function doesn't end its execution, as a normal function would. Instead, a generator is merely suspended. Then, when a request for another value comes along, the generator resumes where it left off.

The following listing provides a simple example of using a generator to generate a sequence of weapons.

Listing 6.1 Using a generator function to generate a sequence of values

```js
function* WeaponGenerator() { 
  yield "Katana"; 
  yield "Wakizashi"; 
  yield "Kusarigama";
}

for(let weapon of WeaponGenerator()) { 
  assert(weapon !== undefined, weapon); 
}
```

We start by defining a generator that will produce a sequence of weapons. Creating a generator function is simple: We append an asterisk (*) after the function keyword. This enables us to use the new yield keyword within the body of the generator to produce individual values. Figure 6.1 illustrates the syntax.

In this example, we create a generator called WeaponGenerator that produces a sequence of weapons: Katana, Wakizashi, and Kusarigama. One way of consuming that sequence of weapons is by using a new kind of loop, the for-of loop:

```js
for(let weapon of WeaponGenerator()) { 
  assert(weapon, weapon); 
}
```

The result of invoking this for-of loop is shown in figure 6.2. (For now, don't worry much about the for-of loop, as we'll explore it later.)

On the right side of the for-of loop, we've placed the result of invoking our generator. But if you take a closer look at the body of the WeaponGenerator function, you'll see that there's no return statement. What's up with that? In this case, shouldn't the right side of the for-of loop evaluate to undefined, as would be the case if we were dealing with a standard function?

The truth is that generators are quite unlike standard functions. For starters, calling a generator doesn't execute the generator function; instead it creates an object called an iterator. Let's explore that object.

2『迭代器对象（Iterator）做一张术语卡片。（2021-05-04）』

1『

Electron 里的代码实现：

```js
export default observer(() => {
  const store = useLocalStore(() => new Store())

  const testFun = () => {
    for (let weapon of WeaponGenerator()) {
      console.log(weapon)
    }
  }

  const WeaponGenerator = function* () { 
    yield "Katana"
    yield "Wakizashi"
    yield "Kusarigama"
  }

  return (
    <div className={styles.homeContainer}>
      <Button type='primary' onClick={testFun}>
        测试
      </Button>
    </div>
  )
})
```

』

6.2 使用生成器函数

生成器函数几乎是一个完全崭新的函数类型，它和标准的普通函数完全不同。生成器（generator）函数能生成一组值的序列，但每个值的生成是基于每次请求，并不同于标准函数那样立即生成。我们必须显示地向生成器请求一个新的值，随后生成器要么响应一个新生成的值，要么就告诉我们它之后都不会再生成新值。更让人好奇的是，每当生成器函数生成了一个值，它都不会像普通函数一样停止执行。相反，生成器几乎从不挂起。随后，当对另一个值的请求到来后，生成器就会从上次离开的位置恢复执行。

清单 6.1 提供了一个简单例子，它使用生成器函数生成了一系列武器数据。

清单 6.1 使用生成器函数生成一些列值 

例子首先定义了一个生成器，它能够生成一系列武器的数据。创建一个生成器函数非常简单：仅仅需要在关键字 function 后面加上一个星号（`*`）。这样一来生成器函数体内就能够使用新关键字 yield，从而生成独立的值。

图 6.1 解释了 yield 的语法。

图 6.1 在关键字 function 后面增加一个星号来定义一个生成器本例创建了一个叫作 WeaponGenerator 的生成器，其用于生成一系列武器数据：Katana、Wakizashi 和 Kusarigama。作为取出武器数据序列值的方法之一，for-of 是一种用于循环结构新类型：

for-of 循环的执行结果如图 6.2 所示（现在不必太关心 for-of 循环，稍后我们会对它进行介绍）。

图 6.2 迭代函数 WeaponGenerator() 得到的结果我们把执行生成器得到的结果放在 for-of 循环的右边。但如果你仔细看看 WeaponGenerator 函数的函数体，你会发现其中并没有 return 语句。这是为什么？这个例子中，for-of 循环的右边不是应该得到 undefined，就像我们处理一个标准函数一样吗？

真相是生成器函数和标准函数非常不同。对初学者来说，调用生成器并不会执行生成器函数，相反，它会创建一个叫作迭代器（iterator）的对象。让我们来探索这个对象吧。

#### 6.2.1 Controlling the generator through the iterator object

Making a call to a generator doesn't mean that the body of the generator function will be executed. Instead, an iterator object is created, an object through which we can communicate with the generator. For example, we can use the iterator to request additional values. Let's adjust our previous example to explore how the iterator object works.

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

ITERATING THE ITERATOR

The iterator, created by calling a generator, exposes a next method through which we can request a new value from the generator. The next method returns an object that carries the value produced by the generator, as well as the information stored in the done property that tells us whether the generator has additional values to produce.

Now we'll take advantage of these facts to use a plain old while loop to iterate over values produced by a generator. See the following listing.

Listing 6.3 Iterating over generator results with a while loop

```js
function* WeaponGenerator() { 
  yield "Katana"; 
  yield "Wakizashi"; 
}

const weaponsIterator = WeaponGenerator(); 
let item; 
while(!(item = weaponsIterator.next()).done) { 
  assert(item !== null, item.value); 
}
```

1『

React 项目里实现：

```js
function* WeaponGenerator() { 
  yield "Katana" 
  yield "Wakizashi" 
}

const codeFun = () => {
  // Creates an iterator
  const weaponsIterator = WeaponGenerator() 
  // Creates a variable in which we'll store items of the generated sequence
  let item 
  // On each loop iteration, fetches one value from the generator and outputs its value. 
  // Stops iterating when the generator has no more values to produce.
  while(!(item = weaponsIterator.next()).done) { 
    // assert(item !== null, item.value) 
    if (item !== null) console.log(item.value)
  }
}

export { codeFun }
```

』

Here we again create an iterator object by calling a generator function:

```js
const weaponsIterator = WeaponGenerator();
```

We also create an item variable in which we'll store individual values produced by the generator. We continue by specifying a while loop with a slightly complicated looping condition, which we'll break down a bit:

```js
while(!(item = weaponsIterator.next()).done) { 
  assert(item !== null, item.value); 
}
```

On each loop iteration, we fetch a value from the generator by calling the next method of our weaponsIterator, and we store that value in the item variable. Like all such objects, the object referenced by the item variable has a value property that stores the value returned from the generator, and a done property that signals whether the generator is finished producing values. If the generator isn't done with its work, we go into another iteration of the loop; and if it is, we stop looping.

And that's how the for-of loop, from our first generator example, works. The for-of loop is syntactic sugar for iterating over iterators:

```js
for(var item of WeaponGenerator()){ 
  assert(item !== null, item); 
}
```

Instead of manually calling the next method of the matching iterator and always checking whether we're finished, we can use the for-of loop to do the exact same thing, only behind the scenes.

1-2『第一次知道 JS 中 for 循环只是迭代器的语法糖。冲击相当大啊，做一张反常识卡片。（2021-05-03）』—— 已完成

YIELDING TO ANOTHER GENERATOR

Just as we often call one standard function from another standard function, in certain cases we want to be able to delegate the execution of one generator to another. Let's take a look at an example that generates both warriors and ninjas.

Listing 6.4 Using `yield*` to delegate to another generator

```js
function* WarriorGenerator() { 
  yield "Sun Tzu"; 
  // yield* delegates to another generator.
  yield* NinjaGenerator(); 
  yield "Genghis Khan"; 
}

function* NinjaGenerator() { 
  yield "Hattori"; 
  yield "Yoshi"; 
}

for(let warrior of WarriorGenerator()) { 
  assert(warrior !== null, warrior); 
}
```

1『

React 项目里实现：

```js
function* WarriorGenerator() { 
  yield "Sun Tzu" 
  yield* NinjaGenerator() 
  yield "Genghis Khan" 
}

function* NinjaGenerator() { 
  yield "Hattori" 
  yield "Yoshi" 
}

const codeFun = () => {
  // Creates an iterator
  const weaponsIterator = WarriorGenerator() 
  for (let warrior of weaponsIterator) {
    if (warrior !== null) console.log(warrior)
  }
}

export { codeFun }
```

』

If you run this code, you'll see that the output is Sun Tzu, Hattori, Yoshi, Genghis Khan. Generating Sun Tzu probably doesn't catch you off guard; it's the first value yielded by the WarriorGenerator. But the second output, Hattori, deserves an explanation.

By using the yield* operator on an iterator, we yield to another generator. In this example, from a WarriorGenerator we're yielding to a new NinjaGenerator; all calls to the current WarriorGenerator iterator's next method are rerouted to the NinjaGenerator. This holds until the NinjaGenerator has no work left to do. So in our example, after Sun Tzu, the program generates Hattori and Yoshi. Only when the NinjaGenerator is done with its work will the execution of the original iterator continue by outputting Genghis Khan. Notice that this is happening transparently to the code that calls the original generator. The for-of loop doesn't care that the WarriorGenerator yields to another generator; it keeps calling next until it's done.

Now that you have a grasp of how generators work in general and how delegating to another generator works, let's look at a couple of practical examples.

6.2.1 通过迭代器对象控制生成器

调用生成器函数不一定会执行生成器函数体。通过创建迭代器对象，可以与生成器通信。例如，可以通过迭代器对象请求满足条件的值。稍微修改一下之前的示例，看看迭代器对象是如何工作的，如清单 6.2 所示。

如你所见，调用生成器后，就会创建一个迭代器（iterator）：

迭代器用于控制生成器的执行。迭代器对象暴露的最基本接口是 next 方法。这个方法可以用来向生成器请求一个值，从而控制生成器：

next 函数调用后，生成器就开始执行代码，当代码执行到 yield 关键字时，就会生成一个中间结果（生成值序列中的一项），然后返回一个新对象，其中封装了结果值和一个指示完成的指示器。每当生成一个当前值后，生成器就会非阻塞地挂起执行，随后耐心等待下一次值请求的到达。这是普通函数完全不具有的强大特性，后续的例子中它还会起到更大的作用。

在本例中，第一次调用生成器的 next 方法让生成器代码执行到第一个 yield 表达式 yield "Katana"，然后返回了一个对象。该对象的属性 value 的值置为 Katana，属性 done 的值置为 false，表明之后还有值会生成。随后，通过再次调用 weaponIterator 的 next 方法，再次向生成器请求另一个值：

该操作将生成器从挂起状态唤醒，中断执行的生成器从上次离开的位置继续执行代码，直到再次遇到另一个中间值：yield "Wakizashi"。随即生成了一个包含着值 Wakizashi 的对象，生成器挂起。最后，当第三次执行 next 方法后，生成器恢复执行。但这一次，没有更多可供它执行的代码了，所以生成器返回一个结果对象，属性 value 被置为 undefined，属性 done 被置为 true，表明它的工作已经完成了。

现在你已经了解了如何通过迭代器控制生成器，希望你已经做好准备进入下一个学习阶段：如何迭代生成的值序列。对迭代器进行迭代通过调用生成器得到的迭代器，暴露出一个 next 方法能让我们向迭代器请求一个新值。next 方法返回一个携带着生成值的对象，而该对象中包含的另一个属性 done 也向我们指示了生成器是否还会追加生成值。现在，我们利用这一原理，试着用普通的 while 循环来迭代生成器生成的值序列，如清单 6.3 所示。

本例中，我们通过调用生成器函数再次创建了一个迭代器对象：

我们还创建了一个变量 item，用于保存由生成器生成的单个值。随后，我们给 while 循环指定了条件，该条件有点复杂需要分解来看：

在每次迭代中，我们通过调用迭代器 weaponsIterator 的 next 方法从生成器中取一个值，然后把值存放在 item 变量中。和所有 next 返回的对象一样，item 变量引用的对象中包含一个属性 value 为生成器返回的值，一个属性 done 指示生成器是否已经完成了值的生成。如果生成器中的值没有生成完毕，我们就会进入下次循环迭代，反之停止循环。这就是第一个生成器示例中 for-of 循环的原理。for-of 循环不过是对迭代器进行迭代的语法糖。

不同于手动调用迭代器的 next 方法，for-of 循环同时还要查看生成器是否完成，它在后台自动做了完全相同的工作。把执行权交给下一个生成器正如在标准函数中调用另一个标准函数，我们需要把生成器的执行委托给另一个生成器。让我们看清单 6.4 的例子，生成器不仅生成了武器值也生成了「忍者」值。

执行这段代码后会输出 Sun Tzu、Hattori、Yoshi、Genghis Khan。第一个输出 Sun Tzu 不会让你感到意外，因为它就是 WarriorGenerator 生成器得到的第一个值。而对于第二个输出的值是 Hattori，我们需要解释一下了。在迭代器上使用 `yield *` 操作符，程序会跳转到另外一个生成器上执行。本例中，程序从 WarriorGenerator 跳转到一个新的 NinjaGenerator 生成器上，每次调用 WarriorGenerator 返回迭代器的 next 方法，都会使执行重新寻址到了 NinjaGenerator 上。该生成器会一直持有执行权直到无工作可做。所以我们本例中生成 Sun Tzu 之后紧接的是 Hattori 和 Yoshi。仅当 NinjaGenerator 的工作完成后，调用原来的迭代器才会继续输出值 Genghis Khan。注意，对于调用最初的迭代器代码来说，这一切都是透明的。for-of 循环不会关心 WarriorGenerator 委托到另一个生成器上，它只关心在 done 状态到来之前都一直调用 next 方法。现在，对于生成器一般的工作，以及如何代理到其他生成器的工作上，你都已经有所掌握了。让我们看看几个实践中的例子。

#### 6.2.2 Using generators

Generating sequences of items is all nice and dandy, but let's get more practical, starting with a simple case of generating unique IDs.

USING GENERATORS TO GENERATE IDS

When creating certain objects, often we need to assign a unique ID to each object. The easiest way to do this is through a global counter variable, but that's kind of ugly because the variable can be accidently messed up from anywhere in our code. Another option is to use a generator, as shown in the following listing.

Listing 6.5 Using generators for generating IDs

```js
function *IdGenerator() { 
  let id = 0; 
  while(true) { 
    yield ++id;
  }
}

const idIterator = IdGenerator();

const ninja1 = { id: idIterator.next().value }; 
const ninja2 = { id: idIterator.next().value }; 
const ninja3 = { id: idIterator.next().value };

assert(ninja1.id === 1, "First ninja has id 1"); 
assert(ninja2.id === 2, "Second ninja has id 2"); 
assert(ninja3.id === 3, "Third ninja has id 3");
```

This example starts with a generator that has one local variable, id, which represents our ID counter. The id variable is local to our generator; there's no fear that someone will accidently modify it from somewhere else in the code. This is followed by an infinite while loop, which at each iteration yields a new id value and suspends its execution until a request for another ID comes along:

```js
function *IdGenerator(){
  let id = 0;
  while(true){ 
    yield ++id; 
  }
}
```

NOTE: Writing infinite loops isn't something that we generally want to do in a standard function. But with generators, everything is fine! Whenever the generator encounters a yield statement, the generator execution is suspended until the next method is called again. So every next call executes only one iteration of our infinite while loop and sends back the next ID value.

After defining the generator, we create an iterator object:

```js
const idIterator = IdGenerator();
```

This allows us to control the generator with calls to the idIterator.next() method. This executes the generator until a yield is encountered, returning a new ID value that we can use for our objects:

```js
const ninja1 = { id: idIterator.next().value };
```

1『这种生成序号的逻辑，当时开发数据流前端，全通全面通风表格时就借用了上面的逻辑，代码很简洁。（2021-05-04）』

See how simple this is? No messy global variables whose value can be accidentally changed. Instead, we use an iterator to request values from a generator. In addition, if later we need another iterator for tracking the IDs of, for example, samurai, we can initialize a new generator for that.

USING GENERATORS TO TRAVERSE THE DOM

As you saw in chapter 2, the layout of a web page is based on the DOM, a tree-like structure of HTML nodes, in which every node, except the root one, has exactly one parent, and can have zero or more children. Because the DOM is such a fundamental structure in web development, a lot of our code is based around traversing it. One relatively easy way to do this is by implementing a recursive function that will be executed for each visited node. See the following code.

Listing 6.6 Recursive DOM traversal 

```js
<div id="subTree">
  <form>
    <input type="text"/>
  </form> 
  <p>Paragraph</p> 
  <span>Span</span> 
</div>

<script> 
  function traverseDOM(element, callback) { 
    callback(element); 
    element = element.firstElementChild; 
    while (element) { 
      traverseDOM(element, callback); 
      element = element.nextElementSibling; 
    } 
  } 
  const subTree = document.getElementById("subTree"); 
  traverseDOM(subTree, function(element) { 
    assert(element !== null, element.nodeName); 
  }); 
</script>
```

In this example, we use a recursive function to traverse all descendants of the element with the id subtree, in the process logging each type of node that we visit. In this case, the code outputs DIV, FORM, INPUT, P, and SPAN. We've been writing such DOM traversal code for a while now, and it has served us perfectly fine. But now that we have generators at our disposal, we can do it differently; see the following code.

Listing 6.7 Iterating over a DOM tree with generators

```js
function* DomTraversal(element) {
  yield element; 
  element = element.firstElementChild; 
  while (element) {
    yield* DomTraversal(element);
    element = element.nextElementSibling;
  }
}

const subTree = document.getElementById("subTree"); 
for(let element of DomTraversal(subTree)) { 
  assert(element !== null, element.nodeName); 
}
```

This listing shows that we can achieve DOM traversals with generators, just as easily as with standard recursion, but with the aditional benefit of not having to use the slightly awkward syntax of callbacks. Instead of processing the subtree of each visited node by recursing another level, we create one generator function for each visited node and yield to it. This enables us to write what's conceptually recursive code in iterable fashion. The benefit is that we can consume the generated sequence of nodes with a simple for-of loop, without resorting to nasty callbacks.

This example is a particulary good one, because it also shows how to use generators in order to separate the code that's producing values (in this case, HTML nodes) from the code that's consuming the sequence of generated values (in this case, the for-of loop that logs the visited nodes), without having to resort to callbacks. In addition, using iterations is, in certain cases, much more natural than recursion, so it's always good to have our options open.

Now that we've explored some practical aspects of generators, let's go back to a slighty more theoretical topic and see how to exchange data with a running generator.

6.2.2 使用生成器

尽管前面例子中生成的序列都不错，但现在来看一个更实际的简单例子，生成唯一 ID 值。

用生成器生成 ID 序列

在创建某些对象时，我们经常需要为每个对象赋一个唯一的 ID 值。最简单的方式是通过一个全局的计数器变量，但这是一种丑陋的写法，因为这个计数器变量很容易就会不慎淹没在混乱的代码中。另外一种方式则是使用生成器，如清单 6.5 所示。

本例开始的迭代器中包含一个局部变量 id，其代表了 ID 计数器。局部变量 id 仅能在该生成器中被访问，故而完全不必担心有人会不小心在代码的其他地方修改 id 值。随后是一个无限的 while 循环，其每次迭代都能生成一个新 id 值并挂起执行，直到下一次 ID 请求到达：

注意：标准函数中一般不应该书写无限循环的代码。但在生成器中没问题！当生成器遇到了一个 yield 语句，它就会一直挂起执行直到下次调用 next 方法，所以只有每次调用一次 next 方法，while 循环才会迭代一次并返回下一个 ID 值。

定义了生成器之后，又创建了一个迭代器对象：

我们能够调用 `idIterator.next()` 方法来控制生成器执行。每当遇到一次 yield 语句生成器就会停止执行，返回一个新的 ID 值可以用于给我们的对象赋值：

看到这个方法多么简单了吧？代码中没有任何会被不小心修改的全局变量。相反，我们使用迭代器从生成器中请求值。另外，如果还需要用另外一个迭代器来记录 ID 序列，例如迭代器 samurai，我们只需要直接再初始化一个新迭代器就可以了。

使用迭代器遍历 DOM 树

如第 2 章中所示，网页的布局是基于 DOM 结构的，它是由 HTML 节点组成的树形结构，除了根节点的每个节点都只有一个父节点，而且可以有 0 个或多个孩子节点。由于 DOM 是网页开发中的基础，所以我们大部分代码都是围绕着对它的遍历。遍历 DOM 的相对简单的方式就是实现一个递归函数，在每次访问节点的时候都会被执行，如清单 6.6 所示。

这个例子使用一个递归函数来遍历 id 为 subtree 的所有节点，在访问每个节点的过程中我们还记录了该节点的类型。本例中分别输出了 DIV、FORM、INPUT、P 和 SPAN。很久以来我们都在编写这种 DOM 遍历代码，它一直能满足我们的需要。但现在我们可以使用生成器了，故而可以换一种方式来实现它，请看清单 6.7。

这个清单展示了我们可以通过生成器实现 DOM 遍历，就像标准递归一样简单，但它不必书写丑陋的回调函数代码。不同于在下一层递归处理每个访问过的节点子树，我们为每个访问过的节点创建了一个生成器并将执行权交给它，从而使我们能够以迭代的方式书写概念上递归的代码。它的好处在于我们能够不凭借讨厌的回调函数，仅仅以一个简单的 for-of 循环就能处理生成的节点。这个案例是一个相当好的例子，因为它还告诉了我们如何在不必使用回调函数的情况下，使用生成器函数来解耦代码，从而将生产值（本例中是 HTML 节点）的代码和消费值（本例中的 for-of 循环打印、访问过的节点）的代码分隔开。除此之外，在很多场景下，使用迭代器比使用递归都要自然，所以保持一个开放的思路很重要。现在我们已经看过生成器的一些实战中的例子了，让我们再看看更理论化一点的主题，并看看如何使用运行中的生成器来交换数据。

#### 6.2.3 Communicating with a generator

In the examples presented so far, you've seen how to return multiple values from a generator by using yield expressions. But generators are even more powerful than that! We can also send data to a generator, thereby achieving two-way communication! With a generator, we can produce an intermediary result, use that result to calculate something else from outside the generator, and then, whenever we're ready, send completely new data back to the generator and resume its execution. We'll use this feature to great effect at the end of the chapter to deal with asynchronous code, but for now, let's keep it simple.

SENDING VALUES AS GENERATOR FUNCTION ARGUMENTS

The easiest way to send data to a generator is by treating it like any other function and using function call arguments. Take a look at the following listing.

Listing 6.8 Sending data to and receiving data from a generator

```js
// A generator can receive standard arguments, like any other function.
function* NinjaGenerator(action) { 
  // The magic happens. By yielding a value, the generator returns an intermediary calculation. 
  // By calling the iterator’s next method with an argument, we send data back to the generator.
  const imposter = yield ("Hattori " + action);
  // The value sent over next becomes the value of the yielded expression, so our imposter is Hanzo.
  assert(imposter === "Hanzo", "The generator has been infiltrated");
  yield ("Yoshi (" + imposter + ") " + action);
}

const ninjaIterator = NinjaGenerator("skulk");
const result1 = ninjaIterator.next(); 
// Triggers the execution of the generator and checks that we get the correct value
assert(result1.value === "Hattori skulk", "Hattori is skulking");
const result2 = ninjaIterator.next("Hanzo"); 
// Sends data to the generator as an argument to the next method and checks whether the value was correctly transferred
assert(result2.value === "Yoshi (Hanzo) skulk", "We have an imposter!");
```

A function receiving data is nothing special; plain old functions do it all the time. But remember, generators have this amazing power; they can be suspended and resumed. And it turns out that, unlike standard functions, generators can even receive data after their execution has started, whenever we resume them by requesting the next value.

USING THE NEXT METHOD TO SEND VALUES INTO A GENERATOR

In addition to providing data when first invoking the generator, we can send data into a generator by passing arguments to the next method. In the process, we wake up the generator from suspension and resume its execution. This passed-in value is used by the generator as the value of the whole yield expression, in which the generator was currently suspended, as shown in figure 6.3.

In this example, we have two calls to the ninjaIterator's next method. The first call, ninjaIterator.next(), requests the first value from the generator. Because our generator hasn't started executing, this call starts the generator, which calculates the value of the expression "Hattori " + action, yields the Hattori skulk value, and suspends the generator's execution. There's nothing special about this; we've done something similar multiple times throughout this chapter.

The interesting thing happens on the second call to the ninjaIterator's next method: ninjaIterator.next("Hanzo"). This time, we're using the next method to pass data back to the generator. Our generator function is patiently waiting, suspended at the expression yield ("Hattori " + action), so the value Hanzo, passed as the argument to next(), is used as the value of the whole yield expression. In our case, this means that the variable imposter in imposter = yield ("Hattori " + action) will end up with the value Hanzo.

Figure 6.3 The first call to ninjaIterator.next() requests a new value from the generator, which returns Hattori skulk and suspends the execution of the generator at the yield expression. The second call to ninjaIterator.next("Hanzo") requests a new value, but also sends the argument Hanzo into the generator. This value will be used as the value of the whole yield expression, and the variable imposter will now carry the value Hanzo.

That's how we achieve two-way communication with a generator. We use yield to return data from a generator, and the iterator's next() method to pass data back to the generator.

NOTE: The next method supplies the value to the waiting yield expression, so if there's no yield expression waiting, there's nothing to supply the value to. For this reason, we can't supply values over the first call to the next method. But remember, if you need to supply an initial value to the generator, you can do so when calling the generator itself, as we did with NinjaGenerator("skulk").

THROWING EXCEPTIONS

There's another, slightly less orthodox, way to supply a value to a generator: by throwing an exception. Each iterator, in addition to having a next method, has a throw method that we can use to throw an exception back to the generator. Again, let's look at a simple example.

Listing 6.9 Throwing exceptions to generators

```js
function* NinjaGenerator() { 
  try {
    yield "Hattori";
    fail("The expected exception didn't occur"); 
  }
  catch(e) { 
    assert(e === "Catch this!", "Aha! We caught an exception"); 
  }
}

const ninjaIterator = NinjaGenerator();
const result1 = ninjaIterator.next();
assert(result1.value === "Hattori", "We got Hattori");
ninjaIterator.throw("Catch this!");
```

Listing 6.9 starts similarly to listing 6.8, by specifying a generator called NinjaGenerator. But this time, the body of the generator is slightly different. We've surrounded the whole function body code with a try-catch block:

```js
function* NinjaGenerator() {
  try { 
    yield "Hattori"; 
    fail("The expected exception didn't occur"); 
  } 
  catch(e) {
    assert(e === "Catch this!", "Aha! We caught an exception"); 
  }
}
```

We then continue by creating an iterator, and getting one value from the generator:

```js
const ninjaIterator = NinjaGenerator(); 
const result1 = ninjaIterator.next();
```

Finally, we use the throw method, available on all iterators, to throw an exception back to the generator:

```js
ninjaIterator.throw("Catch this!");
```

By running this listing, we can see that our exception throwing works as expected, as shown in figure 6.4.

This feature that enables us to throw exceptions back to generators might feel a bit strange at first. Why would we even want to do that? Don't worry; we won't keep you in the dark for long. At the end of this chapter, we'll use this feature to improve asynchronous server-side communication.

Figure 6.4 We can throw exceptions to generators Just be patient a bit longer. from outside a generator.

Now that you've seen several aspects of generators, we're ready to take a look under the hood to see how generators work.

6.2.3 与生成器交互

从目前已经展示的例子来看，你已经看到了如何通过使用 yield 表达式从生成器中返回多个值。但生成器远比这强大！我们还能向生成器发送值，从而实现双向通信！使用生成器我们能够生成中间结果，在生成器以外我们也能够使用该结果进行任何什么操作，然后，一旦准备好了，就能够把整个新计算得到的数据再完完全全返回给生成器，本章的最后我们会利用这个特性来实现异步代码，但现在先学点儿简单的。

作为生成器函数参数发送值

向生成器发送值的最简方法如其他函数一样，调用函数并传入实参，如清单 6.8 所示。

使用 next 方法向生成器发送值

除了在第一次调用生成器的时候向生成器提供数据，我们还能通过 next 方法向生成器传入参数。在这个过程中，我们把生成器函数从挂起状态恢复到了执行状态。在当前挂起的生成器中，生成器把这个传入的值用于整个 yield 表达式，如图 6.3 所示。这个例子中我们调用了两次 ninjaIterator 的 next 方法。第一次调用 `ninjaIterator.next(),` 请求了生成器的第一个值。由于生成器还没开始执行，这次调用则启动了生成器，对表达式 `"Hattori" + action` 进行求值，得到了值 "Hattori skulk"，并将该生成器的执行挂起。这一点没什么特别的，类似的事情我们已经做过很多次了。

然而第二次调用 ninjaIterator 的 next 方法则发生了有趣的事：`ninjaIterator.next ("Hanzo")`。这一次，我们使用 next 方法将计算得到的值又传递回生成器。生成器函数耐心地等待着，在表达式 `yield ("Hattori" + action)` 位置挂起，故而值 Hanzo 作为参数传入了  next() 方法，并用作整个 yield 表达式的值。本例中，也就是表示语句 `imposter = yield ("Hattori" + action)` 中的变量 imposter 会以值 Hanzo 作为结尾。

图 6.3 首次调用 `ninjaIterator.next() `向生成器请求了一个新值，在 yield 表达式的位置返回了 Hattoriskulk，并挂起执行。第二次调用 `ninjaIterator.next ("Hanzo")` 又请求了一个新值，但它同时向生成器发送了实参 Hanzo。这个只会在整个 yield 表达式中使用，同时，imposter 变量也就包含了字符串 Hanzo。

以上展示了如何在生成器中双向通信。我们通过 yield 语句从生成器中返回值，再使用迭代器的 next() 方法把值传回生成器。

注意：next 方法为等待中的 yield 表达式提供了值，所以，如果没有等待中的 yield 表达式，也就没有什么值能应用的。基于这个原因，我们无法通过第一次调用 next 方法来向生成器提供该值。但记住，如果你需要为生成器提供一个初始值，你可以调用生成器自身，就像 `NinjaGenerator ("skulk")`。

抛出异常

还有一种稍微不那么正统的方式将值应用到生成器上：通过抛出一个异常。每个迭代器除了有一个 next 方法，还抛出一个方法，让我们再来看一个简单的例子。

清单 6.9 与清单 6.8 的开始部分很相似，都是声明了一个叫作 NinjaGenerator 的生成器。但这次，生成器函数体内则稍有不同。我们把整个函数体用一个 try-catch 块包裹了起来：

通过创建一个迭代器继续执行，然后从生成器中获取一个值：

最后，通过使用在所有迭代器上都有效的 throw 方法，我们向生成器抛出了一个异常：

运行了这个清单中的代码后，可以看到异常的抛出情况如我们所料，如图 6.4 所示。这个能让我们把异常抛回生成器的特性初看可能有点奇怪。为什么要进行这样的操作呢？不必担心，我们不会让你一直蒙在鼓里。本章的最后部分，我们将使用这个特性来改善异步服务器端的通信。暂且多点儿耐心。现在你已经看过了许多生成器的例子，我们已经做好准备来看一看生成器的内部是如何工作的了。

图 6.4 我们可以从生成器外部向其抛出异常 

#### 6.2.4 Exploring generators under the hood

So far we know that calling a generator doesn't execute it. Instead, it creates a new iterator that we can use to request values from the generator. After a generator produces (or yields) a value, it suspends its execution and waits for the next request. So in a way, a generator works almost like a small program, a state machine that moves between states:

1 Suspended start — When the generator is created, it starts in this state. None of the generator's code is executed.

2 Executing — The state in which the code of the generator is executed. The execution continues either from the beginning or from where the generator was last suspended. A generator moves to this state when the matching iterator's next method is called, and there exists code to be executed.

3 Suspended yield — During execution, when a generator reaches a yield expression, it creates a new object carrying the return value, yields it, and suspends its execution. This is the state in which the generator is paused and is waiting to continue its execution.

4 Completed — If during execution the generator either runs into a return statement or runs out of code to execute, the generator moves into this state.

Figure 6.5 illustrates these states.

Now let's supplement this on an even deeper level, by seeing how the execution of generators is tracked with execution contexts.

1 Create a new generator in the Suspended start state.

```js
const ninjaIterator = NinjaGenerator(); 
```

2 Activate generator. Move from Suspended start to Executing. Execute up to yield "Hattori" and pause. Move to the Suspended yield state. Return a new object: {value: "Hattori", done: false}.

```js
const result1 = ninjaIterator.next(); 
```

3 Reactivate generator. Move from Suspended yield to Executing. Execute up to yield "Yoshi" and pause. Move to the Suspended yield state. Return a new object: {value: "Yoshi", done: false}.

```js
const result2 = ninjaIterator.next(); 
```

4 Reactivate generator. Move from Suspended yield to Executing. No more code to execute. Move to the Completed state. Return a new object: {value: undefined, done: true}.

```js
const result3 = ninjaIterator.next(); 
```

Figure 6.5 During execution, a generator moves between states triggered by calls to the matching iterator's next method.

TRACKING GENERATORS WITH EXECUTION CONTEXTS

In the previous chapter, we introduced the execution context, an internal JavaScript mechanism used to track the execution of functions. Although somewhat special, generators are still functions, so let's take a closer look by exploring the relationship between them and execution contexts. We'll start with a simple code fragment:

```js
function* NinjaGenerator(action) { 
  yield "Hattori " + action; 
  return "Yoshi " + action; 
}

const ninjaIterator = NinjaGenerator("skulk"); 
const result1 = ninjaIterator.next(); 
const result2 = ninjaIterator.next();
```

Here we reuse our generator that produces two values: Hattori skulk and Yoshi skulk.

Now, we'll explore the state of the application, the execution context stack at various points in the application execution. Figure 6.6 gives a snapshot at two positions in the application execution. The first snapshot shows the state of the application execution before calling the NinjaGenerator function B . Because we're executing global code, the execution context stack contains only the global execution context, which references the global environment in which our identifiers are kept. Only the NinjaGenerator identifier references a function, while the values of all other identifiers are undefined.

When we make the call to the NinjaGenerator function

```js
const ninjaIterator = NinjaGenerator("skulk");
```

the control flow enters the generator and, as it happens when we enter any other function, a new NinjaGenerator execution context item is created (alongside the matching lexical environment) and pushed onto the stack. But because generators are special, none of the function code is executed. Instead, a new iterator, which we'll refer to in the code as ninjaIterator, is created and returned. Because the iterator is used to control the execution of the generator, the iterator gets a reference to the execution context in which it was created.

An interesting thing happens when the program execution leaves the generator, as shown in figure 6.7. Typically, when program execution returns from a standard function, the matching execution context is popped from the stack and completely discarded. But this isn't the case with generators.

Figure 6.6 The state of the execution context stack before calling the NinjaGenerator calling the NinjaGenerator function

Figure 6.7 The state of the application when returning from the NinjaGenerator call

The matching NinjaGenerator stack item is popped from the stack, but it's not discarded, because the ninjaIterator keeps a reference to it. You can see it as an analogue to closures. In closures, we need to keep alive the variables that are alive at the moment the function closure is created, so our functions keep a reference to the environment in which they were created. In this way, we make sure that the environment and its variables are alive as long as the function itself. Generators, on the other hand, have to be able to resume their execution. Because the execution of all functions is handled by execution contexts, the iterator keeps a reference to its execution context, so that it's alive for as long as the iterator needs it.

Another interesting thing happens when we call the next method on the iterator:

```js
const result1 = ninjaIterator.next();
```

If this was a standard straightforward function call, this would cause the creation of a new next() execution context item, which would be placed on the stack. But as you might have noticed, generators are anything but standard, and a call to the next method of an iterator behaves a lot differently. It reactivates the matching execution context, in this case, the NinjaGenerator context, and places it on top of the stack, continuing the execution where it left off, as shown in figure 6.8.

Figure 6.8 illustrates a crucial difference between standard functions and generators. Standard functions can only be called anew, and each call creates a new execution context. In contrast, the execution context of a generator can be temporarily suspended and resumed at will.

In our example, because this is the first call to the next method, and the generator hasn't started executing, the generator starts its execution and moves to the Executing state. The next interesting thing happens when our generator function reaches this point:

```js
yield "Hattori " + action
```

Figure 6.8 Calling the iterator's next method reactivates the execution context stack item of the matching generator, pushes it on the stack, and continues where it left off the last time.

The generator determines that the expression equals Hattori skulk, and the evaluation reaches the yield keyword. This means that Hattori skulk is the first intermediary result of our generator and that we want to suspend the execution of the generator and return that value. In terms of the application state, a similar thing happens as before: the NinjaGenerator context is taken off the stack, but it's not completely discarded, because ninjaIterator keeps a reference to it. The generator is now suspended, and has moved to the Suspended Yield state, without blocking. The program execution resumes in global code, by storing the yielded value to result1. The current state of the application is shown in figure 6.9.

The code continues by reaching another iterator call:

```js
const result2 = ninjaIterator.next();
```

Figure 6.9 After yielding a value, the generator's execution context is popped from the stack (but isn't discarded, because ninjaIterator keeps a reference to it), and the generator execution is suspended (the generator moves to the Suspended yield state).

At this point, we go through the whole procedure once again: we reactivate the NinjaGenerator context referenced by ninjaIterator, push it onto the stack, and continue the execution where we left off. In this case, the generator evaluates the expression "Yoshi " + action. But this time there's no yield expression, and instead the program encounters a return statement. This returns the value Yoshi skulk and completes the generator's execution by moving the generator into the Completed state.

Uff, this was something! We went deep into how generators work under the hood to show you that all the wonderful benefits of generators are a side effect of the fact that a generator's execution context is kept alive if we yield from a generator, and not destroyed as is the case with return values and standard functions.

1-2『这一小节的内容要反复反复研读，特别是原文里的几张图，涉及到 JS 的执行上下文，一下子把之前研读有关亚历山大（一个  CEO）的系列文章全部串起来了，太 NB 了。生成器异常强大的核心原因，做一张主题卡片。（2021-05-04）』—— 已完成

Now we recommend that you take a quick breather before continuing on to the second key ingredient required for writing elegant asynchronous code: promises.

6.2.4 探索生成器内部构成

我们已经知道了调用一个生成器不会实际执行它。相反，它创建了一个新的迭代器，通过该迭代器我们才能从生成器中请求值。在生成器生成（或让渡）了一个值后，生成器会挂起执行并等待下一个请求的到来。在某种方面来说，生成器的工作更像是一个小程序，一个在状态中运动的状态机。

1、挂起开始 —— 创建了一个生成器后，它最先以这种状态开始。其中的任何代码都未执行。

2、执行 —— 生成器中的代码已执行。执行要么是刚开始，要么是从上次挂起的时候继续的。当生成器对应的迭代器调用了 next 方法，并且当前存在可执行的代码时，生成器都会转移到这个状态。

3、挂起让渡 —— 当生成器在执行过程中遇到了一个 yield 表达式，它会创建一个包含着返回值的新对象，随后再挂起执行。生成器在这个状态暂停并等待继续执行。

4、完成 —— 在生成器执行期间，如果代码执行到 return 语句或者全部代码执行完毕，生成器就进入该状态。

让我们更进一步补充一些知识，看看生成器是如何跟随执行环境上下文的，如图 6.5 所示。

图 6.5 在执行过程中，生成器在相对应的生成器调用 next 函数之间移动状态

通过执行上下文跟踪生成器函数

在前面的例子中，我们介绍了执行环境上下文。它是一个用于跟踪函数的执行的 JavaScript 内部机制。尽管有些特别，生成器依然是一种函数，所以让我们仔细看看它们和执行环境上下文之间的关系吧。首先从一个简单的代码片段开始：

这里我们对生成器进行了重用，其生成了两个值：Hattori skulk 和 Yoshi skulk。现在，我们将探索应用的状态，看一看在应用执行过程中不同位置上的执行上下文栈。

图 6.6 中展示了应用执行中两个位置的状态快照。第一个快照显示了应用在函数 B 中调用生成器 NinjaGenerator 之前的状态。由于正在执行的是全局代码，故执行上下文栈仅仅包含全局执行上下文，该上下文引用了当前标识符所在的全局环境。而 NinjaGenerator 则仅仅引用了一个函数，此时其他标识符的值都是 undefined。

图 6.6 在调用 NinjaGenerator 函数之前和之后的执行上下文栈的状态

当我们调用 NinjaGenerator 函数：

```js
const ninjaIterator = NinjaGenerator("skulk");
```

控制流则进入了生成器，正如进入任何其他函数一样，当前将会创建一个新的函数环境上下文 NinjaGenerator（和相对应的词法字典并列），并将该上下文入栈。而生成器比较特殊，它不会执行任何函数代码。取而代之则生成一个新的迭代器再从中返回，通过在代码中用 ninjaIterator 可以来引用这个迭代器。由于迭代器是用来控制生成器的执行的，故而迭代器中保存着一个在它创建位置处的执行上下文。

如图 6.7 所示。当程序从生成器中执行完毕后，发生了一个有趣的现象。一般情况下，当程序从一个标准函数返回后，对应的执行环境上下文会从栈中弹出，并被完整地销毁。但在生成器中不是这样。

图 6.7 从调用 NinjaGenerator 中返回后应用的状态

相对应的 NinjaGenerator 会从栈中弹出，但由于 ninjaIterator 还保存着对它的引用，所以它不会被销毁。你可以把它看作一种类似闭包的事物。在闭包中，为了在闭包创建的时候保证变量都可用，所以函数会对创建它的环境持有一个引用。以这种方式，我们能保证只要函数还存在，环境及变量就都存在着。生成器，从另一个角度看，还必须恢复执行。由于所有函数的执行都被执行上下文所控制，故而迭代器保持了一个对当前执行环境的引用，保证只要迭代器还需要它的时候它都存在。当调用迭代器的 next 方法时发生了另一件有趣的事：

```js
const result1 = ninjaIterator.next();
```

如果这只是一个普通的函数调用，这个语句会创建一个新的 next() 的执行环境上下文项，并放入栈中。但你可能注意到了，生成器绝不标准，对 next 方法调用的表现也很不同。它会重新激活对应的执行上下文。在这个例子中，是 NinjaGenerator 上下文，并把该上下文放入栈的顶部，从它上次离开的地方继续执行，如图 6.8 所示。

图 6.8 调用生成器的 next 方法会重新激活执行上下文栈中与该生成器相对应的项，首先将该项入栈，然后从它上次退出的位置继续执行

图 6.8 阐述了函数和生成器之间的关键不同。标准函数仅仅会被重复调用，每次调用都会创建一个新的执行环境上下文。相比之下，生成器的执行环境上下文则会暂时挂起并在将来恢复。在我们的例子中，由于是第一次调用 next 方法，而生成器之前并没执行过，所以生成器开始执行并进入执行状态。当生成器函数运行到这个位置的时候，又会发生一件有趣的事：

```js
yield "Hattori " + action
```

生成器函数运行得到的表达式的结果为 Hattori skulk，然后执行中又遇到了 yield 关键字。这种情况表明了 Hattori skulk 是该生成器的第一个中间值，所以需要挂起生成器的执行并返回该值。从应用状态的角度来看，发生了一件类似前面的事情：NinjaGenerator 上下文离开了调用栈，但由于 ninjaIterator 还持有着对它的引用，故而它并未被销毁。现在生成器挂起了，又在非阻塞的情况下移动到了挂起让渡状态。程序在全局代码中恢复执行，并将生产出的值存入变量 result1。应用的当前状态如图 6.9 所示。

图 6.9 在产生了一个值之后，生成器的执行环境上下文就会从栈中弹出（但由于 ninjaIterator 保存着对它的引用所以它不会被销毁），生成器挂起执行（生成器进入挂起让渡状态）

当遇到另一个迭代器调用时，代码继续运行：

```js
const result2 = ninjaIterator.next();
```

生成器处于挂起让渡状态；生成器的执行环境上下文从栈中弹出，但由于 ninjaIterator 保存着对它的引用所以它不会被销毁。

在这个位置，我们又把整个流程走了一遍：首先通过 ninjaIterator 激活 NinjaGenerator 的上下文引用，将其入栈，在上次离开的位置继续执行。本例中，生成器计算表达式 "Yoshi" + action。但这一次没再遇到 yield 表达式，而是遇到了一个 return 语句。这个语句会返回值 Yoshi skulk 并结束生成器的执行，随之生成器进入结束状态。看，这很强大吧！

我们深入挖掘生成器的工作原理后可以发现，生成器所有不可思议的特点实际都来源于一点，即当我们从生成器中取得控制权后，生成器的执行环境上下文一直是保存的，而不是像标准函数一样退出后销毁。现在我建议你平静一下心情，继续书写优雅异步代码的第二个关键点：promise。

### 6.3 Working with promises

In JavaScript, we rely a lot on asynchronous computations, computations whose results we don't have yet but will at some later point. So ES6 has introduced a new concept that makes handling asynchronous tasks easier: promises.

A promise is a placeholder for a value that we don't have now but will have later; it's a guarantee that we'll eventually know the result of an asynchronous computation. If we make good on our promise, our result will be a value. If a problem occurs, our result will be an error, an excuse for why we couldn't deliver. One great example of using promises is fetching data from a server; we promise that we'll eventually get the data, but there's always a chance that problems will occur.

Creating a new promise is easy, as you can see in the following example.

Listing 6.10 Creating a simple promise

```js
const ninjaPromise = new Promise((resolve, reject) => { 
  resolve("Hattori"); 
  //reject("An error resolving a promise!");
});

ninjaPromise.then(ninja => {
  assert(ninja === "Hattori", "We were promised Hattori!");
}, err => { 
  fail("There shouldn't be an error") 
});
```

To create a promise, we use the new, built-in Promise constructor, to which we pass a function, in this case an arrow function (but we could just as easily use a function expression). This function, called an executor function, has two parameters: resolve and reject. The executor is called immediately when constructing the Promise object with two built-in functions as arguments: resolve, which we manually call if we want the promise to resolve successfully, and reject, which we call if an error occurs.

This code uses the promise by calling the built-in then method on the Promise object, a method to which we pass two callback functions: a success callback and a failure callback. The former is called if the promise is resolved successfully (if the resolve function is called on the promise), and the latter is called if there's a problem (either an unhandled exception occurs or the reject function is called on a promise).

In our example code, we create a promise and immediately resolve it by calling the resolve function with the argument Hattori. Therefore, when we call the then method, the first, success, callback is executed and the test that outputs We were promised Hattori! passes.

Now that we have a general idea of what promises are and how they work, let's take a step back to see some of the problems that promises tackle.

6.3 使用 promise 

使用 JavaScript 编写代码会大量的依赖异步计算，计算那些我们现在不需要但将来某时候可能需要的值。所以 ES6 引入了一个新的概念，用于更简单地处理异步任务：promise。

promise 对象是对我们现在尚未得到但将来会得到值的占位符；它是对我们最终能够得知异步计算结果的一种保证。如果我们兑现了我们的承诺，那结果会得到一个值。如果发生了问题，结果则是一个错误，一个为什么不能交付的借口。使用 promise 的一个最佳例子是从服务器获取数据：我们要承诺最终会拿到数据，但其实总有可能发生错误。新建一个 promise 对象很容易，如清单 6.10 所示。

使用新的内置构造函数 Promise 来创建一个 promise 需要传入一个函数，在本例中是一个箭头函数（当然也可以简单地使用一个函数表达式）。这个函数被称为执行函数（executor function），它包含两个参数 resolve 和 reject。当把两个内置函数：resolve 和 reject 作为参数传入 Promise 构造函数后，执行函数会立刻调用。我们可以手动调用 resolve 让承诺兑现，也可以当错误发生时手动调用 reject。

代码调用 Promise 对象内置的 then 方法，我们向这个方法中传入了两个回调函数：一个成功回调函数和一个失败回调函数。当承诺成功兑现（在 promise 上调用了 resolve），前一个回调就会被调用，而当出现错误就会调用后一个回调函数（可以是发生了一个未处理的异常，也可以是在 promise 上调用了 reject）。

示例代码中，我们通过向 resolve 函数传递参数 Hattori 从而创建了一个承诺并立即兑现。因此，当我们调用 then 方法时，首先到达成功状态，回调函数被执行，测试程序输出 "We were promisedHattori!"，测试通过。现在我们对 promise 如何工作有了一个总的概念，接着来看看 promise 能解决哪些问题。

#### 6.3.1 Understanding the problems with simple callbacks 

We use asynchronous code because we don't want to block the execution of our application (thereby disappointing our users) while long-running tasks are executing. Currently, we solve this problem with callbacks: To a long-running task we provide a function, a callback that's invoked when the task is finally done.

For example, fetching a JSON file from a server is a long-running task, during which we don't want to make the application unresponsive for our users. Therefore, we provide a callback that will be invoked when the task is done:

```js
getJSON("data/ninjas.json", function() { 
  /*Handle results*/ 
});
```

Naturally, during this long-running task, errors can happen. And the problem with callbacks is that you can't use built-in language constructs, such as try-catch statements, in the following way:

```js
try {
  getJSON("data/ninjas.json", function() { 
    //Handle results 
  }); 
} catch(e) {/*Handle errors*/}
```

This happens because the code invoking the callback usually isn't executed in the same step of the event loop as the code that starts the long-running task (you'll see exactly what this means when you learn more about the event loop in chapter 13).

As a consequence, errors usually get lost. Many libraries, therefore, define their own conventions for reporting errors. For example, in the Node.js world, callbacks customarily take two arguments, err and data, where err will be a non-null value if an error occurs somewhere along the way. This leads to the first problem with callbacks: difficult error handling.

After we've performed a long-running task, we often want to do something with the obtained data. This can lead to starting another long-running task, which can eventually trigger yet another long-running task, and so on — leading to a series of interdependent, asynchronous, callback-processed steps. For example, if we want to execute a sneaky plan to find all ninjas at our disposal, get the location of the first ninja, and send him some orders, we'd end up with something like this:

```js
getJSON("data/ninjas.json", function(err, ninjas) { 
  getJSON(ninjas[0].location, function(err, locationInfo) { 
    sendOrder(locationInfo, function(err, status) { 
      /*Process status*/ 
    }) 
  }) 
});
```

You've probably ended up, at least once or twice, with similarly structured code — a bunch of nested callbacks that represent a series of steps that have to be made. You might notice that this code is difficult to understand, inserting new steps is a pain, and error handling complicates your code significantly. You get this "pyramid of doom" that keeps growing and is difficult to manage. This leads us to the second problem with callbacks: performing sequences of steps is tricky.

Sometimes, the steps that we have to go through to get to the final result don't depend on each other, so we don't have to make them in sequence. Instead, to save precious milliseconds, we can do them in parallel. For example, if we want to set a plan in motion that requires us to know which ninjas we have at our disposal, the plan itself, and the location where our plan will play out, we could take advantage of jQuery's get method and write something like this:

```js
var ninjas, mapInfo, plan;

$.get("data/ninjas.json", function(err, data) { 
  if(err) { processError(err); return; } 
  ninjas = data; 
  actionItemArrived(); 
});

$.get("data/mapInfo.json", function(err, data) { 
  if(err) { processError(err); return; } 
  mapInfo = data; 
  actionItemArrived(); 
});

$.get("plan.json", function(err, data) { 
  if(err) {  processError(err); return; }
  plan = data; 
  actionItemArrived (); 
});

function actionItemArrived(){ 
  if(ninjas != null && mapInfo != null && plan != null) { 
    console.log("The plan is ready to be set in motion!"); 
  } 
}

function processError(err) { 
  alert("Error", err) 
}
```

In this code, we execute the actions of getting the ninjas, getting the map info, and getting the plan in parallel, because these actions don't depend on each other. We only care that, in the end, we have all the data at our disposal. Because we don't know the order in which the data is received, every time we get some data, we have to check whether it's the last piece of the puzzle that we're missing. Finally, when all pieces are in place, we can set our plan in motion. Notice that we have to write a lot of boilerplate code just to do something as common as executing a number of actions in parallel. This leads us to the third problem with callbacks: performing a number of steps in parallel is also tricky.

When presenting the first problem with callbacks — dealing with errors — we showed how we can't use some of the fundamental language constructs, such as trycatch statements. A similar thing holds with loops: If you want to perform asynchronous actions for each item in a collection, you have to jump through some more hoops to get it done.

It's true that you can make a library to simplify dealing with all these problems (and many people have). But this often leads to a lot of slightly different ways of dealing with the same problems, so the people behind JavaScript have bestowed upon us promises, a standard approach for dealing with asynchronous computation.

Now that you understand most of the reasons behind the introduction of promises, as well as have a basic understanding of them, let's take it up a notch.

6.3.1 理解简单回调函数所带来的问题

使用异步代码的原因在于不希望在执行长时间任务的时候，应用程序的执行被阻塞（影响用户体验）。当前，通过使用回调函数解决这个问题：对长期执行的任务提供一个函数，当任务结束后会调用该回调函数。例如，从服务器获取 JSON 文件是一个长时间任务，在这个任务执行期间我们不希望用户感到应用未响应。因此，我们提供了一个回调函数用于任务结束后调用：

长时间任务下发生错误也是很自然的现象。问题就在于当回调函数发生错误时，你无法用内置构造函数来处理，类似下面使用 try-catch 的方式：

导致这个问题的原因在于，当长时间任务开始运行，调用回调函数的代码一般不会和开始任务中的这段代码位于事件循环的同一步骤（在第 13 章会学到事件循环，届时你将明白它的准确含义）。导致的结果就是，错误经常会丢失。因此许多函数库定义了各自的报错误规约。例如，在 Node.js 中，回调函数一般具有两个参数：err 和 data。当错误在某处发生时，err 参数中将会是个非空的值。这就引起了第一个问题：错误难以处理。

当执行了一个长时间运行的任务后，我们经常希望用获取的数据来做些什么。这会导致开始另一项长期运行的任务，该任务最后又会触发另一个长期运行的任务，如此一来导致了互相依赖的一系列异步回调任务。如果我们希望找到所有「忍者」来执行一个秘密计划，首先要找到第一个「忍者」所处的位置，然后向他下达一些命令，最后就会出现类似下面的情况：

你的结果可能就是，至少写了一两次类似的结构的代码：一堆嵌套的回调函数用来表明需要执行的一系列步骤。还会意识到这样的代码难以理解，向其中再插入几步简直是一种痛苦，增加错误处理也会大大增加代码的复杂度。你的「金字塔噩梦」在不断增长，代码越来越难以管理。这就是回调函数的第二个问题：执行连续步骤非常棘手。

有时候得到最终结果的这些步骤并不相互依赖，所以我们不必让它们按顺序执行。为了节省时间可以并行地执行这些任务。例如，如果我们想要得知可以用哪个「忍者」来完成一次行动，这个行动地点和找「忍者」两件事情并不互相依赖，所以就可以使用 jQuery 的 get 方法编写类似如下代码：

这段代码中，我们执行了获取「忍者」的行动：由于行动之间互不依赖，所以在获取地图信息的同时获取计划。只需要关心这两点内容最后就能够获取所有数据。我们不知道这些数据获取的顺序，每次获取到一些数据，都检查看看是否是最后一段缺失的数据。最后，当所有的数据都获取到了，我们就能立刻开始执行计划了。注意我们依然不得不书写很多样板代码仅仅用于并行执行多个行动。这导致了回调函数的第三个问题：执行很多并行任务也很棘手。

看过了第一个回调函数问题即错误处理 —— 我们看到了为何我们不能使用语言的基本构造，例如 try-catch 语句。循环也有类似问题：如果你想为集合中的每一项执行异步任务，你必须越过重重关卡才能完成。你可以专门写一个函数库来简化处理所有这些问题（很多人都有这些问题）。没错，但这也常常导致大量的稍有一点不同的解决方案，而它们仅是为了解决同样的问题，所以开发 JavaScript 语言的作者们开发了 promise，它是用于处理异步计算的关键方法。你现在应该能够理解引入 promise 的大部分原因了，让我们继续深入学习 promise。

#### 6.3.2 Diving into promises

A promise is an object that serves as a placeholder for a result of an asynchronous task. It represents a value that we don't have but hope to have in the future. For this reason, during its lifetime, a promise can go through a couple of states, as shown in figure 6.10.

Figure 6.10 States of a promise

A promise starts in the pending state, in which we know nothing about our promised value. That's why a promise in the pending state is also called an unresolved promise. During program execution, if the promise's resolve function is called, the promise moves into the fulfilled state, in which we've successfully obtained the promised value. On the other hand, if the promise's reject function is called, or if an unhandled exception occurs during promise handling, the promise moves into the rejected state, in which we weren't able to obtain the promised value, but in which we at least know why. Once a promise has reached either the fulfilled state or the rejected state, it can't switch (a promise can't go from fulfilled to rejected or vice versa), and it always stays in that state. We say that a promise is resolved (either successfully or not).

The following listing provides a closer look at what's going on when we use promises.

Listing 6.11 A closer look at promise order of execution

```js
report("At code start");
var ninjaDelayedPromise = new Promise((resolve, reject) => { 
  // Calling the Promise constructor immediately invokes the passed-in function.
  report("ninjaDelayedPromise executor"); 
  setTimeout(() => { 
    report("Resolving ninjaDelayedPromise"); 
    // We’ll resolve this promise as successful after a 500ms timeout expires.
    resolve("Hattori"); 
  }, 500);  
});

assert(ninjaDelayedPromise !== null, "After creating ninjaDelayedPromise");

ninjaDelayedPromise.then(ninja => {
  // The Promise then method is used to set up a callback that will be called 
  // when the promise resolves, in our case when the timeout expires.
  assert(ninja === "Hattori", "ninjaDelayedPromise resolve handled with Hattori");
});

// Creates a new promise that gets immediately resolved
const ninjaImmediatePromise = new Promise((resolve, reject) => { 
  report("ninjaImmediatePromise executor. Immediate resolve."); 
  resolve("Yoshi"); 
});

ninjaImmediatePromise.then(ninja => {
  // Sets up a callback to be invoked when the promise resolves. But our promise is already resolved!
  assert(ninja === "Yoshi", "ninjaImmediatePromise resolve handled with Yoshi");
});

report("At code end");
```

The code in listing 6.11 outputs the results shown in figure 6.11. As you can see, the code starts by logging the "At code start" message by using our custom-made report function (appendix C) that outputs the message onscreen. This enables us to easily track the order of execution.

Next we create a new promise by calling the Promise constructor. This immediately invokes the executor function in which we set up a timeout:

```js
setTimeout(() => { 
  report("Resolving ninjaDelayedPromise"); 
  resolve("Hattori"); 
}, 500);
```

The timeout will resolve the promise after 500ms. This could have been any other asynchronous task, but we chose the humble timeout because of its simplicity.

After the ninjaDelayedPromise has been created, it still doesn't know the value that it will eventually have, or whether it will even be successful. (Remember, it's still waiting for the timeout that will resolve it.) So after construction, the ninjaDelayedPromise is in the first promise state, pending.

Figure 6.11 The result of executing listing 6.11

Next we use the then method on the ninjaDelayedPromise to schedule a callback to be executed when the promise successfully resolves:

```js
ninjaDelayedPromise.then(ninja => {
  assert(ninja === "Hattori", "ninjaDelayedPromise resolve handled with Hattori");
});
```

This callback will always be called asynchronously, regardless of the current state of the promise.

We continue by creating another promise, ninjaImmediatePromise, which is resolved immediately during its construction, by calling the resolve function. Unlike the ninjaDelayedPromise, which after construction is in the pending state, the ninjaImmediatePromise finishes construction in the resolved state, and the promise already has the value Yoshi.

Afterward, we use the ninjaImmediatePromise's then method to register a callback that will be executed when the promise successfully resolves. But our promise is already settled; does this mean that the success callback will be immediately called or that it will be ignored? The answer is neither.

Promises are designed to deal with asynchronous actions, so the JavaScript engine always resorts to asynchronous handling, to make the promise behavior predictable. The engine does this by executing the then callbacks after all the code in the current step of the event loop is executed (once again, we'll explore exactly what this means in chapter 13). For this reason, if we study the output in figure 6.11, we'll see that we first log "At code end" and then we log that the ninjaImmediatePromise was resolved. In the end, after the 500ms timeout expires, the ninjaDelayedPromise is resolved, which causes the execution of the matching then callback.

In this example, for the sake of simplicity, we've worked only with the rosy scenario in which everything goes great. But the real world isn't all sunshine and rainbows, so let's see how to deal with all sorts of crazy problems that can occur.

6.3.2 深入研究 promise

promise 对象用于作为异步任务结果的占位符。它代表了一个我们暂时还没获得但在未来有希望获得的值。基于这点原因，在一个 promise 对象的整个生命周期中，它会经历多种状态，如图 6.10 所示。一个 promise 对象从等待（pending）状态开始，此时我们对承诺的值一无所知。因此一个等待状态的 promise 对象也称为未实现（unresolved）的 promise。在程序执行的过程中，如果 promise 的 resolve 函数被调用，promise 就会进入完成（fulfilled）状态，在该状态下我们能够成功获取到承诺的值。

另一方面，如果 promise 的 reject 函数被调用，或者如果一个未处理的异常在 promise 调用的过程中发生了，promise 就会进入到拒绝状态，尽管在该状态下我们无法获取承诺的值，但我们至少知道了原因。一旦某个 promise 进入到完成态或者拒绝态，它的状态都不能再切换了（一个 promise 对象无法从完成态再进入拒绝态或者相反）。让我们仔细看看在使用 promise 的时候到底发生了什么，如清单 6.11 所示。

清单 6.11 的代码输出了图 6.11 中的值。你可以看到，当代码从打印日志「At code start」开始，通过使用我们自定义的 report 函数（见附录 B）将信息输出至屏幕，从而我们能够轻易地跟踪函数的执行过程。下一步则通过调用 Promise 构造函数创建了一个新的 promise 对象。它会立即调用执行函数并建立一个计时器：

计时器会在 500ms 之后调用 promise 的 resolve 方法。这里可以是任何异步任务，简单起见本处选择了定时器。

图 6.11 清单 6.11 的输出结果

在 ninjaDelayedPromise 被创建后，依然无法得知最终会得到什么值，或者无法保证 promise 会成功进入完成状态。（记住，它会一直等待计时器到时后调用 resolve 函数）所以在构造函数调用后，ninjaDelayedPromise 就进入了 promise 的第一个状态 —— 等待状态。然后调用 ninjaDelayedPromise 的 then 方法，用于建立一个预计在 promise 被成功实现后执行的回调函数：

这个回调函数总会被异步调用，无论 promise 当前是什么状态。我们继续创建另一个 promise —— ninjaImmediatePromise，它会在对象构造阶段立刻调用 promise 的 resolve 函数，立即完成承诺。不同于 ninjaDelayedPromise 对象在构造后进入等待状态，ninjaImmediatePromise 对象在解决状态下完成了对象的构造，所以该 promise 对象就已经获得了值 Yoshi。然后，通过调用 ninjaImmediatePromise 的 then 方法，我们为其注册了一个回调函数，用于在 promise 成功被解决后调用。然而此时 promise 已经被解决了，难道这意味着这个成功回调函数会被立即调用，或者被忽略吗？答案是两者都不。

Promise 是设计用来处理异步任务的，所以 JavaScript 引擎经常会凭借异步处理使 promise 的行为得以预见。JavaScript 通过在本次时间循环中的所有代码都执行完毕后，调用 then 回调函数来处理 promise。因此，如果我们研究了图 6.11 中的输出，我们会看到首先是日志「At code end」，然后我们记录了 ninjaImmediatePromise 已经被解决。最后，经过了 500ms，ninjaDelayedPromise 也被解决，从而响应的回调函数被调用。本例中，简单起见，我们选择的场景都很乐观，所以一切都进行得很完美。但现实世界并不总是有阳光和彩虹，让我们来看看如何处理所有可能遇到的问题吧。

#### 6.3.3 Rejecting promises

There are two ways of rejecting a promise: explicitly, by calling the passed-in reject method in the executor function of a promise, and implicitly, if during the handling of a promise, an unhandled exception occurs. Let's start our exploration with the following listing.

Listing 6.12 Explicitly rejecting promises

```js
const promise = new Promise((resolve, reject) => { 
  // A promise can be explicitly rejected by calling the passed-in reject function.
  reject("Explicitly reject a promise!"); 
});

// If a promise is rejected, the second, error, callback is invoked.
promise.then( 
  () => fail("Happy path, won't be called!"), 
  error => pass("A promise was explicitly rejected!") 
);
```

We can explicitly reject a promise, by calling the passed-in reject method: `reject("Explicitly reject a promise!")`. If a promise is rejected, when registering callbacks through the then method, the second, error, callback will always be invoked.

In addition, we can use an alternative syntax for handling promise rejections, by using the built-in catch method, as shown in the following listing.

Listing 6.13 Chaining a catch method

```js
var promise = new Promise((resolve, reject) => { 
  reject("Explicitly reject a promise!"); 
});

// Instead of supplying the second, error, callback, 
// we can chain in the catch method, and pass to it the error callback. The end result is the same.
promise.then(()=> fail("Happy path, won't be called!")) 
        .catch(() => pass("Promise was also rejected"));
```

As listing 6.13 shows, we can chain in the catch method after the then method, to also provide an error callback that will be invoked when a promise gets rejected. In this example, this is a matter of personal style. Both options work equally well, but later, when working with chains of promises, we'll see an example in which chaining the catch method is useful.

In addition to explicit rejection (via the reject call), a promise can also be rejected implicitly, if an exception occurs during its processing. Take a look at the following example.

Listing 6.14 Exceptions implicitly reject a promise

```js
// A promise is implicitly rejected if an unhandled exception occurs when processing the promise.
const promise = new Promise((resolve, reject) => { 
  undeclaredVariable++; 
});

// If an exception occurs, the second, error, callback is invoked.
promise.then(() => fail("Happy path, won't be called!")) 
        .catch(error => pass("Third promise was also rejected"));
```

Within the body of the promise executor, we try to increment undeclaredVariable, a variable that isn't defined in our program. As expected, this results in an exception. Because there's no try-catch statement within the body of the executor, this results in an implicit rejection of the current promise, and the catch callback is eventually invoked. In this situation, we could have just as easily supplied the second callback to the then method, and the end effect would be the same.

This way of treating all problems that happen while working with promises in a uniform way is extremely handy. Regardless of how the promise was rejected, whether explicitly by calling the reject method or even implicitly, if an exception occurs, all errors and rejection reasons are directed to our rejection callback. This makes our lives as developers a little easier.

Now that we understand how promises work, and how to schedule success and failure callbacks, let's take a real-world scenario, getting JSON-formatted data from a server, and "promisify" it.

6.3.3 拒绝 promise 

拒绝一个 promise 有两种方式：显式拒绝，即在一个 promise 的执行函数中调用传入的 reject 方法；隐式拒绝，正处理一个 promise 的过程中抛出了一个异常。让我们一起来探索这个过程，如清单 6.12 所示。

通过调用传入的 reject 函数可以显式拒绝 `promise:reject ("Explicitly reject a promise!")`。如果 promise 被拒绝，则第二个回调函数 error 总会被调用。除此之外可以使用替代预发来处理拒绝 promise，通过使用内置的 catch 方法，如清单 6.13 所示。

清单 6.13 链式调用 catch 方法

如清单 6.13 中所示，通过在 then 方法后链式调用 catch 方法，我们同样可以在 promise 进入被拒绝状态时为其提供错误回调函数。在本例中，是否采用这种方式完全基于个人习惯。两种方式的作用相同，但请稍等片刻，在使用链式调用的 promise 方法后，我们可以看一个例子，在该示例中更适合使用链式调用。如果在执行过程中遇到了一个异常，除了显式拒绝（通过调用 reject）, promise 还可以被隐式拒绝。请看清单 6.14 的例子。

在 promise 函数体内，我们试着对变量 undeclaredVariable 进行自增，该变量并未在程序中定义。不出所料，程序产生了一个异常。由于在执行函数中没有 try-catch 语句，所以当前的 promise 被隐式拒绝了，catch 回调函数最后被调用。在这种情况下，如果我们把错误回调函数作为 then 函数的第二个参数，结果也是相同的。

以这种方式处理 promise 中发生的错误可以说是相当简便。无论 promise 是被如何拒绝的，显示调用 reject 方法还是隐式调用，只要发生了异常，所有错误和拒绝原因都会在拒绝回调函数中被定位。这个特性大大减轻了开发者的工作。现在我们理解了 promise 是如何工作的，如何为 promise 设置成功和失败回调函数。接下来看一个现实的场景，从服务器中获取 JSON 格式的数据，并以 promise 化的形式书写代码。

#### 6.3.4 Creating our first real-world promise

One of the most common asynchronous actions on the client is fetching data from the server. As such, this is an excellent little case study on the use of promises. For the underlying implementation, we'll use the built-in XMLHttpRequest object.

Listing 6.15 Creating a getJSON promise

```js
function getJSON(url) {
  // Creates and returns a new promise
  return new Promise((resolve, reject) => { 
    // Creates an XMLHttpRequest object
    const request = new XMLHttpRequest();
    // Initializes the request
    request.open("GET", url);
    //  Registers an onload handler that will be called if the server has responded
    request.onload = function() { 
      try { 
        // Even if the server has responded, it doesn’t mean everything went as expected. 
        // Use the result only if the server responds with status 200 (everything OK).
        if(this.status === 200 ) { 
          // Try to parse the JSON string; if it succeeds, resolve the promise as successful with the parsed object.
          resolve(JSON.parse(this.response)); 
        } else { reject(this.status + " " + this.statusText); } 
      } catch(e) { 
        reject(e.message);  
      };
    }
    // If the server responds with a different status code, or if there’s an exception parsing the JSON string, reject the promise.

    // If there’s an error while communicating with the server, reject the promise.
    request.onerror = function() { 
      reject(this.status + " " + this.statusText); 
    };
    // Sends the request
    request.send(); 
  });
}

// Uses the promise created by the getJSON function to register resolve and reject callbacks
getJSON("data/ninjas.json").then(ninjas => { 
  assert(ninjas !== null, "Ninjas obtained!");
}).catch(e => fail("Shouldn't be here:" + e));
```

NOTE: Our goal is to create a getJSON function that returns a promise that will enable us to register success and failure callbacks for asynchronously getting JSON-formatted data from the server. For the underlying implementation, we use the built-in XMLHttpRequest object that offers two events: onload and onerror. The onload event is triggered when the browser receives a response from the server, and onerror is triggered when an error in communication happens. These event handlers will be called asynchronously by the browser, as they occur.

If an error in the communication happens, we definitely won't be able to get our data from the server, so the honest thing to do is to reject our promise:

```js
request.onerror = function() { 
  reject(this.status + " " + this.statusText); 
};
```

If we receive a response from the server, we have to analyze that response and consider the exact situation. Without going into too much detail, a server can respond with various things, but in this case, we care only that the response is successful (status 200). If it isn't, again we reject the promise.

Even if the server has successfully responded with data, this still doesn't mean that we're in the clear. Because our goal was to get JSON-formatted objects from the server, the JSON code could always have syntax errors. This is why, when calling the JSON.parse method, we surround the code with a try-catch statement. If an exception occurs while parsing the server response, we also reject the promise. With this, we've taken care of all bad scenarios that can happen.

If everything goes according to plan, and we successfully obtain our objects, we can safely resolve the promise. Finally, we can use our getJSON function to fetch ninjas from the server:

```js
getJSON("data/ninjas.json").then(ninjas => { 
  assert(ninjas !== null, "Ninjas obtained!");
}).catch(e => fail("Shouldn't be here:" + e));
```

In this case, we have three potential sources of errors: errors in establishing the communication between the server and the client, the server responding with unanticipated data (invalid response status), and invalid JSON code. But from the perspective of the code that uses the getJSON function, we don't care about the specifics of error sources. We only supply a callback that gets triggered if everything goes okay and the data is properly received, and a callback that gets triggered if any error occurs. This makes our lives as developers so much easier.

Now we're going to take it up a notch and explore another big advantage of promises: their elegant composition. We'll start by chaining several promises in a series of distinct steps.

6.3.4 创建第一个真实 promise 

案例客户端最通用的异步任务就是从服务器获取数据。同样，这也是一个非常好的用于学习如何使用 promise 的小案例。我们将使用内置 XMLHttpRequest 对象来完成底层的实现，如清单 6.15 所示。

注意：执行本示例代码的前提条件是启动服务器，所有后续的例子都会重用这段代码。例如，你可以使用 www.npmjs.com/package/http-server 提供的服务。

为了从服务器端异步获取 JSON 格式的数据，我们的目标是创建一个 getJSON 函数，它返回一个 promise 对象。通过该对象，我们能够在上面注册成功和失败回调函数。我们采用内置 XMLHttpRequest 来完成底层实现。该内置包含两种事件：onload 和 onerror。当浏览器从服务器端接收到了一个响应，onload 事件就会被触发，当通信出错则会触发 onerror 事件。一旦这些事件发生后，浏览器就会异步调用响应的事件处理函数。如果通信中出现了错误，我们完全无法从服务器中获取数据，所以最真诚的方式就是拒绝掉我们的承诺。

如果从服务器端接收了一个响应，我们必须分析该响应内容并判断当前处在什么情况。由于服务器会返回各种各样的内容，所以先不考虑太多，本例中我们仅仅关心响应成功（状态码为 200）。如果不是这种状态，则一律将 promise 拒绝。

尽管服务器成功地接收到了响应数据，但这并不意味着我们完全清楚了。因为我们的目标是从服务器端获取 JSON 格式的数据，而 JSON 代码很容易出现语法错误。所以我们把对 JSON.parse 的调用包裹在一个 try-catch 语句中。如果在解析服务器响应内容的时候发生错误，我们同样需要拒绝掉 promise。以上，我们已经把所有可能出现的错误场景考虑到了。如果一切都按计划进行，那我们就能够成功获取需要的所有对象，从而安全地解决该 promise。最后，使用 getJSON 函数从服务器中获取「忍者」数据：

本例中有 3 个潜在的错误源：客户端和服务器之间的连接错误、服务器返回错误的数据（无效响应状态码），以及无效的 JSON 代码。但从使用了 getJSON 函数的角度来说，我们不必关心错误源的种类。我们只需提供一个回调函数，当一切正常工作且数据也正确返回时触发该回调函数，并提供另一个回调函数，当任何错误发生时触发该回调函数。这种方式能减轻开发者的工作量。现在我们可以深入挖掘并探索 promise 的另一个最大优点：优雅的编码方式。通过一连串不同步骤中的链式调用多个 promise 来展开这个话题。

#### 6.3.5 Chaining promises

You've already seen how handling a sequence of interdependent steps leads to the pyramid of doom, a deeply nested and difficult-to-maintain sequence of callbacks. Promises are a step toward solving that problem, because they have the ability to be chained.

Earlier in the chapter, you saw how, by using the then method on a promise, we can register a callback that will be executed if a promise is successfully resolved. What we didn't tell you is that calling the then method also returns a new promise. So there's nothing stopping us from chaining as many then methods as we want; see the following code.

Listing 6.16 Chaining promises with then

```js
getJSON("data/ninjas.json")
  .then(ninjas => getJSON(ninjas[0].missionsUrl)) 
  .then(missions => getJSON(missions[0].detailsUrl)) 
  .then(mission => assert(mission !== null, "Ninja mission obtained!")) 
  .catch(error => fail("An error has occurred"));
```

This creates a sequence of promises that will be, if everything goes according to plan, resolved one after another. First, we use the `getJSON("data/ninjas.json")` method to fetch a list of ninjas from the file on the server. After we receive that list, we take the information about the first ninja, and we request a list of missions the ninja is assigned to: `getJSON(ninjas[0].missionsUrl)`. Later, when these missions come in, we make yet another request for the details of the first mission: `getJSON(missions[0].detailsUrl)`. Finally, we log the details of the mission.

Writing such code using standard callbacks would result in a deeply nested sequence of callbacks. Identifying the exact sequence of steps wouldn't be easy, and God forbid we decide to add in an extra step somewhere in the middle.

CATCHING ERRORS IN CHAINED PROMISES

When dealing with sequences of asynchronous steps, an error can occur in any step. We already know that we either can provide a second, error callback to the then call, or can chain in a catch call that takes an error callback. When we care about only the success/failure of the entire sequence of steps, supplying each step with special error handling might be tedious. So, as shown in listing 6.16, we can take advantage of the catch method that you saw earlier:

```js
...catch(error => fail("An error has occurred:" + err));
```

If a failure occurs in any of the previous promises, the catch method catches it. If no error occurs, the program flow continues through it, unobstructed.

Dealing with a sequence of steps is much nicer with promises than with regular callbacks, wouldn't you agree? But it's still not as elegant as it could be. We'll get to that soon, but first let's see how to use promises to take care of parallel asynchronous steps.

6.3.5 链式调用 promise 

你已经见过处理一连串相互关联步骤导致的金字塔噩梦，嵌套太深将形成难以维护的回调函数序列。由于 promise 可以链式调用，故它也是用于解决该问题的重要一步。

本章的前面部分，已看过了如何在 promise 上使用 then 函数，我们可以在 then 函数上注册一个回调函数，一旦 promise 成功兑现就会触发该回调函数。还有一个秘密是调用 then 方法后还会再返回一个新的 promise 对象。所以没有什么能够阻止我们按照我们的需要链式调用许多 then 方法。请看清单 6.16 的代码。

如果一切按计划执行，这段代码会创建一系列 promise，一个接一个地被解决。首先使用 `getJSON ("data/ninjas.json")` 方法从服务器中的文件上获取一个「忍者」列表数据。接收到这个列表后，就可以把信息告诉第一位「忍者」，然后请求分给该「忍者」的任务列表：`getJSON (ninjas [0].missionsUrl)`。当任务到达时，开始请求第一项任务的详情：`getJSON (missions [0].details-Url)`。最后把任务详情写入日志。

使用标准回调函数书写上述代码会生成很深的嵌套回调函数序列。很难准确地识别出当前进行到哪一步，在序列中增加一个额外的步骤也非常棘手。

Promise 链中的错误捕捉

当处理一连串异步任务步骤的时候，任何一步都可能出现错误。我们已经知晓，既可以通过 then 方法传递第二个回调函数，也可以链式地调用一个 catch 方法并向其中传入错误处理回调函数。当我们仅关心整个序列步骤的成功 / 失败时，为每一步都指定错误处理函数就显得很冗长乏味。所以如清单 6.16 所示，我们可以利用前面看到的 catch 方法：

如果错误在前面的任何一个 promise 中产生，catch 方法就会捕捉到它。如果没发生任何错误，则程序流程只会无障碍地继续通过。用 promise 处理一连串步骤比常规回调函数更加方便，你同意吧？但现在的代码还不够优雅。我们马上就会学习到，但现在先看看 promise 是如何处理并行 promise 步骤的。

#### 6.3.6 Waiting for a number of promises

In addition to helping us deal with sequences of interdependent, asynchronous steps, promises significantly reduce the burden of waiting for several independent asynchronous tasks. Let's revisit our example in which we want to, in parallel, gather information about the ninjas at our disposal, the intricacies of the plan, and the map of the location where the plan will be set in motion. With promises, this is as simple as shown in the following listing.

Listing 6.17 Waiting for a number of promises with Promise.all

```js
// The Promise.all method takes an array of promises, 
// and creates a new promise that succeeds if all promises succeed, 
// and fails if even one promise fails.
Promise.all([getJSON("data/ninjas.json"),
            getJSON("data/mapInfo.json"), 
            getJSON("data/plan.json")]).then(results => { 
  // The result is an array of succeed values, in the order of passedin promises.
  const ninjas = results[0], mapInfo = results[1], plan = results[2];
  
  assert(ninjas !== undefined && mapInfo !== undefined && plan !== undefined,
      "The plan is ready to be set in motion!"); 
}).catch(error => {
  fail("A problem in carrying out our plan!"); 
});
```

As you can see, we don't have to care about the order in which tasks are executed, and whether some of them have finished, while others didn't. We state that we want to wait for a number of promises by using the built-in Promise.all method. This method takes in an array of promises and creates a new promise that successfully resolves when all passed-in promises resolve, and rejects if even one of the promises fails. The succeed callback receives an array of succeed values, one for each of the passed-in promises, in order. Take a minute to appreciate the elegance of code that processes multiple parallel asynchronous tasks with promises.

The Promise.all method waits for all promises in a list. But at times we have numerous promises, but we care only about the first one that succeeds (or fails). Meet the Promise.race method.

RACING PROMISES

Imagine that we have a group of ninjas at our disposal, and that we want to give an assignment to the first ninja who answers our call. When dealing with promises, we can write something like the following listing.

Listing 6.18 Racing promises with Promise.race

```js
Promise.race([getJSON("data/yoshi.json"),
              getJSON("data/hattori.json"), 
              getJSON("data/hanzo.json")]) 
        .then(ninja => { 
          assert(ninja !== null, ninja.name + " responded first");
        }).catch(error => fail("Failure!"));
```

It's simple as that. There's no need for manually tracking everything. We use the Promise.race method to take an array of promises and return a completely new promise that resolves or rejects as soon as the first of the promises resolves or rejects.

So far you've seen how promises work, and how we can use them to greatly simplify dealing with a series of asynchronous steps, either in series or in parallel. Although the improvements, when compared to plain old callbacks in terms of error handling and code elegance, are great, promisified code still isn't on the same level of elegance as simple synchronous code. In the next section, the two big concepts that we've introduced in this chapter, generators and promises, come together to provide the simplicity of synchronous code with the nonblocking nature of asynchronous code.

6.3.6 等待多个 promise 

除了处理相互依赖的异步任务序列以外，对于等待多个独立的异步任务，promise 也能够显著地减少代码量。让我们再来看一个并行执行的例子：

获取可以被我们支配的「忍者」列表、复杂的计划，以及行动执行地点的地图。如清单 6.17 所示，这个任务可以很方便地用 promise 来处理。

如你所见，我们不必关心任务执行的顺序，以及它们是不是都已经进入完成态。通过使用内置方法 Promise.all 可以等待多个 promise。这个方法将一个 promise 数组作为参数，然后创建一个新的 promise 对象，一旦数组中的 promise 全部被解决，这个返回的 promise 就会被解决，而一旦其中有一个 promise 失败了，那么整个新 promise 对象也会被拒绝。后续的回调函数接收成功值组成的数组，数组中的每一项都对应 promise 数组中的对应项。花一分钟欣赏一下处理多个并行的异步任务的代码是多么优雅。Promise.all 方法等待列表中的所有 promise。但如果我们只关心第一个成功（或失败）的 promise，可以认识一下 Promise.race 方法。

promise 竞赛

假设我们可以支配一队「忍者」，我们希望给第一个回答命令的「忍者」分配一个任务。如清单 6.18 所示，为了完成上述任务，我们可以书写类似的代码。例子很简单，不需要手动跟踪所有代码。使用 Promise.race 方法并传入一个 promise 数组会返回一个全新的 promise 对象，一旦数组中某一个 promise 被处理或被拒绝，这个返回的 promise 就同样会被处理或被拒绝。

到目前为止，你已经学习了 promise 是如何工作的，如何用 promise 并行或者串行的方式简化一连串的异步任务。比起最原始回调函数的错误处理和代码优雅性，尽管有很大改善，但 promise 化的代码和同步代码的简单程度依旧不在同一个级别上。下一节中，我们会介绍本章的两个重要概念，将生成器和 promise 结合，从而以优雅的同步代码方式完成异步任务。

### 6.4 Combining generators and promises

In this section, we'll combine generators (and their capability to pause and resume their execution) with promises, in order to achieve more elegant asynchronous code. We'll use the example of a functionality that enables users to get details of the highestrated mission done by the most popular ninja. The data representing the ninjas, the summaries of their missions, as well as the details of the missions are stored on a remote server, encoded in JSON.

All of these subtasks are long-running and mutually dependent. If we were to implement them in a synchronous fashion, we'd get the following straightforward code:

```js
try { 
  const ninjas = syncGetJSON("data/ninjas.json"); 
  const missions = syncGetJSON(ninjas[0].missionsUrl); 
  const missionDetails = syncGetJSON(missions[0].detailsUrl);  
  //Study the mission description
} catch(e){ 
  //Oh no, we weren't able to get the mission details 
}
```

Although this code is great for its simplicity and error handling, it blocks the UI, which results in unhappy users. Ideally, we'd like to change this code so that no blocking occurs during a long-running task. One way of doing this is by combining generators and promises.

As we know, yielding from a generator suspends the execution of the generator without blocking. To wake up the generator and continue its execution, we have to call the next method on the generator's iterator. Promises, on the other hand, allow us to specify a callback that will be triggered in case we were able to obtain the promised value, and a callback that will be triggered in case an error has occurred.

The idea, then, is to combine generators and promises in the following way: We put the code that uses asynchronous tasks in a generator, and we execute that generator function. When we reach a point in the generator execution that calls an asynchronous task, we create a promise that represents the value of that asynchronous task. Because we have no idea when that promise will be resolved (or even if it will be resolved), at this point of generator execution, we yield from the generator, so that we don't cause blocking. After a while, when the promise gets settled, we continue the execution of our generator by calling the iterator's next method. We do this as many times as necessary. See the following listing for a practical example.

Listing 6.19 Combining generators and promises

```js
// The function using asynchronous results should be able to pause while waiting for results. 
// Notice the function*. We’re using generators!
async(function*() {
  try { 
    // Yield on each asynchronous task.
    const ninjas = yield getJSON("data/ninjas.json"); 
    const missions = yield getJSON(ninjas[0].missionsUrl); 
    const missionDescription = yield getJSON(missions[0].detailsUrl);
    //Study the mission details
  } catch(e) { 
    // Oh no, we weren't able to get the mission details 
  } 
}); 

// Defines a helper function that will control our generator
function async(generator) { 
  // Creates an iterator through which we'll control the generator
  var iterator = generator();
  // Defines the function that will handle each value generated by the generator
  function handle(iteratorResult) { 
    // Stops when the generator has no more results
    if(iteratorResult.done) { return; }
    const iteratorValue = iteratorResult.value;
    // If the generated value is a promise, register a success and a failure callback. 
    // This is the asynchronous part. If the promise succeeds, great, resume the generator and send in the promised value. 
    // If there’s an error, throw an exception to the generator.
    if(iteratorValue instanceof Promise) { 
      iteratorValue.then(res => handle(iterator.next(res)) 
                    .catch(err => iterator.throw(err)));
    }
  }
  // Restarts the generator execution.
  try { 
    handle(iterator.next()); 
  } catch (e) { iterator.throw(e); }
}
```

The async function takes a generator, calls it, and creates an iterator that will be used to resume the generator execution. Inside the async function, we declare a handle function that handles one return value from the generator — one "iteration" of our iterator. If the generator result is a promise that gets resolved successfully, we use the iterator's next method to send the promised value back to the generator and resume the generator's execution. If an error occurs and the promise gets rejected, we throw that error to the generator by using the iterator's throw method (told you it would come in handy). We keep doing this until the generator says it's done.

NOTE: This is a rough sketch, a minimum amount of code needed to combine generators and promises. We don't recommend that you use this code in production.

Now let's take a closer look at the generator. On the first invocation of the iterator's next method, the generator executes up to the first `getJSON("data/ninjas.json")` call. This call creates a promise that will eventually contain the list of information about our ninjas. Because this value is fetched asynchronously, we have no idea how much time it will take the browser to get it. But we know one thing: We don't want to block the application execution while we're waiting. For this reason, at this moment of execution, the generator yields control, which pauses the generator, and returns the control flow to the invocation of the handle function. Because the yielded value is a getJSON promise, in the handle function, by using the then and catch methods of the promise, we register a success and an error callback, and continue execution. With this, the control flow leaves the execution of the handle function and the body of the async function, and continues after the call to the async function (in our case, there's no more code after, so it idles). During this time, our generator function patiently waits suspended, without blocking the program execution.

Much, much later, when the browser receives a response (either a positive or a negative one), one of the promise callbacks is invoked. If the promise was resolved successfully, the success callback is invoked, which in turn causes the execution of the iterator's next method, which asks the generator for another value. This brings back the generator from suspension and sends to it the value passed in by the callback. This means that we reenter the body of our generator, after the first yield expression, whose value becomes the ninjas list that was asynchronously fetched from the server. The execution of the generator function continues, and the value is assigned to the plan variable.

In the next line of the generator, we use some of the obtained data, ninjas[0] .missionUrl, to make another getJSON call that creates another promise that should eventually contain a list of missions done by the most popular ninja. Again, because this is an asynchronous task, we have no idea how long it's going to take, so we again yield the execution and repeat the whole process.

This process is repeated as long as there are asynchronous tasks in the generator.

This was a tad on the complex side, but we like this example because it combines a lot of things that you've learned so far:

1 Functions as first-class objects — We send a function as an argument to the async function.

2 Generator functions — We use their ability to suspend and resume execution.

3 Promises — They help us deal with asynchronous code.

4 Callbacks — We register success and failure callbacks on our promises.

5 Arrow functions — Because of their simplicity, for callbacks we use arrow functions.

6 Closures — The iterator, through which we control the generator, is created in the async function, and we access it, through closures, in the promise callbacks.

Now that we've gone through the whole process, let's take a minute to appreciate how much more elegant the code that implements our business logic is. Consider this:

```js
getJSON("data/ninjas.json", (err, ninjas) => { 
  if(err) { console.log("Error fetching ninjas", err); return; }

  getJSON(ninjas[0].missionsUrl, (err, missions) => { 
    if(err) { console.log("Error locating ninja missions", err); return; } 
    console.log(misssions); 
  }) 
});
```

Instead of mixed control-flow and error handling, and slightly confusing code, we end up with something like this:

```js
async(function*() {
  try { 
    const ninjas = yield getJSON("data/ninjas.json"); 
    const missions = yield getJSON(ninjas[0].missionsUrl);
    //All information recieved
  } catch(e) { 
    //An error has occurred 
  } 
});
```

This end result combines the advantages of synchronous and asynchronous code. From synchronous code, we have the ease of understanding, and the ability to use all standard control-flow and exception-handling mechanisms such as loops and try-catch statements. From asynchronous code, we get the nonblocking nature; the execution of our application isn't blocked while waiting for long-running asynchronous tasks.

6.4 把生成器和 promise 相结合

本节中，我们将结合生成器（以及生成器暂停和恢复执行的能力）和 promise，来实现更加优雅的异步代码。下面的例子展示了被最受欢迎「忍者」完成率最高的任务详情。它包含了「忍者」、任务总结，以及任务详情。这些数据都被存放在远程服务器上，并以 JSON 形式编码。所有这些子任务都是长期运行且相互依赖的。如果用同步的方式来实现可以得到如下的代码。

尽管这段代码对于简化错误处理很方便，但 UI 被阻塞了，用户不希望看到这个结果。所以我们最好修改这段代码，让其运行长时间任务也不会发生阻塞。一种方法是将生成器和 promise 相结合。如我们所见，从生成器中让渡后会挂起执行而不会发生阻塞。而且仅需调用生成器迭代器的 next 方法就可以唤醒生成器并继续执行。而 promise 在未来触发某种条件的情况下让我们得到它事先许诺的值，而且当错误发生后也会执行相应的回调函数。

这个方法将要以如下方式结合生成器和 promise：把异步任务放入一个生成器中，然后执行生成器函数。因为我们没办法知道承诺什么时候会被兑现（或什么时候调用了 resolved），所以在生成器执行的时候，我们会将执行权让渡给生成器，从而不会导致阻塞。过了一会儿，当承诺被兑现，我们会继续通过迭代器的 next 函数执行生成器。只要有需要就可以重复这个过程。清单 6.19 列出了实际的例子：

async 函数获取了一个生成器，调用它并创建了一个迭代器用来恢复生成器的执行。在 async 函数内，我们声明了一个处理函数用于处理从生成器中返回的值 —— 迭代器的一次「迭代」。如果生成器的结果是一个被成功兑现的承诺，我们就是用迭代器的 next 方法把承诺的值返回给生成器并恢复执行。如果出现错误，承诺被违背，我们就使用迭代器的 throw 方法（告诉过你迟早能派上用场了）抛出一个异常。直到生成器的工作完成前，我们都会一直重复这几个操作。

注意：这只是个粗略的草稿，一个最小化的代码应该把生成器和 promise 结合在一起。不推荐在生产环境下使用这种代码。

现在让我们来仔细看看这个生成器，在第一次调用迭代器的 next 方法后，生成器执行第一次 `getJSON("data/ninjas.json")` 调用。此次调用创建了一个 promise，该 promise 最终会包含「忍者」的信息。但因为这个值是异步获取的，所以我们完全不知道浏览器会花多少时间来获取它。但我们明白一件事：我们不想在等待中阻塞应用的执行。所以对于这个原因，在执行的这一刻，生成器让渡了控制权，生成器暂停，并把控制流还给了回调函数的执行。由于让渡的值是一个 promise 对象 getJSON，在这个回调函数中，通过使用 promise 的 then 和 catch 方法，我们注册了一个 success 和一个 error 回调函数，从而继续了函数的执行。然后，控制流就离开了处理函数的执行及 async 函数的函数体，直到调用 async 函数后才继续执行。（本例后面没有其他代码了，故程序转为空闲转台）这一次，生成器函数耐心地等待着挂起，也没有阻塞程序的执行。

又过了很久，当浏览器接收到了响应（可能是成功响应，也可能是失败响应）, promise 的两个回调函数之一则被调用了。如果 promise 被成功解决，则会执行 success 回调函数，随之而来则是迭代器 next 方法的调用，用于向生成器请求新的值，从而生成器从挂起状态恢复，并把得到的值回传给回调函数。这意味着，程序又重新进入到生成器函数体内，当第一次执行 yield 表达式后，得到的值变成从服务器端获取的「忍者」列表。生成器函数继续执行下去，得到的值也被赋给 plan 变量。下一行代码的生成器函数中，我们使用获取到的数据 ninjas [0].missionUrl 来发起新的 getJSON 请求，从而创建了一个新的 promise 对象，最后会返回最受欢迎的「忍者」列表数据。我们依然无法得知这个异步任务要进行多久，所以我们再一次让渡了这次执行，并重复更个过程。只要生成器中有异步任务，这个过程就会重复一次。这个例子有点儿不同，但它结合了我们前面所学到的很多内容。

1、函数是第一类对象 —— 我们向 async 函数传入了一个参数，该参数也是函数。

2、生成器函数 —— 用它的特性来挂起和恢复执行。

3、promise—— 帮我们处理异步代码。

4、回调函数 —— 在 promise 对象上注册成功和失败的回调函数。

5、箭头函数 —— 箭头函数的简洁适合用在回调函数上。

6、闭包 —— 在我们控制生成器的过程中，迭代器在 async 函数内被创建，随之我们在 promise 的回调函数内通过闭包来获取该迭代器。

现在我们已经看过了所有过程，花一分钟欣赏一下实现业务逻辑的代码是多么优雅吧。看这段代码：

不同于把错误处理和控制流混合在一起，我们使用类似以下写法结束了代码的凌乱：

最终结果结合了同步代码和异步代码的优点。有了同步代码，我们能更容易地理解、使用标准控制流以及异常处理机制、try-catch 语句的能力。而对于异步代码来说，我们有着天生的非阻塞：当等待长时间运行的异步任务时，应用的执行不会被阻塞。

#### 6.4.1 Looking forward — the async function 

Notice that we still had to write some boilerplate code; we had to develop an async function that takes care of handling promises and requesting values from the generator. Although we can write this function only once and then reuse it throughout our code, it would be even nicer if we didn't have to think about it. The people in charge of JavaScript are well aware of the usefulness of the combination of generators and promises, and they want to make our lives even easier by building in direct language support for mixing generators and promises.

For these situations, the current plan is to include two new keywords, async and await, that would take care of this boilerplate code. Soon, we'll be able to write something like this:

```js
(async function () {
  try { 
    const ninjas = await getJSON("data/ninjas.json"); 
    const missions = await getJSON(missions[0].missionsUrl);
  console.log(missions);
  }
  catch(e) { 
    console.log("Error: ", e); 
  } 
})()
```

1-3『此时此刻才意识到，async/await 语法是对「Promise/Generator」组合实现封装的「语法糖」。同时想起了 winter 在「重学前端」专栏课里提到的信息：generator/iterator 也常常被跟异步一起来讲，我们必须说明 generator/iterator 并非异步代码，只是在缺少 async/await 的时候，一些框架（最著名的要数 co）使用这样的特性来模拟 async/await。但是 generator 并非被设计成实现异步，所以有了 async/await 之后，generator/iterator 来模拟异步的方法应该被废弃。async/await 语法，做一张主题卡片。（2021-05-05）』—— 已完成

We use the async keyword in front of the function keyword to specify that this function relies on asynchronous values, and at every place where we call an asynchronous task, we place the await keyword that says to the JavaScript engine, please wait for this result without blocking. In the background, everything happens as we've discussed previously throughout the chapter, but now we don't need to worry about it.

Async functions will appear in the next installment of JavaScript. Currently no browser supports it, but you can use transpilers such as Babel or Traceur if you wish to use async in your code today.

6.4.1 面向未来的 async 函数

可以看到我们仍然需要书写一些样板代码，所以我们此时需要一个 async 函数能够管理所有 promise 函数的调用，还要管理所有向生成器发出的请求。虽然我们可以在代码中只书写一次这个过程，然后每次需要的时候对其进行复用，但如果我们完全不用关心这个问题就更好了。负责维护 JavaScript 的人们也注意到了将生成器和 promise 相结合的强大效果，因而他们也希望直接借助语言层面来支持这个特性，从而使我们的开发更便捷。在这种形势下，当前的 JavaScript 标准计划新增了两个关键字，用于替代上述样板代码。很快我们就能以类似下面的形式书写代码了：

通过在关键字 function 之前使用关键字 async，可以表明当前的函数依赖一个异步返回的值。在每个调用异步任务的位置上，都要放置一个 await 关键字，用来告诉 JavaScript 引擎，请在不阻塞应用执行的情况下在这个位置上等待执行结果。在这个过程背后，其实发生着本章前面所讨论内容，但现在我们不必关心这个过程的内部细节。

注意：在 JavaScript 的下一个版本中将会新增 async 函数。现阶段还没有浏览器对其进行支持，但通过 Babel 或者 Traceur 转译代码后，你可以在代码中使用 async 语法。

### 6.5 Exercises

After running the following code, what are the values of variables a1 to a4?

# 0601. Functions for the future: generators and promises

## Summary

1 Generators are functions that generate sequences of values — not all at once, but on a per request basis.

1 Unlike standard functions, generators can suspend and resume their execution. After a generator has generated a value, it suspends its execution without blocking the main thread and patiently waits for the next request.

2 A generator is declared by putting an asterisk (`*`) after the function keyword. Within the body of the generator, we can use the new yield keyword that yields a value and suspends the execution of the generator. If we want to yield to another generator, we use the `yield*` operator.

3 Calling a generator creates an iterator object through which we control the execution of the generator. We request new values from the generator by using the iterator’s next method, and we can even throw exceptions into the generator by calling the iterator’s throw method. In addition, the next method can be used to send in values to the generator.

4 A promise is a placeholder for the results of a computation; it’s a guarantee that eventually we’ll know the result of the computation, most often an asynchronous computation. A promise can either succeed or fail, and after it has done so, there will be no more changes.

5 Promises significantly simplify our dealings with asynchronous tasks. We can easily work with sequences of interdependent asynchronous steps by using the then method to chain promises. Parallel handling of multiple asynchronous steps is also greatly simplified; we use the Promise.all method.

6 We can combine generators and promises to deal with asynchronous tasks with the simplicity of synchronous code.

1、生成器是一种不会在同时输出所有值序列的函数，而是基于每次的请求生成值。

2、不同于标准函数，生成器可以挂起和回复它们的执行状态。当生成器生成了一个值后，它将会在不阻塞主线程的基础上挂起执行，随后静静地等待下次请求。

3、生成器通过在 function 后面加一个星号（`*`）来定义。在生成器函数体内，我们可以使用新的关键字 yield 来生成一个值并挂起生成器的执行。如果我们想让渡到另一个生成器中，可以使用 yield 操作符。

4、在我们控制生成器的执行过程中，通过使用迭代器的 next 方法调用一个生成器，它能够创建一个迭代器对象。除此之外，我们还能够通过 next 函数向生成器中传入值。

5、promise 是计算结果值的一个占位符，它是对我们最终会得到异步计算结果的一个保证。promise 既可以成功也可以失败，一旦设定好了，就不能够有更多改变。

6、promise 显著地简化了我们处理异步代码的过程。通过使用 then 方法来生成 promise 链，我们就能轻易地处理异步时序依赖。并行执行多个异步任务也同样简单：仅使用 Promise.all 方法即可。

7、通过将生成器和 promise 相结合我们能够使用同步代码来简化异步任务。

## 6.0 

This chapter covers: 1) Continuing function execution with generators. 2) Handling asynchronous tasks with promises. 3) Achieving elegant asynchronous code by combining generators and promises.

In the previous three chapters, we focused on functions, specifically on how to define functions and how to use them to great effect. Although we’ve introduced some ES6 features, such as arrow functions and block scopes, we’ve mostly been exploring features that have been part of JavaScript for quite some time. This chapter tackles the cutting edge of ES6 by presenting generators and promises, two completely new JavaScript features. Generators and promises are both introduced by ES6. You can check out current browser support at http://mng.bz/sOs4 and [[ECMAScript 6 compatibility table](http://kangax.github.io/compat-table/es6/#test-Promise)].

1『作者在 6.3.4 小结里讲解了如何用 promise 对象实现从后端请求数据，值得反复研究。』

Generators are a special type of function. Whereas a standard function produces at most a single value while running its code from start to finish, generators produce multiple values, on a per request basis, while suspending their execution between these requests. Although new in JavaScript, generators have existed for quite some time in Python, PHP, and C#.

Generators are often considered an almost weird or fringe language feature not often used by the average programmer. Though most of this chapter’s examples are designed to teach you how generator functions work, we’ll also explore some practical aspects of generators. You’ll see how to use generators to simplify convoluted loops and how to take advantage of generators’ capability to suspend and resume their execution, which can help you write simpler and more elegant asynchronous code.

Promises, on the other hand, are a new, built-in type of object that help you work with asynchronous code. A promise is a placeholder for a value that we don’t have yet but will at some later point. They’re especially good for working with multiple asynchronous steps.

In this chapter, you’ll see how both generators and promises work, and we’ll finish off by exploring how to combine them to greatly simplify our dealings with asynchronous code. But before going into the specifics, let’s take a sneak peek into how much more elegant our asynchronous code can be.

What are some common uses for a generator function? Why are promises better than simple callbacks for asyn-chronous code? Do you know?

You start a number of long-running tasks with Promise .race. When does the promise resolve? When would it fail to resolve?

本章包括以下内容：1）通过生成器让函数持续执行。2）使用 promise 处理异步任务。3）使用生成器和 promise 书写优雅代码。

前 3 章中我们集中讨论了函数，尤其是如何定义函数及如何有效使用函数。我们已经介绍了 ES6 的一些特性，例如箭头函数和块作用域，我们学习过的大部分特性在很久前就已经是 JavaScript 的一部分。这一章将探索两个全新的 ES6 的前沿特性：生成器（generator）和 promise（promise）。

注意：生成器和 promise 已经引入到 ES6 中。可以通过 http://mng.bz/sOs4 和 http://mng.bz/Du38 来查看浏览器的支持情况。

生成器是一种特殊类型的函数。当从头到尾运行标准函数时，它最多只生成一个值。然而生成器函数会在几次运行请求中暂停，因此每次运行都可能会生成一个值。虽然生成器对 JavaScript 来说还是个新特性，其实它已经在 Pyhton、PHP 和 C# 中存在很长时间了。生成器经常被当作一种古怪不常用的语言特性，普通水平的程序员一般不会使用这个特性。然而本章中大部分例子都是来教你怎样使用生成器函数的，我们还会探索生成器函数的一些很实用的方面。你会学到如何使用生成器来简化复杂循环，如何利用生成器的能力来挂起和恢复循环的执行，这些技巧都能帮你写出更简单、更优雅的异步代码。

另外，对象的一个新的内置类型 promise，也能帮你编写异步代码。promise 对象是一个占位符，暂时替代那些尚未计算出但未来会计算出的值。对于多个异步操作来说，使用 promise 对象是非常有好处的。

你知道吗？1）生成器函数的主要用途是什么？2）在异步代码中，为什么使用 promise 比使用简单的回调函数更好？3）使用 Promise.race 来执行很多长期执行的任务时，promise 最终会在什么时候变成 resolved 状态？它什么时候会无法变成 resolved 状态？

## 6.1 Making our async code elegant with generators and promises

Imagine that you’re a developer working at freelanceninja.com, a popular freelance ninja recruitment site enabling customers to hire ninjas for stealth missions. Your task is to implement a functionality that lets users get details about the highest-rated mission done by the most popular ninja. The data representing the ninjas, the summaries of their missions, as well as the details of the missions are stored on a remote server, encoded in JSON. You might write something like this:

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

This code is relatively easy to understand, and if an error occurs in any of the steps, we can easily catch it in the catch block. But unfortunately, this code has a big problem. Getting data from a server is a long-running operation, and because JavaScript relies on a single-threaded execution model, we’ve just blocked our UI until the long-running operations finish. This leads to unresponsive applications and disappointed users. To solve this problem, we can rewrite it with callbacks, which will be invoked when a task finishes, without blocking the UI:

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

Although this code will be much better received by our users, you’ll probably agree that it’s messy, it adds a lot of boilerplate error-handling code, and it’s plain ugly. This is where generators and promises jump in. By combining them, we can turn the nonblocking but awkward callback code into something much more elegant:

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

Don’t worry if this example doesn’t make much sense or if you find some of the syntax (such as function* or yield) unfamiliar. By the end of this chapter, you’ll meet all the necessary ingredients. For now, it’s enough that you compare the elegance (or the lack thereof) of the nonblocking callback code and the nonblocking generators and promises code.

Let’s start slowly by exploring generator functions, the first stepping stone toward elegant asynchronous code.

6.1 使用生成器和 promise 编写优雅的异步代码

想象你是在 freelancenijia.com 工作的开发者，这是一个流行的自由职业「忍者」招聘网站，为客户招募执行秘密任务的「忍者」。你的任务是实现一个功能，用于让用户了解由最受欢迎的「忍者」完成任务的任务详情。将「忍者」、任务摘要以及任务详情的数据存储展示在远程服务器上，并以 JSON 格式编码。你需要编写类似下面的代码：

这段代码很容易理解，如果其中任何一步出了错误，catch 代码块都能很轻易地捕捉。但很不幸，这样的代码有很大问题。从服务器中获取数据是一个长时间操作，而 JavaScript 依赖于单线程执行模型，所以一直到长时间的操作结束之前，UI 的渲染都会暂停。随后的应用都会无响应，用户会感到不满。我们可以用回调函数解决这个问题，这样每个任务结束后都调用回调函数，从而不会导致 UI 暂停。

尽管这段代码能够显著地提升用户体验，但你也会认同这段代码写得很散乱，其中包含着大量的错误处理样板代码，这样的写法看起来很丑陋。这就是生成器函数和 promise 大显身手的时候了。引入这两种技术后，非阻塞但却丑陋的回调函数代码就会变得更优雅：

如果你不能理解这个例子，或者其中的某些语法你并不熟悉（例如 `function*` 或 yield），不要担心。读完本章，你将能够理解所有的关键要素。至于你现在阅读的这段代码，比起非阻塞回调函数代码，使用生成器和 promise 明显更为优雅。让我们开始慢慢探索生成器函数，它是通往优雅异步代码的第一块垫脚石。

## 6.2 Working with generator functions

Generators are a completely new type of function and are significantly different from standard, run-of-the-mill functions. A generator is a function that generates a sequence of values, but not all at once, as a standard function would, but on a per request basis. We have to explicitly ask the generator for a new value, and the generator will either respond with a value or notify us that it has no more values to produce. What’s even more curious is that after a value is produced, a generator function doesn’t end its execution, as a normal function would. Instead, a generator is merely suspended. Then, when a request for another value comes along, the generator resumes where it left off.

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

The result of invoking this for-of loop is shown in figure 6.2. (For now, don’t worry much about the for-of loop, as we’ll explore it later.)

On the right side of the for-of loop, we’ve placed the result of invoking our generator. But if you take a closer look at the body of the WeaponGenerator function, you’ll see that there’s no return statement. What’s up with that? In this case, shouldn’t the right side of the for-of loop evaluate to undefined, as would be the case if we were dealing with a standard function?

The truth is that generators are quite unlike standard functions. For starters, calling a generator doesn’t execute the generator function; instead it creates an object called an iterator. Let’s explore that object.

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

6.2 使用生成器函数生成器函数

几乎是一个完全崭新的函数类型，它和标准的普通函数完全不同。生成器（generator）函数能生成一组值的序列，但每个值的生成是基于每次请求，并不同于标准函数那样立即生成。我们必须显示地向生成器请求一个新的值，随后生成器要么响应一个新生成的值，要么就告诉我们它之后都不会再生成新值。更让人好奇的是，每当生成器函数生成了一个值，它都不会像普通函数一样停止执行。相反，生成器几乎从不挂起。随后，当对另一个值的请求到来后，生成器就会从上次离开的位置恢复执行。

清单 6.1 提供了一个简单例子，它使用生成器函数生成了一系列武器数据。

清单 6.1 使用生成器函数生成一些列值 

例子首先定义了一个生成器，它能够生成一系列武器的数据。创建一个生成器函数非常简单：仅仅需要在关键字 function 后面加上一个星号（`*`）。这样一来生成器函数体内就能够使用新关键字 yield，从而生成独立的值。

图 6.1 解释了 yield 的语法。

图 6.1 在关键字 function 后面增加一个星号来定义一个生成器本例创建了一个叫作 WeaponGenerator 的生成器，其用于生成一系列武器数据：Katana、Wakizashi 和 Kusarigama。作为取出武器数据序列值的方法之一，for-of 是一种用于循环结构新类型：

for-of 循环的执行结果如图 6.2 所示（现在不必太关心 for-of 循环，稍后我们会对它进行介绍）。

图 6.2 迭代函数 WeaponGenerator() 得到的结果我们把执行生成器得到的结果放在 for-of 循环的右边。但如果你仔细看看 WeaponGenerator 函数的函数体，你会发现其中并没有 return 语句。这是为什么？这个例子中，for-of 循环的右边不是应该得到 undefined，就像我们处理一个标准函数一样吗？

真相是生成器函数和标准函数非常不同。对初学者来说，调用生成器并不会执行生成器函数，相反，它会创建一个叫作迭代器（iterator）的对象。让我们来探索这个对象吧。

### 6.2.1 Controlling the generator through the iterator object

Making a call to a generator doesn’t mean that the body of the generator function will be executed. Instead, an iterator object is created, an object through which we can communicate with the generator. For example, we can use the iterator to request additional values. Let’s adjust our previous example to explore how the iterator object works.

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

As soon as the current value is produced, the generator suspends its execution without blocking and patiently waits for another value request. This is an incredibly powerful feature that standard functions don’t have, a feature that we’ll use later to great effect.

In this case, the first call to the iterator’s next method executes the generator code to the first yield expression, yield "Katana", and returns an object with the property value set to Katana and the property done set to false, signaling that there are more values to produce.

Later, we request another value from the generator, by making another call to the weaponIterator’s next method:

```js
const result2 = weaponsIterator.next();
```

This wakes up the generator from suspension, and the generator continues where it left off, executing its code until another intermediary value is reached: yield "Wakizashi". This suspends the generator and produces an object carrying Wakizashi.

Finally, when we call the next method for the third time, the generator resumes its execution. But this time there’s no more code to execute, so the generator returns an object with value set to undefined, and done set to true, signaling that it’s done with its work.

Now that you’ve seen how to control generators through iterators, you’re ready to learn how to iterate over the produced values.

ITERATING THE ITERATOR

The iterator, created by calling a generator, exposes a next method through which we can request a new value from the generator. The next method returns an object that carries the value produced by the generator, as well as the information stored in the done property that tells us whether the generator has additional values to produce.

Now we’ll take advantage of these facts to use a plain old while loop to iterate over values produced by a generator. See the following listing.

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
  // Creates a variable in which we’ll store items of the generated sequence
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

YIELDING TO ANOTHER GENERATOR

Just as we often call one standard function from another standard function, in certain cases we want to be able to delegate the execution of one generator to another. Let’s take a look at an example that generates both warriors and ninjas.

Listing 6.4 Using yield* to delegate to another generator






If you run this code, you’ll see that the output is Sun Tzu, Hattori, Yoshi, Genghis Khan. Generating Sun Tzu probably doesn’t catch you off guard; it’s the first value yielded by the WarriorGenerator. But the second output, Hattori, deserves an explanation.

By using the yield* operator on an iterator, we yield to another generator. In this example, from a WarriorGenerator we’re yielding to a new NinjaGenerator; all calls to the current WarriorGenerator iterator’s next method are rerouted to the NinjaGenerator. This holds until the NinjaGenerator has no work left to do. So in our example, after Sun Tzu, the program generates Hattori and Yoshi. Only when the NinjaGenerator is done with its work will the execution of the original iterator continue by outputting Genghis Khan. Notice that this is happening transparently to the code that calls the original generator. The for-of loop doesn’t care that the WarriorGenerator yields to another generator; it keeps calling next until it’s done.

Now that you have a grasp of how generators work in general and how delegating to another generator works, let’s look at a couple of practical examples.

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




执行这段代码后会输出 Sun Tzu、Hattori、Yoshi、Genghis Khan。第一个输出 Sun Tzu 不会让你感到意外，因为它就是 WarriorGenerator 生成器得到的第一个值。而对于第二个输出的值是 Hattori，我们需要解释一下了。在迭代器上使用 yield * 操作符，程序会跳转到另外一个生成器上执行。本例中，程序从 WarriorGenerator 跳转到一个新的 NinjaGenerator 生成器上，每次调用 WarriorGenerator 返回迭代器的 next 方法，都会使执行重新寻址到了 NinjaGenerator 上。该生成器会一直持有执行权直到无工作可做。所以我们本例中生成 Sun Tzu 之后紧接的是 Hattori 和 Yoshi。仅当 NinjaGenerator 的工作完成后，调用原来的迭代器才会继续输出值 Genghis Khan。注意，对于调用最初的迭代器代码来说，这一切都是透明的。for-of 循环不会关心 WarriorGenerator 委托到另一个生成器上，它只关心在 done 状态到来之前都一直调用 next 方法。现在，对于生成器一般的工作，以及如何代理到其他生成器的工作上，你都已经有所掌握了。让我们看看几个实践中的例子。




### 6.2.2 Using generators

Generating sequences of items is all nice and dandy, but let’s get more practical, starting with a simple case of generating unique IDs.

USING GENERATORS TO GENERATE IDS

When creating certain objects, often we need to assign a unique ID to each object. The easiest way to do this is through a global counter variable, but that’s kind of ugly because the variable can be accidently messed up from anywhere in our code. Another option is to use a generator, as shown in the following listing.

Listing 6.5 Using generators for generating IDs

This example starts with a generator that has one local variable, id, which represents our ID counter. The id variable is local to our generator; there’s no fear that someone will accidently modify it from somewhere else in the code. This is followed by an infinite while loop, which at each iteration yields a new id value and suspends its execution until a request for another ID comes along:

function *IdGenerator(){

let id = 0;

while(true){ yield ++id; }

}

Writing infinite loops isn’t something that we generally want to do in a standard function. But with generators, everything is fine! Whenever the generator encounters a yield statement, the generator execution is suspended until the next method is called again. So every next call executes only one iteration of our infinite while loop and sends back the next ID value.

NOTE

After defining the generator, we create an iterator object:

const idIterator = IdGenerator();

This allows us to control the generator with calls to the idIterator.next() method. This executes the generator until a yield is encountered, returning a new ID value that we can use for our objects:

const ninja1 = { id: idIterator.next().value };

See how simple this is? No messy global variables whose value can be accidentally changed. Instead, we use an iterator to request values from a generator. In addition, if later we need another iterator for tracking the IDs of, for example, samurai, we can initialize a new generator for that.

USING GENERATORS TO TRAVERSE THE DOM

As you saw in chapter 2, the layout of a web page is based on the DOM, a tree-like structure of HTML nodes, in which every node, except the root one, has exactly one parent, and can have zero or more children. Because the DOM is such a fundamental structure in web development, a lot of our code is based around traversing it. One relatively easy way to do this is by implementing a recursive function that will be executed for each visited node. See the following code.

Listing 6.6 Recursive DOM traversal 

In this example, we use a recursive function to traverse all descendants of the element with the id subtree, in the process logging each type of node that we visit. In this case, the code outputs DIV, FORM, INPUT, P, and SPAN.

We’ve been writing such DOM traversal code for a while now, and it has served us perfectly fine. But now that we have generators at our disposal, we can do it differently; see the following code.

Listing 6.7 Iterating over a DOM tree with generators

This listing shows that we can achieve DOM traversals with generators, just as easily as with standard recursion, but with the aditional benefit of not having to use the slightly awkward syntax of callbacks. Instead of processing the subtree of each visited node by recursing another level, we create one generator function for each visited node and yield to it. This enables us to write what’s conceptually recursive code in iterable fashion. The benefit is that we can consume the generated sequence of nodes with a simple for-of loop, without resorting to nasty callbacks.

This example is a particulary good one, because it also shows how to use generators in order to separate the code that’s producing values (in this case, HTML nodes) from the code that’s consuming the sequence of generated values (in this case, the for-of loop that logs the visited nodes), without having to resort to callbacks. In addition, using iterations is, in certain cases, much more natural than recursion, so it’s always good to have our options open.

Now that we’ve explored some practical aspects of generators, let’s go back to a slighty more theoretical topic and see how to exchange data with a running generator.

### 6.2.3 Communicating with a generator

In the examples presented so far, you’ve seen how to return multiple values from a generator by using yield expressions. But generators are even more powerful than that! We can also send data to a generator, thereby achieving two-way communication! With a generator, we can produce an intermediary result, use that result to calculate something else from outside the generator, and then, whenever we’re ready, send completely new data back to the generator and resume its execution. We’ll use this feature to great effect at the end of the chapter to deal with asynchronous code, but for now, let’s keep it simple.

SENDING VALUES AS GENERATOR FUNCTION ARGUMENTS

The easiest way to send data to a generator is by treating it like any other function and using function call arguments. Take a look at the following listing.

Listing 6.8

Sending data to and receiving data from a generator

A function receiving data is nothing special; plain old functions do it all the time. But remember, generators have this amazing power; they can be suspended and resumed. And it turns out that, unlike standard functions, generators can even receive data after their execution has started, whenever we resume them by requesting the next value.

USING THE NEXT METHOD TO SEND VALUES INTO A GENERATOR

In addition to providing data when first invoking the generator, we can send data into a generator by passing arguments to the next method. In the process, we wake up the generator from suspension and resume its execution. This passed-in value is used by the generator as the value of the whole yield expression, in which the generator was currently suspended, as shown in figure 6.3.

In this example, we have two calls to the ninjaIterator’s next method. The first call, ninjaIterator.next(), requests the first value from the generator. Because our generator hasn’t started executing, this call starts the generator, which calculates the value of the expression "Hattori " + action, yields the Hattori skulk value, and suspends the generator’s execution. There’s nothing special about this; we’ve done something similar multiple times throughout this chapter.

Figure 6.3 The first call to ninjaIterator.next() requests a new value from the generator, which returns Hattori skulk and suspends the execution of the generator at the yield expression. The second call to ninjaIterator.next("Hanzo") requests a new value, but also sends the argument Hanzo into the generator. This value will be used as the value of the whole yield expression, and the variable imposter will now carry the value Hanzo.

The interesting thing happens on the second call to the ninjaIterator’s next method: ninjaIterator.next("Hanzo"). This time, we’re using the next method to pass data back to the generator. Our generator function is patiently waiting, suspended at the expression yield ("Hattori " + action), so the value Hanzo, passed as the argument to next(), is used as the value of the whole yield expression. In our case, this means that the variable imposter in imposter = yield ("Hattori " + action) will end up with the value Hanzo.

That’s how we achieve two-way communication with a generator. We use yield to return data from a generator, and the iterator’s next() method to pass data back to the generator.

The next method supplies the value to the waiting yield expression, so if there’s no yield expression waiting, there’s nothing to supply the value to. For this reason, we can’t supply values over the first call to the next method. But remember, if you need to supply an initial value to the generator, you can do so when calling the generator itself, as we did with NinjaGenerator("skulk").

NOTE

THROWING EXCEPTIONS

There’s another, slightly less orthodox, way to supply a value to a generator: by throwing an exception. Each iterator, in addition to having a next method, has a throw method that we can use to throw an exception back to the generator. Again, let’s look at a simple example.

Listing 6.9

Throwing exceptions to generators

Listing 6.9 starts similarly to listing 6.8, by specifying a generator called NinjaGenerator. But this time, the body of the generator is slightly different. We’ve surrounded the whole function body code with a try-catch block:

We then continue by creating an iterator, and getting one value from the generator:

const ninjaIterator = NinjaGenerator(); const result1 = ninjaIterator.next();

Finally, we use the throw method, available on all iterators, to throw an exception back to the generator:

ninjaIterator.throw("Catch this!");

By running this listing, we can see that our exception throwing works as expected, as shown in figure 6.4.

This feature that enables us to throw exceptions back to generators might feel a bit strange at first. Why would we even want to do that? Don’t worry; we won’t keep you in the dark for long. At the end of this chapter, we’ll use this feature to improve asynchronous server-side communication.

Figure 6.4 We can throw exceptions to generators Just be patient a bit longer. from outside a generator.

Now that you’ve seen several aspects of generators, we’re ready to take a look under the hood to see how generators work.

6.2.4 Exploring generators under the hood

So far we know that calling a generator doesn’t execute it. Instead, it creates a new iterator that we can use to request values from the generator. After a generator produces (or yields) a value, it suspends its execution and waits for the next request. So in a way, a generator works almost like a small program, a state machine that moves between states:

■ Suspended start — When the generator is created, it starts in this state. None of the generator’s code is executed.

■ Executing — The state in which the code of the generator is executed. The execution continues either from the beginning or from where the generator was last suspended. A generator moves to this state when the matching iterator’s next method is called, and there exists code to be executed.

■ Suspended yield — During execution, when a generator reaches a yield expression, it creates a new object carrying the return value, yields it, and suspends its execution. This is the state in which the generator is paused and is waiting to continue its execution.

■ Completed — If during execution the generator either runs into a return statement or runs out of code to execute, the generator moves into this state.

Figure 6.5 illustrates these states.

Now let’s supplement this on an even deeper level, by seeing how the execution of generators is tracked with execution contexts.

const ninjaIterator = NinjaGenerator(); Create a new generator in the Suspended start state.

const result1 = ninjaIterator.next(); Activate generator. Move from Suspended start to Executing. Execute up to yield "Hattori" and pause. Move to the Suspended yield state. Return a new object: {value: "Hattori", done: false}.

const result2 = ninjaIterator.next(); Reactivate generator. Move from Suspended yield to Executing. Execute up to yield "Yoshi" and pause. Move to the Suspended yield state. Return a new object: {value: "Yoshi", done: false}.

const result3 = ninjaIterator.next(); Reactivate generator. Move from Suspended yield to Executing. No more code to execute. Move to the Completed state. Return a new object: {value: undefined, done: true}.

Figure 6.5 During execution, a generator moves between states triggered by calls to the matching iterator’s next method.

TRACKING GENERATORS WITH EXECUTION CONTEXTS

In the previous chapter, we introduced the execution context, an internal JavaScript mechanism used to track the execution of functions. Although somewhat special, generators are still functions, so let’s take a closer look by exploring the relationship between them and execution contexts. We’ll start with a simple code fragment:

function* NinjaGenerator(action) { yield "Hattori " + action; return "Yoshi " + action; }

const ninjaIterator = NinjaGenerator("skulk"); const result1 = ninjaIterator.next(); const result2 = ninjaIterator.next();

Here we reuse our generator that produces two values: Hattori skulk and Yoshi skulk.

Now, we’ll explore the state of the application, the execution context stack at various points in the application execution. Figure 6.6 gives a snapshot at two positions in the application execution. The first snapshot shows the state of the application execution before calling the NinjaGenerator function B . Because we’re executing global code, the execution context stack contains only the global execution context, which references the global environment in which our identifiers are kept. Only the NinjaGenerator identifier references a function, while the values of all other identifiers are undefined.

When we make the call to the NinjaGenerator function C

const ninjaIterator = NinjaGenerator("skulk");

the control flow enters the generator and, as it happens when we enter any other function, a new NinjaGenerator execution context item is created (alongside the matching lexical environment) and pushed onto the stack. But because generators are special, none of the function code is executed. Instead, a new iterator, which we’ll refer to in the code as ninjaIterator, is created and returned. Because the iterator is used to control the execution of the generator, the iterator gets a reference to the execution context in which it was created.

An interesting thing happens when the program execution leaves the generator, as shown in figure 6.7. Typically, when program execution returns from a standard function, the matching execution context is popped from the stack and completely discarded. But this isn’t the case with generators.

Figure 6.6 The state of the execution context stack before calling the NinjaGenerator calling the NinjaGenerator function

Figure 6.7

The state of the application when returning from the NinjaGenerator call

The matching NinjaGenerator stack item is popped from the stack, but it’s not discarded, because the ninjaIterator keeps a reference to it. You can see it as an analogue to closures. In closures, we need to keep alive the variables that are alive at the moment the function closure is created, so our functions keep a reference to the environment in which they were created. In this way, we make sure that the environment and its variables are alive as long as the function itself. Generators, on the other hand, have to be able to resume their execution. Because the execution of all functions is handled by execution contexts, the iterator keeps a reference to its execution context, so that it’s alive for as long as the iterator needs it.

Another interesting thing happens when we call the next method on the iterator:

const result1 = ninjaIterator.next();

If this was a standard straightforward function call, this would cause the creation of a new next() execution context item, which would be placed on the stack. But as you might have noticed, generators are anything but standard, and a call to the next method of an iterator behaves a lot differently. It reactivates the matching execution context, in this case, the NinjaGenerator context, and places it on top of the stack, continuing the execution where it left off, as shown in figure 6.8.

Figure 6.8 illustrates a crucial difference between standard functions and generators. Standard functions can only be called anew, and each call creates a new execution context. In contrast, the execution context of a generator can be temporarily suspended and resumed at will.

In our example, because this is the first call to the next method, and the generator hasn’t started executing, the generator starts its execution and moves to the Executing state. The next interesting thing happens when our generator function reaches this point:

yield "Hattori " + action

Figure 6.8 Calling the iterator’s next method reactivates the execution context stack item of the matching generator, pushes it on the stack, and continues where it left off the last time.

The generator determines that the expression equals Hattori skulk, and the evaluation reaches the yield keyword. This means that Hattori skulk is the first intermediary result of our generator and that we want to suspend the execution of the generator and return that value. In terms of the application state, a similar thing happens as before: the NinjaGenerator context is taken off the stack, but it’s not completely discarded, because ninjaIterator keeps a reference to it. The generator is now suspended, and has moved to the Suspended Yield state, without blocking. The program execution resumes in global code, by storing the yielded value to result1. The current state of the application is shown in figure 6.9.

The code continues by reaching another iterator call:

const result2 = ninjaIterator.next();

Figure 6.9 After yielding a value, the generator’s execution context is popped from the stack (but isn’t discarded, because ninjaIterator keeps a reference to it), and the generator execution is suspended (the generator moves to the Suspended yield state).

At this point, we go through the whole procedure once again: we reactivate the NinjaGenerator context referenced by ninjaIterator, push it onto the stack, and continue the execution where we left off. In this case, the generator evaluates the expression "Yoshi " + action. But this time there’s no yield expression, and instead the program encounters a return statement. This returns the value Yoshi skulk and completes the generator’s execution by moving the generator into the Completed state.

Uff, this was something! We went deep into how generators work under the hood to show you that all the wonderful benefits of generators are a side effect of the fact that a generator’s execution context is kept alive if we yield from a generator, and not destroyed as is the case with return values and standard functions.

Now we recommend that you take a quick breather before continuing on to the second key ingredient required for writing elegant asynchronous code: promises.

6.3 Working with promises

In JavaScript, we rely a lot on asynchronous computations, computations whose results we don’t have yet but will at some later point. So ES6 has introduced a new concept that makes handling asynchronous tasks easier: promises.

A promise is a placeholder for a value that we don’t have now but will have later; it’s a guarantee that we’ll eventually know the result of an asynchronous computation. If we make good on our promise, our result will be a value. If a problem occurs, our result will be an error, an excuse for why we couldn’t deliver. One great example of using promises is fetching data from a server; we promise that we’ll eventually get the data, but there’s always a chance that problems will occur.

Creating a new promise is easy, as you can see in the following example.

Listing 6.10

Creating a simple promise

To create a promise, we use the new, built-in Promise constructor, to which we pass a function, in this case an arrow function (but we could just as easily use a function expression). This function, called an executor function, has two parameters: resolve and reject. The executor is called immediately when constructing the Promise object with two built-in functions as arguments: resolve, which we manually call if we want the promise to resolve successfully, and reject, which we call if an error occurs.

This code uses the promise by calling the built-in then method on the Promise object, a method to which we pass two callback functions: a success callback and a failure callback. The former is called if the promise is resolved successfully (if the resolve function is called on the promise), and the latter is called if there’s a problem (either an unhandled exception occurs or the reject function is called on a promise).

In our example code, we create a promise and immediately resolve it by calling the resolve function with the argument Hattori. Therefore, when we call the then method, the first, success, callback is executed and the test that outputs We were promised Hattori! passes.

Now that we have a general idea of what promises are and how they work, let’s take a step back to see some of the problems that promises tackle.

6.3.1 Understanding the problems with simple callbacks We use asynchronous code because we don’t want to block the execution of our application (thereby disappointing our users) while long-running tasks are executing. Currently, we solve this problem with callbacks: To a long-running task we provide a function, a callback that’s invoked when the task is finally done.

For example, fetching a JSON file from a server is a long-running task, during which we don’t want to make the application unresponsive for our users. Therefore, we provide a callback that will be invoked when the task is done:

getJSON("data/ninjas.json", function() { /*Handle results*/ });

Naturally, during this long-running task, errors can happen. And the problem with callbacks is that you can’t use built-in language constructs, such as try-catch statements, in the following way:

This happens because the code invoking the callback usually isn’t executed in the same step of the event loop as the code that starts the long-running task (you’ll see exactly what this means when you learn more about the event loop in chapter 13).

As a consequence, errors usually get lost. Many libraries, therefore, define their own conventions for reporting errors. For example, in the Node.js world, callbacks customarily take two arguments, err and data, where err will be a non-null value if an error occurs somewhere along the way. This leads to the first problem with callbacks: difficult error handling.

After we’ve performed a long-running task, we often want to do something with the obtained data. This can lead to starting another long-running task, which can eventually trigger yet another long-running task, and so on — leading to a series of interdependent, asynchronous, callback-processed steps. For example, if we want to execute a sneaky plan to find all ninjas at our disposal, get the location of the first ninja, and send him some orders, we’d end up with something like this:

getJSON("data/ninjas.json", function(err, ninjas){ getJSON(ninjas[0].location, function(err, locationInfo){ sendOrder(locationInfo, function(err, status){ /*Process status*/ }) }) });

You’ve probably ended up, at least once or twice, with similarly structured code — a bunch of nested callbacks that represent a series of steps that have to be made. You might notice that this code is difficult to understand, inserting new steps is a pain, and error handling complicates your code significantly. You get this “pyramid of doom” that keeps growing and is difficult to manage. This leads us to the second problem with callbacks: performing sequences of steps is tricky.

Sometimes, the steps that we have to go through to get to the final result don’t depend on each other, so we don’t have to make them in sequence. Instead, to save precious milliseconds, we can do them in parallel. For example, if we want to set a plan in motion that requires us to know which ninjas we have at our disposal, the plan itself, and the location where our plan will play out, we could take advantage of jQuery’s get method and write something like this:

In this code, we execute the actions of getting the ninjas, getting the map info, and getting the plan in parallel, because these actions don’t depend on each other. We only care that, in the end, we have all the data at our disposal. Because we don’t know the order in which the data is received, every time we get some data, we have to check whether it’s the last piece of the puzzle that we’re missing. Finally, when all pieces are in place, we can set our plan in motion. Notice that we have to write a lot of boilerplate code just to do something as common as executing a number of actions in parallel. This leads us to the third problem with callbacks: performing a number of steps in parallel is also tricky.

When presenting the first problem with callbacks — dealing with errors — we showed how we can’t use some of the fundamental language constructs, such as trycatch statements. A similar thing holds with loops: If you want to perform asynchronous actions for each item in a collection, you have to jump through some more hoops to get it done.

It’s true that you can make a library to simplify dealing with all these problems (and many people have). But this often leads to a lot of slightly different ways of dealing with the same problems, so the people behind JavaScript have bestowed upon us promises, a standard approach for dealing with asynchronous computation.

Now that you understand most of the reasons behind the introduction of promises, as well as have a basic understanding of them, let’s take it up a notch.

6.3.2 Diving into promises

A promise is an object that serves as a placeholder for a result of an asynchronous task. It represents a value that we don’t have but hope to have in the future. For this reason, during its lifetime, a promise can go through a couple of states, as shown in figure 6.10.

A promise starts in the pending state, in which we know nothing about our promised value. That’s why a promise in the pending state is also called an unresolved promise. During program execution, if the promise’s resolve function is called, the

Figure 6.10

States of a promise

promise moves into the fulfilled state, in which we’ve successfully obtained the promised value. On the other hand, if the promise’s reject function is called, or if an unhandled exception occurs during promise handling, the promise moves into the rejected state, in which we weren’t able to obtain the promised value, but in which we at least know why. Once a promise has reached either the fulfilled state or the rejected state, it can’t switch (a promise can’t go from fulfilled to rejected or vice versa), and it always stays in that state. We say that a promise is resolved (either successfully or not).

The following listing provides a closer look at what’s going on when we use promises.

Listing 6.11

A closer look at promise order of execution

The code in listing 6.11 outputs the results shown in figure 6.11. As you can see, the code starts by logging the “At code start” message by using our custom-made report function (appendix C) that outputs the message onscreen. This enables us to easily track the order of execution.

Next we create a new promise by calling the Promise constructor. This immediately invokes the executor function in which we set up a timeout:

setTimeout(() => { report("Resolving ninjaDelayedPromise"); resolve("Hattori"); }, 500);

The timeout will resolve the promise after 500ms. This could have been any other asynchronous task, but we chose the humble timeout because of its simplicity.

After the ninjaDelayedPromise has been created, it still doesn’t know the value that it will eventually have, or whether it will even be successful. (Remember, it’s still waiting for the timeout that will resolve it.) So after construction, the ninjaDelayedPromise is in the first promise state, pending.

Figure 6.11

The result of executing listing 6.11

Next we use the then method on the ninjaDelayedPromise to schedule a callback to be executed when the promise successfully resolves:

ninjaDelayedPromise.then(ninja => {

assert(ninja === "Hattori",

"ninjaDelayedPromise resolve handled with Hattori");

});

This callback will always be called asynchronously, regardless of the current state of the promise.

We continue by creating another promise, ninjaImmediatePromise, which is resolved immediately during its construction, by calling the resolve function. Unlike the ninjaDelayedPromise, which after construction is in the pending state, the ninjaImmediatePromise finishes construction in the resolved state, and the promise already has the value Yoshi.

Afterward, we use the ninjaImmediatePromise’s then method to register a callback that will be executed when the promise successfully resolves. But our promise is already settled; does this mean that the success callback will be immediately called or that it will be ignored? The answer is neither.

Promises are designed to deal with asynchronous actions, so the JavaScript engine always resorts to asynchronous handling, to make the promise behavior predictable. The engine does this by executing the then callbacks after all the code in the current step of the event loop is executed (once again, we’ll explore exactly what this means in chapter 13). For this reason, if we study the output in figure 6.11, we’ll see that we first log “At code end” and then we log that the ninjaImmediatePromise was resolved. In the end, after the 500ms timeout expires, the ninjaDelayedPromise is resolved, which causes the execution of the matching then callback.

In this example, for the sake of simplicity, we’ve worked only with the rosy scenario in which everything goes great. But the real world isn’t all sunshine and rainbows, so let’s see how to deal with all sorts of crazy problems that can occur.

6.3.3 Rejecting promises

There are two ways of rejecting a promise: explicitly, by calling the passed-in reject method in the executor function of a promise, and implicitly, if during the handling of a promise, an unhandled exception occurs. Let’s start our exploration with the following listing.

Listing 6.12

Explicitly rejecting promises

We can explicitly reject a promise, by calling the passed-in reject method: reject("Explicitly reject a promise!"). If a promise is rejected, when registering callbacks through the then method, the second, error, callback will always be invoked.

In addition, we can use an alternative syntax for handling promise rejections, by using the built-in catch method, as shown in the following listing.

As listing 6.13 shows, we can chain in the catch method after the then method, to also provide an error callback that will be invoked when a promise gets rejected. In this example, this is a matter of personal style. Both options work equally well, but later, when working with chains of promises, we’ll see an example in which chaining the catch method is useful.

In addition to explicit rejection (via the reject call), a promise can also be rejected implicitly, if an exception occurs during its processing. Take a look at the following example.

Listing 6.14

Exceptions implicitly reject a promise

Within the body of the promise executor, we try to increment undeclaredVariable, a variable that isn’t defined in our program. As expected, this results in an exception. Because there’s no try-catch statement within the body of the executor, this results in an implicit rejection of the current promise, and the catch callback is eventually invoked. In this situation, we could have just as easily supplied the second callback to the then method, and the end effect would be the same.

This way of treating all problems that happen while working with promises in a uniform way is extremely handy. Regardless of how the promise was rejected, whether explicitly by calling the reject method or even implicitly, if an exception occurs, all errors and rejection reasons are directed to our rejection callback. This makes our lives as developers a little easier.

Now that we understand how promises work, and how to schedule success and failure callbacks, let’s take a real-world scenario, getting JSON-formatted data from a server, and “promisify” it.

6.3.4 Creating our first real-world promise

One of the most common asynchronous actions on the client is fetching data from the server. As such, this is an excellent little case study on the use of promises. For the underlying implementation, we’ll use the built-in XMLHttpRequest object.

Listing 6.15

Creating a getJSON promise

NOTE

Our goal is to create a getJSON function that returns a promise that will enable us to register success and failure callbacks for asynchronously getting JSON-formatted data from the server. For the underlying implementation, we use the built-in XMLHttpRequest object that offers two events: onload and onerror. The onload event is triggered when the browser receives a response from the server, and onerror is triggered when an error in communication happens. These event handlers will be called asynchronously by the browser, as they occur.

If an error in the communication happens, we definitely won’t be able to get our data from the server, so the honest thing to do is to reject our promise:

request.onerror = function(){ reject(this.status + " " + this.statusText); };

If we receive a response from the server, we have to analyze that response and consider the exact situation. Without going into too much detail, a server can respond with various things, but in this case, we care only that the response is successful (status 200). If it isn’t, again we reject the promise.

Even if the server has successfully responded with data, this still doesn’t mean that we’re in the clear. Because our goal was to get JSON-formatted objects from the server, the JSON code could always have syntax errors. This is why, when calling the JSON.parse method, we surround the code with a try-catch statement. If an exception occurs while parsing the server response, we also reject the promise. With this, we’ve taken care of all bad scenarios that can happen.

If everything goes according to plan, and we successfully obtain our objects, we can safely resolve the promise. Finally, we can use our getJSON function to fetch ninjas from the server:

getJSON("data/ninjas.json").then(ninjas => { assert(ninjas !== null, "Ninjas obtained!");

}).catch(e => fail("Shouldn't be here:" + e));

In this case, we have three potential sources of errors: errors in establishing the communication between the server and the client, the server responding with unanticipated data (invalid response status), and invalid JSON code. But from the perspective of the code that uses the getJSON function, we don’t care about the specifics of error sources. We only supply a callback that gets triggered if everything goes okay and the data is properly received, and a callback that gets triggered if any error occurs. This makes our lives as developers so much easier.

Now we’re going to take it up a notch and explore another big advantage of promises: their elegant composition. We’ll start by chaining several promises in a series of distinct steps.

6.3.5 Chaining promises

You’ve already seen how handling a sequence of interdependent steps leads to the pyramid of doom, a deeply nested and difficult-to-maintain sequence of callbacks. Promises are a step toward solving that problem, because they have the ability to be chained.

Earlier in the chapter, you saw how, by using the then method on a promise, we can register a callback that will be executed if a promise is successfully resolved. What we didn’t tell you is that calling the then method also returns a new promise. So there’s nothing stopping us from chaining as many then methods as we want; see the following code.

Listing 6.16

Chaining promises with then

This creates a sequence of promises that will be, if everything goes according to plan, resolved one after another. First, we use the getJSON("data/ninjas.json") method to fetch a list of ninjas from the file on the server. After we receive that list, we take the information about the first ninja, and we request a list of missions the ninja is assigned to: getJSON(ninjas[0].missionsUrl). Later, when these missions come in, we make yet another request for the details of the first mission: getJSON(missions[0].detailsUrl). Finally, we log the details of the mission.

Writing such code using standard callbacks would result in a deeply nested sequence of callbacks. Identifying the exact sequence of steps wouldn’t be easy, and God forbid we decide to add in an extra step somewhere in the middle.

CATCHING ERRORS IN CHAINED PROMISES

When dealing with sequences of asynchronous steps, an error can occur in any step. We already know that we either can provide a second, error callback to the then call, or can chain in a catch call that takes an error callback. When we care about only the success/failure of the entire sequence of steps, supplying each step with special error handling might be tedious. So, as shown in listing 6.16, we can take advantage of the catch method that you saw earlier:

...catch(error => fail("An error has occurred:" + err));

If a failure occurs in any of the previous promises, the catch method catches it. If no error occurs, the program flow continues through it, unobstructed.

Dealing with a sequence of steps is much nicer with promises than with regular callbacks, wouldn’t you agree? But it’s still not as elegant as it could be. We’ll get to that soon, but first let’s see how to use promises to take care of parallel asynchronous steps.

6.3.6 Waiting for a number of promises

In addition to helping us deal with sequences of interdependent, asynchronous steps, promises significantly reduce the burden of waiting for several independent asynchronous tasks. Let’s revisit our example in which we want to, in parallel, gather information about the ninjas at our disposal, the intricacies of the plan, and the map of the location where the plan will be set in motion. With promises, this is as simple as shown in the following listing.

Listing 6.17

Waiting for a number of promises with Promise.all

As you can see, we don’t have to care about the order in which tasks are executed, and whether some of them have finished, while others didn’t. We state that we want to wait for a number of promises by using the built-in Promise.all method. This method takes in an array of promises and creates a new promise that successfully resolves when all passed-in promises resolve, and rejects if even one of the promises fails. The succeed callback receives an array of succeed values, one for each of the passed-in promises, in order. Take a minute to appreciate the elegance of code that processes multiple parallel asynchronous tasks with promises.

The Promise.all method waits for all promises in a list. But at times we have numerous promises, but we care only about the first one that succeeds (or fails). Meet the Promise.race method.

RACING PROMISES

Imagine that we have a group of ninjas at our disposal, and that we want to give an assignment to the first ninja who answers our call. When dealing with promises, we can write something like the following listing.

Listing 6.18

Racing promises with Promise.race

It’s simple as that. There’s no need for manually tracking everything. We use the Promise.race method to take an array of promises and return a completely new promise that resolves or rejects as soon as the first of the promises resolves or rejects.

So far you’ve seen how promises work, and how we can use them to greatly simplify dealing with a series of asynchronous steps, either in series or in parallel. Although

the improvements, when compared to plain old callbacks in terms of error handling and code elegance, are great, promisified code still isn’t on the same level of elegance as simple synchronous code. In the next section, the two big concepts that we’ve introduced in this chapter, generators and promises, come together to provide the simplicity of synchronous code with the nonblocking nature of asynchronous code.

6.4 Combining generators and promises

In this section, we’ll combine generators (and their capability to pause and resume their execution) with promises, in order to achieve more elegant asynchronous code. We’ll use the example of a functionality that enables users to get details of the highestrated mission done by the most popular ninja. The data representing the ninjas, the summaries of their missions, as well as the details of the missions are stored on a remote server, encoded in JSON.

All of these subtasks are long-running and mutually dependent. If we were to implement them in a synchronous fashion, we’d get the following straightforward code:

try { const ninjas = syncGetJSON("data/ninjas.json"); const missions = syncGetJSON(ninjas[0].missionsUrl); const missionDetails = syncGetJSON(missions[0].detailsUrl); //Study the mission description } catch(e){ //Oh no, we weren't able to get the mission details }

Although this code is great for its simplicity and error handling, it blocks the UI, which results in unhappy users. Ideally, we’d like to change this code so that no blocking occurs during a long-running task. One way of doing this is by combining generators and promises.

As we know, yielding from a generator suspends the execution of the generator without blocking. To wake up the generator and continue its execution, we have to call the next method on the generator’s iterator. Promises, on the other hand, allow us to specify a callback that will be triggered in case we were able to obtain the promised value, and a callback that will be triggered in case an error has occurred.

The idea, then, is to combine generators and promises in the following way: We put the code that uses asynchronous tasks in a generator, and we execute that generator function. When we reach a point in the generator execution that calls an asynchronous task, we create a promise that represents the value of that asynchronous task. Because we have no idea when that promise will be resolved (or even if it will be resolved), at this point of generator execution, we yield from the generator, so that we don’t cause blocking. After a while, when the promise gets settled, we continue the execution of our generator by calling the iterator’s next method. We do this as many times as necessary. See the following listing for a practical example.

The async function takes a generator, calls it, and creates an iterator that will be used to resume the generator execution. Inside the async function, we declare a handle function that handles one return value from the generator — one “iteration” of our iterator. If the generator result is a promise that gets resolved successfully, we use the iterator’s next method to send the promised value back to the generator and resume the generator’s execution. If an error occurs and the promise gets rejected, we throw that error to the generator by using the iterator’s throw method (told you it would come in handy). We keep doing this until the generator says it’s done.

This is a rough sketch, a minimum amount of code needed to combine generators and promises. We don’t recommend that you use this code in production.

NOTE

Now let’s take a closer look at the generator. On the first invocation of the iterator’s next method, the generator executes up to the first getJSON("data/ninjas.json")

call. This call creates a promise that will eventually contain the list of information about our ninjas. Because this value is fetched asynchronously, we have no idea how much time it will take the browser to get it. But we know one thing: We don’t want to block the application execution while we’re waiting. For this reason, at this moment of execution, the generator yields control, which pauses the generator, and returns the control flow to the invocation of the handle function. Because the yielded value is a getJSON promise, in the handle function, by using the then and catch methods of the promise, we register a success and an error callback, and continue execution. With this, the control flow leaves the execution of the handle function and the body of the async function, and continues after the call to the async function (in our case, there’s no more code after, so it idles). During this time, our generator function patiently waits suspended, without blocking the program execution.

Much, much later, when the browser receives a response (either a positive or a negative one), one of the promise callbacks is invoked. If the promise was resolved successfully, the success callback is invoked, which in turn causes the execution of the iterator’s next method, which asks the generator for another value. This brings back the generator from suspension and sends to it the value passed in by the callback. This means that we reenter the body of our generator, after the first yield expression, whose value becomes the ninjas list that was asynchronously fetched from the server. The execution of the generator function continues, and the value is assigned to the plan variable.

In the next line of the generator, we use some of the obtained data, ninjas[0] .missionUrl, to make another getJSON call that creates another promise that should eventually contain a list of missions done by the most popular ninja. Again, because this is an asynchronous task, we have no idea how long it’s going to take, so we again yield the execution and repeat the whole process.

This process is repeated as long as there are asynchronous tasks in the generator.

This was a tad on the complex side, but we like this example because it combines a lot of things that you’ve learned so far:

■ Functions as first-class objects — We send a function as an argument to the async function.

■ Generator functions — We use their ability to suspend and resume execution.

■ Promises — They help us deal with asynchronous code.

■ Callbacks — We register success and failure callbacks on our promises.

■ Arrow functions — Because of their simplicity, for callbacks we use arrow functions.

■ Closures — The iterator, through which we control the generator, is created in the async function, and we access it, through closures, in the promise callbacks.

Now that we’ve gone through the whole process, let’s take a minute to appreciate how much more elegant the code that implements our business logic is. Consider this:

Instead of mixed control-flow and error handling, and slightly confusing code, we end up with something like this:

async(function*() {

try { const ninjas = yield getJSON("data/ninjas.json"); const missions = yield getJSON(ninjas[0].missionsUrl);

//All information recieved

} catch(e) { //An error has occurred } });

This end result combines the advantages of synchronous and asynchronous code. From synchronous code, we have the ease of understanding, and the ability to use all standard control-flow and exception-handling mechanisms such as loops and try-catch statements. From asynchronous code, we get the nonblocking nature; the execution of our application isn’t blocked while waiting for long-running asynchronous tasks.

6.4.1 Looking forward — the async function Notice that we still had to write some boilerplate code; we had to develop an async function that takes care of handling promises and requesting values from the generator. Although we can write this function only once and then reuse it throughout our code, it would be even nicer if we didn’t have to think about it. The people in charge of JavaScript are well aware of the usefulness of the combination of generators and promises, and they want to make our lives even easier by building in direct language support for mixing generators and promises.

For these situations, the current plan is to include two new keywords, async and await, that would take care of this boilerplate code. Soon, we’ll be able to write something like this:

We use the async keyword in front of the function keyword to specify that this function relies on asynchronous values, and at every place where we call an asynchronous task, we place the await keyword that says to the JavaScript engine, please wait for this result without blocking. In the background, everything happens as we’ve discussed previously throughout the chapter, but now we don’t need to worry about it.

Async functions will appear in the next installment of JavaScript. Currently no browser supports it, but you can use transpilers such as Babel or Traceur if you wish to use async in your code today.

## 6.6 Exercises

After running the following code, what are the values of variables a1 to a4?




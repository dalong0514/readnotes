# 06 Functions for the future: generators and promises

This chapter covers: 1) Continuing function execution with generators. 2) Handling asynchronous tasks with promises. 3) Achieving elegant asynchronous code by combining generators and promises.

In the previous three chapters, we focused on functions, specifically on how to define functions and how to use them to great effect. Although we’ve introduced some ES6 features, such as arrow functions and block scopes, we’ve mostly been exploring features that have been part of JavaScript for quite some time. This chapter tackles the cutting edge of ES6 by presenting generators and promises, two completely new JavaScript features. Generators and promises are both introduced by ES6. You can check out current browser support at http://mng.bz/sOs4 and [[ECMAScript 6 compatibility table](http://kangax.github.io/compat-table/es6/#test-Promise)].

1『作者在 6.3.4 小结里讲解了如何用 promise 对象实现从后端请求数据，值得反复研究。』

Generators are a special type of function. Whereas a standard function produces at most a single value while running its code from start to finish, generators produce multiple values, on a per request basis, while suspending their execution between these requests. Although new in JavaScript, generators have existed for quite some time in Python, PHP, and C#.

Generators are often considered an almost weird or fringe language feature not often used by the average programmer. Though most of this chapter’s examples are designed to teach you how generator functions work, we’ll also explore some practical aspects of generators. You’ll see how to use generators to simplify convoluted loops and how to take advantage of generators’ capability to suspend and resume their execution, which can help you write simpler and more elegant asynchronous code.

Promises, on the other hand, are a new, built-in type of object that help you work with asynchronous code. A promise is a placeholder for a value that we don’t have yet but will at some later point. They’re especially good for working with multiple asynchronous steps.

In this chapter, you’ll see how both generators and promises work, and we’ll finish off by exploring how to combine them to greatly simplify our dealings with asynchronous code. But before going into the specifics, let’s take a sneak peek into how much more elegant our asynchronous code can be.

..............................................................

What are some common uses for a generator function? Why are promises better than simple callbacks for asyn-chronous code? Do you know?

You start a number of long-running tasks with Promise .race. When does the promise resolve? When would it fail to resolve?

..............................................................

## 6.1 Making our async code elegant with generators and promises





Imagine that you’re a developer working at freelanceninja.com, a popular freelance ninja recruitment site enabling customers to hire ninjas for stealth missions. Your task is to implement a functionality that lets users get details about the highest-rated mission done by the most popular ninja. The data representing the ninjas, the summaries of their missions, as well as the details of the missions are stored on a remote server, encoded in JSON. You might write something like this:

```js
try { var ninjas = syncGetJSON("ninjas.json"); var missions = syncGetJSON(ninjas[0].missionsUrl); var missionDetails = syncGetJSON(missions[0].detailsUrl); //Study the mission description } catch(e){ //Oh no, we weren't able to get the mission details }
```

This code is relatively easy to understand, and if an error occurs in any of the steps, we can easily catch it in the catch block. But unfortunately, this code has a big problem. Getting data from a server is a long-running operation, and because JavaScript relies on a single-threaded execution model, we’ve just blocked our UI until the long-running operations finish. This leads to unresponsive applications and disappointed users. To solve this problem, we can rewrite it with callbacks, which will be invoked when a task finishes, without blocking the UI:

getJSON("ninjas.json", function(err, ninjas){ if(err) { console.log("Error fetching list of ninjas", err); return; } getJSON(ninjas[0].missionsUrl, function(err, missions) { if(err) { console.log("Error locating ninja missions", err); return; } getJSON(missions[0].detailsUrl, function(err, missionDetails){ if(err) { console.log("Error locating mission details", err); return; } //Study the intel plan }); }); });

Although this code will be much better received by our users, you’ll probably agree that it’s messy, it adds a lot of boilerplate error-handling code, and it’s plain ugly. This is where generators and promises jump in. By combining them, we can turn the nonblocking but awkward callback code into something much more elegant:

```js
async(function*(){ try { const ninjas = yield getJSON("ninjas.json"); const missions = yield getJSON(ninjas[0].missionsUrl); const missionDescription = yield getJSON(missions[0].detailsUrl); //Study the mission details } catch(e) { //Oh no, we weren't able to get the mission details } });
```

A generator function is defined by putting an asterisk right after the function keyword. We can use the new yield keyword in generator functions.

The promises are hidden within the getJSON method.

Don’t worry if this example doesn’t make much sense or if you find some of the syntax (such as function* or yield) unfamiliar. By the end of this chapter, you’ll meet all the necessary ingredients. For now, it’s enough that you compare the elegance (or the lack thereof) of the nonblocking callback code and the nonblocking generators and promises code.

Let’s start slowly by exploring generator functions, the first stepping stone toward elegant asynchronous code.

6.2 Working with generator functions

Generators are a completely new type of function and are significantly different from standard, run-of-the-mill functions. A generator is a function that generates a sequence of values, but not all at once, as a standard function would, but on a per request basis. We have to explicitly ask the generator for a new value, and the generator will either respond with a value or notify us that it has no more values to produce. What’s even more curious is that after a value is produced, a generator function doesn’t end its execution, as a normal function would. Instead, a generator is merely suspended. Then, when a request for another value comes along, the generator resumes where it left off.

The following listing provides a simple example of using a generator to generate a sequence of weapons.

Listing 6.1

Using a generator function to generate a sequence of values



## 记忆时间

## 0601. Functions for the future: generators and promises

### Summary

1 Generators are functions that generate sequences of values—not all at once, but on a per request basis.

2 Unlike standard functions, generators can suspend and resume their execution. After a generator has generated a value, it suspends its execution without blocking the main thread and patiently waits for the next request.

3 A generator is declared by putting an asterisk (\*) after the function keyword. Within the body of the generator, we can use the new yield keyword that yields a value and suspends the execution of the generator. If we want to yield to another generator, we use the yield\* operator.

4 Calling a generator creates an iterator object through which we control the execution of the generator. We request new values from the generator by using the iterator’s next method, and we can even throw exceptions into the generator by calling the iterator’s throw method. In addition, the next method can be used to send in values to the generator.

5 A promise is a placeholder for the results of a computation; it’s a guarantee that eventually we’ll know the result of the computation, most often an asynchronous computation. A promise can either succeed or fail, and after it has done so, there will be no more changes.

6 Promises significantly simplify our dealings with asynchronous tasks. We can easily work with sequences of interdependent asynchronous steps by using the then method to chain promises. Parallel handling of multiple asynchronous steps is also greatly simplified; we use the Promise.all method.

7 We can combine generators and promises to deal with asynchronous tasks with the simplicity of synchronous code.

This chapter covers: 1) Continuing function execution with generators. 2) Handling asynchronous tasks with promises. 3) Achieving elegant asynchronous code by combining generators and promises.

In the previous three chapters, we focused on functions, specifically on how to define functions and how to use them to great effect. Although we’ve introduced some ES6 features, such as arrow functions and block scopes, we’ve mostly been exploring features that have been part of JavaScript for quite some time. This chapter tackles the cutting edge of ES6 by presenting generators and promises, two completely new JavaScript features. Generators and promises are both introduced by ES6. You can check out current browser support at http://mng.bz/sOs4 and [[ECMAScript 6 compatibility table](http://kangax.github.io/compat-table/es6/#test-Promise)].

1『作者在 6.3.4 小结里讲解了如何用 promise 对象实现从后端请求数据，值得反复研究。』

Generators are a special type of function. Whereas a standard function produces at most a single value while running its code from start to finish, generators produce multiple values, on a per request basis, while suspending their execution between these requests. Although new in JavaScript, generators have existed for quite some time in Python, PHP, and C#.

Generators are often considered an almost weird or fringe language feature not often used by the average programmer. Though most of this chapter’s examples are designed to teach you how generator functions work, we’ll also explore some practical aspects of generators. You’ll see how to use generators to simplify convoluted loops and how to take advantage of generators’ capability to suspend and resume their execution, which can help you write simpler and more elegant asynchronous code.

Promises, on the other hand, are a new, built-in type of object that help you work with asynchronous code. A promise is a placeholder for a value that we don’t have yet but will at some later point. They’re especially good for working with multiple asynchronous steps.

In this chapter, you’ll see how both generators and promises work, and we’ll finish off by exploring how to combine them to greatly simplify our dealings with asynchronous code. But before going into the specifics, let’s take a sneak peek into how much more elegant our asynchronous code can be.

What are some common uses for a generator function? Why are promises better than simple callbacks for asyn-chronous code? Do you know? You start a number of long-running tasks with Promise .race. When does the promise resolve? When would it fail to resolve?

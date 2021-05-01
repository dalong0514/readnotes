# Use function composition in JavaScript

[Use function composition in JavaScript | Codementor](https://www.codementor.io/@michelre/use-function-composition-in-javascript-gkmxos5mj)

Published Feb 11, 2018Last updated Aug 09, 2018

Prerequisite: I use currying in this post, so if you don't know about that, I encourage you to read my previous post: Currying in Javascript.

[Currying in JavaScript | Codementor](https://www.codementor.io/@michelre/currying-in-javascript-g6212s8qv)

## Conclusion

This is a trivial example here, but be aware that you can use it on more complicated ones. The compose function is implemented on the most functional library like lodash or ramda. You can even find variant on function composition. For example Ramda propose a composeP function that allows you to compose functions that return promises: [Ramda Documentation](https://ramdajs.com/docs/#composeP).

## 01. What is function composition?

Function composition is a mechanism of combining multiple simple functions to build a more complicated one. The result of each function is passed to the next one. In mathematics, we often write something like: f(g(x)). So this is the result of g(x) that is passed to f. In programing we can achieved the composition by writing something similar. Let's take a quick example. 

Suppose I need to make some arithmetic by doing the following operation: `2 + 3 * 5`. As you may know, the multiplication has the priority over the addition. So you start by calculating `3 * 5` and then when add 2 to the result. Let's write this in JavaScript. The primary and certainly the most simple approach could be:

```js
const add = (a, b) => a + b;
const mult = (a, b) => a * b;
add(2, mult(3, 5))
```

This is a form of function composition since this is the result of the multiplication that is passed to the add function. Let's go a step further and see another case where function composition can be very useful. Suppose now, that I have a list of users and I need to extract the name of all the adult users. I would personaly write something like:

```js
const users = [
  { name: "Jeff", age: 14 },
    { name: "Jack", age: 18 }, 
    { name: "Milady", age: 22 },
]
const filter = (cb, arr) => arr.filter(cb);
const map = (cb, arr) => arr.map(cb);

map(u => u.name, filter(u => u.age >= 18, users)); //["Jack", "Milady"]
```

It is good, but it could be better if we were able to automate the composition. At least it could be more readable.

## 02. Automate the function composition

So our goal in this section is to create a high order function that take two or more functions and compose them. So let's define our final signature of our future function:

```js
compose(function1, function2, ... , functionN): Function
```

So for example we'd want to call the function like this:

```js
compose(add1, add2)(3) //6
```

So the implementation of such a function could be:

```js
const compose = (...functions) => args => functions.reduceRight((arg, fn) => fn(arg), args);
```

Isn't that awesome? This only one line function allows you to compose any function to build complex transformation. Let me explain what happens here:

1 compose is a high order function. It is a function that returns another function.

2 compose takes multiple functions as arguments and we convert them into an array of functions using the spread opeartor: ...

3 Then we simply apply a reduceRight on those functions. The first parameter of the callback is the current argument. The second argument is the current function. Then we call each function with the current argument and the result is use for the next call.

Now we can use this function on our previous example. I volontarly currified the map and filter functions so it is more readable:

```js
const filter = cb => arr => arr.filter(cb);
const map = cb => arr => arr.map(cb);

compose(
  map(u => u.name),
  filter(u => u.age >= 18)
)(users) //["Jack", "Milady"]
```

I propose to you a last example. Let's implement the traditional MapReduce.

## 03. MapReduce with function composition

The principle of MapReduce is simple. It is just applying a map on a set of data and reduce the result to produce a single result. This is typically the principle of function composition. So for example, we can implement the traditionnal word counter to count a number of words for example. The map will be responsible for just sending 1 when it encounters a value and the reduce will sum up the final array to produce the result:

```js
const reduce = cb => arr => arr.reduce(cb); //Just currify the reduce function

const mapWords = map(() => 1);
const reduceWords = reduce((acc, curr) => acc += curr)(0)

compose(reduceWords, mapWords)(['foo', 'bar', 'baz']); //3
```

## 04. Pipe or composition?

I addded this part since Yeiber Cano mentionned that I first implemented pipe instead of compose. You can read his comment just below this article. So the main difference between compose and pipe is the order of the composition. Compose performs a right-to-left function composition since Pipe performs a left-to-right composition. So let's write the pipe high-order function:

```js
const pipe = (...functions) => args => functions.reduce((arg, fn) => fn(arg), args);
```

So in this case, we use reduce instead of reduceRight to perform the composition from left to right. We can then apply our newly created function to our previous examples:

```js
pipe(
  filter(u => u.age >= 18),
  map(u => u.name),
)(users) //["Jack", "Milady"]

pipe(mapWords, reduceWords)(['foo', 'bar', 'baz']);
```

Some people prefer using pipe over compose because they find it more readable. At least, we can all agree that it is more natural!

2-3『

评论区里竟然还能发掘出一本书，直觉上是个宝藏。已下载书籍「2021075Category-Theory-for-Programmers」。

[hmemcpy/milewski-ctfp-pdf: Bartosz Milewski's 'Category Theory for Programmers' unofficial PDF and LaTeX source](https://github.com/hmemcpy/milewski-ctfp-pdf)

』
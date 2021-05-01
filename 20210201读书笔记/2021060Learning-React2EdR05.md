## 记忆时间

## 目录

附件0301-01Currying-in-JavaScript.md

附件0301-02Use-function-composition-in-JavaScript.md

## 附件0301-01Currying-in-JavaScript.md

[Currying in JavaScript | Codementor](https://www.codementor.io/@michelre/currying-in-javascript-g6212s8qv)

Published Jan 28, 2018Last updated Jul 26, 2018

Currying is an important concept that is at the heart of any functional programing language. So let's have a look at what it is and why to use it.

### Conclusion

Currying is an important part of a functional programing. I encourage you to play with it like I did in this article. If you use functional libraries like Ramda or Lodash/fp the most of functions are curryfied by default, which is great! So remember that decomposing functions of n arguments to n functions of 1 argument is not a really hard task with the ES6 syntax and the lamda functions! So you have no excuse not to create reusable code thanks to currying!

1-2-3『

在想啊，lisp、autolisp 里能不能实现 curry 函数化。（2021-05-01）

[ARNESI](https://common-lisp.net/project/bese/docs/arnesi/html/Higher_0020order_0020functions.html#function_005FIT.BESE.ARNESI_003A_003ACURRY)

[Function CURRY](https://common-lisp.net/project/bese/docs/arnesi/html/api/function_005FIT.BESE.ARNESI_003A_003ACURRY.html)

Returns a function which will call FUNCTION passing it INITIAL-ARGS and then any other args. 

```
(funcall (curry #'list 1) 2) ==> (list 1 2)
```

```
(defun curry (function &rest initial-args)
  "Returns a function which will call FUNCTION passing it
  INITIAL-ARGS and then any other args.

 (funcall (curry #'list 1) 2) ==> (list 1 2)"
  (lambda (&rest args)
    (apply function (append initial-args args))))
```

[clojure - Is it possible to implement auto-currying to the Lisp-family languages? - Stack Overflow](https://stackoverflow.com/questions/11218905/is-it-possible-to-implement-auto-currying-to-the-lisp-family-languages)

[Why LISPs have no auto-currying](https://en.paqmind.com/blog/currying-in-lisp)

』—— 未完成

### 01. What is currying?

Currying is the mean to transform a function of arity n to n functions of arity 1. So, this is the theory. It simply means that currying allows you to not specify all arguments when you call a function. Let's take a simple example. You should be used to do something like this:

```js
const add = (a, b) => a + b

add(1, 2) //should return 3
```

In a curryfied way, I should do something like this instead:

```js
const add = a => b => a + b

add(1)(2) //should return 3
```

1『注意哦，curry 函数的调用是 2 个括号连着的。（2021-05-01）』

Did you notice how the add function is built? It is a function that takes one argument and return another function that takes the second argument. Once all the arguments are there, the computation happens. So in this example, calling add(1) returns a function.

Currying is possible in JavaScript because functions are first-class citizen. It means that functions are like any other values. They can be assigned to variables, passed as argument to other functions and returned by functions.

### 02. Why currying is important

Currying gives you the opportunity to partially configure a function and then, it is the mean to create reusable functions. Let's take another example. Suppose I have a collection like this:

```js
const movies = [
  {
    "id": 1,
    "name": "Matrix"
  },
  {
    "id": 2,
    "name": "Star Wars"
  },
  {
    "id": 3,
    "name": "The wolf of Wall Street"
  }
]
```

Now, suppose I want to extract the ids of this collection. I could simply use the map function to iterate over the collection:

```js
movies.map((movie) => movie.id) //should return [ 1, 2, 3 ]
```

Great, but suppose I have a second collection of series:

```js
const series = [
  {
    "id": 4,
    "name": "South Park"
  },
  {
    "id": 5,
    "name": "The Simpsons"
  },
  {
    "id": 6,
    "name": "The Big Bang Theory"
  }
]
```

And suppose I want to extract the ids as I did before with the movies:

```js
series.map((serie) => serie.id) //should return [ 4, 5, 6 ]
```

The callbacks of map are strictly the same, but we operated on two different collections. In this case, currying can be the solution. Let's make a function call get that should extract a property from an object:

```js
const get = property => object => object[property];
```

Now from this function I can create another function, called getId that is just a partial configuration of the get function:

```js
const getId = get('id');
```

At this step, getId is still a function and this is great because we are now able to use it inside our map calls:

```js
movies.map(getId); //should return [ 1, 2, 3 ]
series.map(getId); //should return [ 4, 5, 6 ]
```

Isn't that nice? But we can go one step further. Suppose now, that we want to extract the name from our objects. How can you could achieve that? Just create a function called getName derived from the get function:

```js
const getName = get('name');
```

And then, you can use it on your collections to extract the name:

```js
movies.map(getName); //should return [ 'Matrix', 'Star Wars', 'The wolf of Wall Street' ]
```

## 附件0301-02Use-function-composition-in-JavaScript.md

[Use function composition in JavaScript | Codementor](https://www.codementor.io/@michelre/use-function-composition-in-javascript-gkmxos5mj)

Published Feb 11, 2018Last updated Aug 09, 2018

Prerequisite: I use currying in this post, so if you don't know about that, I encourage you to read my previous post: Currying in Javascript.

[Currying in JavaScript | Codementor](https://www.codementor.io/@michelre/currying-in-javascript-g6212s8qv)

### Conclusion

This is a trivial example here, but be aware that you can use it on more complicated ones. The compose function is implemented on the most functional library like lodash or ramda. You can even find variant on function composition. For example Ramda propose a composeP function that allows you to compose functions that return promises: [Ramda Documentation](https://ramdajs.com/docs/#composeP).

### 01. What is function composition?

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

### 02. Automate the function composition

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

### 03. MapReduce with function composition

The principle of MapReduce is simple. It is just applying a map on a set of data and reduce the result to produce a single result. This is typically the principle of function composition. So for example, we can implement the traditionnal word counter to count a number of words for example. The map will be responsible for just sending 1 when it encounters a value and the reduce will sum up the final array to produce the result:

```js
const reduce = cb => arr => arr.reduce(cb); //Just currify the reduce function

const mapWords = map(() => 1);
const reduceWords = reduce((acc, curr) => acc += curr)(0)

compose(reduceWords, mapWords)(['foo', 'bar', 'baz']); //3
```

### 04. Pipe or composition?

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
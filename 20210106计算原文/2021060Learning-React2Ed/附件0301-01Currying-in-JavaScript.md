# Currying in JavaScript

[Currying in JavaScript | Codementor](https://www.codementor.io/@michelre/currying-in-javascript-g6212s8qv)

Published Jan 28, 2018Last updated Jul 26, 2018

Currying is an important concept that is at the heart of any functional programing language. So let's have a look at what it is and why to use it.

## Conclusion

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

## 01. What is currying?

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

## 02. Why currying is important

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
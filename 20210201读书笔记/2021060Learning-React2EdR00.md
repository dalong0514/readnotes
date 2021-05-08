## 记忆时间

整体的感觉，作者的文笔和技术水平都很好，本书读起来很舒服。（2021-05-01）

## 卡片

### 0101. 主题卡 —— npm 和 yarn 包管理

信息源自「2021060Learning-React0101.md」

用 npm 安装 yarn。

```
npm install -g yarn
```

1、初始化项目。

If you're starting your own project from scratch and want to include dependencies, simply run the command:

```
npm init -y
```

2、安装、卸载依赖包。

 To install a package with npm, you'll run:

```
npm install package-name
```

To remove a package with npm, you'll run:

```
npm remove package-name
```

To install a specific package with yarn, run:

```
yarn add package-name
```

To remove a dependency, the command is familiar, too:

```
yarn remove package-name
```

Yarn is used in production by Facebook and is included in projects like React, React Native, and Create React App. If you ever find a project that contains a yarn.lock file, the project uses yarn. Similar to the npm install command, you can install all the dependencies of the project by typing yarn.

1-2『 npm 和 yarn 包管理，常用命令做一张主题卡片。（2021-04-29）』—— 已完成

3、全部重新安装依赖包。

```
npm install
```

```
yarn
```

### 0102. 主题卡 —— 解构对象

信息源自「2021060Learning-React0201.md」

Destructuring assignment allows you to locally scope fields within an object and to declare which values will be used. Consider the sandwich object. It has four keys, but we only want to use the values of two. We can scope bread and meat to be used locally:

```js
const sandwich = {
  bread: "dutch crunch",
  meat: "tuna",
  cheese: "swiss",
  toppings: ["lettuce", "tomato", "mustard"]
};
  
const { bread, meat } = sandwich;
console.log(bread, meat); // dutch crunch tuna
```

1『又见解构赋值了，真香，哈哈。（2021-04-29）』

The code pulls bread and meat out of the object and creates local variables for them. Also, since we declared these destructed variables using let, the bread and meat variables can be changed without changing the original sandwich:

```js
const sandwich = {
  bread: "dutch crunch",
  meat: "tuna",
  cheese: "swiss",
  toppings: ["lettuce", "tomato", "mustard"]
};
  
let { bread, meat } = sandwich;
bread = "garlic";
meat = "turkey";
console.log(bread); // garlic
console.log(meat); // turkey
console.log(sandwich.bread, sandwich.meat); // dutch crunch tuna 
```

We can also destructure incoming function arguments. Consider this function that would log a person's name as a lord:

```js
const lordify = regularPerson => {
  console.log(`${regularPerson.firstname} of Canterbury`);
};
  
const regularPerson = {
  firstname: "Bill",
  lastname: "Wilson"
};

lordify(regularPerson); // Bill of Canterbury
```

Instead of using dot notation syntax to dig into objects, we can destructure the values we need out of regularPerson:

```js
const lordify = ({ firstname }) => {
  console.log(`${firstname} of Canterbury`);
};
  
const regularPerson = {
  firstname: "Bill",
  lastname: "Wilson"
};

lordify(regularPerson); // Bill of Canterbury
```

Let's take this one level farther to reflect a data change. Now, the regularPerson object has a new nested object on the spouse key: 

```js
const regularPerson = {
  firstname: "Bill",
  lastname: "Wilson",
  spouse: {
    firstname: "Phil",
    lastname: "Wilson"
  }
};
```

If we wanted to lordify the spouse's first name, we'd adjust the function's destructured arguments slightly:

```js
const lordify = ({ spouse: { firstname } }) => {
  console.log(`${firstname} of Canterbury`);
};
  
lordify(regularPerson); // Phil of Canterbury
```

Using the colon and nested curly braces, we can destructure the firstname from the spouse object.

2『解构对象，做一张主题卡片。（2021-04-29）』—— 已完成

### 0103. 主题卡 —— 解构数组

信息源自「2021060Learning-React0201.md」

Values can also be destructured from arrays. Imagine that we wanted to assign the first value of an array to a variable name:

```js
const [firstAnimal] = ["Horse", "Mouse", "Cat"]; 
console.log(firstAnimal); // Horse
```

We can also pass over unnecessary values with list matching using commas. List matching occurs when commas take the place of elements that should be skipped. With the same array, we can access the last value by replacing the first two values with commas: 

```js
const [, , thirdAnimal] = ["Horse", "Mouse", "Cat"];
console.log(thirdAnimal); // Cat
```

Later in this section, we'll take this example a step farther by combining array destructuring and the spread operator.

2『解构数组，做一张主题卡片。（2021-04-29）』—— 已完成

### 0104. 主题卡 —— 对象强化

信息源自「2021060Learning-React0201.md」

Object literal enhancement is the opposite of destructuring. It's the process of restructuring or putting the object back together. With object literal enhancement, we can grab variables from the global scope and add them to an object:

```js
const name = "Tallac";
const elevation = 9738;
const funHike = { name, elevation };
console.log(funHike); // {name: "Tallac", elevation: 9738}
```

name and elevation are now keys of the funHike object. We can also create object methods with object literal enhancement or restructuring:

```js
const name = "Tallac";
const elevation = 9738;
const print = function() {
  console.log(`Mt. ${this.name} is ${this.elevation} feet tall`);
};
const funHike = { name, elevation, print };
funHike.print(); // Mt. Tallac is 9738 feet tall 
```

Notice we use this to access the object keys. When defining object methods, it's no longer necessary to use the function keyword:

```js
// Old
var skier = {
  name: name,
  sound: sound,
  powderYell: function() {
    var yell = this.sound.toUpperCase();
    console.log(`${yell} ${yell} ${yell}!!!`);
  },
  speed: function(mph) {
    this.speed = mph;
    console.log("speed:", mph);
  }
};
  
// New
const skier = {
  name,
  sound,
  powderYell() {
    let yell = this.sound.toUpperCase();
    console.log(`${yell} ${yell} ${yell}!!!`);
  },
  speed(mph) {
    this.speed = mph;
    console.log("speed:", mph);
  }
};
```

Object literal enhancement allows us to pull global variables into objects and reduces typing by making the function keyword unnecessary.

2『对象强化，做一张主题卡片。（2021-04-29）』—— 已完成

### 0105. 主题卡 —— spread operator

扩展符号的用途汇总：1）组合数据。2）复制一个数组。`[...array]` 表示基于 array 数组 copy 了一个新数组，这个可以实现「数据的不变性」。3）`const [first, ...others] = lakes`，截取除了首位元素的剩余数组部分，跟 Lisp 里的 `cdr` 函数功能相同。4）作为函数的「形参列表」。5）对「对象」的操作雷同对「数组」的操作。（2021-05-03）

信息源自「2021060Learning-React0201.md」

The spread operator is three dots (...) that perform several different tasks. First, the spread operator allows us to combine the contents of arrays. For example, if we had two arrays, we could make a third array that combines the two arrays into one:

```js
const peaks = ["Tallac", "Ralston", "Rose"]; 
const canyons = ["Ward", "Blackwood"]; 
const tahoe = [...peaks, ...canyons];

console.log(tahoe.join(", ")); // Tallac, Ralston, Rose, Ward, Blackwood 
```

All of the items from peaks and canyons are pushed into a new array called tahoe.

Let's take a look at how the spread operator can help us deal with a problem. Using the peaks array from the previous sample, let's imagine that we wanted to grab the last item from the array rather than the first. We could use the Array.reverse method to reverse the array in combination with array destructuring:

```js
const peaks = ["Tallac", "Ralston", "Rose"]; 
const [last] = peaks.reverse();
console.log(last); // Rose
console.log(peaks.join(", ")); // Rose, Ralston, Tallac 
```

See what happened? The reverse function has actually altered or mutated the array. In a world with the spread operator, we don't have to mutate the original array. Instead, we can create a copy of the array and then reverse it:

```js
const peaks = ["Tallac", "Ralston", "Rose"]; 
const [last] = [...peaks].reverse();
console.log(last); // Rose
console.log(peaks.join(", ")); // Tallac, Ralston, Rose 
```

1『大赞，Spread Operator 是实现「函数式编程范式」中数据不变性的一种手段。（2021-04-29）』

Since we used the spread operator to copy the array, the peaks array is still intact and can be used later in its original form. The spread operator can also be used to get the remaining items in the array:

```js
const lakes = ["Donner", "Marlette", "Fallen Leaf", "Cascade"]; 
const [first, ...others] = lakes;
console.log(others.join(", ")); // Marlette, Fallen Leaf, Cascade 
```

We can also use the three-dot syntax to collect function arguments as an array. When used in a function, these are called rest parameters. Here, we build a function that takes in n number of arguments using the spread operator, then uses those arguments to print some console messages:

```js
function directions(...args) {
  let [start, ...remaining] = args;
  let [finish, ...stops] = remaining.reverse();
  console.log(`drive through ${args.length} towns`);
  console.log(`start in ${start}`);
  console.log(`the destination is ${finish}`);
  console.log(`stopping ${stops.length} times in between`);
}
  
directions("Truckee", "Tahoe City", "Sunnyside", "Homewood", "Tahoma"); 
```

The directions function takes in the arguments using the spread operator. The first argument is assigned to the start variable. The last argument is assigned to a finish variable using `Array.reverse`. We then use the length of the arguments array to display how many towns we're going through. The number of stops is the length of the arguments array minus the finish stop. This provides incredible flexibility because we could use the directions function to handle any number of stops.

The spread operator can also be used for objects (see the GitHub page for Rest/Spread Properties). Using the spread operator with objects is similar to using it with arrays. In this example, we'll use it the same way we combined two arrays into a third array, but instead of arrays, we'll use objects:

3『 [tc39/proposal-object-rest-spread: Rest/Spread Properties for ECMAScript](https://github.com/tc39/proposal-object-rest-spread) 』

```js
const morning = {
  breakfast: "oatmeal",
  lunch: "peanut butter and jelly"
};
  
const dinner = "mac and cheese";
const backpackingMeals = {
  ...morning,
  dinner
};
  
console.log(backpackingMeals);
  
// {
// breakfast: "oatmeal",
// lunch: "peanut butter and jelly",
// dinner: "mac and cheese"
// }
```

2『spread operator，做一张主题卡片。（2021-04-29）』—— 已完成

### 0106. 主题卡 —— 函数式编程范式的 5 大核心特征

信息源自「2021060Learning-React0301.md」

Now that you've been introduced to functional programming and what it means to be 'functional' or 'declarative', we'll move on to introducing the core concepts of functional programming: immutability, purity, data transformation, higher-order functions, and recursion.

2『函数式编程范式的 5 大核心特征，做一张主题卡片。（2021-05-01）』—— 已完成

1 immutability.

To understand how immutability works, let's take a look at what it means to mutate data. Consider an object that represents the color lawn:

```js
let color_lawn = {
  title: "lawn",
  color: "#00FF00",
  rating: 0 
};

```

We could build a function that would rate colors and use that function to change the rating of the color object:

```js
function rateColor(color, rating) {
  color.rating = rating;
  return color;
}
  
console.log(rateColor(color_lawn, 5).rating); // 5
console.log(color_lawn.rating); // 5
```

In JavaScript, function arguments are references to the actual data. Setting the color's rating like this changes or mutates the original color object. (Imagine if you tasked a business with redacting and sharing your birth certificate and they returned your original birth certificate with black marker covering the important details. You'd hope that a business would have the common sense to make a copy of your birth certificate and return the original unharmed.) We can rewrite the rateColor function so that it does not harm the original goods (the color object):

```js
const rateColor = function(color, rating) {
  return Object.assign({}, color, { rating: rating });
};
  
console.log(rateColor(color_lawn, 5).rating); // 5
console.log(color_lawn.rating); // 0
```

1『又看到了老朋友 `Object.assign()`，用的频率超级高。（2021-05-01）』

Here, we used Object.assign to change the color rating. Object.assign is the copy machine. It takes a blank object, copies the color to that object, and overwrites the rating on the copy. Now we can have a newly rated color object without having to change the original.

We can write the same function using an arrow function along with the object spread operator. This rateColor function uses the spread operator to copy the color into a new object and then overwrite its rating:

```js
const rateColor = (color, rating) => ({
  ...color,
  rating
});
```

1『上面的写法真简洁优雅，牢记。（2021-05-01）』

This version of the rateColor function is exactly the same as the previous one. It treats color as an immutable object, does so with less syntax, and looks a little bit cleaner. Notice that we wrap the returned object in parentheses. With arrow functions, this is a required step since the arrow can't just point to an object's curly braces.

Let's consider an array of color names:

```js
let list = [{ title: "Rad Red" }, { title: "Lawn" }, { title: "Party Pink" }];
```

We could create a function that will add colors to that array using Array.push:

```js
const addColor = function(title, colors) {
  colors.push({ title: title });
  return colors;
};
  
console.log(addColor("Glam Green", list).length); // 4
console.log(list.length); // 4
```

However, Array.push is not an immutable function. This addColor function changes the original array by adding another field to it. In order to keep the colors array immutable, we must use Array.concat instead:

```js
const addColor = (title, array) => array.concat({ title }); 
console.log(addColor("Glam Green", list).length); // 4
console.log(list.length); // 3
```

Array.concat concatenates arrays. In this case, it takes a new object with a new color title and adds it to a copy of the original array.

You can also use the spread operator to concatenate arrays in the same way it can be used to copy objects. Here's the emerging JavaScript equivalent of the previous addColor function:

```js
const addColor = (title, list) => [...list, { title }]; 
```

This function copies the original list to a new array and then adds a new object containing the color's title to that copy. It is immutable.

2 Pure Functions.

A pure function is a function that returns a value that's computed based on its arguments. Pure functions take at least one argument and always return a value or another function. They do not cause side effects, set global variables, or change anything about application state. They treat their arguments as immutable data. In order to understand pure functions, let's first take a look at an impure function:

```js
const frederick = {
  name: "Frederick Douglass",
  canRead: false,
  canWrite: false
};
  
function selfEducate() {
  frederick.canRead = true;
  frederick.canWrite = true;
  return frederick;
}

selfEducate();
console.log(frederick);
// {name: "Frederick Douglass", canRead: true, canWrite: true}
```

The selfEducate function is not a pure function. It does not take any arguments, and it does not return a value or a function. It also changes a variable outside of its scope: Frederick. Once the selfEducate function is invoked, something about the「world」has changed. It causes side effects:

```js
const frederick = {
  name: "Frederick Douglass",
  canRead: false,
  canWrite: false
};
  
const selfEducate = person => {
  person.canRead = true;
  person.canWrite = true;
  return person;
};

console.log(selfEducate(frederick));
console.log(frederick);
// {name: "Frederick Douglass", canRead: true, canWrite: true}
// {name: "Frederick Douglass", canRead: true, canWrite: true}
```

PURE FUNCTIONS ARE TESTABLE

Pure functions are naturally testable. They do not change anything about their environment or「world,」and therefore do not require a complicated test setup or teardown. Everything a pure function needs to operate it accesses via arguments.

When testing a pure function, you control the arguments, and thus you can estimate the outcome. This selfEducate function is also impure: it causes side effects. Invoking this function mutates the objects that are sent to it. If we could treat the arguments sent to this function as immutable data, then we would have a pure function.

Let's have this function take an argument:

```js
const frederick = {
  name: "Frederick Douglass",
  canRead: false,
  canWrite: false
};

const selfEducate = person => ({
  ...person,
  canRead: true,
  canWrite: true
});

console.log(selfEducate(frederick));
console.log(frederick);
// {name: "Frederick Douglass", canRead: true, canWrite: true}
// {name: "Frederick Douglass", canRead: false, canWrite: false}
```

Finally, this version of selfEducate is a pure function. It computes a value based on the argument that was sent to it: the person. It returns a new person object without mutating the argument sent to it and therefore has no side effects.

Now let's examine an impure function that mutates the DOM: 

```js
function Header(text) {
  let h1 = document.createElement("h1");
  h1.innerText = text;
  document.body.appendChild(h1);
}

Header("Header() caused side effects");
```

The Header function creates a heading — one element with specific text — and adds it to the DOM. This function is impure. It does not return a function or a value, and it causes side effects: a changed DOM.

In React, the UI is expressed with pure functions. In the following sample, Header is a pure function that can be used to create h1 elements just like in the previous example. However, this function on its own does not cause side effects because it does not mutate the DOM. This function will create an h1 element, and it's up to some other part of the application to use that element to change the DOM: 

```js
const Header = props => <h1>{props.title}</h1>; 
```

Pure functions are another core concept of functional programming.

They will make your life much easier because they will not affect your application's state. When writing functions, try to follow these three rules:

1 The function should take in at least one argument.

2 The function should return a value or another function.

3 The function should not change or mutate any of its arguments.

1-3『纯函数核心的三样东西，这节的信息比郑烨专栏里讲纯函数要细致丰富很多，反复去看。（2021-05-01）』

3 Data Transformations.

How does anything change in an application if the data is immutable? Functional programming is all about transforming data from one form to another. We'll produce transformed copies using functions. These functions make our code less imperative and thus reduce complexity.

You do not need a special framework to understand how to produce one dataset that is based upon another. JavaScript already has the necessary tools for this task built into the language. There are two core functions that you must master in order to be proficient with functional JavaScript: Array.map and Array.reduce.

In this section, we'll take a look at how these and some other core functions transform data from one type to another.

Consider this array of high schools:

```js
const schools = ["Yorktown", "Washington & Liberty", "Wakefield"]; 
```

We can get a comma-delimited list of these and some other strings by using the Array.join function:

```js
console.log(schools.join(", "));
// "Yorktown, Washington & Liberty, Wakefield"
```

Array.join is a built-in JavaScript array method that we can use to extract a delimited string from our array. The original array is still intact; join simply provides a different take on it. The details of how this string is produced are abstracted away from the programmer.

If we wanted to create a function that creates a new array of the schools that begin with the letter "W", we could use the Array.filter method:

```js
const wSchools = schools.filter(school => school[0] === "W"); 
console.log(wSchools);
// ["Washington & Liberty", "Wakefield"]
```

Array.filter is a built-in JavaScript function that produces a new array from a source array. This function takes a predicate as its only argument. A predicate is a function that always returns a Boolean value: true or false. Array.filter invokes this predicate once for every item in the array. That item is passed to the predicate as an argument, and the return value is used to decide if that item will be added to the new array. In this case, Array.filter is checking every school to see if its name begins with a "W".

When it's time to remove an item from an array, we should use Array.filter over Array.pop or Array.splice because Array.filter is immutable. In this next sample, the cutSchool function returns new arrays that filter out specific school names:

```js
const cutSchool = (cut, list) => list.filter(school => school !== cut); 
console.log(cutSchool("Washington & Liberty", schools).join(", "));
// "Yorktown, Wakefield"
console.log(schools.join("\n"));
// Yorktown
// Washington & Liberty
// Wakefield
```

In this case, the cutSchool function is used to return a new array that does not contain "Washington & Liberty". Then, the join function is used with this new array to create a string out of the remaining two school names. cutSchool is a pure function. It takes a list of schools and the name of the school that should be removed and returns a new array without that specific school.

Another array function that is essential to functional programming is Array.map. Instead of a predicate, the Array.map method takes a function as its argument. This function will be invoked once for every item in the array, and whatever it returns will be added to the new array:

```js
const highSchools = schools.map(school => `${school} High School`); 
console.log(highSchools.join("\n"));
// Yorktown High School
// Washington & Liberty High School
// Wakefield High School
console.log(schools.join("\n"));
// Yorktown
// Washington & Liberty
// Wakefield
```

In this case, the map function was used to append "High School" to each school name. The schools array is still intact.

In the last example, we produced an array of strings from an array of strings. The map function can produce an array of objects, values, arrays, other functions — any JavaScript type. Here's an example of the map function returning an object for every school:

```js
const highSchools = schools.map(school => ({ name: school })); 
console.log(highSchools);
// [
// { name: "Yorktown" },
// { name: "Washington & Liberty" },
// { name: "Wakefield" }
// ]
```

1-3『看到这里再一次认识到，JS 里的 map 函数，等同于 lisp 里的 mapcar 函数。（2021-05-01）』

An array containing objects was produced from an array that contains strings. If you need to create a pure function that changes one object in an array of objects, map can be used for this, too. In the following example, we'll change the school with the name of "Stratford" to "HB Woodlawn" without mutating the schools array:

```js
let schools = [
  { name: "Yorktown" },
  { name: "Stratford" },
  { name: "Washington & Liberty" },
  { name: "Wakefield" }
];

let updatedSchools = editName("Stratford", "HB Woodlawn", schools);
console.log(updatedSchools[1]); // { name: "HB Woodlawn" }
console.log(schools[1]); // { name: "Stratford" }
```

The schools array is an array of objects. The updatedSchools variable calls the editName function and we send it the school we want to update, the new school, and the schools array. This changes the new array but makes no edits to the original:

```js
const editName = (oldName, name, arr) => arr.map(item => {
  if (item.name === oldName) {
    return {
      ...item,
      name
    };
  } else {
    return item;
  }
});
```

Within editName, the map function is used to create a new array of objects based upon the original array. The editName function can be written entirely in one line. Here's an example of the same function using a shorthand if/else statement:

```js
const editName = (oldName, name, arr) =>
  arr.map(item => (item.name === oldName ? { ...item, name } : item)); 
```

1-3『又一次感叹，上面的实现多么的简洁，越发觉得本书是「2019030Refactoring2Ed」很好的补充资料。（2021-05-01）』

If you need to transform an array into an object, you can use Array.map in conjunction with Object.keys. Object.keys is a method that can be used to return an array of keys from an object. Let's say we needed to transform the schools object into an array of schools:

```js
const schools = {
  Yorktown: 10,
  "Washington & Liberty": 2,
  Wakefield: 5
};

const schoolArray = Object.keys(schools).map(key => ({
  name: key,
  wins: schools[key]
}));

console.log(schoolArray);
// [
// {
// name: "Yorktown",
// wins: 10
// },
// {
// name: "Washington & Liberty",
// wins: 2
// },
// {
// name: "Wakefield",
// wins: 5
// }
// ]
```

In this example, Object.keys returns an array of school names, and we can use map on that array to produce a new array of the same length. The name of the new object will be set using the key, and wins is set equal to the value.

1『赞，Object.keys 只是产生了对象的「索引」的数组，只是用 map 对这个索引数组进行处理，通过每个索引去读取 schools 对象里的「值」从而构成一个新的数组。（2021-05-01）』

So far, we've learned that we can transform arrays with Array.map and Array.filter. We've also learned that we can change arrays into objects by combining Object.keys with Array.map. The final tool that we need in our functional arsenal is the ability to transform arrays into primitives and other objects.

The reduce and reduceRight functions can be used to transform an array into any value, including a number, string, boolean, object, or even a function. Let's say we need to find the maximum number in an array of numbers. We need to transform an array into a number; therefore, we can use reduce:

```js
const ages = [21, 18, 42, 40, 64, 63, 34];

const maxAge = ages.reduce((max, age) => {
  console.log(`${age} > ${max} = ${age > max}`);
  if (age > max) {
    return age;
  } else {
    return max;
  }
}, 0);

console.log("maxAge", maxAge);
// 21 > 0 = true
// 18 > 21 = false
// 42 > 21 = true
// 40 > 42 = false
// 64 > 42 = true
// 63 > 64 = false
// 34 > 64 = false
// maxAge 64
```

The ages array has been reduced into a single value: the maximum age, 64. reduce takes two arguments: a callback function and an original value. In this case, the original value is 0, which sets the initial maximum value to 0. The callback is invoked once for every item in the array. The first time this callback is invoked, age is equal to 21, the first value in the array, and max is equal to 0, the initial value. The callback returns the greater of the two numbers, 21, and that becomes the max value during the next iteration. Each iteration compares each age against the max value and returns the greater of the two. Finally, the last number in the array is compared and returned from the previous callback.

If we remove the console.log statement from the preceding function and use a shorthand if/else statement, we can calculate the max value in any array of numbers with the following syntax:

```js
const max = ages.reduce((max, value) => (value > max ? value : max), 0); 
```

ARRAY.REDUCERIGHT

Array.reduceRight works the same way as Array.reduce; the difference is that it starts reducing from the end of the array rather than the beginning. 

Sometimes we need to transform an array into an object. The following example uses reduce to transform an array that contains colors into a hash:

```js
const colors = [
  {
    id: "xekare",
    title: "rad red",
    rating: 3
  },
  {
    id: "jbwsof",
    title: "big blue",
    rating: 2
  },
  {
    id: "prigbj",
    title: "grizzly grey",
    rating: 5
  },
  {
    id: "ryhbhsl",
    title: "banana",
    rating: 1
  }
];
  
const hashColors = colors.reduce((hash, { id, title, rating }) => {
  hash[id] = { title, rating };
  return hash;
}, {});

console.log(hashColors);
// {
// "xekare": {
// title:"rad red",
// rating:3
// },
// "jbwsof": {
// title:"big blue",
// rating:2
// },
// "prigbj": {
// title:"grizzly grey",
// rating:5
// },
// "ryhbhsl": {
// title:"banana",
// rating:1
// }
// }
```

In this example, the second argument sent to the reduce function is an empty object. This is our initial value for the hash. During each iteration, the callback function adds a new key to the hash using bracket notation and sets the value for that key to the id field of the array. Array.reduce can be used in this way to reduce an array to a single value — in this case, an object.

1-2『数组转变为一个「大」json 对象，这个实现逻辑很值得借鉴，思想可以用，这个功能直觉上 JS 应该有内置的 json 功能函数可以直接实现。（2021-04-30）』

We can even transform arrays into completely different arrays using reduce. Consider reducing an array with multiple instances of the same value to an array of unique values. The reduce method can be used to accomplish this task:

```js
const colors = ["red", "red", "green", "blue", "green"]; 
const uniqueColors = colors.reduce((unique, color) =>
  unique.indexOf(color) !== -1 ? unique : [...unique, color],
  []
);

console.log(uniqueColors);
// ["red", "green", "blue"]
```

2『又获得了一个数组去重的实现，做一张任意卡片。（2021-05-01）』

In this example, the colors array is reduced to an array of distinct values. The second argument sent to the reduce function is an empty array. This will be the initial value for distinct. When the distinct array does not already contain a specific color, it will be added.

Otherwise, it will be skipped, and the current distinct array will be returned. map and reduce are the main weapons of any functional programmer, and JavaScript is no exception. If you want to be a proficient JavaScript engineer, then you must master these functions. The ability to create one dataset from another is a required skill and is useful for any type of programming paradigm.

4 Higher-Order Functions.

The use of higher-order functions is also essential to functional programming. We've already mentioned higher-order functions, and we've even used a few in this chapter. Higher-order functions are functions that can manipulate other functions. They can take functions in as arguments or return functions or both.

The first category of higher-order functions are functions that expect other functions as arguments. Array.map, Array.filter, and Array.reduce all take functions as arguments. They are higher-order functions.

Let's take a look at how we can implement a higher-order function. In the following example, we create an invokeIf callback function that will test a condition and invoke a callback function when it's true and another callback function when the condition is false:

```js
const invokeIf = (condition, fnTrue, fnFalse) => condition ? fnTrue() : fnFalse();
const showWelcome = () => console.log("Welcome!!!"); 
const showUnauthorized = () => console.log("Unauthorized!!!"); 

invokeIf(true, showWelcome, showUnauthorized); // "Welcome!!!"
invokeIf(false, showWelcome, showUnauthorized); // "Unauthorized!!!"
```

invokeIf expects two functions: one for true and one for false. This is demonstrated by sending both showWelcome and showUnauthorized to invokeIf. When the condition is true, showWelcome is invoked. When it's false, showUnauthorized is invoked.

Higher-order functions that return other functions can help us handle the complexities associated with asynchronicity in JavaScript. They can help us create functions that can be used or reused at our convenience.

Currying is a functional technique that involves the use of higher-order functions.

The following is an example of currying. The userLogs function hangs on to some information (the username) and returns a function that can be used and reused when the rest of the information (the message) is made available. In this example, log messages will all be prepended with the associated username. Notice that we're using the getFakeMembers function that returns a promise from Chapter 2: 

```js
const userLogs = userName => message => 
  console.log(`${userName} -> ${message}`);

const log = userLogs("grandpa23");

log("attempted to load 20 fake members");
getFakeMembers(20).then(
  members => log(`successfully loaded ${members.length} members`), 
  error => log("encountered an error loading members")
);

// grandpa23 -> attempted to load 20 fake members
// grandpa23 -> successfully loaded 20 members
// grandpa23 -> attempted to load 20 fake members
// grandpa23 -> encountered an error loading members 
```

userLogs is the higher-order function. The log function is produced from userLogs, and every time the log function is used, "grandpa23" is prepended to the message.

1『目前上面的代码没看明白，关键是异步函数 getFakeMembers 的定义没找到。（2021-05-01）』

05 Recursion.

Recursion is a technique that involves creating functions that recall themselves. Often, when faced with a challenge that involves a loop, a recursive function can be used instead. Consider the task of counting down from 10. We could create a for loop to solve this problem, or we could alternatively use a recursive function. In this example, countdown is the recursive function:

1『作者的意思，只要是循环语句，都可以通过「递归」来实现，我原以为只有特性的场景下才需要递归，那么以后循环逻辑都可以尝试用递归来实现，也训练训练自己的大脑，大赞。（2021-05-30）』

```js
const countdown = (value, fn) => {
  fn(value);
  return value > 0 ? countdown(value - 1, fn) : value;
};

countdown(10, value => console.log(value));
// 10
// 9
// 8
// 7
// 6
// 5
// 4
// 3
// 2
// 1
// 0
```

countdown expects a number and a function as arguments. In this example, it's invoked with a value of 10 and a callback function. When countdown is invoked, the callback is invoked, which logs the current value. Next, countdown checks the value to see if it's greater than 0. If it is, countdown recalls itself with a decremented value. Eventually, the value will be 0, and countdown will return that value all the way back up the call stack.

Recursion is a pattern that works particularly well with asynchronous processes. Functions can recall themselves when they're ready, like when the data is available or when a timer has finished.

The countdown function can be modified to count down with a delay. This modified version of the countdown function can be used to create a countdown clock:

```js
const countdown = (value, fn, delay = 1000) => {
  fn(value);
  return value > 0
  ? setTimeout(() => countdown(value - 1, fn, delay), delay)
  : value;
};

const log = value => console.log(value);
countdown(10, log);
```

In this example, we create a 10-second countdown by initially invoking countdown once with the number 10 in a function that logs the countdown. Instead of recalling itself right away, the countdown function waits one second before recalling itself, thus creating a clock.

Recursion is a good technique for searching data structures. You can use recursion to iterate through subfolders until a folder that contains only files is identified. You can also use recursion to iterate though the HTML DOM until you find an element that does not contain any children. In the next example, we'll use recursion to iterate deeply into an object to retrieve a nested value:

```js
const dan = {
  type: "person",
  data: {
    gender: "male",
    info: {
      id: 22,
      fullname: {
        first: "Dan",
        last: "Deacon"
      }
    }
  }
};

deepPick("type", dan); // "person"
deepPick("data.info.fullname.first", dan); // "Dan"
```

deepPick can be used to access Dan's type, stored immediately in the first object, or to dig down into nested objects to locate Dan's first name. Sending a string that uses dot notation, we can specify where to locate values that are nested deep within an object:

```js
const deepPick = (fields, object = {}) => {
  const [first, ...remaining] = fields.split("."); 
  return remaining.length
    ? deepPick(remaining.join("."), object[first])
    : object[first];
};
```

The deepPick function is either going to return a value or recall itself until it eventually returns a value. First, this function splits the dot-notated fields string into an array and uses array destructuring to separate the first value from the remaining values. If there are remaining values, deepPick recalls itself with slightly different data, allowing it to dig one level deeper.

This function continues to call itself until the fields string no longer contains dots, meaning that there are no more remaining fields. In this sample, you can see how the values for first, remaining, and object[first] change as deepPick iterates through:

```js
deepPick("data.info.fullname.first", dan); // "Dan"

// First Iteration
// first = "data"
// remaining.join(".") = "info.fullname.first"
// object[first] = { gender: "male", {info} }

// Second Iteration
// first = "info"
// remaining.join(".") = "fullname.first"
// object[first] = {id: 22, {fullname}}

// Third Iteration
// first = "fullname"
// remaining.join("." = "first"
// object[first] = {first: "Dan", last: "Deacon" }

// Finally...
// first = "first"
// remaining.length = 0
// object[first] = "Deacon"
```

Recursion is a powerful functional technique that's fun to implement.

3『

[ES6 JavaScript compose function](https://gist.github.com/JamieMason/172460a36a0eaef24233e6edb2706f83)

Definition

```js
const compose = (...fns) =>
  fns.reduceRight((prevFn, nextFn) =>
    (...args) => nextFn(prevFn(...args)),
    value => value
  );
```

Example

Create the function, composed of three others:

```
const example = compose(
  val => { console.log(1); return `1<${val}>`; },
  val => { console.log(2); return `2<${val}>`; },
  val => { console.log(3); return `3<${val}>`; }
);
```

Console output is:

```
3
2
1
"1<2<3<hello>>>"
```

搞了半天，compose 不是内置函数，是自己定义的。在 Electron 上跑通了。

```js
export default observer(() => {
  const store = useLocalStore(() => new Store())

  const compose = (...fns) =>
    fns.reduceRight((prevFn, nextFn) =>
      (...args) => nextFn(prevFn(...args)),
      value => value
    )

  const example = compose(
    val => {
      console.log(1)
      return `1<${val}>`
    },
    val => { 
      console.log(2)
      return `2<${val}>`
    },
    val => { 
      console.log(3)
      return `3<${val}>`
    }
  )

  const testFun = () => {
    console.log(example('dalong'))
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

[Currying in JavaScript | Codementor](https://www.codementor.io/@michelre/currying-in-javascript-g6212s8qv)

[Use function composition in JavaScript | Codementor](https://www.codementor.io/@michelre/use-function-composition-in-javascript-gkmxos5mj)

[Curry and Function Composition.  | JavaScript Scene | Medium](https://medium.com/javascript-scene/curry-and-function-composition-2c208d774983)

前 2 篇文章作为本书的附件：「附件 0301-01Currying-in-JavaScript」「附件0301-02Use-function-composition-in-JavaScript」，后面的那篇 Medium 上的文档消化后放入 Medium 专栏里。

』

Putting It All Together

Now that we've been introduced to the core concepts of functional programming, let's put those concepts to work for us and build a small JavaScript application.

Our challenge is to build a ticking clock. The clock needs to display hours, minutes, seconds, and time of day in civilian time. Each field must always have double digits, meaning leading zeros need to be applied to single-digit values like 1 or 2. The clock must also tick and change the display every second.

First, let's review an imperative solution for the clock:

```js
// Log Clock Time every Second
setInterval(logClockTime, 1000);

function logClockTime() {
  // Get Time string as civilian time
  let time = getClockTime();
  // Clear the Console and log the time
  console.clear();
  console.log(time);
}

function getClockTime() {
  // Get the Current Time
  let date = new Date();
  let time = "";
  // Serialize clock time
  let time = {
    hours: date.getHours(),
    minutes: date.getMinutes(),
    seconds: date.getSeconds(),
    ampm: "AM"
  };

  // Convert to civilian time
  if (time.hours == 12) {
    time.ampm = "PM";
  } else if (time.hours > 12) {
    time.ampm = "PM";
    time.hours -= 12;
  }

  // Prepend a 0 on the hours to make double digits
  if (time.hours < 10) {
    time.hours = "0" + time.hours;
  }

  // prepend a 0 on the minutes to make double digits
  if (time.minutes < 10) {
    time.minutes = "0" + time.minutes;
  }

  // prepend a 0 on the seconds to make double digits 
  if (time.seconds < 10) {
    time.seconds = "0" + time.seconds;
  }

  // Format the clock time as a string "hh:mm:ss tt"
  return time.hours + ":" + time.minutes + ":" + time.seconds + " " + time.ampm;
}
```

This solution works, and the comments help us understand what's happening. However, these functions are large and complicated. Each function does a lot. They're hard to comprehend, they require comments, and they're tough to maintain. Let's see how a functional approach can produce a more scalable application.

Our goal will be to break the application logic up into smaller parts: functions. Each function will be focused on a single task, and we'll compose them into larger functions that we can use to create the clock.

First, let's create some functions that give us values and manage the console. We'll need a function that gives us one second, a function that gives us the current time, and a couple of functions that will log messages on a console and clear the console. In functional programs, we should use functions over values wherever possible. We'll invoke the function to obtain the value when needed:

```js
const oneSecond = () => 1000;
const getCurrentTime = () => new Date();
const clear = () => console.clear();
const log = message => console.log(message);
```

Next, we'll need some functions for transforming data. These three functions will be used to mutate the Date object into an object that can be used for our clock:

1 serializeClockTime. Takes a date object and returns an object for clock time that contains hours, minutes, and seconds.

2 civilianHours. Takes the clock time object and returns an object where hours are converted to civilian time. For example: 1300 becomes 1:00.

3 appendAMPM. Takes the clock time object and appends time of day (AM or PM) to that object.

```js
const serializeClockTime = date => ({
  hours: date.getHours(),
  minutes: date.getMinutes(),
  seconds: date.getSeconds()
});

const civilianHours = clockTime => ({
  ...clockTime,
  hours: clockTime.hours > 12 ? clockTime.hours - 12 : clockTime.hours
});

const appendAMPM = clockTime => ({
  ...clockTime,
  ampm: clockTime.hours >= 12 ? "PM" : "AM"
});
```

These three functions are used to transform data without changing the original. They treat their arguments as immutable objects.

Next, we'll need a few higher-order functions: 

1 display. Takes a target function and returns a function that will send a time to the target. In this example, the target will be console.log.

2 formatClock. Takes a template string and uses it to return clock time formatted based on the criteria from the string. In this example, the template is "hh:mm:ss tt". From there, formatClock will replace the placeholders with hours, minutes, seconds, and time of day.

3 prependZero. Takes an object's key as an argument and prepends a zero to the value stored under that object's key. It takes in a key to a specific field and prepends values with a zero if the value is less than 10.

```js
const display = target => time => target(time); 
const formatClock = format => time =>
  format
    .replace("hh", time.hours)
    .replace("mm", time.minutes)
    .replace("ss", time.seconds)
    .replace("tt", time.ampm);

const prependZero = key => clockTime => ({
  ...clockTime,
  key: clockTime[key] < 10 ? "0" + clockTime[key] : clockTime[key]
});
```

These higher-order functions will be invoked to create the functions that will be reused to format the clock time for every tick. Both formatClock and prependZero will be invoked once, initially setting up the required template or key. The inner functions they return will be invoked once every second to format the time for display.

Now that we have all of the functions required to build a ticking clock, we'll need to compose them. We'll use the compose function that we defined in the last section to handle composition:

1 convertToCivilianTime. A single function that takes clock time as an argument and transforms it into civilian time by using both civilian hours.

2 doubleDigits. A single function that takes civilian clock time and makes sure the hours, minutes, and seconds display double digits by prepending zeros where needed.

3 startTicking. Starts the clock by setting an interval that invokes a callback every second. The callback is composed using all our functions. Every second the console is cleared, currentTime is obtained, converted, civilianized, formatted, and displayed.

```js
const convertToCivilianTime = clockTime =>
  compose(
  appendAMPM,
  civilianHours
  )(clockTime);

const doubleDigits = civilianTime =>
  compose(
  prependZero("hours"),
  prependZero("minutes"),
  prependZero("seconds")
  )(civilianTime);

const startTicking = () =>
  setInterval(
  compose(
    clear,
    getCurrentTime,
    serializeClockTime,
    convertToCivilianTime,
    doubleDigits,
    formatClock("hh:mm:ss tt"),
    display(log)
  ),
  oneSecond()
  );

startTicking();
```

This declarative version of the clock achieves the same results as the imperative version. However, there quite a few benefits to this approach. First, all of these functions are easily testable and reusable. They can be used in future clocks or other digital displays. Also, this program is easily scalable. There are no side effects. There are no global variables outside of functions themselves. There could still be bugs, but they'll be easier to find.

In this chapter, we've introduced functional programming principles.

Throughout the book when we discuss best practices in React, we'll continue to demonstrate how many React concepts are based in functional techniques. In the next chapter, we'll dive into React officially with an improved understanding of the principles that guided its development.

### 0107. 主题卡 —— 使用 map 函数生成一系列 React Elements

信息源自「2021060Learning-React0401.md」

The major advantage of using React is its ability to separate data from UI elements. Since React is just JavaScript, we can add JavaScript logic to help us build the React component tree. For example, ingredients can be stored in an array, and we can map that array to the React elements.

Let's go back and think about the unordered list for a moment: 

```js
React.createElement( 
  "ul", 
  null, 
  React.createElement("li", null, "2 lb salmon"), 
  React.createElement("li", null, "5 sprigs fresh rosemary"), 
  React.createElement("li", null, "2 tablespoons olive oil"), 
  React.createElement("li", null, "2 small lemons"), 
  React.createElement("li", null, "1 teaspoon kosher salt"), 
  React.createElement("li", null, "4 cloves of chopped garlic") 
);
```

The data used in this list of ingredients can easily be represented using a JavaScript array:

```js
const items = [ 
  "2 lb salmon", 
  "5 sprigs fresh rosemary", 
  "2 tablespoons olive oil", 
  "2 small lemons", 
  "1 teaspoon kosher salt", 
  "4 cloves of chopped garlic" 
];
```

We want to use this data to generate the correct number of list items without having to hard-code each one. We can map over the array and create list items for as many ingredients as there are:

```js
React.createElement( 
  "ul", { className: "ingredients" }, 
  items.map(ingredient => React.createElement("li", null, ingredient)) 
);
```

1-2『首次看到使用 map 函数生成一系列 React Elements，对我意义重大。做一张主题卡片。（2021-05-02）』—— 已完成

This syntax creates a React element for each ingredient in the array. Each string is displayed in the list item's children as text. The value for each ingredient is displayed as the list item. When running this code, you'll see a console warning like the one shown in Figure 4-1.

Figure 4-1. Console warning

When we build a list of child elements by iterating through an array, React likes each of those elements to have a key property. The key property is used by React to help it update the DOM efficiently. You can make this warning go away by adding a unique key property to each of the list item elements. You can use the array index for each ingredient as that unique value:

```js
React.createElement( 
  "ul", 
  { className: "ingredients" }, 
  items.map((ingredient, i) => 
    React.createElement("li", { key: i }, ingredient) ) 
);
```

We'll cover keys in more detail when we discuss JSX, but adding this to each list item will clear the console warning.

### 0108. 主题卡 —— 创建 React Elements 时直接传递「数据」作为组件的属性

信息源自「2021060Learning-React0401.md」

This is pretty cool, but we've hardcoded this data into the component. What if we could build one component and then pass data into that component as properties? And then what if that component could render the data dynamically? Maybe someday that will happen!

2『下面有关创建 React Elements 时直接传递「数据」作为组件的属性，做一张主题卡片。（2021-05-02）』—— 已完成

Just kidding — that day is now. Here's an array of secretIngredients needed to put together a recipe:

```js
const secretIngredients = [
  "1 cup unsalted butter", 
  "1 cup crunchy peanut butter", 
  "1 cup brown sugar", 
  "1 cup white sugar", 
  "2 eggs", 
  "2.5 cups all purpose flour", 
  "1 teaspoon baking powder", 
  "0.5 teaspoon salt" 
];
```

Then we'll adjust the IngredientsList component to map over these items, constructing an li for however many items are in the items array:

```js
function IngredientsList() {
  return React.createElement( 
    "ul", 
    { className: "ingredients" }, 
    items.map((ingredient, i) => 
      React.createElement("li", { key: i }, ingredient) 
    ) 
  );
}
```

Then we'll pass those secretIngredients as a property called items, which is the second argument used in createElement:

```js
ReactDOM.render( 
  React.createElement(IngredientsList, { items: secretIngredients }, null),
  document.getElementById("root") 
);
```

Now, let's look at the DOM. The data property items is an array with eight ingredients. Because we made the li tags using a loop, we were able to add a unique key using the index of the loop:

```js
<IngredientsList items="[...]">
  <ul className="ingredients">
    <li key="0">1 cup unsalted butter</li> 
    <li key="1">1 cup crunchy peanut butter</li>
    <li key="2">1 cup brown sugar</li>
    <li key="3">1 cup white sugar</li>
    <li key="4">2 eggs</li>
    <li key="5">2.5 cups all purpose flour</li>
    <li key="6">1 teaspoon baking powder</li>
    <li key="7">0.5 teaspoon salt</li>
  </ul> 
</IngredientsList>
```

Creating our component this way will make the component more flexible. Whether the items array is one item or a hundred items long, the component will render each as a list item.

Another adjustment we can make here is to reference the items array from React props. Instead of mapping over the global items, we'll make items available on the props object. Start by passing props to the function, then mapping over props.items:

```js
function IngredientsList(props) {
  return React.createElement( 
    "ul", 
    { className: "ingredients" }, 
    props.items.map((ingredient, i) => 
      React.createElement("li", { key: i }, ingredient) 
    ) 
  );
}
```

We could also clean up the code a bit by destructuring items from props:

```js
function IngredientsList({ items }) { 
  return React.createElement( 
    "ul", 
    { className: "ingredients" }, 
    items.map((ingredient, i) => 
      React.createElement("li", { key: i }, ingredient) 
    ) 
  );
}
```

Everything that's associated with the UI for IngredientsList is encapsulated into one component. Everything we need is right there.

### 0109. 主题卡 —— State 和 Property 在 React 的数据「地图」上各占半壁江山

信息源自「2021060Learning-React0601.md」

In the last chapter, we constructed a component tree: a hierarchy of components that data was able to flow through as properties. Properties are half of the picture. State is the other half. The state of a React application is driven by data that has the ability to change. Introducing state to the recipe application could make it possible for chefs to create new recipes, modify existing recipes, and remove old ones.

2『 State 和 Property 在 React 的数据「地图」上各占半壁江山。做一张主题卡片。（2021-05-04）』—— 已完成

State and properties have a relationship with each other. When we work with React applications, we gracefully compose components that are tied together based on this relationship. When the state of a component tree changes, so do the properties. The new data flows through the tree, causing specific leaves and branches to render to reflect the new content.

In this chapter, we're going to bring applications to life by introducing state. We'll learn to create stateful components and how state can be sent down a component tree and user interactions back up the component tree. We'll learn techniques for collecting form data from users. And we'll take a look at the various ways in which we can separate concerns within our applications by introducing stateful context providers.

### 0110. 主题卡 —— 钩子的核心作用在于重新渲染

信息源自「2021060Learning-React0601.md」

The most important thing to remember about Hooks is that they can cause the component they're hooked into to rerender. Every time we invoke the setSelectedStars function to change the value of selectedStars, the StarRating function component will be reinvoked by the hook, and it will render again, this time with a new value for selectedStars. This is why Hooks are such a killer feature.

When data within the hook changes, they have the power to rerender the component they're hooked into with new data.

2『钩子的核心作用在于重新渲染，做一张主题卡片。（2021-05-08）』—— 已完成

The StarRating component will be rerendered every time a user clicks a Star. When the user clicks the Star, the onSelect property of that star is invoked. When the onSelect property is invoked, we'll invoke the setSelectedStars function and send it the number of the star that was just selected. We can use the i variable from the map function to help us calculate that number. When the map function renders the first Star, the value for i is 0. This means that we need to add 1 to this value to get the correct number of stars. When setSelectedStars is invoked, the StarRating component is invoked with a the value for selectedStars, as shown in Figure 6-4.

### 0201. 术语卡 —— Declarative Programming and Imperative Programming

信息源自「2021060Learning-React0301.md」

Functional programming is a part of a larger programming paradigm: declarative programming. Declarative programming is a style of programming where applications are structured in a way that prioritizes describing what should happen over defining how it should happen.

1『之前在耗子哥的专栏里有看到过「申明式」编程的概念，Declarative Programming 做一张术语卡片。（2021-05-01）』—— 已完成

In order to understand declarative programming, we'll contrast it with imperative programming, or a style of programming that's only concerned with how to achieve results with code. Let's consider a common task: making a string URL-friendly. Typically, this can be accomplished by replacing all of the spaces in a string with hyphens, since spaces are not URL-friendly. First, let's examine an imperative approach to this task:


```js
const string = "Restaurants in Hanalei"; 
const urlFriendly = "";

for (var i = 0; i < string.length; i++) {
  if (string[i] === " ") {
    urlFriendly += "-";
  } else {
    urlFriendly += string[i];
  }
}

console.log(urlFriendly); // "Restaurants-in-Hanalei"
```

In this example, we loop through every character in the string, replacing spaces as they occur. The structure of this program is only concerned with how such a task can be achieved. We use a for loop and an if statement and set values with an equality operator. Just looking at the code alone does not tell us much. Imperative programs require lots of comments in order to understand what's going on.

Now let's look at a declarative approach to the same problem: 

```js
const string = "Restaurants in Hanalei"; 
const urlFriendly = string.replace(/ /g, "-"); 

console.log(urlFriendly);
```

Here we are using string.replace along with a regular expression to replace all instances of spaces with hyphens. Using string.replace is a way of describing what's supposed to happen: spaces in the string should be replaced. The details of how spaces are dealt with are abstracted away inside the replace function. In a declarative program, the syntax itself describes what should happen, and the details of how things happen are abstracted away.

Declarative programs are easy to reason about because the code itself describes what is happening. For example, read the syntax in the following sample. It details what happens after members are loaded from an API:

```js
const loadAndMapMembers = compose(
  combineWith(sessionStorage, "members"),
  save(sessionStorage, "members"),
  scopeMembers(window),
  logMemberInfoToConsole,
  logFieldsToConsole("name.first"),
  countMembersBy("location.state"),
  prepStatesForMapping,
  save(sessionStorage, "map"),
  renderUSMap
);
  
getFakeMembers(100).then(loadAndMapMembers);
```

The declarative approach is more readable and, thus, easier to reason about. The details of how each of these functions is implemented are abstracted away. Those tiny functions are named well and combined in a way that describes how member data goes from being loaded to being saved and printed on a map, and this approach does not require many comments. Essentially, declarative programming produces applications that are easier to reason about, and when it's easier to reason about an application, that application is easier to scale. Additional details about the declarative programming paradigm can be found at the Declarative Programming wiki.

The declarative approach is more readable and, thus, easier to reason about. The details of how each of these functions is implemented are abstracted away. Those tiny functions are named well and combined in a way that describes how member data goes from being loaded to being saved and printed on a map, and this approach does not require many comments. Essentially, declarative programming produces applications that are easier to reason about, and when it's easier to reason about an application, that application is easier to scale. Additional details about the declarative programming paradigm can be found at the Declarative Programming wiki.

Now, let's consider the task of building a document object model, or DOM. An imperative approach would be concerned with how the DOM is constructed:

```js
const target = document.getElementById("target");
const wrapper = document.createElement("div"); 
const headline = document.createElement("h1"); 
wrapper.id = "welcome";
headline.innerText = "Hello World";
wrapper.appendChild(headline);
target.appendChild(wrapper);
```

This code is concerned with creating elements, setting elements, and adding them to the document. It would be very hard to make changes, add features, or scale 10,000 lines of code where the DOM is constructed imperatively.

Now let's take a look at how we can construct a DOM declaratively using a React component:

```js
const { render } = ReactDOM;
const Welcome = () => (
  <div id="welcome">
    <h1>Hello World</h1>
  </div>
);
render(<Welcome />, document.getElementById("target")); 
```

React is declarative. Here, the Welcome component describes the DOM that should be rendered. The render function uses the instructions declared in the component to build the DOM, abstracting away the details of how the DOM is to be rendered. We can clearly see that we want to render our Welcome component into the element with the ID of target.

### 0202. 术语卡 —— SPA

信息源自「2021060Learning-React0401.md」

In the past, websites consisted of independent HTML pages. When the user navigated these pages, the browser would request and load different HTML documents. The invention of AJAX (Asynchronous JavaScript and XML) brought us the single-page application, or SPA. Since browsers could request and load tiny bits of data using AJAX, entire web applications could now run out of a single page and rely on JavaScript to update the user interface.

In an SPA, the browser initially loads one HTML document. As users navigate through the site, they actually stay on the same page. JavaScript destroys and creates a new user interface as the user interacts with the application. It may feel as though you're jumping from page to page, but you're actually still on the same HTML page, and JavaScript is doing the heavy lifting.

2『 SPA 做一张术语卡片。（2021-05-02）』—— 已完成

### 0203. 术语卡 —— React DOM 和 React elements

React DOM 和 React elements 是 React 的核心。

信息源自「2021060Learning-React0401.md」

The DOM API is a collection of objects that JavaScript can use to interact with the browser to modify the DOM. If you've used document.createElement or document.appendChild, you've worked with the DOM API.

React is a library that's designed to update the browser DOM for us. We no longer have to be concerned with the complexities associated with building high-performing SPAs because React can do that for us. With React, we do not interact with the DOM API directly. Instead, we provide instructions for what we want React to build, and React will take care of rendering and reconciling the elements we've instructed it to create.

2『 DOM API（React DOM）是一个 JS 库，这个库帮我们跟浏览器的 DOM 打交道。React DOM 和 React elements 做一张术语卡片。（2021-05-02）』—— 已完成

The browser DOM is made up of DOM elements. Similarly, the React DOM is made up of React elements. DOM elements and React elements may look the same, but they're actually quite different. A React element is a description of what the actual DOM element should look like. In other words, React elements are the instructions for how the browser DOM should be created.

We can create a React element to represent an h1 using React.createElement:

```js
React.createElement("h1", { id: "recipe-0" }, "Baked Salmon"); 
```

The first argument defines the type of element we want to create. In this case, we want to create an h1 element. The second argument represents the element's properties. This h1 currently has an id of recipe-0. The third argument represents the element's children: any nodes that are inserted between the opening and closing tag (in this case, just some text).

During rendering, React will convert this element to an actual DOM element:

```html
<h1 id="recipe-0" > Baked Salmon</h1> 
```

The properties are similarly applied to the new DOM element: the properties are added to the tag as attributes, and the child text is added as text within the element. A React element is just a JavaScript literal that tells React how to construct the DOM element. If you were to log this element, it would look like this:

```json
{
  $$typeof: Symbol(React.element),
  "type": "h1",
  "key": null,
  "ref": null,
  "props": {id: "recipe-0", children: "Baked Salmon"},
  "_owner": null,
  "_store": {}
}
```

This is the structure of a React element. There are fields that are used by React: `_owner`, `_store`, and `$$typeof`. The key and ref fields are important to React elements, but we'll introduce those later. For now, let's take a closer look at the type and props fields.

The type property of the React element tells React what type of HTML or SVG element to create. The props property represents the data and child elements required to construct a DOM element. The children property is for displaying other nested elements as text.

CREATING ELEMENTS

We're taking a peek at the object that React.createElement returns. You won't actually create these elements by hand; instead, you'll use the React.createElement function.

### 0204. 术语卡 —— JSX

信息源自「2021060Learning-React0501.md」

In the last chapter, we dove deep into how React works, breaking down our React applications into small reusable pieces called components. These components render trees of elements and other components.

Using the createElement function is a good way to see how React works, but as React developers, that's not what we do. We don't go around composing complex, barely readable trees of JavaScript syntax and call it fun. In order to work efficiently with React, we need one more thing: JSX.

JSX combines the JS from JavaScript and the X from XML. It is a JavaScript extension that allows us to define React elements using a tag-based syntax directly within our JavaScript code. Sometimes JSX is confused with HTML because they look similar. JSX is just another way of creating React elements, so you don't have to pull your hair out looking for the missing comma in a complex createElement call.

2『 JSX 做一张术语卡片。（2021-05-03）』

### 0205. 术语卡 —— Babel

信息源自「2021060Learning-React0501.md」

Many software languages require you to compile your source code. JavaScript is an interpreted language: the browser interprets the code as text, so there's no need to compile JavaScript. However, not all browsers support the latest JavaScript syntax, and no browser supports JSX syntax. Since we want to use the latest features of JavaScript along with JSX, we're going to need a way to convert our fancy source code into something that the browser can interpret. This process is called compiling, and it's what Babel is designed to do.

1-2『本书作者给了自己很多醍醐灌顶的知识点，看到上面的信息才算弄明白 Babel 干啥的。虽然 JS 是解释性语言，但不是所有的浏览器都支持 JS 的最新相关语法（ES6、JSX 等），所需需要 Babel 来「翻译」。Babel 做一张术语卡片。（2021-05-03）』—— 已完成

The first version of the project was called 6to5, and it was released in September 2014. 6to5 was a tool that could be used to convert ES6 syntax to ES5 syntax, which was more widely supported by web browsers. As the project grew, it aimed to be a platform to support all of the latest changes in ECMAScript. It also grew to support converting JSX into JavaScript. The project was renamed Babel in February 2015.

Babel is used in production at Facebook, Netflix, PayPal, Airbnb, and more. Previously, Facebook had created a JSX transformer that was their standard, but it was soon retired in favor of Babel.

There are many ways of working with Babel. The easiest way to get started is to include a link to the Babel CDN directly in your HTML, which will compile any code in script blocks that have a type of 'text/babel'. Babel will compile the source code on the client before running it. Although this may not be the best solution for production, it's a great way to get started with JSX:

### 0206. 术语卡 —— Webpack

搞了半天，才意识到目前在做的事情是用 webpack 把所有前端代码打包成一个静态文件，服务器上直接读这个静态文件即可。就是数据流前端开发后，在公司服务器上 `yarn build:prod` 或者阿里云上 `yarn build:stage` 在干的事情一样。真实恍然大悟的感觉。补充进 webpack 的术语卡片中。（2021-05-03）

信息源自「2021060Learning-React0501.md」

Once we start working with React in real projects, there are a lot of questions to consider: How do we want to deal with JSX and ESNext transformation? How can we manage our dependencies? How can we optimize our images and CSS?

Many different tools have emerged to answer these questions, including Browserify, gulp, Grunt, Prepack, and more. Due to its features and widespread adoption by large companies, webpack has also emerged as one of the leading tools for bundling.

The React ecosystem has matured to include tools like create-react-app, Gatsby, and Code Sandbox. When you use these tools, a lot of the details about how the code gets compiled are abstracted away. For the remainder of this chapter, we are going to set up our own webpack build. This day in age, understanding that your JavaScript/React code is being compiled by something like webpack is vital, but knowing how to compile your JavaScript/React with something like webpack is not as important. We understand if you want to skip ahead.

Webpack is billed as a module bundler. A module bundler takes all of our different files (JavaScript, LESS, CSS, JSX, ESNext, and so on) and turns them into a single file. The two main benefits of bundling are modularity and network performance.

12『这里的信息让自己对 Webpack 理解比以前深了些，但感觉还是云里雾里，没吃透。先做一张术语卡片。（2021-05-03）』—— 已完成

Modularity will allow you to break down your source code into parts, or modules, that are easier to work with, especially in a team environment. Network performance is gained by only needing to load one dependency in the browser: the bundle. Each script tag makes an HTTP request, and there's a latency penalty for each HTTP request.

Bundling all the dependencies into a single file allows you to load everything with one HTTP request, thereby avoiding additional latency.

Aside from code compilation, webpack also can handle:

1 Code splitting: Splits up your code into different chunks that can be loaded when you need them. Sometimes these are called rollups or layers; the aim is to break up code as needed for different pages or devices.

2 Minification: Removes whitespace, line breaks, lengthy variable names, and unnecessary code to reduce the file size.

3 Feature Flagging: Sends code to one or more — but not all — environments when testing out features.

4 Hot Module Replacement (HMR): Watches for changes in source code. Changes only the updated modules immediately.

The Recipes app we built earlier in this chapter has some limitations that webpack will help us alleviate. Using a tool like webpack to statically build client JavaScript makes it possible for teams to work together on large-scale web applications. We can also gain the following benefits by incorporating the webpack module bundler: 

1 Modularity: Using the module pattern to export modules that will later be imported or required by another part of the application makes source code more approachable. It allows development teams to work together, by allowing them to create and work with separate files that will be statically combined into a single file before sending to production.

2 Composition: With modules, we can build small, simple, reusable React components that we can compose efficiently into applications. Smaller components are easier to comprehend, test, and reuse. They're also easier to replace down the line when enhancing applications.

3 Speed: Packaging all the application's modules and dependencies into a single client bundle will reduce the load time of an application because there's latency associated with each HTTP request. Packaging everything together in a single file means that the client will only need to make a single request. Minifying the code in the bundle will improve load time as well.

4 Consistency: Since webpack will compile JSX and JavaScript, we can start using tomorrow's JavaScript syntax today. Babel supports a wide range of ESNext syntax, which means we don't have to worry about whether the browser supports our code. It allows developers to consistently use cutting-edge JavaScript syntax.

### 0301. 数据信息卡 —— 函数申明和函数表达式创建函数对象的区别

信息源自「2021060Learning-React0201.md」

One thing to be aware of when deciding between a function declaration and a function expression is that function declarations are hoisted and function expressions are not. In other words, you can invoke a function before you write a function declaration. You cannot invoke a function created by a function expression. This will cause an error. For example:

2『函数申明和函数表达式创建函数对象的区别，做一张信息数据卡片。（2021-04-29）』—— 已完成

```js
// Invoking the function before it's declared
hey();
// Function Declaration
function hey() {
  alert("hey!");
}
```

This works. You'll see the alert appear in the browser. It works because the function is hoisted, or moved up, to the top of the file's scope. Trying the same exercise with a function expression will cause an error:

```js
// Invoking the function before it's declared
hey();
// Function Expression
const hey = function() {
  alert("hey!");
};
```

```
TypeError: hey is not a function
```

This is obviously a small example, but this TypeError can occasionally arise when importing files and functions in a project. If you see it, you can always refactor as a declaration.

### 0302. 数据信息卡 —— 箭头函数返回对象

信息源自「2021060Learning-React0201.md」

What happens if you want to return an object? Consider a function called person that builds an object based on parameters passed in for firstName and lastName:

```js
const person = (firstName, lastName) => {
  first: firstName,
  last: lastName
}

console.log(person("Brad", "Janson")); 
```

As soon as you run this, you'll see the error: 

```
Uncaught SyntaxError: Unexpected token :. 
```

To fix this, just wrap the object you're returning with parentheses:

```js
const person = (firstName, lastName) => ({
  first: firstName,
  last: lastName
});
  
console.log(person("Flad", "Hanson")); 
```

These missing parentheses are the source of countless bugs in JavaScript and React apps, so it's important to remember this one!

1『解惑了解惑了，很多地方看到了这种语句，箭头函数返回对象，做一张信息数据卡片。（2021-04-29）』—— 已完成

### 0303. 数据信息卡 —— React Fragments 容纳多个组件

信息源自「2021060Learning-React0501.md」

In the previous section, we rendered the Menu component, a parent component that rendered the Recipe component. We want to take a moment to look at a small example of rendering two sibling components using a React fragment. Let's start by creating a new component called Cat that we'll render to the DOM at the root: 

```js
function Cat({ name }) {
  return <h1>The cat's name is {name}</h1>;
}
  
ReactDOM.render(
  <Cat name="Jungle" />, 
  document.getElementById("root")
); 
```

This will render the h1 as expected, but what might happen if we added a p tag to the Cat component at the same level as the h1?

```js
function Cat({ name }) {
  return (
    <h1>The cat's name is {name}</h1>
    <p>He's good.</p>
  );
}
```

Immediately, we'll see an error in the console that reads Adjacent JSX elements must be wrapped in an enclosing tag and recommends using a fragment. This is where fragments come into play! React will not render two or more adjacent or sibling elements as a component, so we used to have to wrap these in an enclosing tag like a div. This led to a lot of unnecessary tags being created, though, and a bunch of wrappers without much purpose. If we use a React fragment, we can mimic the behavior of a wrapper without actually creating a new tag. Start by wrapping the adjacent tags, the h1 and p, with a React.Fragment tag:

```js
function Cat({ name }) {
  return (
    <React.Fragment>
      <h1>The cat's name is {name}</h1>
      <p>He's good.</p>
    </React.Fragment>
  );
}
```

Adding this clears the warning. You also can use a fragment shorthand to make this look even cleaner:

```js
function Cat({ name }) {
  return (
    <>
      <h1>The cat's name is {name}</h1>
      <p>He's good.</p>
    </>
  );
}
```

1『大赞啊，上面的代码涨知识了，而且也解决了自己之前遇到的困惑。React Fragments 容纳多个组件，做一张信息数据卡片。（2021-05-03）』—— 已完成

If you look at the DOM, the fragment is not visible in the resulting tree:

```js
<div id="root" >
  <h1> The cat's name is Jungle</h1>
  <p> He's good</p>
</div>
```

Fragments are a relatively new feature of React and do away with the need for extra wrapper tags that can pollute the DOM.

### 0401. 任意卡 —— 通过 reduce 实现数据去重

信息源自「2021060Learning-React0301.md」

We can even transform arrays into completely different arrays using reduce. Consider reducing an array with multiple instances of the same value to an array of unique values. The reduce method can be used to accomplish this task:

```js
const colors = ["red", "red", "green", "blue", "green"]; 
const uniqueColors = colors.reduce((unique, color) =>
  unique.indexOf(color) !== -1 ? unique : [...unique, color],
  []
);

console.log(uniqueColors);
// ["red", "green", "blue"]
```

2『又获得了一个数组去重的实现，做一张任意卡片。（2021-05-01）』

In this example, the colors array is reduced to an array of distinct values. The second argument sent to the reduce function is an empty array. This will be the initial value for distinct. When the distinct array does not already contain a specific color, it will be added.

Otherwise, it will be skipped, and the current distinct array will be returned. map and reduce are the main weapons of any functional programmer, and JavaScript is no exception. If you want to be a proficient JavaScript engineer, then you must master these functions. The ability to create one dataset from another is a required skill and is useful for any type of programming paradigm.

### 0402. 任意卡 —— 如何同时渲染多个 React Elements

信息源自「2021060Learning-React0301.md」

We can render a React element, including its children, to the DOM with ReactDOM.render. The element we want to render is passed as the first argument, and the second argument is the target node, where we should render the element:

```js
const dish = React.createElement("h1", null, "Baked Salmon"); 
ReactDOM.render(dish, document.getElementById("root"));
```

Rendering the title element to the DOM would add an h1 element to the div with the id of root, which we would already have defined in our HTML. We build this div inside the body tag:

```html
<body>
  <div id="root" >
    <h1> Baked Salmon</h1>
  </div>
</body>
```

Anything related to rendering elements to the DOM is found in the ReactDOM package. In versions of React earlier than React 16, you could only render one element to the DOM. Today, it's possible to render arrays as well. When the ability to do this was announced at ReactConf 2017, everyone clapped and screamed. It was a big deal.

This is what that looks like:

```js
const dish = React.createElement("h1", null, "Baked Salmon");
const dessert = React.createElement("h2", null, "Coconut Cream Pie"); 
ReactDOM.render([dish, dessert], document.getElementById("root")); 
```

This will render both of these elements as siblings inside of the root container. We hope you just clapped and screamed! In the next section, we'll get an understanding of how to use props.children.

2『如何同时渲染多个 React Elements，做一张任意卡片。（2021-05-02）』

### 0501. 金句卡 ——

最后根据他写的非常震撼的话语——产生一张金句卡。

## Preface

This book is for developers who want to learn the React library while learning the latest techniques currently emerging in the JavaScript language. This is an exciting time to be a JavaScript developer. The ecosystem is exploding with new tools, syntax, and best practices that promise to solve many of our development problems. Our aim with this book is to organize these techniques so you can get to work with React right away. We'll get into state management, React Router, testing, and server rendering, so we promise not to introduce only the basics and then throw you to the wolves.

This book does not assume any knowledge of React at all. We'll introduce all of React's basics from scratch. Similarly, we won't assume that you've worked with the latest JavaScript syntax. This will be introduced in Chapter 2 as a foundation for the rest of the chapters.

You'll be better prepared for the contents of the book if you're comfortable with HTML, CSS, and JavaScript. It's almost always best to be comfortable with these big three before diving into a JavaScript library.

Along the way, check out the GitHub repository. All of the examples are there and will allow you to practice hands-on.

Supplemental material (code examples, exercises, etc.) is available for download at https://github.com/moonhighway/learning-react. If you have a technical question or a problem using the code examples, please send email to bookquestions@oreilly.com.

1-2-3『

[MoonHighway/learning-react: The code samples for Learning React by Alex Banks and Eve Porcello, published by O'Reilly Media](https://github.com/moonhighway/learning-react)

已下载源码作为本书附件。（2021-04-29）

』

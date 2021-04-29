## 记忆时间

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

### 0201. 术语卡 ——

根据反常识，再补充三个证据——就产生三张术语卡。

### 0202. 术语卡 ——

### 0203. 术语卡 ——

### 0301. 金句卡 ——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0401. 数据信息卡 —— 函数申明和函数表达式创建函数对象的区别

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

### 0401. 数据信息卡 —— 箭头函数返回对象

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

### 0601. 任意卡 ——

最后还有一张任意卡，记录个人阅读感想。

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

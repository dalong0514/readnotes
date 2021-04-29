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

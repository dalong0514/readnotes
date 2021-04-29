## 记忆时间

## 目录

0101Welcome to React

0201JavaScript for React

## 0101. Welcome to React

What makes a JavaScript library good? Is it the number of stars on GitHub? The number of downloads on npm? Is the number of tweets that ThoughtLeaders™ write about it on a daily basis important? How do we pick the best tool to use to build the best thing? How do we know it's worth our time? How do we know it's good?

When React was first released, there was a lot of conversation around whether it was good, and there were many skeptics. It was new, and the new can often be upsetting.

To respond to these critiques, Pete Hunt from the React team wrote an article called「Why React?」that recommended that you「give it [React] five minutes.」He wanted to encourage people to work with React first before thinking that the team's approach was too wild.

Yes, React is a small library that doesn't come with everything you might need out of the box to build your application. Give it five minutes.

Yes, in React, you write code that looks like HTML right in your JavaScript code. And yes, those tags require preprocessing to run in a browser. And you'll probably need a build tool like webpack for that. Give it five minutes.

As React approaches a decade of use, a lot of teams decided that it's good because they gave it five minutes. We're talking Uber, Twitter, Airbnb, and Twitter — huge companies that tried React and realized that it could help teams build better products faster. At the end of the day, isn't that what we're all here for? Not for the tweets. Not for the stars.

Not for the downloads. We're here to build cool stuff with tools that we like to use. We're here for the glory of shipping stuff that we're proud to say we built. If you like doing those types of things, you'll probably like working with React.

### 1.1 A Strong Foundation

Whether you're brand new to React or looking to this text to learn some of the latest features, we want this book to serve as a strong foundation for all your future work with the library. The goal of this book is to avoid confusion in the learning process by putting things in a sequence: a learning roadmap.

Before digging into React, it's important to know JavaScript. Not all of JavaScript, not every pattern, but having a comfort with arrays, objects, and functions before jumping into this book will be useful.

In the next chapter, we'll look at newer JavaScript syntax to get you acquainted with the latest JavaScript features, especially those that are frequently used with React. Then we'll give an introduction to functional JavaScript so you can understand the paradigm that gave birth to React. A nice side effect of working with React is that it can make you a stronger JavaScript developer by promoting patterns that are readable, reusable, and testable. Sort of like a gentle, helpful brainwashing.

From there, we'll cover foundational React knowledge to understand how to build out a user interface with components. Then we'll learn to compose these components and add logic with props and state. We'll cover React Hooks, which allow us to reuse stateful logic between components.

Once the basics are in place, we'll build a new application that allows users to add, edit, and delete colors. We'll learn how Hooks and Suspense can help us with data fetching. Throughout the construction of that app, we'll introduce a variety of tools from the broader React ecosystem that are used to handle common concerns like routing, testing, and server-side rendering.

We hope to get you up to speed with the React ecosystem faster by approaching it this way — not just to scratch the surface, but to equip you with the tools and skills necessary to build real-world React applications.

### 1.2 React's Past and Future

React was first created by Jordan Walke, a software engineer at Facebook. It was incorporated into Facebook's newsfeed in 2011 and later on Instagram when it was acquired by Facebook in 2012. At JSConf 2013, React was made open source, and it joined the crowded category of UI libraries like jQuery, Angular, Dojo, Meteor, and others.

At that time, React was described as「the V in MVC.」In other words, React components acted as the view layer or the user interface for your JavaScript applications.

From there, community adoption started to spread. In January 2015, Netflix announced that they were using React to power their UI development. Later that month, React Native, a library for building mobile applications using React, was released. Facebook also released ReactVR, another tool that brought React to a broader range of rendering targets. In 2015 and 2016, a huge number of popular tools like React Router, Redux, and Mobx came on the scene to handle tasks like routing and state management. After all, React was billed as a library: concerned with implementing a specific set of features, not providing a tool for every use case.

Another huge event on the timeline was the release of React Fiber in 2017. Fiber was a rewrite of React's rendering algorithm that was sort of magical in its execution. It was a full rewrite of React's internals that changed barely anything about the public API. It was a way of making React more modern and performant without affecting its users.

More recently in 2019, we saw the release of Hooks, a new way of adding and sharing stateful logic across components. We also saw the release of Suspense, a way to optimize asynchronous rendering with React.

In the future, we'll inevitably see more change, but one of the reasons for React's success is the strong team that has worked on the project over the years. The team is ambitious yet cautious, pushing forward-thinking optimizations while constantly considering the impact any changes to the library will send cascading through the community.

As changes are made to React and related tools, sometimes there are breaking changes. In fact, future versions of these tools may break some of the example code in this book. You can still follow along with the code samples. We'll provide exact version information in the package.json file so that you can install these packages at the correct version.

Beyond this book, you can stay on top of changes by following along with the official React blog. When new versions of React are released, the core team will write a detailed blog post and changelog about what's new. The blog has also been translated into an ever-expanding list of languages, so if English isn't your native language, you can find localized versions of the docs on the languages page of the docs site.

1-3『

所以官网的博客、社区要经常去看：

[Introducing Zero-Bundle-Size React Server Components – React Blog](https://reactjs.org/blog/2020/12/21/data-fetching-with-react-server-components.html)

[Where To Get Support – React](https://reactjs.org/community/support.html)

』

Learning React: Second Edition Changes

This is the second edition of Learning React. We felt it was important to update the book because React has evolved quite a bit over the past few years. We intend to focus on all the current best practices that are advocated by the React team, but we'll also share information about deprecated React features. There's a lot of React code that was written years ago using old styles that still works well and must be maintained.

In all cases, we'll make mention of these features in a sidebar in case you find yourself working with legacy React applications.

### 1.3 Working with the Files

In this section, we'll discuss how to work with the files for this book and how to install some useful React tools.

#### 1.3.1 File Repository

The GitHub repository associated with this book provides all the code files organized by chapter.

#### 1.3.2 React Developer Tools

We'd highly recommend installing React Developer Tools to support your work on React projects. These tools are available as a browser extension for Chrome and Firefox and as a standalone app for use with Safari, IE, and React Native. Once you install the dev tools, you'll be able to inspect the React component tree, view props and state details, and even view which sites are currently using React in production.

These are really useful when debugging and when learning about how React is used in other projects.

To install, head over to the GitHub repository. There, you'll find links to the Chrome and Firefox extensions.

Once installed, you'll be able to see which sites are using React.

Anytime the React icon is illuminated in the browser toolbar as shown in Figure 1-1, you'll know that the site has React on the page.

Figure 1-1. Viewing the React Developer Tools in Chrome Then, when you open the developer tools, there will be a new tab visible called React, as shown in Figure 1-2. Clicking on that will show all the components that make up the page you're currently viewing.

Figure 1-2. Inspecting the DOM with the React Developer Tools 

#### 1.3.3 Installing Node.js

Node.js is a JavaScript runtime environment used to build full-stack applications. Node is open source and can be installed on Windows, macOS, Linux, and other platforms. We'll be using Node in Chapter 12 when we build an Express server.

You need to have Node installed, but you do not need to be a Node expert in order to use React. If you're not sure if Node.js is installed on your machine, you can open a Terminal or Command Prompt window and type:

```
node -v
```

When you run this command, you should see a node version number returned to you, ideally 8.6.2 or higher. If you type the command and see an error message that says「Command not found,」Node.js is not installed. This is easily fixed by installing Node.js from the Node.js website. Just go through the installer's automated steps, and when you type in the node -v command again, you'll see the version number.

NPM

When you installed Node.js, you also installed npm, the Node package manager. In the JavaScript community, engineers share open source code projects to avoid having to rewrite frameworks, libraries, or helper functions on their own. React itself is an example of a useful npm library. We'll use npm to install a variety of packages throughout this book.

Most JavaScript projects you encounter today will contain an assorted collection of files plus a package.json file. This file describes the project and all its dependencies. If you run npm install in the folder that contains the package.json file, npm will install all the packages listed in the project.

If you're starting your own project from scratch and want to include dependencies, simply run the command:

```
npm init -y
```

This will initialize the project and create a package.json file. From there, you can install your own dependencies with npm. To install a package with npm, you'll run:

```
npm install package-name
```

To remove a package with npm, you'll run:

```
npm remove package-name
```

YARN

An alternative to npm is Yarn. It was released in 2016 by Facebook in collaboration with Exponent, Google, and Tilde. The project helps Facebook and other companies manage their dependencies reliably. If you're familiar with the npm workflow, getting up to speed with Yarn is fairly simple. First, install Yarn globally with npm:

```
npm install -g yarn
```

Then, you're ready to install packages. When installing dependencies from package.json, in place of npm install, you can run yarn.

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

Now that you have your environment set up for React development, you're ready to start walking the path of learning React. In Chapter 2, we'll get up to speed with the latest JavaScript syntax that's most commonly found in React code.

## 0201. JavaScript for React

Since its release in 1995, JavaScript has gone through many changes.

At first, we used JavaScript to add interactive elements to web pages: button clicks, hover states, form validation, etc.. Later, JavaScript got more robust with DHTML and AJAX. Today, with Node.js, JavaScript has become a real software language that's used to build full-stack applications. JavaScript is everywhere.

JavaScript's evolution has been guided by a group of individuals from companies that use JavaScript, browser vendors, and community leaders. The committee in charge of shepherding the changes to JavaScript over the years is the European Computer Manufacturers Association (ECMA). Changes to the language are community-driven, originating from proposals written by community members. Anyone can submit a proposal to the ECMA committee. The responsibility of the ECMA committee is to manage and prioritize these proposals to decide what's included in each spec.

The first release of ECMAScript was in 1997, ECMAScript1. This was followed in 1998 by ECMAScript2. ECMAScript3 came out in 1999, adding regular expressions, string handling, and more. The process of agreeing on an ECMAScript4 became a chaotic, political mess that proved to be impossible. It was never released. In 2009, ECMAScript5(ES5) was released, bringing features like new array methods, object properties, and library support for JSON.

Since then, there has been a lot more momentum in this space. After ES6 or ES2015 was released in, yes, 2015, there have been yearly releases of new JS features. Anything that's part of the stage proposals is typically called ESNext, which is a simplified way of saying this is the next stuff that will be part of the JavaScript spec.

Proposals are taken through clearly defined stages, from stage 0, which represents the newest proposals, up through stage 4, which represents the finished proposals. When a proposal gains traction, it's up to the browser vendors like Chrome and Firefox to implement the features.

Consider the const keyword. When creating variables, we used to use var in all cases. The ECMA committee decided there should be a const keyword to declare constants (more on that later in the chapter).

When const was first introduced, you couldn't just write const in JavaScript code and expect it to run in a browser. Now you can because browser vendors have changed the browser to support it.

Many of the features we'll discuss in this chapter are already supported by the newest browsers, but we'll also be covering how to compile your JavaScript code. This is the process of transforming new syntax that the browser doesn't recognize into older syntax that the browser understands. The kangax compatibility table is a great place to stay informed about the latest JavaScript features and their varying degrees of support by browsers.

In this chapter, we'll show you all the JavaScript syntax we'll be using throughout the book. We hope to provide a good baseline of JavaScript syntax knowledge that will carry you through all of your work with React. If you haven't made the switch to the latest syntax yet, now would be a good time to get started. If you're already comfortable with the latest language features, skip to the next chapter.

### 2.1 Declaring Variables

Prior to ES2015, the only way to declare a variable was with the var keyword. We now have a few different options that provide improved functionality.

#### 2.1.1 The const Keyword

A constant is a variable that cannot be overwritten. Once declared, you cannot change its value. A lot of the variables that we create in JavaScript should not be overwritten, so we'll be using const a lot.

Like other languages had done before it, JavaScript introduced constants with ES6. Before constants, all we had were variables, and variables could be overwritten:

```js
var pizza = true;
pizza = false;
console.log(pizza); // false
```

We cannot reset the value of a constant variable, and it will generate a console error (as shown in Figure 2-1) if we try to overwrite the value: 

```js
const pizza = true;
pizza = false;
```

Figure 2-1. An attempt at overwriting a constant

#### 2.1.2 The let Keyword

JavaScript now has lexical variable scope. In JavaScript, we create code blocks with curly braces (`{}`). In functions, these curly braces block off the scope of any variable declared with var. On the other hand, consider if/else statements. If you're coming from other languages, you might assume that these blocks would also block variable scope. This was not the case until let came along.

If a variable is created inside of an if/else block, that variable is not scoped to the block:

```js
var topic = "JavaScript";

if (topic) {
  var topic = "React";
  console.log("block", topic); // block React
}

console.log("global", topic); // global React 
```

The topic variable inside the if block resets the value of topic outside of the block. With the let keyword, we can scope a variable to any code block. Using let protects the value of the global variable:

```js
var topic = "JavaScript";

if (topic) {
  let topic = "React";
  console.log("block", topic); // React
}

console.log("global", topic); // JavaScript 
```

The value of topic is not reset outside of the block.

Another area where curly braces don't block off a variable's scope is in for loops:

```js
var div,
  container = document.getElementById("container"); 

for (var i = 0; i < 5; i++) {
  div = document.createElement("div");
  div.onclick = function() {
    alert("This is box #" + i);
  };
  container.appendChild(div);
}
```

In this loop, we create five divs to appear within a container. Each div is assigned an onclick handler that creates an alert box to display the index. Declaring i in the for loop creates a global variable named i, then iterates over it until its value reaches 5. When you click on any of these boxes, the alert says that i is equal to 5 for all divs, because the current value for the global i is 5 (see Figure 2-2).

Figure 2-2. i is equal to 5 for each box

Declaring the loop counter i with let instead of var does block off the scope of i. Now clicking on any box will display the value for i that was scoped to the loop iteration (see Figure 2-3): 

```js
const container = document.getElementById("container"); 
let div;

for (let i = 0; i < 5; i++) {
  div = document.createElement("div");
  div.onclick = function() {
    alert("This is box #: " + i);
  };
  container.appendChild(div);
}
```

Figure 2-3. The scope of i is protected with let

The scope of i is protected with let.

#### 2.1.3 Template Strings

Template strings provide us with an alternative to string concatenation. They also allow us to insert variables into a string. You'll hear these referred to as template strings, template literals, or string templates interchangeably.

Traditional string concatenation uses plus signs to compose a string using variable values and strings:

```js
console.log(lastName + ", " + firstName + " " + middleName); 
```

With a template, we can create one string and insert the variable values by surrounding them with `${ }`:

```js
console.log(`${lastName}, ${firstName} ${middleName}`);
```

Any JavaScript that returns a value can be added to a template string between the `${ }` in a template string. Template strings honor whitespace, making it easier to draft up email templates, code examples, or anything else that contains whitespace.

Now you can have a string that spans multiple lines without breaking your code:

```js
const email = `
Hello ${firstName},

Thanks for ordering ${qty} tickets to ${event}.

Order Details
${firstName} ${middleName} ${lastName}
  ${qty} x $${price} = $${qty*price} to ${event}

You can pick your tickets up 30 minutes before
the show.
Thanks,

${ticketAgent}
`
```

Previously, using an HTML string directly in our JavaScript code was not so easy to do because we'd need to run it together on one line. Now that the whitespace is recognized as text, you can insert formatted HTML that is easy to read and understand:

```js
document.body.innerHTML = `
<section>
  <header>
    <h1>The React Blog</h1>
  </header>
  <article>
    <h2>${article.title}</h2>
    ${article.body}
  </article>
  <footer>
    <p>copyright ${new Date().getYear()} | The React Blog</p>
  </footer>
</section>
`;
```

Notice that we can include variables for the page title and article text as well.

### 2.2 Creating Functions

Any time you want to perform some sort of repeatable task with JavaScript, you can use a function. Let's take a look at some of the different syntax options that can be used to create a function and the anatomy of those functions.

#### 2.2.1 Function Declarations

A function declaration or function definition starts with the function keyword, which is followed by the name of the function, logCompliment. The JavaScript statements that are part of the function are defined between the curly braces:

```js
function logCompliment() {
  console.log("You're doing great!");
}
```

Once you've declared the function, you'll invoke or call it to see it execute:

```js
function logCompliment() {
console.log("You're doing great!");
}

logCompliment();
```

Once invoked, you'll see the compliment logged to the console.

#### 2.2.2 Function Expressions

Another option is to use a function expression. This just involves creating the function as a variable:

```js
const logCompliment = function() {
  console.log("You're doing great!");
};

logCompliment();
```

The result is the same, and You're doing great! is logged to the console.

One thing to be aware of when deciding between a function declaration and a function expression is that function declarations are hoisted and function expressions are not. In other words, you can invoke a function before you write a function declaration. You cannot invoke a function created by a function expression. This will cause an error. For example:

2『函数申明和函数表达式创建函数对象的区别，做一张信息数据卡片。（2021-04-29）』 —  —  已完成

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

#### 2.2.3 Passing Arguments

The logCompliment function currently takes in no arguments or parameters. If we want to provide dynamic variables to the function, we can pass named parameters to a function simply by adding them to the parentheses. Let's start by adding a firstName variable: 

```js
const logCompliment = function(firstName) {
  console.log(`You're doing great, ${firstName}`);
};
logCompliment("Molly");
```

Now when we call the logCompliment function, the firstName value sent will be added to the console message. We could add to this a bit by creating another argument called message. Now, we won't hard-code the message. We'll pass in a dynamic value as a parameter:

```js
const logCompliment = function(firstName, message) {
  console.log(`${firstName}: ${message}`);
};
logCompliment("Molly", "You're so cool"); 
```

#### 2.2.4 Function Returns

The logCompliment function currently logs the compliment to the console, but more often, we'll use a function to return a value. Let's add a return statement to this function. A return statement specifies the value returned by the function. We'll rename the function createCompliment:

```js
const createCompliment = function(firstName, message) {
  return `${firstName}: ${message}`;
};
createCompliment("Molly", "You're so cool"); 
```

If you wanted to check to see if the function is executing as expected, just wrap the function call in a console.log:

```js
console.log(createCompliment("You're so cool", "Molly")); 
```

#### 2.2.5 Default Parameters

Languages including C++ and Python allow developers to declare default values for function arguments. Default parameters are included in the ES6 spec, so in the event that a value is not provided for the argument, the default value will be used. For example, we can set up default strings for the parameters name and activity:

```js
function logActivity(name = "Shane McConkey", activity = "skiing") {
  console.log(`${name} loves ${activity}`);
}
```

If no arguments are provided to the logActivity function, it will run correctly using the default values. Default arguments can be any type, not just strings:

```jsconst defaultPerson = {
  name: {
    first: "Shane",
    last: "McConkey"
  },
  favActivity: "skiing"
};
  
function logActivity(person = defaultPerson) {
  console.log(`${person.name.first} loves ${person.favActivity}`);
}
```

1『函数的默认参数也能是对象，赞。（2021-04-29）』

#### 2.2.6 Arrow Functions

Arrow functions are a useful new feature of ES6. With arrow functions, you can create functions without using the function keyword. You also often do not have to use the return keyword. Let's consider a function that takes in a firstName and returns a string, turning the person into a lord. Anyone can be a lord:

```js
const lordify = function(firstName) {
  return `${firstName} of Canterbury`;
};

console.log(lordify("Dale")); // Dale of Canterbury 
console.log(lordify("Gail")); // Gail of Canterbury 
```

With an arrow function, we can simplify the syntax tremendously: 

```js
const lordify = firstName => `${firstName} of Canterbury`; 
```

With the arrow, we now have an entire function declaration on one line. The function keyword is removed. We also remove return because the arrow points to what should be returned. Another benefit is that if the function only takes one argument, we can remove the parentheses around the arguments. More than one argument should be surrounded by parentheses:

```js
// Typical function
const lordify = function(firstName, land) {
  return `${firstName} of ${land}`;
};

// Arrow Function
const lordify = (firstName, land) => `${firstName} of ${land}`; 
console.log(lordify("Don", "Piscataway")); // Don of Piscataway 
console.log(lordify("Todd", "Schenectady")); // Todd of Schenectady 
```

We can keep this as a one-line function because there is only one statement that needs to be returned. If there are multiple lines, you'll use curly braces:

```js
const lordify = (firstName, land) => {
  if (!firstName) {
    throw new Error("A firstName is required to lordify");
  }
  if (!land) {
    throw new Error("A lord must have a land");
  }
  return `${firstName} of ${land}`;
};
  
console.log(lordify("Kelly", "Sonoma")); // Kelly of Sonoma 
console.log(lordify("Dave")); // ! JAVASCRIPT ERROR
```

These if/else statements are surrounded with brackets but still benefit from the shorter syntax of the arrow function.

#### 2.2.7 Return Objects

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

1『解惑了解惑了，很多地方看到了这种语句，箭头函数返回对象，做一张信息数据卡片。（2021-04-29）』 —  —  已完成

#### 2.2.8 Arrow Function And Scope

Regular functions do not block this. For example, this becomes something else in the setTimeout callback, not the tahoe object: 

```js
const tahoe = {
  mountains: ["Freel", "Rose", "Tallac", "Rubicon", "Silver"], 
  print: function(delay = 1000) {
    setTimeout(function() {
      console.log(this.mountains.join(", "));
    }, delay);
  }
};
  
tahoe.print(); // Uncaught TypeError: Cannot read property 'join' of undefined
```

This error is thrown because it's trying to use the .join method on what this is. If we log this, we'll see that it refers to the Window object:

```js
console.log(this); // Window {}
```

To solve this problem, we can use the arrow function syntax to protect the scope of this:

```js
const tahoe = {
  mountains: ["Freel", "Rose", "Tallac", "Rubicon", "Silver"], 
  print: function(delay = 1000) {
    setTimeout(() => {
      console.log(this.mountains.join(", "));
    }, delay);
  }
};
  
tahoe.print(); // Freel, Rose, Tallac, Rubicon, Silver 
```

This works as expected, and we can .join the resorts with a comma. Be careful that you're always keeping scope in mind. Arrow functions do not block off the scope of this:

```js
const tahoe = {
  mountains: ["Freel", "Rose", "Tallac", "Rubicon", "Silver"], 
  print: (delay = 1000) => {
    setTimeout(() => {
      console.log(this.mountains.join(", "));
    }, delay);
  }
};
  
tahoe.print(); // Uncaught TypeError: Cannot read property 'join' of undefined
```

Changing the print function to an arrow function means that this is actually the window.

1-2-3『这里的知识点跟目前脑子的里的知识关联上了，箭头函数 this 值总是指向全局对象 window，但第二个、第三个例子放在一起目前就糊涂了，this 不是应该都可以指向 window 么。待研究。（2021-04-29）』 —  —  未完成

### 2.3 Compiling JavaScript

When a new JavaScript feature is proposed and gains support, the community often wants to use it before it's supported by all browsers. The only way to be sure that your code will work is to convert it to more widely compatible code before running it in the browser. This process is called compiling. One of the most popular tools for JavaScript compilation is Babel.

In the past, the only way to use the latest JavaScript features was to wait weeks, months, or even years until browsers supported them. Now, Babel has made it possible to use the latest features of JavaScript right away. The compiling step makes JavaScript similar to other languages. It's not quite traditional compiling: our code isn't compiled to binary. Instead, it's transformed into syntax that can be interpreted by a wider range of browsers. Also, JavaScript now has source code, meaning that there will be some files that belong to your project that don't run in the browser.

As an example, let's look at an arrow function with some default arguments:

```js
const add = (x = 5, y = 10) => console.log(x + y);
```

If we run Babel on this code, it will generate the following:

```js
"use strict";

var add = function add() {
  var x =
    arguments.length <= 0 || arguments[0] === undefined ? 5 : arguments[0];
  var y =
    arguments.length <= 1 || arguments[1] === undefined ? 10 : arguments[1];
  return console.log(x + y);
};
```


Babel added a "use strict" declaration to run in strict mode. The variables x and y are defaulted using the arguments array, a technique you may be familiar with. The resulting JavaScript is more widely supported. A great way to learn more about how Babel works is to check out the Babel REPL on the documentation website. Type some new syntax on the left side, then see some older syntax created.

3『 [Babel · The compiler for next generation JavaScript](https://babeljs.io/repl) 』

The process of JavaScript compilation is typically automated by a build tool like webpack or Parcel. We'll discuss that in more detail later in the book.

### 2.4 Objects and Arrays

Since ES2016, JavaScript syntax has supported creative ways of scoping variables within objects and arrays. These creative techniques are widely used among the React community. Let's take a look at a few of them, including destructuring, object literal enhancement, and the spread operator.

#### 2.4.1 Destructuring Objects

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

2『解构对象，做一张主题卡片。（2021-04-29）』 —  —  已完成

#### 2.4.2 Destructuring Arrays

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

2『解构数组，做一张主题卡片。（2021-04-29）』 —  —  已完成

#### 2.4.3 Object Literal Enhancement

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

2『对象强化，做一张主题卡片。（2021-04-29）』 —  —  已完成

#### 2.4.4 The Spread Operator

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

2『spread operator，做一张主题卡片。（2021-04-29）』 —  —  已完成

### 2.5 Asynchronous JavaScript

The code samples that have been part of this chapter so far have been synchronous. When we write synchronous JavaScript code, we're providing a list of instructions that execute immediately in order. For example, if we wanted to use JavaScript to handle some simple DOM manipulation, we'd write the code to do so like this:

```js
const header = document.getElementById("heading"); 
header.innerHTML = "Hey!";
```

These are instructions.「Yo, go select that element with an id of heading. Then when you're done with that, how about you set that inner HTML to Hey.」It works synchronously. While each operation is happening, nothing else is happening.

With the modern web, we need to perform asynchronous tasks. These tasks often have to wait for some work to finish before they can be completed. We might need to access a database. We might need to stream video or audio content. We might need to fetch data from an API. With JavaScript, asynchronous tasks do not block the main thread. JavaScript is free to do something else while we wait for the API to return data. JavaScript has evolved a lot over the past few years to make handling these asynchronous actions easier. Let's explore some of the features that make this possible.

#### 2.5.1 Simple Promises with Fetch

Making a request to a REST API used to be pretty cumbersome. We'd have to write 20+ lines of nested code just to load some data into our app. Then the fetch() function showed up and simplified our lives. Thanks to the ECMAScript committee for making fetch happen.

Let's get some data from the randomuser.me API. This API has information like email address, name, phone number, location, and so on for fake members and is great to use as dummy data. fetch takes in the URL for this resource as its only parameter:

```js
console.log(fetch("https://api.randomuser.me/?nat=US&results=1")); 
```

When we log this, we see that there is a pending promise. Promises give us a way to make sense out of asynchronous behavior in JavaScript. The promise is an object that represents whether the async operation is pending, has been completed, or has failed. Think of this like the browser saying,「Hey, I'm going to try my best to go get this data. Either way, I'll come back and let you know how it went.」

So back to the fetch result. The pending promise represents a state before the data has been fetched. We need to chain on a function called `.then()`. This function will take in a callback function that will run if the previous operation was successful. In other words, fetch some data, then do something else.

The something else we want to do is turn the response into JSON: 

```js
fetch("https://api.randomuser.me/?nat=US&results=1").then(res => 
  console.log(res.json())
);
```

The then method will invoke the callback function once the promise has resolved. Whatever you return from this function becomes the argument of the next then function. So we can chain together then functions to handle a promise that has been successfully resolved: 

```js
fetch("https://api.randomuser.me/?nat=US&results=1")
  .then(res => res.json())
  .then(json => json.results)
  .then(console.log)
  .catch(console.error);
```

First, we use fetch to make a GET request to randomuser.me. If the request is successful, we'll then convert the response body to JSON.

Next, we'll take the JSON data and return the results, then we'll send the results to the console.log function, which will log them to the console. 

Finally, there is a catch function that invokes a callback if the fetch did not resolve successfully. Any error that occurred while fetching data from randomuser.me will be based on that callback. Here, we simply log the error to the console using console.error.

#### 2.5.2 Async/Await

Another popular approach for handling promises is to create an async function. Some developers prefer the syntax of async functions because it looks more familiar, like code that's found in a synchronous function. Instead of waiting for the results of a promise to resolve and handling it with a chain of then functions, async functions can be told to wait for the promise to resolve before further executing any code found in the function.

Let's make another API request but wrap the functionality with an async function:

```js
const getFakePerson = async () => {
  let res = await fetch("https://api.randomuser.me/?nat=US&results=1"); 
  let { results } = res.json();
  console.log(results);
};
  
getFakePerson();
```

Notice that the getFakePerson function is declared using the async keyword. This makes it an asynchronous function that can wait for promises to resolve before executing the code any further. The await keyword is used before promise calls. This tells the function to wait for the promise to resolve. This code accomplishes the exact same task as the code in the previous section that uses then functions. Well, almost the exact same task…

```js
const getFakePerson = async () => {
  try {
    let res = await fetch("https://api.randomuser.me/?nat=US&results=1"); 
    let { results } = res.json();
    console.log(results); 
  } catch (error) {
    console.error(error); 
  }
};
getFakePerson();
```

There we go — now this code accomplishes the exact same task as the code in the previous section that uses then functions. If the fetch call is successful, the results are logged to the console. If it's unsuccessful, then we'll log the error to the console using console.error. When

using async and await, you need to surround your promise call in a try…catch block to handle any errors that may occur due to an unresolved promise.

#### 2.5.3 Building Promises

When making an asynchronous request, one of two things can happen: everything goes as we hope, or there's an error. There can be many different types of successful or unsuccessful requests. For example, we could try several ways to obtain the data to reach success. We could also receive multiple types of errors. Promises give us a way to simplify back to a simple pass or fail.

The getPeople function returns a new promise. The promise makes a request to the API. If the promise is successful, the data will load. If the promise is unsuccessful, an error will occur:

```js
const getPeople = count =>
  new Promise((resolves, rejects) => {
    const api = `https://api.randomuser.me/?nat=US&results=${count}`; 
    const request = new XMLHttpRequest();
    request.open("GET", api);
    request.onload = () =>
      request.status === 200
        ? resolves(JSON.parse(request.response).results)
        : reject(Error(request.statusText));
    request.onerror = err => rejects(err);
    request.send();
});
```

With that, the promise has been created, but it hasn't been used yet. We can use the promise by calling the getPeople function and passing in the number of members that should be loaded. The then function can be chained on to do something once the promise has been fulfilled.

When a promise is rejected, any details are passed back to the catch function, or the catch block if using async/await syntax: 

```js
getPeople(5)
  .then(members => console.log(members))
  . catch(error => console.error(`getPeople failed: ${error.message}`))
```

Promises make dealing with asynchronous requests easier, which is good, because we have to deal with a lot of asynchronicity in JavaScript. A solid understanding of asynchronous behavior is essential for the modern JavaScript engineer.

### 2.6 Classes

Prior to ES2015, there was no official class syntax in the JavaScript spec. When classes were introduced, there was a lot of excitement about how similar the syntax of classes was to traditional object-oriented languages like Java and C++. The past few years saw the React library leaning on classes heavily to construct user interface components. Today, React is beginning to move away from classes, instead using functions to construct components. You'll still see classes all over the place, particularly in legacy React code and in the world of JavaScript, so let's take a quick look at them.

JavaScript uses something called prototypical inheritance. This technique can be wielded to create structures that feel object-oriented. For example, we can create a Vacation constructor that needs to be invoked with a new operator:

```js
function Vacation(destination, length) {
  this.destination = destination;
  this.length = length;
}
  
Vacation.prototype.print = function() {
  console.log(this.destination + " | " + this.length + " days");
};

const maui = new Vacation("Maui", 7); maui.print(); // Maui | 7 days
```

This code creates something that feels like a custom type in an object-oriented language. A Vacation has properties (destination, length), and it has a method (print). The maui instance inherits the print method through the prototype. If you are or were a developer accustomed to more standard classes, this might fill you with a deep rage. ES2015 introduced class declaration to quiet that rage, but the dirty secret is that JavaScript still works the same way. Functions are objects, and inheritance is handled through the prototype. Classes provide a syntactic sugar on top of that gnarly prototype syntax:

```js
class Vacation {
  constructor(destination, length) {
    this.destination = destination;
    this.length = length;
  }
  
  print() {
    console.log(`${this.destination} will take ${this.length} days.`);
  }  
}
```

When you're creating a class, the class name is typically capitalized. Once you've created the class, you can create a new instance of the class using the new keyword. Then you can call the custom method on the class:

```js
const trip = new Vacation("Santiago, Chile", 7); 
trip.print(); // Chile will take 7 days.
```

Now that a class object has been created, you can use it as many times as you'd like to create new vacation instances. Classes can also be extended. When a class is extended, the subclass inherits the properties and methods of the superclass. These properties and methods can be manipulated from here, but as a default, all will be inherited.

You can use Vacation as an abstract class to create different types of vacations. For instance, an Expedition can extend the Vacation class to include gear:

```js
class Expedition extends Vacation {
  constructor(destination, length, gear) {
    super(destination, length);
    this.gear = gear;
  }
  
  print() {
    super.print();
    console.log(`Bring your ${this.gear.join(" and your ")}`);
  }
}
```

That's simple inheritance: the subclass inherits the properties of the superclass. By calling the print method of Vacation, we can append some new content onto what is printed in the print method of Expedition. Creating a new instance works the exact same way — create a variable and use the new keyword:

```js
const trip = new Expedition("Mt. Whitney", 3, [
  "sunglasses",
  "prayer flags",
  "camera"
]);
  
trip.print();
// Mt. Whitney will take 3 days.
// Bring your sunglasses and your prayer flags and your camera 
```

### 2.7 ES6 Modules

A JavaScript module is a piece of reusable code that can easily be incorporated into other JavaScript files without causing variable collisions. JavaScript modules are stored in separate files, one file per module. There are two options when creating and exporting a module: you can export multiple JavaScript objects from a single module or one JavaScript object per module.

In text-helpers.js, two functions are exported:

```js
export const print=(message) => log(message, new Date()) 
export const log=(message, timestamp) => 
  console.log(`${timestamp.toString()}: ${message}`)
```

export can be used to export any JavaScript type that will be consumed in another module. In this example, the print function and log function are being exported. Any other variables declared in text-helpers.js will be local to that module.

Modules can also export a single main variable. In these cases, you can use export default. For example, the mt-freel.js file can export a specific expedition:

```js
export default new Expedition("Mt. Freel", 2, ["water", "snack"]); 
```

export default can be used in place of export when you wish to export only one type. Again, both export and export default can be used on any JavaScript type: primitives, objects, arrays, and functions.

Modules can be consumed in other JavaScript files using the import statement. Modules with multiple exports can take advantage of object destructuring. Modules that use export default are imported into a single variable:

```js
import { print, log } from "./text-helpers"; 
import freel from "./mt-freel";
print("printing a message");
log("logging a message");
freel.print();
```

You can scope module variables locally under different variable names:

```js
import { print as p, log as l } from "./text-helpers"; 
p("printing a message");
l("logging a message");
```

You can also import everything into a single variable using `*`: 

```js
import * as fns from './text-helpers`
```

This import and export syntax is not yet fully supported by all browsers or by Node. However, like any emerging JavaScript syntax, it's supported by Babel. This means you can use these statements in your source code and Babel will know where to find the modules you want to include in your compiled JavaScript.

#### 2.7.1 CommonJS

CommonJS is the module pattern that's supported by all versions of Node (see the Node.js documentation on modules). You can still use these modules with Babel and webpack. With CommonJS, JavaScript objects are exported using module.exports.

For example, in CommonJS, we can export the print and log functions as an object:

```js
const print(message) => log(message, new Date()) 
const log(message, timestamp) =>
  console.log(`${timestamp.toString()}: ${message}`}
module.exports = {print, log}
```

CommonJS does not support an import statement. Instead, modules are imported with the require function:

```js
const { log, print } = require("./txt-helpers"); 
```

JavaScript is indeed moving quickly and adapting to the increasing demands that engineers are placing on the language, and browsers are quickly implementing new features. For up-to-date compatibility information, see the ESNext compatibility table. Many of the features that are included in the latest JavaScript syntax are present because they support functional programming techniques. In functional JavaScript, we can think of our code as being a collection of functions that can be composed into applications. In the next chapter, we'll explore functional techniques in more detail and will discuss why you might want to use them.

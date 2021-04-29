## 记忆时间

## 目录

2021060Learning-React0101.md

## 2021060Learning-React0101.md

### 0101. Welcome to React

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

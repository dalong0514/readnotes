## 记忆时间

## 卡片

### 0101. 主题卡 —— 如何用 vue-router 搭建单页应用

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0102. 主题卡 —— 如何用 vuex 搭建数据中心 store

### 0201. 术语卡 —— SPA

Most websites are broken up into pages in order to make the information they contain easier to consume. Traditionally this is done with a server/client model, where each page must be loaded from the server with a different URL. To navigate to a new page, the browser must send a request to the URL of that page. The server will send the data back and the browser can unload the existing page and load the new one. For the average internet connection, this process will likely take a few seconds, during which the user must wait for the new page to load.

By using a powerful frontend framework and an AJAX utility, a different model is possible: the browser can load an initial web page, but navigating to new pages will not require the browser to unload the page and load a new one. Instead, any data required for new pages can be loaded asynchronously with AJAX. From a user's perspective, such a website would appear to have pages just like any other, but from a technical perspective, this site really only has one page. Hence the name, Single-Page Application (SPA).

The advantage of the Single-Page Application architecture is that it can create a more seamless experience for the user. Data for new pages must still be retrieved, and will therefore create some small disruption to the user's flow, but this disruption is minimized since the data retrieval can be done asynchronously and JavaScript can continue to run. Also, since SPA pages usually require less data due to the reuse of some page elements, page loading is quicker.

The disadvantage of the SPA architecture is that it makes the client app bulkier due to the added functionality, so gains from speeding up page changes may be negated by the fact that the user must download a large app on the first page load. Also, handling routes adds complexity to the app as multiple states must be managed, URLs must be handled, and a lot of default browser functionality must be recreated in the app.

### 0202. 术语卡 —— Routers

If you are going with an SPA architecture and your app design includes multiple pages, you'll want to use a router. A router, in this context, is a library that will mimic browser navigation through JavaScript and various native APIs so that the user gets an experience similar to that of a traditional multi-page app. Routers will typically include functionality to: 1) Handle navigation actions from within the page. 2) Match parts of the application to routes. 3) Manage the address bar. 4) Manage the browser history. 5) Manage scroll bar behavior.

### 0203. 术语卡 —— 组件里的 props

发现一个很好的类比，函数。组件是 html 里的自定义标签，把标签当一个函数来看，标签的属性名称（对应于 props）就好比是这个函数的形参，其声明是在组件定义里的 props 属性里，是个列表对象。实参是这个标签里实际传递给组件的对象，最关键的是这个对象可以是 vue 实例里的数据对象（数据或方法）。

```html
<my-component :title="dalong"></my-component>
```

上面的例子里，title 是 props，dalong 是传递给这个组件的数据对象。注意 title 需要绑定一下。

### 0204. 术语卡 —— watcher

如何对跟 vue 实例平行的节点操作，还是得靠 DOM 的 API，但前提是 vue 能告知 DOM 相关信息，watcher 就是做这个的。

Vue 实例里增加 watch 方法调用浏览器的 API 从而操作与 vue 实例同级别的 DOM 节点。

```js
    watch: {
        modalOpen: function() {
            var className = "modal-open";
            if (this.modalOpen) {
                document.body.classList.add(className);
            } else {
                document.body.classList.remove(className);
            }
        },
    },
```

### 0205. 术语卡 —— Flux application architecture

Flux is not a library. You can't go to GitHub and download it. Flux is a set of guiding principles that describe a scalable frontend architecture that sufficiently mitigates this flaw. It is not just for a chat app, but for any complex UI with components which share state, like Vuebnb. Let's now explore the guiding principles of Flux.

Principle #1 – Single source of truth

Components may have local data that only they need to know about. For example, the position of the scroll bar in the user list component is probably of no interest to other components:

But any data that is to be shared between components, for example application data, needs to be kept in a single place, separate from the components that use it. This location is referred to as the store. Components must read application data from this location and not keep their own copy to prevent conflict or disagreement:

Principle #2 – Data is read-only

Components can freely read data from the store. But they cannot change data in the store, at least not directly. Instead, they must inform the store of their intent to change the data and the store will be responsible for making those changes via a set of defined functions called mutator methods.

Why this approach? If we centralize the data-altering logic then we don't have to look far if there are inconsistencies in the state. We're minimizing the possibility that some random component (possibly in a third party module) has changed the data in an unexpected fashion.

Principle #3 – Mutations are synchronous

It's much easier to debug state inconsistencies in an app that implements the above two principles in its architecture. You could log commits and observe how the state changes in response (which automatically happens with Vue Devtools, as we'll see).

But this ability would be undermined if our mutations were applied asynchronously. We'd know the order our commits came in, but we would not know the order in which our components committed them. Synchronous mutations ensure state is not dependent on the sequence and timing of unpredictable events.

### 0206. 术语卡 —— AJAX

AJAX 即 Asynchronous JavaScript and XML（非同步的 JavaScript 与 XML 技术），指的是一套综合了多项技术的浏览器端网页开发技术。Ajax 的概念由杰西·詹姆士·贾瑞特所提出。

传统的 Web 应用允许用户端填写表单（form），当送出表单时就向网页服务器发送一个请求。服务器接收并处理传来的表单，然后送回一个新的网页，但这个做法浪费了许多带宽，因为在前后两个页面中的大部分 HTML 码往往是相同的。由于每次应用的沟通都需要向服务器发送请求，应用的回应时间依赖于服务器的回应时间。这导致了用户界面的回应比本机应用慢得多。

与此不同，AJAX 应用可以仅向服务器发送并取回必须的数据，并在客户端采用 JavaScript 处理来自服务器的回应。因为在服务器和浏览器之间交换的数据大量减少，服务器回应更快了。同时，很多的处理工作可以在发出请求的客户端机器上完成，因此 Web 服务器的负荷也减少了。

类似于 DHTML 或 LAMP，AJAX 不是指一种单一的技术，而是有机地利用了一系列相关的技术。虽然其名称包含 XML，但实际上数据格式可以由 JSON 代替，进一步减少数据量，形成所谓的 AJAJ。而客户端与服务器也并不需要异步。一些基于 AJAX 的「派生／合成」式（derivative / composite）的技术也正在出现，如 AFLAX。

## 总体

Copyright © 2017 Packt Publishing

[Vuebnb](http://vuebnb.vuejsdevelopers.com/)

### Book Description

Vue is a JavaScript framework that can be used for anything from simple data display to sophisticated front-end applications and Laravel is a PHP framework used for developing fast and secure web-sites. This book gives you practical knowledge of building modern full-stack web apps from scratch using Vue with a Laravel back end.

In this book, you will build a room-booking website named "Vuebnb". This project will show you the core features of Vue, Laravel and other state-of-the-art web development tools and techniques. The book begins with a thorough introduction to Vue.js and its core concepts like data binding, directives and computed properties, with each concept being explained first, then put into practice in the case-study project.

You will then use Laravel to set up a web service and integrate the front end into a full-stack app. You will be shown a best-practice development workflow using tools like Webpack and Laravel Mix. With the basics covered, you will learn how sophisticated UI features can be added using ES+ syntax and a component-based architecture. You will use Vue Router to make the app multi-page and Vuex to manage application state.

Finally, you will learn how to use Laravel Passport for authenticated AJAX requests between Vue and the API, completing the full-stack architecture. Vuebnb will then be prepared for production and deployed to a free Heroku cloud server.

### Preface

The year is 2014 and the war of Single-Page Application (SPA) solutions is truly raging. There are many rivals: Angular, React, Ember, Knockout, and Backbone, to name but a few. However, the battle being most closely watched is between Google's Angular and Facebook's React.

1『原来 Angular 是 Google 的，而 React 是 Facebook 的。』

Angular, the SPA king until this point, is a full-fledged framework that follows the familiar MVC paradigm. React, the unlikely challenger seems quite odd in comparison with its core library only dealing with the view layer and markup written entirely in JavaScript! While Angular holds the bigger market share, React has caused a seismic shift in how developers think about web application design and has raised the bar on framework size and performance.

Meanwhile, a developer named Evan You was experimenting with his own new framework, Vue.js. It would combine the best features of Angular and React to achieve a perfect balance between simplicity and power. Your vision would resonate so well with other developers that Vue would soon be among the most popular SPA solutions.

Despite the fierce competition, Vue gained traction quickly. This was partly thanks to Taylor Otwell, the creator of Laravel, who tweeted in early 2015 about how impressed he was with Vue. This tweet generated a lot of interest in Vue from the Laravel community.

The partnership of Vue and Laravel would become further entwined with the release of Laravel version 5.3 in September 2016, when Vue was included as a default frontend library. This was a perfectly logical alliance for two software projects with the same philosophy: simplicity and an emphasis on the developer experience.

Today, Vue and Laravel offer an immensely powerful and flexible full-stack framework for developing web applications, and as you'll find throughout this book, they're a real treat to work with.

### What this book covers

Building a full-stack app requires a wide variety of knowledge, not just about Vue and Laravel, but also Vue Router, Vuex, and Webpack, not to mention JavaScript, PHP, and web development in general. As such, one of the biggest challenges for me as the author was deciding what should and shouldn't be included. The topics I ultimately settled upon arose as answers to one of the two following questions: 1) What are the essential features, tools, and design patterns that the reader will use in all, or most, of their Vue.js apps? 2) What are the key issues of designing and building full-stack Vue.js apps as opposed to other architectures?

Here's how the chosen topics are distributed across the chapters of the book:

Chapter 1, Hello Vue - An Introduction to Vue.js, presents an overview of Vue.js, and the book's case-study project, Vuebnb.

Chapter 2, Prototyping Vuebnb, Your First Vue.js Project, provides a practical introduction to the essential features of Vue.js, including installation, template syntax, directives, lifecycle hooks and so on.

Chapter 3, Setting Up a Laravel Development Environment, shows how to set up a new Laravel project for inclusion in a full-stack Vue.js app.

Chapter 4, Building a Web Service with Laravel, is about laying the foundations of the backend of our case-study project, by setting up the database, models, and API endpoints.

Chapter 5, Integrating Laravel and Vue.js with Webpack, explains how a sophisticated Vue app will require a build step, and introduces Webpack for bundling project assets.

1『 vue 和 laravel 是通过 Webpack 集成在一起的。』

Chapter 6, Composing Widgets with Vue.js Components, teaches how components are an essential concept of modern UI development and one of the most powerful features of Vue.js.

Chapter 7, Building a Multi-Page App with Vue Router, introduces Vue Router and shows how we can add virtual pages to a frontend app.

Chapter 8, Managing Your Application State with Vuex, explains how state management is a must-have feature for managing complex UI data. We introduce the Flux pattern and Vuex.

Chapter 9, Adding a User Login and API Authentication With Passport, focuses on one of the trickiest aspects of full-stack apps—authentication. This chapter shows how to use Passport for secure AJAX calls to the backend.

Chapter 10, Deploying a Full-Stack App to the Cloud, describes how to build and deploy our completed project to a cloud-based server and use a CDN for serving static assets.

What you will learn? 1) Core features of Vue.js to create sophisticated user interfaces. 2) Build a secure backend API with Laravel. 3) Learn a state-of-the-art web development workflow with Webpack. 4) Full-stack app design principles and best practices. 5) Learn to deploy a full-stack app to a cloud server and CDN. 6) Managing complex application state with Vuex. 7) Securing a web service with Laravel Passport.

2『已下载书籍源码「2020121Full-Stack-Vue.js-2-and-Laravel-5源码」。github 上发现作者还有另外 3 本书「Vue.js Design Patterns and Best Practices」、「Vue.js 2.x by Example」和「Vue.js 2 Web Development Projects」。顺藤摸瓜，找到出版社的书籍源码集合：[Packt](https://github.com/PacktPublishing)。』

## 0101. Hello Vue – An Introduction to Vue.js

Topics this chapter covers: 1) Basic features of Vue, including templates, directives, and components. 2) Advanced features of Vue including single-file components and server-side rendering. 3) Tools in the Vue ecosystem including Vue Devtools, Vue Router, and Vuex. 4) The main case-study project that you'll be building as you progress through the book, Vuebnb. 5) Instructions for installing the project code.

### Summary

In this first chapter, we did a high-level introduction to Vue.js, covering the basic features such as templates, directives, and components, as well as advanced features such as single-file components and server-side rendering. We also had a look at the tools in Vue's ecosystem including Vue Router and Vuex. We then did an overview of Vuebnb, the full-stack project that you'll be building as you progress through the book, and saw how to install the code base from GitHub. In the next chapter, we'll get properly acquainted with Vue's basic features and starting putting them to use by building a prototype of Vuebnb.

### 1.1 Introducing Vue.js

At the time of writing in late 2017, Vue.js is at version 2.5. In less than four years from its first release, Vue has become one of the most popular open source projects on GitHub. This popularity is partly due to its powerful features, but also to its emphasis on developer experience and ease of adoption.

The core library of Vue.js, like React, is only for manipulating the view layer from the MVC architectural pattern. However, Vue has two official supporting libraries, Vue Router and Vuex, responsible for routing and data management respectively.

Vue is not supported by a tech giant in the way that React and Angular are and relies on donations from a small number of corporate patrons and dedicated Vue users. Even more impressively, Evan You is currently the only full-time Vue developer, though a core team of 20 more developers from around the world assist with development, maintenance, and documentation.

The key design principles of Vue are as follows: 1) Focus: Vue has opted for a small, focused API, and its sole purpose is the creation of UIs. 2) Simplicity: Vue's syntax is terse and easy to follow. 3) Compactness: The core library script is ~25 KB minified, making it smaller than React and even jQuery. 4) Speed: Rendering benchmarks beat many of the main frameworks, including React. 5) Versatility: Vue works well for small jobs where you might normally use jQuery, but can scale up as a legitimate SPA solution.

### 1.4 Templates

By default, Vue will use an HTML file for its template. An included script will declare an instance of Vue and use the el property in the configuration object to tell Vue where in the template the app will be mounted:

```js
<div id="app">
    <!--Vue has dominion within this node--> 
</div> 
<script> 
    new Vue({ el: '#app' }); 
</script>
```

We can bind data to our template by creating it as a data property and using the mustache syntax to print it in the page:

```js
<div id="app"> 
    {{ message }} 
    <!--Renders as "Hello World"--> 
</div> 
<script> 
    new Vue({ 
        el: '#app', 
        data: { message: 'Hello World' } 
    }); 
</script>
```

### 1.5 Directives

Similar to Angular, we can add functionality to our templates by using directives. These are special properties we add to HTML tags starting with the v- prefix. Say we have an array of data. We can render this data to the page as sequential HTML elements by using the v-for directive:

```js
<div id="app"> 
    <h3>Grocery list</h3> 
    <ul> 
        <li v-for="grocery in groceries">{{ grocery }}</li> 
    </ul> 
</div> 
<script> 
    var app = new Vue({ 
        el: '#app', 
        data: { 
            groceries: [ 'Bread', 'Milk' ] 
        } 
    }); 
</script>
```

The preceding code renders as follows:

```html
<div id="app"> 
    <h3>Grocery list</h3> 
    <ul> 
        <li>Bread</li> 
        <li>Milk</li> 
    </ul> 
</div>
```

### 1.6 Reactivity

A key feature of Vue's design is its reactivity system. When you modify data, the view automatically updates to reflect that change. For example, if we create a function that pushes another item to our array of grocery items after the page has already been rendered, the page will automatically re-render to reflect that change:

```js
setTimeout(function() { 
    app.groceries.push('Apples'); 
}, 2000);
```

Two seconds after the initial rendering, we see this:

```html
<div id="app"> 
    <h3>Grocery list</h3> 
    <ul> 
        <li>Bread</li> 
        <li>Milk</li> 
        <li>Apples</li> 
    </ul> 
</div>
```

### 1.7 Components

Components extend basic HTML elements and allow you to create your own reusable custom elements. For example, here I've created a custom element, grocery-item, which renders as a li. The text child of that node is sourced from a custom HTML property, title, which is accessible from within the component code:

```js
<div id="app"> 
    <h3>Grocery list</h3> 
    <ul> 
        <grocery-item title="Bread"></grocery-item> 
        <grocery-item title="Milk"></grocery-item> 
    </ul> 
</div> 

// js
<script> 
    Vue.component( 'grocery-item', { 
        props: [ 'title' ], 
        template: '<li>{{ title }}</li>' 
    }); 
    
    new Vue({ el: '#app' }); 
</script>
```

This renders as follows:

```html
<div id="app"> 
    <h3>Grocery list</h3>
    <ul> 
        <li>Bread</li> 
        <li>Milk</li> 
    </ul> 
</div>
```

But probably the main reason to use components is that it makes it easier to architect a larger application. Functionality can be broken into reuseable, self-contained components.

### 1.9 Single-file components

A drawback of using components is that you need to write your template in a JavaScript string outside of your main HTML file. There are ways to write template definitions in your HTML file, but then you have an awkward separation between markup and logic. A convenient solution to this is single-file components:

```js
<template> 
    <li v-on:click="bought = !bought" v-bind:class="{ bought: bought }"> 
        <div>{{ title }}</div> 
    </li> 
</template> 

<script> 
    export default { 
        props: [ 'title' ], 
        data: function() { 
            return { bought: false }; 
        } } 
</script> 

<style> 
    .bought { 
        opacity: 0.5; 
    } 
</style>
```

These files have the .vue extension and encapsulate the component template, JavaScript configuration, and style all in a single file. Of course, a web browser can't read these files, so they need to be first processed by a build tool such as Webpack.

1『关键点来了，所以得使用框架。』

### 1.10 Module build

As we saw earlier, Vue can be dropped into a project as an external script for direct use in a browser. Vue is also available as an NPM module for use in more sophisticated projects, including a build tool such as Webpack. If you're unfamiliar with Webpack, it's a module bundler that takes all your project assets and bundles them up into something you can provide to the browser. In the bundling process, you can transform those assets as well.

Using Vue as a module and introducing Webpack opens possibilities such as the following: 1) Single-file components. 2) ES feature proposals not currently supported in browsers. 3) Modularized code. 4) Pre-processors such as SASS and Pug.

We will be exploring Webpack more extensively in Chapter 5, Integrating Laravel and Vue.js with Webpack.

### 1.11 Server-side rendering

Server-side rendering is a great way to increase the perception of loading speed in full-stack apps. Users get a complete page with visible content when they load your site, as opposed to an empty page that doesn't get populated until JavaScript runs. Say we have an app built with components. If we use our browser development tool to view our page DOM after the page has loaded, we will see our fully rendered app:

```html
<div id="app"> 
    <ul> 
        <li>Component 1</li> 
        <li>Component 2</li> 
        <li> 
            <div>Component 3</div> 
        </li> 
    </ul> 
</div>
```

But if we view the source of the document, that is, index.html, as it was when sent by the server, you'll see it just has our mount element:

    <div id="app"></div>

Why? Because JavaScript is responsible for building our page and, ipso facto, JavaScript has to run before the page is built. But with server-side rendering, our index file includes the HTML needed for the browser to build a DOM before JavaScript is downloaded and run. The app does not load any faster, but content is shown sooner.

### 1.12 The Vue ecosystem

While Vue is a standalone library, it is even more powerful when combined with some of the optional tools in its ecosystem. For most projects, you'll include Vue Router and Vuex in your frontend stack, and use Vue Devtools for debugging.

#### 1.12.1 Vue Devtools

Vue Devtools is a browser extension that can assist you in the development of a Vue.js project. Among other things, it allows you to see the hierarchy of components in your app and the state of components, which is useful for debugging:

We'll see what else it can do later in this section.

#### 1.12.2 Vue Router

Vue Router allows you to map different states of your SPA to different URLs, giving you virtual pages. For example, mydomain.com/ might be the front page of a blog and have a component hierarchy like this:

```html
<div id="app"> 
    <my-header></my-header> 
    <blog-summaries></blog-summaries> 
    <my-footer></my-footer> 
</div>
```

Whereas mydomain.com/post/1 might be an individual post from the blog and look like this:

```html
<div id="app"> 
    <my-header></my-header> 
    <blog-post post-id="id"> 
    <my-footer></my-footer> 
</div>
```

Changing from one page to the other doesn't require a reload of the page, just swapping the middle component to reflect the state of the URL, which is exactly what Vue Router does.

#### 1.12.3 Vuex

Vuex provides a powerful way to manage the data of an application as the complexity of the UI increases, by centralizing the application's data into a single store. We can get snapshots of the application's state by inspecting the store in Vue Devtools:

The left column tracks changes made to the application data. For example, say the user saves or unsaves an item. You might name this event toggleSaved. Vue Devtools lets you see the particulars of this event as it occurs. We can also revert to any previous state of the data without having to touch the code or reload the page. This function, called Time Travel Debugging, is something you'll find very useful for debugging complex UIs.
# 0101 Hello Vue – An Introduction to Vue.js

Welcome to Full-Stack Vue.js 2 and Laravel 5! In this first chapter, we'll take a high-level overview of Vue.js, getting you familiar with what it can do, in preparation for learning how to do it. We'll also get acquainted with Vuebnb, the main case-study project featured in this book.

Topics this chapter covers:

Basic features of Vue, including templates, directives, and components.

Advanced features of Vue including single-file components and server-side rendering.

Tools in the Vue ecosystem including Vue Devtools, Vue Router, and Vuex.

The main case-study project that you'll be building as you progress through the book, Vuebnb.

Instructions for installing the project code.

## 01. Introducing Vue.js

At the time of writing in late 2017, Vue.js is at version 2.5. In less than four years from its first release, Vue has become one of the most popular open source projects on GitHub. This popularity is partly due to its powerful features, but also to its emphasis on developer experience and ease of adoption.

The core library of Vue.js, like React, is only for manipulating the view layer from the MVC architectural pattern. However, Vue has two official supporting libraries, Vue Router and Vuex, responsible for routing and data management respectively.

Vue is not supported by a tech giant in the way that React and Angular are and relies on donations from a small number of corporate patrons and dedicated Vue users. Even more impressively, Evan You is currently the only full-time Vue developer, though a core team of 20 more developers from around the world assist with development, maintenance, and documentation.

The key design principles of Vue are as follows: 1) Focus: Vue has opted for a small, focused API, and its sole purpose is the creation of UIs. 2) Simplicity: Vue's syntax is terse and easy to follow. 3) Compactness: The core library script is ~25 KB minified, making it smaller than React and even jQuery. 4) Speed: Rendering benchmarks beat many of the main frameworks, including React. 5) Versatility: Vue works well for small jobs where you might normally use jQuery, but can scale up as a legitimate SPA solution.

## 02. Basic features

Let's now do a high-level overview of Vue's basic features. If you want, you can create an HTML file on your computer like the following one, open it in your browser, and code along with the following examples. If you'd rather wait until the next chapter, when we start working on the case-study project, that's fine too as our objective here is simply to get a feel for what Vue can do:

```html
<!DOCTYPE html> <html lang="en"> <head> <meta charset="utf-8"> <meta http-equiv="X-UA-Compatible" content="IE=edge"> <title>Hello Vue</title> </head> <body> <!--We'll be adding stuff here!--> </body> </html>
```

## 03. Installation

Although Vue can be used as a JavaScript module in more sophisticated setups, it can also simply be included as an external script in the body of your HTML document:

```
<script src="https://unpkg.com/vue/dist/vue.js"></script>
```

## 04. Templates

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

## 05. Directives

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

## 06. Reactivity

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

## 07. Components

Components extend basic HTML elements and allow you to create your own reusable custom elements. For example, here I've created a custom element, grocery-item, which renders as a li. The text child of that node is sourced from a custom HTML property, title, which is accessible from within the component code:

```js
<div id="app"> 
    <h3>Grocery list</h3> 
    <ul> 
        <grocery-item title="Bread"></grocery-item> 
        <grocery-item title="Milk"></grocery-item> 
    </ul> 
</div> 
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

## 08. Advanced features

If you have been coding along with the examples so far, close your browser now until next chapter, as the following advanced snippets can't simply be included in a browser script.

## 09. Single-file components

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

1『关键点来了，所以得适用框架。』

## 10. Module build

As we saw earlier, Vue can be dropped into a project as an external script for direct use in a browser. Vue is also available as an NPM module for use in more sophisticated projects, including a build tool such as Webpack. If you're unfamiliar with Webpack, it's a module bundler that takes all your project assets and bundles them up into something you can provide to the browser. In the bundling process, you can transform those assets as well.

Using Vue as a module and introducing Webpack opens possibilities such as the following: 1) Single-file components. 2) ES feature proposals not currently supported in browsers. 3) Modularized code. 4) Pre-processors such as SASS and Pug.

We will be exploring Webpack more extensively in Chapter 5, Integrating Laravel and Vue.js with Webpack.

## 11. Server-side rendering

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

## 12. The Vue ecosystem

While Vue is a standalone library, it is even more powerful when combined with some of the optional tools in its ecosystem. For most projects, you'll include Vue Router and Vuex in your frontend stack, and use Vue Devtools for debugging.

### 1. Vue Devtools

Vue Devtools is a browser extension that can assist you in the development of a Vue.js project. Among other things, it allows you to see the hierarchy of components in your app and the state of components, which is useful for debugging:

Figure 1.1. Vue Devtools component hierarchy

We'll see what else it can do later in this section.

### 2. Vue Router

Vue Router allows you to map different states of your SPA to different URLs, giving you virtual pages. For example, mydomain.com/ might be the front page of a blog and have a component hierarchy like this:

```
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

### 3. Vuex

Vuex provides a powerful way to manage the data of an application as the complexity of the UI increases, by centralizing the application's data into a single store. We can get snapshots of the application's state by inspecting the store in Vue Devtools:

Figure 1.2. Vue Devtools Vuex tab

The left column tracks changes made to the application data. For example, say the user saves or unsaves an item. You might name this event toggleSaved. Vue Devtools lets you see the particulars of this event as it occurs. We can also revert to any previous state of the data without having to touch the code or reload the page. This function, called Time Travel Debugging, is something you'll find very useful for debugging complex UIs.

## 13. Case-study project

After a whirlwind overview of Vue's key features, I'm sure you're keen now to start properly learning Vue and putting it to use. Let's first have a look at the case-study project you'll be building throughout the book.

### 1. Vuebnb

Vuebnb is a realistic, full-stack web application which utilizes many of the main features of Vue, Laravel, and the other tools and design patterns covered in this book. From a user's point of view, Vuebnb is an online marketplace for renting short-term lodgings in cities around the world. You may notice some likeness between Vuebnb and another online marketplace for accommodation with a similar name!

You can view a completed version of Vuebnb here: [Vuebnb](http://vuebnb.vuejsdevelopers.com/).

If you don't have internet access right now, here are screenshots of two of the main pages. Firstly, the home page, where users can search or browse through accommodation options:

Figure 1.3. Vuebnb home page

Secondly, the listing page, where users view information specific to a single lodging they may be interested in renting:

Figure 1.4. Vuebnb listing page

### 2. Code base

The case-study project runs through the entire duration of this book, so once you've created the code base you can keep adding to it chapter by chapter. By the end, you'll have built and deployed a full-stack app from scratch.

The code base is in a GitHub repository. Download it in whatever folder on your computer that you normally put projects in, for example, ~/Projects:

```
$ cd ~/Projects 
$ git clone https://github.com/PacktPublishing/Full-Stack-Vue.js-2-and-Laravel-5 
$ cd Full-Stack-Vue.js-2-and-Laravel-5
```

Rather than cloning this repository directly, you could first make a fork and clone that. This will allow you to make any changes you like and save your work to your own remote repository. Here's a guide to forking a repository on GitHub: https://help.github.com/articles/fork-a-repo/.

### 3. Folders

The code base contains the following folders:

Figure 1.5. Code base directory contents

Here's a rundown of what each folder is used for:

1. Chapter02 to Chapter10 contains the completed state of the code for each chapter (excluding this one).

2. The images directory contains sample images for use in Vuebnb. This will be explained in Chapter 4, Building a Web Service with Laravel.

3. vuebnb is the project code you'll use for the main case-study project that we begin work on in Chapter 3, Setting Up a Laravel Development Environment.

4. vuebnb-prototype is the project code of the Vuebnb prototype that we'll build in Chapter 2, Prototyping Vuebnb, Your First Vue.js Project.

## Summary

In this first chapter, we did a high-level introduction to Vue.js, covering the basic features such as templates, directives, and components, as well as advanced features such as single-file components and server-side rendering. We also had a look at the tools in Vue's ecosystem including Vue Router and Vuex.

We then did an overview of Vuebnb, the full-stack project that you'll be building as you progress through the book, and saw how to install the code base from GitHub.

In the next chapter, we'll get properly acquainted with Vue's basic features and starting putting them to use by building a prototype of Vuebnb.

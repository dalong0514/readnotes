Learn to build professional full-stack web apps with Vue.js and Laravel

Key Features

Copyright © 2017 Packt Publishing

## Book Description

Vue is a JavaScript framework that can be used for anything from simple data display to sophisticated front-end applications and Laravel is a PHP framework used for developing fast and secure web-sites. This book gives you practical knowledge of building modern full-stack web apps from scratch using Vue with a Laravel back end.

In this book, you will build a room-booking website named "Vuebnb". This project will show you the core features of Vue, Laravel and other state-of-the-art web development tools and techniques. The book begins with a thorough introduction to Vue.js and its core concepts like data binding, directives and computed properties, with each concept being explained first, then put into practice in the case-study project.

You will then use Laravel to set up a web service and integrate the front end into a full-stack app. You will be shown a best-practice development workflow using tools like Webpack and Laravel Mix. With the basics covered, you will learn how sophisticated UI features can be added using ES+ syntax and a component-based architecture. You will use Vue Router to make the app multi-page and Vuex to manage application state.

Finally, you will learn how to use Laravel Passport for authenticated AJAX requests between Vue and the API, completing the full-stack architecture. Vuebnb will then be prepared for production and deployed to a free Heroku cloud server.

## What you will learn

Core features of Vue.js to create sophisticated user interfaces.

Build a secure backend API with Laravel.

Learn a state-of-the-art web development workflow with Webpack.

Full-stack app design principles and best practices.

Learn to deploy a full-stack app to a cloud server and CDN.

Managing complex application state with Vuex.

Securing a web service with Laravel Passport.

## Table of Contents

Hello Vue: An Introduction To Vue.js

Prototyping Vuebnb, Your First Vue.js Project

Hello Laravel: Getting Started With Laravel

Building A Web Service With Laravel

Integrating Laravel And Vue.js With Webpack

Composing Widgets With Vue.js Components

Building A Multi-Page App With Vue

Managing Your Application State With Vuex

Adding A User Login & API Authentication With Passport

Deploying A Full-Stack App To The Cloud

## About the Author

Anthony Gore is a full-stack web developer from Sydney, Australia. He loves to share knowledge about web technologies, with a particular passion for JavaScript. Anthony is the founder of Vue.js Developers, the largest online community of Vue enthusiasts, and he curates the weekly Vue.js Developers Newsletter. He is also a frequent blogger and the author of Ultimate Vue.js Developers Video Course. Besides web development, Anthony is a keen musician and is often traveling abroad and working remotely.

## About the Reviewer

Ashley Menhennett is a developer from South Australia, with 6 years of experience in web and software development, thriving on solving real-world problems through the application of software engineering processes. Ashley has recently accepted an offer of a graduate position in platform engineering, with plans to continue future study in the field of computer science. Ashley enjoys spending time with family and his Jack Russell, Alice.

www.PacktPub.com

## Preface

The year is 2014 and the war of Single-Page Application (SPA) solutions is truly raging. There are many rivals: Angular, React, Ember, Knockout, and Backbone, to name but a few. However, the battle being most closely watched is between Google's Angular and Facebook's React.

Angular, the SPA king until this point, is a full-fledged framework that follows the familiar MVC paradigm. React, the unlikely challenger seems quite odd in comparison with its core library only dealing with the view layer and markup written entirely in JavaScript! While Angular holds the bigger market share, React has caused a seismic shift in how developers think about web application design and has raised the bar on framework size and performance.

Meanwhile, a developer named Evan You was experimenting with his own new framework, Vue.js. It would combine the best features of Angular and React to achieve a perfect balance between simplicity and power. Your vision would resonate so well with other developers that Vue would soon be among the most popular SPA solutions.

Despite the fierce competition, Vue gained traction quickly. This was partly thanks to Taylor Otwell, the creator of Laravel, who tweeted in early 2015 about how impressed he was with Vue. This tweet generated a lot of interest in Vue from the Laravel community.

The partnership of Vue and Laravel would become further entwined with the release of Laravel version 5.3 in September 2016, when Vue was included as a default frontend library. This was a perfectly logical alliance for two software projects with the same philosophy: simplicity and an emphasis on the developer experience.

Today, Vue and Laravel offer an immensely powerful and flexible full-stack framework for developing web applications, and as you'll find throughout this book, they're a real treat to work with.

## What this book covers

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

## What you need for this book

Before you begin development on the case-study project, you must ensure that you have the correct software and hardware.

### Operating system

You can use a Windows or Linux-based operating system. I'm a Mac guy though, so any Terminal commands used in this book will be Linux commands.

Note that we'll be using the Homestead virtual development environment, which includes the Ubuntu Linux operating system. If you SSH into the box and run all your Terminal commands from there, you can use the same commands as me, even if you have a Windows host operating system.

### Development tools

Downloading the project code will require Git. If you haven't got Git installed already, follow the directions in this guide: https://git-scm.com/book/en/v2/Getting-Started-Installing-Git.

To develop a JavaScript application you'll need Node.js and NPM. These can be installed from the same package; see the instructions here: https://nodejs.org/en/download/.

We'll also be using Laravel Homestead. Instructions will be given in Chapter 3, Setting Up a Laravel Development Environment.

### Browser

Vue requires ECMAScript 5, which means you can use a recent version of any major browser to run it. I recommend you use Google Chrome, though, as I'll be giving debugging examples for Chrome Dev Tools, and it will be easier for you to follow along if you're using Chrome as well.

When choosing your browser, you should also consider compatibility with Vue Devtools.

### Vue Devtools

The Vue Devtools browser extension makes debugging Vue a breeze, and we'll be using it extensively in this book. The extension is made for Google Chrome, but will also work in Firefox (and Safari, with a bit of hacking.)

See the following link for more information and installation instructions: https://github.com/vuejs/vue-devtools

### IDE

You will, of course, need a text editor or IDE for developing the case-study project.

### Hardware

You'll need a computer with specs sufficient for installing and running the software just mentioned. The most resource-intensive program will be VirtualBox 5.2 (or VMWare or Parallels), which we'll be using to set up the Homestead virtual development environment.

You'll also need an internet connection for downloading the source code and project dependencies.

## Who this book is for

This book is for Laravel developers who are seeking a practical and best-practice approach to full-stack development with Vue.js and Laravel. Any web developer interested in the topic can successfully use this book, though, so long as they meet the following criteria:

Note that readers will not need any prior experience with Vue.js or other JavaScript frameworks.

## Conventions

In this book, you will find a number of text styles that distinguish between different kinds of information. Here are some examples of these styles and an explanation of their meaning.

Code words in text, database table names, folder names, filenames, file extensions, pathnames, dummy URLs, user input, and Twitter handles are shown as follows: "For example, here I've created a custom element, grocery-item, which renders as a li."

A block of code is set as follows:

```js
<div id="app"> <!--Vue has dominion within this node--> </div> <script> new Vue({ el: '#app' }); </script>
```

Any command-line input or output is written as follows:

    $ npm install

New terms and important words are shown in bold. Words that you see on the screen, for example, in menus or dialog boxes, appear in the text like this: "This is not permitted by Vue and if you attempt it you will get this error: Do not mount Vue to \<html> or <body> - mount to normal elements instead."

Warnings or important notes appear in a box like this.

Tips and tricks appear like this.

## Reader feedback

Feedback from our readers is always welcome. Let us know what you think about this book-what you liked or disliked. Reader feedback is important for us as it helps us develop titles that you will really get the most out of.

To send us general feedback, simply e-mail feedback@packtpub.com, and mention the book's title in the subject of your message.

If there is a topic that you have expertise in and you are interested in either writing or contributing to a book, see our author guide at www.packtpub.com/authors.

## Customer support

Now that you are the proud owner of a Packt book, we have a number of things to help you to get the most from your purchase.

## Downloading the example code

You can download the example code files for this book from your account at http://www.packtpub.com. If you purchased this book elsewhere, you can visit http://www.packtpub.com/support and register to have the files e-mailed directly to you.

You can download the code files by following these steps:

You can also download the code files by clicking on the Code Files button on the book's webpage at the Packt Publishing website. This page can be accessed by entering the book's name in the Search box. Please note that you need to be logged in to your Packt account.

Once the file is downloaded, please make sure that you unzip or extract the folder using the latest version of:

The code bundle for the book is also hosted on GitHub at https://github.com/PacktPublishing/Full-Stack-Vue.js-2-and-Laravel-5. We also have other code bundles from our rich catalog of books and videos available at https://github.com/PacktPublishing/. Check them out!

## Errata

Although we have taken every care to ensure the accuracy of our content, mistakes do happen. If you find a mistake in one of our books-maybe a mistake in the text or the code-we would be grateful if you could report this to us. By doing so, you can save other readers from frustration and help us improve subsequent versions of this book. If you find any errata, please report them by visiting http://www.packtpub.com/submit-errata, selecting your book, clicking on the Errata Submission Form link, and entering the details of your errata. Once your errata are verified, your submission will be accepted and the errata will be uploaded to our website or added to any list of existing errata under the Errata section of that title.

To view the previously submitted errata, go to https://www.packtpub.com/books/content/support and enter the name of the book in the search field. The required information will appear under the Errata section.

## Piracy

Piracy of copyrighted material on the Internet is an ongoing problem across all media. At Packt, we take the protection of our copyright and licenses very seriously. If you come across any illegal copies of our works in any form on the Internet, please provide us with the location address or website name immediately so that we can pursue a remedy.

Please contact us at copyright@packtpub.com with a link to the suspected pirated material.

We appreciate your help in protecting our authors and our ability to bring you valuable content.

## Questions

If you have a problem with any aspect of this book, you can contact us at questions@packtpub.com, and we will do our best to address the problem.
# 0201. Prototyping Vuebnb, Your First Vue.js Project

In this chapter, we will learn the basic features of Vue.js. We'll then put this knowledge into practice by building a prototype of the case-study project, Vuebnb.

Topics this chapter covers: 1) Installation and basic configuration of Vue.js. 2) Vue.js essential concepts, such as data binding, directives, watchers and lifecycle hooks. 3) How Vue's reactivity system works. 4) Project requirements for the case-study project. 5) Using Vue.js to add page content including dynamic text, lists, and a header image. 6) Building an image modal UI feature with Vue.

## 2.1. Vuebnb prototype

In this chapter, we'll be building a prototype of Vuebnb, the case-study project that runs for the duration of this book. The prototype will just be of the listing page, and by the end of the chapter will look like this:

Figure 2.1. Vuebnb prototype

Once we've set up our backend in Chapter 3, Setting Up a Laravel Development Environment, and Chapter 4, Building a Web Service with Laravel, we'll migrate this prototype into the main project.

## 2.2 Project code

Before we begin, you'll need to download the code base to your computer by cloning it from GitHub. Instructions are given in the section Code base in Chapter 1, Hello Vue - An Introduction to Vue.js. The folder vuebnb-prototype has the project code for the prototype we'll now be building. Change into that folder and list the contents:

    $ cd vuebnb-prototype 
    $ ls -la

The folder contents should look like this:

Figure 2.2. vuebnb-prototype project files

Unless otherwise specified, all further Terminal commands in this chapter will assume you're in the vuebnb-prototype folder.

## 2.3 NPM install

You'll now need to install the third-party scripts used in this project, including Vue.js itself. The NPM install method will read the included package.json file and download the required modules:

    $ npm install

You'll now see a new node\_modules directory has appeared in your project folder.

### 2.3.1 Main files

Open the vuebnb-prototype directory in your IDE. Note that the following index.html file is included. It's mostly comprised of boilerplate code, but also has some structural markup included in the body tag. Also note that this file links to style.css, where our CSS rules will be added, and app.js, where our JavaScript will be added.

index.html:

```html
<!DOCTYPE html> 
<html> 
<head> 
    <meta charset="UTF-8"> 
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"> 
    <meta name="viewport" content="width=device-width,initial-scale=1"> 
    <title>Vuebnb</title> 
    <link href="node_modules/open-sans-all/css/open-sans.css" rel="stylesheet"> 
    <link rel="stylesheet" href="style.css" type="text/css"> 
</head> 

<body> 
<div id="toolbar"> 
    <img class="icon" src="logo.png"> 
    <h1>vuebnb</h1> 
</div> 
<div id="app"> 
    <div class="container"></div> 
</div> 
<script src="app.js"></script> 
</body> 
</html>
```

Currently app.js is an empty file, but I have included some CSS rules in style.css to get us started.

style.css:

```css
body {
  font-family: 'Open Sans', sans-serif;
  color: #484848;
  font-size: 17px;
  margin: 0;
}

.container {
  margin: 0 auto;
}

@media (min-width: 744px) {
  .container {
    width: 696px;
  }
}

#toolbar {
  display: flex;
  align-items: center;
  border-bottom: 1px solid #e4e4e4;
  box-shadow: 0 1px 5px rgba(0, 0, 0, 0.1);
}

#toolbar .icon {
  height: 34px;
  padding: 16px 12px 16px 24px;
  display: inline-block;
}

#toolbar h1 {
  color: #4fc08d;
  display: inline-block;
  font-size: 28px;
  margin: 0;
}

```

### 2.3.2 Opening in the browser

To view the project, locate the index.html file in your web browser. In Chrome, it's as simple as File | Open File. When it loads, you'll see a page that is mostly empty, other than the toolbar at the top.

### 2.3.3 Installing Vue.js

Now it's time to add the Vue.js library to our project. Vue was downloaded as part of our NPM install, so now we can simply link to the browser-build of Vue.js with a script tag.

index.html:

```html
<body> 
<div id="toolbar">...</div> 
<div id="app">...</div> 
<script src="node_modules/vue/dist/vue.js"></script> 
<script src="app.js"></script> 
</body>
```

It's important that we include the Vue library before our own custom app.js script, as scripts run sequentially.

1『重点，顺序不能错，先引用 vue.js 再引用 app.js。』

Vue will now be registered as a global object. We can test this by going to our browser and typing the following in the JavaScript console:

    console.log(Vue);

Here is the result:

Figure 2.3. Checking Vue is registered as a global object

## 2.4 Page content

With our environment set up and starter code installed, we're now ready to take the first steps in building the Vuebnb prototype. Let's add some content to the page, including the header image, the title, and the About section. We'll be adding structure to our HTML file and using Vue.js to insert the correct content where we need it.

## 2.5 The Vue instance

Looking at our app.js file, let's now create our root instance of Vue.js by using the new operator with the Vue object.

app.js:

    var app = new Vue();

When you create a Vue instance, you will usually want to pass in a configuration object as an argument. This object is where your project's custom data and functions are defined.

app.js:

```html
var app = new Vue({ 
    el: '#app' 
});
```

As our project progresses, we'll be adding much more to this configuration object, but for now we've just added the el property that tells Vue where to mount itself in the page. You can assign to it a string (a CSS selector) or an HTML node object. In our case, we've used the #app string, which is a CSS selector referring to the element with the app ID.

index.html:

```html
<div id="app"> 
    <!--Mount element--> 
</div>
```

Vue has dominion over the element it mounts on and any child node. For our project so far, Vue could manipulate the div with the header class, but it could not manipulate the div with the toolbar ID. Anything placed within this latter div will be invisible to Vue.

index.html:

```js
<body> 
<div id="toolbar">...</div> 
<div id="app"> 
    <!--Vue only has dominion here--> 
    <div class="header">...</header> 
    ... 
</div> 
<script src="node_modules/vue/dist/vue.js"></script> 
<script src="app.js"></script> 
</body>
```

From now on, we'll refer to our mount node and its children as our template.

## 2.6 Data binding

A simple task for Vue is to bind some JavaScript data to the template. Let's create a data property in our configuration object and assign to it an object including a title property with a 'My apartment' string value.

app.js:

```js
var vm = new Vue({
    el: "#app",
    data: {
        title: "My apartment"
    },
});
```

Any property of this data object will be available within our template. To tell Vue where to bind this data, we can use mustache syntax, that is, double curly brackets, for example, {{ myProperty }}. When Vue instantiates, it compiles the template, replaces the mustache syntax with the appropriate text, and updates the DOM to reflect this. This process is called text interpolation and is demonstrated in the following code block.

index.html:

```html
<div id="app">
    <div class="header">{{ title }}</div>
</div
```

Will render as this:

```html
<div id="app">
    <div class="header">My apartment</div>
</div
```

Let's add a few more data properties now and enhance our template to include more of the page structure.

app.js:

```js
var vm = new Vue({
    el: "#app",
    data: {
        title: "My apartment",
        address: "12 My Street, My City, My Country",
        about: "This is a description of my apartment.",
    },
});
```

index.html:

```html
<body>
    <div id="toolbar"></div>
    <div id="app">
        <div class="heading">
            <h1>{{ title }}</h1>
            <p>{{ address }}</p>
        </div>
        <hr>
        <div class="about">
            <h3>About this listing</h3>
            <p>{{ about }}</p>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script src="js/vueapp.js"></script>
</body>
```

Let's also add some new CSS rules.

style.css:

```css
.heading {
    margin-bottom: 2em;
    margin-left: 2em;
}

.heading h1 {
    font-size: 32px;
    font-weight: 700;
}

.heading p {
    font-size: 15px;
    color: #767676;
}

hr {
    border: 0;
    border-top: 1px solid #dce0e0;
}

.about {
    margin-top: 2em;
    margin-left: 2em;
}

.about h3 {
    font-size: 22px;
}

.about p {
    white-space: pre-wrap;
}
```

If you now save and refresh your page, it should look like this:

Figure 2.4. Listing page with basic data binding

1『

总算基本弄清楚 Laravel-Mix 前端任务自动化的实现过程。可以通过安装热启动作为切入点：

    npm run watch-poll

会自动安装缺失的组件。安装好后会自动创建如下文件：

```
 create mode 100644 laravel/public/css/app.css
 create mode 100644 laravel/public/js/app.js
 create mode 100644 laravel/public/mix-manifest.json
```

上面的 2 个文件相当于从 resources 文件夹下面的 js、sass 自动编译过来的。先看 css 方面，在 resources/sass/app.scss 文件里添加各个样式，热启动会自动生成 /public/css/app.css 文件，所以只需在页面文件 html 里引入根目录下的样式文件即可。

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="css/app.css">
</head
```

接着看 js 方面。新建 resources/js/vueapp.js，此时的 vueapp.js 不会自动通过热启动编译过去（目前只有 resources/js/app.js 可以自动编译到 public/js/app.js），可以在 resources/js/app.js 里面引入它：

```js
require('./bootstrap');
require('./vueapp');
```

引入的话，页面文件那边引入 app.js 即可：

    <script src="js/app.js"></script>

也可以将 resources/js/vueapp.js 单独编译到 public/js/vueapp.js，在 webpack.mix.js 里：

```js
const mix = require('laravel-mix');

/*
 |--------------------------------------------------------------------------
 | Mix Asset Management
 |--------------------------------------------------------------------------
 |
 | Mix provides a clean, fluent API for defining some Webpack build steps
 | for your Laravel application. By default, we are compiling the Sass
 | file for the application as well as bundling up all the JS files.
 |
 */

mix.js('resources/js/app.js', 'public/js')
    .js('resources/js/vueapp.js', 'public/js')
    .sass('resources/sass/app.scss', 'public/css');
```

这样的话，在页面文件那边引入 vueapp.js 即可：

    <script src="js/vueapp.js"></script>

』

## 2.7 Mock listing

While we're developing, it'd be nice to work with some mock data so that we can see how our completed page will look. I've included sample/data.js in the project for this very reason. Let's load it in our document, making sure it goes above our app.js file.

index.html:

```html
<body>
    <div id="toolbar"></div>
    <div id="app">
        <div class="heading">
            <h1>{{ title }}</h1>
            <p>{{ address }}</p>
        </div>
        <hr>
        <div class="about">
            <h3>About this listing</h3>
            <p>{{ about }}</p>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script src="data.js"></script>
    <script src="js/vueapp.js"></script>
</body>
```

Have a look at the file and you'll see that it declares a sample object. We will now utilize it in our data configuration.

app.js:

```js
var vm = new Vue({
    el: "#app",
    data: {
        title: sample.title,
        address: sample.address,
        about: sample.about,
    },
});
```

Once you save and refresh, you'll see more realistic data on the page:

Figure 2.5. Page including mock-listing sample

Using global variables split over different script files in this way is not an ideal practice. We'll only be doing this in the prototype, though, and later we'll get this mock-listing sample from the server.

1『

在 vueapp.js 里直接引入 data.js 走不通，原因待确认。

```js
require('./data');

var vm = new Vue({

    el: "#app",
    data: {
        title: sample.title,
        address: sample.address,
        about: sample.about,
    },
});
```

把 data.js 放入根目录下，页面文件里直接引入是可以的。

』

## 2.8 Header image

No room listing would be complete without a big, glossy image to show it off. We've got a header image in our mock listing that we'll now include. Add this markup to the page.

index.html:

```html
<div id="app"> 
    <div class="header"> 
        <div class="header-img"></div> 
    </div> 
    <div class="container">...</div> 
</div>
```

And this to the CSS file.

style.css:

```css
.header {
    height: 320px;
}

.header .header-img {
    background-repeat: no-repeat;
    background-size: cover;
    background-position: 50% 50%;
    background-color: #f5f5f5;
    height: 100%;
}
```

1『上面的「.header .header-img」一定要先设置，否则后面的图片显示不出来，这个问题找了很久才解决。（2020-04-18）』

You may be wondering why we're using a div rather than an img tag. To help with positioning, we're going to set our image as the background of the div with the header-img class.

## 2.9 Style binding

To set a background image, we must provide the URL as a property in a CSS rule like this:

```
.header .header-img { 
    background-image: url(...); 
}
```

Obviously, our header image should be specific to each individual listing, so we don't want to hard code this CSS rule. Instead, we can have Vue bind the URL from data to our template. Vue can't access our CSS style sheet, but it can bind to an inline style attribute:

```html
<div class="header-img" style="background-image: url(...);"></div>
```

You may think using a text interpolation is the solution here, for example:

```html
<div class="header-img" style="background-image: {{ headerUrl }}"></div>
```

1『这个曲线救国的方法有趣。』

But this is not valid Vue.js syntax. This is, instead, a job for another Vue.js feature called a directive. Let's explore directives first and then come back to solving this problem.

## 2.10 Directives

Vue's directives are special HTML attributes with the v- prefix, for example, v-if, which provide a simple way to add functionality to our templates. Some examples of directives you can add to an element are: 1) v-if: Conditionally render the element. 2) v-for: Render the element multiple times based on an array or object. 3) v-bind: Dynamically bind an attribute of the element to a JavaScript expression. 4) v-on: Attach an event listener to the element.

There are more that we will explore throughout the book.

### 2.10.1 Usage

Just like normal HTML attributes, directives are usually name/value pairs in the form name="value". To use a directive, simply add it to an HTML tag as you would an attribute, for example:

    <p v-directive="value">

### 2.10.2 Expressions

If a directive requires a value, it will be an expression. In the JavaScript language, expressions are small, evaluable statements that produce a single value. Expressions can be used wherever a value is expected, for example in the parenthesis of an if statement:

```js
if (expression) { 
    ... 
}
```

The expression here could be any of the following: 1) A mathematical expression, for example x + 7. 2) A comparison, for example v <= 7. 3) A Vue data property, for example this.myval.

Directives and text interpolations both accept expression values:

    <div v-dir="someExpression">{{ firstName + " " + lastName }}</div>

### 2.10.3 Example: v-if

v-if will conditionally render an element if its value is a truthy expression. In the following case, v-if will remove/insert the p element depending on the myval value:

```
<div id="app"> <p v-if="myval">Hello Vue</p> </div> <script> var app = new Vue({ el: '#app', data: { myval: true } }); </script>
```

Will renders as:

```
<div id="app"> <p>Hello Vue</p> </div>
```

If we add a consecutive element with the v-else directive (a special directive that requires no value), it will be symmetrically removed/inserted as myval changes:

```
<p v-if="myval">Hello Vue</p> <p v-else>Goodbye Vue</p>
```

### 2.10.4 Arguments

Some directives take an argument, denoted by a colon after the directive name. For example, the v-on directive, which listens to DOM events, requires an argument to specify which event should be listened to:

    <a v-on:click="doSomething">

Instead of click, the argument could be mouseenter, keypress, scroll, or any other event (including custom events).

### 2.10.5 Style binding (continued)

Coming back to our header image, we can use the v-bind directive with the style argument to bind a value to the style attribute.

index.html:

```
<div class="header-img" v-bind:style="headerImageStyle"></div>
```

headerImageStyle is an expression that evaluates to a CSS rule that sets the background image to the correct URL. It sounds very confusing, but when you see it working, it will be quite clear. Let's now create headerImageStyle as a data property. When binding to a style attribute, you can use an object where the properties and values are equivalent to the CSS properties and values.

app.js:

```js
data: { 
    ... 
    headerImageStyle: { 
        'background-image': 'url(sample/header.jpg)' 
    } 
},
```

Save the code, refresh the page, and the header image will be shown:

Figure 2.6. Page including header image

Inspect the page with your browser Dev Tools and notice how the v-bind directive has evaluated:

    <div class="header-img" style="background-image: url('sample/header.jpg');"></div>

## 2.11 Lists section

The next bit of content we'll add to our page is the Amenities and Prices lists:

Figure 2.7. Lists section

If you look at the mock-listing sample, you'll see that the amenities and prices properties on the object are both arrays.

sample/data.js:

```js
    amenities: [
      {
        title: 'Wireless Internet',
        icon: 'fa-wifi'
      },
      {
        title: 'Pets Allowed',
        icon: 'fa-paw'
      },
      {
        title: 'TV',
        icon: 'fa-television'
      },
      {
        title: 'Kitchen',
        icon: 'fa-cutlery'
      },
      {
        title: 'Breakfast',
        icon: 'fa-coffee'
      },
      {
        title: 'Laptop friendly workspace',
        icon: 'fa-laptop'
      }
    ],
    prices: [
      {
        title: 'Per night',
        value: '$89'
      },
      {
        title: 'Extra people',
        value: 'No charge'
      },
      {
        title: 'Weekly discount',
        value: '18%'
      },
      {
        title: 'Monthly discount',
        value: '50%'
      }
    ]
```

Wouldn't it be easy if we could just loop over these arrays and print each item to the page? We can! This is what the v-for directive does. First, let's add these as data properties on our root instance.

app.js:

```js
var vm = new Vue({
    el: "#app",
    data: {
        title: sample.title,
        address: sample.address,
        about: sample.about,
        headerImageStyle: {
            "background-image": "url('image/header.jpg')"
        },
        amenities: sample.amenities,
        prices: sample.prices,
    },
})
```

### 2.11.1 List rendering

The v-for directive requires a special type of expression in the form of item in items, where items is the source array, and item is an alias for the current array element being looped over. Let's work on the amenities array first. Each member of this array is an object with a title and icon property, that is:

    { title: 'something', icon: 'something' }

We'll add the v-for directive into the template and the expression we assign to it will be amenity in amenities. The alias part of the expression, that is amenity, will refer, throughout the loop sequence, to each object in the array, starting with the first.

index.html:

```html
<div class="container">
    <div class="heading">
        <h1>{{ title }}</h1>
        <p>{{ address }}</p>
    </div>
    <hr>
    <div class="about">
        <h3>About this listing</h3>
        <p>{{ about }}</p>
    </div>
    <div class="lists">
        <div v-for="amenity in amenities">{{ amenity.title }}</div>
    </div>
</div>
```

It will render as:

```
<div class="container"> <div class="heading">...</div> <hr> <div class="about">...</div> <div class="lists"> <div>Wireless Internet</div> <div>Pets Allowed</div> <div>TV</div> <div>Kitchen</div> <div>Breakfast</div> <div>Laptop friendly workspace</div> </div> </div>
```

### 2.11.2 Icons

The second property of our amenity objects is icon. This is actually a class relating to an icon in the Font Awesome icon font. We've installed Font Awesome as an NPM module already, so add this to the head of the page to now use it.

index.html:

```html
<head> 
    ... 
    <link rel="stylesheet" href="node_modules/open-sans-all/css/open-sans.css"> 
    <link rel="stylesheet" href="node_modules/font-awesome/css/font-awesome.css"> 
    <link rel="stylesheet" href="style.css" type="text/css"> 
</head>
```

Now we can complete the structure of our amenities section in the template.

3『

[How to use Font Awesome 5 on VueJS Project - Frontend Weekly - Medium](https://medium.com/front-end-weekly/how-to-use-fon-awesome-5-on-vuejs-project-ff0f28310821)

如何使用 Font Awesome 待实现。

』

index.html:

```html
<div class="lists"> <hr> <div class="amenities list"> <div class="title"><strong>Amenities</strong></div> <div class="content"> <div class="list-item" v-for="amenity in amenities"> <i class="fa fa-lg" v-bind:class="amenity.icon"></i> <span>{{ amenity.title }}</span> </div> </div> </div> </div>
```

style.css:

```css
.list { display: flex; flex-wrap: nowrap; margin: 2em 0; } .list .title { flex: 1 1 25%; } .list .content { flex: 1 1 75%; display: flex; flex-wrap: wrap; } .list .list-item { flex: 0 0 50%; margin-bottom: 16px; } .list .list-item > i { width: 35px; } @media (max-width: 743px) { .list .title { flex: 1 1 33%; } .list .content { flex: 1 1 67%; } .list .list-item { flex: 0 0 100%; } }
```

### 2.11.3 Key

As you might expect, the DOM nodes generated by v-for="amenity in amenities" are reactively bound to the amenities array. If the content of amenities changes, Vue will automatically re-render the nodes to reflect the change. When using v-for, it's recommended you provide a unique key property to each item in the list. This allows Vue to target the exact DOM nodes that need to be changed, making DOM updates more efficient. Usually, the key would be a numeric ID, for example:

```html
<div v-for="item in items" v-bind:key="item.id"> 
    {{ item.title }} 
</div>
```

1『跟小程序一样一样的。』

For the amenities and prices lists, the content is not going to change over the life of the app, so there's no need for us to provide a key. Some linters may warn you about this, but in this case, the warning can be safely ignored.

### 2.11.4 Prices

Let's now add the price list to our template as well.

index.html:

```
<div class="lists"> <hr> <div class="amenities list">...</div> <hr> <div class="prices list"> <div class="title"> <strong>Prices</strong> </div> <div class="content"> <div class="list-item" v-for="price in prices"> {{ price.title }}: <strong>{{ price.value }}</strong> </div> </div> </div> </div>
```

I'm sure you'll agree that looping a template is far easier than writing out every item. However, you may notice that there is still some common markup between these two lists. Later in the book we'll utilize components to make this part of the template even more modular.

## 2.12 Show more feature

We've run into a problem now that the lists section is after the About section. The About section has an arbitrary length, and in some of the mock listings that we'll add you'll see that this section is quite long. We don't want it to dominate the page and force the user to do a lot of unwelcome scrolling to see the lists section, so we need a way to hide some of the text if it's too long, yet allow the user to view the full text if they choose.

Let's add a show more UI feature that will crop the About text after a certain length and give the user a button to reveal the hidden text:

Figure 2.8. Show more feature

We'll start by adding a contracted class to the p tag that contains the about text interpolation. The CSS rule for this class will restrict its height to 250 pixels and hide any text overflowing the element.

index.html:

```html
<div class="about">
    <h3>About this listing</h3>
    <p class="contracted">{{ about }}</p>
    <button class="more">+ More</button>
</div>
```

style.css:

```css
.about p.contracted {
    height: 250px;
    overflow: hidden;
}
```

We'll also put a button after the p tag that the user can click to expand the section to full height.

index.html:

```html
<div class="about">
    <h3>About this listing</h3>
    <p class="contracted">{{ about }}</p>
    <button class="more">+ More</button>
</div>
```

Here's the CSS that's needed, including a generic button rule that will provide base styling for all buttons that we'll add throughout the project.

style.css:

```css
.button {
    text-align: center;
    vertical-align: middle;
    user-select: none;
    white-space: nowrap;
    cursor: pointer;
    display: inline-block;
    margin-bottom: 0;
}

.about button.more {
    background: transparent;
    border: 0;
    color: #008489;
    padding: 0;
    font-size: 17px;
    font-weight: bold;
}

.about button.more:hover,
.about button.more:focus,
.about button.more:active {
    text-decoration: underline;
    outline: none;
}
```

To make this work, we need a way to remove the contracted class when the user clicks the More button. Seems like a good job for directives!

### 2.12.1 Class binding

How we'll approach this is to dynamically bind the contracted class. Let's create a contracted data property and set its initial value to true.

app.js:

```js
data: { 
    ... 
    contracted: true 
}
```

Like our style binding, we can bind this class to an object. In the expression, the contracted property is the name of the class to be bound, the contracted value is a reference to the data property of that same name, which is a Boolean. So if the contracted data property evaluates to true, that class will be bound to the element, and if it evaluates to false, it will not.

index.html:

```html
<p v-bind:class="{ contracted: contracted }">{{ about }}</p>
```

It follows that when the page loads the contracted class is bound:

```html
<p class="contracted">...</p>
```

### 2.12.2 Event listener

We now want to remove the contracted class automatically when the user clicks the More button. To do this job, we'll use the v-on directive, which listens to DOM events with a click argument. The value of the v-on directive can be an expression that assigns contracted to false.

index.html:

```html
<div class="about">
    <h3>About this listing</h3>
    <p v-bind:class="{contracted: contracted}">{{ about }}</p>
    <button class="more" v-on:click="contracted = false">+ More</button>
</div
```

## 2.13 Reactivity

When we click the More button, the contracted value changes and Vue will instantly update the page to reflect this change. How does Vue know to do this? To answer this question we must first understand the concept of getters and setters.

Getters and setters. To assign a value to a property of a JavaScript object is as simple as:

```js
var myObj = { 
    prop: 'Hello' 
}
```

To retrieve it is just as simple:

    myObj.prop

There's no trick here. The point I want to make though, is that we can replace this normal assignment/retrieval mechanism of an object through use of getters and setters. These are special functions that allow custom logic for getting or setting the property's value. Getters and setters are especially useful when one property's value is determined by another. Here's an example:

```js
var person = { 
    firstName: 'Abraham', 
    lastName: 'Lincoln', 
    get fullName() { 
        return this.firstName + ' ' + this.lastName; 
    }, 
    set fullName(name) { 
        var words = name.toString().split(' '); 
        this.firstName = words[0] || ''; 
        this.lastName = words[1] || ''; 
    } 
}
```

The get and set functions of the fullName property are invoked whenever we attempt a normal assignment/retrieval of its value:

```js
console.log(person.fullName); // Abraham Lincoln 
person.fullName = 'George Washington'; 
console.log(person.firstName); // George 
console.log(person.lastName) // Washington
```

### 2.13.1 Reactive data properties

Another one of Vue's initialization steps is to walk through all of the data properties and assign them getters and setters. If you look in the following screenshot, you can see how each property in our current app has a get and set function added to it:

Figure 2.9. Getters and setters

Vue added these getters and setters to enable it to perform dependency tracking and change notification when the properties are accessed or modified. So, when the contracted value is changed by the click event, its set method is triggered. The set method will set the new value, but will also carry out a secondary task of informing Vue that a value has changed and any part of the page relying on it may need to be re-rendered.

If you'd like to know more about Vue's reactivity system, check out the article Reactivity In Vue.js (And Its Pitfalls) at https://vuejsdevelopers.com/2017/03/05/vue-js-reactivity/.

### 2.13.1 Hiding the More button

Once the About section has been expanded, we want to hide the More button as it's no longer needed. We can use the v-if directive to achieve this in conjunction with the contracted property.

index.html:

```html
<button v-if="contracted" class="more" v-on:click="contracted = false">
    + More
</button>
```

## 2.14 Image modal window

To prevent our header image from dominating the page, we've cropped it and limited its height. But what if the user wants to see the image in its full glory? A great UI design pattern to allow the user to focus on a single item of content is a modal window. Here's what our modal will look like when opened:

Figure 2.10. Header image modal

Our modal will give a properly scaled view of the header image so the user can focus on the appearance of the lodgings without the distraction of the rest of the page. Later in the book, we will insert an image carousel into the modal so the user can browse through a whole collection of room images!

For now, though, here are the required features for our modal: 1) Open the modal by clicking the header image. 2) Freeze the main window. 3) Show the image. 3) Close the modal window with a close button or the Escape key.

### 2.14.1 Opening

First, let's add a Boolean data property that will represent the opened or closed state of our modal. We'll initialize it to false.

app.js:

```js
data: { 
    ... 
    modalOpen: false 
}
```

We'll make it so that clicking our header image will set the modal to open. We'll also overlay a button labelled View Photos in the bottom-left corner of the header image to give a stronger signal to the user that they should click to show the image.

index.html:

```
<div class="header">
    <div 
    class="header-img" 
    v-bind:style="headerImageStyle"
    v-on:click="modalOpen = true"
    >
        <button class="view-photos">View Photos</button>
    </div>
</div>
```

Note that, by putting the click listener on the wrapping div, the click event will be captured regardless of whether the user clicks the button or the div due to DOM event propagation. We'll add some more CSS to our header image to make the cursor a pointer, letting the user know the header can be clicked, and giving the header a relative position so the button can be positioned within it. We'll also add rules to style the button.

style.css:

```css
.header .header-img {
    background-repeat: no-repeat;
    background-size: cover;
    background-position: 50% 50%;
    background-color: #f5f5f5;
    height: 100%;
    cursor: pointer;
    position: relative;
}

button {
    border-radius: 4px;
    border: 1px solid #c4c4c4;
    text-align: center;
    vertical-align: middle;
    font-weight: bold;
    line-height: 1.43;
    user-select: none;
    white-space: nowrap;
    cursor: pointer;
    background: white;
    color: #484848;
    padding: 7px 18px;
    font-size: 14px;
    display: inline-block;
    margin-bottom: 0;
}

.header .header-img .view-photos {
    position: absolute;
    bottom: 20px;
    left: 20px;
}
```

1『注意 css 里，button 前面是没有点号的。』

Let's now add the markup for our modal. I've put it after the other elements in the page, though it doesn't really matter as the modal will be out of the regular flow of the document. We remove it from the flow by giving it a fixed position in the following CSS.

index.html:

```html
<div id="app"> 
    <div class="header">...</div> 
    <div class="container">...</div> 
    <div id="modal" v-bind:class="{ show : modalOpen }"></div> 
</div>
```

The main modal div will act as a container for the rest of the modal content, but also as a background panel that will cover up the main window content. To achieve this, we use CSS rules to stretch it to completely cover the viewport by giving it top, right, bottom, and left values of 0. We'll set the z-index to a high number to ensure the modal is stacked in front of any other element in the page.

Note also that the display is initially set to none, but we're dynamically binding a class to the modal called show that gives it block display. The addition/removal of this class will, of course, be bound to the value of modalOpen.

style.css:

```
#modal {
    display: none;
    position: fixed;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    z-index: 2000;
}
```

### 2.14.2 Window

Let's now add markup for the window that will be overlaid on our background panel. The window will have a width constraint and will be centered in the viewport.

index.html:

```html
<div id="modal" v-bind:class="{ show: modalOpen }">
    <div class="modal-content">
        <img src="image/header.jpg"/>
    </div>
</div>
```

style.css:

```css
.modal-content {
    height: 100%;
    max-width: 105vh;
    padding-top: 12vh;
    margin: 0 auto;
    position: relative;
}

.modal-content img {
    max-width: 100%;
}
```

### 2.14.3 Disabling the main window

When the modal is open, we want to prevent any interaction with the main window and also make a clear distinction between the main window and the child window. We can do this by: 1) Dimming the main window. 2) Preventing body scroll.

Dimming the main window. We could simply hide our main window when the modal is open, but it's better if the user can still be aware of where they are in flow of the app. To achieve this, we will dim the main window under a semi-transparent panel. We can do this by giving our modal panel an opaque black background.

style.css:

```css
#modal { 
    ... 
    background-color: rgba(0,0,0,0.85); 
}
```

Preventing body scroll. We have a problem, though. Our modal panel, despite being full screen, is still a child of the body tag. This means we can still scroll the main window! We don't want users to interact with the main window in any way while the modal is open, so we must disable scrolling on the body.

The trick is to add the CSS overflow property to the body tag and set it to hidden. This has the effect of clipping any overflow (that is, part of the page not currently in view), and the rest of the content will be made invisible. We'll need to dynamically add and remove this CSS rule, as we obviously want to be able to scroll through the page when the modal is closed. So, let's create a class called modal-open that we can apply to the body tag when the modal is open.

style.css:

```
body.modal-open { 
    overflow: hidden;
    position: fixed; 
}
```

We can use v-bind:class to add/remove this class, right? Unfortunately, no. Remember that Vue only has dominion over the element where it is mounted:

```html
<body> 
    <div id="app"> 
        <!--This is where Vue has dominion and can modify the page freely--> 
    </div> 
    <!--Vue is unable to change this part of the page or any ancestors--> 
</body>
```

If we add a directive to the body tag, it will not be seen by Vue.

## 2.15 Vue's mount element

What if we just mounted Vue on the body tag, wouldn't that solve our problems? For example:

    new Vue({ el: 'body' });

This is not permitted by Vue and if you attempt it you will get this error: 

    Do not mount Vue to <html> or <body> - mount to normal elements instead.

Remember that Vue has to compile the template and replaces the mount node. If you have script tags as children of the mount node, as you often do with body, or if your user has browser plugins that modify the document (many do) then all sorts of hell might break loose on the page when it replaces that node. If you define your own root element with a unique ID, there should be no such conflict.

1『上面的是一个关键知识点。』

## 2.16 Watchers

So, how can we add/remove classes from the body if it's out of Vue's dominion? We'll have to do it the old-fashioned way with the browser's Web API. We need to run the following statements when the modal is opened or closed:

```
// Modal opens 
document.body.classList.add('modal-open'); 

// Modal closes 
document.body.classList.remove('modal-closed');
```

As discussed, Vue adds reactive getters and setters to each data property so that when data changes it knows to update the DOM appropriately. Vue also allows you to write custom logic that hooks into reactive data changes via a feature called watchers.

To add a watcher, first add the watch property to your Vue instance. Assign an object to this where each property has the name of a declared data property, and each value is a function. The function has two arguments: the old value and new value. Whenever a data property changes, Vue will trigger any declared watcher methods:

```js
<script>
    var vm1 = new Vue({
        // el: "#app1",
        data: {
            message: "Hello World",
        },
        watch: {
            message: function(newVal, oldVal) {
                console.log(oldVal, ", ", newVal);
            },
        },
    });
    setTimeout(function() {
        vm1.message = "Goodbye world";
    }, 2000);
</script>
```

Vue can't update the body tag for us, but it can trigger custom logic that will. Let's use a watcher to update the body tag when our modal is opened and closed.

1『实现方法：Vue 实例里增加 watch 方法。』

app.js:

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

Now when you try to scroll the page you'll see it won't budge!

## 2.17 Closing

Users will need a way to close their modal and return to the main window. We'll overlay a button in the top-right corner that, when clicked, evaluates an expression to set modalOpen to false. The show class on our wrapper div will consequentially be removed, which means the display CSS property will return to none, thus removing the modal from the page.

index.html:

```
<div id="modal" v-bind:class="{ show: modalOpen }">
    <button v-on:click="modalOpen = false" class="modal-close">
        &times;
    </button>
    <div class="modal-content">
        <img src="image/header.jpg"/>
    </div>
</div>
```

style.css:

```
.modal-close {
    position: absolute;
    right: 0;
    top: 0;
    padding: 0px 28px 8px;
    font-size: 4em;
    width: auto;
    height: auto;
    background: transparent;
    border: 0;
    outline: none;
    color: #ffffff;
    z-index: 1000;
    font-weight: 100;
    line-height: 1;
}
```

### 2.17.1 Escape key

Having a close button for our modal is handy, but most people's instinctual action for closing a window is the Escape key. v-on is Vue's mechanism for listening to events and seems like a good candidate for this job. Adding the keyup argument will trigger a handler callback after any key is pressed while this input is focused:

    <input v-on:keyup="handler">

### 2.17.2 Event modifiers

Vue makes it easy to listen for specific keys by offering modifiers to the v-on directive. Modifiers are postfixes denoted by a dot (.), for example:

    <input v-on:keyup.enter="handler">

As you'd probably guess, the .enter modifier tells Vue to only call the handler when the event is triggered by the Enter key. Modifiers save you from having to remember the specific key code, and also make your template logic more obvious. Vue offers a variety of other key modifiers, including: 1) tab. 2) delete. 3) space. 4) esc. With that in mind, it seems like we could close our modal with this directive:

    v-on:keyup.esc="modalOpen = false"

But then what tag do we attach this directive to? Unfortunately, unless an input is focused on, key events are dispatched from the body element, which, as we know, is out of Vue's jurisdiction! To handle this event we'll, once again, resort to the Web API.

app.js:

```
var app = new Vue({ ... }); 

document.addEventListener('keyup', function(evt) {
    if (evt.keyCode === 27 && vm.modalOpen) {
        vm.modalOpen = false;
    }
});
```

1『函数的第一个传参如果用原书里的「\</span>'keyup'」会报错，目前还没解决。』

This works, with one caveat (discussed in the next section). But Vue can help us make it perfect.

## 2.18 Lifecycle hooks

When your main script is run and your instance of Vue is set up, it goes through a series of initialization steps. As we said earlier, Vue will walk through your data objects and make them reactive, as well as compile the template and mount to the DOM. Later in the lifecycle, Vue will also go through updating steps, and later still, tear-down steps. Here is a diagram of the lifecycle instance taken from http://vuejs.org. Many of these steps concern concepts that we haven't yet covered, but you should get the gist:

Figure 2.11. Vue.js lifecycle diagram

Vue allows you to execute custom logic at these different steps via lifecycle hooks, which are callbacks defined in the configuration object. For example, here we utilize the beforeCreate and created hooks:

```js
new Vue({ 
data: { message: 'Hello' }, 
beforeCreate: function() { 
    console.log('beforeCreate message: ' + this.message); // "beforeCreate message: undefined" 
}, 
created: function() { 
    console.log('created: '+ this.message); // "created message: Hello" 
}, 
});
```

Vue will alias data properties to the context object after the beforeCreate hook is called but before the created hook is called, hence why this.message is undefined in the former.

The caveat I mentioned earlier about the Escape key listener is this: although unlikely, if the Escape key was pressed and our callback was called before Vue has proxied the data properties, app.modalOpen would be undefined rather than true and so our if statement would not control flow like we expect. To overcome this we can set up the listener in the created lifecycle hook that will be called after Vue has proxied the data properties. This gives us a guarantee that modalOpen will be defined when the callback is run.

app.js:

```js
// to set up the listener in the created lifecycle
function escapeKeyListenser(evt) {
    if (evt.keyCode === 27 && vm.modalOpen) {
        vm.modalOpen = false;
    }
}

// Vue 实例
var vm = new Vue({
    el: "#app",
    data: {
        title: sample.title,
        address: sample.address,
        about: sample.about,
        headerImageStyle: {
            "background-image": "url('image/header.jpg')"
        },
        amenities: sample.amenities,
        prices: sample.prices,
        contracted: true,
        modalOpen: false,
    },
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
    created: function() {
        document.addEventListener('keyup', escapeKeyListenser);
    },
});
```

## 2.19 Methods

The Vue configuration object also has a section for methods. Methods are not reactive, so you could define them outside of the Vue configuration without any difference in functionality, but the advantage to Vue methods is that they are passed the Vue instance as context and therefore have easy access to your other properties and methods. Let's refactor our escapeKeyListener to be a Vue instance method.

app.js:

```
// Vue 实例
var vm = new Vue({
    el: "#app",
    data: {
        title: sample.title,
        address: sample.address,
        about: sample.about,
        headerImageStyle: {
            "background-image": "url('image/header.jpg')"
        },
        amenities: sample.amenities,
        prices: sample.prices,
        contracted: true,
        modalOpen: false,
    },
    methods: {
        escapeKeyListenser: function(evt) {
            if (evt.keyCode === 27 && this.modalOpen) {
                vm.modalOpen = false;
            }
        }
    },
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
    created: function() {
        document.addEventListener('keyup', this.escapeKeyListenser);
    },
});
```

1『留意下「this.escapeKeyListenser」。』

### 2.19.1 Proxied properties

You may have noticed that our escapeKeyListener method can refer to this.modalOpen. Shouldn't it be this.methods.modalOpen?

When a Vue instance is constructed, it proxies any data properties, methods, and computed properties to the instance object. This means that from within any method you can refer to this.myDataProperty, this.myMethod, and so on, rather than this.data.myDataProperty or this.methods.myMethod, as you might assume:

```
var app = new Vue({ data: { myDataProperty: 'Hello' }, methods: { myMethod: function() { return this.myDataProperty + ' World'; } } }); console.log(app.myMethod()); // Output: 'Hello World'
```

You can see these proxied properties by printing the Vue object in the browser console:

Figure 2.12. Our app's Vue instance

Now the simplicity of text interpolations might make more sense, they have the context of the Vue instance, and thanks to proxied properties, can be referenced like {{ myDataProperty }}. However, while proxying to the root makes syntax terser, a consequence is that you can't name your data properties, methods, or computed properties with the same name!

### 2.19.2 Removing listener

To avoid any memory leaks, we should also use removeEventListener to get rid of the listener when the Vue instance is torn down. We can use the destroy hook and call our escapeKeyListener method for this purpose.

```js
destoryed: function() {
    document.removeEventListener('keyup', this.escapeKeyListenser);
}
```

## Summary

In this chapter, we got familiar with the essential features of Vue including installation and basic configuration, data binding, text interpolation, directives, methods, watchers and lifecycle hooks. We also learned about Vue's inner workings, including the reactivity system.

We then used this knowledge to set up a basic Vue project and create page content for the Vuebnb prototype with text, lists of information, a header image, and UI widgets like the show more button and the modal window.

In the next chapter, we'll take a brief break from Vue while we set up a backend for Vuebnb using Laravel.
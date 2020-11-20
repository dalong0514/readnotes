# 2020121Full-Stack-Vuejs2-R01

## 记忆时间

## 0201. Prototyping Vuebnb, Your First Vue.js Project

In this chapter, we will learn the basic features of Vue.js. We'll then put this knowledge into practice by building a prototype of the case-study project, Vuebnb.

Topics this chapter covers: 1) Installation and basic configuration of Vue.js. 2) Vue.js essential concepts, such as data binding, directives, watchers and lifecycle hooks. 3) How Vue's reactivity system works. 4) Project requirements for the case-study project. 5) Using Vue.js to add page content including dynamic text, lists, and a header image. 6) Building an image modal UI feature with Vue.

### Summary

In this chapter, we got familiar with the essential features of Vue including installation and basic configuration, data binding, text interpolation, directives, methods, watchers and lifecycle hooks. We also learned about Vue's inner workings, including the reactivity system. We then used this knowledge to set up a basic Vue project and create page content for the Vuebnb prototype with text, lists of information, a header image, and UI widgets like the show more button and the modal window. In the next chapter, we'll take a brief break from Vue while we set up a backend for Vuebnb using Laravel.

### 2.3 NPM install

You'll now need to install the third-party scripts used in this project, including Vue.js itself. The NPM install method will read the included package.json file and download the required modules:

    $ npm install

You'll now see a new node\_modules directory has appeared in your project folder.

#### 2.3.1 Main files

Open the vuebnb-prototype directory in your IDE. Note that the following index.html file is included. It's mostly comprised of boilerplate code, but also has some structural markup included in the body tag. Also note that this file links to style.css, where our CSS rules will be added, and app.js, where our JavaScript will be added.

#### 2.3.2 Installing Vue.js

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

### 2.6 Data binding

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

### 2.7 Mock listing

While we're developing, it'd be nice to work with some mock data so that we can see how our completed page will look. I've included sample/data.js in the project for this very reason. Let's load it in our document, making sure it goes above our app.js file.

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

### 2.8 Header image

No room listing would be complete without a big, glossy image to show it off. We've got a header image in our mock listing that we'll now include. Add this markup to the page.

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

### 2.9 Style binding

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

### 2.10 Directives

#### 2.10.1 Usage

Just like normal HTML attributes, directives are usually name/value pairs in the form name="value". To use a directive, simply add it to an HTML tag as you would an attribute, for example:

```html
<p v-directive="value">
```

#### 2.10.2 Expressions

If a directive requires a value, it will be an expression. In the JavaScript language, expressions are small, evaluable statements that produce a single value. Expressions can be used wherever a value is expected, for example in the parenthesis of an if statement:

```js
if (expression) { 
    ... 
}
```

The expression here could be any of the following: 1) A mathematical expression, for example x + 7. 2) A comparison, for example v <= 7. 3) A Vue data property, for example this.myval. Directives and text interpolations both accept expression values:

```html
<div v-dir="someExpression">
    {{ firstName + " " + lastName }}
</div>
```

#### 2.10.3 Example: v-if

v-if will conditionally render an element if its value is a truthy expression. In the following case, v-if will remove/insert the p element depending on the myval value:

```html
<div id="app"> <p v-if="myval">Hello Vue</p> </div> <script> var app = new Vue({ el: '#app', data: { myval: true } }); </script>
```

Will renders as:

```html
<div id="app"> <p>Hello Vue</p> </div>
```

If we add a consecutive element with the v-else directive (a special directive that requires no value), it will be symmetrically removed/inserted as myval changes:

```html
<p v-if="myval">Hello Vue</p> <p v-else>Goodbye Vue</p>
```

#### 2.10.4 Arguments

Some directives take an argument, denoted by a colon after the directive name. For example, the v-on directive, which listens to DOM events, requires an argument to specify which event should be listened to:

```html
<a v-on:click="doSomething">
```

Instead of click, the argument could be mouseenter, keypress, scroll, or any other event (including custom events).

1『形成条件反射，指令后面有冒号 : 的话，后面的是要传递给该指令的参数。』

#### 2.10.5 Style binding (continued)

Coming back to our header image, we can use the v-bind directive with the style argument to bind a value to the style attribute.

index.html:

```html
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

Inspect the page with your browser Dev Tools and notice how the v-bind directive has evaluated:

```html
<div class="header-img" style="background-image: url('sample/header.jpg');"></div>
```

### 2.11 Lists section

The next bit of content we'll add to our page is the Amenities and Prices lists:

If you look at the mock-listing sample, you'll see that the amenities and prices properties on the object are both arrays.

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

#### 2.11.1 List rendering

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

#### 2.11.2 Icons

The second property of our amenity objects is icon. This is actually a class relating to an icon in the Font Awesome icon font. We've installed Font Awesome as an NPM module already, so add this to the head of the page to now use it.

3『

[How to use Font Awesome 5 on VueJS Project - Frontend Weekly - Medium](https://medium.com/front-end-weekly/how-to-use-fon-awesome-5-on-vuejs-project-ff0f28310821)

如何使用 Font Awesome 待实现。

』

#### 2.11.3 Key

As you might expect, the DOM nodes generated by v-for="amenity in amenities" are reactively bound to the amenities array. If the content of amenities changes, Vue will automatically re-render the nodes to reflect the change. When using v-for, it's recommended you provide a unique key property to each item in the list. This allows Vue to target the exact DOM nodes that need to be changed, making DOM updates more efficient. Usually, the key would be a numeric ID, for example:

```html
<div v-for="item in items" v-bind:key="item.id"> 
    {{ item.title }} 
</div>
```

1『跟小程序一样一样的。』

For the amenities and prices lists, the content is not going to change over the life of the app, so there's no need for us to provide a key. Some linters may warn you about this, but in this case, the warning can be safely ignored.

#### 2.11.4 Prices

Let's now add the price list to our template as well. I'm sure you'll agree that looping a template is far easier than writing out every item. However, you may notice that there is still some common markup between these two lists. Later in the book we'll utilize components to make this part of the template even more modular.

### 2.12 Show more feature

We've run into a problem now that the lists section is after the About section. The About section has an arbitrary length, and in some of the mock listings that we'll add you'll see that this section is quite long. We don't want it to dominate the page and force the user to do a lot of unwelcome scrolling to see the lists section, so we need a way to hide some of the text if it's too long, yet allow the user to view the full text if they choose. Let's add a show more UI feature that will crop the About text after a certain length and give the user a button to reveal the hidden text:

We'll start by adding a contracted class to the p tag that contains the about text interpolation. The CSS rule for this class will restrict its height to 250 pixels and hide any text overflowing the element.

```html
<div class="about">
    <h3>About this listing</h3>
    <p class="contracted">{{ about }}</p>
    <button class="more">+ More</button>
</div>
```

```css
.about p.contracted {
    height: 250px;
    overflow: hidden;
}
```

We'll also put a button after the p tag that the user can click to expand the section to full height. Here's the CSS that's needed, including a generic button rule that will provide base styling for all buttons that we'll add throughout the project.

#### 2.12.1 Class binding

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

#### 2.12.2 Event listener

We now want to remove the contracted class automatically when the user clicks the More button. To do this job, we'll use the v-on directive, which listens to DOM events with a click argument. The value of the v-on directive can be an expression that assigns contracted to false.

index.html:

```html
<div class="about">
    <h3>About this listing</h3>
    <p v-bind:class="{contracted: contracted}">{{ about }}</p>
    <button class="more" v-on:click="contracted = false">+ More</button>
</div
```

### 2.13 Reactivity

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

#### 2.13.1 Reactive data properties

Another one of Vue's initialization steps is to walk through all of the data properties and assign them getters and setters. If you look in the following screenshot, you can see how each property in our current app has a get and set function added to it:

Vue added these getters and setters to enable it to perform dependency tracking and change notification when the properties are accessed or modified. So, when the contracted value is changed by the click event, its set method is triggered. The set method will set the new value, but will also carry out a secondary task of informing Vue that a value has changed and any part of the page relying on it may need to be re-rendered.

#### 2.13.2 Hiding the More button

Once the About section has been expanded, we want to hide the More button as it's no longer needed. We can use the v-if directive to achieve this in conjunction with the contracted property.

```html
<button v-if="contracted" class="more" v-on:click="contracted = false">
    + More
</button>
```

### 2.14 Image modal window

To prevent our header image from dominating the page, we've cropped it and limited its height. But what if the user wants to see the image in its full glory? A great UI design pattern to allow the user to focus on a single item of content is a modal window. Here's what our modal will look like when opened:

Our modal will give a properly scaled view of the header image so the user can focus on the appearance of the lodgings without the distraction of the rest of the page. Later in the book, we will insert an image carousel into the modal so the user can browse through a whole collection of room images!

For now, though, here are the required features for our modal: 1) Open the modal by clicking the header image. 2) Freeze the main window. 3) Show the image. 3) Close the modal window with a close button or the Escape key.

#### 2.14.1 Opening

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

```html
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

#### 2.14.2 Window

Let's now add markup for the window that will be overlaid on our background panel. The window will have a width constraint and will be centered in the viewport.

#### 2.14.3 Disabling the main window

When the modal is open, we want to prevent any interaction with the main window and also make a clear distinction between the main window and the child window. We can do this by: 1) Dimming the main window. 2) Preventing body scroll.

 Dimming the main window. We could simply hide our main window when the modal is open, but it's better if the user can still be aware of where they are in flow of the app. To achieve this, we will dim the main window under a semi-transparent panel. We can do this by giving our modal panel an opaque black background.

```css
#modal { 
    ... 
    background-color: rgba(0,0,0,0.85); 
}
```

1『

点详细图一直出不来，这个问题卡了很久。最后通过对比作者样式的源码，发现需要添加如下代码。（2020-04-24）

```css
#modal.show {
    display: block;
}
```

』

Preventing body scroll. We have a problem, though. Our modal panel, despite being full screen, is still a child of the body tag. This means we can still scroll the main window! We don't want users to interact with the main window in any way while the modal is open, so we must disable scrolling on the body.

The trick is to add the CSS overflow property to the body tag and set it to hidden. This has the effect of clipping any overflow (that is, part of the page not currently in view), and the rest of the content will be made invisible. We'll need to dynamically add and remove this CSS rule, as we obviously want to be able to scroll through the page when the modal is closed. So, let's create a class called modal-open that we can apply to the body tag when the modal is open.

```css
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

### 2.15 Vue's mount element

What if we just mounted Vue on the body tag, wouldn't that solve our problems? For example:

    new Vue({ el: 'body' });

This is not permitted by Vue and if you attempt it you will get this error: 

    Do not mount Vue to <html> or <body> - mount to normal elements instead.

Remember that Vue has to compile the template and replaces the mount node. If you have script tags as children of the mount node, as you often do with body, or if your user has browser plugins that modify the document (many do) then all sorts of hell might break loose on the page when it replaces that node. If you define your own root element with a unique ID, there should be no such conflict.

1『上面的是一个关键知识点。vue 是不能挂在 body 或 html 跟节点上的。』

### 2.16 Watchers

So, how can we add/remove classes from the body if it's out of Vue's dominion? We'll have to do it the old-fashioned way with the browser's Web API. We need to run the following statements when the modal is opened or closed:

```html
// Modal opens 
document.body.classList.add('modal-open'); 

// Modal closes 
document.body.classList.remove('modal-closed');
```

As discussed, Vue adds reactive getters and setters to each data property so that when data changes it knows to update the DOM appropriately. Vue also allows you to write custom logic that hooks into reactive data changes via a feature called watchers.

1『如何对跟 vue 实例平行的节点操作，还是得靠 DOM 的 API，但前提是 vue 能告知 DOM 相关信息，watcher 就是做这个的。』

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

### 2.17 Closing

Users will need a way to close their modal and return to the main window. We'll overlay a button in the top-right corner that, when clicked, evaluates an expression to set modalOpen to false. The show class on our wrapper div will consequentially be removed, which means the display CSS property will return to none, thus removing the modal from the page.

#### 2.17.1 Escape key

Having a close button for our modal is handy, but most people's instinctual action for closing a window is the Escape key. v-on is Vue's mechanism for listening to events and seems like a good candidate for this job. Adding the keyup argument will trigger a handler callback after any key is pressed while this input is focused:

    <input v-on:keyup="handler">

#### 2.17.2 Event modifiers

Vue makes it easy to listen for specific keys by offering modifiers to the v-on directive. Modifiers are postfixes denoted by a dot (.), for example:

```html
<input v-on:keyup.enter="handler">
```

As you'd probably guess, the .enter modifier tells Vue to only call the handler when the event is triggered by the Enter key. Modifiers save you from having to remember the specific key code, and also make your template logic more obvious. Vue offers a variety of other key modifiers, including: 1) tab. 2) delete. 3) space. 4) esc. With that in mind, it seems like we could close our modal with this directive:

```html
v-on:keyup.esc="modalOpen = false"
```

But then what tag do we attach this directive to? Unfortunately, unless an input is focused on, key events are dispatched from the body element, which, as we know, is out of Vue's jurisdiction! To handle this event we'll, once again, resort to the Web API.

app.js:

```js
var app = new Vue({ ... }); 

document.addEventListener('keyup', function(evt) {
    if (evt.keyCode === 27 && vm.modalOpen) {
        vm.modalOpen = false;
    }
});
```

1『函数的第一个传参如果用原书里的「\</span>'keyup'」会报错，是印刷的原因，有些地方会多出字符 \</span>，后面章节还会遇到。』

This works, with one caveat (discussed in the next section). But Vue can help us make it perfect.

### 2.18 Lifecycle hooks

When your main script is run and your instance of Vue is set up, it goes through a series of initialization steps. As we said earlier, Vue will walk through your data objects and make them reactive, as well as compile the template and mount to the DOM. Later in the lifecycle, Vue will also go through updating steps, and later still, tear-down steps. Here is a diagram of the lifecycle instance taken from http://vuejs.org. Many of these steps concern concepts that we haven't yet covered, but you should get the gist:

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

2『上面的代码有时间码一遍。』

Vue will alias data properties to the context object after the beforeCreate hook is called but before the created hook is called, hence why this.message is undefined in the former.

The caveat I mentioned earlier about the Escape key listener is this: although unlikely, if the Escape key was pressed and our callback was called before Vue has proxied the data properties, app.modalOpen would be undefined rather than true and so our if statement would not control flow like we expect. To overcome this we can set up the listener in the created lifecycle hook that will be called after Vue has proxied the data properties. This gives us a guarantee that modalOpen will be defined when the callback is run.

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

### 2.19 Methods

The Vue configuration object also has a section for methods. Methods are not reactive, so you could define them outside of the Vue configuration without any difference in functionality, but the advantage to Vue methods is that they are passed the Vue instance as context and therefore have easy access to your other properties and methods. Let's refactor our escapeKeyListener to be a Vue instance method.

```js
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
            if (evt.keyCode === 27 && vm.modalOpen) {
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

#### 2.19.1 Proxied properties

You may have noticed that our escapeKeyListener method can refer to this.modalOpen. Shouldn't it be this.methods.modalOpen?

When a Vue instance is constructed, it proxies any data properties, methods, and computed properties to the instance object. This means that from within any method you can refer to this.myDataProperty, this.myMethod, and so on, rather than this.data.myDataProperty or this.methods.myMethod, as you might assume: 

You can see these proxied properties by printing the Vue object in the browser console. Now the simplicity of text interpolations might make more sense, they have the context of the Vue instance, and thanks to proxied properties, can be referenced like {{ myDataProperty }}. However, while proxying to the root makes syntax terser, a consequence is that you can't name your data properties, methods, or computed properties with the same name!

1『 When a Vue instance is constructed, it proxies any data properties, methods, and computed properties to the instance object. 代理机制解答了之前的困惑，数据绑定直接写属性名即可。』

#### 2.19.2 Removing listener

To avoid any memory leaks, we should also use removeEventListener to get rid of the listener when the Vue instance is torn down. We can use the destroy hook and call our escapeKeyListener method for this purpose.

```js
destoryed: function() {
    document.removeEventListener('keyup', this.escapeKeyListenser);
}
```

## 0301. Setting Up a Laravel Development Environment

In the first two chapters of the book, we introduced Vue.js. You should now be pretty comfortable with its basic features. In this chapter, we'll get a Laravel development environment up and running as we prepare to build the Vuebnb backend.

Topics covered in this chapter: 1) A brief introduction to Laravel. 2) Setting up the Homestead virtual development environment. 3) Configuring Homestead to host Vuebnb.

### Summary

In this brief chapter, we discussed the requirements for developing a Laravel project. We then installed and configured the Homestead virtual development environment to host our main project, Vuebnb. In the next chapter, we will begin work on our main project by building a web service to supply data to the frontend of Vuebnb.

### 3.1 Laravel

Laravel is an open source MVC framework for PHP that is used to build robust web applications. Laravel is currently at version 5.5 and is among the most popular PHP frameworks, beloved for its elegant syntax and powerful features. Laravel is suitable for creating a variety of web-based projects, such as the following: 1) Websites with user authentication, such as a customer portal or a social network. 2) Web applications, such as an image cropper or a monitoring dashboard. 3) Web services, such as RESTful APIs.

### 3.2 Laravel and Vue

Laravel may seem like a monolithic framework because it includes features for building almost any kind of web application. Under the hood, though, Laravel is a collection of many separate modules, some developed as part of the Laravel project and some from third-party authors. Part of what makes Laravel great is its careful curation and seamless connection of these constituent modules.

Since Laravel version 5.3, Vue.js has been the default frontend framework included in a Laravel installation. There's no official reason why Vue was chosen over other worthy options, such as React, but my guess is that it's because Vue and Laravel share the same philosophy: simplicity and an emphasis on the developer experience. Whatever the reason, Vue and Laravel offer an immensely powerful and flexible full-stack framework for developing web applications.

### 3.3 Environment

We'll be using Laravel 5.5 for the backend of Vuebnb. This version of Laravel requires PHP 7, several PHP extensions, and the following software: 1) Composer. 2) A web server, such as Apache or Nginx. 3) A database, such as MySQL or MariaDB.

Rather than manually installing the Laravel requirements on your computer, I strongly recommend you use the Homestead development environment, which has everything you need pre-installed.

1『已经好几个地方看到推荐用 Homestead 开发环境了。』

### 3.4 Homestead

Laravel Homestead is a virtual web application environment which runs on Vagrant and VirtualBox and can be run on any Windows, Mac, or Linux system. Using Homestead will save you the headache of setting up an development environment from scratch. It will also ensure you have an identical environment to the one I'm using, which will make it easier for you to follow along with this book. If you don't have Homestead installed on your computer, follow the directions in the Laravel documentation: https://laravel.com/docs/5.5/homestead. Use the default configuration options. Once you've installed Homestead and launched the Vagrant box with the vagrant up command, you're ready to continue.

### 3.5 Vuebnb

In Chapter 2, Prototyping Vuebnb, Your First Vue.js Project, we made a prototype of the frontend of Vuebnb. The prototype was created from a single HTML file that we loaded directly from the browser. Now we'll start working on the full-stack Vuebnb project, of which the prototype will soon be a critical part. This main project will be a full Laravel installation with a web server and database.

1『后面的几个小结都是有关 Homestead 配置的，目前用不到。』

## 0401. Building a Web Service with Laravel

In the last chapter, we got the Homestead development environment up and running, and began serving the main Vuebnb project. In this chapter, we will create a simple web service that will make Vuebnb's room listing data ready for display in the frontend.

Topics covered in this chapter: 1) Using Laravel to create a web service. 2) Writing database migrations and seed files. 3) Creating API endpoints to make data publicly accessible. 4) Serving images from Laravel.

### Summary

In this chapter, we built a web service with Laravel to make the Vuebnb listing data publicly accessible. This involved setting up a database table using a migration and schema, then seeding the database with mock listing data. We then created a public interface for the web service using routes. This returned the mock data as a JSON payload, including links to our mock images. In the next chapter, we'll introduce Webpack and the Laravel Mix build tool to set up a full-stack development environment. We'll migrate the Vuebnb prototype into the project, and refactor it to fit the new workflow.

### 4.1 Vuebnb room listings

In Chapter 2, Prototyping Vuebnb, Your First Vue.js Project, we built a prototype of the listing page of the frontend app. Soon we'll be removing the hardcoded data on this page and turning it into a template that can display any room listing.

We won't be adding functionality for a user to create their own room listing in this book. Instead, we'll use a package of mock data comprising 30 different listings, each with their own unique titles, descriptions, and images. We will seed the database with these listings and configure Laravel to serve them to the frontend as required.

### 4.2 Web service

A web service is an application that runs on a server and allows a client (such as a browser) to remotely write/retrieve data to/from the server over HTTP. The interface of a web service will be one or more API endpoints, sometimes protected with authentication, that will return data in an XML or JSON payload:

Web services are a speciality of Laravel, so it won't be hard to create one for Vuebnb. We'll use routes for our API endpoints and represent the listings with Eloquent models that Laravel will seamlessly synchronize with the database: API Routes, Model, Database.

Laravel also has inbuilt features to add API architectures such as REST, though we won't need this for our simple use case.

### 4.3 Mock data

The mock listing data is in the file database/data.json. This file includes a JSON-encoded array of 30 objects, with each object representing a different listing. Having built the listing page prototype, you'll no doubt recognize a lot of the same properties on these objects, including the title, address, and description. database/data.json:

Each mock listing includes several images of the room as well. Images aren't really part of a web service, but they will be stored in a public folder in our app to be served as needed. The image files are not in the project code, but are in the code base we downloaded from GitHub. We'll copy them into our project folder later in the chapter.

2『源码里的「data.json」复制进「database」文件夹。』

### 4.4 Database

Our web service will require a database table for storing the mock listing data. To set this up we'll need to create a schema and migration. We'll then create a seeder that will load and parse our mock data file and insert it into the database, ready for use in the app.

### 4.5 Migration

A migration is a special class that contains a set of actions to run against the database, such as creating or modifying a database table. Migrations ensure your database gets set up identically every time you create a new instance of your app, for example, installing in production or on a teammate's machine. To create a new migration, use the make:migration Artisan CLI command. The argument of the command should be a snake-cased description of what the migration will do:

    $ php artisan make:migration create_listings_table

You'll now see your new migration in the database/migrations directory. You'll notice the filename has a prefixed timestamp, such as 2017_06_20_133317_create_listings_table.php. The timestamp allows Laravel to determine the proper order of the migrations, in case it needs to run more than one at a time.

Your new migration declares a class that extends Migration. It overrides two methods: up, which is used to add new tables, columns, or indexes to your database; and down, which is used to delete them. We'll implement these methods shortly.

### 4.6 Schema

A schema is a blueprint for the structure of a database. For a relational database such as MySQL, the schema will organize data into tables and columns. In Laravel, schemas are declared by using the Schema facade's create method.

1『 laravel 建数据表是通过 facade 的 create() 方法。Facade 在这里的应用是一个面向对象设计的一种模式，目前还无法理解是哪种模式以及如何实现的。（2020-04-30）』

We'll now make a schema for a table to hold Vuebnb listings. The columns of the table will match the structure of our mock listing data. Note that we set a default false value for the amenities and allow the prices to have a NULL value. All other columns require a value. The schema will go inside our migration's up method. We'll also fill out the down with a call to Schema::drop.

2017_06_20_133317_create_listings_table.php:

```php
public function up()
{
    Schema::create('listings', function (Blueprint $table) {
        $table->primary('id');
        $table->unsignedInteger('id');
        $table->string('title');
        $table->string('address');
        $table->longText('about');

        // Amenities
        $table->boolean('amenity_wifi')->default(false);
        $table->boolean('amenity_pets_allowed')->default(false);
        $table->boolean('amenity_tv')->default(false);
        $table->boolean('amenity_kitchen')->default(false);
        $table->boolean('amenity_breakfast')->default(false);
        $table->boolean('amenity_laptop')->default(false);

        // Prices
        $table->string('price_per_night')->nullable();
        $table->string('price_extra_people')->nullable();
        $table->string('price_weekly_discount')->nullable();
        $table->string('price_monthly_discount')->nullable();
    });
}

/**
 * Reverse the migrations.
 *
 * @return void
 */
public function down()
{
    Schema::drop('listings');
}
```

A facade is an object-oriented design pattern for creating a static proxy to an underlying class in the service container. The facade is not meant to provide any new functionality; its only purpose is to provide a more memorable and easily readable way of performing a common action. Think of it as an object-oriented helper function.

### 4.7 Execution

Now that we've set up our new migration, let's run it with this Artisan command:

    $ php artisan migrate

You should see an output like this in the Terminal:

    Migrating: 2017_06_20_133317_create_listings_table Migrated: 2017_06_20_133317_create_listings_table

To confirm the migration worked, let's use Tinker to show the new table structure. If you've never used Tinker, it's a REPL tool that allows you to interact with a Laravel app on the command line. When you enter a command into Tinker it will be evaluated as if it were a line in your app code.

Firstly, open the Tinker shell:

    $ php artisan tinker

Now enter a PHP statement for evaluation. Let's use the DB facade's select method to run an SQL DESCRIBE query to show the table structure:

    >>>> DB::select('DESCRIBE listings;');

The output is quite verbose so I won't reproduce it here, but you should see an object with all your table details, confirming the migration worked.

### 4.8 Seeding mock listings

Now that we have a database table for our listings, let's seed it with the mock data. To do so we're going to have to do the following: 1) Load the database/data.json file. 2) Parse the file. 3) Insert the data into the listings table.

#### 4.8.1 Creating a seeder

Laravel includes a seeder class that we can extend called Seeder. Use this Artisan command to implement it:

    $ php artisan make:seeder ListingsTableSeeder

When we run the seeder, any code in the run method is executed.

database/ListingsTableSeeder.php:

```php
<?php

use Illuminate\Database\Seeder;

class ListingsTableSeeder extends Seeder
{
    /**
     * Run the database seeds.
     *
     * @return void
     */
    public function run()
    {
        //
    }
}
```

#### 4.8.2 Loading the mock data

Laravel provides a File facade that allows us to open files from disk as simply as File::get(\$path). To get the full path to our mock data file we can use the base\_path() helper function, which returns the path to the root of our application directory as a string.

It's then trivial to convert this JSON file to a PHP array using the built-in json_decode method. Once the data is an array, it can be directly inserted into the database given that the column names of the table are the same as the array keys.

database/ListingsTableSeeder.php:

```php
<?php

use Illuminate\Database\Seeder;
use Illuminate\Support\Facades\File;
use Illuminate\Support\Facades\DB;

class ListingsTableSeeder extends Seeder
{
    /**
     * Run the database seeds.
     *
     * @return void
     */
    public function run()
    {
        // load the file
        $path = base_path() . '/database/data.json';
        $file = File::get($path);
        $data = json_decode($file, true);

        // insert into the database
        DB::table('listings')->insert($data);
    }
}

```

1『从本地文件里读取数据写进数据库，可以借用上面的实现。注意前面的 use 引用需要的方法。借用上面的知识点实现了「数据流一体化」里将清洗好的数据写入数据库的环节。（2020-04-30）』

#### 4.8.3 Inserting the data

In order to insert the data, we'll use the DB facade again. This time we'll call the table method, which returns an instance of Builder. The Builder class is a fluent query builder that allows us to query the database by chaining constraints, for example, DB::table(...)->where(...)->join(...) and so on. Let's use the insert method of the builder, which accepts an array of column names and values.

1『上面给出了查询数据库的线索，可以深挖。』

#### 4.8.4 Executing the seeder

To execute the seeder we must call it from the DatabaseSeeder.php file, which is in the same directory.

database/seeds/DatabaseSeeder.php:

```php
<?php

use Illuminate\Database\Seeder;

class DatabaseSeeder extends Seeder
{
    /**
     * Seed the application's database.
     *
     * @return void
     */
    public function run()
    {
        // $this->call(UsersTableSeeder::class);
        $this->call(ListingsTableSeeder::class);
    }
}
```

With that done, we can use the Artisan CLI to execute the seeder:

    $ php artisan db:seed

You should see the following output in your Terminal:

    Seeding: ListingsTableSeeder

We'll again use Tinker to check our work. There are 30 listings in the mock data, so to confirm the seed was successful, let's check for 30 rows in the database:

```
$ php artisan tinker 
>>>> DB::table('listings')->count(); # Output: 30
```

Finally, let's inspect the first row of the table just to be sure its content is what we expect:

```
>>>> DB::table('listings')->get()->first();
```

### 4.9 Listing model

We've now successfully created a database table for our listings and seeded it with mock listing data. How do we access this data now from the Laravel app? We saw how the DB facade lets us execute queries on our database directly. But Laravel provides a more powerful way to access data via the Eloquent ORM.

1『直接查询数据库里的数据是用 tinker 结合 「DB facade」。』

### 4.10 Eloquent ORM

Object-Relational Mapping (ORM) is a technique for converting data between incompatible systems in object-oriented programming languages. Relational databases such as MySQL can only store scalar values such as integers and strings, organized within tables. We want to make use of rich objects in our app, though, so we need a means of robust conversion.

Eloquent is the ORM implementation used in Laravel. It uses the active record design pattern, where a model is tied to a single database table, and an instance of the model is tied to a single row. To create a model in Laravel using Eloquent ORM, simply extend the Illuminate\Database\Eloquent\Model class using Artisan:

    $ php artisan make:model Listing

This generates a new file.

app/Listing.php:

```php
<?php

namespace App;

use Illuminate\Database\Eloquent\Model;

class Listing extends Model
{
    //
}
```

How do we tell the ORM what table to map to, and what columns to include? By default, the Model class uses the class name (Listing) in lowercase (listing) as the table name to use. And, by default, it uses all the fields from the table. Now, any time we want to load our listings we can use code such as this, anywhere in our app:

### 4.11 Casting

The data types in a MySQL database don't completely match up to those in PHP. For example, how does an ORM know if a database value of 0 is meant to be the number 0, or the Boolean value of false? An Eloquent model can be given a \$casts property to declare the data type of any specific attribute. \$casts is an array of key/values where the key is the name of the attribute being cast, and the value is the data type we want to cast to.

For the listings table, we will cast the amenities attributes as Booleans.

app/Listing.php:

```php
<?php

namespace App;

use Illuminate\Database\Eloquent\Model;

class Listing extends Model
{
    protected $casts = [
        'amenity_wifi' => 'boolean',
        'amenity_pets_allowed' => 'boolean',
        'amenity_tv' => 'boolean',
        'amenity_kitchen' => 'boolean',
        'amenity_breakfast' => 'boolean',
        'amenity_laptop' => 'boolean'
    ];
}
```

Now these attributes will have the correct type, making our model more robust:

```php
echo gettype($listing->amenity_wifi()); // boolean
```

### 4.12 Public interface

The final piece of our web service is the public interface that will allow a client app to request the listing data. Since the Vuebnb listing page is designed to display one listing at a time, we'll at least need an endpoint to retrieve a single listing. Let's now create a route that will match any incoming GET requests to the URI /api/listing/{listing} where {listing} is an ID. We'll put this in the routes/api.php file, where routes are automatically given the /api/ prefix and have middleware optimized for use in a web service by default.

We'll use a closure function to handle the route. The function will have a \$listing argument, which we'll type hint as an instance of the Listing class, that is, our model. Laravel's service container will resolve this as an instance with the ID matching {listing}. We can then encode the model as JSON and return it as a response.

routes/api.php:

```php
Route::get('/listing/{listing}', function(ListingModel $listing) {
    return $listing->toJson();
```

We can test this works by using the curl command from the Terminal:

    $ curl http://vuebnb.test/api/listing/1

1『这个实现很赞，借鉴下。重点是那个闭包函数，特别是传参那块；之前一直获取不了数据，弄了半天找到原因，因为数据库连到了之前的「laravel」上，设置里更改数据后为「vuebnb」之后，一定要重启服务器，否则还是连到老的数据。』

### 4.13 Controller

We'll be adding more routes to retrieve the listing data as the project progresses. It's a best practice to use a controller class for this functionality to keep a separation of concerns. Let's create one with Artisan CLI:

    $ php artisan make:controller ListingController

We'll then move the functionality from the route into a new method, get\_listing\_api.

app/Http/Controllers/ListingController.php:

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Models\ListingModel;

class ListingController extends Controller
{
    public function get_listing_api(ListingModel $listing)
    {
        return $listing->toJson();
    }

    // test for require data by a function in model file
    public function get_listing()
    {
        $listing = ListingModel::getListing();
        return $listing->toJson();
    }
}
```

1『这里也试验了下之前常规获取数据的方法，在 model 文件里写一个方法专门提取数据库里的数据。』

For the Route::get method we can pass a string as the second argument instead of a closure function. The string should be in the form [controller]@[method], for example, ListingController@get_listing_web. Laravel will correctly resolve this at runtime.

routes/api.php:

```php
<?php Route::get('/listing/{listing}', 'ListingController@get_listing_api');
```

3『 [Database: Query Builder - Laravel - The PHP Framework For Web Artisans](https://laravel.com/docs/7.x/queries) 』

### 4.14 Images

As stated at the beginning of the chapter, each mock listing comes with several images of the room. These images are not in the project code and must be copied from a parallel directory in the code base called images. Copy the contents of this directory into the public/images folder:

1『把源码里的图片都移到自己的项目里。』

#### 4.14.1 Accessing images

Files in the public directory can be directly requested by appending their relative path to the site URL. For example, the default CSS file, public/css/app.css, can be requested at http://vuebnb.test/css/app.css. The advantage of using the public folder, and the reason we've put our images there, is to avoid having to create any logic for accessing them. A frontend app can then directly call the images in an img tag. You may think it's inefficient for our web server to serve images like this, and you'd be right. Later in the book, we'll serve the images from a CDN when in production mode. Let's try to open one of the mock listing images in our browser to test this thesis: 

http://vuebnb.test/images/1/Image_1.jpg

#### 4.14.2 Image links

The payload for each listing in the web service should include links to these new images so a client app knows where to find them. Let's add the image paths to our listing API payload so it looks like this:

```json
{ 
"id": 1, 
"title": "...",
"description": "...", 
... 
"image_1": "http://vuebnb.test/app/image/1/Image_1.jpg", 
"image_2": "http://vuebnb.test/app/image/1/Image_2.jpg", 
"image_3": "http://vuebnb.test/app/image/1/Image_3.jpg", 
"image_4": "http://vuebnb.test/app/image/1/Image_4.jpg" 
}
```

The thumbnail image won't be used until later in the project. To implement this, we'll use our model's toArray method to make an array representation of the model. We'll then easily be able to add new fields. Each mock listing has exactly four images, numbered 1 to 4, so we can use a for loop and the asset helper to generate fully-qualified URLs to files in the public folder. We finish by creating an instance of the Response class by calling the response helper. We use the json; method and pass in our array of fields, returning the result.

1『这就是之前自己一直想实现的，如何管理图片 URL，如何把这些信息做进对象数据里。』

3『 [Helpers - Laravel - The PHP Framework For Web Artisans](https://laravel.com/docs/7.x/helpers)

这里还获取了一个重要知识点，laravel 里有很多 helper 函数可以使用。比如 URLs 标签里的 asset()：

The asset function generates a URL for an asset using the current scheme of the request (HTTP or HTTPS):

```php
$url = asset('img/photo.jpg');
```

You can configure the asset URL host by setting the ASSET\_URL variable in your .env file. This can be useful if you host your assets on an external service like Amazon S3:

```php
// ASSET_URL=http://example.com/assets
$url = asset('img/photo.jpg'); // http://example.com/assets/img/photo.jpg
```

之前遇到七牛头 URL 在生产环境里替换不了的情况，想到的解决办法是声明一个常量，再字符串拼接。完全可以用上面的 asset() 函数实现，更简洁。（2020-05-01）

』

app/Http/Controllers/ListingController.php:

```php
public function get_listing_api(ListingModel $listing)
{
    $model = $listing->toArray();
    for ($i = 1; $i <=4; $i++) {
        $model['image_' . $i] = asset(
            'images/' . $listing->id . '/Image_' . $i . '.jpg');
    }
    return response()->json($model);
}
```

The /api/listing/{listing} endpoint is now ready for consumption by a client app.

1『

发现做出来的 url 里都多了反斜杠：

    "image_1":"http:\/\/localhost:8000\/images\/1\/Image_1.jpg"

感觉反斜杠只是转移字符，使用的时候是没有的，待确认。回复：的确是之前想的，转义字符显示，实际用的时候没有。（2020-05-01）

顺便搜了篇文章，有空看看：[Laravel’s URL::to() vs URL::asset() - Simon Wicki - Medium](https://medium.com/@zwacky/laravels-url-to-vs-url-asset-fd427ed6f7ef)

』

3『

```php
return response()->json($model);
```

这个语句引申出来的知识点：

[Returning JSON from a PHP Script - Stack Overflow](https://stackoverflow.com/questions/4064444/returning-json-from-a-php-script)

I want to return JSON from a PHP script. Do I just echo the result? Do I have to set the Content-Type header?

Reply: While you're usually fine without it, you can and should set the Content-Type header:

```php
<?PHP
$data = /** whatever you're serializing **/;
header('Content-Type: application/json');
echo json_encode($data);
```

If I'm not using a particular framework, I usually allow some request params to modify the output behavior. It can be useful, generally for quick troubleshooting, to not send a header, or sometimes print\_r the data payload to eyeball it (though in most cases, it shouldn't be necessary).

[HTTP Responses - Laravel - The PHP Framework For Web Artisans](https://laravel.com/docs/7.x/responses)

All routes and controllers should return a response to be sent back to the user's browser. Laravel provides several different ways to return responses. The most basic response is returning a string from a route or controller. The framework will automatically convert the string into a full HTTP response:

「最后的 return response() 是这个意思，路由和控制器得返回一个 response（数据）给浏览器。」

```php
Route::get('/', function () {
    return 'Hello World';
});
```

In addition to returning strings from your routes and controllers, you may also return arrays. The framework will automatically convert the array into a JSON response:

```php
Route::get('/', function () {
    return [1, 2, 3];
});
```

Typically, you won't just be returning simple strings or arrays from your route actions. Instead, you will be returning full Illuminate\Http\Response instances or views. Returning a full Response instance allows you to customize the response's HTTP status code and headers. A Response instance inherits from the Symfony\Component\HttpFoundation\Response class, which provides a variety of methods for building HTTP responses:

```php
Route::get('home', function () {
    return response('Hello World', 200)
                  ->header('Content-Type', 'text/plain');
});
```

上面的文档已存入「2020014laravel-document -> 2001-HTTP-Responses.md」，好好读读。

又看到一篇好文章：[How to Use JSON Data with PHP or JavaScript – Tania Rascia](https://www.taniarascia.com/how-to-use-json-data-with-php-or-javascript/)，以存入计算机类里的「2020碎片知识 -> 20200501How-to-Use-JSON-Data-with-PHP-or-JavaScript.md」。

As you can see, it's a human readable format of data that might traditionally be stored in a table. Some companies might have public .json files located that you can access and extract data from (an API you can connect to). You might also save a .json file somewhere in your project that you want to extract data from. Goals: JSON data can be accessed and utilized with many programming languages. In this tutorial, we'll learn how to access JSON with PHP and JavaScript.

详细的内容可以到消化后的「2020006IT碎片知识RS02.md」里看。

』

## 0501. Integrating Laravel and Vue.js with Webpack

In this chapter, we'll migrate the Vuebnb frontend prototype into our main Laravel project, achieving the first full-stack iteration of Vuebnb. This fully-integrated environment will include a Webpack build step, allowing us to incorporate more sophisticated tools and techniques as we continue to build the frontend.

Topics covered in this chapter: 1) An introduction to Laravel's out-of-the-box frontend app. 2) A high-level overview of Webpack. 3) How to configure Laravel Mix to compile frontend assets. 4) Migrating the Vuebnb prototype into the full-stack Laravel environment. 5) Using ES2015 with Vue.js, including syntax and polyfills for older browsers. 6) Switching hard-coded data in the frontend app to backend data.

### Summary

In this chapter, we got familiar with the files and configuration of Laravel's default frontend app. We then migrated the Vuebnb client app prototype into our Laravel project, achieving the first full-stack iteration of Vuebnb. We also learned about Webpack, seeing how it addresses the JavaScript dependency management problem by bundling modules into a browser-friendly build file. We set up Webpack in our project via Laravel Mix, which offers a simple API for common build scenarios. We then investigated tools for making our frontend development process easier, including Webpack watch mode and BrowserSync. Finally, we saw how to get data from the backend into the frontend app by injecting it into the document head.

In Chapter 6, Composing Widgets with Vue.js Components, we will be introduced to one of the most important and powerful tools for building user interfaces with Vue.js: components. We will build an image carousel for Vuebnb, and use knowledge of components to refactor the Vuebnb client app into a flexible component-based architecture.

### 5.1 Laravel frontend

We think of Laravel as being a backend framework, but a fresh Laravel project includes boilerplate code and configuration for a frontend app as well. The out-of-the-box frontend includes JavaScript and Sass asset files, as a well as a package.json file that specifies dependencies such as Vue.js, jQuery, and Bootstrap.

Let's take a look at this boilerplate code and configuration so we get an idea of how the Vuebnb frontend app will fit into our Laravel project when we begin the migration.

#### 5.1.1 JavaScript

JavaScript assets are kept in the resources/assets/js folder. There are several .js files in this directory, as well as a sub-directory component, with a .vue file. This latter file will be explained in another chapter so we'll ignore it for now. The main JavaScript file is app.js. You'll see the familiar Vue constructor in this file, but also some syntax that may not be as familiar. On the first line is a require function that is intended to import an adjacent file, bootstrap.js, which in turn loads other libraries including jQuery and Lodash.

1『几个重要的第三方 JS 库：jQuery、Lodash、Bootstrap、Vue。』

require is not a standard JavaScript function and must be resolved somehow before this code can be used in a browser.

resources/assets/js/app.js:

```js
require('./bootstrap'); 
window.Vue = require('vue'); 
Vue.component('example', require('./components/Example.vue')); 
const app = new Vue({ 
    el: '#app' 
});
```

#### 5.1.2 CSS

If you haven't heard of Sass before, it's a CSS extension that makes it easier to develop CSS. A default Laravel installation includes the resources/assets/sass directory, which includes two boilerplate Sass files. The main Sass file is app.scss. Its job is to import other Sass files including the Bootstrap CSS framework.

resources/assets/sass/app.scss:

```css
// Fonts 
@import url("https://fonts.googleapis.com/css?family=Raleway:300,400,600"); 

// Variables 
@import "variables"; 

// Bootstrap 
@import "~bootstrap-sass/assets/stylesheets/bootstrap";
```

#### 5.1.3 Node modules

Another key aspect of the Laravel frontend is the package.json file in the root of the project directory. Similar to composer.json, this file is used for configuration and dependency management, only for Node modules rather than PHP. One of the properties of package.json is devDependencies, which specifies the modules required in the development environment, including jQuery, Vue, and Lodash.

package.json:

```json
{ 
... 
"devDependencies": { 
    "axios": "^0.17", 
    "bootstrap-sass": "^3.3.7", 
    "cross-env": "^5.1", 
    "jquery": "^3.2", 
    "laravel-mix": "^1.4", 
    "lodash": "^4.17.4", 
    "vue": "^2.5.3" 
} 
}
```

#### 5.1.4 Views

To serve the frontend app with Laravel, it needs to be included in a view. The only out-of-the-box view provided is the welcome view, located at resources/views/welcome.blade.php, which is used as a boilerplate home page. The welcome view does not actually include the frontend app and it's left to the user to install it themselves. We'll look at how to do this later in the chapter.

#### 5.1.5 Asset compilation

The files in resources/assets include functions and syntax that can't be used directly in a browser. For example, the require method used in app.js, which is designed to import a JavaScript module, is not a native JavaScript method and is not part of the standard Web API:

A build tool is needed to take these asset files, resolve any non-standard functions and syntax, and output code that the browser can use. There are a number of popular build tools for frontend assets including Grunt, Gulp, and Webpack:

Figure 5.2. Asset compilation process

1『上面的图很形象，/resources 里的 Assets(JS, sass etc) 文件，需要通过一个「Build tool」转化为 /public 根目录下的「Browser bundle」，才能去前端显示。』

The reason we go to the effort of using this asset compilation process is so we can author our frontend app without the constraints of what a browser allows. We can introduce a variety of handy development tools and features that'll allow us to write our code and fix problems more easily.

### 5.2 Webpack

Webpack is the default build tool supplied with Laravel 5.5 and we'll be making use of it in the development of Vuebnb. What makes Webpack different to other popular build tools, such as Gulp and Grunt, is that it's first and foremost a module bundler. Let's begin our overview of Webpack by getting an understanding of how the module bundling process works.

#### 5.2.1 Dependencies

In a frontend application, we are likely to have dependencies for third-party JavaScript libraries or even other files in our own code base. For example, the Vuebnb prototype is dependent on Vue.js and the mock-listing data file:

There's no real way of managing these dependencies in a browser, other than to ensure any shared functions and variables have global scope and that scripts are loaded in the right order. For example, since node\_modules/vue/dist/vue.js defines a global Vue object and is loaded first, we're able to use the Vue object in our app.js script. If either of those conditions was not met, Vue would not be defined when app.js ran, resulting in an error:

```html
<script src="node_modules/vue/dist/vue.js"></script> 
<script src="sample/data.js"></script> 
<script src="app.js"></script>
```

This system has a number of downsides: 1) Global variables introduce possibilities of naming collisions and accidental mutations. 2) Script loading order is fragile and can be easily broken as the app grows. 3) We can't utilize performance optimizations, such as loading scripts asynchronously.

#### 5.2.2 Modules

A solution to the dependency management problem is to use a module system, such as CommonJS or native ES modules. These systems allow JavaScript code to be modularized and imported into other files. 

Here is a CommonJS example:

```js
// moduleA.js 
module.exports = function(value) { 
    return value * 2; 
} 

// moduleB.js 
var multiplyByTwo = require('./moduleA'); 
console.log(multiplyByTwo(2)); 
// Output: 4
```

And here is a Native ES modules example:

```js
// moduleA.js 
export default function(value) { 
    return value * 2; 
} 

// moduleB.js 
import multiplyByTwo from './moduleA';
console.log(multiplyByTwo(2));
// Output: 4
```

The problem is that CommonJS cannot be used in a browser (it was designed for server-side JavaScript) and native ES modules are only now getting browser support. If we want to use a module system in a project, we'll need a build tool: Webpack.

1『所以后面有一章里专门有个表，说说明了各个类型的 vue.js 内核支持哪种 Modules，是 CommonJS 还是 Native ES。本书的项目用的是 Native ES。』

#### 5.2.3 Bundling

The process of resolving modules into browser-friendly code is called bundling. Webpack begins the bundling process with the entry file as a starting point. In the Laravel frontend app, resources/assets/js/app.js is the entry file. Webpack analyzes the entry file to find any dependencies. In the case of app.js, it will find three: bootstrap, vue, and Example.vue.

resources/assets/js/app.js:

```js
require('./bootstrap'); 
window.Vue = require('vue'); 
Vue.component('example', require('./components/Example.vue')); ...
```

Webpack will resolve these dependencies and then analyze them to find any dependencies that they might have. This process continues until all dependencies of the project are found. The result is a graph of dependencies that, in a large project, might include hundreds of different modules. Webpack uses this graph of dependencies as a blueprint for bundling all the code into a single browser-friendly file:

```html
<script src="bundle.js"></script>
```

#### 5.2.4 Loaders

Part of what makes Webpack so powerful is that during the bundling process it can transform a module with one or more Webpack loaders. For example, Babel is a compiler that transforms next-generation JavaScript syntax such as ES2015 into standard ES5. The Webpack Babel loader is one of the most popular as it allows developers to write their code using modern features, but still provide support in older browsers.

1『 JS 的忍者秘籍里也有提到，新版本 JS 开发的东西可以自动转码到老的浏览器版本上使用，这是前端大发展的前提。』

For example, in the entry file, we see the ES2015 const declaration that isn't supported by IE10.

resources/assets/js/app.js:

```js
const app = new Vue({ 
    el: '#app' 
});
```

If the Babel loader is used, const will be transformed to var before it's added to the bundle.

public/js/app.js:

```js
var app = new Vue({ el: '#app' });
```

#### 5.2.5 Laravel Mix

One of the downsides of Webpack is that configuring it is arduous. To make thing easier, Laravel includes a module called Mix that takes the most commonly-used Webpack options and puts them behind a simple API.

1『原来 Mix 是为了解决 Webpack 配置难的痛点。』

The Mix configuration file can be found in the root of the project directory. Mix configuration involves chaining methods to the mix object that declare the basic build steps of your app. For example, the js method takes two arguments, the entry file and the output directory, and the Babel loader is applied by default. The sass method works in an equivalent way.

webpack.mix.js:

```js
let mix = require('laravel-mix'); 
mix.js('resources/assets/js/app.js', 'public/js') 
    .sass('resources/assets/sass/app.scss', 'public/css');
```

1『 JS 里的链式方法，记得「2020096JavaScript-The-Good-Parts」里有提到。』

### 5.3 Running Webpack

Now that we have a high-level understanding of Webpack, let's run it and see how it bundles the default frontend asset files. First, ensure you have all the development dependencies installed:

    $ npm install

#### 5.3.1. CLI

Webpack is typically runs from the command line, for example:

    $ webpack [options]

Rather than figuring out the correct CLI option ourselves, we can use one of the Weback scripts predefined in package.json. For example, the development script will run Webpack with options suitable for creating a development build.

#### 5.3.2 First build

Let's now run the dev script (a shortcut for the development script):

    $ npm run dev

After this runs, you should see an output in the Terminal similar to the following:

This output tells us a number of things, but most importantly that the build was successful and what files were created in the output including fonts, JavaScript, and CSS. Note that the output file path is relative not to the project root but to the public directory, so the js/apps.js file will be found at public/js/app.js.

#### 5.3.3 JavaScript

Inspecting the output JavaScript file, public/js/app.js, we see a whole lot of code in there - around 42,000 lines! That's because jQuery, Lodash, Vue, and the other JavaScript dependencies have all been bundled into this one file. It's also because we've used a development build that does not include minification or uglification. If you search through the file, you'll see that the code from our entry file, app.js, has been transpiled to ES5 as expected:

#### 5.3.4 CSS

We also have a CSS bundle file, public/css/app.css. If you inspect this file you will find the imported Bootstrap CSS framework has been included and the Sass syntax has been compiled to plain CSS.

#### 5.3.5 Fonts

You might think it's strange that there are fonts in the output, since Mix did not include any explicit font configuration. These fonts are dependencies of the Bootstrap CSS framework and Mix, by default, will output them individually rather than in a font bundle.

1『后面有个地方记录了如何安装字体以及图标，过程中踩过一些坑。』

### 5.4 Migrating Vuebnb

Now that we're familiar with the default Laravel frontend app code and configuration, we're ready to migrate the Vuebnb prototype into the main project. This migration will allow us to have all our source code in one place, plus we can utilize this more sophisticated development environment for building the remainder of Vuebnb.

The migration will involve: 1) Removing any unnecessary modules and files. 2) Moving the prototype files into the Laravel project structure. 3) Modifications to the prototype files to adapt them to the new environment.

1『图很形象，描述了要迁移的原始文件对应的目标文件：style.css->css、logo.png->images、app.js->js、index.html->views。』

#### 5.4.1 Removing unnecessary dependencies and files

Let's begin by removing the Node dependencies we no longer need. We'll keep axis as it'll be used in a later chapter, and cross-env because it ensures our NPM scripts can be run in a variety of environments. We'll get rid of the rest:

    $ npm uninstall bootstrap-sass jquery lodash --save-dev

1『原来可以同时卸载几个第三方库。』

This command will leave your dev dependencies looking like this. Next, we'll remove the files we don't need. This includes several of the JavaScript assets, all of the Sass plus the welcome view:

Since we're removing all the Sass files, we'll also need to remove the sass method in the Mix configuration.

webpack.mix.js:

```js
let mix = require('laravel-mix'); 
mix 
    .js('resources/assets/js/app.js', 'public/js') ;
```

Now our frontend app is free from clutter and we can move the prototype files into their new home.

#### 5.4.2 HTML

Let's now copy the contents of index.html from the prototype project we completed in Chapter 2, Prototyping Vuebnb, Your First Vue.js Project, into a new file, app.blade.php. This will allow the template to be used as a Laravel view:

We'll also update the home web route to point to this new view instead of welcome.

routes/web.php:

```php
<?php Route::get('/', function () { return view('app'); });
```

1『发现文件名中不能带 balde，否则渲染不了，只能还是 app.php。因为 vue 跟 blade 的语法冲突导致的，但其实可以加 balde，下面小结给出了解决办法：在所有绑定的数据前面加上 @ 即可解决。而且通过后面的学习，用单文件模式（SFC）时不存在这个问题，在 .vue 文件里绑定数据不需要加上 @。（2020-05-02）』

#### 5.4.3 Syntax clash

Using the prototype template file as a view will cause a small issue as Vue and Blade share a common syntax. For example, look at the heading section where Vue.js interpolates the title and address of a listing.

When Blade processes this, it will think the double curly brackets are its own syntax and will generate a PHP error as neither title nor address are defined functions. There is a simple solution: escape these double curly brackets to let Blade know to ignore them. This can be done by placing an @ symbol as a prefix.

resources/views/app.blade.php:

```html
<div class="heading"> 
    <h1>@{{ title }}</h1> 
    <p>@{{ address }}</p> 
</div>
```

Once you've done that for each set of double curly brackets in the file, load the home route in the browser to test the new view. Without the JavaScript or CSS it doesn't look great, but at least we can confirm it works:

#### 5.4.4 JavaScript

Let's now move the prototype's main script file, app.js, into the Laravel project:

Given the current Mix settings, this will now be the entry file of the JavaScript bundle. This means JavaScript dependencies at the bottom of the view can be replaced with the bundle, that is.

resources/views/app.blade.php:

```html
<script src="node_modules/vue/dist/vue.js"></script> 
<script src="sample/data.js"></script> 
<script src="app.js"></script>
```

Can be replaced with, resources/views/app.blade.php:

```html
<script src="{{ asset('js/app.js') }}"></script>
```

#### 5.4.5 Mock data dependency

Let's copy the mock data dependency into the project as well:

Currently, this file declares a global variable sample that is then picked up in the entry file. Let's make this file a module by replacing the variable declaration with an ES2015 export default.

resources/assets/js/data.js:

```
export default { ... }
```

1『

应用了下「重学前端」里获取的知识点，改进了下 data.js：

```js
var sample = {...}
export default sample;
```

』

We can now import this module at the top of our entry file. Note that Webpack can guess the file extension in an import statement so you can omit the .js from data.js.

resources/assets/js/app.js:

```js
import sample from './data'; 
var app = new Vue({ ... });
```

While Laravel has opted to use CommonJS syntax for including modules, that is require, we will use native ES module syntax, that is import. This is because ES modules are making their way into the JavaScript standard, and it's more consistent with the syntax used by Vue.

1『记住，native ES module syntax 更适合 vue。』

#### 5.4.6 Displaying modules with Webpack

Let's run a Webpack build to make sure the JavaScript migration is working so far:

    $ npm run dev

If all is well, you'll see the JavaScript bundle file being output:

It'd be nice to know that the mock data dependency was added without having to manually inspect the bundle to find the code. We can do this by telling Webpack to print the modules it has processed in the Terminal output. In the development script in our package.json, a --hide-modules flag has been set, as some developers prefer a succinct output message. Let's remove it for now and instead add the --display-modules flag, so the script looks like this:

```json
"scripts": { 
    ... 
    "development": "cross-env NODE_ENV=development node_modules/webpack/bin/webpack.js --progress --display-modules --config=node_modules/laravel-mix/setup/webpack.config.js", 
    ... 
}
```

1『上面的可以配置下，能显示更多的信息。』

#### 5.4.7 Vue.js dependency

Let's now import Vue.js as a dependency of our entry file.

resources/assets/js/app.js:

```js
import Vue from 'vue'; 
import sample from './data'; 

var app = new Vue({ ... });
```

3『2020006IT碎片知识RS02 >> 20200409Why-should-you-use-Vuejs-when-using-Laravel.md

报错，还好之前有研究过，得先安装 vue：

    yarn add vue

引入 vue 的话，书籍介绍的加上之前研究的，目前知道两种：

```
// 1
import Vue from 'vue';

// 2
window.Vue = require('vue')
```

用方法 1 的话，发现在 app.blade.php 里如果实例化另外一个 vue 实例时，报错：(index):52 Uncaught ReferenceError: Vue is not defined。也是的，因为另外的那个 vue 实例的 id 是 app1，在 app.js 里实例化的只有 app 那个实例。然而用方法 2 不会报错，本质原因还没弄明白。那么，能不能再另一个 js 文件里声明一个 vue 实例，然后在 app.js 里引用，或者直接在 app.js 里再声明一个，这样的话就可以通说 webpack 编译掉，待验证（2020-05-02）。

』

You may be wondering how import Vue from 'vue' resolves, as it doesn't seem to be a proper file reference. Webpack will, by default, check the node\_modules folder in the project for any dependencies, saving you from having to put import Vue from 'node\_modules/vue';.

But how, then, does it know the entry file of this package? Looking at the Webpack Terminal output in the preceding screenshot, you can see that it has included node\_modules/vue/dist/vue.common.js. It knows to use this file because, when Webpack is adding node modules as dependencies, it checks their package.json file and looks for the main property, which in the case of Vue is.

node_modules/vue/package.json:

```json
{ 
... 
"main": "dist/vue.runtime.common.js", 
... 
}
```

However, Laravel Mix overrides this to force a different Vue build.

node_modules/laravel-mix/setup/webpack.config.js:

```
alias: { 'vue$': 'vue/dist/vue.common.js' }
```

In short, import Vue from 'vue' is effectively the same as import Vue from 'node_modules/vue/dist/vue.common.js'. We'll explain the different Vue builds in Chapter 6, Composing Widgets with Vue.js Components. With that done, our JavaScript has been successfully migrated. Loading the home route again, we can better make out the listing page of Vuebnb with the JavaScript now included:

#### 5.4.8 CSS

To migrate CSS, we'll copy style.css from the prototype into the Laravel project. The default Laravel frontend app used Sass rather than CSS, so we'll need to make a directory for CSS assets first:

Let's then make a new declaration in our Mix config to get a CSS bundle using the styles method.

webpack.mix.js:

```js
mix 
    .js('resources/assets/js/app.js', 'public/js') 
    .styles('resources/assets/css/style.css', 'public/css/style.css') ;
```

We'll now link to the CSS bundle in our view by updating the link's href.

resources/views/app.blade.php:

```html
<link rel="stylesheet" href="{{ asset('css/style.css') }}" type="text/css">
```

1『上面是比较容易忽略的点，要去 HTML 页面里的 head 标签里引用下这个样式文件。』

#### 5.4.9 Font styles

We also have the Open Sans and Font Awesome style sheets to include. First, install the font packages with NPM:

    $ npm i --save-dev font-awesome open-sans-all

We'll modify our Mix configuration to bundle our app CSS, Open Sans, and Font Awesome CSS together. We can do this by passing an array to the first argument of the styles method. Mix will append statistics about the CSS bundle into the Terminal output:

Remember to remove the links to the font style sheets from the view as these will now be in the CSS bundle.

1『

```
yarn add font-awesome --dev
yarn add open-sans-all --dev
```

记得把 HTML 文件里 head 标签内的字体引用链接删掉（有的话）。

』

#### 5.4.10 Fonts

Open Sans and Font Awesome need both a CSS style sheet, and the relevant font files. Like CSS, Webpack can bundle fonts as modules, but we currently don't need to take advantage of this. Instead, we'll use the copy method, which tells Mix to copy the fonts from their home directory into the public folder where they can be accessed by the frontend app.

After building again, you'll now see a public/fonts folder in the project structure.

#### 5.4.11 Images

We'll now migrate the images, including the logo for the toolbar, and the mock data header image:

Let's chain on another copy method to include these in the public/images directory.

webpack.mix.js:

```js
mix.js('resources/js/app.js', 'public/js')
    .styles([
        'node_modules/open-sans-all/css/open-sans.css',
        'node_modules/font-awesome/css/font-awesome.css',
        'resources/sass/app.scss'
    ], 'public/css/app.css')
    .copy('node_modules/open-sans-all/fonts', 'public/fonts')
    .copy('node_modules/font-awesome/fonts', 'public/fonts')
    .copy('resources/images', 'public/images');
```

We also need to ensure the view is pointing to the correct file location for the images. In the toolbar.

resources/views/app.blade.php:

```html
<div id="toolbar"> 
    <img class="icon" src="{{ asset('images/logo.png') }}"> 
    <h1>vuebnb</h1> 
</div>
```

And in the modal. resources/views/app.blade.php:

```html
<div class="modal-content"> 
    <img src="{{ asset('images/header.jpg') }}"/> 
</div>
```

Don't forget that the headerImageStyle data property in the entry file also needs to be updated. resources/assets/js/app.js:

```json
headerImageStyle: { 'background-image': 'url(/images/header.jpg)' },
```

While not exactly an image, we'll also migrate the favicon. This can be put straight into the public folder:

    $ cp ../vuebnb-prototype/favicon.ico ./public

1『目前还不知道这个图片啥用。』

### 5.5 Development tools

We can utilize some handy development tools to improve our frontend workflow, including: 1) Watch mode. 2) BrowserSync.

#### 5.5.1 Watch mode

So far, we've been running builds of our app manually using npm run dev every time we make a change. Webpack also has a watch mode where it automatically runs a build when a dependency changes. Thanks to the design of Webpack, it is able to efficiently complete these automatic builds by only rebuilding modules that have changed. To use watch mode, run the watch script included in package.json:

    $ npm run watch

To test that it works, add this at the bottom of resources/assets/js/app.js:

    console.log("Testing watch");

If watch mode is running correctly, saving this file will trigger a build, and you'll see updated build statistics in the Terminal. If you then refresh the page you'll see the Testing watch message in the console. To turn off watch mode, press Ctrl + C in the Terminal. It can then be restarted at any time. Don't forget to remove the console.log once you're satisfied watch mode is working. I'll assume you're using watch for the rest of the book, so I won't remind you to build your project after changes anymore!

#### 5.5.2 BrowserSync

Another useful development tool is BrowserSync. Similar to watch mode, BrowserSync monitors your files for changes, and when one occurs inserts the change into the browser. This saves you from having to do a manual browser refresh after every build.

To use BrowserSync, you'll need to have the Yarn package manager installed. If you're running terminal commands from within the Vagrant Box, you're all set, as Yarn is pre-installed with Homestead. Otherwise, follow the installation instructions for Yarn here: https://yarnpkg.com/en/docs/install.

BrowserSync has been integrated with Mix and can be used by chaining a call to the browserSync method in your Mix configuration. Pass an options object with the app's URL as a proxy property, for example, browserSync({ proxy: http://vuebnb.test }).

We have the app's URL stored as an environment variable in the .env file, so let's get it from there rather than hard-coding into our Mix file. First, install the NPM dotenv module, which reads a .env file into a Node project:

    $ npm i dotenv --save-devpm

3『原来「dotenv」包的作用是可以直接在 laravel 文件里调用「.env」定义的变量，之前遇到的七牛头 HTTP 读不出来，又提供了一个解决方案。』

Require the dotenv module at the top of the Mix configuration file and use the config method to load .env. Any environment variables will then be available as properties of the process.env object. We can now pass an options object to the browserSync method with process.env.APP_URL assigned to proxy. I also like to use the open: false option as well, which prevents BrowserSync from automatically opening a tab.

webpack.mix.js:

```js
require('dotenv').config();
const mix = require('laravel-mix');

mix.js('resources/js/app.js', 'public/js')
    .styles([
        'node_modules/open-sans-all/css/open-sans.css',
        'node_modules/font-awesome/css/font-awesome.css',
        'resources/sass/app.scss'
    ], 'public/css/app.css')
    .copy('node_modules/open-sans-all/fonts', 'public/fonts')
    .copy('node_modules/font-awesome/fonts', 'public/fonts')
    .copy('resources/images', 'public/images')
    .browserSync({
        proxy: process.env.APP_URL,
        open: false,
    });
```

BrowserSync runs on its own port, 3000 by default. When you run npm run watch again, open a new tab at localhost:3000. After you make changes to your code you'll find they are automatically reflected in this BrowserSync tab!

Note that if you run BrowserSync inside your Homestead box you can access it at vuebnb.test:3000.

Even though the BrowserSync server runs on a different port to the web server, I will continue to refer to URLs in the app without specifying the port to avoid any confusion, for example, vuebnb.test rather than localhost:3000 or vuebnb.test:3000.

1『安装的时候提示要单独安装 webpack，「yarn add webpack」，后来发现没自动更新（待解决）。为了减少电脑负担，这个功能目前没用。（2020-04-19）』

#### 5.5.3 ES2015

The js Mix method applies the Babel plugin to Webpack, ensuring that any ES2015 code is transpiled down to browser-friendly ES5 before it's added to the bundle file. We wrote the Vuebnb frontend app prototype using only ES5 syntax, as we ran it directly in the browser without any build step. But now we can take advantage of ES2015 syntax, which includes a lot of handy features. For example, we can use a shorthand for assigning a function to an object property.

resources/assets/js/app.js:

```js
escapeKeyListener: function(evt) { ... }
```

Can be changed to this:

```js
escapeKeyListener(evt) { ... }
```

There are several instances of this in app.js that we can change. There aren't any other opportunities for using ES2015 syntax in our code yet, though in the coming chapters we'll see more.

#### 5.5.4 Polyfills

The ES2015 proposal includes new syntax, but also new APIs, such as Promise, and additions to existing APIs, such as Array and Object. The Webpack Babel plugin can transpile ES2015 syntax, but new API methods require polyfilling. A polyfill is a script that is run in the browser to cover an API or API method that may be missing.

For example, Object.assign is a new API method that is not supported in Internet Explorer 11. If we want to use it in our frontend app, we have to check at the top of our script whether the API method exists, and if not, we define it manually with a polyfill:

```js
if (typeof Object.assign != 'function') { 
    // Polyfill to define Object.assign 
}
```

Speaking of which, Object.assign is a handy way of merging objects and would be useful in our frontend app. Let's use it in our code, then add a polyfill to ensure the code will run in older browsers.

Look at the data object in our entry file, resources/assets/js/app.js. We are manually assigning each property of the sample object to the data object, giving it the same property name. To save having to repeat ourselves, we can instead use Object.assign and simply merge the two objects. In practice, this doesn't do anything different, it's just more succinct code.

resources/assets/js/app.js:

```js
data: Object.assign(sample, { 
    headerImageStyle: { 'background-image': 'url(/images/header.jpg)' }, 
    contracted: true, 
    modalOpen: false 
}),
```

3『 

Object.assign 这个 API 的作用是合并对象，在前端开发中经常用，经验证目前的开发框架是支持的，不需要再手动安装了。

[Object.assign() - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)

The Object.assign() method copies all enumerable own properties from one or more source objects to a target object. It returns the target object.

```js
const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };

const returnedTarget = Object.assign(target, source);

console.log(target);
// expected output: Object { a: 1, b: 4, c: 5 }

console.log(returnedTarget);
// expected output: Object { a: 1, b: 4, c: 5 }
```

    Object.assign(target, ...sources)

target, The target object — what to apply the sources’ properties to, which is returned after it is modified. sources, The source object(s) — objects containing the properties you want to apply.

Properties in the target object are overwritten by properties in the sources if they have the same key. Later sources' properties overwrite earlier ones. The Object.assign() method only copies enumerable and own properties from a source object to a target object. 

It uses [[Get]] on the source and [[Set]] on the target, so it will invoke getters and setters. Therefore it assigns properties, versus copying or defining new properties. This may make it unsuitable for merging new properties into a prototype if the merge sources contain getters. For copying property definitions (including their enumerability) into prototypes, use Object.getOwnPropertyDescriptor() and Object.defineProperty() instead.

Both String and Symbol properties are copied. In case of an error, for example if a property is non-writable, a TypeError is raised, and the target object is changed if any properties are added before the error is raised. 

Note: Object.assign() does not throw on null or undefined sources.

文档里给了大量的例子，可以看看，而且有中文文档。

Cloning an object.

```js
const obj = { a: 1 };
const copy = Object.assign({}, obj);
console.log(copy); // { a: 1 }
```

Warning for Deep Clone. For deep cloning, we need to use alternatives, because Object.assign() copies property values. If the source value is a reference to an object, it only copies the reference value.

```js
function test() {
  'use strict';

  let obj1 = { a: 0 , b: { c: 0}};
  let obj2 = Object.assign({}, obj1);
  console.log(JSON.stringify(obj2)); // { "a": 0, "b": { "c": 0}}
  
  obj1.a = 1;
  console.log(JSON.stringify(obj1)); // { "a": 1, "b": { "c": 0}}
  console.log(JSON.stringify(obj2)); // { "a": 0, "b": { "c": 0}}
  
  obj2.a = 2;
  console.log(JSON.stringify(obj1)); // { "a": 1, "b": { "c": 0}}
  console.log(JSON.stringify(obj2)); // { "a": 2, "b": { "c": 0}}
  
  obj2.b.c = 3;
  console.log(JSON.stringify(obj1)); // { "a": 1, "b": { "c": 3}}
  console.log(JSON.stringify(obj2)); // { "a": 2, "b": { "c": 3}}
  
  // Deep Clone
  obj1 = { a: 0 , b: { c: 0}};
  let obj3 = JSON.parse(JSON.stringify(obj1));
  obj1.a = 4;
  obj1.b.c = 4;
  console.log(JSON.stringify(obj3)); // { "a": 0, "b": { "c": 0}}
}

test();
```

』

To polyfill Object.assign we must install a new core-js dependency, which is a library of polyfills for most new JavaScript APIs. We'll use some other core-js polyfills later in the project:

    $ npm i --save-dev core-js

3『

安装完的提示：

```
Thank you for using core-js ( https://github.com/zloirock/core-js ) for polyfilling JavaScript standard library!

The project needs your help! Please consider supporting of core-js on Open Collective or Patreon:
> https://opencollective.com/core-js
> https://www.patreon.com/zloirock

Also, the author of core-js ( https://github.com/zloirock ) is looking for a good job -)
```

』

At the top of app.js, add this line to include the Object.assign polyfill:

    import "core-js/fn/object/assign";

1『发现不需要引用上面语句，引用反而报错。原理待了解。（2020-05-01）』

After this builds, refresh your page to see whether it works. Most likely you will not notice any difference unless you can test this on an older browser, such as Internet Explorer, but now you have the assurance that this code will run almost anywhere.

### 5.6 Mock data

We've now completely migrated the Vuebnb prototype into our Laravel project, plus we've added a build step. Everything in the frontend app is working as it was in Chapter 2, Prototyping Vuebnb, Your First Vue.js Project. However, we still have mock data hard-coded into the frontend app. In this last part of the chapter, we're going to remove that hard-coded data and replace it with data from the backend.

#### 5.6.1 Routes

Currently, the home route, that is, /, loads our frontend app. But what we've built for our frontend app so far is not meant to be a home page! We'll be building that in future chapters. What we've built is the listing page, which should be at a route like /listing/5, where 5 is the ID of the mock data listing being used. Let's modify the route to reflect this.

routes/web.php:

```php
<?php

use Illuminate\Support\Facades\Route;
use App\Models\ListingModel;

Route::get('/listing/{listing}', function($id) {
    return view('app');
});
```

Just like in our api/listing/{listing} route, the dynamic segment is meant to match the ID for one of our mock data listings. If you recall from the previous chapter, we created 30 mock data listings with an ID range of 1 to 30. If we now type hint the Listing model in the closure function's profile, Laravel's service container will pass in a model with an ID that matches that dynamic route segment.

```php
<?php

use Illuminate\Support\Facades\Route;
use App\Models\ListingModel;

Route::get('/listing/{listing}', function(ListingModel $listing) {
    return view('app');
});

// echo $listing->id // will equal 5 for route /listing/5 return view('app');
```

One cool in-built feature is, if the dynamic segment does not match a model, for example /listing/50 or /listing/somestring, Laravel will abort the route and return a 404.

#### 5.6.2 Architecture

Given that we can retrieve the correct listing model in the route handler, and that, thanks to the Blade templating system, we can dynamically insert content into our app view, an obvious architecture emerges: we can inject the model into the head of the page. That way, when the Vue app loads, it will have immediate access to the model:

#### 5.6.3 Injecting data

Getting the mock-listing data into the client app will take several steps. We'll begin by converting the model to an array. The view helper can then be used to make the model available within the template at runtime.

routes/web.php:

```php
Route::get('/listing/{listing}', function(ListingModel $listing) {
    $model = $listing->toArray();
    return view('app', [ 'model' => $model ]);
});
```

Now, in the Blade template, we'll create a script in the head of the document. By using double curly brackets, we can interpolate the model directly into the script.

```html
<head> .
    .. 
    <script type="text/javascript"> 
        console.log({{ $model[ 'id' ] }}); 
    </script> 
</head>
```

If we now go to the /listing/5 route, we will see the following in our page source:

```html
<script type="text/javascript"> 
    console.log(5); 
</script>
```

And you will see the following in our console:

1『如此方便的将数据从后端传递到前端，多亏了 Blade templating system。』

#### 5.6.4 JSON

We'll now encode the entire model as JSON within the view. The JSON format is good because it can be stored as a string and can be parsed by both PHP and JavaScript. In our inline script, let's format the model as a JSON string and assign to a model variable.

resources/views/app.blade.php:

```html
<script type="text/javascript">
    var model = "{!!addslashes(json_encode($model))!!}";
    console.log(model);
</script
```

1『这里相当于一步步教你如何把数据从后端传递到前端来。』

Notice we also had to wrap json\_encode in another global function, addslashes. This function will add backslashes before any character that needs to be escaped. It's necessary to do this because the JavaScript JSON parser doesn't know which quotes in the string are part of the JavaScript syntax, and which are part of the JSON object.

1『原来全局函数 addslashes() 是给 json 数据加转义字符的，赞。』

We also had to use a different kind of Blade syntax for interpolation. A feature of Blade is that statements within double curly brackets {{ }} are automatically sent through PHP's htmlspecialchars function to prevent XSS attacks. This will, unfortunately, invalidate our JSON object. The solution is to use the alternative {!! !!} syntax, which does not validate the contents. This is safe to do in this scenario because we're sure we're not using any user-supplied content. Now if we refresh the page, we'll see the JSON object as a string in the console:

If we change the log command to console.log(JSON.parse(model));, we see our model not as a string, but as a JavaScript object:

We've now successfully gotten our model from the backend into the frontend app!

#### 5.6.5 Sharing data between scripts

We have another issue to overcome now. The inline script in the head of the document, which is where our model object is, is a different script to the one where we have our client application, which is where it's needed. As we've discussed in the previous section, multiple scripts and global variables are generally not preferred as they make the app fragile. But in this scenario, they're a necessity. The safest way to share an object or function between two scripts is to make it a property of the global window object. That way, it's very obvious from your code that you're intentionally using a global variable:

1『两个脚本间传递对象，最安全的方式是把它作为全局 window 对象的一个属性。』

```js
// scriptA.js 
window.myvar = 'Hello World'; 

// scriptB.js 
console.log(window.myvar); // Hello World
```

If you add additional scripts to your project, particularly third-party ones, they might also add to the window object, and there's a possibility of a naming collision. To avoid this the best we can, we'll make sure we use a very specific property name.

resources/views/app.blade.php:

```html
<script type="text/javascript">
    window.vuebnb_listing_model = "{!!addslashes(json_encode($model))!!}";
</script
```

Now, over in the entry file of the frontend app, we can work with this window property in our script.

resources/assets/js/app.js:

```js
let model = JSON.parse(window.vuebnb_listing_model); 

var app = new Vue({ ... });
```

#### 5.6.6 Replacing the hard-coded model

We now have access to our listing model in the entry file, so let's switch it with our hard-coded model in the data property assignment.

resources/assets/js/app.js:

```js
let model = JSON.parse(window.vuebnb_listing_model); 

var app = new Vue({ 
    el: '#app', 
    data: Object.assign(model, { ... }) 
    ...
 });
```

With that done, we can now remove the import sample from './data'; statement from the top of app.js. We can also delete the sample data files as they won't be used any further in the project:

1『

报错：5:55 GET http://localhost:8000/listing/js/app.js 404 (Not Found)

[javascript - js/app/js file net::ERR_ABORTED 404 (Not Found) - Stack Overflow](https://stackoverflow.com/questions/58010053/js-app-js-file-neterr-aborted-404-not-found)

上面论坛里的解决方案没有解决我的问题。研究后发现地址多了个 listing，但不知道如何解决。

找到原因了。去掉路由里根目录下里的「listing」即可。

```php
Route::get('/{listing}', 'ListingController@get_listing_web');
```

但是访问的路由变成了「http://localhost:8000/4」、「http://localhost:8000/6」、「http://localhost:8000/9」，不是我们想要的，还是想要实现「http://localhost:8000/listing/4」。最后问题定位在：

```html
<script src="js/app.js" type="text/javascript"></script>
```

因为源码里是：

```html
<script src="{{ asset('js/app.js') }}" type="text/javascript"></script>
```

之前一直觉得在 resources 下，又建一个「assets」文件夹放资源感觉多余，所以一直把 js、sass、images 文件夹直接放在 resources 目录下的，尝试新建一个文件夹 assets，把这些资源放进去。接着修改主页代码：

```html
<script src="{{ assets('js/app.js') }}" type="text/javascript"></script>
```

报错：Call to undefined function assets()

说明 asset() 其实是一个函数，自己把函数名拼错了，修改成下面代码即可解决问题。

```html
<script src="{{ asset('js/app.js') }}" type="text/javascript"></script>
```

函数 asset() 是 laravel 框架里，将文件自动转化为 url 的内置函数。之前是误打误撞解决了问题，src="{{ asset('js/app.js') }}" 跟资源夹那边半毛钱关系也没有，它只是引用 public 文件夹下的 js/app.js，之前没有用 asset() 函数时，url 里是没有 HTTP 头的，其实手动把头补全也可以解决上述问题。（2020-05-01）

』

#### 5.6.7 Amenities and prices

If you refresh the page now, it will load, but the script will have some errors. The problem is that the amenities and prices data are structured differently in the frontend app to how they are in the backend. This is because the model initially came from our database, which stores scalar values. In JavaScript, we can use richer objects which allow us to nest data, making it much easier to work with and manipulate. Here is how the model object currently looks. Notice that the amenities and prices are scalar values:

1『关键知识点。』

This is how we need it to look, with the amenities and prices as arrays:

To fix this problem, we'll need to transform the model before we pass it to Vue. To save you having to think too much about this, I've put the transformation function into a file, resources/assets/js/helpers.js. This file is a JavaScript module that we can import into our entry file and use by simply passing the model object into the function.

resources/assets/js/app.js:

```js
import Vue from 'vue'; 
import { populateAmenitiesAndPrices } from './helpers'; 

let model = JSON.parse(window.vuebnb_listing_model); 
model = populateAmenitiesAndPrices(model)</span>;
```

发现个问题，因为复制的时候会把一些多余的标签拷进来，得删除。比如：

```php
model = populateAmenitiesAndPrices(model);
```

Once we've added this and refreshed the page, we should see the new model data in the text parts of the page (although still with the hard-coded images):

#### 5.6.8 Image URLs

The last thing to do is replace the hard-coded images' URLs in the frontend app. These URLs are not currently a part of the model, so need to be manually added to the model before we inject it into the template. We've already done a very similar job back in Chapter 4, Building a Web Service With Laravel, for the API listing route.

app/Http/Controllers/ListingController.php:

```php
public function get_listing_api(ListingModel $listing)
{
    $model = $listing->toArray();
    for ($i = 1; $i <=4; $i++) {
        $model['image_' . $i] = asset(
            'images/' . $listing->id . '/Image_' . $i . '.jpg');
    }
    return response()->json($model);
}
```

2『又看到 asset() 函数，去查下。回复：前面有个地方给出了 laravel 文档里这个函数的相关信息，是一个 helper 函数，用来输出文件的 URL。（2020-05-02）』

In fact, our web route will end up with identical code to this API route, only instead of returning JSON, it will return a view. Let's share the common logic. Begin by moving the route closure function into a new get\_listing\_web method in the listing controller.

app/Http/Controllers/ListingController.php:

```php
    public function get_listing_web(ListingModel $listing)
    {
        $model = $listing->toArray();
        return view('app', ['model' => $model]);
    }
```

Then adjust the route to call this new controller method.

routes/web.php:

```php
<?php Route::get('/listing/{listing}', 'ListingController@get_listing_web');
```

Let's now update the controller so both the web and API routes get the images' URLs added to their model. We'll first create a new add\_image\_urls method, which abstracts the logic that was used in get\_listing\_api. Now both of the route-handling methods will call this new method.

app/Http/Controllers/ListingController.php:

```php
public function get_listing_web(ListingModel $listing)
{
    $model = $listing->toArray();
    $model = $this->add_image_urls($model, $listing->id);
    return view('app', ['model' => $model]);
}

private function add_image_urls($model, $id)
{
    for($i = 1; $i <=4; $i++) {
        $model['image_' . $i] = asset('images/' . $id . '/Image_' . $i . '.jpg');
    }
    return $model;
}
```

With that done, if we refresh the app and open Vue Devtools, we should see that we have the image URLs as an images data property:

#### 5.6.9 Replacing the hard-coded image URLs

The final step is to use these image URLs from the backend instead of the hard-coded URL. Remembering that images is an array of URLs, we'll use the first image as a default, that is, images[0]. First, we'll update the entry file,

resources/assets/js/app.js:

```js
headerImageStyle: { 
    'background-image': `url(${model.images[0]})` 
}
```

Then the view for the modal image.

resources/views/app.blade.php:

```php
<div class="modal-content"> <img v-bind:src="images[0]"/> </div>
```
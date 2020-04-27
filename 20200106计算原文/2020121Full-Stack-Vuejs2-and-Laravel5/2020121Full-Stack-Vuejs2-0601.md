# 0601. Composing Widgets with Vue.js Components

Components are becoming an essential aspect of frontend development, and are a feature in most modern frontend frameworks, including Vue, React, Angular, Polymer, and so on. Components are even becoming native to the web through a new standard called Web Components.

In this chapter, we will use components to create an image carousel for Vuebnb, which allows users to peruse the different photos of a room listing. We'll also refactor Vuebnb to conform to a component-based architecture. Topics covered in this chapter: 1) What components are and how to create them with Vue.js. 2) Component communication through props and events. 3) Single-file components-one of Vue's most useful features. 4) Adding custom content to a component with slots. 5) The benefit of architecting apps entirely from components. 6) How render functions can be used to skip the template compiler. 7) Using the runtime-only build of Vue to lighten the bundle size.

## 01. Components

When we're constructing a template for a web app, we can use HTML elements such as div, table, and span. This variety of elements makes it easy to create whatever structures we need for organizing content on the page. What if we could create our own custom elements, through, for example, my-element? This would allow us to create reusable structures specifically designed for our app.

Components are a tool for creating custom elements in Vue.js. When we register a component, we define a template which renders as one or more standard HTML elements:

![](./res/2020007.png)

Figure 6.1. Components facilitate reusable markup and render as standard HTML

### 1.1 Registration

There are many ways to register a component, but the easiest is to use the component API method. The first argument is the name you want to give the component, the second is the configuration object. The configuration object will often include a template property to declare the component's markup using a string:

```js
Vue.component('my-component', { 
    template: '<div>My component!</div>' 
}); 

new Vue({ 
    el: '#app' 
});
```

Once we've registered a component like this, we can use it within our project:

```html
<div id="app"> 
    <my-component></my-component> 
    <!-- Renders as <div>My component!</div> --> 
</div>
```

### 1.2 Data

In addition to reusable markup, components allow us to reuse JavaScript functionality. The configuration object can not only include a template but can also include its own state, just like the Vue instance. In fact, each component can be thought of as a mini-instance of Vue with its own data, methods, lifecycle hooks, and so on. We treat component data slightly differently to the Vue instance though, as components are meant to be reusable. For example, we might create a bank of check-box components like this:

```js
<div id="app"> 
    <check-box></check-box> 
    <check-box></check-box> 
    <check-box></check-box> 
</div> 

<script> 
    Vue.component('check-box', { 
        template: '<div v-on:click="checked = !checked"></div>' 
        data: { 
            checked: false 
        } 
    }); 
</script>
```

As it is, if a user clicks a checkbox div, the checked state toggles from true to false for every checkbox simultaneously! This is not what we want, but it is what will happen, as all instances of the component refer to the same data object and therefore have the same state.

To give each instance its own unique state, the data property shouldn't be an object, but a factory function that returns an object. That way, every time the component is instantiated, it links to a fresh data object. Implementing this is as simple as:

```js
data() { 
    return { checked: false } 
}
```

## 02. Image carousel

Let's build a new feature for the Vuebnb frontend app using components. As you'll recall from previous chapters, each of our mock data listings has four different images, and we're passing the URLs to the frontend app. To allow the user to peruse these images, we're going to create an image carousel. This carousel will replace the static image that currently occupies the modal window that pops up when you click the header of a listing. Begin by opening the app view. Remove the static image and replace it with a custom HTML element image-carousel.

resources/views/app.blade.php:

```php
<div class="modal-content"> 
    <image-carousel></image-carousel> 
</div>
```

A component can be referred to in your code by a kebab-case name such as my-component, a PascalCase name such as MyComponent, or a camelCase name such as myComponent. Vue sees these all as the same component. However, in a DOM or string template, the component should always be kebab-cased. Vue doesn't enforce this, but markup in the page gets parsed by the browser before Vue gets to work with it, so it should conform to W3C naming conventions or the parser may strip it out.

1『又看到接触过的 3 种命名方式：kebab-case、PascalCase、camelCase，推荐使用 kebab-cased，因为 DOM 和 string template 用它。』

Let's now register the component in our entry file. The template of this new component will simply be the image tag we removed from the view, wrapped in a div. We add this wrapping element, as component templates must have a single root element, and we'll soon be adding more elements inside it.

1『组件与根实例是并列结构的。』

As a proof of concept, the component data will include an array of hard-coded image URLs. Once we learn how to pass data into a component, we will remove these hard-coded URLs and replace them with dynamic ones from our model.

resources/assets/js/app.js:

```js
Vue.component('image-carousel', {
    template: `<div class="image-carousel">
                    <img v-bind:src="images[0]"/>
               </div>`,
    data() {
        return {
            images: [
                'images/1/Image_1.jpg',
                'images/1/Image_2.jpg',
                'images/1/Image_3.jpg',
                'images/1/Image_4.jpg',
            ]
        }
    }
});
```

1『

报错：GET http://localhost:8000/listing/images/1/Image_1.jpg 404 (Not Found)

目前问题没解决。（2020-04-20）

但是曲线救国，通过另一个方式获取了图片 url 的信息。

```js
// images carousel
Vue.component('image-carousel', {
    template: `<div class="image-carousel">
                    <img v-bind:src="images[0]"/>>
               </div>`,
    data() {
        return {
            images: Object.assign(model).images,
        }
    }
});
```

』

Before we test this component, let's make an adjustment to our CSS. We previously had a rule to ensure the image inside the modal window stretched to full width by using the .modal-content img selector. Let's instead use the .image-carousel selector for this rule, as we're decoupling the image from the modal window.

resources/assets/css/style.css:

```css
.image-carousel img { width: 100%; }
```

After your code has rebuilt, navigate the browser to /listing/1 and you should see no difference, as the component should render in almost exactly the same way as the previous markup did. If we check Vue Devtools, however, and open up to the Components tab, you'll see that we now have the ImageCarousel component nested below the Root instance. Selecting ImageCarousel, we can even inspect its state:

Figure 6.2. Vue Devtools showing ImageCarousel component

### 2.1 Changing images

The point of a carousel is to allow the user to peruse a collection of images without having to scroll the page. To permit this functionality, we'll need to create some UI controls. But first, let's add a new data property, index, to our component, which will dictate the current image being displayed. It will be initialized at 0 and the UI controls will later be able to increment or decrement the value. We will bind the image source to the array item at position index.

resources/assets/js/app.js:

```js
Vue.component('image-carousel', { template: `<div class="image-carousel"> <img v-bind:src="images[index]"/> </div>`, data() { return { images: [ '/images/1/Image_1.jpg', '/images/1/Image_2.jpg', '/images/1/Image_3.jpg', '/images/1/Image_4.jpg' ], index: 0 } } });
```

A page refresh should, again, reveal no change to what you see on screen. However, if you initialize the value of index to 1, 2, or 3, you will find a different image is shown when you re-open the modal window:

Figure 6.3. Setting index to 2 selects a different URL and a different image is shown

## 03. Computed properties

It's convenient to write logic straight into our template as an expression, for example, v-if="myExpression". But what about more complex logic that can't be defined as an expression, or simply becomes too verbose for the template? For this scenario, we use computed properties. These are properties we add to our Vue configuration that can be thought of as reactive methods which are rerun whenever a dependent value is changed.

In the following example, we've declared a computed property, message, under the computed configuration section. Note the function is dependent on val, that is, the returned value of of message will be different as val changes. When this script runs, Vue will note any dependencies of message and will set up reactive binding so that, unlike a regular method, the function will be rerun whenever the dependencies change:

```js
<script> 
    var app = new Vue({ 
        el: '#app', 
        data: { val: 1 }, 
        computed: { 
            message() { 
                return `The value is ${this.val}` 
            } 
        } 
    }); 
    setTimeout(function() { 
        app.val = 2; 
    }, 2000); 
</script> 

<div id="app"> <!--Renders as "The value is 1"--> <!--After 2 seconds, re-renders as "The value is 2"--> {{ message }} </div>
```

Going back to the image carousel, let's make the template terser by abstracting the expression bound to the image src into a computed property.

resources/assets/js/app.js:

```js
Vue.component('image-carousel', { 
    template: `<div class="image-carousel"> <img v-bind:src="image"/> </div>`, 
    data() { ... }, 
    computed: { 
        image() { 
            return this.images[this.index]; 
        } 
    } 
});
```

## 04. Composing with components

Components can be nested in other components in the same way that standard HTML elements can be nested. For example, component B can be a child of component A, if component A declares component B in its template:


```js
<div id="app"> 
    <component-a></component-a> 
</div> 

<script> 
    Vue.component('component-a', { 
        template: ` 
        <div> 
            <p>Hi I'm component A</p> 
            <component-b></component-b> 
        </div>` 
    }); 
    
    Vue.component('component-b', { 
        template: `<p>And I'm component B</p>` 
    }); 
    
    new Vue({ 
        el: '#app' 
    }); 
</script>
```

This renders as:

```html
<div id="app"> 
    <div> 
        <p>Hi I'm component A</p> 
        <p>And I'm component B</p> 
    </div> 
</div>
```

## 05. Registration scope

While some components are designed for use anywhere in an app, other components may be designed with a more specific purpose. When we register a component using the API, that is, Vue.component, that component is globally registered and can be used within any other component or instance. We can also locally register a component by declaring it in the components option in the root instance, or in another component:

```js
Vue.component('component-a', { 
    template: ` <div> <p>Hi I'm component A</p> <component-b></component-b> </div>`, 
    components: { 'component-b': { 
        template: `<p>And I'm component B</p>`
        } 
    } 
});
```

## 06. Carousel controls

To allow a user to change the currently shown image in the carousel, let's create a new component, CarouselControl. This component will be presented as an arrowhead that floats over the carousel and will respond to a user's click. We'll use two instances, as there will be a left and right arrow for either decrementing or incrementing the image index.

We'll register CarouselControl locally for the ImageCarousel component. The CarouselControl template will render as an i tag, which is often used for displaying icons. A good icon for carousels is the Font Awesome chevron icon, which is an elegantly shaped arrowhead. Currently, we don't have a way to distinguish between the left and right, so for now, both instances will have a left-facing icon.

resources/assets/js/app.js:

```js
// images carousel
Vue.component('image-carousel', {
    template: `<div class="image-carousel">
                    <img v-bind:src="image">
                    <div class="controls">
                        <carousel-control></carousel-control>
                        <carousel-control></carousel-control>
                    </div>
               </div>`,
    data() {
        return {
            // images: [
            //     'images/1/Image_1.jpg',
            //     'images/1/Image_2.jpg',
            //     'images/1/Image_3.jpg',
            //     'images/1/Image_4.jpg',
            // ],
            images: Object.assign(model).images,
            index: 0,
        }
    },
    computed: {
        image() {
            return this.images[this.index];
        }
    },
    components: {
        'carousel-control': {
            template: `<i class="carousel-control fa fa-2x fa-chevron-left"></i>`
        }
    },
});
```

To have these controls float nicely over our image carousel, we'll add some new rules to our CSS file as well.

resources/assets/css/style.css:

```css
.image-carousel img {
    width: 100%;
    margin-top: -12vh;
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
}

.image-carousel .controls {
    position: absolute;
    width: 100%;
    display: flex;
    justify-content: space-between;
}

.carousel-control {
    padding: 1rem;
    color: #ffffff;
    opacity: 0.85;
}

@media (min-width: 744px) {
    .container {
        width: 696px;
    }
    .carousel-control {
        font-size: 3rem;
    }
}
```

With that code added, open the modal window to see our handywork so far:

Figure 6.4. Carousel controls added to the image carousel

## 07. Communicating with components

A key aspect of components is that they are reusable, which is why we give them their own state to keep them independent from the rest of the app. However, we may still want to send in data, or send it out. Components have an interface for communicating with other parts of the app, which we will now explore.

### 7.1 Props

We can send data to a component through a custom HTML property know as a prop. We must also register this custom property in an array, props, in the component's configuration. In the following example, we've created a prop, title:

```js
<div id="app"> 
    <my-component title="My component!"></my-component>
     <!-- Renders as <div>My component!</div> --> 
</div> 

<script> 
    Vue.component('my-component', { 
        template: '<div>{{ title }}</div>', 
        props: ['title'] 
    }); 
    
    new Vue({ 
        el: '#app' 
    }); 
</script>
```

A prop can be used just like any data property of the component: you can interpolate it in the template, use it in methods and computed properties, and so on. However, you should not mutate prop data. Think of prop data as being borrowed from another component or instance - only the owner should change it.

1『隐喻：prop data 是从其他组件或实例里借来的数据，所以只有原主人可以修改。』

Props are proxied to the instance just like data properties, meaning you can refer to a prop as this.myprop within that component's code. Be sure to name your props uniquely to your data properties to avoid a clash!

### 7.2 One-way data flow

Since props must be declared in the template where the component is used, prop data can only pass from a parent to a child. This is why you shouldn't mutate a prop - since data flows down, the change will not be reflected in the parent, and therefore you will have different versions of what is meant to be the same bit of state. If you do need to tell the owner to change the data, there is a separate interface for passing data from a child to a parent, which we'll see later.

1『 prop data 的数据流是自上而下的，只能从父模板传递到子模板。』

### 7.3 Dynamic props

We can reactively bind data to a component using the v-bind directive. When the data changes in the parent, it will automatically flow down to the child. In the following example, the value of title in the root instance gets programmatically updated after two seconds. This change will automatically flow down to MyComponent, which will reactively re-render to display the new value:

```js
<body>
    <div id="app">
        <my-component :title="title"></my-component>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        Vue.component('my-component', {
            template: ''<div>@{{ title }}</div>',
            props: ['title'],
        });

        var vm = new Vue({
            el: "#app",
            data: {
                title: "hello world"
            },
        });

        setTimeout(() => {
            vm.title = "goodbye world";
        }, 2000);
    </script>
</body>
```

1『注意，码了一遍发现报错，title 变量未定义。因为是在 laravel 框架里，绑定数据的格式跟 blade 冲突，所以得在前面加一个 @。备注：作者也是对的，放到外面的 js 模块代码作为引入时就不需要加 @，vue 实例化直接在 html 页面里就得加上。（2020-04-23）目前还没弄明白，在作者项目里，为什么不能在一个页面里注册 2 个 vue 实例。自己新建了一个实验页面就可以注册多个 vue 实例。经试验，可以在作者项目里的页面里引入自己试验的 js 模块，以后项目开发里可以采用同样的思路，分模块引用。（2020-04-23）』

Since the v-bind directive is used so commonly in templates, you can omit the directive name as a shorthand: \<div v-bind:title="title"> can be shortened to \<div :title="title">.

## 08. Image URLs

When we created ImageCarousel, we hard-coded the image URLs. With props, we now have a mechanism for sending dynamic data from the root instance down to a component. Let's bind the root instance data property images to a prop, also called images, in our ImageCarousel declaration.

resources/views/app.blade.php:

```php
<div class="modal-content"> 
    <image-carousel :images="images"></image-carousel> 
</div>
```

Now, delete the data property images in the ImageCarousel component, and instead declare images as a prop.

1『可以把模板里的图片 url 数据删掉了，所以之前记录的那个纯写图片地址产生的问题也就不存在了。』

resources/assets/js/app.js:

```js
Vue.component('image-carousel', { 
    props: ['images'], 
    data() { return { index: 0 } }, 
    ... 
}
```

The root instance will now be responsible for the state of the image URLs, and the image carousel component will just be responsible for displaying them. Using Vue Devtools, we can inspect the state of the image carousel component, which now includes images as a prop value instead of a data value:

Figure 6.5. Image URLs are props sent to the ImageCarousel component

Now that the image URLs are coming from the model, we can access other listing routes, such as /listing/2, and see the correct image displaying in the modal window again.

## 09. Distinguishing carousel controls

The CarouselControl component should have two possible states: either left-pointing or right-pointing. When clicked by the user, the former will ascend through the available images, the latter will descend. This state should not be internally determined, but instead passed down from ImageCarousel. To do so, let's add a prop dir to CarouselControl that will take a string value, and should be either left or right.

With the dir prop, we can now bind the correct icon to the i element. This is done with a computed property which appends the prop's value to the string fa-chevron-, resulting in either fa-chevron-left or fa-chevron-right.

resources/assets/js/app.js:

```js
Vue.component('image-carousel', {
    template: `<div class="image-carousel">
                    <img v-bind:src="image">
                    <div class="controls">
                        <carousel-control dir="left"></carousel-control>
                        <carousel-control dir="right"></carousel-control>
                    </div>
               </div>`,
    props: ['images'],
    data() {
        return {
            index: 0,
        }
    },
    computed: {
        image() {
            return this.images[this.index];
        }
    },
    components: {
        'carousel-control': {
            template: `<i :class="classes"></i>`,
            props: ['dir'],
            computed: {
                classes() {
                    return 'carousel-control fa fa-2x fa-chevron-' + this.dir;
                },
            },
        }
    },
});
```

Now we can see the carousel control icons correctly directed:

Figure 6.6. Carousel control icons are now correctly directed

## 10. Custom events

Our carousel controls are displaying nicely, but they still don't do anything! When they're clicked, we need them to tell ImageCarousel to either increment or decrement its index value, which will result in the image being changed. Dynamic props won't work for this task, as props can only send data down from a parent to a child. What do we do when the child needs to send data up to the parent?

Custom events can be emitted from a child component and listened to by its parent. To implement this, we use the \$emit instance method in the child, which takes the event name as the first argument and an arbitrary number of additional arguments for any data to be sent along with the event, such as this.\$emit('my-event', 'My event payload');.

The parent can listen to this event using the v-on directive in the template where the component is declared. If you handle the event with a method, any arguments sent with the event will be passed to this method as parameters. Consider this example, where a child component, MyComponent, emits an event called toggle to tell the parent, the root instance, to change the value of a data property, toggle:

1『子模板可以通过 emits 通知父模板，需要改变什么数据值。』

```js
<body>
    <div id="app">
        <my-component @toggle="toggle=!toggle"></my-component>
        @{{ message }}
    </div>
    <!-- <script src="{{ asset('js/testapp.js') }}" type="text/javascript"></script> -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        Vue.component('my-component', {
            template: '<div v-on:click="clicked">click me</div>',
            methods: {
                clicked: function() {
                    this.$emit('toggle');
                },
            },
        });

        var vm = new Vue({
            el: "#app",
            data: {
                toggle: false,
            },
            computed: {
                message: function() {
                    return this.toggle ? 'On' : 'Off';
                },
            },
        });
    </script>
</body>
```

1『

报错：[Vue warn]: Property or method "clicked" is not defined on the instance but referenced during render. Make sure that this property is reactive, either in the data option, or for class-based components, by initializing the property.

找了半天后发现，组件里的方法属性应该是 methods 而非 method，真的是魔鬼在细节。

』

## 11. Changing carousel images

Returning to CarouselControl, let's respond to a user's click by using the v-on directive and triggering a method, clicked. This method will, in turn, emit a custom event, change-image, which will include a payload of either -1 or 1, depending on whether the state of the component is left or right. Just like with v-bind, there is a shorthand for v-on as well. Simply replace v-on: with @; for instance, \<div @click="handler">\</div> is the equivalent of \<div v-on:click="handler">\</div>.

resources/assets/js/app.js:

```js
components: {
    'carousel-control': {
        template: `<i :class="classes" @click="clicked"></i>`,
        props: ['dir'],
        computed: {
            classes() {
                return 'carousel-control fa fa-2x fa-chevron-' + this.dir;
            }
        },
        methods: {
            clicked() {
                this.$emit('change-image', this.dir === 'left' ? -1 : 1);
            }
        },
    }
},
```

Open Vue Devtools to the Events tab, and, at the same time, click on the carousel controls. Custom events are logged here, so we can verify change-image is being emitted:

Figure 6.7. Screenshot showing a custom event and its payload

ImageCarousel will now need to listen for the change-image event via the v-on directive. The event will be handled by a method changeImage which will have a single parameter, val, reflecting the payload being sent in the event. The method will then use val to step the value of index, ensuring it loops to the start or end if it exceeds the bounds of the array it indexes.

resources/assets/js/app.js:

```js
Vue.component('image-carousel', {
    template: `<div class="image-carousel">
                    <img v-bind:src="image">
                    <div class="controls">
                        <carousel-control dir="left" @change-image="changeImage"></carousel-control>
                        <carousel-control dir="right" @changeImage="changeImage"></carousel-control>
                    </div>
               </div>`,
    props: ['images'],
    data() {
        return {
            index: 0,
        }
    },
    computed: {
        image() {
            return this.images[this.index];
        }
    },
    components: {
        'carousel-control': {
            template: `<i :class="classes" @click="clicked"></i>`,
            props: ['dir'],
            computed: {
                classes() {
                    return 'carousel-control fa fa-2x fa-chevron-' + this.dir;
                }
            },
            methods: {
                clicked() {
                    this.$emit('change-image', this.dir === 'left' ? -1 : 1);
                }
            },
        }
    },
    methods: {
        changeImage(val) {
            let newVal = this.index + parseInt(val);
            if (newVal < 0) {
                this.index = this.images.length - 1;
            } else if (newVal === this.images.length) {
                this.index = 0;
            } else {
                this.index = newVal;
            }
        },
    },
});
```

With this done, the image carousel will now work perfectly:

Figure 6.8. The state of the image carousel after the image has been changed

## 12. Single-file components

Single-File Components (SFCs) are files with a .vue extension that contain the complete definition of a single component and can be imported into your Vue.js app. SFCs make it simple to create and use components, and come with a variety of other benefits which we'll soon explore. SFCs are similar to HTML files but have (at most) three root elements: 1) template. 2) script. 3) style.

The component definition goes inside the script tag and will be exactly like any other component definition except: 1) It will export an ES module. 2) It will not need a template property (or a render function; more on that later).

The component's template will be declared as HTML markup inside the template tag. This should be a welcome relief from writing cumbersome template strings! The style tag is a feature unique to SFCs and can contain any CSS rules you need for the component. This mostly just helps with the organization of your CSS. Here's an example of the declaration and usage of a single-file component.

MyComponent.vue:

```js
<template> 
    <div id="my-component">{{ title }}</div> 
</template> 
<script> 
    export default { 
        data() { 
            title: 'My Component' 
        } 
    }; 
</script> 
<style> 
    .my-component { 
        color: red; 
    } 
</style>
```

app.js:

```js
import 'MyComponent' from './MyComponent.vue'; 

new Vue({ 
    el: '#app', 
    components: { MyComponent } 
});
```

## 13. Transformation

To use a single-file component in your app, you simply import it like it were an ES module. The .vue file is not a valid JavaScript module file, however. Just like we use the Webpack Babel plugin to transpile our ES2015 code into ES5 code, we must use Vue Loader to transform .vue files into JavaScript modules.

Vue Loader is already configured by default with Laravel Mix, so there's nothing further we need to do in this project; any SFCs we import will just work! To learn more about Vue Loader, check out the documentation at [Introduction | Vue Loader](https://vue-loader.vuejs.org/).

## 14. Refactoring components to SFCs

Our resource/assets/js/app.js file is almost 100 lines long now. If we keep adding components, it will start to get unmanageable, so it's time to think about splitting it up. Let's begin by refactoring our existing components to be SFCs. First, we'll create a new directory, then we will create the .vue files:

```
$ mkdir resources/assets/components 
$ touch resources/assets/components/ImageCarousel.vue 
$ touch resources/assets/components/CarouselControl.vue
```

Starting with ImageCarousel.vue, the first step is to create the three root elements.

resources/assets/components/ImageCarousel.vue:

```
<template></template> 
<script></script> 
<style></style>
```

Now, we move the template string into the template tag, and the component definition into the script tag. The component definition must be exported as a module.

resources/assets/components/ImageCarousel.vue:

```js
<template>
    <div class="image-carousel">
        <img v-bind:src="image">
        <div class="controls">
            <carousel-control dir="left" 
                @change-image="changeImage"></carousel-control>
            <carousel-control dir="right" 
                @change-image="changeImage"></carousel-control>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['images'],
        data() {
            return {
                index: 0,
            }
        },
        computed: {
            image() {
                return this.images[this.index];
            }
        },
        components: {
            'carousel-control': {
                template: `<i :class="classes" @click="clicked"></i>`,
                props: ['dir'],
                computed: {
                    classes() {
                        return 'carousel-control fa fa-2x fa-chevron-' + this.dir;
                    }
                },
                methods: {
                    clicked() {
                        this.$emit('change-image', this.dir === 'left' ? -1 : 1);
                    }
                },
            }
        },
        methods: {
            changeImage(val) {
                let newVal = this.index + parseInt(val);
                if (newVal < 0) {
                    this.index = this.images.length - 1;
                } else if (newVal === this.images.length) {
                    this.index = 0;
                } else {
                    this.index = newVal;
                }
            },
        },
    }
</script>

<style>

</style>
```

Now we can import this file into our app and register it locally in the root instance. As mentioned, Vue is able to automatically switch between kebab-case component names and Pascal-case ones. This means we can use the object shorthand syntax inside the component configuration and Vue will correctly resolve it.

resources/assets/js/app.js:

```js
import ImageCarousel from '../components/ImageCarousel.vue'; 

var app = new Vue({ 
    ... 
    components: { ImageCarousel } 
});
```

Be sure to delete any remaining code from the original ImageCarousel component definition in app.js before moving on.

### 14.1 CSS

SFCs allow us to add style to a component, helping to better organize our CSS code. Let's move the CSS rules we created for the image carousel into this new SFC's style tag:

```css
<template>...</template> 
<script>...</script> 

<style> 
    .image-carousel { 
        height: 100%; 
        margin-top: -12vh; 
        position: relative; 
        display: flex; 
        align-items: center; 
        justify-content: center; 
    } 
    .image-carousel img { 
        width: 100%; 
    } 
    .image-carousel .controls { 
        position: absolute; 
        width: 100%; 
        display: flex; 
        justify-content: space-between; 
    } 
</style>
```

When the project builds, you should find it still appears the same. The interesting thing, though, is where the CSS has ended up in the build. If you check public/css/style.css, you'll find it's not there. It's actually included in the JavaScript bundle as a string:

Figure 6.9. CSS stored as a string in the JavaScript bundle file

To use it, Webpack's bootstrapping code will inline this CSS string into the head of the document when the app runs:

Figure 6.10. Inlined CSS in document head

1『样式跑到头文件里去了。』

Inlining CSS is actually the default behavior of Vue Loader. However, we can override this and get Webpack to write SFC styles to their own file. Add the following to the bottom of the Mix configuration.

webpack.mix.js:

```js
mix.options({ 
    extractVueStyles: 'public/css/vue-style.css' 
});
```

Now an additional file, public/css/vue-style.css, will be outputted in the build:

Figure 6.11. Webpack output including single-file component styles

We'll need to load this new file in our view, after the main style sheet.

resources/views/app.blade.php:

```php
<head> 
    ... 
    <link rel="stylesheet" href="{{ asset('css/style.css') }}" type="text/css"> 
    <link rel="stylesheet" href="{{ asset('css/vue-style.css') }}" type="text/css"> 
    ... 
</head>
```

### 14.2 CarouselControl

Let's now abstract our CarouselControl component into an SFC, and move any relevant CSS rules from resources/assets/css/style.css as well.

resources/assets/components/CarouselControl.vue:

```js
<template>
    <i :class="classes" @click="clicked"></i>
</template>

<script>
export default {
    props: ['dir'],
    computed: {
        classes() {
            return 'carousel-control fa fa-2x fa-chevron-' + this.dir;
        }
    },
    methods: {
        clicked() {
            this.$emit('change-image', this.dir === 'left' ? -1 : 1);
        }
    },
}
</script>

<style>
    .carousel-control {
        padding: 1rem;
        color: #ffffff;
        opacity: 0.85;
    }

    @media (min-width: 744px) {
        .container {
            width: 696px;
        }
        .carousel-control {
            font-size: 3rem;
        }
    }
</style>
```

This file can now be imported by the ImageCarousel component.

resources/assets/components/ImageCarousel.vue:

```js
<template>...</style> 
<script> 
    import CarouselControl from '../components/CarouselControl.vue'; 
    export default { 
        ... 
        components: { CarouselControl } 
    } 
</script> 
<style>...</style>
```

With that done, our existing components have been refactored to SFCs. This has not made any obvious difference to the functionality of our app (although it is slightly faster, as I'll explain later), but it will make development easier as we continue.

## 15. Content distribution

Imagine you're going to build a component-based Vue.js app that resembles the following structure:

![](./res/2020008.png)

Figure 6.12. Component-based Vue.js app

Notice that in the left-branch of the above diagram, Component C is declared by Component B. However, in the right branch, Component D is declared by a different instance of Component B.

With what you know about components so far, how would you make the template for Component B, given that it has to declare two different components? Perhaps it would include a v-if directive to use either Component C or Component D depending on some variable passed down as a prop from Component A. This approach would work, however, it makes Component B very inflexible, limiting its reusability in other parts of the app.

1『上面的痛点是「插槽」要解决的问题。』

## 16. Slots

We've learned so far that the content of a component is defined by its own template, not by its parent, so we wouldn't expect the following to work:

```html
<div id="app"> 
    <my-component> 
        <p>Parent content</p> 
    </my-component> 
</div>
```

But it will work if MyComponent has a slot. Slots are distribution outlets inside a component, defined with the special slot element:

```js
Vue.component('my-component', { 
    template: ` 
        <div> 
            <slot></slot> 
            <p>Child content</p> 
        </div>` 
}); 
new Vue({ 
    el: '#app' 
});
```

This renders as:

```js
<div id="app"> 
    <div> 
        <p>Parent content</p> 
        <p>Child content</p> 
    </div> 
</div>
```

If Component B has a slot in its template, like this:

```js
Vue.component('component-b', {
    template: '<slot></slot>'
});
```

We can solve the problem just stated without having to use a cumbersome v-for:

```html
<component-a> 
    <component-b> 
        <component-c></component-c> 
    </component-b> 
    <component-b> 
        <component-d></component-d> 
    </component-b> 
</component-a>
```

It's important to note that content declared inside a component in the parent template is compiled in the scope of the parent. Although it is rendered inside the child, it cannot access any of the child's data. The following example should distinguish this:

```js
<div id="app"> 
    <my-component> 
        <!--This works--> 
        <p>{{ parentProperty }}</p> 
        <!--This does not work. childProperty is undefined, as this content--> 
        <!--is compiled in the parent's scope--> 
        <p>{{ childProperty }} </p> 
    </my-component> 
</div> 

<script> 
    Vue.component('my-component', { 
        template: ` 
            <div> 
                <slot></slot> 
                <p>Child content</p> 
            </div>`, 
        data() { 
            return { childProperty: 'World' } 
        } 
    }); 
    new Vue({ el: '#app', data: { parentProperty: 'Hello' } }); 
</script>
```

## 17. Modal window

A lot of the functionality left in our root Vue instance concerns the modal window. Let's abstract this into a separate component. First, we'll create the new component file:

    $ touch resources/assets/components/ModalWindow.vue

Now, we'll transplant the markup from the view to the component. To ensure the carousel stays decoupled from the modal window, we'll replace the ImageCarousel declaration in the markup with a slot.

resources/assets/components/ModalWindow.vue:

```js
<template>
    <div id="modal" :class="{ show: modalOpen }">
        <button @click="modalOpen=false" class="modal-close">&times;</button>
        <div class="modal-content">
            <slot></slot>
        </div>
    </div>    
</template>
```

We can now declare a ModalWindow element in the hole we just created in the view, with an ImageCarousel as content for the slot.

resources/views/app.blade.php:

```js
<div id="app"> 
    <div class="header">...</div> 
    <div class="container">...</div> 
    <modal-window> 
        <image-carousel :images="images"></image-carousel> 
    </modal-window> 
</div>
```

We will now move the needed functionality from the root instance and place it inside the script tag.

resources/assets/components/ModalWindow.vue:

```js
<script>
    export default {
        data() {
            return {
                modalOpen: false,
            }
        },
        methods: {
            escapeKeyListenser: function(evt) {
                if (evt.keyCode === 27 && this.modalOpen) {
                    this.modalOpen = false;
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
        destoryed: function() {
            document.removeEventListener('keyup', this.escapeKeyListenser);
        },
    }
</script>
```

Next we import ModalWindow in the entry file.

resources/assets/js/app.js:

```js
// import "core-js/fn/object/assign";
import Vue from 'vue';
// window.Vue = require('vue');
import { populateAmenitiesAndPrices } from './helpers';
import ImageCarousel from '../components/ImageCarousel.vue';
import ModalWindow from '../components/ModalWindow.vue';

let model = JSON.parse(window.vuebnb_listing_model);
model = populateAmenitiesAndPrices(model);

// Vue 实例
var vm = new Vue({
    el: "#app",
    // ployfills
    data: Object.assign(model, {
        headerImageStyle: {
            "background-image": `url(${model.images[0]})`
        },
        contracted: true,
    }),
    components: { 
        ImageCarousel,
        ModalWindow,
    },
});
```

Finally, let's move any modal-related CSS rules into the SFC as well:

```css
<style>
    #modal {
        display: none;
        position: fixed;
        top: 0;
        bottom: 0;
        right: 0;
        left: 0;
        z-index: 2000;
        background-color: rgba(0, 0, 0, 0.85);
    }

    #modal.show {
        display: block;
    }

    body.modal-open {
        overflow: hidden;
        position: fixed;
    }

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

    .modal-content {
        height: 100%;
        max-width: 105vh;
        padding-top: 12vh;
        margin: 0 auto;
        position: relative;
    }
</style>
```

After the project builds, you'll notice the modal window won't open. We'll fix that in the next section. If you check Vue Devtools, you'll see a ModalWindow component in the hierarchy of components now:

Figure 6.13. Vue Devtools showing hierarchy of components

The representation of our app in Vue Devtools is slightly misleading. It makes it seem as though ImageCarousel is a child of ModalWindow. Even though ImageCarousel renders within ModalWindow due to the slot, these components are actually siblings!

## 18. Refs

In its initial state, the modal window is hidden with a display: none CSS rule. To open the modal, the user must click the header image. A click event listener will then set the root instance data property modelOpen to true, which will, in turn, add a class to the modal to overwrite the display: none to display: block.

1『数据流的走向。会解析业务的数据流很重要。』

After refactoring, however, modalOpen has been moved into the ModalWindow component along with the rest of the modal logic, and hence the modal opening functionality is currently broken. One possible way to fix this is to let the root instance manage the opened/closed state of the modal by moving the logic back into the root instance. We could then use a prop to inform the modal when it needs to open. When the modal is closed (this happens in the scope of the modal component, where the close button is) it would send an event to the root instance to update the state.

This approach would work, but it's not in the spirit of making our components decoupled and reusable; the modal component should manage its own state. How, then, can we allow the modal to keep its state, but let the root instance (the parent) change it? An event won't work, as events can only flow up, not down.

1『 Refs 是为了解决上面场景而生的。作者讲解知识点的方式很好，先抛出一个真实场景里遇到的问题，然后引出要学的技术，技术都是为了解决具体问题而创造出来的。』

ref is a special property that allows you to directly reference a child component's data. To use it, declare the ref property and assign it a unique value, such as imagemodal.

resources/views/app.blade.php:

```html
<modal-window ref="imagemodal"> 
    ... 
</modal-window>
```

Now the root instance has access to this specific ModalWindow component's data via the \$refs object. This means we can change the value of modalOpen inside a root instance method, just like we could from within ModalWindow.

resources/assets/js/app.js:

```js
methods: {
    openModal() {
        this.$ref.imagemodal.modalOpen = true;
    }
},
```

Now we can call the openModal method in the header image's click listener, thus restoring the modal opening functionality.

resources/views/app.blade.php:

```html
<div class="header">
    <div class="header-img" :style="headerImageStyle" @click="openModal">
        <button class="view-photos">View Photos</button>
    </div>
</div
```

It is an anti-pattern to use ref when the normal methods of interacting with a component, props and events, are sufficient. ref is usually only required for communicating with elements that fall outside of the normal flow of a page, as a modal window does.

## 19. Header image

Let's now abstract the header image into a component. Firstly, create a new .vue file:

    $ touch resources/assets/components/HeaderImage.vue

Now move in the markup, data, and CSS. Take note of the following modifications: 1) An event header-clicked must be emitted. This will be used to open the modal. 2) The image URL is passed as a prop, image-url, then transformed to be an inline style rule via a computed property.

resource/assets/components/HeaderImage.vue:

```js
<template>
    <div class="header">
        <div class="header-img" :style="headerImageStyle" 
            @click="$emit('header-clicked')">
            <button class="view-photos">View Photos</button>
        </div>
    </div>
</template>

<script>
    export default {
        computed: {
            headerImageStyle() {
                return {
                    "background-image": `url(${this.imageUrl})`}
            },
        },
        props: ['image-url'],
    }
</script>

<style>
    .header {
        height: 320px;
    }

    .header .header-img {
        background-repeat: no-repeat;
        background-size: cover;
        background-position: 50% 50%;
        background-color: #f5f5f5;
        height: 100%;
        cursor: pointer;
        position: relative;
    }

    .header .header-img button {
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
</style>
```

Once you've imported this component in resources/assets/js/app.js, declare it in the main template. Be sure to bind the image-url prop and handle the click event.

resources/views/app.blade.php:

```html
<header-image :image-url="images[0]" @header-clicked="openModal"></header-image>
```

## 20. Feature lists

Let's continue our process of refactoring Vuebnb into components, and abstract the amenities and prices lists. These lists have a similar purpose and structure, so it makes sense that we create a single, versatile component for both. Let's remind ourselves of how the markup for the lists currently looks.

resources/views/app.blade.php:

```html
<div class="lists">
    <hr>
    <div class="amenities list">
        <div class="title"><strong>Amentities</strong></div>
        <div class="content">
            <div class="list-item" v-for="amenity in amenities">
                <i class="fa fa-lg" v-bind:class="amenity.icon"></i>
                <span>@{{ amenity.title }}</span>
            </div>
        </div>
    </div>
    <hr>
    <div class="prices list">
        <div class="title"><strong>Prices</strong></div>
        <div class="content">
            <div class="list-item" v-for="price in prices">
                @{{ price.title }}: <strong>@{{ price.value }}</strong>
            </div>
        </div>
    </div>
</div>
```

The main difference between the two lists is inside the \<div class="content">...\</div> section, as the data being displayed in each list has a slightly different structure. The amenities have an icon and a title whereas the prices have a title and a value. We'll use a slot in this section to allow the parent to customize the content for each. But first, let's create the new FeatureList component file:

    $ touch resources/assets/components/FeatureList.vue

We'll move the markup for one of the lists in, using a slot to replace the list content. We'll also add a prop for the title and move in any list-related CSS.

resources/assets/components/FeatureList.vue:

```js
<template>
    <div>
        <hr>
        <div class="list">
            <div class="title"><strong>{{ title }}</strong></div>
            <div class="content">
                <slot></slot>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['title'],
    }
    </script>

    <style>
    hr {
        border: 0;
        border-top: 1px solid #dce0e0;
    }

    .list {
        display: flex;
        flex-wrap: nowrap;
        margin: 2em 0;
    }

    .list .title {
        flex: 1 1 25%;
    }
    
    .list .content {
        flex: 1 1 75%;
        display: flex;
        flex-wrap: wrap;
    }
    
    .list .list-item {
        flex: 0 0 50%;
        margin-bottom: 16px;
    }
    
    .list .list-item > i {
        width: 35px;
    }

    @media (max-width: 743px) {
        .list .title {
        flex: 1 1 33%;
        }
    
        .list .content {
        flex: 1 1 67%;
        }
    
        .list .list-item {
        flex: 0 0 100%;
        }
    }
</style>
```

Go ahead and import FeatureList into resources/assets/js/app.js, and add it to the locally registered components. Now we can use FeatureList in our main template, with a separate instance for each list.

1『这里有个之前遗漏的知识点，局部注册组件（locally registered components）。』

resources/views/app.blade.php:

```html
    <div class="lists">
        <feature-list title="Amenities">
            <div class="list-item" v-for="amenity in amenities">
                <i class="fa fa-lg" v-bind:class="amenity.icon"></i>
                <span>@{{ amenity.title }}</span>
            </div>
        </feature-list>
        <feature-list title="Prices">
            <div class="list-item" v-for="price in prices">
                @{{ price.title }}: <strong>@{{ price.value }}</strong>
            </div>
        </feature-list>
    </div>
```

## 21. Scoped slots

The FeatureList component works but is quite weak. The majority of the content comes through the slot and so it seems like the parent is doing too much work, and the child too little. Given that there's repeated code in both declarations of the component (\<div class="list-item" v-for="...">), it'd be good to delegate this to the child.

To allow our component template to be more versatile, we can use a scoped slot instead of a regular slot. Scoped slots allow you to pass a template to the slot instead of passing a rendered element. When this template is declared in the parent, it will have access to any props supplied in the child. 

For example, a component child with a scoped slot might look like the following:

1『上面的关键知识点：Scoped slots 的概念。』

```html
<div> 
    <slot my-prop="Hello from child"></slot> 
</div>
```

A parent that uses this component will declare a template element, which will have a property slot-scope that names an alias object. Any props added to the slot in the child template are available as properties of the alias object:

```html
<child> 
    <template slot-scope="props"> 
        <span>Hello from parent</span> 
        <span>{{ props.my-prop }}</span> 
    </template> 
</child>
```

This renders as:

```html
<div> 
    <span>Hello from parent</span> 
    <span>Hello from child</span> 
</div>
```

Let's go through the steps of including a scoped slot with our FeatureList component. The goal is to be able to pass the list items array in as a prop and get the FeatureList component to iterate them. That way, FeatureList is taking ownership of any repeated functionality. The parent will then provide a template to define how each list item should display.

resources/views/app.blade.php:

```html
<div class="lists"> 
    <feature-list title="Amenities" :items="amenities"> 
        <!--template will go here--> 
    </feature-list> 
    <feature-list title="Prices" :items="prices"> 
        <!--template will go here--> 
    </feature-list> 
</div>
```

Focusing now on the FeatureList component, follow these steps: 1) Add items to the props array in the configuration object. 2) items will be array which we iterate inside the \<div class="content"> section. 3) In the loop, item is an alias to any particular list item. We can create a slot and bind that list item to the slot using v-bind="item". (We haven't used v-bind without an argument before, but this will bind the properties of an entire object to the element. This is useful as the amenities and prices objects have different properties and we now don't have to specify them.)

resources/assets/components/FeatureList.vue:

```html
<template>
    <div>
        <hr>
        <div class="list">
            <div class="title"><strong>{{ title }}</strong></div>
            <div class="content">
                <div class="list-item" v-for="item in items">
                    <slot v-bind="item"></slot>
                </div>
            </div>
        </div>
    </div>
</template>
```

Now we'll return to our view. Let's work on the amenities list first: 1) Declare a template element inside the FeatureList declaration. 2) The template must include the slot-scope property to which we assign an alias, amenity. This alias allows us to access the scoped props. 3) Inside the template, we can use exactly the same markup we had before to display our amenity list items.

resources/views/app.blade.php:

```html
<div class="lists">
    <feature-list title="Amenities" :items="amenities">
        <template slot-scope="amenity">
            <i class="fa fa-lg" :class="amenity.icon"></i>
            <span>@{{ amenity.title }}</span>
        </template>
    </feature-list>
    <feature-list title="Prices" :items="prices">
        <template slot-scope="price">
            @{{ price.title }}: <strong>@{{ price.value }}</strong>
        </template>
    </feature-list>
</div>
```

Although this approach has just as much markup as before, it has delegated more common functionality to the component, which makes for a more robust design.

## 22. Expandable text

We created functionality back in Chapter 2, Prototyping Vuebnb, Your First Vue.js Project, to allow the About text to be partially contracted when the page loads and expanded to its full length by clicking a button. Let's abstract this functionality into a component as well:

    $ touch resources/assets/components/ExpandableText.vue

Move all the markup, configuration, and CSS into the new component. Note that we use a slot for the text content.

resources/assets/components/ExpandableText.vue:

```js
<template>
    <div>
        <p :class="{contracted: contracted}">
            <slot></slot>
        </p>
        <button class="more" v-if="contracted" @click="contracted=false">
            + More
        </button>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                contracted: true,
            }
        },
    }
</script>

<style>
    .about p {
        white-space: pre-wrap;
    }

    .about p.contracted {
        height: 250px;
        overflow: hidden;
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
</style>
```

Once you've imported this component in resources/assets/js/app.js, declare it in the main template, remembering to interpolate the about data property in the slot.

resource/views/app.blade.php:

```html
<div class="about">
    <h3>About this listing</h3>
    <expandable-text>@{{ about }}</expandable-text>
</div>
```

With that done, most of the data and functionality of the Vuebnb client app has been abstracted into components. Let's take a look at resources/assets/js/app.js and see how bare it has become!

resources/assets/js/app.js:

```js
// import "core-js/fn/object/assign";
import Vue from 'vue';
// window.Vue = require('vue');
import { populateAmenitiesAndPrices } from './helpers';
import ImageCarousel from '../components/ImageCarousel.vue';
import ModalWindow from '../components/ModalWindow.vue';
import HeaderImage from '../components/HeaderImage.vue';
import FeatureList from '../components/FeatureList.vue';
import ExpandableText from '../components/ExpandableText.vue';

let model = JSON.parse(window.vuebnb_listing_model);
model = populateAmenitiesAndPrices(model);

// Vue 实例
var vm = new Vue({
    el: "#app",
    // ployfills
    data: Object.assign(model, {}),
    components: { 
        ImageCarousel,
        ModalWindow,
        HeaderImage,
        FeatureList,
        ExpandableText,
    },
    methods: {
        openModal() {
            this.$refs.imagemodal.modalOpen = true;
        }
    },
});
```

1『这里 vue 实例里的数据，一直觉得很精妙「data: Object.assign(model, {}),」。』

## 23. Virtual DOM

Let's change tack now and discuss how Vue renders components. Take a look at this example:

```js
Vue.component('my-component', { 
    template: '<div id="my-component">My component</div>' 
});
```

In order for Vue to be able to render this component to the page, it will first transform the template string into a JavaScript object using an internal template compiler library:

![](./res/2020009.png)

Figure 6.14. How the template compiler turns a template string into an object

Once the template has been compiled, any state or directives can easily be applied. For example, if the template includes a v-for, a simple for-loop can be used to multiply the nodes and interpolate the correct variables. After that, Vue can interface with the DOM API to synchronize the page with the state of the component.

## 24. Render functions

Rather than supplying a string template for your component, you can instead supply a render function. Without understanding the syntax, you can probably tell from the following example that the render function is generating a semantically equivalent template to the string template in the previous example. Both define a div with an id attribute of my-component and with inner text of My component:

```js
Vue.component('my-component'</span>, { 
    render(createElement) { 
        createElement('div', {attrs:{id:'my-component'}}, 'My component'); 
        // Equivalent to <div id="my-component">My component</div> 
    } 
})
```

Render functions are more efficient because they don't require Vue to first compile the template string. The downside, though, is that writing a render function is not as easy or expressive as markup syntax, and, once you get a large template, will be difficult to work with.

## 25. Vue Loader

Wouldn't it be great if we could create HTML markup templates in development, then get Vue's template compiler to turn them into render functions as part of the build step? That would be the best of both worlds.

This is exactly what happens to single-file components when Webpack transforms them via Vue Loader. Take a look at the following snippet of the JavaScript bundle and you can see the ImageCarousel component after Webpack has transformed and bundled it:

1『上面说了 Vue Loader 可以解决的问题，目前还不是很清楚。（2020-04-26）』

Figure 6.15. image-carousel component in the bundle file

## 26. Refactoring the main template as single-file component

The template for our app's root instance is the content within the #app element in the app view. A DOM template like this requires the Vue template compiler, just like any string template does. If we were able to abstract this DOM template into an SFC as well, it would mean all our frontend app templates would be built as render functions and would not need to invoke the template compiler at runtime.

Let's create a new SFC for the main template and call it ListingPage, as this part of the app is our listing page:

    $ touch resources/assets/components/ListingPage.vue

We'll move the main template, root configuration and any relevant CSS into this component. Take note of the following: 1) We need to put the template inside a wrapping div as components must have a single root element. 2) We can now remove the @ escapes as this file won't be processed by Blade. 3) The component is now adjacent to the other components we created, so be sure to change the relative paths of the imports.

resource/assets/components/ListingPage.vue:

```js
<template>
    <div>
        <header-image :image-url="images[0]" 
        @header-clicked="openModal"></header-image>
        <div class="container">
            <div class="heading">
                <h1>{{ title }}</h1>
                <p>{{ address }}</p>
            </div>
            <hr>
            <div class="about">
                <h3>About this listing</h3>
                <expandable-text>{{ about }}</expandable-text>
            </div>
            <div class="lists">
                <feature-list title="Amenities" :items="amenities">
                    <template slot-scope="amenity">
                        <i class="fa fa-lg" :class="amenity.icon"></i>
                        <span>{{ amenity.title }}</span>
                    </template>
                </feature-list>
                <feature-list title="Prices" :items="prices">
                    <template slot-scope="price">
                        {{ price.title }}: <strong>{{ price.value }}</strong>
                    </template>
                </feature-list>
            </div>
        </div>
        <modal-window ref="imagemodal">
            <image-carousel :images="images"></image-carousel> 
        </modal-window>
    </div>
</template>

<script>
    import { populateAmenitiesAndPrices } from '../js/helpers';
    import ImageCarousel from './ImageCarousel.vue';
    import ModalWindow from './ModalWindow.vue';
    import HeaderImage from './HeaderImage.vue';
    import FeatureList from './FeatureList.vue';
    import ExpandableText from './ExpandableText.vue';

    let model = JSON.parse(window.vuebnb_listing_model);
    model = populateAmenitiesAndPrices(model);

    export default {
        data() {
            return Object.assign(model, {});
        },
        components: { 
            ImageCarousel,
            ModalWindow,
            HeaderImage,
            FeatureList,
            ExpandableText,
        },
        methods: {
            openModal() {
                this.$refs.imagemodal.modalOpen = true;
            }
        },
}
</script>

<style>
    .about {
        margin-top: 2em;
    }

    .about h3 {
        font-size: 22px;
    }
</style>
```

## 27. Mounting the root-level component with a render function

Now the mount element in our main template will be empty. We need to declare the Listing component, but we don't want to do it in the view.

resources/views/app.blade.php:

```html
<div id="app">
    <listing-page></listing-page>
</div>
```

If we do it like that, we wouldn't fully eliminate all string and DOM templates from our app, so we'll keep the mount element empty.

resources/views/app.blade.php:

```html
... 
<div id="app"></div> 
...
```

We can now declare Listing with a render function inside our root instance.

resources/assets/js/app.js:

```js
// import "core-js/fn/object/assign";
// window.Vue = require('vue');
import Vue from 'vue';
import ListingPage from '../components/ListingPage.vue';

// Vue 实例
var vm = new Vue({
    el: "#app",
    render: h => h(ListingPage),
    // components: {ListingPage},
});
```

1『又往上抽象了一层，太赞了。』

To avoid getting side-tracked, I won't explain the syntax of render functions here, as this is the only one we'll write throughout the book. If you'd like to learn more about render functions, check out the Vue.js documentation at https://vuejs.org/.

Now that Vuebnb is no longer using string or DOM templates, we don't need the template compiler functionality anymore. There's a special build of Vue we can use which doesn't include it!

1『

抽象到单页后报错：

```html
ERROR in ./resources/assets/components/ListingPage.vue?vue&type=template&id=3e09ee1e& (./node_modules/vue-loader/lib/loaders/templateLoader.js??vue-loader-options!./node_modules/vue-loader/lib??vue-loader-options!./resources/assets/components/ListingPage.vue?vue&type=template&id=3e09ee1e&)
Module Error (from ./node_modules/vue-loader/lib/loaders/templateLoader.js):
(Emitted value instead of an instance of Error)

  Errors compiling template:

  tag <image-carousel> has no matching end tag.

  28 |      </div>
  29 |      <modal-window ref="imagemodal">
  30 |          <image-carousel :images="images"><image-carousel/>
     |          ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  31 |      </modal-window>
  32 |  </div>

 @ ./resources/assets/components/ListingPage.vue?vue&type=template&id=3e09ee1e& 1:0-215 1:0-215
 @ ./resources/assets/components/ListingPage.vue
 @ ./resources/assets/js/app.js
 @ multi ./resources/assets/js/app.js
```

找了半天发现是 \<image-carousel> 写错了，改为：
```
<modal-window ref="imagemodal">
    <image-carousel :images="images"></image-carousel> 
</modal-window>
```

又一次体验到「细节」的重要性。

』

## 28. Vue.js builds

There are a number of different environments and use cases for running Vue.js. In one project, you might load Vue directly in the browser, in another you may load it on a Node.js server for the purpose of server rendering. As such, there are different builds of Vue provided so you can choose the most suitable one.

Looking in the dist folder of the Vue NPM package, we can see eight different Vue.js builds:

```
-rw-r--r--   1 Daglas  staff   313K  4 11 22:36 vue.common.dev.js
-rw-r--r--   1 Daglas  staff   157B  4 11 22:36 vue.common.js
-rw-r--r--   1 Daglas  staff    91K  4 11 22:36 vue.common.prod.js
-rw-r--r--   1 Daglas  staff   308K  4 11 22:36 vue.esm.browser.js
-rw-r--r--   1 Daglas  staff    91K  4 11 22:36 vue.esm.browser.min.js
-rw-r--r--   1 Daglas  staff   319K  4 11 22:36 vue.esm.js
-rw-r--r--   1 Daglas  staff   334K  4 11 22:36 vue.js
-rw-r--r--   1 Daglas  staff    91K  4 11 22:36 vue.min.js
-rw-r--r--   1 Daglas  staff   218K  4 11 22:36 vue.runtime.common.dev.js
-rw-r--r--   1 Daglas  staff   173B  4 11 22:36 vue.runtime.common.js
-rw-r--r--   1 Daglas  staff    63K  4 11 22:36 vue.runtime.common.prod.js
-rw-r--r--   1 Daglas  staff   222K  4 11 22:36 vue.runtime.esm.js
-rw-r--r--   1 Daglas  staff   233K  4 11 22:36 vue.runtime.js
-rw-r--r--   1 Daglas  staff    63K  4 11 22:36 vue.runtime.min.js
```

Figure 6.16. The various builds in the node\_modules/vue/dist folder

The Vue.js website provides a table to explain these eight different builds:

### 28.1 Module system

The columns of the table categorize the builds as either UMD, CommonJS, or ES Module. We discussed CommonJS and ES modules back in Chapter 5, Integrating Laravel And Vue.js with Webpack, but we didn't mention UMD (Universal Module Definition). The main things you need to know about UMD is that it's yet another module pattern, and that it works well in a browser. UMD is the choice if you are directly linking to Vue in a script tag.

### 28.2 Production builds

The rows of the table are split into two types: full or runtime, and with or without production. A production build is used in a deployed app, as opposed to one running in development. It has been minified, and any warnings, comments, or other development options are turned off or stripped out. The point is to make the build as small and secure as possible, which is what you'd want in production.

Note that there is only a UMD version of the production build as only UMD runs directly in a browser. CommonJS and ES Module are to be used in conjunction with a build tool, like Webpack, which provides its own production processing.

### 28.3 Full build vs runtime-only

As we've been discussing, Vue includes a template compiler for converting any string or DOM templates to render functions at runtime. The full build includes the template compiler and is what you would normally use. However, if you've already transformed your templates into render functions in development, you can use the runtime-only build, which drops the compiler and is about 30% smaller!

### 28.4 Selecting a build

A good build for Vuebnb is vue.runtime.esm.js since we're using Webpack and we don't need the template compiler. We could also use vue.runtime.common.js, but that wouldn't be consistent with our use of ES modules elsewhere in the project. In practice, though, there is no difference as Webpack will process them in the same way.

Remember that we include Vue at the top of our entry file with the statement import Vue from 'vue'. The last 'vue' is an alias to the Vue build that Webpack resolves when it runs. Currently, this alias is defined within the default Mix configuration and is set to the build vue.common.js. We can override that configuration by adding the following to the bottom of our webpack.mix.js file.

```js
webpack.mix.js:

...

mix.webpackConfig({ 
    resolve: { 
        alias: { 
            'vue$': 'vue/dist/vue.runtime.esm.js' 
        } 
    } 
});
```

After a new build, we should expect to see a smaller bundle size due to the template compiler being removed. In the following screenshot, I've shown the bundle before and after I ran a dev build in a separate Terminal tab:

Figure 6.17. The difference between bundle sizes after applying the runtime-only build

Keep in mind that without the template compiler we can no longer provide string templates for our components. Doing so will cause an error at runtime. That shouldn't be a problem though since we've got the far more powerful option of SFCs.

## Summary

In this chapter, we saw how components are used to create reusable custom elements. We then registered our first Vue.js components, defining them with template strings. Next, we looked at component communication with props and custom events. We used this knowledge to build an image carousel within the listing page modal window.

In the second half of the chapter, we got an introduction to single-file components, which we used to refactor Vuebnb into a component-based architecture. We then learned how slots can help us make more versatile components by combining parent and child content. Finally, we saw how the runtime-only build can be used to give a Vue app a smaller size.

In the next chapter, we will make Vuebnb a multi-page app by building a home page, and using Vue Router to allow navigation between pages without reloading.
# 2020121Full-Stack-Vuejs2-R02

## 记忆时间

## 0601. Composing Widgets with Vue.js Components

Components are becoming an essential aspect of frontend development, and are a feature in most modern frontend frameworks, including Vue, React, Angular, Polymer, and so on. Components are even becoming native to the web through a new standard called Web Components.

In this chapter, we will use components to create an image carousel for Vuebnb, which allows users to peruse the different photos of a room listing. We'll also refactor Vuebnb to conform to a component-based architecture. Topics covered in this chapter: 1) What components are and how to create them with Vue.js. 2) Component communication through props and events. 3) Single-file components-one of Vue's most useful features. 4) Adding custom content to a component with slots. 5) The benefit of architecting apps entirely from components. 6) How render functions can be used to skip the template compiler. 7) Using the runtime-only build of Vue to lighten the bundle size.

### Summary

In this chapter, we saw how components are used to create reusable custom elements. We then registered our first Vue.js components, defining them with template strings. Next, we looked at component communication with props and custom events. We used this knowledge to build an image carousel within the listing page modal window.

In the second half of the chapter, we got an introduction to single-file components, which we used to refactor Vuebnb into a component-based architecture. We then learned how slots can help us make more versatile components by combining parent and child content. Finally, we saw how the runtime-only build can be used to give a Vue app a smaller size. In the next chapter, we will make Vuebnb a multi-page app by building a home page, and using Vue Router to allow navigation between pages without reloading.

### 6.1 Components

When we're constructing a template for a web app, we can use HTML elements such as div, table, and span. This variety of elements makes it easy to create whatever structures we need for organizing content on the page. What if we could create our own custom elements, through, for example, my-element? This would allow us to create reusable structures specifically designed for our app.

Components are a tool for creating custom elements in Vue.js. When we register a component, we define a template which renders as one or more standard HTML elements:

#### 6.1.1 Registration

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

#### 6.1.2 Data

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

### 6.2 Image carousel

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

#### 6.2.1 Changing images

The point of a carousel is to allow the user to peruse a collection of images without having to scroll the page. To permit this functionality, we'll need to create some UI controls. But first, let's add a new data property, index, to our component, which will dictate the current image being displayed. It will be initialized at 0 and the UI controls will later be able to increment or decrement the value. We will bind the image source to the array item at position index.

A page refresh should, again, reveal no change to what you see on screen. However, if you initialize the value of index to 1, 2, or 3, you will find a different image is shown when you re-open the modal window:

### 6.3 Computed properties

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

### 6.4 Composing with components

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

### 6.5 Registration scope

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

### 6.6 Carousel controls

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

### 6.7 Communicating with components

A key aspect of components is that they are reusable, which is why we give them their own state to keep them independent from the rest of the app. However, we may still want to send in data, or send it out. Components have an interface for communicating with other parts of the app, which we will now explore.

#### 6.7.1 Props

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

#### 6.7.2 One-way data flow

Since props must be declared in the template where the component is used, prop data can only pass from a parent to a child. This is why you shouldn't mutate a prop - since data flows down, the change will not be reflected in the parent, and therefore you will have different versions of what is meant to be the same bit of state. If you do need to tell the owner to change the data, there is a separate interface for passing data from a child to a parent, which we'll see later.

1『 prop data 的数据流是自上而下的，只能从父模板传递到子模板。』

#### 6.7.3 Dynamic props

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

1『注意，码了一遍发现报错，title 变量未定义。因为是在 laravel 框架里，绑定数据的格式跟 blade 冲突，所以得在前面加一个 @。』

Since the v-bind directive is used so commonly in templates, you can omit the directive name as a shorthand: \<div v-bind:title="title"> can be shortened to \<div :title="title">.

### 6.8 Image URLs

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

### 6.9 Distinguishing carousel controls

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

### 6.10 Custom events

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

### 6.11 Changing carousel images

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

1『

发现左箭头可以，右箭头没反应。定位到作者源码里右箭头点击事件，绑定的方法名称写错了，更改如下：

```html
<div class="controls">
    <carousel-control dir="left" @change-image="changeImage"></carousel-control>
    <carousel-control dir="right" @change-image="changeImage"></carousel-control>
</div>
```

』

### 6.12 Single-file components

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

### 6.13 Transformation

To use a single-file component in your app, you simply import it like it were an ES module. The .vue file is not a valid JavaScript module file, however. Just like we use the Webpack Babel plugin to transpile our ES2015 code into ES5 code, we must use Vue Loader to transform .vue files into JavaScript modules.

1『如同 Webpack Babel 将 ES2015 code 转换为 ES5 code，Vue Loader 将 .vue files 转换为 JavaScript modules。』

Vue Loader is already configured by default with Laravel Mix, so there's nothing further we need to do in this project; any SFCs we import will just work! To learn more about Vue Loader, check out the documentation at [Introduction | Vue Loader](https://vue-loader.vuejs.org/).

### 6.14 Refactoring components to SFCs

Our resource/assets/js/app.js file is almost 100 lines long now. If we keep adding components, it will start to get unmanageable, so it's time to think about splitting it up. Let's begin by refactoring our existing components to be SFCs. First, we'll create a new directory, then we will create the .vue files:

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


#### 6.14.1 CSS

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

To use it, Webpack's bootstrapping code will inline this CSS string into the head of the document when the app runs:

1『样式跑到头文件里去了。』

Inlining CSS is actually the default behavior of Vue Loader. However, we can override this and get Webpack to write SFC styles to their own file. Add the following to the bottom of the Mix configuration.

webpack.mix.js:

```js
mix.options({ 
    extractVueStyles: 'public/css/vue-style.css' 
});
```

Now an additional file, public/css/vue-style.css, will be outputted in the build:

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

#### 6.14.2 CarouselControl

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

### 6.15 Content distribution

Imagine you're going to build a component-based Vue.js app that resembles the following structure:

Notice that in the left-branch of the above diagram, Component C is declared by Component B. However, in the right branch, Component D is declared by a different instance of Component B.

With what you know about components so far, how would you make the template for Component B, given that it has to declare two different components? Perhaps it would include a v-if directive to use either Component C or Component D depending on some variable passed down as a prop from Component A. This approach would work, however, it makes Component B very inflexible, limiting its reusability in other parts of the app.

1『上面的痛点是「插槽」要解决的问题。』

### 6.16 Slots

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

### 6.17 Modal window

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

After the project builds, you'll notice the modal window won't open. We'll fix that in the next section. If you check Vue Devtools, you'll see a ModalWindow component in the hierarchy of components now:

1『报错记录：app.js:1576 [Vue warn]: Property or method "modalOpen" is not defined on the instance but referenced during render. Make sure that this property is reactive, either in the data option, or for class-based components, by initializing the property. See: https://vuejs.org/v2/guide/reactivity.html#Declaring-Reactive-Properties. 』

The representation of our app in Vue Devtools is slightly misleading. It makes it seem as though ImageCarousel is a child of ModalWindow. Even though ImageCarousel renders within ModalWindow due to the slot, these components are actually siblings!

### 6.18 Refs

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













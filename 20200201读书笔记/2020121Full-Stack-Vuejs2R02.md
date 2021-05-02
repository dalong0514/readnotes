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

1『确实，组件就好比小型的 vue 实例。』

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

1『用场景解释为什么组件里的数据要使用 return 语句返回一个对象。』

### 6.2 Image carousel

Let's build a new feature for the Vuebnb frontend app using components. As you'll recall from previous chapters, each of our mock data listings has four different images, and we're passing the URLs to the frontend app. To allow the user to peruse these images, we're going to create an image carousel. This carousel will replace the static image that currently occupies the modal window that pops up when you click the header of a listing. Begin by opening the app view. Remove the static image and replace it with a custom HTML element image-carousel.

resources/views/app.blade.php:

```html
<div class="modal-content"> 
    <image-carousel></image-carousel> 
</div>
```

A component can be referred to in your code by a kebab-case name such as my-component, a PascalCase name such as MyComponent, or a camelCase name such as myComponent. Vue sees these all as the same component. However, in a DOM or string template, the component should always be kebab-cased. Vue doesn't enforce this, but markup in the page gets parsed by the browser before Vue gets to work with it, so it should conform to W3C naming conventions or the parser may strip it out.

1『又看到接触过的 3 种命名方式：kebab-case、PascalCase、camelCase，推荐使用 kebab-cased，因为 DOM 和 string template 用它。』

Let's now register the component in our entry file. The template of this new component will simply be the image tag we removed from the view, wrapped in a div. We add this wrapping element, as component templates must have a single root element, and we'll soon be adding more elements inside it.

1『从定义的语法上看，组件与根实例是并列结构的。』

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

1『隐喻：prop data 是从其他组件或实例里借来的数据，所以只有原主人可以修改。也解释了后面看到的，组件的数据流只能自上而下。』

Props are proxied to the instance just like data properties, meaning you can refer to a prop as this.myprop within that component's code. Be sure to name your props uniquely to your data properties to avoid a clash!

#### 6.7.2 One-way data flow

Since props must be declared in the template where the component is used, prop data can only pass from a parent to a child. This is why you shouldn't mutate a prop - since data flows down, the change will not be reflected in the parent, and therefore you will have different versions of what is meant to be the same bit of state. If you do need to tell the owner to change the data, there is a separate interface for passing data from a child to a parent, which we'll see later.

1『 prop data 的数据流是自上而下的，只能从父模板传递到子模板。』

#### 6.7.3 Dynamic props

We can reactively bind data to a component using the v-bind directive. When the data changes in the parent, it will automatically flow down to the child. In the following example, the value of title in the root instance gets programmatically updated after two seconds. This change will automatically flow down to MyComponent, which will reactively re-render to display the new value:

```html
<body>
    <div id="app">
        <my-component :title="title"></my-component>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        Vue.component('my-component', {
            template: `<div>@{{ title }}</div>`,
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

```html
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

1『子模板可以通过 emits 通知父模板，需要改变什么数据值。简单说子组件通过 emits 发的通知可以被父组件监听到，父组件根据通知做出动作。这个过程跟 html 文件那边的事件很相似，浏览器对应于父组件，猜测因为这种类似的过程所以被称为「Custom events」。自定义组件解决了数据从向往上反馈的难题。』

```html
<body>
    <div id="app">
        <my-component @toggle="toggle=!toggle"></my-component>
        @{{ message }}
    </div>
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

1『父组件里，通过在 methods 里定义一个监听方法来处理子组件发送过来的通知。changeImage() 是父组件的监听方法，传入的参数 val 是子组件发送过来的通知。』

resources/assets/js/app.js:

```html
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

```html
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

```html
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

### 6.19 Header image

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
...
</style>
```

Once you've imported this component in resources/assets/js/app.js, declare it in the main template. Be sure to bind the image-url prop and handle the click event.

resources/views/app.blade.php:

```html
<header-image :image-url="images[0]" @header-clicked="openModal"></header-image>
```

### 6.20 Feature lists

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
...
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

### 6.21 Scoped slots

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

### 6.22 Expandable text

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
...
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

### 6.23 Virtual DOM

Let's change tack now and discuss how Vue renders components. Take a look at this example:

```js
Vue.component('my-component', { 
    template: '<div id="my-component">My component</div>' 
});
```

In order for Vue to be able to render this component to the page, it will first transform the template string into a JavaScript object using an internal template compiler library:

Figure 6.14. How the template compiler turns a template string into an object

Once the template has been compiled, any state or directives can easily be applied. For example, if the template includes a v-for, a simple for-loop can be used to multiply the nodes and interpolate the correct variables. After that, Vue can interface with the DOM API to synchronize the page with the state of the component.

### 6.24 Render functions

Rather than supplying a string template for your component, you can instead supply a render function. Without understanding the syntax, you can probably tell from the following example that the render function is generating a semantically equivalent template to the string template in the previous example. Both define a div with an id attribute of my-component and with inner text of My component:

```js
Vue.component('my-component', { 
    render(createElement) { 
        createElement('div', {attrs:{id:'my-component'}}, 'My component'); 
        // Equivalent to <div id="my-component">My component</div> 
    } 
})
```

Render functions are more efficient because they don't require Vue to first compile the template string. The downside, though, is that writing a render function is not as easy or expressive as markup syntax, and, once you get a large template, will be difficult to work with.

### 6.25 Vue Loader

Wouldn't it be great if we could create HTML markup templates in development, then get Vue's template compiler to turn them into render functions as part of the build step? That would be the best of both worlds.

This is exactly what happens to single-file components when Webpack transforms them via Vue Loader. Take a look at the following snippet of the JavaScript bundle and you can see the ImageCarousel component after Webpack has transformed and bundled it:

1『 Vue Loader 可以解决上面提到的问题，即 render function 难写。』

Figure 6.15. image-carousel component in the bundle file

### 6.26 Refactoring the main template as single-file component

The template for our app's root instance is the content within the #app element in the app view. A DOM template like this requires the Vue template compiler, just like any string template does. If we were able to abstract this DOM template into an SFC as well, it would mean all our frontend app templates would be built as render functions and would not need to invoke the template compiler at runtime.

Let's create a new SFC for the main template and call it ListingPage, as this part of the app is our listing page:

    $ touch resources/assets/components/ListingPage.vue

We'll move the main template, root configuration and any relevant CSS into this component. Take note of the following: 1) We need to put the template inside a wrapping div as components must have a single root element. 2) We can now remove the @ escapes as this file won't be processed by Blade. 3) The component is now adjacent to the other components we created, so be sure to change the relative paths of the imports.

1『注意点：这个根组件必须最外层有个 \<div> 标签；数据绑定可以移除 @ 了，在根组件里不会跟 blade 冲突了；导入其他组件的文路径得改了。』

resource/assets/components/ListingPage.vue:

```js
<template>
    <div>
        ...
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
...
</style>
```

### 6.27 Mounting the root-level component with a render function

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

### 6.28 Vue.js builds

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

The Vue.js website provides a table to explain these eight different builds:

#### 6.28.1 Module system

The columns of the table categorize the builds as either UMD, CommonJS, or ES Module. We discussed CommonJS and ES modules back in Chapter 5, Integrating Laravel And Vue.js with Webpack, but we didn't mention UMD (Universal Module Definition). The main things you need to know about UMD is that it's yet another module pattern, and that it works well in a browser. UMD is the choice if you are directly linking to Vue in a script tag.

#### 6.28.2 Production builds

The rows of the table are split into two types: full or runtime, and with or without production. A production build is used in a deployed app, as opposed to one running in development. It has been minified, and any warnings, comments, or other development options are turned off or stripped out. The point is to make the build as small and secure as possible, which is what you'd want in production.

Note that there is only a UMD version of the production build as only UMD runs directly in a browser. CommonJS and ES Module are to be used in conjunction with a build tool, like Webpack, which provides its own production processing.

1『应该是要选 ES Module，只有 ES Module 和 CommonJS 可以跟 Webpack 结合。ES Module 里面又有 2 个：vue.esm.js 和 vue.runtime.esm.js，vue.esm.js 生产环境用，而 vue.runtime.esm.js 开发环境用。』

#### 6.28.3 Full build vs runtime-only

As we've been discussing, Vue includes a template compiler for converting any string or DOM templates to render functions at runtime. The full build includes the template compiler and is what you would normally use. However, if you've already transformed your templates into render functions in development, you can use the runtime-only build, which drops the compiler and is about 30% smaller!

#### 6.28.4 Selecting a build

A good build for Vuebnb is vue.runtime.esm.js since we're using Webpack and we don't need the template compiler. We could also use vue.runtime.common.js, but that wouldn't be consistent with our use of ES modules elsewhere in the project. In practice, though, there is no difference as Webpack will process them in the same way.

Remember that we include Vue at the top of our entry file with the statement import Vue from 'vue'. The last 'vue' is an alias to the Vue build that Webpack resolves when it runs. Currently, this alias is defined within the default Mix configuration and is set to the build vue.common.js. We can override that configuration by adding the following to the bottom of our webpack.mix.js file.

1『默认加载的是 vue.common.js。』

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

1『最后改为「vue.esm.js」，性能差点无所谓，按作者的意思如果不使用 SFCs，即涉及到模板编译的时候，vue.runtime.esm.js 应该有问题。（2020-04-26）』

## 0701. Building a Multi-Page App with Vue Router

In the last chapter, we learned about Vue.js components and converted Vuebnb to a component-based architecture. Now that we've done this, we can easily add new pages to our app using Vue Router. In this chapter, we'll create a home page for Vuebnb, including a gallery of clickable thumbnails that showcase the full set of mock listings.

Topics covered in this chapter: 1) An explanation of what router libraries are and why they are a critical part of single-page applications. 2) An overview of Vue Router and its main features. 3) Installation and basic configuration of Vue Router. 4) Using the RouterLink and RouterView special components to manage page navigation. 5) Setting up AJAX with Vue to retrieve data from the web service without a page refresh. 7) Using route navigation guards to retrieve data before a new page is loaded.

3『官方文档：[Introduction | Vue Router](https://router.vuejs.org/)。』

### Summary

In this chapter, we learned how router libraries work and why they are a crucial addition to SPAs. We then got familiar with the key features of Vue Router including the route object, navigation guards, and the RouterLink and RouterView special components. Putting this knowledge into practice, we installed Vue Router and configured it for use in our app. We then built a home page for Vuebnb, including a gallery of listing summaries organized within image sliders. Finally, we implemented an architecture for correctly matching pages with either available local data or new data retrieved from the web service via AJAX.

1『这一章的核心内容：路由对象、路由连接和路由页面这 2 个组件、导航卫士。』

Now that we have a substantial number of components in our app, many of which communicate data between one another, it's time to investigate another key Vue.js tool: Vuex. Vuex is a Flux-based library that offers a superior way of managing application state.

### 7.1 Single-page applications

Most websites are broken up into pages in order to make the information they contain easier to consume. Traditionally this is done with a server/client model, where each page must be loaded from the server with a different URL. To navigate to a new page, the browser must send a request to the URL of that page. The server will send the data back and the browser can unload the existing page and load the new one. For the average internet connection, this process will likely take a few seconds, during which the user must wait for the new page to load.

By using a powerful frontend framework and an AJAX utility, a different model is possible: the browser can load an initial web page, but navigating to new pages will not require the browser to unload the page and load a new one. Instead, any data required for new pages can be loaded asynchronously with AJAX. From a user's perspective, such a website would appear to have pages just like any other, but from a technical perspective, this site really only has one page. Hence the name, Single-Page Application (SPA).

2『解释了 SPA 架构的概念，以及其利弊。单文件应用能够实现的前提是利用 ajax 异步与服务器交互数据。做张术语卡片。』

The advantage of the Single-Page Application architecture is that it can create a more seamless experience for the user. Data for new pages must still be retrieved, and will therefore create some small disruption to the user's flow, but this disruption is minimized since the data retrieval can be done asynchronously and JavaScript can continue to run. Also, since SPA pages usually require less data due to the reuse of some page elements, page loading is quicker.

The disadvantage of the SPA architecture is that it makes the client app bulkier due to the added functionality, so gains from speeding up page changes may be negated by the fact that the user must download a large app on the first page load. Also, handling routes adds complexity to the app as multiple states must be managed, URLs must be handled, and a lot of default browser functionality must be recreated in the app.

### 7.2 Routers

If you are going with an SPA architecture and your app design includes multiple pages, you'll want to use a router. A router, in this context, is a library that will mimic browser navigation through JavaScript and various native APIs so that the user gets an experience similar to that of a traditional multi-page app. Routers will typically include functionality to: 1) Handle navigation actions from within the page. 2) Match parts of the application to routes. 3) Manage the address bar. 4) Manage the browser history. 5) Manage scroll bar behavior.

2『路由的概念做张术语卡。』

#### 7.2.1 Vue Router

Some frontend frameworks, such as Angular or Ember, include a router library out-of-the-box. The philosophy guiding these frameworks is that the developer is better served with a complete, integrated solution for their SPA. Others frameworks/libraries, such as React and Vue.js, do not include a router. Instead, you must install a separate library.

In the case of Vue.js, an official router library is available called Vue Router. This library has been developed by the Vue.js core team, so it is optimized for usage with Vue.js and makes full use of fundamental Vue features such as components and reactivity.

With Vue Router, different pages of the application are represented by different components. When you set up Vue Router, you will pass in configuration to tell it which URLs map to which component. Then, when a link is clicked in the app, Vue Router will swap the active component so as to match the new URL, for example:

```js
let routes = [ 
    { path: '/', component: HomePage }, 
    { path: '/about', component: AboutPage }, 
    { path: '/contact', component: ContactPage } 
];
```

Since rendering a component is an almost instantaneous process in normal circumstances, the transition between pages with Vue Router is as well. However, there are asynchronous hooks that can be invoked to give you the opportunity to load new data from the server, if your different pages require it.

1『又提到异步「钩子」的重要性。』

#### 7.2.2 Special components

When you install Vue Router, two components are registered globally for use throughout your app: RouterLink and RouterView. 1) RouterLink is generally used in place of a tags and gives your links access to the special features of Vue Router. As explained, Vue Router will swap designated page components as a way of mimicking browser navigation. 2) RouterView is the outlet in which this component swap takes place. Like a slot, you put it somewhere in your main page template. For example:

```html
<div id="app"> 
    <header></header> 
    <router-view> 
        // This is where different page components display 
    </router-view> 
    <footer></footer> 
</div>
```

### 7.3 Vuebnb routing

It was never a stated goal for Vuebnb to be a single-page application. Indeed, Vuebnb will deviate from pure SPA architecture as we'll see later in the book. That said, incorporating Vue Router will be very beneficial to the user's experience of navigation in the app, so we'll add it to Vuebnb in this chapter.

Of course, if we're going to add a router, we'll need some extra pages! So far in the project, we've been working on the listing page of Vuebnb, but are yet to start work on the front page of the app. So in addition to installing Vue Router, we will start work on the Vuebnb home page, which displays thumbnails and links to all our mock listings:

#### 7.3.1 Installing Vue Router

Vue Router is an NPM package and can be installed on the command line:

    $ npm i --save-dev vue-router

3『

改用 yarn 安装。有个疑问，为啥安装成开发者依赖。

[yarn install | Yarn](https://classic.yarnpkg.com/en/docs/cli/install/)

yarn install is used to install all dependencies for a project. This is most commonly used when you have just checked out code for a project, or when another developer on the project has added a new dependency that you need to pick up.

If you are used to using npm you might be expecting to use --save or --save-dev. These have been replaced by yarn add and yarn add --dev. For more information, see the yarn add documentation.

Running yarn with no command will run yarn install, passing through any provided flags. If you need reproducible dependencies, which is usually the case with the continuous integration systems, you should pass --frozen-lockfile flag.

[yarn add | Yarn](https://classic.yarnpkg.com/en/docs/cli/add)

Installs a package and any packages that it depends on.

#### Adding dependencies

In general, a package is simply a folder with code and a package.json file that describes the contents. When you want to use another package, you first need to add it to your dependencies. This means running yarn add [package-name] to install it into your project.

This will also update your package.json and your yarn.lock so that other developers working on the project will get the same dependencies as you when they run yarn or yarn install. Most packages will be installed from the npm registry and referred to by simply their package name. For example, yarn add react will install the react package from the npm registry. You can specify versions using one of these:

```
yarn add package-name installs the “latest” version of the package.
yarn add package-name@1.2.3 installs a specific version of a package from the registry.
yarn add package-name@tag installs a specific “tag” (e.g. beta, next, or latest).
```

You can also specify packages from different locations:

```
yarn add package-name installs the package from the npm registry unless you have specified another one in your package.json.
yarn add file:/path/to/local/folder installs a package that is on your local file system. This is useful to test out other packages of yours that haven’t been published to the registry.
yarn add file:/path/to/local/tarball.tgz installs a package from a gzipped tarball which could be used to share a package before publishing it.
yarn add link:/path/to/local/folder installs a symlink to a package that is on your local file system. This is useful to develop related packages in monorepo environments.
yarn add <git remote url> installs a package from a remote git repository.
yarn add <git remote url>#<branch/commit/tag> installs a package from a remote git repository at specific git branch, git commit or git tag.
yarn add https://my-project.org/package.tgz installs a package from a remote gzipped tarball.
```

#### Caveats

If you have used a package manager like npm previously, you may be looking for how to add global dependencies. For the vast majority of packages it is considered a bad practice to have global dependencies because they are implicit. It is much better to add all of your dependencies locally so that they are explicit and anyone else using your project gets the same set of dependencies. If you are trying to use a CLI tool that has a bin you can access these in your ./node_modules/.bin directory. You can also use the global command:

    yarn global add <package...>

#### Commands

    yarn add <package...>

This will install one or more packages in your dependencies.

    yarn add <package...> [--dev/-D]

Using --dev or -D will install one or more packages in your devDependencies.

    yarn add <package...> [--peer/-P]

Using --peer or -P will install one or more packages in your peerDependencies.

    yarn add <package...> [--optional/-O]

Using --optional or -O will install one or more packages in your optionalDependencies.

    yarn add <package...> [--exact/-E]

Using --exact or -E installs the packages as exact versions. The default is to use the most recent release with the same major version. For example, yarn add foo@1.2.3 would accept version 1.9.1, but yarn add foo@1.2.3 --exact would only accept version 1.2.3.

    yarn add <package...> [--tilde/-T]

Using --tilde or -T installs the most recent release of the packages that have the same minor version. The default is to use the most recent release with the same major version. For example, yarn add foo@1.2.3 --tilde would accept 1.2.9 but not 1.3.0.

    yarn add <package...> [--ignore-workspace-root-check/-W]

Using --ignore-workspace-root-check or -W allows a package to be installed at the workspaces root. This tends not to be desired behaviour, as dependencies are generally expected to be part of a workspace. For example yarn add lerna --ignore-workspace-root-check --dev at the workspaces root would allow lerna to be used within the scripts of the root package.json.

    yarn add <alias-package>@npm:<package>

This will install a package under a custom alias. Aliasing, allows multiple versions of the same dependency to be installed, each referenced via the alias-package name given. For example, yarn add my-foo@npm:foo will install the package foo (at the latest version) in your dependencies under the specified alias my-foo. Also, yarn add my-foo@npm:foo@1.0.1 allows a specific version of foo to be installed.

    yarn add <package...> --audit

Checks for known security issues with the installed packages. A count of found issues will be added to the output. Use the yarn audit command for additional details.

』

Let's put our router configuration into a new file, router.js:

    $ touch resources/assets/js/router.js

To add Vue Router to our project, we must import the library and then use the Vue.use API method to make Vue compatible with Vue Router. This will give Vue a new configuration property, router, that we can use to connect a new router. We then create an instance of Vue Router with new VueRouter().

resources/assets/js/router.js:

```js
import Vue from 'vue'; 
import VueRouter from 'vue-router'; 
Vue.use(VueRouter); 

export default new VueRouter();
```

By exporting our router instance from this new file, we've made it into a module that can be imported in app.js. If we name the imported module router, object destructuring can be used to succinctly connect it to our main configuration object.

resources/assets/js/app.js:

```js
// import "core-js/fn/object/assign";
// window.Vue = require('vue');
import Vue from 'vue';
import ListingPage from '../components/ListingPage.vue';
import router from './router';

// Vue 实例
var vm = new Vue({
    el: "#app",
    render: h => h(ListingPage),
    // components: {ListingPage},
    router,
});

```

#### 7.3.2 Creating routes

The most basic configuration for Vue Router is to provide a routes array, which maps URLs to the corresponding page components. This array will contain objects with at least two properties: path and component.

1『核心是创建路由数组，将 URL 和组件对应起来。』

Note that by page components I'm simply referring to any components that we've designated to represent a page in our app. They are regular components in every other way. For now, we're only going to have two routes in our app, one for our home page and one for our listing page. The HomePage component doesn't exist yet, so we'll keep its route commented out until we create it.

resources/assets/js/router.js:

```js
import ListingPage from '../components/ListingPage.vue';

export default new VueRouter({ 
    mode: 'history', 
    routes: [ 
        // { path: '/', component: HomePage }, // doesn't exist yet! 
        { path: '/listing/:listing', component: ListingPage } 
    ] 
});
```

You'll notice that the path for our ListingPage component contains a dynamic segment :listing so that this route will match paths including /listing/1, listing/2 ... listing/whatever.

There are two modes for Vue Router: hash mode and history mode. Hash mode uses the URL hash to simulate a full URL so that the page won't be reloaded when the hash changes. History mode has real URLs and leverages the history.pushState API to change the URL without causing a page reload. The only downside to history mode is that URLs outside of the app, such as /some/weird/path, can't be handled by Vue and must be handled by the server. That's no problem for us, so we'll use history mode for Vuebnb.

### 7.4 App component

For our router to work, we need to declare a RouterView component somewhere in our page template. Otherwise, there's nowhere for the page components to render. We'll slightly restructure our app to do this. As it is, the ListingPage component is the root component of the app, as it is at the top of the component hierarchy and loads all other components that we use.

Since we want the router to switch between ListingPage and HomePage based on the URL, we need another component to be above ListingPage in the hierarchy and handle this work. We'll call this new root component App:

Figure 7.2. The relationship between App, ListingPage, and HomePage

1『上面的图解很形象，多看看。vue 的根实例变成了「router-view」。』

Let's create the App component file:

    $ touch resources/assets/components/App.vue

The root instance of Vue should render this to the page when it loads, instead of ListingPage.

resources/assets/js/app.js:

```js
import App from '../components/App.vue'; 
... 
var app = new Vue({ 
    el: '#app', 
    render: h => h(App), 
    router 
});
```

The following is the content of the App component. I've added the special RouterView component into the template, which is the outlet where either the HomePage or ListingPage component will render.

You'll also notice I've moved the toolbar from app.blade.php into the template of App. This is so the toolbar is in the domain of Vue; before it was outside of the mount point and therefore untouchable by Vue. I've done this so that later we can make the main logo a link to the home page using RouterLink, as this is a convention for most websites. I've moved any toolbar related CSS into the style element as well.

resources/assets/components/App.vue:

```js
<template>
    <div id="toolbar">
        <img src="{{ asset('images/logo.png') }}" class="icon">
        <h1>vuebnb</h1>
    </div>
    <router-view></router-view>
</template>

<style>
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
</style>
```

1『

这里会报错：Errors compiling template:

src="{{ asset('images/logo.png') }}": Interpolation inside attributes has been removed.

得改下模板里的：

```html
<div id="toolbar">
    <img src="/images/logo.png" class="icon">
    <h1>vuebnb</h1>
</div>
```

改完还是报错，发现最外层缺了个 div 容器，加上就好了。

```
<div>
    <div id="toolbar">
        <img src="/images/logo.png" class="icon">
        <h1>vuebnb</h1>
    </div>
    <router-view></router-view>
</div>
```

原理目前没弄明白。（2020-04-27）

』

With that done, if you now navigate the browser to a URL like /listing/1, you'll see everything looks the same as it did before. However, if you look at Vue Devtools, you'll see the component hierarchy has changed, reflecting the addition of the App component. There's also an indicator, which tells us that the ListingPage component is the active page component for Vue Router:

### 7.5 Home page

Let's start work on our home page now. We'll first create a new component, HomePage:

    $ touch resources/assets/components/HomePage.vue

For now, let's add placeholder markup to the component before we set it up properly.

resources/assets/components/HomePage.vue:

```html
<template> 
    <div>Vuebnb home page</div> 
</template>
```

Be sure to import this component in the router file, and uncomment the route where it's used.

resources/assets/js/router.js:

```js
import Vue from 'vue';
import VueRouter from 'vue-router';
import ListingPage from '../components/ListingPage.vue';
import HomePage from '../components/HomePage.vue';

Vue.use(VueRouter);

export default new VueRouter( {
    mode: 'history',
    routes: [
        {
            path: '/',
            component: HomePage
        },
        {
            path: '/listing/:listing',
            component: ListingPage
        },
    ]
});
```

You might be tempted to test this new route out by putting the URL http://vuebnb.test/ into your browser address bar. You'll find, though, that it results in a 404 error. Remember, we still haven't created a route for this on our server. Although Vue is managing routes from within the app, any address bar navigation requests must be served from Laravel.

1『

关键知识点：服务器上建路由必须通过 laravel，vue-router 只是网站内部间的路由管理。

感觉这是针对「history」模式，需要再后端设置路由，如果是 hash 模式，估计不需要，待验证。（2020-05-20）

』

Let's now create a link to our home page in the toolbar by using the RouterLink component. This component is like an enhanced a tag. For example, if you give your routes a name property, you can simply use the to prop rather than having to supply an href. Vue will resolve this to the correct URL on render.

resources/assets/components/App.vue:

```html
<template>
    <div>
        <div id="toolbar">
            <router-link :to="{name:'home'}">
                <img src="/images/logo.png" class="icon">
                <h1>vuebnb</h1>
            </router-link>
        </div>
        <router-view></router-view>
    </div>
</template>
```

Let's also add name properties to our routes for this to work.

resources/assets/js/router.js:

```js
export default new VueRouter( {
    mode: 'history',
    routes: [
        {
            path: '/',
            component: HomePage,
            name: 'home',
        },
        {
            path: '/listing/:listing',
            component: ListingPage,
            name: 'listing',
        },
    ]
});
```

We'll also have to modify our CSS now since we now have another tag wrapped around our logo. Modify the toolbar CSS rules to match those that follow.

resources/assets/components/App.vue:

```css
<style>
    #toolbar {
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

    #toolbar a {
        display: flex;
        align-items: center;
        text-decoration: none;
    }
</style>
```

Let's now open a listing page, such as /listing/1. If you inspect the DOM, you'll see that our toolbar now has a new a tag inside it with a correctly resolved link back to the home page:

Figure 7.4. The toolbar is a link back to the home page via the RouterLink element

If you click that link, you'll be taken to the home page! Remember, the page hasn't actually changed; Vue router simply swapped ListingPage for HomePage within RouterView, and also updated the browser URL via the history.pushState API:

#### 7.5.1 Home route

Let's now add a server-side route for the home page so that we can load our app from the root path. This new route will point to a get\_home\_web method in our ListingController class.

routes/web.php:

```php
<?php

Route::get('/', 'ListingController@get_home_web'); 
Route::get('/listing/{listing}', 'ListingController@get_listing_web');
```

Going to the controller now, we'll make it so the get\_home\_web method returns the app view, just as it does for the listing web route. The app view includes a template variable model which we use to pass through the initial application state, as set up in Chapter 5, Integrating Laravel and Vue.js with Webpack. For now, just assign an empty array as a placeholder.

1『加空的数据组占位，这个细节解决了开发「数据流」遇到的大问题，牢记这种思路。（2020-05-14）』

app/Http/Controllers/ListingController.php:

```php
public function get_home_web() { 
    return view('app', ['model' => []]); 
}
```

With that done, we can now navigate to http://vuebnb.test/ and it will work! When the Vue app is bootstrapped, Vue Router will check the URL value and, seeing that the path is /, will load the HomePage component inside the RouterView outlet for the first rendering of the app.

Viewing the source of this page, it's exactly the same page as we get when we load the listing route since it's the same view, that is, app.blade.php. The only difference is that the initial state is an empty array:

Figure 7.6. Page source of vuebnb.test with empty initial state

#### 7.5.2 Initial state

Just like our listing page, our home page will need initial state. Looking at the finished product, we can see that the home page displays a summary of all our mock listings with a thumbnail image, a title, and short description:

#### 7.5.3 Refactoring

Before we inject the initial state into the home page, let's do a small refactoring of the code including renaming some variables and restructuring some methods. This will ensure that the code semantics reflect the changing requirements and keep our code readable and easy to understand.

1『重构的思想出来了，微小的改动，比如重命名变量名、重构函数等。』

Firstly, let's rename our template variable from \$model to the more general \$data.

resources/views/app.blade.php:

```html
<script type="text/javascript"> window.vuebnb_server_data = "{!! addslashes(json_encode($data)) !!}" </script>
```

In our listing controller, we're now going to abstract any common logic from our listing route methods into a new helper method called get\_listing. In this helper method, we will nest the Listing model inside a Laravel Collection under the listing key. Collection is an array-like wrapper for Eloquent models that offers a bunch of handy methods that we'll be putting to use shortly. get\_listing will include logic from the add\_image\_urls helper method, which can now safely be deleted. We'll also need to reflect the change to our template variable when we call the view method.

app/Http/Controllers/ListingController.php:

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Models\ListingModel;

class ListingController extends Controller
{
    // refactoring methods
    public function get_listing($listing)
    {
        $model = $listing->toArray();
        for($i = 1; $i <=4; $i++) {
            $model['image_' . $i] = asset('images/' . $listing->id . '/Image_' . $i . '.jpg');
        }
        return collect(['listing' => $model]);
    }

    public function get_listing_api(ListingModel $listing)
    {
        $data = $this->get_listing($listing);
        return response()->json($data);
    }

    public function get_listing_web(ListingModel $listing)
    {
        $data = $this->get_listing($listing);
        return view('app', ['model' => $data]);
    }

    // home page
    public function get_home_web()
    {
        return view('app', ['data' => []]);
    }
}
```

Finally, we'll need to update our ListingPage component to reflect the new name and structure of the server data we're injecting.

resources/assets/components/ListingPage.vue:

```html
<script> let serverData = JSON.parse(window.vuebnb_server_data); 
let model = populateAmenitiesAndPrices(serverData.listing); 
... 
</script>
```

#### 7.5.4 Home page initial state

Using Eloquent ORM, it's trivial to retrieve all our listing entries using the method Listing::all. Multiple Model instances are returned by this method within a Collection object.

Note that we don't need all the fields on the model, for example, amenities, about, and so on are not used in the listing summaries that populate the home page. To ensure our data is as lean as possible, we can pass an array of fields to the Listing::all method that will tell the database to only include those fields explicitly mentioned.

app/Http/Controllers/ListingController.php:

```php
// home page
public function get_home_web()
{
    $collection = ListingModel::all([
        'id', 'address', 'title', 'price_per_night'
    ]);
    $data = collect(['listing' => $collection->toArray()]);
    return view('app', ['data' => $data]);
}
```

1『

目前首页没问题，但详细页面报错：

```
$data is undefined
Make the variable optional in the blade template. Replace {{ $data }} with {{ $data ?? '' }}

Make variable optional
```

』

### 7.6 Adding the thumbnail

Each mock listing has a thumbnail version of the first image, which can be used for the listing summary. The thumbnail is much smaller than the image we use for the header of the listing page and is ideal for the listing summaries on the home page. The URL for the thumbnail is public/images/{x}/Image\_1\_thumb.jpg where {x} is the ID of the listing.

Collection objects have a helper method, transform, that we can use to add the thumbnail image URL to each listing. transform accepts a callback closure function that is called once per item, allowing you to modify that item and return it to the collection without fuss.

2『又见到 Collection 对象，感觉很重要，larave-excel 里也用到，去研究下其具体信息。（2020-04-27）』

app/Http/Controllers/ListingController.php:

```php
// home page
public function get_home_web()
{
    $collection = ListingModel::all([
        'id', 'address', 'title', 'price_per_night'
    ]);
    // 增加 thumb 图片的 url
    $collection->transform(function($listing) {
        $listing->thumb = asset(
            'images/' . $listing->id . '/Image_1_thumb.jpg'
        );
        return $listing;
    });
    $data = collect(['listing' => $collection->toArray()]);
    return view('app', ['data' => $data]);
}
```

1『感觉又是个关键知识点，collect() 方法可以在原有的数据中额外增加字段属性。』

### 7.7 Receiving in the client

With the initial state now ready, let's add it to our HomePage component. Before we can use it though there's an additional aspect we need to consider: the listing summaries are grouped by country. Look again at Figure 7.7 to see how these groups are displayed.

After we've parsed our injected data, let's modify the object so the listings are grouped by country. We can easily create a function to do this, as every listing object has an address property in which the country is always explicitly named, for example, No. 51, Hanzhong Street, Wanhua District, Taipei City, Taiwan 108. To save you having to write this function, I have supplied one in the helpers module called groupByCountry which can be imported at the top of the component configuration.

1『

找到了 helper.js 里该函数的实现：

```js
let groupByCountry = function (listings) {
  if (!listings) return {};
  return listings.reduce(function (rv, x) {
    let key = ['Taiwan', 'Poland', 'Cuba'].find(country => x.address.indexOf(country) > -1);
    if (!rv[key]) {
      rv[key] = [];
    }
    rv[key].push(x);
    return rv;
  }, {});
};

export { groupByCountry };
```

上面的函数实现值得好好研究。

』


resources/assets/components/HomePage.vue:

```js
... 
<script> 
    import { groupByCountry } from '../js/helpers'; 
    
    let serverData = JSON.parse(window.vuebnb_server_data); 
    let listing_groups = groupByCountry(serverData.listings); 
    
    export default { 
        data() { 
            return { listing_groups } 
        } 
    } 
</script>
```

1『

发现报错说没有 reduce() 这个方法，发现传参传错了，是 serverData.listings 而非 serverData，serverData 是个对象。改完后发现获取的数据是空值，结果发现之前做数据的时候把对象里的属性名做成了「listing」而非作者的「listings」，改下即可。

serverData 是个对象这也是个关键知识点。

```
return Object.assign(serverData, {});
```

Object.assign() 函数里的第一个参数只能是个对象。

』

We'll now see through Vue Devtools that HomePage has successfully loaded the listing summaries, grouped by country and ready for display:

### 7.8 ListingSummary component

Now that the HomePage component has data available, we can work on displaying it. To begin with, clear out the existing content of the component and replace it with a div. This div will feature a v-for directive to iterate through each of our listing groups. Since listing\_groups is an object with key/value pairs, we'll give our v-for two aliases: group and country, which are the value and key of each object item respectively.

We will interpolate country inside a heading. group will be used in the next section.

resources/assets/components/HomePage.vue:

```html
<template>
    <div>
        <div v-for="(group, country) in listing_groups">
            <h1>Places in {{ country }}</h1>
        </div>
        Each listing will go here
    </div>
</template>

<script>...</script>
```

This is what the home page will now look like:

Figure 7.9. Iterating the listing summary groups in the HomePage component

Since each listing summary will be of some complexity, we'll create a separate component, ListingSummary, for displaying them:

    $ touch resources/assets/components/ListingSummary.vue

Let's declare ListingSummary within our HomePage template. We'll again use a v-for directive to iterate group, an array, creating a new instance of ListingSummary for each member. The data for each member will be bound to a single prop, listing.

resources/assets/components/HomePage.vue:

```html
<template>
    <div>
        <div v-for="(group, country) in listing_groups">
            <h1>Places in {{ country }}</h1>
            <div class="listing-summaries">
                <listing-summary v-for="listing in group" :key="listing.id"
                :listing="listing"></listing-summary>
            </div>
        </div>
    </div>
</template>

<script>
import { groupByCountry } from '../js/helpers';
import ListingSummary from './ListingSummary';

let serverData = JSON.parse(window.vuebnb_server_data);
let listing_groups = groupByCountry(serverData.listing);

export default {
    data() {
        return { listing_groups }
    },
    components: {
        ListingSummary,
    },
}
</script>
```

Let's create some simple content for the ListingSummary component, just to test our approach.

resources/assets/components/ListingSummary.vue:

```html
<template>
    <div class="listing-summary">
        {{ listing.address }}
    </div>
</template>

<script>
export default {
    props: ['listing'],
}
</script>
```

Refreshing our page, we'll now see this prototype of our listing summaries:

Figure 7.10. Prototype of ListingSummary component

Since this approach is working, let's now complete the structure of the ListingSummary component. To display the thumbnail, we bind it as a background image for a fixed width/height div. We'll also need some CSS rules to get this displaying nicely.

resources/assets/components/ListingSummary.vue:

```html
<template>
    <div class="listing-summary">
        <div class="wrapper">
            <div class="thumbnail" :style="backgroundImageStyle"></div>
            <div class="info title">
                <span>{{ listing.price_per_night }}</span>
                <span>{{ listing.title }}</span>
            </div>
            <div class="info address">{{ listing.address }}</div>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['listing'],
        computed: {
            backgroundImageStyle() {
                return {
                    'background-image': `url("${this.listing.thumb}")`
                }
            }
        },
    }
</script>

<style>
...
</style>
```

1『

```
.listing-summary .thumbnail {
    max-width: 350px;
    height: 250px;
    background-size: cover;
    background-position: center;
}
```

添加完上面代码后，图片才显示出来的。

』

We gave each listing summary a fixed width/height so that we could display them in a neat grid. Currently, they're displaying in one tall column, so let's add some CSS flex rules to the HomePage component to get the summaries into rows. We'll add a class listing-summary-group to the element that wraps the summaries. We'll also add a class home-container to the root div to constrain the width of the page and center the content.

resources/assets/components/HomePage.vue:

```js
<template>
    <div class="home-container">
        <div v-for="(group, country) in listing_groups">
            <h1>Places in {{ country }}</h1>
            <div class="listing-summaries">
                <listing-summary v-for="listing in group" :key="listing.id"
                :listing="listing"></listing-summary>
            </div>
        </div>
    </div>
</template>

<script>
    import { groupByCountry } from '../js/helpers';
    import ListingSummary from './ListingSummary';

    let serverData = JSON.parse(window.vuebnb_server_data);
    let listing_groups = groupByCountry(serverData.listing);

    export default {
        data() {
            return { listing_groups }
        },
        components: {
            ListingSummary,
        },
    }
</script>

<style>
...
</style>
```

Finally, we'll need to add a rule to prevent the listings from forcing the edge of the document to exceed the viewport. Add this to the main CSS file.

resources/assets/css/style.css:

```css
html, body { 
    overflow-x: hidden; 
}
```

You'll notice that at full page width, we can only see three listings from each country group. The other seven are hidden by the CSS overflow: hidden rule. Soon, we'll be adding image slider functionality to each group to allow the user to browse through all the listings.

3『 [overflow - CSS（层叠样式表） | MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/overflow)

CSS 属性 overflow 定义当一个元素的内容太大而无法适应「块级格式化上下文」时候该做什么。它是 overflow-x 和 overflow-y 的简写属性。

这个选项包含剪切，显示滚动条，或者显示从容器溢出到周围区域的内容。指定除 visible（默认值）以外的值将创建一个新的块级格式化上下文，这在技术层面上是必须的——如果一个浮动元素和滚动条相交，它会在每个滚动步骤后强行重新包装内容，从而导致慢滚动体验。为使 overflow 有效果，块级容器必须有一个指定的高度（height 或者 max-height）或者将 white-space 设置为 nowrap。

注意:  设置一个轴为 visible（默认值），同时设置另一个轴为不同的值，会导致设置 visible 的轴的行为会变成 auto。 即使将 overflow 设置为 hidden，也可以使用 JavaScript Element.scrollTop 属性来滚动 HTML 元素。

```css
/* 默认值。内容不会被修剪，会呈现在元素框之外 */
overflow: visible;

/* 内容会被修剪，并且其余内容不可见 */
overflow: hidden;

/* 内容会被修剪，浏览器会显示滚动条以便查看其余内容 */
overflow: scroll;

/* 由浏览器定夺，如果内容被修剪，就会显示滚动条 */
overflow: auto;

/* 规定从父元素继承overflow属性的值 */
overflow: inherit;
```

从下面列表中选出一个或两个关键字来指定 overflow 属性。如果指定了两个关键字，第一个关键字应用于 overflow-x，第二个关键字应用于 overflow-y。否则，overflow-x 和 overflow-y 都设置为相同的值。

』

### 7.9 In-app navigation

If we use the address bar of the browser to navigate to the home page, http://vuebnb.test/, it works because Laravel is now serving a page at this route. But, if we navigate to the home page from the listing page, there's no longer any page content:

We currently don't have any links to the listing page from the home page, but if we did, we'd experience a similar issue. The reason is that our page components currently get their initial state from the data we've injected into the head of the document. If we navigate to a different page using Vue Router, which doesn't invoke a page refresh, the next page component will have the wrong initial state merged in.

1『这个问题之前就发现了，目前列表页面没有数据。』

We need to improve our architecture so that when a page is navigated to we check if the model injected into the head matches the current page. To facilitate this, we'll add a path property to the model and check that it matches the active URL. If not, we'll use AJAX to get the right data from the web service:

If you're interested in reading more about this design pattern, check out the article Avoid This Common Anti-Pattern In Full-Stack Vue/Laravel Apps at [stack-ajax](https://vuejsdevelopers.com/2017/08/06/vue-js-laravel-full-stack-ajax/).

1『作者的核心思想是在每一个页面的数据对象里，添加一个 url 属性，检测数据对象是否匹配目前激活着的页面，不匹配的话再后台请求数据。不过对于逻辑简单的页面，也可以通过「v-if」选择性展示，不用跳转到另外一个页面。』

2『上面的文章作为本书的附件「附件01-Avoid-This-Common-Anti-Pattern」。』

#### 7.9.1 Adding a path to the model

Let's go to the listing controller and add a path property to the data injected into the head of our view. To do this, we'll add a helper function called add\_meta\_data which will add the path, as well as some other meta properties in later chapters.

Note that the path of the current route can be determined by the Request object. This object can be declared as the last argument of any route-handling functions and is provided in each request by the service container.

app/Http/Controllers/ListingController.php:

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Models\ListingModel;

class ListingController extends Controller
{
    // refactoring methods
    public function get_listing($listing)
    {
        $model = $listing->toArray();
        for($i = 1; $i <=4; $i++) {
            $model['image_' . $i] = asset('images/' . $listing->id . '/Image_' . $i . '.jpg');
        }
        return collect(['listing' => $model]);
    }

    // adding a path to the model
    private function add_meta_data($collection, $request) {
        return $collection->merge([
            'path' => $request->getPathInfo()
        ]);
    }

    public function get_listing_api(ListingModel $listing)
    {
        $data = $this->get_listing($listing);
        return response()->json($data);
    }

    public function get_listing_web(ListingModel $listing, Request $request)
    {
        $data = $this->get_listing($listing);
        $data = $this->add_meta_data($data, $request);
        return view('app', ['data' => $data]);
    }

    // home page
    public function get_home_web(Request $request)
    {
        $collection = ListingModel::all([
            'id', 'address', 'title', 'price_per_night'
        ]);
        // 增加 thumb 图片的 url
        $collection->transform(function($listing) {
            $listing->thumb = asset(
                'images/' . $listing->id . '/Image_1_thumb.jpg'
            );
            return $listing;
        });
        $data = collect(['listings' => $collection->toArray()]);
        $data = $this->add_meta_data($data, $request);
        return view('app', ['data' => $data]);
    }
}
```

1『

有 2 个注意点：

1、详细页里的数据跟 public function get_listing() 方法挂钩，该页面返回的数据对象里的属性名是「listing」。

2、首页里的数据跟 get_home_web() 方法挂钩，该页面返回的数据对象里的属性名是「listings」。

原来 \$request->getPathInfo() 能从前端发来的请求中获取 url 信息。

』

#### 7.9.2 Route navigation guards

Similar to lifecycle hooks, navigation guards allow you to intercept Vue Router navigations at a particular point in their life cycle. These guards can be applied to a specific component, a specific route, or to all routes. For example, afterEach is the navigation guard called after any route is navigated away from. You might use this hook to store analytics information, for example:

```js
router.afterEach((to, from) => { 
    storeAnalytics(userId, from.path); 
})
```

We can use the beforeRouteEnter navigation guard to fetch data from our web service if the data in the head is unsuitable. Consider the following pseudo-code for how we might implement this:

```js
beforeRouteEnter(to, from, next) { 
    if (to !== injectedData.path) { 
        getDataWithAjax.then(data => { 
            applyData(data) 
        }) 
        } else { 
            applyData(injectedData) 
        } 
    next() 
}
```

#### 7.9.3 next

An important feature of navigation guards is that they will halt navigation until the next function is called. This allows asynchronous code to be executed before the navigation is resolved:

```js
beforeRouteEnter(to, from, next) { 
    new Promise(...).then(() => { 
        next(); 
    }); 
}
```

1『明 beforeRouteEnter 是个迭代器。』

You can pass false to the next function to prevent a navigation, or you can pass a different route to redirect it. If you don't pass anything, the navigation is considered confirmed. The beforeRouteEnter guard is a special case. Firstly, this is undefined within it since it is called before the next page component has been created:

```js
beforeRouteEnter(to, from, next) { 
    console.log(this); // undefined 
}
```

However, the next function in beforeRouteEnter can accept a callback function as an argument, for example, next(component => { ... }); where component is the page component instance. This callback is not triggered until the route is confirmed and the component instance has been created. Due to how JavaScript closures work, the callback will have access to the scope of the surrounding code where it was called:

```js
beforeRouteEnter(to, from, next) { 
    var data = { ... } 
    next(component => { 
        component.$data = data; 
    }); 
}
```

1『 next() 里传入回调函数这个用法妙，可惜目前没有完全吃透，不清楚具体在哪些场景下使用。（2020-05-22）』

### 7.10 HomePage component

Let's add beforeRouteEnter to the HomePage component. Firstly, move any logic for retrieving data from the document head into the hook. We then check the path property of the data to see if it matches the current route. If so, we call next and pass a callback function that applies the data to the component's instance. If not, we'll need to use AJAX to get the right data.

resources/assets/components/HomePage.vue:

```js
<script>
    import { groupByCountry } from '../js/helpers';
    import ListingSummary from './ListingSummary';

    export default {
        data() {
            return { 
                listing_groups: [],
            };
        },
        components: {
            ListingSummary,
        },
        beforeRouteEnter(to, from, next) {
            let serverData = JSON.parse(window.vuebnb_server_data);
            if (to.path === serverData.path) {
                let listing_groups = groupByCountry(serverData.listings);
                next(component => component.listing_groups = listing_groups);
            } else {
                console.log('Need to get data with AJAX!');
                next(false);
            }
        },
    }
</script>
```

I've added listing\_groups as a data property. Before, we were applying our data to the component instance as it was created. Now, we're applying the data after the component is created. To set up reactive data, Vue must know the names of the data properties, so we initialize with an empty value and update it when the data needed is available.

1『这里注意一点，listing_groups 声明一个空数组占坑。』

#### 7.10.1 Home API endpoint

We'll now implement the AJAX functionality. Before we do, though, we need to add a home page endpoint to our web service. Let's first add the home API route.

routes/api.php:

```php
...

Route::get('/', 'ListingController@get_home_api');
```

Looking now at the ListingController class, we'll abstract the bulk of the logic from get\_home\_web into a new function, get\_listing\_summaries. We'll then use this function in the get\_home\_api method and return a JSON response.

app/Http/Controllers/ListingController.php:

```php
private function get_listing_summaries() {
    $collection = ListingModel::all([
        'id', 'address', 'title', 'price_per_night'
    ]);
    // 增加 thumb 图片的 url
    $collection->transform(function($listing) {
        $listing->thumb = asset(
            'images/' . $listing->id . '/Image_1_thumb.jpg'
        );
        return $listing;
    });
    return collect(['listings' => $collection->toArray()]);
}

// home page
public function get_home_web(Request $request)
{
    $data = $this->get_listing_summaries();
    $data = $this->add_meta_data($data, $request);
    return view('app', ['data' => $data]);
}

// home api endpoint
public function get_home_api() {
    $data = $this->get_listing_summaries();
    return response()->json($data);
}
```

#### 7.10.2 Axios

To perform AJAX requests to the web service, we'll use the Axios HTTP client, which is included with Laravel's default frontend code. Axios has a very simple API allowing us to make requests to a GET URL like this:

```js
axios.get('/my-url');
```

Axios is a Promise-based library, so in order to retrieve the response, you can simply chain a then callback:

```js
axios.get('/my-url').then(response => { 
    console.log(response.data); // Hello from my-url 
});
```

As the Axios NPM package is already installed, we can go ahead and import the HomePage component. We can then use it to perform the request to the home API endpoint, /api/. In the then callback, we apply the returned data to the component instance exactly as we did with the inlined model.

resources/assets/components/HomePage.vue:

```js
<script>
    import { groupByCountry } from '../js/helpers';
    import ListingSummary from './ListingSummary';
    import axios from 'axios';

    export default {
        data() {
            return { 
                listing_groups: [],
            };
        },
        components: {
            ListingSummary,
        },
        beforeRouteEnter(to, from, next) {
            let serverData = JSON.parse(window.vuebnb_server_data);
            if (to.path === serverData.path) {
                let listing_groups = groupByCountry(serverData.listings);
                next(component => component.listing_groups = listing_groups);
            } else {
                console.log('Need to get data with AJAX!');
                axios.get(`api`).then(({data}) => {
                    let listing_groups = groupByCountry(data.listings);
                    next(component => component.listing_groups = listing_groups);
                })
            }
        },
    }
</script>
```

And with that, we can now navigate to the home page in two ways, either via the address bar, or by going from a link from the listing page. Either way, we get the right data!

### 7.11 Mixins

If you have any functionality that is common between components, you can put it in a mixin to avoid rewriting the same functionality. A Vue mixin is an object in the same form as a component configuration object. To use it in a component, declare within an array and assign it to the configuration property mixin. When this component is instantiated, any configuration options of the mixin will be merged with what you've declared on the component:

1『原来 mixins 是用来解决组件之间公共函数库的。它可以分发 Vue 组件中的可复用功能。一个混入对象可以包含任意组件选项。当组件使用混入对象时，所有混入对象的选项将被「混合」进入该组件本身的选项。』

```js
var mixin = { 
    methods: { 
        commonMethod() { 
            console.log('common method'); 
        } 
    } 
}; 

Vue.component('a', { 
    mixins: [ mixin ] 
}); 

Vue.component('b', { 
    mixins: [ mixin ] 
    methods: { 
        otherMethod() { ... } 
    } 
});
```

You might be wondering what happens if the component configuration has a method or other property that conflicts with the mixin. The answer is that mixins have a merging strategy that determines the priority of any conflicts. Generally, the component's specified configuration will take precedence. The details of the merging strategy are explained in the Vue.js documentation at http://vuejs.org.

3『 [混入 — Vue.js](https://cn.vuejs.org/v2/guide/mixins.html#%E5%9F%BA%E7%A1%80)

#### 1.1 基础

混入 (mixin) 提供了一种非常灵活的方式，来分发 Vue 组件中的可复用功能。一个混入对象可以包含任意组件选项。当组件使用混入对象时，所有混入对象的选项将被“混合”进入该组件本身的选项。

例子：

```js
// 定义一个混入对象
var myMixin = {
  created: function () {
    this.hello()
  },
  methods: {
    hello: function () {
      console.log('hello from mixin!')
    }
  }
}

// 定义一个使用混入对象的组件
var Component = Vue.extend({
  mixins: [myMixin]
})

var component = new Component() // => "hello from mixin!"
```

#### 1.2 选项合并

当组件和混入对象含有同名选项时，这些选项将以恰当的方式进行「合并」。比如，数据对象在内部会进行递归合并，并在发生冲突时以组件数据优先。

```js
var mixin = {
  data: function () {
    return {
      message: 'hello',
      foo: 'abc'
    }
  }
}

new Vue({
  mixins: [mixin],
  data: function () {
    return {
      message: 'goodbye',
      bar: 'def'
    }
  },
  created: function () {
    console.log(this.$data)
    // => { message: "goodbye", foo: "abc", bar: "def" }
  }
})
```

同名钩子函数将合并为一个数组，因此都将被调用。另外，混入对象的钩子将在组件自身钩子之前调用。

```js
var mixin = {
  created: function () {
    console.log('混入对象的钩子被调用')
  }
}

new Vue({
  mixins: [mixin],
  created: function () {
    console.log('组件钩子被调用')
  }
})

// => "混入对象的钩子被调用"
// => "组件钩子被调用"
```

值为对象的选项，例如 methods、components 和 directives，将被合并为同一个对象。两个对象键名冲突时，取组件对象的键值对。

```js
var mixin = {
  methods: {
    foo: function () {
      console.log('foo')
    },
    conflicting: function () {
      console.log('from mixin')
    }
  }
}

var vm = new Vue({
  mixins: [mixin],
  methods: {
    bar: function () {
      console.log('bar')
    },
    conflicting: function () {
      console.log('from self')
    }
  }
})

vm.foo() // => "foo"
vm.bar() // => "bar"
vm.conflicting() // => "from self"
```

注意：Vue.extend() 也使用同样的策略进行合并。

#### 1.3 全局混入

混入也可以进行全局注册。使用时格外小心！一旦使用全局混入，它将影响每一个之后创建的 Vue 实例。使用恰当时，这可以用来为自定义选项注入处理逻辑。

```js
// 为自定义的选项 'myOption' 注入一个处理器。
Vue.mixin({
  created: function () {
    var myOption = this.$options.myOption
    if (myOption) {
      console.log(myOption)
    }
  }
})

new Vue({
  myOption: 'hello!'
})
// => "hello!"
```

请谨慎使用全局混入，因为它会影响每个单独创建的 Vue 实例（包括第三方组件）。大多数情况下，只应当应用于自定义选项，就像上面示例一样。推荐将其作为插件发布，以避免重复应用混入。

』

#### 7.11.1 Moving the solution to a mixin

Let's generalize the solution for getting the right data to the home page so that we can use it on the listing page as well. To do this, we'll move Axios and the beforeRouteEnter hook from the HomePage component into a mixin that can then be added to both page components:

    $ touch resources/assets/js/route-mixin.js

At the same time, let's improve the code by removing the repetition of the next function call. To do this, we'll create a new method, getData, which will be responsible for figuring out where to get the right data for the page and also for getting it. Note that this method will be asynchronous since it may need to wait for AJAX to resolve, so it will return a Promise rather than an actual value. This Promise is then resolved within the navigation guard.

resources/assets/js/route-mixin.js:

```js
import axios from 'axios';

function getData(to) {
    return new Promise((resolve) => {
        let serverData = JSON.parse(window.vuebnb_server_data);
        if (!serverData.path || to.path !== serverData.path) {
            axios.get(`api${to.path}`).then(({data}) => {
                resolve(data);
            })
        } else {
            resolve(serverData);
        }
    });
}

export default {
    beforeRouteEnter: (to, from, next) => {
        getData(to).then((data) => {
            next(component => component.assignData(data));
        });
    }
};
```

We don't need a polyfill for Promise as that is already supplied in the Axios library.

#### 7.11.2 assignData

You'll notice that within the next callback we call a method on the subject component called assignData, passing the data object as an argument. We'll need to implement the assignData method in any component that uses this mixin. We do it this way so that the component can process the data, if necessary, before it is applied to the component instance. For example, the ListingPage component must process the data via the populateAmenitiesAndPrices helper function.

resources/assets/components/ListingPage.vue:

```js
<script>
    import { populateAmenitiesAndPrices } from '../js/helpers';
    import ImageCarousel from './ImageCarousel.vue';
    import ModalWindow from './ModalWindow.vue';
    import HeaderImage from './HeaderImage.vue';
    import FeatureList from './FeatureList.vue';
    import ExpandableText from './ExpandableText.vue';
    import routeMixin from '../js/route-mixin';

    export default {
        mixins: [routeMixin],
        data() {
            return {
                title: null,
                about: null,
                address: null,
                amenities: [],
                prices: [],
                images: [],
            }
        },
        components: { 
            ImageCarousel,
            ModalWindow,
            HeaderImage,
            FeatureList,
            ExpandableText,
        },
        methods: {
            assignData({listing}) {
                Object.assign(this.$data, populateAmenitiesAndPrices(listing));
            },
            openModal() {
                this.$refs.imagemodal.modalOpen = true;
            },
        },
}
</script>
```

We'll also need to add assignData to the HomePage component.

resources/assets/components/HomePage.vue:

```js
<script>
    import { groupByCountry } from '../js/helpers';
    import ListingSummary from './ListingSummary';
    import axios from 'axios';
    import routeMixin from '../js/route-mixin';

    export default {
        mixins: [routeMixin],
        data() {
            return { 
                listing_groups: [],
            };
        },
        methods: {
            assignData({listings}) {
                this.listing_groups = groupByCountry(listings);
            }
        },
        components: {
            ListingSummary,
        },
    }
</script>
```

#### 7.11.3 Linking to the listing page

The above should work but we can't test it since there are not yet any in-app links to the listing page!

Each of our ListingSummary instances represents a single listing, and should therefore be a clickable link to the page for that listing. Let's use the RouterLink component to achieve this. Note that the object we bind to the to prop includes the name of the route as well as a params object which includes a value for the dynamic segment of the route, the listing ID.

resources/assets/components/ListingSummary.vue:

```html
<template>
    <div class="listing-summary">
        <router-link :to="{name:'listing', params:{listing:listing.id}}">
            <div class="wrapper">
                <div class="thumbnail" :style="backgroundImageStyle"></div>
                <div class="info title">
                    <span>{{ listing.price_per_night }}</span>
                    <span>{{ listing.title }}</span>
                </div>
                <div class="info address">{{ listing.address }}</div>
            </div>
        </router-link>
    </div>
</template>
```

1『

发现详细页面没数据，报错：

http://localhost:8000/listing/api/listing/1 404 (Not Found)

可以看出请求的数据出问题了，路由的名字错了，api 应该在 listing 前面。推理出问题应该在路由上，最后找到（route-mixin.js）：

```js
axios.get(`api${to.path}`).then(({data}) => {
    resolve(data);
})
```

应该是：

```js
axios.get(`/api${to.path}`).then(({data}) => {
    resolve(data);
})
```

少了个 /，魔鬼在细节。

弄错了，关键不是少了 /，关键是前面的 === 应该是 ！===，有没有 / 没有啥影响。

```js
if (!serverData.path || to.path !== serverData.path) {
    axios.get(`api${to.path}`).then(({data}) => {
        resolve(data);
    })
```

』

With that done, the listing summaries will now be links. Clicking from one to the listing page, we see this:

Figure 7.15. Successful AJAX call after navigating to listing page

We can see in Figure 7.15 that the AJAX call to the listing API was successful and returned the data we wanted. If we also look at the Vue Devtools tab, as well as the Dev Tools console, we can see the correct data in our component instance. The problem is that we now have an unhandled 404 error for the header image:

Figure 7.16. Dev Tools console showing error

The reason for this is that the component's first render occurs before the callback in the next hook is called. This means that the initialization values for the component data are used in the first render.

resources/assets/components/ListingPage.vue:

```js
data() { 
    return { 
        title: null, 
        about: null, 
        address: null, 
        amenities: [], 
        prices: [], 
        images: [] 
    } 
},
```

In the HeaderImage declaration, we bind the first image like this: :image-url="images[0]". Since the array is initially empty, this will be an undefined value and results in the unhandled error. The explanation is complex, but the fix is easy: just add a v-if to header-image, ensuring it won't render until valid data is available.

resources/assets/components/ListingPage.vue:

```html
    <header-image v-if="images[0]" 
    :image-url="images[0]" 
    @header-clicked="openModal"></header-image>
```

1『这个解决思路很好，应该可以应用到其他场景。（2020-05-22）』

### 7.12 Scroll behavior

Another aspect of website navigation that the browser automatically manages is scroll behavior. For example, if you scroll to the bottom of a page, then navigate to a new page, the scroll position is reset. But if you return to the previous page, the scroll position is remembered by the browser, and you're taken back to the bottom.

The browser can't do this when we've hijacked navigation with Vue Router. So, when you scroll to the bottom of the Vuebnb home page and click a listing in Cuba, let's say, the scroll position is unchanged when the listing page component is loaded. This feels really unnatural to the user, who would expect to be taken to the top of the new page:

Figure 7.17. Scroll position issue after navigating with Vue Router

Vue Router has a scrollbehavior method that allows you to adjust where the page is scrolled when you change routes by simply defining the x and y positions of the horizontal and vertical scroll bars. To keep it simple, and yet to still keep the UX natural, let's make it so we are always at the top of the page when a new page is loaded.

resources/assets/js/router.js:

```js
export default new VueRouter({ 
    mode: 'history', 
    routes: [ ... ], 
    scrollBehavior (to, from, savedPosition) { 
        return { x: 0, y: 0 } 
    } 
});
```

### 7.13 Adding a footer

To improve the design of Vuebnb, let's add a footer to the bottom of each page. We'll make it a reusable component, so let's begin by creating that:

    $ touch resources/assets/components/CustomFooter.vue

Here is the markup. For now, it's just a stateless component.

resources/assets/js/CustomFooter.vue:

```html
<template>
    <div id="footer">
        <div class="container">
            <p>
                <img src="/images/logo_grey.png" class="icon">
                <span>
                    <strong>Vuebnb</strong>. A full-stack Vue.js and Laravel demo app
                </span>
            </p>
        </div>
    </div>
</template>

<style>
...
</style>
```

Let's add the footer to the App component, just below the RouterView where the pages are output.

resources/assets/js/App.vue:

```html
<template>
    <div>
        <div id="toolbar">
            <router-link :to="{name:'home'}">
                <img src="/images/logo.png" class="icon">
                <h1>vuebnb</h1>
            </router-link>
        </div>
        <router-view></router-view>
        <custom-footer></custom-footer>
    </div>
</template>

<script>
import CustomFooter from './CustomFooter';
export default {
    components: {
        CustomFooter,
    }
}
</script>
```

Here's how it looks on the listing page:

Now here's how it looks on the home page. It doesn't look as good because the text is not aligned left as you'd expect. This is because the container constraints used on this page are different to the .container class we've added to the footer:

1『详细页面里排版可以，但首页里的这个版本就比较乱。』

In fact, .container was specifically designed for the listing page, while .home-container was designed for the home page. To fix this, and to make things less confusing, let's firstly rename the .container class to .listing-container. You'll also need to update the ListingPage component to ensure it's using this new class name. Secondly, let's move .home-container to the main CSS file as well, since we'll start to use it globally as well.

Now we have .home-container and .listing-container as two possible containers for our custom-footer component. Let's dynamically select the class depending on the route, so the footer is always correctly aligned.

1『这是不是就是样式的全局污染问题，element-admin 作者提到的用 scope style 可以解决，此信息点待验证。（2020-05-22）』

#### 7.13.1 The route object

The route object represents the state of the currently active route and can be accessed inside the root instance, or a component instance, as this.\$route. This object contains parsed information of the current URL and the route records matched by the URL:

```js
created() { 
    console.log(this.$route.fullPath); // /listing/1 
    console.log(this.$route.params); // { listing: "1" } 
}
```

#### 7.13.2 Dynamically selecting the container class

In order to select the correct container class in custom-footer, we can get the name of the current route from the route object, and use that in a template literal.

resources/assets/components/CustomFooter.vue:

```js
<template>
    <div id="footer">
        <div class="hr"></div>
        <div :class="containerClass">
            <p>
                <img src="/images/logo_grey.png" class="icon">
                <span>
                    <strong>Vuebnb</strong>. A full-stack Vue.js and Laravel demo app
                </span>
            </p>
        </div>
    </div>
</template>

<script>
export default {
    computed: {
        containerClass() {
            // this.$route.name is either 'home' or 'listing'
            return `${this.$route.name}-container`;
        }
    },
}
</script>
```

Now the footer will use .home-container when displayed on the home page:

1『用 this.\$route.name 可以获得当前页面的路由名称。』

### 7.14 Listing summary image slider

On our home page, we need to make it so that a user can see more than just three of the possible 10 listings for each country. To do this, we will turn each listing summary group into an image slider. Let's create a new component to house each listing summary group. We'll then add arrowheads to the sides of this component, allowing the user to easily step through its listings:

    $ touch resources/assets/components/ListingSummaryGroup.vue

We'll now abstract the markup and logic for displaying listing summaries from HomePage into this new component. Each group will need to know the name of the country and the included listings, so we'll add this data as props.

resources/assets/components/ListingSummaryGroup.vue:

```js
<template>
    <div class="listing-summary-group">
        <h1>Places in {{ country }}</h1>
        <div class="listing-summaries">
            <listing-summary 
            v-for="listing in listings"
            :key="listing.id"
            :listing="listing"></listing-summary>
        </div>
    </div>
</template>

<script>
    import ListingSummary from './ListingSummary.vue';
    export default {
        props: ['country', 'listings'],
        components: {
            ListingSummary,
        },
    }
</script>

<style>
...
</style>
```

Back in the HomePage, we will declare the ListingSummaryGroup with a v-for, iterating over each country group.

resources/assets/components/HomePage.vue:

```js
<template>
    <div class="home-container">
        <listing-summary-group 
        v-for="(group, country) in listing_groups"
        :key="country"
        :listings="group"
        :country="country"
        class="listing-summary-group">
        </listing-summary-group>
    </div>
</template>

<script>
    import { groupByCountry } from '../js/helpers';
    import routeMixin from '../js/route-mixin';
    import ListingSummaryGroup from './ListingSummaryGroup.vue';

    export default {
        mixins: [routeMixin],
        data() {
            return { 
                listing_groups: [],
            };
        },
        methods: {
            assignData({listings}) {
                this.listing_groups = groupByCountry(listings);
            }
        },
        components: {
            ListingSummaryGroup,
        },
    }
</script>
```

Most developers will use the terms image carousel and image slider interchangeably. In this book, I make a slight distinction, a carousel contains a single image that gets completely switched out with another, while a slider shifts the position of images, with several visible at once.

1『

报错，说找不到组件 ListingSummary，找的是找了很久，看了一遍又一遍，最后是发现在 ListingSummaryGroup 里注册 ListingSummary 组件时，少打了一个 s。

```
// 漏掉了组件后面的 s，应该是 components
component: {
    ListingSummary,
},
```

细节细节细节！

』

#### 7.14.1 Adding the slider

We'll now add the slider functionality to ListingSummaryGroup. To do this, we'll reuse the CarouselControl component we made back in Chapter 6, Composing Widgets with Vue.js Components. We'll want to display one on either side of the group, so let's put them into the template, remembering to declare the dir attribute. We'll also add some structural markup and CSS for displaying the controls.

resources/assets/components/ListingSummaryGroup.vue:

```js
<template>
    <div class="listing-summary-group">
        <h1>Places in {{ country }}</h1>
        <div class="listing-carousel">
            <div class="controls">
                <carousel-control dir="left"></carousel-control>
                <carousel-control dir="right"></carousel-control>
            </div>
            <div class="listing-summaries-wrapper">
                <div class="listing-summaries">
                    <listing-summary 
                    v-for="listing in listings"
                    :key="listing.id"
                    :listing="listing"></listing-summary>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import ListingSummary from './ListingSummary.vue';
    import CarouselControl from './CarouselControl';
    export default {
        props: ['country', 'listings'],
        components: {
            ListingSummary,
            CarouselControl,
        },
    }
</script>
```

#### 7.14.2 Translate

In order to shift our listing summaries in response to the carousel controls being clicked, we will use a CSS transform called translate. This moves an affected element from its current position by an amount specified in pixels.

The total width of each listing summary is 365px (350px fixed width plus 15px margin). This means if we move our group to the left by 365px, it will give the effect of shifting the position of all images by one. You can see here I've added the translate as inline styling to test if it works. Note that we translate in a negative direction to get the group to move to the left:

By binding inline style to the element with the listing-summary class, we can control the translate from JavaScript. Let's do this via a computed property so we can calculate the translate amount dynamically.

resources/assets/components/ListingSummaryGroup.vue:

```js
<script>
    import ListingSummary from './ListingSummary.vue';
    import CarouselControl from './CarouselControl';
    export default {
        props: ['country', 'listings'],
        computed: {
            style() {
                return {transform: `translateX(-365px)`}
            }
        },
        components: {
            ListingSummary,
            CarouselControl,
        },
    }
</script>
```

Now all of our summary groups will be shifted:

The problem evident in Figure 7.23 is that we can only see three images at once and that they're overflowing out of the container into the other parts of the page. To fix this, we'll move the CSS rule overflow: hidden from listing-summaries to listing-summaries-wrapper.

resources/assets/components/ListingSummaryGroup.vue:

```css
... 

.listing-summaries-wrapper { 
    overflow: hidden; 
} 

.listing-summaries { 
    display: flex; 
    flex-direction: row; 
    justify-content: space-between; 
} 

...
```

#### 7.14.3 Carousel controls

We now need the carousel controls to change the value of the translate. To do so, let's add a data property, offset, to ListingSummaryGroup. This will track how many images we've shifted along, that is, it will start at zero, and go up to a maximum of seven (not 10 because we don't want to shift so far along that all of the images are off-screen).

We'll also add a method change, which will serve as an event handling function for the custom event that the carousel control components emit. This method accepts one argument, val, which will either be -1 or 1, depending on whether the left or right carousel control was triggered. change will step the value of offset, which is then multiplied by the width of each listing (365px) to calculate the translate.

resources/assets/components/ListingSummaryGroup.vue:

```js
const rowSize = 3;
const listingSummaryWidth = 365;

export default {
    props: ['country', 'listings'],
    data() {
        return {
            offset:0
        }
    },
    methods: {
        change(val) {
            let newVal = this.offset + parseInt(val);
            if (newVal >= 0 && newVal <= this.listings.length-rowSize) {
                this.offset = newVal;
            }
        }
    },
    computed: {
        style() {
            return {
                transform: `translateX(${this.offset *- listingSummaryWidth}px)`
            }
        }
    },
    components: {
        ListingSummary,
        CarouselControl,
    },
}
```

Lastly, we must use a v-on directive in the template to register a listener for the change-image event of the CarouselControl components.

resources/assets/components/ListingSummaryGroup.vue:

```html
<div class="controls">
    <carousel-control dir="left" @change-image="change"></carousel-control>
    <carousel-control dir="right" @change-image="change"></carousel-control>
</div>
```

With that done, we have a working image slider for each listing group!

#### 7.14.4 Finishing touches

There are two more small features to add to these image sliders to give Vuebnb users the best possible experience. Firstly, let's add a CSS transition to animate the translate change over a period of half a second and give a nice sliding effect.

resources/assets/components/ListingSummaryGroup.vue:

```css
.listing-summaries { 
    display: flex; 
    flex-direction: row; 
    justify-content: space-between; 
    transition: transform 0.5s; 
}
```

Sadly you can't see the effects of this in a book, so you'll have to try it for yourself! 

Finally, unlike our image carousel, these sliders are not continuous; they have a minimum and maximum value. Let's hide the appropriate arrow if that minimum or maximum is reached. For example, when the sliders load, the left arrow should be hidden because the user cannot decrement the offset further below zero. To do this, we'll use style bindings to dynamically add a visibility: hidden CSS rule.

resources/assets/components/ListingSummaryGroup.vue:

```js
<div class="controls">
    <carousel-control 
    dir="left" 
    @change-image="change"
    :style="leftArrowStyle"></carousel-control>
    <carousel-control 
    dir="right" 
    @change-image="change"
    :style="rightArrowStyle"></carousel-control>
</div>
```

And the computed properties.

resources/assets/components/ListingSummaryGroup.vue:

```js
computed: {
    style() {
        return {
            transform: `translateX(${this.offset *- listingSummaryWidth}px)`
        }
    },
    leftArrowStyle() {
        return { visibility: (this.offset > 0 ? 'visible' : 'hidden') }
    },
    rightArrowStyle() {
        return {
            visibility: (
                this.offset < (this.listings.length - rowSize) ? 'visible' : 'hidden'
            )
        }
    },
},
```